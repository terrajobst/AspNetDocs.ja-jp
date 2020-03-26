---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: JQuery UI Datepicker とモデルバインドおよび web フォームとの統合 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521980"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="68f01-104">JQuery UI Datepicker とモデルバインドおよび web フォームとの統合</span><span class="sxs-lookup"><span data-stu-id="68f01-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="68f01-105">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="68f01-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="68f01-106">このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。</span><span class="sxs-lookup"><span data-stu-id="68f01-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="68f01-107">モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。</span><span class="sxs-lookup"><span data-stu-id="68f01-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="68f01-108">このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。</span><span class="sxs-lookup"><span data-stu-id="68f01-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="68f01-109">このチュートリアルでは、JQuery UI [Datepicker ウィジェット](http://jqueryui.com/datepicker/)を Web フォームに追加し、モデルバインドを使用して、選択した値でデータベースを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="68f01-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="68f01-110">このチュートリアルは、シリーズの[第 1](retrieving-data.md)部と[第 2](updating-deleting-and-creating-data.md)部で作成したプロジェクトに基づいています。</span><span class="sxs-lookup"><span data-stu-id="68f01-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="68f01-111">完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。</span><span class="sxs-lookup"><span data-stu-id="68f01-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="68f01-112">ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。</span><span class="sxs-lookup"><span data-stu-id="68f01-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="68f01-113">このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="68f01-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="68f01-114">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="68f01-114">What you'll build</span></span>

<span data-ttu-id="68f01-115">このチュートリアルでは、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="68f01-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="68f01-116">学生の登録日を記録するために、モデルにプロパティを追加します</span><span class="sxs-lookup"><span data-stu-id="68f01-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="68f01-117">JQuery UI Datepicker ウィジェットを使用して、ユーザーが登録日を選択できるようにします</span><span class="sxs-lookup"><span data-stu-id="68f01-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="68f01-118">登録日に検証規則を適用する</span><span class="sxs-lookup"><span data-stu-id="68f01-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="68f01-119">JQuery UI Datepicker ウィジェットを使用すると、ユーザーがフィールドと対話したときに表示されるカレンダーから日付を簡単に選択できます。</span><span class="sxs-lookup"><span data-stu-id="68f01-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="68f01-120">このウィジェットを使用すると、ユーザーが手動で日付を入力するよりも便利です。</span><span class="sxs-lookup"><span data-stu-id="68f01-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="68f01-121">データ操作にモデルバインドを使用するページに Datepicker ウィジェットを統合するには、少量の追加作業のみが必要です。</span><span class="sxs-lookup"><span data-stu-id="68f01-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="68f01-122">新しいプロパティをモデルに追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-122">Add a new property to the model</span></span>

<span data-ttu-id="68f01-123">まず、スチューデントモデルに**Datetime**プロパティを追加し、その変更をデータベースに移行します。</span><span class="sxs-lookup"><span data-stu-id="68f01-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="68f01-124">**UniversityModels.cs**を開き、強調表示されているコードを Student モデルに追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="68f01-125">**Rangeattribute**は、プロパティの検証規則を適用するために含まれています。</span><span class="sxs-lookup"><span data-stu-id="68f01-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="68f01-126">このチュートリアルでは、Contoso 大学が2013年1月1日に設立されていることを前提としています。そのため、以前の登録日は無効です。</span><span class="sxs-lookup"><span data-stu-id="68f01-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="68f01-127">[Package Management] ウィンドウで、 **AddEnrollmentDate**コマンドを実行して移行を追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="68f01-128">移行コードによって、新しい Datetime 列が Student テーブルに追加されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="68f01-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="68f01-129">RangeAttribute で指定した値と一致させるには、次の強調表示されているコードに示すように、新しい列の既定値を追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="68f01-130">移行ファイルに変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="68f01-130">Save your change to the migration file.</span></span>

<span data-ttu-id="68f01-131">データを再度シードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="68f01-131">You do not need to seed the data again.</span></span> <span data-ttu-id="68f01-132">そのため、[移行] フォルダーで**Configuration.cs**を開き、 **Seed**メソッドのコードを削除またはコメントアウトします。</span><span class="sxs-lookup"><span data-stu-id="68f01-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="68f01-133">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="68f01-133">Save and close the file.</span></span>

<span data-ttu-id="68f01-134">次に、コマンド**update-database**を実行します。</span><span class="sxs-lookup"><span data-stu-id="68f01-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="68f01-135">列がデータベースに存在し、既存のすべてのレコードの既定値が EnrollmentDate になっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="68f01-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="68f01-136">登録日の動的コントロールを追加する</span><span class="sxs-lookup"><span data-stu-id="68f01-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="68f01-137">ここで、登録日を表示および編集するためのコントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="68f01-138">この時点で、値はテキストボックスを使用して編集されます。</span><span class="sxs-lookup"><span data-stu-id="68f01-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="68f01-139">このチュートリアルの後半では、テキストボックスを JQuery Datepicker ウィジェットに変更します。</span><span class="sxs-lookup"><span data-stu-id="68f01-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="68f01-140">まず、 **Addstudent .aspx**ファイルを変更する必要がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="68f01-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="68f01-141">DynamicEntity コントロールは、新しいプロパティを自動的に表示します。</span><span class="sxs-lookup"><span data-stu-id="68f01-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="68f01-142">**Student**を開き、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="68f01-143">アプリケーションを実行して、登録日の値を日付を入力して設定できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="68f01-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="68f01-144">新しい学生を追加する場合:</span><span class="sxs-lookup"><span data-stu-id="68f01-144">When adding a new student:</span></span>

![日付の設定](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="68f01-146">または、既存の値を編集します。</span><span class="sxs-lookup"><span data-stu-id="68f01-146">Or, editing an existing value:</span></span>

![日付の編集](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="68f01-148">日付を入力しても機能しますが、お客様が提供するユーザーエクスペリエンスとは限りません。</span><span class="sxs-lookup"><span data-stu-id="68f01-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="68f01-149">次のセクションでは、カレンダーを使用して日付を選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="68f01-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="68f01-150">JQuery UI を使用するための NuGet パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="68f01-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="68f01-151">**ジュース ui** NuGet パッケージを使用すると、JQuery ui ウィジェットを web アプリケーションに簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="68f01-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="68f01-152">このパッケージを使用するには、NuGet を使用してインストールします。</span><span class="sxs-lookup"><span data-stu-id="68f01-152">To use this package, install it through NuGet.</span></span>

![ジュース UI の追加](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="68f01-154">インストールするジュース UI のバージョンが、アプリケーションの JQuery のバージョンと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="68f01-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="68f01-155">このチュートリアルを続行する前に、アプリケーションを実行してみてください。</span><span class="sxs-lookup"><span data-stu-id="68f01-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="68f01-156">JavaScript エラーが発生した場合は、JQuery バージョンを調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="68f01-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="68f01-157">必要なバージョンの JQuery を Scripts フォルダー (このチュートリアルの作成時にバージョン 1.8.2) に追加するか、または、サイトで JQuery ファイルへのパスを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="68f01-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="68f01-158">Datepicker ウィジェットを含めるように DateTime テンプレートをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="68f01-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="68f01-159">Datetime 値を編集するために、動的データテンプレートに Datepicker ウィジェットを追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="68f01-160">テンプレートにウィジェットを追加すると、新しい学生を追加するためのフォームと、学生を編集するためのグリッドビューの両方に自動的にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="68f01-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="68f01-161">**DateTime\_Edit .ascx**を開き、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="68f01-162">分離コードファイルでは、DatePicker の日付の最小値と最大値を設定します。</span><span class="sxs-lookup"><span data-stu-id="68f01-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="68f01-163">これらの値を設定すると、ユーザーが無効な日付に移動するのを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="68f01-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="68f01-164">DateTime プロパティの**Rangeattribute**から最小値と最大値を取得します (指定されている場合)。</span><span class="sxs-lookup"><span data-stu-id="68f01-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="68f01-165">**DateTime\_Edit.ascx.cs**を開き、次の強調表示されたコードをページ\_Load メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="68f01-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="68f01-166">Web アプリケーションを実行し、AddStudent ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="68f01-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="68f01-167">フィールドに値を指定すると、登録日のテキストボックスをクリックするとカレンダーが表示されることがわかります。</span><span class="sxs-lookup"><span data-stu-id="68f01-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![日付の選択](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="68f01-169">日付を選択し、 **[挿入]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="68f01-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="68f01-170">RangeAttribute は、サーバーで検証を強制します。</span><span class="sxs-lookup"><span data-stu-id="68f01-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="68f01-171">Datepicker の minDate プロパティを設定することにより、クライアントに検証も適用します。</span><span class="sxs-lookup"><span data-stu-id="68f01-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="68f01-172">このカレンダーでは、ユーザーは minDate の値より前の日付に移動することはできません。</span><span class="sxs-lookup"><span data-stu-id="68f01-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="68f01-173">グリッドビューでレコードを編集すると、カレンダーも表示されます。</span><span class="sxs-lookup"><span data-stu-id="68f01-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![GridView の Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="68f01-175">まとめ</span><span class="sxs-lookup"><span data-stu-id="68f01-175">Conclusion</span></span>

<span data-ttu-id="68f01-176">このチュートリアルでは、モデルバインドを使用する web フォームに JQuery ウィジェットを組み込む方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="68f01-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="68f01-177">次の[チュートリアル](using-query-string-values-to-retrieve-data.md)では、データを選択するときにクエリ文字列値を使用します。</span><span class="sxs-lookup"><span data-stu-id="68f01-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="68f01-178">[前へ](sorting-paging-and-filtering-data.md)
> [次へ](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="68f01-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
