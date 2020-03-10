---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート 2 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET MV... でエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498418"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="77eee-103">ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート2</span><span class="sxs-lookup"><span data-stu-id="77eee-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>

<span data-ttu-id="77eee-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="77eee-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="77eee-105">このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="77eee-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="77eee-106">自動 DateTime テンプレートの追加</span><span class="sxs-lookup"><span data-stu-id="77eee-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="77eee-107">このチュートリアルの最初の部分では、モデルに属性を追加して書式を明示的に指定する方法と、モデルの表示に使用するテンプレートを明示的に指定する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="77eee-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="77eee-108">たとえば、次のコードの[Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性は、`ReleaseDate` プロパティの書式を明示的に指定します。</span><span class="sxs-lookup"><span data-stu-id="77eee-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicitly specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="77eee-109">次の例では、 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性を使用して、`Date` 列挙型を使用して、日付テンプレートを使用してモデルを表示するように指定しています。</span><span class="sxs-lookup"><span data-stu-id="77eee-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="77eee-110">プロジェクトに日付テンプレートがない場合は、組み込みの日付テンプレートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="77eee-111">ただし、ASP。MVC では、型の名前と一致するテンプレートを検索することで、構成上の規則を使用して型の照合を実行できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="77eee-112">これにより、属性やコードをまったく使用せずにデータを自動的に書式設定するテンプレートを作成できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="77eee-113">このチュートリアルのパートでは、 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)型のモデルプロパティに自動的に適用されるテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="77eee-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="77eee-114">属性またはその他の構成を使用して、 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)型のすべてのモデルプロパティを表示するためにテンプレートを使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="77eee-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="77eee-115">また、個々のプロパティや個々のフィールドの表示をカスタマイズする方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="77eee-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="77eee-116">まず、既存の書式設定情報を削除して、アプリケーションに完全な日付を表示してみましょう。</span><span class="sxs-lookup"><span data-stu-id="77eee-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="77eee-117">*Movie.cs*ファイルを開き、`ReleaseDate` プロパティの `DataType` 属性をコメントアウトします。</span><span class="sxs-lookup"><span data-stu-id="77eee-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="77eee-118">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="77eee-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="77eee-119">`ReleaseDate` プロパティには、日付と時刻の両方が表示されることに注意してください。これは、書式設定情報が提供されない場合の既定値であるためです。</span><span class="sxs-lookup"><span data-stu-id="77eee-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="77eee-120">新しいテンプレートをテストするための CSS スタイルの追加</span><span class="sxs-lookup"><span data-stu-id="77eee-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="77eee-121">日付の書式を設定するためのテンプレートを作成する前に、新しいテンプレートに適用できる CSS スタイルルールをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="77eee-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="77eee-122">これらは、レンダリングされたページが新しいテンプレートを使用していることを確認するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="77eee-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="77eee-123">*Content¥ siteof cs*ファイルを開き、次の CSS ルールをファイルの末尾に追加します。</span><span class="sxs-lookup"><span data-stu-id="77eee-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="77eee-124">DateTime 表示テンプレートの追加</span><span class="sxs-lookup"><span data-stu-id="77eee-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="77eee-125">新しいテンプレートを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="77eee-125">Now you can create the new template.</span></span> <span data-ttu-id="77eee-126">*Views\Movies*フォルダーで*displaytemplates*フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="77eee-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="77eee-127">*Views\Shared*フォルダーで、 *Displaytemplates*フォルダーと*editortemplates*フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="77eee-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="77eee-128">*Views\Shared\DisplayTemplates*フォルダー内の表示テンプレートは、すべてのコントローラーで使用されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="77eee-129">*Views\Movie\DisplayTemplates*フォルダー内の表示テンプレートは、`Movie` コントローラーでのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="77eee-130">(同じ名前のテンプレートが両方のフォルダーに存在する場合、 *Views\Movie\DisplayTemplates*フォルダー内のテンプレート (つまり、より具体的なテンプレート) は、`Movie` コントローラーから返されたビューに対して優先されます)。</span><span class="sxs-lookup"><span data-stu-id="77eee-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="77eee-131">**ソリューションエクスプローラー**で、 *Views*フォルダーを展開し、*共有*フォルダーを展開して、 *Views\Shared\DisplayTemplates*フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="77eee-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="77eee-132">**[追加]** をクリックし、 **[表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="77eee-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="77eee-133">**[ビューの追加]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="77eee-134">**[ビュー名]** ボックスに「`DateTime`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="77eee-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="77eee-135">(この名前は、型の名前と一致させるために使用する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="77eee-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="77eee-136">**[部分ビューとして作成]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="77eee-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="77eee-137">[**レイアウトまたはマスターページを使用**し、**厳密に型指定されたビューを作成**する] チェックボックスがオフになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="77eee-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="77eee-138">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="77eee-138">Click **Add**.</span></span> <span data-ttu-id="77eee-139">*Views\Shared\DisplayTemplates*に*DateTime. cshtml*テンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="77eee-140">次の図は、`DateTime` 表示とエディターのテンプレートが作成された後の**ソリューションエクスプローラー**の*Views*フォルダーを示しています。</span><span class="sxs-lookup"><span data-stu-id="77eee-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="77eee-141">*Views\Shared\DisplayTemplates\DateTime.cshtml*ファイルを開き、次のマークアップを追加します。このマークアップは、 [String. format](https://msdn.microsoft.com/library/system.string.format.aspx)メソッドを使用して、プロパティを時刻なしの日付として書式設定します。</span><span class="sxs-lookup"><span data-stu-id="77eee-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="77eee-142">(`{0:d}` 形式では、短い日付形式を指定します)。</span><span class="sxs-lookup"><span data-stu-id="77eee-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="77eee-143">この手順を繰り返して、 *Views\Movie\DisplayTemplates*フォルダーに `DateTime` テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="77eee-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="77eee-144">*Views\Movie\DisplayTemplates\DateTime.cshtml*ファイルで次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="77eee-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="77eee-145">`loud-1` CSS クラスを使用すると、日付が太字の赤いテキストで表示されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="77eee-146">`loud-1` CSS クラスを一時的なメジャーとして追加したので、この特定のテンプレートがいつ使用されているかを簡単に確認できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="77eee-147">完了した内容と、ASP.NET が日付を表示するために使用するカスタマイズされたテンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="77eee-148">より一般的なテンプレート ( *Views\Shared\DisplayTemplates*フォルダー内) には、単純な短い日付が表示されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="77eee-149">`Movie` controller ( *Views\Movies\DisplayTemplates*フォルダー内) に特化したテンプレートでは、短い形式の日付が太字で太字で表示されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="77eee-150">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="77eee-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="77eee-151">ブラウザーは、アプリケーションのインデックスビューをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="77eee-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="77eee-152">`ReleaseDate` プロパティには、時刻を含まない太字の赤いフォントで日付が表示されるようになりました。これにより、共有フォルダー (*Views\Shared\DisplayTemplates*) の `DateTime` テンプレート化されたヘルパー上で、 *Views\Movies\DisplayTemplates*フォルダー内の `DateTime` テンプレートヘルパーが選択されていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="77eee-153">次に、 *Views\Movies\DisplayTemplates\DateTime.cshtml*ファイルの名前を*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*に変更します。</span><span class="sxs-lookup"><span data-stu-id="77eee-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="77eee-154">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="77eee-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="77eee-155">今回は、[`ReleaseDate`] プロパティに、時刻のない日付と太字の赤いフォントが表示されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="77eee-156">これは、データ型の名前 (この場合 `DateTime`) を持つテンプレートが、その型のすべてのモデルプロパティを表示するために自動的に使用されることを示しています。</span><span class="sxs-lookup"><span data-stu-id="77eee-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="77eee-157">*Datetime. cshtml*ファイルの名前を*LoudDateTime*に変更した後、ASP.NET は*Views\Movies\DisplayTemplates*フォルダー内のテンプレートを見つけられなくなりました。そのため、\* Views\Movies\Shared\* フォルダーの*テンプレートを使用しまし*た。</span><span class="sxs-lookup"><span data-stu-id="77eee-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the \*Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="77eee-158">(テンプレートの照合では大文字と小文字が区別されないため、テンプレートファイル名は大文字と小文字を区別して作成できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="77eee-159">たとえば、 *datetime. cshtml, datetime.* cshtml, and *datetime*は、すべて `DateTime` 型に一致します)。</span><span class="sxs-lookup"><span data-stu-id="77eee-159">For example, *DATETIME.cshtml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="77eee-160">確認する: この時点では、 *Views\Movies\DisplayTemplates\DateTime.cshtml*テンプレートを使用して `ReleaseDate` フィールドが表示されます。このテンプレートでは、短い日付形式を使用してデータが表示されますが、それ以外の場合は特別な形式は追加されません。</span><span class="sxs-lookup"><span data-stu-id="77eee-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="77eee-161">UIHint を使用して表示テンプレートを指定する</span><span class="sxs-lookup"><span data-stu-id="77eee-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="77eee-162">Web アプリケーションに多くの `DateTime` フィールドがあり、既定ではそれらのすべてまたはほとんどを日付のみの形式で表示する場合は、 *DateTime. cshtml*テンプレートを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="77eee-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="77eee-163">しかし、完全な日付と時刻を表示する日付がいくつかある場合はどうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="77eee-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="77eee-164">ご安心ください。</span><span class="sxs-lookup"><span data-stu-id="77eee-164">No problem.</span></span> <span data-ttu-id="77eee-165">追加のテンプレートを作成し、 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を使用して、完全な日付と時刻の書式を指定できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="77eee-166">その後、そのテンプレートを選択的に適用できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-166">You can then selectively apply that template.</span></span> <span data-ttu-id="77eee-167">モデルレベルで[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を使用することも、ビュー内でテンプレートを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="77eee-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="77eee-168">このセクションでは、`UIHint` 属性を使用して、日付/時刻フィールドの一部のインスタンスの書式設定を選択的に変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="77eee-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="77eee-169">*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*ファイルを開き、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="77eee-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="77eee-170">これにより、完全な日付と時刻が表示され、テキストを緑色と large にする CSS クラスが追加されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="77eee-171">*Movie.cs*ファイルを開き、次の例に示すように、 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を `ReleaseDate` プロパティに追加します。</span><span class="sxs-lookup"><span data-stu-id="77eee-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="77eee-172">これは、ASP.NET プロパティ (具体的には `DateTime` オブジェクトではなく) を `ReleaseDate` 表示するときに、 *LoudDateTime*テンプレートを使用する必要があることを MVC に指示します。</span><span class="sxs-lookup"><span data-stu-id="77eee-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="77eee-173">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="77eee-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="77eee-174">`ReleaseDate` プロパティに、日付と時刻が大きな緑色のフォントで表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="77eee-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="77eee-175">*Movie.cs*ファイルの `UIHint` 属性に戻り、 *LoudDateTime*テンプレートが使用されないようにコメントアウトします。</span><span class="sxs-lookup"><span data-stu-id="77eee-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="77eee-176">アプリケーションをもう一度実行する</span><span class="sxs-lookup"><span data-stu-id="77eee-176">Run the application again.</span></span> <span data-ttu-id="77eee-177">リリース日は、大と緑で表示されません。</span><span class="sxs-lookup"><span data-stu-id="77eee-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="77eee-178">これにより、 *Views\Shared\DisplayTemplates\DateTime.cshtml*テンプレートがインデックスビューと詳細ビューで使用されていることが確認されます。</span><span class="sxs-lookup"><span data-stu-id="77eee-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="77eee-179">既に説明したように、ビューにテンプレートを適用することもできます。これにより、データの個々のインスタンスにテンプレートを適用できます。</span><span class="sxs-lookup"><span data-stu-id="77eee-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="77eee-180">*Views\Movies\Details.cshtml*ビューを開きます。</span><span class="sxs-lookup"><span data-stu-id="77eee-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="77eee-181">`ReleaseDate` フィールドの[Html. displayfor](https://msdn.microsoft.com/library/ee407420.aspx)呼び出しの2番目のパラメーターとして `"LoudDateTime"` を追加します。</span><span class="sxs-lookup"><span data-stu-id="77eee-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="77eee-182">完成したコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="77eee-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="77eee-183">これにより、モデルに適用される属性に関係なく、`LoudDateTime` テンプレートを使用してモデルのプロパティを表示する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="77eee-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="77eee-184">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="77eee-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="77eee-185">ムービーのインデックスページが*Views\Shared\DisplayTemplates\DateTime.cshtml*テンプレート (赤の太字) を使用しており、 *mo の詳細*ページで*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*テンプレート (large と green) が使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="77eee-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="77eee-186">次のセクションでは、複合型のテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="77eee-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77eee-187">[前へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [次へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="77eee-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
