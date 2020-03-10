---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート 3 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET MV... でエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433216"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="ee2de-103">ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート3</span><span class="sxs-lookup"><span data-stu-id="ee2de-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="ee2de-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ee2de-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="ee2de-105">このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="ee2de-106">複合型の使用</span><span class="sxs-lookup"><span data-stu-id="ee2de-106">Working with Complex Types</span></span>

<span data-ttu-id="ee2de-107">このセクションでは、アドレスクラスを作成し、テンプレートを表示するためのテンプレートを作成する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="ee2de-108">[*モデル*] フォルダーで、 *Person.cs*という名前の新しいクラスファイルを作成します。ここで、`Person` クラスと `Address` クラスの2つの型を指定します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="ee2de-109">`Person` クラスには、`Address`として型指定されたプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="ee2de-110">`Address` 型は複合型です。つまり、`int`、`string`、`double`などの組み込み型の1つではありません。</span><span class="sxs-lookup"><span data-stu-id="ee2de-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="ee2de-111">代わりに、いくつかのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="ee2de-111">Instead, it has several properties.</span></span> <span data-ttu-id="ee2de-112">新しいクラスのコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ee2de-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="ee2de-113">`Movie` コントローラーで、person インスタンスを表示するには、次の `PersonDetail` アクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="ee2de-114">次に、`Movie` コントローラーに次のコードを追加して、`Person` モデルにいくつかのサンプルデータを設定します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="ee2de-115">*Views\Movies\PersonDetail.cshtml*ファイルを開き、`PersonDetail` ビューの次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="ee2de-116">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行し、[*ムービー/個人情報*] に移動します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="ee2de-117">このスクリーンショットに示すように、`PersonDetail` ビューには複合型 `Address` が含まれていません。</span><span class="sxs-lookup"><span data-stu-id="ee2de-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="ee2de-118">(アドレスは表示されません)。</span><span class="sxs-lookup"><span data-stu-id="ee2de-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="ee2de-119">`Address` モデルデータは、複合型であるため表示されません。</span><span class="sxs-lookup"><span data-stu-id="ee2de-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="ee2de-120">アドレス情報を表示するには、 *Views\Movies\PersonDetail.cshtml*ファイルをもう一度開き、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="ee2de-121">`PersonDetail` ビューの完全なマークアップは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ee2de-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="ee2de-122">アプリケーションをもう一度実行し、[`PersonDetail`] ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="ee2de-123">アドレス情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="ee2de-124">複合型のテンプレートの作成</span><span class="sxs-lookup"><span data-stu-id="ee2de-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="ee2de-125">このセクションでは、`Address` 複合型をレンダリングするために使用するテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="ee2de-126">`Address` の種類のテンプレートを作成すると、ASP.NET MVC は自動的にそのテンプレートを使用して、アプリケーション内の任意の場所でアドレスモデルの書式を設定できます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="ee2de-127">これにより、アプリケーション内の1つの場所から `Address` 型のレンダリングを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="ee2de-128">*Views\Shared\DisplayTemplates*フォルダーで、厳密に型指定された**Address**という名前の部分ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="ee2de-129">**[追加]** をクリックし、新しい*Views\Shared\DisplayTemplates\Address.cshtml*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="ee2de-130">新しいビューには、次の生成されたマークアップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ee2de-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="ee2de-131">アプリケーションを実行し、[`PersonDetail`] ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="ee2de-132">今回は、先ほど作成した `Address` テンプレートを使用して `Address` 複合型が表示されるため、表示は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ee2de-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="ee2de-133">まとめ: モデルの表示形式とテンプレートを指定する方法</span><span class="sxs-lookup"><span data-stu-id="ee2de-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="ee2de-134">モデルプロパティの形式またはテンプレートを指定するには、次の方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="ee2de-135">モデルのプロパティに `DisplayFormat` 属性を適用します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="ee2de-136">たとえば、次のコードでは、日付が時刻なしで表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="ee2de-137">データ型を指定して、モデル内のプロパティに[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性を適用します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="ee2de-138">たとえば、次のコードでは、日付が時刻なしで表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="ee2de-139">アプリケーションに*Views\Shared\DisplayTemplates*フォルダーまたは*Views\Movies\DisplayTemplates*フォルダー内に*日付の cshtml*テンプレートが含まれている場合、そのテンプレートを使用して `DateTime` プロパティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="ee2de-140">それ以外の場合は、組み込みの ASP.NET テンプレートシステムによって、プロパティが日付として表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee2de-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="ee2de-141">*Views\Shared\DisplayTemplates*フォルダーまたは*Views\Movies\DisplayTemplates*フォルダーで、書式設定するデータ型と一致する名前を持つ表示テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="ee2de-142">たとえば、モデルに属性を追加したり、ビューにマークアップを追加しなくても、 *Views\Shared\DisplayTemplates\DateTime.cshtml*を使用してモデル内の `DateTime` プロパティを表示したことがわかります。</span><span class="sxs-lookup"><span data-stu-id="ee2de-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="ee2de-143">モデルの[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を使用して、モデルのプロパティを表示するテンプレートを指定します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="ee2de-144">表示テンプレート名をビューの[Html. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)呼び出しに明示的に追加します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="ee2de-145">使用する方法は、アプリケーションで何を行う必要があるかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="ee2de-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="ee2de-146">これらの方法を組み合わせて、必要な書式設定の種類を正確に取得することは珍しくありません。</span><span class="sxs-lookup"><span data-stu-id="ee2de-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="ee2de-147">次のセクションでは、1ビットの歯車を切り替え、データの表示方法をカスタマイズして入力方法をカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="ee2de-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="ee2de-148">JQuery datepicker をアプリケーションの編集ビューにフックして、日付を指定するための洗練された方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="ee2de-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ee2de-149">[前へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [次へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="ee2de-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
