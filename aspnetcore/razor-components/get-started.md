---
title: Razor のコンポーネントを概要します。
author: guardrex
description: 作成と Razor コンポーネント プロジェクトを変更して Razor コンポーネントを開始する方法について説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/03/2019
uid: razor-components/get-started
ms.openlocfilehash: a9ada603e5ed4e0e75c4aebc5105c331118666e6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036389"
---
# <a name="get-started-with-razor-components"></a><span data-ttu-id="8d673-103">Razor のコンポーネントを概要します。</span><span class="sxs-lookup"><span data-stu-id="8d673-103">Get started with Razor Components</span></span>

<span data-ttu-id="8d673-104">作成者: [Daniel Roth](https://github.com/danroth27)、[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8d673-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="8d673-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d673-105">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="8d673-106">必要条件:</span><span class="sxs-lookup"><span data-stu-id="8d673-106">Prerequisites:</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

<span data-ttu-id="8d673-107">Visual Studio で、最初の Razor コンポーネント プロジェクトを作成するには</span><span class="sxs-lookup"><span data-stu-id="8d673-107">To create your first Razor Components project in Visual Studio:</span></span>

1. <span data-ttu-id="8d673-108">選択**ファイル** > **新しいプロジェクト** > **Web** > **ASP.NET Core Web アプリケーション**します。</span><span class="sxs-lookup"><span data-stu-id="8d673-108">Select **File** > **New Project** > **Web** > **ASP.NET Core Web Application**.</span></span>
1. <span data-ttu-id="8d673-109">確認します **.NET Core**と**ASP.NET Core 3.0**上部にある選択されます。</span><span class="sxs-lookup"><span data-stu-id="8d673-109">Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.</span></span>
1. <span data-ttu-id="8d673-110">選択、 **Razor コンポーネント**テンプレートと選択**OK**します。</span><span class="sxs-lookup"><span data-stu-id="8d673-110">Choose the **Razor Components** template and select **OK**.</span></span>

   ![新しいアプリのダイアログ](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. <span data-ttu-id="8d673-112">**F5 キー**を押してアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="8d673-112">Press **F5** to run the app.</span></span>

<span data-ttu-id="8d673-113">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="8d673-113">Congratulations!</span></span> <span data-ttu-id="8d673-114">最初の Razor コンポーネント アプリを実行しました。</span><span class="sxs-lookup"><span data-stu-id="8d673-114">You just ran your first Razor Components app!</span></span>

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Razor Components project in Visual Studio Code:

1. Execute the following command from a command shell:

   ```console
   dotnet new razorcomponents -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Add a *.vscode* folder.

1. Add a *tasks.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/tasks.json)]

1. Add a *launch.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/launch.json)]

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Razor Components app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.


[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Razor Components project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **ASP.NET Core Razor Components** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Razor Components app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="8d673-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="8d673-115">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="8d673-116">必要条件:</span><span class="sxs-lookup"><span data-stu-id="8d673-116">Prerequisites:</span></span>

* [<span data-ttu-id="8d673-117">.NET core SDK 3.0 プレビュー</span><span class="sxs-lookup"><span data-stu-id="8d673-117">.NET Core SDK 3.0 Preview</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. <span data-ttu-id="8d673-118">コマンド シェルから、最初の Razor コンポーネント プロジェクトを作成するには</span><span class="sxs-lookup"><span data-stu-id="8d673-118">To create your first Razor Components project from a command shell:</span></span>

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. <span data-ttu-id="8d673-119">ブラウザーで、`https://localhost:5001` に移動します。</span><span class="sxs-lookup"><span data-stu-id="8d673-119">In a browser, navigate to `https://localhost:5001`.</span></span>

<span data-ttu-id="8d673-120">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="8d673-120">Congratulations!</span></span> <span data-ttu-id="8d673-121">最初の Razor コンポーネント アプリを実行しました。</span><span class="sxs-lookup"><span data-stu-id="8d673-121">You just ran your first Razor Components app!</span></span>

---

## <a name="razor-components-project"></a><span data-ttu-id="8d673-122">Razor のコンポーネントのプロジェクト</span><span class="sxs-lookup"><span data-stu-id="8d673-122">Razor Components project</span></span>

<span data-ttu-id="8d673-123">コンポーネントの Razor テンプレートによって作成されたソリューションには、2 つのプロジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d673-123">The solution created by the Razor Components template contains two projects:</span></span>

* <span data-ttu-id="8d673-124">*WebApplication1.Server* &ndash;サーバー プロジェクトは、ASP.NET Core プロジェクトは、Razor コンポーネント アプリケーションをホストするように設定します。</span><span class="sxs-lookup"><span data-stu-id="8d673-124">*WebApplication1.Server* &ndash; The server project is an ASP.NET Core project set up to host the Razor Components app.</span></span>
* <span data-ttu-id="8d673-125">*WebApplication1.App* &ndash; Razor コンポーネントを使用するクライアント側の web UI プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="8d673-125">*WebApplication1.App* &ndash; The client-side web UI project that uses Razor Components.</span></span>

<span data-ttu-id="8d673-126">UI ロジック、 *WebApplication1.App*プロジェクトは ASP.NET Core 3.0 プレビュー 2 の技術的な制限により、アプリの残りの部分から分離します。</span><span class="sxs-lookup"><span data-stu-id="8d673-126">The UI logic in the *WebApplication1.App* project is separated from the rest of the app due to a technical limitation in ASP.NET Core 3.0 Preview 2.</span></span> <span data-ttu-id="8d673-127">Razor ファイルの拡張子 (*.cshtml*) 使用の Razor コンポーネントは、Razor ページと MVC のビューにも使用します。</span><span class="sxs-lookup"><span data-stu-id="8d673-127">The Razor file extension (*.cshtml*) used for Razor Components is also used for Razor Pages and MVC views.</span></span> <span data-ttu-id="8d673-128">現時点では、Razor のコンポーネントと Razor ページ/MVC は、さまざまなコンパイル モデルをあるので、Razor のコンポーネントの Razor ファイルが個別に保存されます。</span><span class="sxs-lookup"><span data-stu-id="8d673-128">Currently, Razor Components and Razor Pages/MVC have different compilation models, so the Razor Components Razor files are kept separate.</span></span> <span data-ttu-id="8d673-129">Razor のコンポーネントの新しいファイル拡張子を導入する予定の今後のプレビュー (*.razor*)。</span><span class="sxs-lookup"><span data-stu-id="8d673-129">In a future preview, we plan to introduce a new file extension for Razor Components (*.razor*).</span></span> <span data-ttu-id="8d673-130">コンポーネント、ページ、およびビューをホストする*同じプロジェクトで*します。</span><span class="sxs-lookup"><span data-stu-id="8d673-130">Components, pages, and views will be hosted *in the same project*.</span></span>

<span data-ttu-id="8d673-131">アプリを実行すると、複数のページは、サイドバー内のタブから利用できます。</span><span class="sxs-lookup"><span data-stu-id="8d673-131">When the app is run, multiple pages are available from tabs in the sidebar:</span></span>

* <span data-ttu-id="8d673-132">Home</span><span class="sxs-lookup"><span data-stu-id="8d673-132">Home</span></span>
* <span data-ttu-id="8d673-133">カウンター</span><span class="sxs-lookup"><span data-stu-id="8d673-133">Counter</span></span>
* <span data-ttu-id="8d673-134">データをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="8d673-134">Fetch data</span></span>

<span data-ttu-id="8d673-135">Counter ページ上で **[クリックしてください]** ボタンを選択し、ページを更新することなくカウンターをインクリメントします。</span><span class="sxs-lookup"><span data-stu-id="8d673-135">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="8d673-136">Web ページでカウンターをインクリメントする場合、通常は JavaScript を記述することが必要ですが、Razor Components には C# を使ったより優れた方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="8d673-136">Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.</span></span>

<span data-ttu-id="8d673-137">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8d673-137">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

<span data-ttu-id="8d673-138">要求を`/counter`で指定したとおり、ブラウザーで、`@page`上部にあるディレクティブがそのコンテンツを表示するために、カウンターのコンポーネント。</span><span class="sxs-lookup"><span data-stu-id="8d673-138">A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content.</span></span> <span data-ttu-id="8d673-139">コンポーネントは、柔軟で効率的な方法で UI を更新するために使用するレンダリング ツリーのメモリ内表現にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="8d673-139">Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.</span></span>

<span data-ttu-id="8d673-140">毎回、 **Click me**ボタンが選択されています。</span><span class="sxs-lookup"><span data-stu-id="8d673-140">Each time the **Click me** button is selected:</span></span>

* <span data-ttu-id="8d673-141">`onclick`イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="8d673-141">The `onclick` event is fired.</span></span>
* <span data-ttu-id="8d673-142">`IncrementCount` メソッドが呼び出された場合。</span><span class="sxs-lookup"><span data-stu-id="8d673-142">The `IncrementCount` method is called.</span></span>
* <span data-ttu-id="8d673-143">`currentCount`がインクリメントされます。</span><span class="sxs-lookup"><span data-stu-id="8d673-143">The `currentCount` is incremented.</span></span>
* <span data-ttu-id="8d673-144">コンポーネントは、もう一度表示されます。</span><span class="sxs-lookup"><span data-stu-id="8d673-144">The component is rendered again.</span></span>

<span data-ttu-id="8d673-145">ランタイムは、前のコンテンツを新しいコンテンツを比較し、ドキュメント オブジェクト モデル (DOM) に変更されたコンテンツにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="8d673-145">The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).</span></span>

<span data-ttu-id="8d673-146">HTML のような構文を使用して別のコンポーネントにコンポーネントを追加します。</span><span class="sxs-lookup"><span data-stu-id="8d673-146">Add a component to another component using an HTML-like syntax.</span></span> <span data-ttu-id="8d673-147">コンポーネントのパラメーターは、属性または子コンテンツを使用して指定されます。</span><span class="sxs-lookup"><span data-stu-id="8d673-147">Component parameters are specified using attributes or child content.</span></span> <span data-ttu-id="8d673-148">追加することでカウンター コンポーネントをアプリのホーム ページに追加するなど、`<Counter />`インデックス コンポーネント要素。</span><span class="sxs-lookup"><span data-stu-id="8d673-148">For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.</span></span>

<span data-ttu-id="8d673-149">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8d673-149">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

<span data-ttu-id="8d673-150">アプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="8d673-150">Run the app.</span></span> <span data-ttu-id="8d673-151">ホームページには、独自のカウンターを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d673-151">The homepage has its own counter.</span></span>

<span data-ttu-id="8d673-152">カウンターのコンポーネントにパラメーターを追加する更新コンポーネントの`@functions`ブロック。</span><span class="sxs-lookup"><span data-stu-id="8d673-152">To add a parameter to the Counter component, update the component's `@functions` block:</span></span>

* <span data-ttu-id="8d673-153">プロパティを追加`IncrementAmount`で修飾された、`[Parameter]`属性。</span><span class="sxs-lookup"><span data-stu-id="8d673-153">Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.</span></span>
* <span data-ttu-id="8d673-154">`currentCount` の値を増やすときに `IncrementAmount` を使うように `IncrementCount` メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="8d673-154">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

<span data-ttu-id="8d673-155">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8d673-155">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

<span data-ttu-id="8d673-156">属性を使って、Home コンポーネントの `<Counter>` 要素に `IncrementAmount` パラメーターを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d673-156">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span>

<span data-ttu-id="8d673-157">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8d673-157">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

<span data-ttu-id="8d673-158">アプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="8d673-158">Run the app.</span></span> <span data-ttu-id="8d673-159">ホームページには、10 たびにインクリメントする独自のカウンター、 **Click me**ボタンが選択されています。</span><span class="sxs-lookup"><span data-stu-id="8d673-159">The homepage has its own counter that increments by ten each time the **Click me** button is selected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d673-160">次の手順</span><span class="sxs-lookup"><span data-stu-id="8d673-160">Next steps</span></span>

<xref:tutorials/first-razor-components-app>
