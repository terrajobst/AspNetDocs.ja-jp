---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ヘルプ ページを作成する ASP.NET web API - ASP.NET 4.x
author: MikeWasson
description: コードで、このチュートリアルは、ASP.NET での ASP.NET Web API のヘルプ ページを作成する方法を示しています。 4.x です。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: e3f6a9b8a6835b034a075d580cd9a33136969990
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395018"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="e5a6c-103">ASP.NET Web API のヘルプ ページの作成</span><span class="sxs-lookup"><span data-stu-id="e5a6c-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="e5a6c-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e5a6c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="e5a6c-105">コードで、このチュートリアルは、ASP.NET での ASP.NET Web API のヘルプ ページを作成する方法を示しています。 4.x です。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="e5a6c-106">Web API を作成するときに多くの場合のヘルプ ページを作成すると便利他の開発者は、API を呼び出す方法を認識できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="e5a6c-107">すべてのドキュメントを手動で作成する可能性がありますが、できるだけ多くの自動生成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="e5a6c-108">この作業を容易にするには、ASP.NET Web API は、実行時のヘルプ ページの自動生成するライブラリを提供します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="e5a6c-109">API ヘルプ ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-109">Creating API Help Pages</span></span>

<span data-ttu-id="e5a6c-110">インストール[ASP.NET および Web Tools 2012.2 の Update](https://go.microsoft.com/fwlink/?LinkId=282650)します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="e5a6c-111">この更新プログラムは、Web API プロジェクト テンプレートに、ヘルプ ページを統合します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="e5a6c-112">次に、新しい ASP.NET MVC 4 プロジェクトを作成し、Web API プロジェクト テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="e5a6c-113">プロジェクト テンプレートの作成という名前の API の例のコント ローラーを`ValuesController`します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="e5a6c-114">テンプレートには、API のヘルプ ページも作成します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-114">The template also creates the API help pages.</span></span> <span data-ttu-id="e5a6c-115">すべてのヘルプ ページのコード ファイルは、プロジェクトの [区分] フォルダーに配置されます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="e5a6c-116">アプリケーションを実行すると、ホーム ページには、API ヘルプ ページへのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="e5a6c-117">ホーム ページからは、相対パスは、/Help が。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="e5a6c-118">このリンクでは、API の概要ページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="e5a6c-119">このページの MVC ビューは、Areas/HelpPage/Views/Help/Index.cshtml で定義されます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="e5a6c-120">レイアウト、概要、タイトル、スタイル、およびなどを変更するには、このページを編集することができます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="e5a6c-121">ページの主要部分では、コント ローラーでグループ化された Api のテーブルです。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="e5a6c-122">テーブルのエントリも動的に生成されたを使用して、 **IApiExplorer**インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="e5a6c-123">(説明しますこのインターフェイスについては後で。)新しい API コント ローラーを追加すると、実行時に、テーブルが自動的に更新します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="e5a6c-124">"API"の列には、HTTP メソッドと相対 URI が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="e5a6c-125">「説明」列には、各 API のドキュメントが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="e5a6c-126">最初に、ドキュメントは、プレース ホルダー テキストだけです。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="e5a6c-127">次のセクションでは、XML のコメントからドキュメントを追加する方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="e5a6c-128">各 API では、例の要求および応答の本文を含む、詳細な情報をページにリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="e5a6c-129">既存のプロジェクトに追加のヘルプ ページ</span><span class="sxs-lookup"><span data-stu-id="e5a6c-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="e5a6c-130">ヘルプ ページは、NuGet パッケージ マネージャーを使用して既存の Web API プロジェクトに追加できます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="e5a6c-131">このオプションは、"Web API"テンプレートよりも、別のプロジェクト テンプレートから開始するは便利です。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="e5a6c-132">**ツール**メニューの  **NuGet パッケージ マネージャー**、し、**パッケージ マネージャー コンソール**します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="e5a6c-133">[パッケージ マネージャー コンソール](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)ウィンドウで、次のコマンドのいずれかを入力します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="e5a6c-134">**C#** アプリケーション。 `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="e5a6c-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="e5a6c-135">**Visual Basic**アプリケーション。 `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="e5a6c-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="e5a6c-136">C# と Visual basic の 2 つのパッケージがあります。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="e5a6c-137">プロジェクトに一致する 1 つを使用してください。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="e5a6c-138">このコマンドは、必要なアセンブリをインストールし、(領域/HelpPage フォルダーにあります) のヘルプ ページの MVC ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="e5a6c-139">ヘルプ ページへのリンクを手動で追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="e5a6c-140">URI は、/Help です。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-140">The URI is /Help.</span></span> <span data-ttu-id="e5a6c-141">Razor ビューで、リンクを作成するには、次のように追加します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="e5a6c-142">また、領域を登録することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-142">Also, make sure to register areas.</span></span> <span data-ttu-id="e5a6c-143">Global.asax ファイルで次のコードを追加、**アプリケーション\_開始**メソッドが存在しない場合。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="e5a6c-144">API のドキュメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-144">Adding API Documentation</span></span>

<span data-ttu-id="e5a6c-145">既定では、ヘルプ ページがあるドキュメントのプレース ホルダー文字列。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="e5a6c-146">使用することができます[XML ドキュメント コメント](https://msdn.microsoft.com/library/b2s063f7.aspx)ドキュメントを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="e5a6c-147">この機能を有効にするには、ファイル領域/HelpPage/アプリを開く\_Start/HelpPageConfig.cs、次の行をコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="e5a6c-148">XML ドキュメントを有効にするようになりました。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-148">Now enable XML documentation.</span></span> <span data-ttu-id="e5a6c-149">ソリューション エクスプ ローラーでプロジェクトを右クリックし、選択**プロパティ**します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="e5a6c-150">選択、**ビルド**ページ。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="e5a6c-151">**出力**、確認**XML ドキュメント ファイル**します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="e5a6c-152">編集ボックスで、次のように入力します。"アプリ\_Data/XmlDocument.xml"。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="e5a6c-153">コードを次に、開く、 `ValuesController` /Controllers/ValuesController.cs で定義されている API コント ローラー。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="e5a6c-154">コント ローラーのメソッドには、いくつかのドキュメントのコメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="e5a6c-155">例:</span><span class="sxs-lookup"><span data-stu-id="e5a6c-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="e5a6c-156">ヒント :メソッド上の行にキャレットを配置し、次の 3 つのスラッシュを入力する場合、Visual Studio は自動的に XML 要素を挿入します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="e5a6c-157">空白を入力します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-157">Then you can fill in the blanks.</span></span>


<span data-ttu-id="e5a6c-158">今すぐビルドし、もう一度アプリケーションを実行し、ヘルプ ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="e5a6c-159">API テーブル内のドキュメント文字列が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="e5a6c-160">ヘルプ ページは、実行時に、XML ファイルから文字列を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="e5a6c-161">(アプリケーションを展開するときに必ず XML ファイルをデプロイする。)</span><span class="sxs-lookup"><span data-stu-id="e5a6c-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="e5a6c-162">内部的には</span><span class="sxs-lookup"><span data-stu-id="e5a6c-162">Under the Hood</span></span>

<span data-ttu-id="e5a6c-163">ヘルプ ページがの上に構築された、**ための ApiExplorer**クラスは、Web API フレームワークの一部です。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="e5a6c-164">**ための ApiExplorer**クラスは、ヘルプ ページを作成するため、原材料を提供します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="e5a6c-165">各 api では、**ための ApiExplorer**が含まれています、 **ApiDescription** API を記述します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="e5a6c-166">このため、"API"は、HTTP メソッドと相対 URI の組み合わせとして定義されます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="e5a6c-167">たとえば、異なる Api がいくつか次に示します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="e5a6c-168">/Api/Products を取得します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-168">GET /api/Products</span></span>
- <span data-ttu-id="e5a6c-169">GET /api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="e5a6c-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="e5a6c-170">Api/製品を投稿します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-170">POST /api/Products</span></span>

<span data-ttu-id="e5a6c-171">コント ローラーのアクションは、複数の HTTP メソッドをサポートしている場合、**ための ApiExplorer**各メソッドを個別の API として扱われます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="e5a6c-172">API を非表示にする、**ための ApiExplorer**、追加、 **ApiExplorerSettings**属性を設定しアクション*IgnoreApi*を true にします。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="e5a6c-173">コント ローラー全体を除外する、コント ローラーにこの属性を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="e5a6c-174">ドキュメント文字列を取得するための ApiExplorer クラス、 **IDocumentationProvider**インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="e5a6c-175">ヘルプ ページ ライブラリは、既に説明したように**IDocumentationProvider** XML ドキュメントの文字列からドキュメントを取得します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="e5a6c-176">コードは/Areas/HelpPage/XmlDocumentationProvider.cs にあります。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="e5a6c-177">取得できますドキュメントの別のソースを記述して、独自**IDocumentationProvider**します。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="e5a6c-178">結び付けるを呼び出し、 **SetDocumentationProvider**で定義された拡張機能メソッド**HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="e5a6c-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="e5a6c-179">**ための ApiExplorer**を自動的に呼び出す、 **IDocumentationProvider**各 api のドキュメント文字列を取得するインターフェイス。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="e5a6c-180">それらを保存、**ドキュメント**のプロパティ、 **ApiDescription**と**ApiParameterDescription**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5a6c-181">次の手順</span><span class="sxs-lookup"><span data-stu-id="e5a6c-181">Next Steps</span></span>

<span data-ttu-id="e5a6c-182">方法は、次のとおりのヘルプ ページに限定されません。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="e5a6c-183">実際、**ための ApiExplorer**ヘルプ ページを作成するのには限定されません。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="e5a6c-184">Yao Huang Lin はすぐ概説するいくつかの優れたブログの投稿を書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="e5a6c-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="e5a6c-185">ASP.NET Web API ヘルプ ページへの単純なテスト クライアントの追加</span><span class="sxs-lookup"><span data-stu-id="e5a6c-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="e5a6c-186">ASP.NET Web API ヘルプ ページ自己ホスト型サービスで作業を行う</span><span class="sxs-lookup"><span data-stu-id="e5a6c-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="e5a6c-187">ヘルプ ページ (またはクライアント) の ASP.NET Web API のデザイン時の生成</span><span class="sxs-lookup"><span data-stu-id="e5a6c-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="e5a6c-188">高度なヘルプ ページのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="e5a6c-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
