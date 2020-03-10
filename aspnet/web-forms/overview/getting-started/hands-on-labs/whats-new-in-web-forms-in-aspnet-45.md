---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5 | の Web フォームの新機能Microsoft Docs
author: rick-anderson
description: 新しいバージョンの ASP.NET Web フォームでは、データを操作する際のユーザーエクスペリエンスの向上に焦点を合わせた多くの機能強化が導入されています。 以前のバージョンの
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421924"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a><span data-ttu-id="e680b-104">ASP.NET 4.5 の Web フォームの新機能</span><span class="sxs-lookup"><span data-stu-id="e680b-104">What's New in Web Forms in ASP.NET 4.5</span></span>

<span data-ttu-id="e680b-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="e680b-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="e680b-106">新しいバージョンの ASP.NET Web フォームでは、データを操作する際のユーザーエクスペリエンスの向上に焦点を合わせた多くの機能強化が導入されています。</span><span class="sxs-lookup"><span data-stu-id="e680b-106">The new version of ASP.NET Web Forms introduces a number of improvements focused on improving user experience when working with data.</span></span>
> 
> <span data-ttu-id="e680b-107">以前のバージョンの Web フォームでは、データバインディングを使用してオブジェクトメンバーの値を出力する場合、データバインディング式 Bind () または Eval () が使用されていました。</span><span class="sxs-lookup"><span data-stu-id="e680b-107">In previous versions of Web Forms, when using data-binding to emit the value of an object member, you used the data-binding expressions Bind() or Eval().</span></span> <span data-ttu-id="e680b-108">新しいバージョンの ASP.NET では、新しい ItemType プロパティを使用して、コントロールがバインドされるデータの種類を宣言できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-108">In the new version of ASP.NET, you are able to declare what type of data a control is going to be bound to by using a new ItemType property.</span></span> <span data-ttu-id="e680b-109">このプロパティを設定すると、厳密に型指定された変数を使用して、IntelliSense、メンバーナビゲーション、コンパイル時のチェックなど、Visual Studio の開発エクスペリエンスのすべての利点を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-109">Setting this property will enable you to use a strongly-typed variable to receive the full benefits of the Visual Studio development experience, such as IntelliSense, member navigation, and compile-time checking.</span></span>
> 
> <span data-ttu-id="e680b-110">データバインドコントロールを使用すると、データを選択、更新、削除、挿入するための独自のカスタムメソッドを指定できるようになりました。また、ページコントロールとアプリケーションロジックの間のやり取りが簡単になります。</span><span class="sxs-lookup"><span data-stu-id="e680b-110">With the data-bound controls, you can now also specify your own custom methods for selecting, updating, deleting and inserting data, simplifying the interaction between the page controls and your application logic.</span></span> <span data-ttu-id="e680b-111">また、モデルバインド機能が ASP.NET に追加されています。つまり、ページからのデータをメソッドの型パラメーターに直接マップできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-111">Additionally, model binding capabilities have been added to ASP.NET, which means you can map data from the page directly into method type parameters.</span></span>
> 
> <span data-ttu-id="e680b-112">ユーザー入力の検証は、Web フォームの最新バージョンでも簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-112">Validating user input should also be easier with the latest version of Web Forms.</span></span> <span data-ttu-id="e680b-113">**System.componentmodel**名前空間の検証属性を使用してモデルクラスに注釈を付け、すべてのサイトコントロールがその情報を使用してユーザー入力を検証するように要求できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-113">You can now annotate your model classes with validation attributes from the **System.ComponentModel.DataAnnotations** namespace and request that all your site controls validate user input using that information.</span></span> <span data-ttu-id="e680b-114">Web フォームでのクライアント側の検証が jQuery と統合され、クライアント側のコードと控えめな JavaScript 機能が提供されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-114">Client-side validation in Web Forms is now integrated with jQuery, providing cleaner client-side code and unobtrusive JavaScript features.</span></span>
> 
> <span data-ttu-id="e680b-115">[要求の検証] 領域では、アプリケーションの特定の部分に対する要求の検証を選択的にオフにするか、無効化された要求データを読み取ることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-115">In the request validation area, improvements have been made to make it easier to selectively turn off request validation for specific parts of your applications or read invalidated request data.</span></span>
> 
> <span data-ttu-id="e680b-116">HTML5 の新機能を利用するために、Web フォームサーバーコントロールにいくつかの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="e680b-116">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>
> 
> - <span data-ttu-id="e680b-117">TextBox コントロールの TextMode プロパティが更新され、email や datetime などの新しい HTML5 入力型がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-117">The TextMode property of the TextBox control has been updated to support the new HTML5 input types like email, datetime, and so on.</span></span>
> - <span data-ttu-id="e680b-118">FileUpload コントロールで、この HTML5 機能をサポートするブラウザーからの複数のファイルアップロードがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-118">The FileUpload control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
> - <span data-ttu-id="e680b-119">検証コントロールは、HTML5 入力要素の検証をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-119">Validator controls now support validating HTML5 input elements.</span></span>
> - <span data-ttu-id="e680b-120">URL を表す属性を持つ新しい HTML5 要素では、runat =&quot;server&quot;がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-120">New HTML5 elements that have attributes that represent a URL now support runat=&quot;server&quot;.</span></span> <span data-ttu-id="e680b-121">その結果、URL パスで ASP.NET 規則を使用することができます。たとえば、~ 演算子を使用すると、アプリケーションのルートを表すことができます (&lt;video runat =&quot;server&quot; src =&quot;~/myvideo&quot;&gt;&lt;/ビデオ&gt;)。</span><span class="sxs-lookup"><span data-stu-id="e680b-121">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat=&quot;server&quot; src=&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;).</span></span>
> - <span data-ttu-id="e680b-122">UpdatePanel コントロールは、HTML5 入力フィールドの投稿をサポートするように修正されました。</span><span class="sxs-lookup"><span data-stu-id="e680b-122">The UpdatePanel control has been fixed to support posting HTML5 input fields.</span></span>
> 
> <span data-ttu-id="e680b-123">公式 ASP.NET ポータルでは、ASP.NET WebForms 4.5 の新機能の例をご覧いただけます。 [ASP.NET 4.5 と Visual Studio 2012 の新](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)機能</span><span class="sxs-lookup"><span data-stu-id="e680b-123">In the official ASP.NET portal you can find more examples of the new features in ASP.NET WebForms 4.5: [What's New in ASP.NET 4.5 and Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span></span>
> 
> <span data-ttu-id="e680b-124">すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="e680b-124">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="e680b-125">目標</span><span class="sxs-lookup"><span data-stu-id="e680b-125">Objectives</span></span>

<span data-ttu-id="e680b-126">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="e680b-126">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="e680b-127">厳密に型指定されたデータバインディング式を使用する</span><span class="sxs-lookup"><span data-stu-id="e680b-127">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="e680b-128">Web フォームでの新しいモデルバインド機能の使用</span><span class="sxs-lookup"><span data-stu-id="e680b-128">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="e680b-129">ページデータを分離コードメソッドにマップするための値プロバイダーの使用</span><span class="sxs-lookup"><span data-stu-id="e680b-129">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="e680b-130">ユーザー入力の検証にデータ注釈を使用する</span><span class="sxs-lookup"><span data-stu-id="e680b-130">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="e680b-131">Web フォームの jQuery を使用した控えめなクライアント側の検証を活用する</span><span class="sxs-lookup"><span data-stu-id="e680b-131">Take advantage of unobtrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="e680b-132">詳細な要求の検証を実装する</span><span class="sxs-lookup"><span data-stu-id="e680b-132">Implement granular request validation</span></span>
- <span data-ttu-id="e680b-133">Web フォームでの非同期ページ処理の実装</span><span class="sxs-lookup"><span data-stu-id="e680b-133">Implement asynchronous page processing in Web Forms</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="e680b-134">前提条件</span><span class="sxs-lookup"><span data-stu-id="e680b-134">Prerequisites</span></span>

<span data-ttu-id="e680b-135">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="e680b-135">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="e680b-136">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="e680b-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="e680b-137">セットアップ</span><span class="sxs-lookup"><span data-stu-id="e680b-137">Setup</span></span>

<span data-ttu-id="e680b-138">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="e680b-138">**Installing Code Snippets**</span></span>

<span data-ttu-id="e680b-139">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="e680b-139">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="e680b-140">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="e680b-140">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="e680b-141">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-141">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="e680b-142">手順</span><span class="sxs-lookup"><span data-stu-id="e680b-142">Exercises</span></span>

<span data-ttu-id="e680b-143">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e680b-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="e680b-144">演習 1: ASP.NET Web フォームでのモデルバインド</span><span class="sxs-lookup"><span data-stu-id="e680b-144">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>](#Exercise1)
2. [<span data-ttu-id="e680b-145">演習 2: データの検証</span><span class="sxs-lookup"><span data-stu-id="e680b-145">Exercise 2: Data Validation</span></span>](#Exercise2)
3. [<span data-ttu-id="e680b-146">演習 3: ASP.NET Web フォームでの非同期ページ処理</span><span class="sxs-lookup"><span data-stu-id="e680b-146">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="e680b-147">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="e680b-147">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="e680b-148">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-148">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="e680b-149">このラボの推定所要時間: **60 分**。</span><span class="sxs-lookup"><span data-stu-id="e680b-149">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a><span data-ttu-id="e680b-150">演習 1: ASP.NET Web フォームでのモデルバインド</span><span class="sxs-lookup"><span data-stu-id="e680b-150">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>

<span data-ttu-id="e680b-151">新しいバージョンの ASP.NET Web フォームでは、データを操作する際のエクスペリエンスの向上に焦点を合わせた多くの拡張機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="e680b-151">The new version of ASP.NET Web Forms introduces a number of enhancements focused on improving the experience when working with data.</span></span> <span data-ttu-id="e680b-152">この演習では、厳密に型指定されたデータコントロールとモデルバインドについて学習します。</span><span class="sxs-lookup"><span data-stu-id="e680b-152">Throughout this exercise, you will learn about strongly typed data-controls and model binding.</span></span>

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a><span data-ttu-id="e680b-153">タスク 1-厳密に型指定されたデータバインディングの使用</span><span class="sxs-lookup"><span data-stu-id="e680b-153">Task 1 - Using Strongly-Typed Data-Bindings</span></span>

<span data-ttu-id="e680b-154">このタスクでは、ASP.NET 4.5 で使用可能な新しい厳密に型指定されたバインディングについて説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-154">In this task, you will discover the new strongly-typed bindings available in ASP.NET 4.5.</span></span>

1. <span data-ttu-id="e680b-155">**Source/Ex1-ModelBinding/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-155">Open the **Begin** solution located at **Source/Ex1-ModelBinding/Begin/** folder.</span></span>

   1. <span data-ttu-id="e680b-156">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-156">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e680b-157">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e680b-157">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e680b-158">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-158">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e680b-159">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="e680b-159">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e680b-160">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="e680b-160">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e680b-161">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-161">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e680b-162">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-162">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e680b-163">**[Customers]** ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-163">Open the **Customers.aspx** page.</span></span> <span data-ttu-id="e680b-164">メインコントロールに番号なしのリストを配置し、各顧客を一覧表示するための内に repeater コントロールを含めます。</span><span class="sxs-lookup"><span data-stu-id="e680b-164">Place an unnumbered list in the main control and include a repeater control inside for listing each customer.</span></span> <span data-ttu-id="e680b-165">次のコードに示すように、リピータ名を「**顧客 Srepeater** 」に設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-165">Set the repeater name to **customersRepeater** as shown in the following code.</span></span>

    <span data-ttu-id="e680b-166">以前のバージョンの Web フォームでは、データバインディングを使用して、データバインディング先のオブジェクトのメンバーの値を出力する場合、Eval メソッドの呼び出しと共にデータバインディング式を使用して、メンバーの名前を文字列として渡します。</span><span class="sxs-lookup"><span data-stu-id="e680b-166">In previous versions of Web Forms, when using data-binding to emit the value of a member on an object you're data-binding to, you would use a data-binding expression, along with a call to the Eval method, passing in the name of the member as a string.</span></span>

    <span data-ttu-id="e680b-167">実行時に、Eval へのこれらの呼び出しは、指定された名前を持つメンバーの値を読み取るために、現在バインドされているオブジェクトに対してリフレクションを使用し、結果を HTML に表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-167">At runtime, these calls to Eval will use reflection against the currently bound object to read the value of the member with the given name, and display the result in the HTML.</span></span> <span data-ttu-id="e680b-168">この方法を使用すると、任意の整形されていないデータに対してデータバインドを非常に簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-168">This approach makes it very easy to data-bind against arbitrary, unshaped data.</span></span>

    <span data-ttu-id="e680b-169">残念ながら、メンバー名の IntelliSense、ナビゲーションのサポート ([定義へ移動] など)、およびコンパイル時チェックを含む、Visual Studio の優れた開発時エクスペリエンス機能の多くが失われています。</span><span class="sxs-lookup"><span data-stu-id="e680b-169">Unfortunately, you lose many of the great development-time experience features in Visual Studio, including IntelliSense for member names, support for navigation (like Go To Definition), and compile-time checking.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. <span data-ttu-id="e680b-170">**Customers.aspx.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-170">Open the **Customers.aspx.cs** file.</span></span>
4. <span data-ttu-id="e680b-171">次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-171">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. <span data-ttu-id="e680b-172">**ページ\_Load**メソッドで、顧客の一覧を使用してリピータに設定するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-172">In the **Page\_Load** method, add code to populate the repeater with the list of customers.</span></span>

    <span data-ttu-id="e680b-173">(コードスニペット- *Web フォーム Ex01-Bind Customers データソース*)</span><span class="sxs-lookup"><span data-stu-id="e680b-173">(Code Snippet - *Web Forms Lab - Ex01 - Bind Customers Data Source*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    <span data-ttu-id="e680b-174">このソリューションでは、EntityFramework と CodeFirst を使用して、データベースを作成し、アクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-174">The solution uses EntityFramework together with CodeFirst to create and access the database.</span></span> <span data-ttu-id="e680b-175">次のコードでは、顧客の Srepeater は、データベースからすべての顧客を返す具体化されたクエリにバインドされています。</span><span class="sxs-lookup"><span data-stu-id="e680b-175">In the following code, the customersRepeater is bound to a materialized query that returns all the customers from the database.</span></span>
6. <span data-ttu-id="e680b-176">**F5**キーを押してソリューションを実行し、 **[Customers]** ページにアクセスして、リピータが動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-176">Press **F5** to run the solution and go to the **Customers** page to see the repeater in action.</span></span> <span data-ttu-id="e680b-177">ソリューションが CodeFirst を使用しているときは、アプリケーションの実行時にデータベースが作成され、ローカルの SQL Express インスタンスに設定されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-177">As the solution is using CodeFirst, the database will be created and populated in your local SQL Express instance when running the application.</span></span>

    <span data-ttu-id="e680b-178">![リピータを使用した顧客の一覧表示](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "リピータを使用した顧客の一覧表示")</span><span class="sxs-lookup"><span data-stu-id="e680b-178">![Listing the customers with a repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Listing the customers with a repeater")</span></span>

    <span data-ttu-id="e680b-179">*リピータを使用した顧客の一覧表示*</span><span class="sxs-lookup"><span data-stu-id="e680b-179">*Listing the customers with a repeater*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-180">Visual Studio 2012 では、IIS Express は既定の Web 開発サーバーです。</span><span class="sxs-lookup"><span data-stu-id="e680b-180">In Visual Studio 2012, IIS Express is the default Web development server.</span></span>
7. <span data-ttu-id="e680b-181">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-181">Close the browser and go back to Visual Studio.</span></span>
8. <span data-ttu-id="e680b-182">ここで、実装を置き換えて、厳密に型指定されたバインディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="e680b-182">Now replace the implementation to use strongly typed bindings.</span></span> <span data-ttu-id="e680b-183">**Customers**ページを開き、repeater の新しい**ItemType**属性を使用して、**顧客**の種類をバインドの種類として設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-183">Open the **Customers.aspx** page and use the new **ItemType** attribute in the repeater to set the **Customer** type as the binding type.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    <span data-ttu-id="e680b-184">ItemType プロパティを使用すると、コントロールがバインドされるデータの種類を宣言し、データバインドコントロール内で厳密に型指定されたバインディングを使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="e680b-184">The ItemType property enables you to declare which type of data the control is going to be bound to and allows you to use strongly-typed binding inside the data-bound control.</span></span>
9. <span data-ttu-id="e680b-185">ItemTemplate コンテンツを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e680b-185">Replace the ItemTemplate content with the following code.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    <span data-ttu-id="e680b-186">上記のアプローチの欠点の1つは、Eval () および Bind () の呼び出しが遅延バインディングされることです。つまり、プロパティ名を表す文字列を渡します。</span><span class="sxs-lookup"><span data-stu-id="e680b-186">One downside with the above approaches is that the calls to Eval() and Bind() are late-bound - meaning you pass strings to represent the property names.</span></span> <span data-ttu-id="e680b-187">つまり、メンバー名に対して Intellisense を使用したり、コードナビゲーション ([定義へ移動] など) をサポートしたり、コンパイル時のチェックをサポートしたりすることはありません。</span><span class="sxs-lookup"><span data-stu-id="e680b-187">This means you don't get Intellisense for the member names, support for code navigation (like Go To Definition), nor compile-time checking support.</span></span>

    <span data-ttu-id="e680b-188">ItemType プロパティを設定すると、2つの新しい型指定された変数が、 **Item**および**BindItem**というデータバインディング式のスコープ内に生成されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-188">Setting the ItemType property causes two new typed variables to be generated in the scope of the data-binding expressions: **Item** and **BindItem**.</span></span> <span data-ttu-id="e680b-189">これらの厳密に型指定された変数をデータバインディング式で使用して、Visual Studio 開発環境のすべての利点を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-189">You can use these strongly typed variables in the data-binding expressions and get the full benefits of the Visual Studio development experience.</span></span>

    <span data-ttu-id="e680b-190">式で使用されている &quot; **:** &quot; は、セキュリティの問題 (クロスサイトスクリプティング攻撃など) を回避するために、出力を自動的に HTML エンコードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-190">The &quot;**:** &quot; used in the expression will automatically HTML-encode the output to avoid security issues (for example, cross-site scripting attacks).</span></span> <span data-ttu-id="e680b-191">この表記は、応答の書き込みのために .NET 4 以降で使用できるようになりましたが、現在はデータバインディング式でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-191">This notation was available since .NET 4 for response writing, but now is also available in data-binding expressions.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-192">項目メンバーは、一方向のバインドに対して機能します。</span><span class="sxs-lookup"><span data-stu-id="e680b-192">The Item member works for one-way binding.</span></span> <span data-ttu-id="e680b-193">双方向のバインドを実行する場合は、 **BindItem**メンバーを使用します。</span><span class="sxs-lookup"><span data-stu-id="e680b-193">If you want to perform two-way binding use the **BindItem** member.</span></span>

    <span data-ttu-id="e680b-194">![厳密に型指定されたバインディングでの IntelliSense のサポート](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "厳密に型指定されたバインディングでの IntelliSense のサポート")</span><span class="sxs-lookup"><span data-stu-id="e680b-194">![IntelliSense support in strongly-typed binding](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "IntelliSense support in strongly-typed binding")</span></span>

    <span data-ttu-id="e680b-195">*厳密に型指定されたバインディングでの IntelliSense のサポート*</span><span class="sxs-lookup"><span data-stu-id="e680b-195">*IntelliSense support in strongly-typed binding*</span></span>
10. <span data-ttu-id="e680b-196">**F5**キーを押してソリューションを実行し、[Customers] ページにアクセスして、変更が期待どおりに動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-196">Press **F5** to run the solution and go to the Customers page to make sure the changes work as expected.</span></span>

    <span data-ttu-id="e680b-197">![顧客の詳細の一覧表示](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "顧客の詳細の一覧表示")</span><span class="sxs-lookup"><span data-stu-id="e680b-197">![Listing customer details](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Listing customer details")</span></span>

    <span data-ttu-id="e680b-198">*顧客の詳細の一覧表示*</span><span class="sxs-lookup"><span data-stu-id="e680b-198">*Listing customer details*</span></span>
11. <span data-ttu-id="e680b-199">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-199">Close the browser and go back to Visual Studio.</span></span>

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a><span data-ttu-id="e680b-200">タスク 2-Web フォームでのモデルバインドの概要</span><span class="sxs-lookup"><span data-stu-id="e680b-200">Task 2 - Introducing Model Binding in Web Forms</span></span>

<span data-ttu-id="e680b-201">以前のバージョンの ASP.NET Web フォームでは、データの取得と更新の両方で双方向のデータバインディングを実行する場合、データソースオブジェクトを使用する必要がありました。</span><span class="sxs-lookup"><span data-stu-id="e680b-201">In previous versions of ASP.NET Web Forms, when you wanted to perform two-way data-binding, both retrieving and updating data, you needed to use a Data Source object.</span></span> <span data-ttu-id="e680b-202">これには、オブジェクトデータソース、SQL データソース、LINQ データソースなどがあります。</span><span class="sxs-lookup"><span data-stu-id="e680b-202">This could be an Object Data Source, a SQL Data Source, a LINQ Data Source and so on.</span></span> <span data-ttu-id="e680b-203">ただし、データを処理するためのカスタムコードが必要なシナリオでは、オブジェクトデータソースを使用する必要があります。これにより、いくつかの欠点がもたらされます。</span><span class="sxs-lookup"><span data-stu-id="e680b-203">However if your scenario required custom code for handling the data, you needed to use the Object Data Source and this brought some drawbacks.</span></span> <span data-ttu-id="e680b-204">たとえば、複合型を避け、検証ロジックの実行時に例外を処理する必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="e680b-204">For example, you needed to avoid complex types and you needed to handle exceptions when executing validation logic.</span></span>

<span data-ttu-id="e680b-205">新しいバージョンの ASP.NET Web フォームでは、データバインドコントロールはモデルバインドをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="e680b-205">In the new version of ASP.NET Web Forms the data-bound controls support model binding.</span></span> <span data-ttu-id="e680b-206">つまり、選択、更新、挿入、および削除の各メソッドをデータバインドコントロールに直接指定して、分離コードファイルまたは別のクラスからロジックを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-206">This means that you can specify select, update, insert and delete methods directly in the data-bound control to call logic from your code-behind file or from another class.</span></span>

<span data-ttu-id="e680b-207">この詳細については、GridView を使用して、新しい**SelectMethod**属性を使用して製品カテゴリを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-207">To learn about this, you will use a GridView to list the product categories using the new **SelectMethod** attribute.</span></span> <span data-ttu-id="e680b-208">この属性を使用すると、GridView データを取得するメソッドを指定できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-208">This attribute enables you to specify a method for retrieving the GridView data.</span></span>

1. <span data-ttu-id="e680b-209">**Products**ページを開き、 **GridView**を含めます。</span><span class="sxs-lookup"><span data-stu-id="e680b-209">Open the **Products.aspx** page and include a **GridView**.</span></span> <span data-ttu-id="e680b-210">次に示すように GridView を構成して、厳密に型指定されたバインディングを使用し、並べ替えとページングを有効にします。</span><span class="sxs-lookup"><span data-stu-id="e680b-210">Configure the GridView as shown below to use strongly-typed bindings and enable sorting and paging.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. <span data-ttu-id="e680b-211">新しい**SelectMethod**属性を使用して、 **GetCategories**メソッドを呼び出してデータを選択するように GridView を構成します。</span><span class="sxs-lookup"><span data-stu-id="e680b-211">Use the new **SelectMethod** attribute to configure the GridView to call a **GetCategories** method to select the data.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. <span data-ttu-id="e680b-212">**Products.aspx.cs**分離コードファイルを開き、次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-212">Open the **Products.aspx.cs** code-behind file and add the following using statements.</span></span>

    <span data-ttu-id="e680b-213">(コードスニペット- *Web フォーム Ex01-名前空間*)</span><span class="sxs-lookup"><span data-stu-id="e680b-213">(Code Snippet - *Web Forms Lab - Ex01 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. <span data-ttu-id="e680b-214">Products クラスにプライベートメンバーを追加し、**製品** **コンテキスト**の新しいインスタンスを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="e680b-214">Add a private member in the **Products** class and assign a new instance of **ProductsContext**.</span></span> <span data-ttu-id="e680b-215">このプロパティには、データベースに接続できるようにする Entity Framework データコンテキストが格納されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-215">This property will store the Entity Framework data context that enables you to connect to the database.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. <span data-ttu-id="e680b-216">LINQ を使用してカテゴリの一覧を取得するための**GetCategories**メソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="e680b-216">Create a **GetCategories** method to retrieve the list of categories using LINQ.</span></span> <span data-ttu-id="e680b-217">このクエリには**products**プロパティが含まれているため、GridView は各カテゴリの製品の量を表示できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-217">The query will include the **Products** property so the GridView can show the amount of products for each category.</span></span> <span data-ttu-id="e680b-218">メソッドは、ページのライフサイクルで後で実行されるクエリを表す未加工の IQueryable オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="e680b-218">Notice that the method returns a raw IQueryable object that represent the query to be executed later on the page lifecycle.</span></span>

    <span data-ttu-id="e680b-219">(コードスニペット- *Web フォーム Ex01-GetCategories*)</span><span class="sxs-lookup"><span data-stu-id="e680b-219">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="e680b-220">以前のバージョンの ASP.NET Web フォームでは、オブジェクトデータソースコンテキスト内で独自のリポジトリロジックを使用して並べ替えとページングを有効にすることで、独自のカスタムコードを記述し、必要なすべてのパラメーターを受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-220">In previous versions of ASP.NET Web Forms, enabling sorting and paging using your own repository logic within an Object Data Source context, required to write your own custom code and receive all the necessary parameters.</span></span> <span data-ttu-id="e680b-221">これで、データバインディングメソッドが IQueryable を返すことができるようになりました。これは実行されているクエリを表しているため、ASP.NET はクエリを変更して適切な並べ替えとページングパラメーターを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-221">Now, as the data-binding methods can return IQueryable and this represents a query still to be executed, ASP.NET can take care of modifying the query to add the proper sorting and paging parameters.</span></span>
6. <span data-ttu-id="e680b-222">**F5**キーを押してサイトのデバッグを開始し、[製品] ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-222">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="e680b-223">GridView には、GetCategories メソッドによって返されるカテゴリが設定されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="e680b-223">You should see that the GridView is populated with the categories returned by the GetCategories method.</span></span>

    <span data-ttu-id="e680b-224">![モデルバインドを使用した GridView の設定](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "モデルバインドを使用した GridView の設定")</span><span class="sxs-lookup"><span data-stu-id="e680b-224">![Populating a GridView using model binding](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Populating a GridView using model binding")</span></span>

    <span data-ttu-id="e680b-225">*モデルバインドを使用した GridView の設定*</span><span class="sxs-lookup"><span data-stu-id="e680b-225">*Populating a GridView using model binding*</span></span>
7. <span data-ttu-id="e680b-226">**SHIFT**キーを押し+**F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="e680b-226">Press **SHIFT**+**F5** Stop debugging.</span></span>

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a><span data-ttu-id="e680b-227">タスク 3-モデルバインドの値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="e680b-227">Task 3 - Value Providers in Model Binding</span></span>

<span data-ttu-id="e680b-228">モデルバインドを使用すると、データバインドコントロールでデータを直接操作するカスタムメソッドを指定できるだけでなく、ページのデータをこれらのメソッドのパラメーターにマップすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-228">Model binding not only enables you to specify custom methods to work with your data directly in the data-bound control, but also allows you to map data from the page into parameters from these methods.</span></span> <span data-ttu-id="e680b-229">メソッドパラメーターでは、値プロバイダーの属性を使用して値のデータソースを指定できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-229">On the method parameter, you can use value provider attributes to specify the value's data source.</span></span> <span data-ttu-id="e680b-230">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-230">For example:</span></span>

- <span data-ttu-id="e680b-231">ページ上のコントロール</span><span class="sxs-lookup"><span data-stu-id="e680b-231">Controls on the page</span></span>
- <span data-ttu-id="e680b-232">クエリ文字列の値</span><span class="sxs-lookup"><span data-stu-id="e680b-232">Query string values</span></span>
- <span data-ttu-id="e680b-233">データの表示</span><span class="sxs-lookup"><span data-stu-id="e680b-233">View data</span></span>
- <span data-ttu-id="e680b-234">セッションの状態</span><span class="sxs-lookup"><span data-stu-id="e680b-234">Session state</span></span>
- <span data-ttu-id="e680b-235">Cookie</span><span class="sxs-lookup"><span data-stu-id="e680b-235">Cookies</span></span>
- <span data-ttu-id="e680b-236">ポストされたフォームデータ</span><span class="sxs-lookup"><span data-stu-id="e680b-236">Posted form data</span></span>
- <span data-ttu-id="e680b-237">状態の表示</span><span class="sxs-lookup"><span data-stu-id="e680b-237">View state</span></span>
- <span data-ttu-id="e680b-238">カスタム値プロバイダーもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e680b-238">Custom value providers are supported as well</span></span>

<span data-ttu-id="e680b-239">ASP.NET MVC 4 を使用している場合は、モデルバインディングのサポートも似ていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="e680b-239">If you have used ASP.NET MVC 4, you will notice the model binding support is similar.</span></span> <span data-ttu-id="e680b-240">実際、これらの機能は ASP.NET MVC から取得さ**れ、system.web アセンブリに**移動され、web フォームでも使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-240">Indeed, these features were taken from ASP.NET MVC and moved into the **System.Web** assembly to be able to use them on Web Forms as well.</span></span>

<span data-ttu-id="e680b-241">このタスクでは、GridView を更新して、各カテゴリの製品の数によって結果をフィルター処理し、モデルバインドでフィルターパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-241">In this task, you will update the GridView to filter its results by the amount of products for each category, receiving the filter parameter with model binding.</span></span>

1. <span data-ttu-id="e680b-242">**[Products]** ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-242">Go back to the **Products.aspx** page.</span></span>
2. <span data-ttu-id="e680b-243">GridView の上部に、次に示すように、各カテゴリの製品数を選択する**ラベル**と**コンボボックス**を追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-243">At the top of the GridView, add a **Label** and a **ComboBox** to select the number of products for each category as shown below.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. <span data-ttu-id="e680b-244">選択した数の製品が含まれているカテゴリが存在しない場合にメッセージを表示するには、 **EmptyDataTemplate**を GridView に追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-244">Add an **EmptyDataTemplate** to the GridView to show a message when there are no categories with the selected number of products.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. <span data-ttu-id="e680b-245">**Products.aspx.cs**の分離コードを開き、次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-245">Open the **Products.aspx.cs** code-behind and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. <span data-ttu-id="e680b-246">**GetCategories**メソッドを変更して、整数の**min製品カウント**引数を受け取り、返された結果をフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="e680b-246">Modify the **GetCategories** method to receive an integer **minProductsCount** argument and filter the returned results.</span></span> <span data-ttu-id="e680b-247">これを行うには、メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e680b-247">To do this, replace the method with the following code.</span></span>

    <span data-ttu-id="e680b-248">(コードスニペット- *Web フォーム Ex01-GetCategories 2*)</span><span class="sxs-lookup"><span data-stu-id="e680b-248">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    <span data-ttu-id="e680b-249">**Min$ count**引数の新しい **[Control]** 属性は、ページ内のコントロールを使用してその値を設定する必要があることを ASP.NET に伝えます。</span><span class="sxs-lookup"><span data-stu-id="e680b-249">The new **[Control]** attribute on the **minProductsCount** argument will let ASP.NET know its value must be populated using a control in the page.</span></span> <span data-ttu-id="e680b-250">ASP.NET は、引数の名前 (Min$ Count) に一致するコントロールを検索し、必要なマッピングと変換を実行して、パラメーターにコントロールの値を設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-250">ASP.NET will look for any control matching the name of the argument (minProductsCount) and perform the necessary mapping and conversion to fill the parameter with the control value.</span></span>

    <span data-ttu-id="e680b-251">または、属性はオーバーロードされたコンストラクターを提供します。このコンストラクターを使用すると、値の取得元のコントロールを指定できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-251">Alternatively, the attribute provides an overloaded constructor that enables you to specify the control from where to get the value.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-252">データバインディング機能の1つの目的は、ページの操作のために記述する必要があるコードの量を減らすことです。</span><span class="sxs-lookup"><span data-stu-id="e680b-252">One goal of the data-binding features is to reduce the amount of code that needs to be written for page interaction.</span></span> <span data-ttu-id="e680b-253">[コントロール] 値プロバイダーとは別に、メソッドパラメーターで他のモデルバインディングプロバイダーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-253">Apart from the [Control] value provider, you can use other model-binding providers in your method parameters.</span></span> <span data-ttu-id="e680b-254">これらの一部は、タスクの概要に記載されています。</span><span class="sxs-lookup"><span data-stu-id="e680b-254">Some of them are listed in the task introduction.</span></span>
6. <span data-ttu-id="e680b-255">**F5**キーを押してサイトのデバッグを開始し、[製品] ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-255">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="e680b-256">ドロップダウンリストから複数の製品を選択すると、GridView がどのように更新されたかがわかります。</span><span class="sxs-lookup"><span data-stu-id="e680b-256">Select a number of products in the drop-down list and notice how the GridView is now updated.</span></span>

    <span data-ttu-id="e680b-257">![ドロップダウンリストの値を使用して GridView をフィルター処理する](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "ドロップダウンリストの値を使用して GridView をフィルター処理する")</span><span class="sxs-lookup"><span data-stu-id="e680b-257">![Filtering the GridView with a drop-down list value](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "Filtering the GridView with a drop-down list value")</span></span>

    <span data-ttu-id="e680b-258">*ドロップダウンリストの値を使用して GridView をフィルター処理する*</span><span class="sxs-lookup"><span data-stu-id="e680b-258">*Filtering the GridView with a drop-down list value*</span></span>
7. <span data-ttu-id="e680b-259">デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="e680b-259">Stop debugging.</span></span>

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a><span data-ttu-id="e680b-260">タスク 4-フィルター処理にモデルバインドを使用する</span><span class="sxs-lookup"><span data-stu-id="e680b-260">Task 4 - Using Model Binding for Filtering</span></span>

<span data-ttu-id="e680b-261">このタスクでは、選択したカテゴリ内の製品を表示するために、2番目の子 GridView を追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-261">In this task, you will add a second, child GridView to show the products within the selected category.</span></span>

1. <span data-ttu-id="e680b-262">**Products**ページを開き、カテゴリ GridView を更新して、[選択] ボタンを自動生成します。</span><span class="sxs-lookup"><span data-stu-id="e680b-262">Open the **Products.aspx** page and update the categories GridView to auto-generate the Select button.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. <span data-ttu-id="e680b-263">一番下にある $ $ 2 番目の "製品" という**名前の 2**つ目の**GridView**を追加</span><span class="sxs-lookup"><span data-stu-id="e680b-263">Add a second **GridView** named **productsGrid** at the bottom.</span></span> <span data-ttu-id="e680b-264">**ItemType**を**webいる datakeynames**に設定します。これは**ProductId**に 、 **SelectMethod**を**getproducts**に設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-264">Set the **ItemType** to **WebFormsLab.Model.Product**, the **DataKeyNames** to **ProductId** and the **SelectMethod** to **GetProducts**.</span></span> <span data-ttu-id="e680b-265">**AutoGenerateColumns**を**false**に設定し、ProductId、ProductName、Description、および UnitPrice の列を追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-265">Set **AutoGenerateColumns** to **false** and add the columns for ProductId, ProductName, Description and UnitPrice.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. <span data-ttu-id="e680b-266">**Products.aspx.cs**分離コードファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-266">Open the **Products.aspx.cs** code-behind file.</span></span> <span data-ttu-id="e680b-267">Category GridView からカテゴリ ID を受け取り、製品をフィルター処理するには、 **Getproducts**メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="e680b-267">Implement the **GetProducts** method to receive the category ID from the category GridView and filter the products.</span></span> <span data-ttu-id="e680b-268">モデルバインドでは、**カテゴリグリッド**で選択された行を使用して、パラメーター値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-268">Model binding will set the parameter value using the selected row in the **categoriesGrid**.</span></span> <span data-ttu-id="e680b-269">引数の名前とコントロール名が一致しないため、コントロールの名前をコントロールの値プロバイダーに指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-269">Since the argument name and control name do not match, you should specify the name of the control in the Control value provider.</span></span>

    <span data-ttu-id="e680b-270">(コードスニペット- *Web フォーム Ex01-GetProducts*)</span><span class="sxs-lookup"><span data-stu-id="e680b-270">(Code Snippet - *Web Forms Lab - Ex01 - GetProducts*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="e680b-271">この方法を使用すると、これらのメソッドの単体テストが簡単になります。</span><span class="sxs-lookup"><span data-stu-id="e680b-271">This approach makes it easier to unit test these methods.</span></span> <span data-ttu-id="e680b-272">Web フォームが実行されていない単体テストコンテキストでは、[コントロール] 属性は特定のアクションを実行しません。</span><span class="sxs-lookup"><span data-stu-id="e680b-272">On a unit test context, where Web Forms is not executing, the [Control] attribute will not perform any specific action.</span></span>
4. <span data-ttu-id="e680b-273">**Products**ページを開き、[Products] GridView を見つけます。</span><span class="sxs-lookup"><span data-stu-id="e680b-273">Open the **Products.aspx** page and locate the products GridView.</span></span> <span data-ttu-id="e680b-274">Products GridView を更新して、選択した製品を編集するためのリンクを表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-274">Update the products GridView to show a link for editing the selected product.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. <span data-ttu-id="e680b-275">**Productdetails .aspx**ページを開き、 **selectproduct**メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e680b-275">Open the **ProductDetails.aspx** page code-behind and replace the **SelectProduct** method with the following code.</span></span>

    <span data-ttu-id="e680b-276">(コードスニペット- *Web フォーム Ex01-SelectProduct メソッド*)</span><span class="sxs-lookup"><span data-stu-id="e680b-276">(Code Snippet - *Web Forms Lab - Ex01 - SelectProduct Method*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="e680b-277">**[QueryString]** 属性を使用して、クエリ文字列の productId パラメーターからメソッドパラメーターを設定することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-277">Notice that the **[QueryString]** attribute is used to fill the method parameter from a productId parameter in the query string.</span></span>
6. <span data-ttu-id="e680b-278">**F5**キーを押してサイトのデバッグを開始し、[製品] ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-278">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="e680b-279">[カテゴリ] GridView から任意のカテゴリを選択し、[products] GridView が更新されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-279">Select any category from the categories GridView and notice that the products GridView is updated.</span></span>

    <span data-ttu-id="e680b-280">![選択したカテゴリの製品を表示しています](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "選択したカテゴリの製品を表示しています")</span><span class="sxs-lookup"><span data-stu-id="e680b-280">![Showing products from the selected category](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Showing products from the selected category")</span></span>

    <span data-ttu-id="e680b-281">*選択したカテゴリの製品を表示しています*</span><span class="sxs-lookup"><span data-stu-id="e680b-281">*Showing products from the selected category*</span></span>
7. <span data-ttu-id="e680b-282">製品の **[表示]** リンクをクリックして、productdetails .aspx ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-282">Click the **View** link on a product to open the ProductDetails.aspx page.</span></span>

    <span data-ttu-id="e680b-283">ページが、クエリ文字列から productId パラメーターを使用して、SelectMethod を使用して製品を取得していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-283">Notice that the page is retrieving the product with the SelectMethod using the productId parameter from the query string.</span></span>

    <span data-ttu-id="e680b-284">![製品の詳細を表示する](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "製品の詳細を表示する")</span><span class="sxs-lookup"><span data-stu-id="e680b-284">![Viewing the product details](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Viewing the product details")</span></span>

    <span data-ttu-id="e680b-285">*製品の詳細を表示する*</span><span class="sxs-lookup"><span data-stu-id="e680b-285">*Viewing the product details*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-286">次の演習では、HTML の説明を入力する機能を実装します。</span><span class="sxs-lookup"><span data-stu-id="e680b-286">The ability to type an HTML description will be implemented in the next exercise.</span></span>

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a><span data-ttu-id="e680b-287">タスク 5-モデルバインドを使用した更新操作</span><span class="sxs-lookup"><span data-stu-id="e680b-287">Task 5 - Using Model Binding for Update Operations</span></span>

<span data-ttu-id="e680b-288">前のタスクでは、主にデータを選択するためにモデルバインドを使用しました。このタスクでは、更新操作でモデルバインドを使用する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="e680b-288">In the previous task, you have used model binding mainly for selecting data, in this task you will learn how to use model binding in update operations.</span></span>

<span data-ttu-id="e680b-289">カテゴリ GridView を更新して、ユーザーがカテゴリを更新できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e680b-289">You will update the categories GridView to let the user update categories.</span></span>

1. <span data-ttu-id="e680b-290">**Products**ページを開き、[カテゴリ] GridView を更新して [Edit] \ (編集 \) ボタンを自動生成し、[new **UpdateMethod** ] 属性を使用して、選択した項目を更新する**UpdateCategory**メソッドを指定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-290">Open the **Products.aspx** page and update the categories GridView to auto-generate the Edit button and use the new **UpdateMethod** attribute to specify an **UpdateCategory** method to update the selected item.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    <span data-ttu-id="e680b-291">GridView のいる datakeynames 属性は、モデルバインドオブジェクトを一意に識別するメンバーであることを定義します。この属性は、update メソッドが少なくとも受信する必要があるパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="e680b-291">The DataKeyNames attribute in the GridView define which are the members that uniquely identify the model-bound object and therefore, which are the parameters the update method should at least receive.</span></span>
2. <span data-ttu-id="e680b-292">**Products.aspx.cs**分離コードファイルを開き、 **UpdateCategory**メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="e680b-292">Open the **Products.aspx.cs** code-behind file and implement the **UpdateCategory** method.</span></span> <span data-ttu-id="e680b-293">メソッドは、現在のカテゴリを読み込むためにカテゴリ ID を受け取り、GridView から値を設定して、カテゴリを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-293">The method should receive the category ID to load the current category, populate the values from the GridView and then update the category.</span></span>

    <span data-ttu-id="e680b-294">(コードスニペット- *Web フォーム Ex01-UpdateCategory*)</span><span class="sxs-lookup"><span data-stu-id="e680b-294">(Code Snippet - *Web Forms Lab - Ex01 - UpdateCategory*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    <span data-ttu-id="e680b-295">ページクラスの新しい**TryUpdateModel**メソッドは、ページ内のコントロールの値を使用して、モデルオブジェクトに値を設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-295">The new **TryUpdateModel** method in the Page class is responsible of populating the model object using the values from the controls in the page.</span></span> <span data-ttu-id="e680b-296">この場合、更新された値は、編集中の現在の GridView 行から**category**オブジェクトに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="e680b-296">In this case, it will replace the updated values from the current GridView row being edited into the **category** object.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-297">次の演習では、オブジェクトの編集時にユーザーが入力したデータを検証するための ModelState. IsValid の使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-297">The next exercise will explain the usage of the ModelState.IsValid for validating the data entered by the user when editing the object.</span></span>
3. <span data-ttu-id="e680b-298">サイトを実行し、[製品] ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-298">Run the site and go to the Products page.</span></span> <span data-ttu-id="e680b-299">カテゴリを編集します。</span><span class="sxs-lookup"><span data-stu-id="e680b-299">Edit a category.</span></span> <span data-ttu-id="e680b-300">新しい名前を入力し、 **[更新]** をクリックして変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="e680b-300">Type a new name and then click **Update** to persist the changes.</span></span>

    <span data-ttu-id="e680b-301">![カテゴリの編集](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "カテゴリの編集")</span><span class="sxs-lookup"><span data-stu-id="e680b-301">![Editing categories](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Editing categories")</span></span>

    <span data-ttu-id="e680b-302">*カテゴリの編集*</span><span class="sxs-lookup"><span data-stu-id="e680b-302">*Editing categories*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a><span data-ttu-id="e680b-303">演習 2: データの検証</span><span class="sxs-lookup"><span data-stu-id="e680b-303">Exercise 2: Data Validation</span></span>

<span data-ttu-id="e680b-304">この演習では、ASP.NET 4.5 の新しいデータ検証機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-304">In this exercise, you will learn about the new data validation features in ASP.NET 4.5.</span></span> <span data-ttu-id="e680b-305">新しい控えめな検証機能については、Web フォームをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e680b-305">You will check out the new unobtrusive validation features in Web Forms.</span></span> <span data-ttu-id="e680b-306">ユーザー入力の検証には、アプリケーションモデルクラスのデータ注釈を使用します。最後に、ページ内の個々のコントロールに対する要求の検証をオンまたはオフにする方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="e680b-306">You will use data annotations in the application model classes for user input validation, and finally, you will learn how to turn on or off request validation to individual controls in a page.</span></span>

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a><span data-ttu-id="e680b-307">タスク 1-控えめな検証</span><span class="sxs-lookup"><span data-stu-id="e680b-307">Task 1 - Unobtrusive Validation</span></span>

<span data-ttu-id="e680b-308">検証コントロールなどの複雑なデータを含むフォームでは、ページ内の JavaScript コードの生成回数が多すぎる傾向があります。これは、コードの約60% を表す可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-308">Forms with complex data including validators tend to generate too much JavaScript code in the page, which can represent about 60% of the code.</span></span> <span data-ttu-id="e680b-309">控えめな検証が有効になっていると、HTML コードはすっきりと tidier に見えます。</span><span class="sxs-lookup"><span data-stu-id="e680b-309">With unobtrusive validation enabled, your HTML code will look cleaner and tidier.</span></span>

<span data-ttu-id="e680b-310">このセクションでは、ASP.NET で控えめな検証を有効にして、両方の構成で生成された HTML コードを比較します。</span><span class="sxs-lookup"><span data-stu-id="e680b-310">In this section, you will enable unobtrusive validation in ASP.NET to compare the HTML code generated by both configurations.</span></span>

1. <span data-ttu-id="e680b-311">**Visual Studio 2012**を開き、このラボの ソース の **開始** フォルダーにある **開始** ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-311">Open **Visual Studio 2012** and open the **Begin** solution located in the **Source\Ex2-Validation\Begin** folder of this lab.</span></span> <span data-ttu-id="e680b-312">または、前の演習の既存のソリューションで作業を続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-312">Alternatively, you can continue working on your existing solution from the previous exercise.</span></span>

   1. <span data-ttu-id="e680b-313">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-313">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e680b-314">これを行うには、ソリューションエクスプローラーで、 **[Web フォームラボ]** プロジェクト **[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-314">To do this, in the Solution Explorer, click the **WebFormsLab** project **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e680b-315">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-315">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e680b-316">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="e680b-316">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e680b-317">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="e680b-317">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e680b-318">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-318">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e680b-319">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-319">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e680b-320">**F5**キーを押して web アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="e680b-320">Press **F5** to start the web application.</span></span> <span data-ttu-id="e680b-321">顧客 ページにアクセスし、**新しい顧客の追加** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-321">Go to the Customers page and click the **Add a New Customer** link.</span></span>
3. <span data-ttu-id="e680b-322">ブラウザーページを右クリックし、[ソースの**表示**] オプションを選択して、アプリケーションによって生成された HTML コードを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-322">Right-click on the browser page, and select **View Source** option to open the HTML code generated by the application.</span></span>

    <span data-ttu-id="e680b-323">![ページの HTML コードを表示する](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "ページの HTML コードを表示する")</span><span class="sxs-lookup"><span data-stu-id="e680b-323">![Showing the page HTML code](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Showing the page HTML code")</span></span>

    <span data-ttu-id="e680b-324">*ページの HTML コードを表示する*</span><span class="sxs-lookup"><span data-stu-id="e680b-324">*Showing the page HTML code*</span></span>
4. <span data-ttu-id="e680b-325">ページのソースコードをスクロールして、検証を実行してエラー一覧を表示するために、ASP.NET によって JavaScript コードとデータ検証コントロールがページに挿入されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-325">Scroll through the page source code and notice that ASP.NET has injected JavaScript code and data validators in the page to perform the validations and show the error list.</span></span>

    <span data-ttu-id="e680b-326">![[顧客の詳細] ページの検証 JavaScript コード](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "[顧客の詳細] ページの検証 JavaScript コード")</span><span class="sxs-lookup"><span data-stu-id="e680b-326">![Validation JavaScript code in CustomerDetails page](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "Validation JavaScript code in CustomerDetails page")</span></span>

    <span data-ttu-id="e680b-327">*[顧客の詳細] ページの検証 JavaScript コード*</span><span class="sxs-lookup"><span data-stu-id="e680b-327">*Validation JavaScript code in CustomerDetails page*</span></span>
5. <span data-ttu-id="e680b-328">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-328">Close the browser and go back to Visual Studio.</span></span>
6. <span data-ttu-id="e680b-329">次に、控えめな検証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="e680b-329">Now you will enable unobtrusive validation.</span></span> <span data-ttu-id="e680b-330">Web.config**を開き、** **AppSettings**セクションで**validationsettings: UnobtrusiveValidationMode** key を**見つけます。**</span><span class="sxs-lookup"><span data-stu-id="e680b-330">Open **Web.Config** and locate **ValidationSettings:UnobtrusiveValidationMode** key in the **AppSettings** section **.**</span></span> <span data-ttu-id="e680b-331">キーの値を**WebForms**に設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-331">Set the key value to **WebForms**.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > <span data-ttu-id="e680b-332">また、一部のページに対してのみ控えめな検証を有効にする場合は、[&quot;] ページでこのプロパティを設定して&quot; イベント **\_読み込む**こともできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-332">You can also set this property in the &quot;**Page\_Load**&quot; event in case you want to enable Unobtrusive Validation only for some pages.</span></span>
7. <span data-ttu-id="e680b-333">[**顧客の詳細] .aspx**を開き、 **F5**キーを押して Web アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="e680b-333">Open **CustomerDetails.aspx** and press **F5** to start the Web application.</span></span>
8. <span data-ttu-id="e680b-334">F12 キーを押して、IE 開発者ツールを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-334">Press the F12 key to open the IE developer tools.</span></span> <span data-ttu-id="e680b-335">開発者ツールが開いたら、スクリプト タブを選択します。メニューから **顧客詳細** を選択し、ページで jQuery を実行するために必要なスクリプトがローカルサイトからブラウザーに読み込まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-335">Once the developer tools is open, select the script tab. Select **CustomerDetails.aspx** from the menu and take note that the scripts required to run jQuery on the page have been loaded into the browser from the local site.</span></span>

    <span data-ttu-id="e680b-336">![ローカル IIS サーバーから直接 jQuery JavaScript ファイルを読み込む](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "ローカル IIS サーバーから直接 jQuery JavaScript ファイルを読み込む")</span><span class="sxs-lookup"><span data-stu-id="e680b-336">![Loading the jQuery JavaScript files directly from the local IIS server](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "Loading the jQuery JavaScript files directly from the local IIS server")</span></span>

    <span data-ttu-id="e680b-337">*ローカル IIS サーバーから直接 jQuery JavaScript ファイルを読み込む*</span><span class="sxs-lookup"><span data-stu-id="e680b-337">*Loading the jQuery JavaScript files directly from the local IIS server*</span></span>
9. <span data-ttu-id="e680b-338">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-338">Close the browser to return to Visual Studio.</span></span> <span data-ttu-id="e680b-339">もう一度、**サイトの .master**ファイルを開き、 **ScriptManager**を見つけます。</span><span class="sxs-lookup"><span data-stu-id="e680b-339">Open the **Site.Master** file again and locate the **ScriptManager**.</span></span> <span data-ttu-id="e680b-340">属性**Enablecdn**プロパティに値**True**を追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-340">Add the attribute **EnableCdn** property with the value **True**.</span></span> <span data-ttu-id="e680b-341">これにより、ローカルサイトの URL からではなく、オンライン URL から jQuery が読み込まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="e680b-341">This will force jQuery to be loaded from the online URL, not from the local site's URL.</span></span>
10. <span data-ttu-id="e680b-342">Visual Studio で [**顧客の詳細] .aspx**を開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-342">Open **CustomerDetails.aspx** in Visual Studio.</span></span> <span data-ttu-id="e680b-343">F5 キーを押してサイトを実行します。</span><span class="sxs-lookup"><span data-stu-id="e680b-343">Press the F5 key to run the site.</span></span> <span data-ttu-id="e680b-344">Internet Explorer が開いたら、F12 キーを押して開発者ツールを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-344">Once Internet Explorer opens, press the F12 key to open the developer tools.</span></span> <span data-ttu-id="e680b-345">**[スクリプト]** タブを選択し、ドロップダウンリストを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-345">Select the **Script** tab, and then take a look at the drop-down list.</span></span> <span data-ttu-id="e680b-346">JQuery JavaScript ファイルはローカルサイトから読み込まれなくなりますが、オンライン jQuery CDN から読み込まれることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-346">Note the jQuery JavaScript files are no longer being loaded from the local site, but rather from the online jQuery CDN.</span></span>

    <span data-ttu-id="e680b-347">![CDN からの jQuery JavaScript ファイルの読み込み](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN からの jQuery JavaScript ファイルの読み込み")</span><span class="sxs-lookup"><span data-stu-id="e680b-347">![Loading the jQuery JavaScript files from the CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "Loading the jQuery JavaScript files from the CDN")</span></span>

    <span data-ttu-id="e680b-348">*CDN からの jQuery JavaScript ファイルの読み込み*</span><span class="sxs-lookup"><span data-stu-id="e680b-348">*Loading the jQuery JavaScript files from the CDN*</span></span>
11. <span data-ttu-id="e680b-349">ブラウザーで [ソースの表示] オプションを使用して、HTML ページのソースコードをもう一度開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-349">Open the HTML page source code again using the View source option in the browser.</span></span> <span data-ttu-id="e680b-350">控えめな検証 ASP.NET を有効にすると、挿入された JavaScript コードがデータ \*属性に置き換えられていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-350">Notice that by enabling the unobtrusive validation ASP.NET has replaced the injected JavaScript code with data- \*attributes.</span></span>

    <span data-ttu-id="e680b-351">![控えめに検証するコード](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "控えめに検証するコード")</span><span class="sxs-lookup"><span data-stu-id="e680b-351">![Unobtrusive validation code](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Unobtrusive validation code")</span></span>

    <span data-ttu-id="e680b-352">*控えめに検証するコード*</span><span class="sxs-lookup"><span data-stu-id="e680b-352">*Unobtrusive validation code*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-353">この例では、データ注釈付きの検証の概要がいくつかの HTML および JavaScript の行に簡略化されています。</span><span class="sxs-lookup"><span data-stu-id="e680b-353">In this example, you saw how a validation summary with Data annotations was simplified to only a few HTML and JavaScript lines.</span></span> <span data-ttu-id="e680b-354">以前は、控えめな検証を行わないと、追加する検証コントロールが増えるにつれて、JavaScript の検証コードが大きくなります。</span><span class="sxs-lookup"><span data-stu-id="e680b-354">Previously, without unobtrusive validation, the more validation controls you add, the bigger your JavaScript validation code will grow.</span></span>

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a><span data-ttu-id="e680b-355">タスク 2-データ注釈を使用してモデルを検証する</span><span class="sxs-lookup"><span data-stu-id="e680b-355">Task 2 - Validating the Model with Data Annotations</span></span>

<span data-ttu-id="e680b-356">ASP.NET 4.5 では、Web フォームのデータ注釈の検証について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-356">ASP.NET 4.5 introduces data annotations validation for Web Forms.</span></span> <span data-ttu-id="e680b-357">各入力に対して検証コントロールを作成するのではなく、モデルクラスで制約を定義し、すべての web アプリケーションで使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-357">Instead of having a validation control on each input, you can now define constraints in your model classes and use them across all your web application.</span></span> <span data-ttu-id="e680b-358">このセクションでは、データ注釈を使用して、顧客の新規/編集フォームを検証する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-358">In this section, you will learn how to use data annotations for validating a new/edit customer form.</span></span>

1. <span data-ttu-id="e680b-359">[**顧客の詳細] .aspx**ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-359">Open **CustomerDetail.aspx** page.</span></span> <span data-ttu-id="e680b-360">**EditItemTemplate**セクションと**insertitemposition**セクションの顧客名と2番目の名前は、RequiredFieldValidator コントロールを使用して検証されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-360">Notice that the customer first name and second name in the **EditItemTemplate** and **InsertItemTemplate** sections are validated using a RequiredFieldValidator controls.</span></span> <span data-ttu-id="e680b-361">各検証コントロールは特定の条件に関連付けられているため、確認する条件として複数の検証コントロールを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-361">Each validator is associated to a particular condition, so you need to include as many validators as conditions to check.</span></span>
2. <span data-ttu-id="e680b-362">Customer モデルクラスを検証するためのデータ注釈を追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-362">Add data annotations to validate the Customer model class.</span></span> <span data-ttu-id="e680b-363">**モデル**フォルダーの**Customer.cs**クラスを開き、データ注釈の属性を使用して各プロパティを*装飾*します。</span><span class="sxs-lookup"><span data-stu-id="e680b-363">Open **Customer.cs** class in the **Model** folder and *decorate* each property using data annotation attributes.</span></span>

    <span data-ttu-id="e680b-364">(コードスニペット- *Web フォーム Ex02-データ注釈*)</span><span class="sxs-lookup"><span data-stu-id="e680b-364">(Code Snippet - *Web Forms Lab - Ex02 - Data Annotations*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > <span data-ttu-id="e680b-365">.NET Framework 4.5 により、既存のデータ注釈のコレクションが拡張されました。</span><span class="sxs-lookup"><span data-stu-id="e680b-365">.NET Framework 4.5 has extended the existing data annotation collection.</span></span> <span data-ttu-id="e680b-366">使用できるデータ注釈の一部を次に示します。 [CreditCard]、[Phone]、[EmailAddress]、[Range]、[Compare]、[Url]、[FileExtensions]、[Required]、 [Key]、[RegularExpression]。</span><span class="sxs-lookup"><span data-stu-id="e680b-366">These are some of the data annotations you can use: [CreditCard], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].</span></span>
    > 
    > <span data-ttu-id="e680b-367">いくつかの使用例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-367">Some usage examples:</span></span>
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > <span data-ttu-id="e680b-369">各属性内に独自のエラーメッセージを定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-369">You can also define your own error messages within each attribute.</span></span>
3. <span data-ttu-id="e680b-370">RequiredFieldValidators**を開き、** FormView コントロールの EditItemTemplate セクションと insertitemposition セクションで、first name フィールドと last name フィールドのすべてのを削除します。</span><span class="sxs-lookup"><span data-stu-id="e680b-370">Open **CustomerDetails.aspx** and remove all the RequiredFieldValidators for the first and last name fields in the in EditItemTemplate and InsertItemTemplate sections of the FormView control.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > <span data-ttu-id="e680b-371">データ注釈を使用する利点の1つは、アプリケーションページで検証ロジックが複製されないことです。</span><span class="sxs-lookup"><span data-stu-id="e680b-371">One advantage of using data annotations is that validation logic is not duplicated in your application pages.</span></span> <span data-ttu-id="e680b-372">モデルに一度定義し、データを操作するすべてのアプリケーションページで使用します。</span><span class="sxs-lookup"><span data-stu-id="e680b-372">You define it once in the model, and use it across all the application pages that manipulate data.</span></span>
4. <span data-ttu-id="e680b-373">[**顧客の詳細] .aspx**分離コードを開き、SaveCustomer メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="e680b-373">Open **CustomerDetails.aspx** code-behind and locate the SaveCustomer method.</span></span> <span data-ttu-id="e680b-374">このメソッドは、新しい顧客を挿入するときに呼び出され、FormView コントロール値から Customer パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-374">This method is called when inserting a new customer and receives the Customer parameter from the FormView control values.</span></span> <span data-ttu-id="e680b-375">ページコントロールとパラメーターオブジェクトの間のマッピングが発生すると、ASP.NET はすべてのデータ注釈属性に対してモデル検証を実行し、ModelState ディクショナリに発生したエラーがある場合はそれを入力します。</span><span class="sxs-lookup"><span data-stu-id="e680b-375">When the mapping between the page controls and the parameter object occurs, ASP.NET will execute the model validation against all the data annotation attributes and fill the ModelState dictionary with the errors encountered, if any.</span></span>

    <span data-ttu-id="e680b-376">ModelState. IsValid は、検証を実行した後、モデルのすべてのフィールドが有効な場合にのみ true を返します。</span><span class="sxs-lookup"><span data-stu-id="e680b-376">The ModelState.IsValid will only return true if all the fields on your model are valid after performing the validation.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. <span data-ttu-id="e680b-377">顧客の詳細 ページの最後に  **Validationsummary** コントロールを追加して、モデルエラーの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-377">Add a **ValidationSummary** control at the end of the CustomerDetails page to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    <span data-ttu-id="e680b-378">**Showmodelstateerrors**は、validationsummary コントロールの新しいプロパティです。 **true**に設定すると、コントロールに modelstate ディクショナリからのエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-378">The **ShowModelStateErrors** is a new property on the ValidationSummary control that when set to **true**, the control will show the errors from the ModelState dictionary.</span></span> <span data-ttu-id="e680b-379">これらのエラーは、データ注釈の検証から取得されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-379">These errors come from the data annotations validation.</span></span>
6. <span data-ttu-id="e680b-380">**F5**キーを押して Web アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="e680b-380">Press **F5** to run the Web application.</span></span> <span data-ttu-id="e680b-381">いくつかの誤った値を指定してフォームに入力し、 **[保存]** をクリックして検証を実行します。</span><span class="sxs-lookup"><span data-stu-id="e680b-381">Complete the form with some erroneous values and click **Save** to execute validation.</span></span> <span data-ttu-id="e680b-382">下部にエラーの概要が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-382">Notice the error summary at the bottom.</span></span>

    <span data-ttu-id="e680b-383">![データ注釈を使用した検証](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "データ注釈を使用した検証")</span><span class="sxs-lookup"><span data-stu-id="e680b-383">![Validation with Data Annotations](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Validation with Data Annotations")</span></span>

    <span data-ttu-id="e680b-384">*データ注釈を使用した検証*</span><span class="sxs-lookup"><span data-stu-id="e680b-384">*Validation with Data Annotations*</span></span>

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a><span data-ttu-id="e680b-385">タスク 3-ModelState を使用してカスタムデータベースエラーを処理する</span><span class="sxs-lookup"><span data-stu-id="e680b-385">Task 3 - Handling Custom Database Errors with ModelState</span></span>

<span data-ttu-id="e680b-386">以前のバージョンの Web フォームでは、長い文字列や一意のキー違反などのデータベースエラーを処理する場合、リポジトリコードで例外をスローし、コードビハインドで例外を処理してエラーを表示することがあります。</span><span class="sxs-lookup"><span data-stu-id="e680b-386">In previous version of Web Forms, handling database errors such as a too long string or a unique key violation could involve throwing exceptions in your repository code and then handling the exceptions on your code-behind to display an error.</span></span> <span data-ttu-id="e680b-387">比較的単純な操作を実行するには、コードの大部分が必要です。</span><span class="sxs-lookup"><span data-stu-id="e680b-387">A great amount of code is required to do something relatively simple.</span></span>

<span data-ttu-id="e680b-388">Web フォーム4.5 では、ModelState オブジェクトを使用して、モデルまたはデータベースから、一貫性のある方法でページのエラーを表示できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-388">In Web Forms 4.5, the ModelState object can be used to display the errors on the page, either from your model or from the database, in a consistent manner.</span></span>

<span data-ttu-id="e680b-389">このタスクでは、データベースの例外を適切に処理し、ModelState オブジェクトを使用してユーザーに適切なメッセージを表示するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-389">In this task, you will add code to properly handle database exceptions and show the appropriate message to the user using the ModelState object.</span></span>

1. <span data-ttu-id="e680b-390">アプリケーションがまだ実行中の場合は、重複する値を使用してカテゴリの名前を更新してみてください。</span><span class="sxs-lookup"><span data-stu-id="e680b-390">While the application is still running, try to update the name of a category using a duplicated value.</span></span>

    <span data-ttu-id="e680b-391">![重複する名前を持つカテゴリの更新](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "重複する名前を持つカテゴリの更新")</span><span class="sxs-lookup"><span data-stu-id="e680b-391">![Updating a category with a duplicated name](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Updating a category with a duplicated name")</span></span>

    <span data-ttu-id="e680b-392">*重複する名前を持つカテゴリの更新*</span><span class="sxs-lookup"><span data-stu-id="e680b-392">*Updating a category with a duplicated name*</span></span>

    <span data-ttu-id="e680b-393">&quot;は、**区分**列の一意の&quot; 制約があるため、例外がスローされることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-393">Notice that an exception is thrown due to the &quot;unique&quot; constraint of the **CategoryName** column.</span></span>

    <span data-ttu-id="e680b-394">![重複するカテゴリ名の例外](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重複するカテゴリ名の例外")</span><span class="sxs-lookup"><span data-stu-id="e680b-394">![Exception for duplicated category names](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Exception for duplicated category names")</span></span>

    <span data-ttu-id="e680b-395">*重複するカテゴリ名の例外*</span><span class="sxs-lookup"><span data-stu-id="e680b-395">*Exception for duplicated category names*</span></span>
2. <span data-ttu-id="e680b-396">デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="e680b-396">Stop debugging.</span></span> <span data-ttu-id="e680b-397">**Products.aspx.cs**分離コードファイルで、 **UpdateCategory**メソッドを更新して、db によってスローされた例外を処理します。SaveChanges () メソッドを呼び出し、 **Modelstate**オブジェクトにエラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-397">In the **Products.aspx.cs** code-behind file, update the **UpdateCategory** method to handle the exceptions thrown by the db.SaveChanges() method call and add an error to the **ModelState** object.</span></span>

    <span data-ttu-id="e680b-398">新しい**TryUpdateModel**メソッドは、ユーザーが指定したフォームデータを使用して、データベースから取得したカテゴリオブジェクトを更新します。</span><span class="sxs-lookup"><span data-stu-id="e680b-398">The new **TryUpdateModel** method updates the category object retrieved from the database using the form data provided by the user.</span></span>

    <span data-ttu-id="e680b-399">(コードスニペット- *Web フォーム Ex02-UpdateCategory Handle エラー*)</span><span class="sxs-lookup"><span data-stu-id="e680b-399">(Code Snippet - *Web Forms Lab - Ex02 - UpdateCategory Handle Errors*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > <span data-ttu-id="e680b-400">理想的には、DbUpdateException の原因を特定し、根本原因が一意キー制約の違反であるかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-400">Ideally, you would have to identify the cause of the DbUpdateException and check if the root cause is the violation of a unique key constraint.</span></span>
3. <span data-ttu-id="e680b-401">**Products**を開き、[カテゴリ] GridView の下に**validationsummary**コントロールを追加して、モデルエラーの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-401">Open **Products.aspx** and add a **ValidationSummary** control below the categories GridView to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. <span data-ttu-id="e680b-402">サイトを実行し、[製品] ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-402">Run the site and go to the Products page.</span></span> <span data-ttu-id="e680b-403">重複する値を使用して、カテゴリの名前を更新してみてください。</span><span class="sxs-lookup"><span data-stu-id="e680b-403">Try to update the name of a category using an duplicated value.</span></span>

    <span data-ttu-id="e680b-404">例外が処理され、 **Validationsummary**コントロールにエラーメッセージが表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-404">Notice that the exception was handled and the error message appears in the **ValidationSummary** control.</span></span>

    <span data-ttu-id="e680b-405">![重複したカテゴリエラー](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "重複したカテゴリエラー")</span><span class="sxs-lookup"><span data-stu-id="e680b-405">![Duplicated category error](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Duplicated category error")</span></span>

    <span data-ttu-id="e680b-406">*重複したカテゴリエラー*</span><span class="sxs-lookup"><span data-stu-id="e680b-406">*Duplicated category error*</span></span>

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a><span data-ttu-id="e680b-407">タスク 4-ASP.NET Web フォーム4.5 での要求の検証</span><span class="sxs-lookup"><span data-stu-id="e680b-407">Task 4 - Request Validation in ASP.NET Web Forms 4.5</span></span>

<span data-ttu-id="e680b-408">ASP.NET の要求検証機能は、クロスサイトスクリプティング (XSS) 攻撃に対して一定レベルの既定の保護を提供します。</span><span class="sxs-lookup"><span data-stu-id="e680b-408">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="e680b-409">以前のバージョンの ASP.NET では、要求の検証は既定で有効になっており、ページ全体に対してのみ無効にすることができました。</span><span class="sxs-lookup"><span data-stu-id="e680b-409">In previous versions of ASP.NET, request validation was enabled by default and could only be disabled for an entire page.</span></span> <span data-ttu-id="e680b-410">新しいバージョンの ASP.NET Web フォームを使用すると、1つのコントロールの要求の検証を無効にしたり、レイジー要求の検証を実行したり、検証されていない要求データにアクセスしたりできます (これを行う場合は注意してください)。</span><span class="sxs-lookup"><span data-stu-id="e680b-410">With the new version of ASP.NET Web Forms you can now disable the request validation for a single control, perform lazy request validation or access un-validated request data (be careful if you do so!).</span></span>

1. <span data-ttu-id="e680b-411">Ctrl キーを押し**ながら F5**キーを押して、デバッグなしでサイトを起動し、[製品] ページにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-411">Press **Ctrl+F5** to start the site without debugging and go to the Products page.</span></span> <span data-ttu-id="e680b-412">カテゴリを選択し、いずれかの製品の **[編集]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-412">Select a category and then click the **Edit** link on any of the products.</span></span>
2. <span data-ttu-id="e680b-413">危険性のあるコンテンツを含む説明を入力します。たとえば、HTML タグを含めます。</span><span class="sxs-lookup"><span data-stu-id="e680b-413">Type a description containing potentially dangerous content, for instance including HTML tags.</span></span> <span data-ttu-id="e680b-414">要求の検証によってスローされた例外を確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-414">Take notice of the exception thrown due to the request validation.</span></span>

    <span data-ttu-id="e680b-415">![危険性のあるコンテンツを含む製品の編集](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "危険性のあるコンテンツを含む製品の編集")</span><span class="sxs-lookup"><span data-stu-id="e680b-415">![Editing a product with potentially dangerous content](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Editing a product with potentially dangerous content")</span></span>

    <span data-ttu-id="e680b-416">*危険性のあるコンテンツを含む製品の編集*</span><span class="sxs-lookup"><span data-stu-id="e680b-416">*Editing a product with potentially dangerous content*</span></span>

    <span data-ttu-id="e680b-417">![要求の検証により例外がスローされました](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "要求の検証により例外がスローされました")</span><span class="sxs-lookup"><span data-stu-id="e680b-417">![Exception thrown due to request validation](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "Exception thrown due to request validation")</span></span>

    <span data-ttu-id="e680b-418">*要求の検証により例外がスローされました*</span><span class="sxs-lookup"><span data-stu-id="e680b-418">*Exception thrown due to request validation*</span></span>
3. <span data-ttu-id="e680b-419">ページを閉じ、Visual Studio で SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="e680b-419">Close the page and, in Visual Studio, press **SHIFT+F5** to stop debugging.</span></span>
4. <span data-ttu-id="e680b-420">**Productdetails .aspx**ページを開き、 **[説明]** ボックスを見つけます。</span><span class="sxs-lookup"><span data-stu-id="e680b-420">Open the **ProductDetails.aspx** page and locate the **Description** TextBox.</span></span>
5. <span data-ttu-id="e680b-421">新しい**ValidateRequestMode**プロパティをテキストボックスに追加し、その値を **[無効]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-421">Add the new **ValidateRequestMode** property to the TextBox and set its value to **Disabled**.</span></span>

    <span data-ttu-id="e680b-422">新しい**ValidateRequestMode**属性を使用すると、各コントロールの要求の検証を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-422">The new **ValidateRequestMode** attribute allows you to disable the request validation granularly on each control.</span></span> <span data-ttu-id="e680b-423">これは、HTML コードを受け取る可能性があるものの、ページの残りの部分では検証の動作を維持する必要がある入力を使用する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="e680b-423">This is useful when you want to use an input that may receive HTML code, but want to keep the validation working for the rest of the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. <span data-ttu-id="e680b-424">**F5**キーを押して web アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="e680b-424">Press **F5** to run the web application.</span></span> <span data-ttu-id="e680b-425">[製品の編集] ページをもう一度開き、HTML タグを含む製品の説明を入力します。</span><span class="sxs-lookup"><span data-stu-id="e680b-425">Open the edit product page again and complete a product description including HTML tags.</span></span> <span data-ttu-id="e680b-426">ここで、説明に HTML コンテンツを追加できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-426">Notice that you can now add HTML content to the description.</span></span>

    <span data-ttu-id="e680b-427">![製品の説明に対して要求の検証が無効になりました](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "製品の説明に対して要求の検証が無効になりました")</span><span class="sxs-lookup"><span data-stu-id="e680b-427">![Request validation disabled for the product description](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Request validation disabled for the product description")</span></span>

    <span data-ttu-id="e680b-428">*製品の説明に対して要求の検証が無効になりました*</span><span class="sxs-lookup"><span data-stu-id="e680b-428">*Request validation disabled for the product description*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-429">実稼働アプリケーションでは、ユーザーが入力した HTML コードをサニタイズして、安全な HTML タグのみが入力されていることを確認する必要があります (たとえば、&lt;スクリプト&gt; タグはありません)。</span><span class="sxs-lookup"><span data-stu-id="e680b-429">In a production application, you should sanitize the HTML code entered by the user to make sure only safe HTML tags are entered (for example, there are no &lt;script&gt; tags).</span></span> <span data-ttu-id="e680b-430">これを行うには、 [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS)を使用します。</span><span class="sxs-lookup"><span data-stu-id="e680b-430">To do this, you can use [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS).</span></span>
7. <span data-ttu-id="e680b-431">製品をもう一度編集します。</span><span class="sxs-lookup"><span data-stu-id="e680b-431">Edit the product again.</span></span> <span data-ttu-id="e680b-432">名前 フィールドに HTML コードを入力し、**保存** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-432">Type HTML code in the Name field and click **Save**.</span></span> <span data-ttu-id="e680b-433">要求の検証は説明フィールドに対してのみ無効になっており、残りのフィールドは危険な可能性のあるコンテンツに対して引き続き検証されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-433">Notice that Request Validation is only disabled for the Description field and the rest of the fields re still validated against the potentially dangerous content.</span></span>

    <span data-ttu-id="e680b-434">![残りのフィールドで、要求の検証が有効になります。](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "残りのフィールドで、要求の検証が有効になります。")</span><span class="sxs-lookup"><span data-stu-id="e680b-434">![Request validation enabled in the rest of the fields](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "Request validation enabled in the rest of the fields")</span></span>

    <span data-ttu-id="e680b-435">*残りのフィールドで、要求の検証が有効になります。*</span><span class="sxs-lookup"><span data-stu-id="e680b-435">*Request validation enabled in the rest of the fields*</span></span>

    <span data-ttu-id="e680b-436">ASP.NET Web フォーム4.5 には、要求の検証を遅延させる新しい要求検証モードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e680b-436">ASP.NET Web Forms 4.5 includes a new request validation mode to perform request validation lazily.</span></span> <span data-ttu-id="e680b-437">要求の検証モードが**4.5**に設定されている場合、コードの一部が ASP.NET *[&quot;key&quot;]* にアクセスすると、フォームコレクション内の特定の要素に対する要求の検証のみがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="e680b-437">With the request validation mode set to **4.5**, if a piece of code accesses *Request.Form[&quot;key&quot;]*, ASP.NET 4.5's request validation will only trigger request validation for that specific element in the form collection.</span></span>

    <span data-ttu-id="e680b-438">さらに、ASP.NET 4.5 には、Microsoft の XSS ライブラリ v4.0 のコアエンコードルーチンが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e680b-438">Additionally, ASP.NET 4.5 now includes core encoding routines from the Microsoft Anti-XSS Library v4.0.</span></span> <span data-ttu-id="e680b-439">XSS 防止エンコードルーチンは、新しい**system.web. web.config**名前空間で検出された新しい*アンチ Xssenプログラマ*型によって実装されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-439">The Anti-XSS encoding routines are implemented by the new *AntiXssEncoder* type found in the new **System.Web.Security.AntiXss** namespace.</span></span> <span data-ttu-id="e680b-440">**EncoderType**パラメーターを使用するように構成されている場合は、ASP.NET 内の*すべての出力*エンコードによって、新しいエンコードルーチンが自動的に使用されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-440">With the **encoderType** parameter configured to use *AntiXssEncoder*, all output encoding within ASP.NET automatically uses the new encoding routines.</span></span>
8. <span data-ttu-id="e680b-441">ASP.NET 4.5 要求の検証では、要求データへの検証されていないアクセスもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e680b-441">ASP.NET 4.5 request validation also supports un-validated access to request data.</span></span> <span data-ttu-id="e680b-442">ASP.NET 4.5 は、**未検証**という**HttpRequest**オブジェクトに新しいコレクションプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-442">ASP.NET 4.5 adds a new collection property to the **HttpRequest** object called **Unvalidated**.</span></span> <span data-ttu-id="e680b-443">**未検証**に移動すると、フォーム、Querystrings、Cookie、url など、要求データのすべての共通部分にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-443">When you navigate into **HttpRequest.Unvalidated** you have access to all of the common pieces of request data, including Forms, QueryStrings, Cookies, URLs, and so on.</span></span>

    <span data-ttu-id="e680b-444">![未検証オブジェクト](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "未検証オブジェクト")</span><span class="sxs-lookup"><span data-stu-id="e680b-444">![Request.Unvalidated object](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated object")</span></span>

    <span data-ttu-id="e680b-445">*未検証オブジェクト*</span><span class="sxs-lookup"><span data-stu-id="e680b-445">*Request.Unvalidated object*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-446">**未検証プロパティは注意して使用してください。**</span><span class="sxs-lookup"><span data-stu-id="e680b-446">**Please use the HttpRequest.Unvalidated property with caution!**</span></span> <span data-ttu-id="e680b-447">生の要求データに対してカスタム検証を慎重に実行して、危険なテキストがラウンドトリップされず、疑いのない顧客に返されることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-447">Make sure you carefully perform custom validation on the raw request data to ensure that dangerous text is not round-tripped and rendered back to unsuspecting customers!</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a><span data-ttu-id="e680b-448">演習 3: ASP.NET Web フォームでの非同期ページ処理</span><span class="sxs-lookup"><span data-stu-id="e680b-448">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>

<span data-ttu-id="e680b-449">この演習では、ASP.NET Web フォームの新しい非同期ページ処理機能について紹介します。</span><span class="sxs-lookup"><span data-stu-id="e680b-449">In this exercise, you will be introduced to the new asynchronous page processing features in ASP.NET Web Forms.</span></span>

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a><span data-ttu-id="e680b-450">タスク 1-[製品の詳細] ページを更新してイメージをアップロードして表示する</span><span class="sxs-lookup"><span data-stu-id="e680b-450">Task 1 - Updating the Product Details Page to Upload and Show Images</span></span>

<span data-ttu-id="e680b-451">このタスクでは、製品の詳細ページを更新して、ユーザーが製品のイメージの URL を指定し、読み取り専用のビューに表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e680b-451">In this task, you will update the product details page to allow the user to specify an image URL for the product and display it in the read-only view.</span></span> <span data-ttu-id="e680b-452">指定されたイメージを同期的にダウンロードして、ローカルコピーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e680b-452">You will create a local copy of the specified image by downloading it synchronously.</span></span> <span data-ttu-id="e680b-453">次のタスクでは、この実装を更新して非同期的に動作するようにします。</span><span class="sxs-lookup"><span data-stu-id="e680b-453">In the next task, you will update this implementation to make it work asynchronously.</span></span>

1. <span data-ttu-id="e680b-454">**Visual Studio 2012**を開き、このラボのフォルダーから**開始**して、ソースにある**begin**ソリューションを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="e680b-454">Open **Visual Studio 2012** and load the **Begin** solution located in **Source\Ex3-Async\Begin** from this lab's folder.</span></span> <span data-ttu-id="e680b-455">または、前の演習の既存のソリューションで作業を続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-455">Alternatively, you can continue working on your existing solution from the previous exercises.</span></span>

   1. <span data-ttu-id="e680b-456">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-456">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e680b-457">これを行うには、ソリューションエクスプローラーで、 **[Webフォームラボ]** プロジェクトをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e680b-457">To do this, in the Solution Explorer, click the **WebFormsLab** project and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e680b-458">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-458">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e680b-459">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="e680b-459">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e680b-460">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="e680b-460">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e680b-461">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-461">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e680b-462">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-462">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e680b-463">**Productdetails .aspx**ページソースを開き、FormView の ItemTemplate にフィールドを追加して、製品の画像を表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-463">Open the **ProductDetails.aspx** page source and add a field in the FormView's ItemTemplate to show the product image.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. <span data-ttu-id="e680b-464">フィールドを追加して、FormView の EditTemplate に画像の URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-464">Add a field to specify the image URL in the FormView's EditTemplate.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. <span data-ttu-id="e680b-465">**ProductDetails.aspx.cs**分離コードファイルを開き、次の名前空間ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-465">Open the **ProductDetails.aspx.cs** code-behind file and add the following namespace directives.</span></span>

    <span data-ttu-id="e680b-466">(コードスニペット- *Web フォーム Ex03-名前空間*)</span><span class="sxs-lookup"><span data-stu-id="e680b-466">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. <span data-ttu-id="e680b-467">リモートイメージをローカル**イメージ**フォルダーに格納する**UpdateProductImage**メソッドを作成し、[新しいイメージの場所] の値を使用して product エンティティを更新します。</span><span class="sxs-lookup"><span data-stu-id="e680b-467">Create an **UpdateProductImage** method to store remote images in the local **Images** folder and update the product entity with the new image location value.</span></span>

    <span data-ttu-id="e680b-468">(コードスニペット- *Web フォーム Ex03-UpdateProductImage*)</span><span class="sxs-lookup"><span data-stu-id="e680b-468">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. <span data-ttu-id="e680b-469">**UpdateProductImage**メソッドを呼び出すように**updateproduct**メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="e680b-469">Update the **UpdateProduct** method to call the **UpdateProductImage** method.</span></span>

    <span data-ttu-id="e680b-470">(コードスニペット- *Web フォーム Ex03-UpdateProductImage 呼び出し*)</span><span class="sxs-lookup"><span data-stu-id="e680b-470">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Call*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. <span data-ttu-id="e680b-471">アプリケーションを実行して、製品のイメージをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-471">Run the application and try to upload an image for a product.</span></span> <span data-ttu-id="e680b-472">たとえば、Office クリップアートから次の画像の URL を使用できます: [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span><span class="sxs-lookup"><span data-stu-id="e680b-472">For example, you can use the following image URL from Office Clip Arts: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span></span>

    <span data-ttu-id="e680b-473">![製品のイメージの設定](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "製品のイメージの設定")</span><span class="sxs-lookup"><span data-stu-id="e680b-473">![Setting an image for a product](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Setting an image for a product")</span></span>

    <span data-ttu-id="e680b-474">*製品のイメージの設定*</span><span class="sxs-lookup"><span data-stu-id="e680b-474">*Setting an image for a product*</span></span>

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a><span data-ttu-id="e680b-475">タスク 2-[製品の詳細] ページに非同期処理を追加する</span><span class="sxs-lookup"><span data-stu-id="e680b-475">Task 2 - Adding Asynchronous Processing to the Product Details Page</span></span>

<span data-ttu-id="e680b-476">このタスクでは、[製品の詳細] ページを更新して、非同期で動作するようにします。</span><span class="sxs-lookup"><span data-stu-id="e680b-476">In this task, you will update the product details page to make it work asynchronously.</span></span> <span data-ttu-id="e680b-477">ASP.NET 4.5 の非同期ページ処理を使用して、実行時間の長いタスク (イメージのダウンロードプロセス) を強化します。</span><span class="sxs-lookup"><span data-stu-id="e680b-477">You will enhance a long running task - the image download process - by using ASP.NET 4.5 asynchronous page processing.</span></span>

<span data-ttu-id="e680b-478">Web アプリケーションの非同期メソッドは、ASP.NET スレッドプールの使用方法を最適化するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-478">Asynchronous methods in web applications can be used to optimize the way ASP.NET thread pools are used.</span></span> <span data-ttu-id="e680b-479">ASP.NET では、要求に参加するためのスレッドの数には制限があります。したがって、すべてのスレッドがビジー状態になると、ASP.NET は新しい要求を拒否し、アプリケーションエラーメッセージを送信して、サイトを使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="e680b-479">In ASP.NET there are a limited number of threads in the thread pool for attending requests, thus, when all the threads are busy, ASP.NET starts to reject new requests, sends application error messages and makes your site unavailable.</span></span>

<span data-ttu-id="e680b-480">Web サイトでの時間のかかる操作は、割り当てられたスレッドを長時間にわたって占有するため、非同期プログラミングに適しています。</span><span class="sxs-lookup"><span data-stu-id="e680b-480">Time-consuming operations on your web site are great candidates for asynchronous programming because they occupy the assigned thread for a long time.</span></span> <span data-ttu-id="e680b-481">これには、データベースに対するクエリや外部 web サーバーへのアクセスなど、オフライン操作を必要とする多数の異なる要素やページを含むページが長時間要求されることが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e680b-481">This includes long running requests, pages with lots of different elements and pages that require offline operations, such querying a database or accessing an external web server.</span></span> <span data-ttu-id="e680b-482">これらの操作に非同期メソッドを使用すると、ページの処理中にスレッドが解放されてスレッドプールに戻され、新しいページ要求への参加に使用できるという利点があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-482">The advantage is that if you use asynchronous methods for these operations, while the page is processing, the thread is freed and returned to the thread pool and can be used to attend to a new page request.</span></span> <span data-ttu-id="e680b-483">つまり、ページはスレッドプールからの1つのスレッドで処理を開始し、非同期処理が完了すると、別のスレッドで処理が完了する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-483">This means, the page will start processing in one thread from the thread pool and might complete processing in a different one, after the async processing completes.</span></span>

1. <span data-ttu-id="e680b-484">**Productdetails .aspx**ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-484">Open the **ProductDetails.aspx** page.</span></span> <span data-ttu-id="e680b-485">**Async**属性を**Page**要素に追加し、 **true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="e680b-485">Add the **Async** attribute in the **Page** element and set it to **true**.</span></span> <span data-ttu-id="e680b-486">この属性は、IHttpAsyncHandler インターフェイスを実装するように ASP.NET に指示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-486">This attribute tells ASP.NET to implement the IHttpAsyncHandler interface.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. <span data-ttu-id="e680b-487">ページの下部にラベルを追加すると、ページを実行しているスレッドの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-487">Add a Label at the bottom of the page to show the details of the threads running the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. <span data-ttu-id="e680b-488">**ProductDetails.aspx.cs**を開き、次の名前空間ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-488">Open up **ProductDetails.aspx.cs** and add the following namespace directives.</span></span>

    <span data-ttu-id="e680b-489">(コードスニペット- *Web フォーム Ex03-名前空間 2*)</span><span class="sxs-lookup"><span data-stu-id="e680b-489">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. <span data-ttu-id="e680b-490">非同期タスクを使用してイメージをダウンロードするように**UpdateProductImage**メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="e680b-490">Modify the **UpdateProductImage** method to download the image with an asynchronous task.</span></span> <span data-ttu-id="e680b-491">**WebClient** **Downloadfile**メソッドを**downloadfiletaskasync**メソッドに置き換え、 **await**キーワードを含めます。</span><span class="sxs-lookup"><span data-stu-id="e680b-491">You will replace the **WebClient** **DownloadFile** method with the **DownloadFileTaskAsync** method and include the **await** keyword.</span></span>

    <span data-ttu-id="e680b-492">(コードスニペット- *Web フォーム Ex03-UpdateProductImage Async*)</span><span class="sxs-lookup"><span data-stu-id="e680b-492">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Async*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    <span data-ttu-id="e680b-493">RegisterAsyncTask は、別のスレッドで実行される新しいページ非同期タスクを登録します。</span><span class="sxs-lookup"><span data-stu-id="e680b-493">The RegisterAsyncTask registers a new page asynchronous task to be executed in a different thread.</span></span> <span data-ttu-id="e680b-494">このメソッドは、実行するタスク (t) を含むラムダ式を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-494">It receives a lambda expression with the Task (t) to be executed.</span></span> <span data-ttu-id="e680b-495">**Downloadfiletaskasync**メソッドの**await**キーワードは、 **downloadfiletaskasync**メソッドが完了した後に非同期的に呼び出されるコールバックにメソッドの残りの部分を変換します。</span><span class="sxs-lookup"><span data-stu-id="e680b-495">The **await** keyword in the **DownloadFileTaskAsync** method converts the remainder of the method into a callback that is invoked asynchronously after the **DownloadFileTaskAsync** method has completed.</span></span> <span data-ttu-id="e680b-496">ASP.NET は、すべての HTTP 要求の元の値を自動的に維持することで、メソッドの実行を再開します。</span><span class="sxs-lookup"><span data-stu-id="e680b-496">ASP.NET will resume the execution of the method by automatically maintaining all the HTTP request original values.</span></span> <span data-ttu-id="e680b-497">.NET 4.5 の新しい非同期プログラミングモデルを使用すると、同期コードと非常によく似た非同期コードを記述し、コンパイラがコールバック関数または継続コードの複雑さを処理できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-497">The new asynchronous programming model in .NET 4.5 enables you to write asynchronous code that looks very much like synchronous code, and let the compiler handle the complications of callback functions or continuation code.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e680b-498">RegisterAsyncTask と PageAsyncTask は、.NET 2.0 以降で既に利用できました。</span><span class="sxs-lookup"><span data-stu-id="e680b-498">RegisterAsyncTask and PageAsyncTask were already available since .NET 2.0.</span></span> <span data-ttu-id="e680b-499">Await キーワードは、.NET 4.5 の非同期プログラミングモデルの新しいものであり、.NET WebClient オブジェクトの新しい TaskAsync メソッドと共に使用できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-499">The await keyword is new from the .NET 4.5 asynchronous programming model and can be used together with the new TaskAsync methods from the .NET WebClient object.</span></span>
5. <span data-ttu-id="e680b-500">コードを追加して、コードが開始され、実行が完了したスレッドを表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-500">Add code to display the threads on which the code started and finished executing.</span></span> <span data-ttu-id="e680b-501">これを行うには、次のコードを使用して**UpdateProductImage**メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="e680b-501">To do this, update the **UpdateProductImage** method with the following code.</span></span>

    <span data-ttu-id="e680b-502">(コードスニペット- *Web フォーム Ex03-スレッドの表示*)</span><span class="sxs-lookup"><span data-stu-id="e680b-502">(Code Snippet - *Web Forms Lab - Ex03 - Show threads*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. <span data-ttu-id="e680b-503">**Web サイトの web.config ファイルを**開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-503">Open the web site's **Web.config** file.</span></span> <span data-ttu-id="e680b-504">次の appSetting 変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="e680b-504">Add the following appSetting variable.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. <span data-ttu-id="e680b-505">**F5**キーを押してアプリケーションを実行し、製品のイメージをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-505">Press **F5** to run the application and upload an image for the product.</span></span> <span data-ttu-id="e680b-506">コードが開始および終了したスレッド ID が異なる場合があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-506">Notice the threads ID where the code started and finished may be different.</span></span> <span data-ttu-id="e680b-507">これは、非同期タスクは ASP.NET スレッドプールとは別のスレッドで実行されるためです。</span><span class="sxs-lookup"><span data-stu-id="e680b-507">This is because asynchronous tasks run on a separate thread from ASP.NET thread pool.</span></span> <span data-ttu-id="e680b-508">タスクが完了すると、ASP.NET はタスクをキューに戻し、使用可能なすべてのスレッドを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="e680b-508">When the task completes, ASP.NET puts the task back in the queue and assigns any of the available threads.</span></span>

    <span data-ttu-id="e680b-509">![画像を非同期的にダウンロードする](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "画像を非同期的にダウンロードする")</span><span class="sxs-lookup"><span data-stu-id="e680b-509">![Downloading an image asynchronously](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Downloading an image asynchronously")</span></span>

    <span data-ttu-id="e680b-510">*画像を非同期的にダウンロードする*</span><span class="sxs-lookup"><span data-stu-id="e680b-510">*Downloading an image asynchronously*</span></span>

> [!NOTE]
> <span data-ttu-id="e680b-511">また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Azure にデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-511">Additionally, you can deploy this application to Azure following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="e680b-512">まとめ</span><span class="sxs-lookup"><span data-stu-id="e680b-512">Summary</span></span>

<span data-ttu-id="e680b-513">このハンズオンラボでは、次の概念について説明しました。</span><span class="sxs-lookup"><span data-stu-id="e680b-513">In this hands-on lab, the following concepts have been addressed and demonstrated:</span></span>

- <span data-ttu-id="e680b-514">厳密に型指定されたデータバインディング式を使用する</span><span class="sxs-lookup"><span data-stu-id="e680b-514">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="e680b-515">Web フォームでの新しいモデルバインド機能の使用</span><span class="sxs-lookup"><span data-stu-id="e680b-515">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="e680b-516">ページデータを分離コードメソッドにマップするための値プロバイダーの使用</span><span class="sxs-lookup"><span data-stu-id="e680b-516">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="e680b-517">ユーザー入力の検証にデータ注釈を使用する</span><span class="sxs-lookup"><span data-stu-id="e680b-517">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="e680b-518">Web フォームの jQuery を使用した控えめなクライアント側の検証を活用する</span><span class="sxs-lookup"><span data-stu-id="e680b-518">Take advantage of unobtrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="e680b-519">詳細な要求の検証を実装する</span><span class="sxs-lookup"><span data-stu-id="e680b-519">Implement granular request validation</span></span>
- <span data-ttu-id="e680b-520">Web フォームでの非同期ページ処理の実装</span><span class="sxs-lookup"><span data-stu-id="e680b-520">Implement asynchronous page processing in Web Forms</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="e680b-521">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="e680b-521">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="e680b-522">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-522">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="e680b-523">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-523">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="e680b-524">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e680b-524">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="e680b-525">または、Web Platform Installer が既にインストールされている場合は、それを開いて、 <em>AZURE SDK&quot;で web 用に 2012 Visual Studio Express を</em>検索 &quot;ことができます。</span><span class="sxs-lookup"><span data-stu-id="e680b-525">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="e680b-526">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-526">Click on **Install Now**.</span></span> <span data-ttu-id="e680b-527">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="e680b-527">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="e680b-528">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="e680b-528">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="e680b-529">![Visual Studio Express のインストール](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="e680b-529">![Install Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="e680b-530">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="e680b-530">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="e680b-531">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="e680b-531">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    <span data-ttu-id="e680b-533">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="e680b-533">*Accepting the license terms*</span></span>
5. <span data-ttu-id="e680b-534">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="e680b-534">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    <span data-ttu-id="e680b-536">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="e680b-536">*Installation progress*</span></span>
6. <span data-ttu-id="e680b-537">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-537">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    <span data-ttu-id="e680b-539">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="e680b-539">*Installation completed*</span></span>
7. <span data-ttu-id="e680b-540">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="e680b-540">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="e680b-541">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-541">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    <span data-ttu-id="e680b-543">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="e680b-543">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e680b-544">付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="e680b-544">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="e680b-545">この付録では、azure によって提供される Web 配置公開機能を活用して、Azure Portal から新しい web サイトを作成し、取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-545">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="e680b-546">タスク 1-Azure Portal から新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="e680b-546">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="e680b-547">[Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="e680b-547">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-548">Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-548">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="e680b-549">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-549">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="e680b-550">![Windows Azure portal にログオンします。](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="e680b-550">![Log on to Windows Azure portal](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="e680b-551">*ポータルへのログオン*</span><span class="sxs-lookup"><span data-stu-id="e680b-551">*Log on to the Portal*</span></span>
2. <span data-ttu-id="e680b-552">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-552">Click **New** on the command bar.</span></span>

    <span data-ttu-id="e680b-553">![新しい Web サイトの作成](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="e680b-553">![Creating a new Web Site](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="e680b-554">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="e680b-554">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="e680b-555">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-555">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="e680b-556">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="e680b-556">Then select **Quick Create** option.</span></span> <span data-ttu-id="e680b-557">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-557">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-558">Azure は、管理および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="e680b-558">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="e680b-559">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Azure にデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="e680b-559">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="e680b-560">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="e680b-560">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="e680b-561">![簡易作成を使用した新しい Web サイトの作成](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="e680b-561">![Creating a new Web Site using Quick Create](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="e680b-562">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="e680b-562">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="e680b-563">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="e680b-563">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="e680b-564">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-564">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="e680b-565">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-565">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="e680b-566">![新しい web サイトを参照しています](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="e680b-566">![Browsing to the new web site](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="e680b-567">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="e680b-567">*Browsing to the new web site*</span></span>

    <span data-ttu-id="e680b-568">![実行中の Web サイト](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="e680b-568">![Web site running](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Web site running")</span></span>

    <span data-ttu-id="e680b-569">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="e680b-569">*Web site running*</span></span>
6. <span data-ttu-id="e680b-570">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="e680b-570">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="e680b-571">![Web サイトの管理ページを開く](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="e680b-571">![Opening the web site management pages](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="e680b-572">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="e680b-572">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="e680b-573">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-573">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-574">*発行プロファイル*には、有効になっている各発行方法について、Azure に web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e680b-574">The *publish profile* contains all of the information required to publish a web application to Azure for each enabled publication method.</span></span> <span data-ttu-id="e680b-575">発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e680b-575">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="e680b-576">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Azure に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e680b-576">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="e680b-577">![Web サイト発行プロファイルをダウンロードしています](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="e680b-577">![Downloading the web site publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="e680b-578">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="e680b-578">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="e680b-579">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="e680b-579">Download the publish profile file to a known location.</span></span> <span data-ttu-id="e680b-580">この演習では、このファイルを使用して Visual Studio から Azure に web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e680b-580">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="e680b-581">![発行プロファイルファイルを保存しています](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="e680b-581">![Saving the publish profile file](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Saving the publish profile")</span></span>

    <span data-ttu-id="e680b-582">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="e680b-582">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="e680b-583">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="e680b-583">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="e680b-584">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-584">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="e680b-585">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-585">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="e680b-586">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="e680b-586">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="e680b-587">Azure 管理ポータルのサブスクリプションから**SQL Database サーバーを**表示するには、 **SQL データベース** | サーバー | **サーバーのダッシュボード**を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e680b-587">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="e680b-588">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-588">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="e680b-589">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="e680b-589">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="e680b-590">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="e680b-590">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="e680b-591">![SQL Database サーバーダッシュボード](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="e680b-591">![SQL Database Server Dashboard](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="e680b-592">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="e680b-592">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="e680b-593">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="e680b-593">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="e680b-594">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-594">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    <span data-ttu-id="e680b-596">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="e680b-596">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="e680b-597">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="e680b-597">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    <span data-ttu-id="e680b-599">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="e680b-599">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e680b-600">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="e680b-600">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="e680b-601">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="e680b-601">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="e680b-602">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e680b-602">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="e680b-603">![アプリケーションの発行](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="e680b-603">![Publishing the Application](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Publishing the Application")</span></span>

    <span data-ttu-id="e680b-604">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="e680b-604">*Publishing the web site*</span></span>
2. <span data-ttu-id="e680b-605">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="e680b-605">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="e680b-606">![発行プロファイルをインポートしています](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="e680b-606">![Importing the publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Importing the publish profile")</span></span>

    <span data-ttu-id="e680b-607">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="e680b-607">*Importing publish profile*</span></span>
3. <span data-ttu-id="e680b-608">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-608">Click **Validate Connection**.</span></span> <span data-ttu-id="e680b-609">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-609">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e680b-610">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-610">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="e680b-611">![接続の検証](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="e680b-611">![Validating connection](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Validating connection")</span></span>

    <span data-ttu-id="e680b-612">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="e680b-612">*Validating connection*</span></span>
4. <span data-ttu-id="e680b-613">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-613">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="e680b-614">![Web deploy の構成](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="e680b-614">![Web deploy configuration](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy configuration")</span></span>

    <span data-ttu-id="e680b-615">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="e680b-615">*Web deploy configuration*</span></span>
5. <span data-ttu-id="e680b-616">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="e680b-616">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="e680b-617">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="e680b-617">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="e680b-618">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="e680b-618">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="e680b-619">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="e680b-619">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="e680b-620">新しいデータベース名を入力します。</span><span class="sxs-lookup"><span data-stu-id="e680b-620">Type a new database name.</span></span>

     <span data-ttu-id="e680b-621">![変換先の接続文字列を構成しています](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="e680b-621">![Configuring destination connection string](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="e680b-622">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="e680b-622">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="e680b-623">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="e680b-623">Then click **OK**.</span></span> <span data-ttu-id="e680b-624">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-624">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="e680b-625">![データベースの作成](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="e680b-625">![Creating the database](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Creating the database string")</span></span>

    <span data-ttu-id="e680b-626">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="e680b-626">*Creating the database*</span></span>
7. <span data-ttu-id="e680b-627">Azure で SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-627">The connection string you will use to connect to SQL Database in Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="e680b-628">続けて、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-628">Then click **Next**.</span></span>

    <span data-ttu-id="e680b-629">![SQL Database を指す接続文字列](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="e680b-629">![Connection string pointing to SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="e680b-630">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="e680b-630">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="e680b-631">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-631">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="e680b-632">![Web アプリケーションの発行](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="e680b-632">![Publishing the web application](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Publishing the web application")</span></span>

    <span data-ttu-id="e680b-633">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="e680b-633">*Publishing the web application*</span></span>
9. <span data-ttu-id="e680b-634">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-634">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="e680b-635">付録 C: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="e680b-635">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="e680b-636">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="e680b-636">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="e680b-637">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="e680b-637">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="e680b-638">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="e680b-638">![Using Visual Studio code snippets to insert code into your project](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="e680b-639">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="e680b-639">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="e680b-640">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="e680b-640">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="e680b-641">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="e680b-641">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="e680b-642">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="e680b-642">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="e680b-643">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-643">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="e680b-644">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="e680b-644">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="e680b-645">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="e680b-645">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="e680b-646">![スニペット名の入力を開始します](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="e680b-646">![Start typing the snippet name](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Start typing the snippet name")</span></span>

<span data-ttu-id="e680b-647">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="e680b-647">*Start typing the snippet name*</span></span>

<span data-ttu-id="e680b-648">![Tab キーを押して、強調表示されているスニペットを選択します](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="e680b-648">![Press Tab to select the highlighted snippet](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="e680b-649">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="e680b-649">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="e680b-650">![もう一度 Tab キーを押すと、スニペットが展開されます。](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="e680b-650">![Press Tab again and the snippet will expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="e680b-651">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="e680b-651">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="e680b-652">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="e680b-652">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="e680b-653">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="e680b-653">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="e680b-654">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="e680b-654">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="e680b-655">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="e680b-655">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="e680b-656">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="e680b-656">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="e680b-657">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="e680b-657">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="e680b-658">![一覧から関連するスニペットをクリックして選択します。](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="e680b-658">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="e680b-659">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="e680b-659">*Pick the relevant snippet from the list, by clicking on it*</span></span>
