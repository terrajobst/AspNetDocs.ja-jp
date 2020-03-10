---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API のヘルプページを作成する-ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、ASP.NET 4.x で ASP.NET Web API 用のヘルプページを作成する方法を示します。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448618"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="bdd12-103">ASP.NET Web API のヘルプページの作成</span><span class="sxs-lookup"><span data-stu-id="bdd12-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="bdd12-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bdd12-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bdd12-105">このチュートリアルでは、ASP.NET 4.x で ASP.NET Web API 用のヘルプページを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="bdd12-106">Web API を作成するときは、多くの場合、他の開発者が API の呼び出し方法を理解できるように、ヘルプページを作成すると便利です。</span><span class="sxs-lookup"><span data-stu-id="bdd12-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="bdd12-107">すべてのドキュメントを手動で作成することもできますが、可能な限り自動生成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bdd12-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="bdd12-108">このタスクを簡単にするために、ASP.NET Web API では、実行時に自動生成ヘルプページ用のライブラリが用意されています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="bdd12-109">API ヘルプページの作成</span><span class="sxs-lookup"><span data-stu-id="bdd12-109">Creating API Help Pages</span></span>

<span data-ttu-id="bdd12-110">[ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="bdd12-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="bdd12-111">この更新プログラムは、ヘルプページを Web API プロジェクトテンプレートに統合します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="bdd12-112">次に、新しい ASP.NET MVC 4 プロジェクトを作成し、[Web API プロジェクト] テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="bdd12-113">プロジェクトテンプレートは、`ValuesController`という名前の API コントローラーの例を作成します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="bdd12-114">このテンプレートは、API のヘルプページも作成します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-114">The template also creates the API help pages.</span></span> <span data-ttu-id="bdd12-115">ヘルプページのすべてのコードファイルは、プロジェクトの [区分] フォルダーに配置されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="bdd12-116">アプリケーションを実行すると、ホームページに API ヘルプページへのリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="bdd12-117">ホームページから、相対パスは/helpになります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="bdd12-118">このリンクを使用すると、API の概要ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="bdd12-119">このページの MVC ビューは、Areas/HelpPage/Views/Help/Index. cshtml で定義されています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="bdd12-120">このページを編集して、レイアウト、概要、タイトル、スタイルなどを変更できます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="bdd12-121">ページの主要な部分は、コントローラー別にグループ化された Api のテーブルです。</span><span class="sxs-lookup"><span data-stu-id="bdd12-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="bdd12-122">テーブルエントリは、 **Iapiexplorer**インターフェイスを使用して動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="bdd12-123">(このインターフェイスについては後で詳しく説明します)。新しい API コントローラーを追加すると、テーブルは実行時に自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="bdd12-124">[API] 列には、HTTP メソッドと相対 URI が一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="bdd12-125">[説明] 列には、各 API のドキュメントが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="bdd12-126">最初に、ドキュメントはプレースホルダーテキストにすぎません。</span><span class="sxs-lookup"><span data-stu-id="bdd12-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="bdd12-127">次のセクションでは、XML コメントからドキュメントを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="bdd12-128">各 API には、要求や応答の本文など、詳細な情報が記載されたページへのリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="bdd12-129">既存のプロジェクトへのヘルプページの追加</span><span class="sxs-lookup"><span data-stu-id="bdd12-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="bdd12-130">NuGet パッケージマネージャーを使用して、既存の Web API プロジェクトにヘルプページを追加できます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="bdd12-131">このオプションは、"Web API" テンプレートとは別のプロジェクトテンプレートから開始する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="bdd12-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="bdd12-132">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="bdd12-133">[[パッケージマネージャーコンソール](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)] ウィンドウで、次のいずれかのコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="bdd12-134">**C#** アプリケーションの場合: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="bdd12-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="bdd12-135">**Visual Basic**アプリケーションの場合: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="bdd12-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="bdd12-136">パッケージは2つあります。 C# 1 つは Visual Basic 用、もう1つは1つです。</span><span class="sxs-lookup"><span data-stu-id="bdd12-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="bdd12-137">プロジェクトに一致するものを使用してください。</span><span class="sxs-lookup"><span data-stu-id="bdd12-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="bdd12-138">このコマンドは、必要なアセンブリをインストールし、ヘルプページの MVC ビューを追加します (区分/ヘルプページフォルダーにあります)。</span><span class="sxs-lookup"><span data-stu-id="bdd12-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="bdd12-139">ヘルプページへのリンクを手動で追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="bdd12-140">URI は/helpです。</span><span class="sxs-lookup"><span data-stu-id="bdd12-140">The URI is /Help.</span></span> <span data-ttu-id="bdd12-141">Razor ビューでリンクを作成するには、次のように追加します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="bdd12-142">また、領域を登録してください。</span><span class="sxs-lookup"><span data-stu-id="bdd12-142">Also, make sure to register areas.</span></span> <span data-ttu-id="bdd12-143">Global.asax ファイルで、次のコードを**アプリケーション\_Start**メソッドに追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="bdd12-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="bdd12-144">API ドキュメントの追加</span><span class="sxs-lookup"><span data-stu-id="bdd12-144">Adding API Documentation</span></span>

<span data-ttu-id="bdd12-145">既定では、ヘルプページにドキュメントのプレースホルダー文字列があります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="bdd12-146">[XML ドキュメントコメント](https://msdn.microsoft.com/library/b2s063f7.aspx)を使用して、ドキュメントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="bdd12-147">この機能を有効にするには、[ファイルエリア]、[ヘルプ] ページ、[アプリ] の順に開き、[Start/\_] を開き、次の行をコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="bdd12-148">ここで XML ドキュメントを有効にします。</span><span class="sxs-lookup"><span data-stu-id="bdd12-148">Now enable XML documentation.</span></span> <span data-ttu-id="bdd12-149">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="bdd12-150">**[ビルド]** ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="bdd12-151">**[出力]** で、 **[XML ドキュメントファイル]** を確認します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="bdd12-152">[編集] ボックスに「App\_Data/XmlDocument .xml」と入力します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="bdd12-153">次に、/Controllers/ValuesController.cs. で定義されている `ValuesController` API コントローラーのコードを開きます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="bdd12-154">いくつかのドキュメントコメントをコントローラーメソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="bdd12-155">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="bdd12-156">ヒント: メソッドの上の行にカレットを置き、3つのスラッシュを入力すると、Visual Studio によって自動的に XML 要素が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="bdd12-157">次に、空白を入力します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="bdd12-158">次に、アプリケーションを再度ビルドして実行し、ヘルプページに移動します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="bdd12-159">ドキュメント文字列が API テーブルに表示されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="bdd12-160">ヘルプページは、実行時に XML ファイルから文字列を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="bdd12-161">(アプリケーションを配置するときは、必ず XML ファイルを展開してください)。</span><span class="sxs-lookup"><span data-stu-id="bdd12-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="bdd12-162">しくみ</span><span class="sxs-lookup"><span data-stu-id="bdd12-162">Under the Hood</span></span>

<span data-ttu-id="bdd12-163">ヘルプページは、Web API フレームワークの一部である**Apiexplorer**クラスの上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="bdd12-164">**Apiexplorer**クラスは、ヘルプページを作成するための未加工のマテリアルを提供します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="bdd12-165">API ごとに、 **Apiexplorer**に api を説明する**apiexplorer**が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="bdd12-166">このため、"API" は HTTP メソッドと相対 URI の組み合わせとして定義されています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="bdd12-167">たとえば、次の Api があります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="bdd12-168">Api/製品を入手</span><span class="sxs-lookup"><span data-stu-id="bdd12-168">GET /api/Products</span></span>
- <span data-ttu-id="bdd12-169">GET /api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="bdd12-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="bdd12-170">投稿/Api/製品</span><span class="sxs-lookup"><span data-stu-id="bdd12-170">POST /api/Products</span></span>

<span data-ttu-id="bdd12-171">コントローラーアクションで複数の HTTP メソッドがサポートされている場合、 **Apiexplorer**は各メソッドを個別の API として扱います。</span><span class="sxs-lookup"><span data-stu-id="bdd12-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="bdd12-172">**Apiexplorer**から API を非表示にするには、アクションに**ApiExplorerSettings**属性を追加し、 *ignoreapi*を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="bdd12-173">コントローラー全体を除外するために、コントローラーにこの属性を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="bdd12-174">ApiExplorer クラスは、 **Idocumentation プロバイダー**インターフェイスからドキュメント文字列を取得します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="bdd12-175">既に説明したように、ヘルプページライブラリには、XML ドキュメント文字列からドキュメントを取得する**Idocumentation プロバイダー**が用意されています。</span><span class="sxs-lookup"><span data-stu-id="bdd12-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="bdd12-176">このコードは/Areas/HelpPage/XmlDocumentationProvider.cs. にあります。</span><span class="sxs-lookup"><span data-stu-id="bdd12-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="bdd12-177">独自の**Idocumentation プロバイダー**を作成することによって、別のソースからドキュメントを取得できます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="bdd12-178">これを行うには、 **HelpPageConfigurationExtensions**で定義されている**setdocumentation provider**拡張メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="bdd12-179">**Apiexplorer**は、 **idocumentation プロバイダー**インターフェイスを自動的に呼び出し、各 API のドキュメント文字列を取得します。</span><span class="sxs-lookup"><span data-stu-id="bdd12-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="bdd12-180">これらは、 **apidescription**オブジェクトと**apiparameterdescription**オブジェクトの**Documentation**プロパティに格納されます。</span><span class="sxs-lookup"><span data-stu-id="bdd12-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdd12-181">次の手順</span><span class="sxs-lookup"><span data-stu-id="bdd12-181">Next Steps</span></span>

<span data-ttu-id="bdd12-182">ここに表示されているヘルプページには制限がありません。</span><span class="sxs-lookup"><span data-stu-id="bdd12-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="bdd12-183">実際、 **Apiexplorer**はヘルプページの作成に限定されません。</span><span class="sxs-lookup"><span data-stu-id="bdd12-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="bdd12-184">Yao のリンクは、すぐに使えるように、優れたブログ投稿を作成しました。</span><span class="sxs-lookup"><span data-stu-id="bdd12-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="bdd12-185">ASP.NET Web API のヘルプページへの単純なテストクライアントの追加</span><span class="sxs-lookup"><span data-stu-id="bdd12-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="bdd12-186">自己ホスト型サービスでの ASP.NET Web API ヘルプページの作成</span><span class="sxs-lookup"><span data-stu-id="bdd12-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="bdd12-187">ASP.NET Web API 用のヘルプページ (またはクライアント) のデザイン時生成</span><span class="sxs-lookup"><span data-stu-id="bdd12-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="bdd12-188">詳細なヘルプページのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="bdd12-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
