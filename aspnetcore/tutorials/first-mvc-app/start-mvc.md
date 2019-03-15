---
title: ASP.NET Core MVC の概要
author: rick-anderson
description: ASP.NET Core MVC の概要について説明します。
ms.author: riande
ms.date: 12/12/2018
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: c09c06f55c4179e9e2174f0063ab7387b7e4c31b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059249"
---
# <a name="get-started-with-aspnet-core-mvc"></a><span data-ttu-id="fdf5c-103">ASP.NET Core MVC の概要</span><span class="sxs-lookup"><span data-stu-id="fdf5c-103">Get started with ASP.NET Core MVC</span></span>

<span data-ttu-id="fdf5c-104">作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fdf5c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="fdf5c-105">このチュートリアルでは、ASP.NET Core の MVC Web アプリの構築の基礎について説明します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-105">This tutorial teaches the basics of building an ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="fdf5c-106">このアプリでは、映画タイトルのデータベースを管理します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-106">The app manages a database of movie titles.</span></span> <span data-ttu-id="fdf5c-107">以下の方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdf5c-108">Web アプリを作成する。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-108">Create a web app.</span></span>
> * <span data-ttu-id="fdf5c-109">モデルを追加してスキャフォールディングする。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-109">Add and scaffold a model.</span></span>
> * <span data-ttu-id="fdf5c-110">データベースを使用する。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-110">Work with a database.</span></span>
> * <span data-ttu-id="fdf5c-111">検索と検証を追加する。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-111">Add search and validation.</span></span>

<span data-ttu-id="fdf5c-112">最後には、映画データを管理および表示できるアプリが完成します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-112">At the end, you have an app that can manage and display movie data.</span></span>

[!INCLUDE[](~/includes/mvc-intro/download.md)]

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="fdf5c-113">Web アプリの作成</span><span class="sxs-lookup"><span data-stu-id="fdf5c-113">Create a web app</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="fdf5c-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fdf5c-114">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="fdf5c-115">Visual Studio で **[ファイル]、[新規作成]、[プロジェクト]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-115">From Visual Studio, select  **File > New > Project**.</span></span>

![[ファイル] > [新規] > [プロジェクト]](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="fdf5c-117">**[新しいプロジェクト]** ダイアログで次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-117">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="fdf5c-118">左側のウィンドウで、**[.NET Core]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-118">In the left pane, select **.NET Core**</span></span>
* <span data-ttu-id="fdf5c-119">中央のウィンドウで、**[ASP.NET Core Web Application (.NET Core)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-119">In the center pane, select **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="fdf5c-120">プロジェクトに "MvcMovie" と名前を付けます (コードをコピーするときに名前空間が一致するようにするために、プロジェクトに "MvcMovie" と名前を付けることが重要です)。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-120">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="fdf5c-121">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-121">select **OK**</span></span>

![<span data-ttu-id="fdf5c-122">[新しいプロジェクト] ダイアログ、左ウィンドウの .NET Core、ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="fdf5c-122">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="fdf5c-123">**[ASP.NET Core Web Application (.NET Core) - MvcMovie]** ダイアログを次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-123">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="fdf5c-124">バージョン セレクター ドロップダウン ボックスで、**[ASP.NET Core 2.2]** を選択します</span><span class="sxs-lookup"><span data-stu-id="fdf5c-124">In the version selector drop-down box select **ASP.NET Core 2.2**</span></span>
* <span data-ttu-id="fdf5c-125">**[Web アプリケーション (モデル ビュー コントローラー)]** を選択します</span><span class="sxs-lookup"><span data-stu-id="fdf5c-125">Select **Web Application (Model-View-Controller)**</span></span>
* <span data-ttu-id="fdf5c-126">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-126">select **OK**.</span></span>

![<span data-ttu-id="fdf5c-127">[新しいプロジェクト] ダイアログ、左ウィンドウの .NET Core、ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="fdf5c-127">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="fdf5c-128">Visual Studio は、作成した MVC プロジェクトの既定のテンプレートを使用しました。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-128">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="fdf5c-129">プロジェクト名を入力し、いくつかのオプションを選択すると、すぐに作業アプリができあがります。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-129">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="fdf5c-130">これは基本的なスターター プロジェクトなので、ここから始めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-130">This is a basic starter project, and it's a good place to start.</span></span>

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="fdf5c-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fdf5c-131">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="fdf5c-132">このチュートリアルは VS Code の知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-132">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="fdf5c-133">詳細については、[VS Code の概要](https://code.visualstudio.com/docs)、および [Visual Studio Code のヘルプ](#visual-studio-code-help)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-133">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span>

* <span data-ttu-id="fdf5c-134">[統合ターミナル](https://code.visualstudio.com/docs/editor/integrated-terminal)を開きます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-134">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="fdf5c-135">ディレクトリ (`cd`) を、プロジェクトを格納するフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-135">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="fdf5c-136">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-136">Run the following command:</span></span>

   ```console
   dotnet new mvc -o MvcMovie
   code -r MvcMovie
   ```

  * <span data-ttu-id="fdf5c-137">"**ビルドとデバッグに必要な資産が 'MvcMovie' にありません。追加しますか?**" という内容のダイアログ ボックスが表示されたら、</span><span class="sxs-lookup"><span data-stu-id="fdf5c-137">A dialog box appears with **Required assets to build and debug are missing from 'MvcMovie'. Add them?**</span></span>  <span data-ttu-id="fdf5c-138">**[はい]** を選択します</span><span class="sxs-lookup"><span data-stu-id="fdf5c-138">Select **Yes**</span></span>

  * <span data-ttu-id="fdf5c-139">`dotnet new mvc -o MvcMovie`: *MvcMovie* フォルダー内に新しい ASP.NET Core MVC プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-139">`dotnet new mvc -o MvcMovie`: creates a new ASP.NET Core MVC project in the *MvcMovie* folder.</span></span>
  * <span data-ttu-id="fdf5c-140">`code -r MvcMovie`:Visual Studio Code で *MvcMovie.csproj* プロジェクト ファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-140">`code -r MvcMovie`: Loads the *MvcMovie.csproj* project file in Visual Studio Code.</span></span>

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="fdf5c-141">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="fdf5c-141">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="fdf5c-142">**[ファイル]**、**[新しいソリューション]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-142">Select **File** > **New Solution**.</span></span>

  ![macOS の新しいソリューション](~/tutorials/first-web-api-mac/_static/sln.png)

* <span data-ttu-id="fdf5c-144">**[.NET Core アプリ]** > **[ASP.NET Core]** > **[ASP.NET Core Web アプリ (MVC)]** > **[次へ]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-144">Select **.NET Core App** > **ASP.NET Core** > **ASP.NET Core Web App (MVC)** > **Next**.</span></span>

  ![macOS の [新しいプロジェクト] ダイアログ](~/tutorials/first-mvc-app-mac/start-mvc/1.png)

* <span data-ttu-id="fdf5c-146">**[Configure your new ASP.NET Core Web API]\(新しい ASP.NET Core Web API を構成する\)** ダイアログ ボックスで、既定の**ターゲット フレームワーク** \**.NET Core 2.2* を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-146">In the **Configure your new ASP.NET Core Web API** dialog, accept the default **Target Framework** of \**.NET Core 2.2*.</span></span>

* <span data-ttu-id="fdf5c-147">プロジェクトに **MvcMovie** という名前を付けて、**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-147">Name the project **MvcMovie**, and then select **Create**.</span></span>

---  
<!-- End of VS tabs -->

### <a name="run-the-app"></a><span data-ttu-id="fdf5c-148">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="fdf5c-148">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="fdf5c-149">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fdf5c-149">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="fdf5c-150">**Ctrl + F5** キーを押して、デバッグ以外のモードでアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-150">Select **Ctrl-F5** to run the app in non-debug mode.</span></span>

[!INCLUDE[](~/includes/trustCertVS.md)]

* <span data-ttu-id="fdf5c-151">Visual Studio で [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) が開始され、アプリが実行されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-151">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="fdf5c-152">アドレス バーには、`example.com` などではなく、`localhost:port#` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-152">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="fdf5c-153">これは、`localhost` がローカル コンピューターの標準のホスト名であるためです。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-153">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="fdf5c-154">Visual Studio が Web プロジェクトを作成する場合は、Web サーバーにランダム ポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-154">When Visual Studio creates a web project, a random port is used for the web server.</span></span>
* <span data-ttu-id="fdf5c-155">Ctrl + F5 キー (非デバッグ モード) でアプリを起動することで、コードの変更、ファイルの保存、ブラウザーの更新、コード変更の確認を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-155">Launching the app with Ctrl+F5 (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="fdf5c-156">多くの開発者は、すばやくアプリを起動し、変更を確認できる非デバッグ モードの使用を好みます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-156">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="fdf5c-157">**[デバッグ]** メニュー項目から、デバッグ モードまたは非デバッグ モードでアプリを起動できます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-157">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

  ![[デバッグ] メニュー](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="fdf5c-159">**[IIS Express]** ボタンを選択することで、アプリをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-159">You can debug the app by selecting the **IIS Express** button</span></span>

  ![IIS Express](start-mvc/_static/iis_express.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="fdf5c-161">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fdf5c-161">Visual Studio Code</span></span>](#tab/visual-studio-code) 

<span data-ttu-id="fdf5c-162">Ctrl + F5 キーを押して、デバッガーなしで実行します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-162">Press Ctrl+F5 to run without the debugger.</span></span>

[!INCLUDE[](~/includes/trustCertVSC.md)]

  <span data-ttu-id="fdf5c-163">Visual Studio Code で [Kestrel](xref:fundamentals/servers/kestrel) が開始され、ブラウザーが起動され、`https://localhost:5001` に移動されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-163">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `https://localhost:5001`.</span></span> <span data-ttu-id="fdf5c-164">アドレス バーには、`example.com` などではなく、`localhost:port:5001` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-164">The address bar shows `localhost:port:5001` and not something like `example.com`.</span></span> <span data-ttu-id="fdf5c-165">これは、`localhost` がローカル コンピューターの標準のホスト名であるためです。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-165">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="fdf5c-166">localhost では、ローカル コンピューターからの Web 要求のみが処理されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-166">Localhost only serves web requests from the local computer.</span></span>

  <span data-ttu-id="fdf5c-167">Ctrl + F5 キー (非デバッグ モード) でアプリを起動することで、コードの変更、ファイルの保存、ブラウザーの更新、コード変更の確認を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-167">Launching the app with Ctrl+F5 (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="fdf5c-168">多くの開発者は、ページを更新して変更を確認できる非デバッグ モードの使用を好みます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-168">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="fdf5c-169">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="fdf5c-169">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="fdf5c-170">**[実行]** > **[デバッグなしで開始]** の順に選択してアプリを起動します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-170">Select **Run** > **Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="fdf5c-171">Visual Studio for Mac によって [Kestrel](xref:fundamentals/servers/index#kestrel) サーバーが開始され、ブラウザーが起動して `http://localhost:port` にアクセスします。*port* はランダムに選択されたポート番号になります。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-171">Visual Studio for Mac starts [Kestrel](xref:fundamentals/servers/index#kestrel) server, launches a browser, and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span>

[!INCLUDE[](~/includes/trustCertMac.md)]

* <span data-ttu-id="fdf5c-172">アドレス バーには、`example.com` などではなく、`localhost:port#` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-172">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="fdf5c-173">これは、`localhost` がローカル コンピューターの標準のホスト名であるためです。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-173">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="fdf5c-174">Visual Studio が Web プロジェクトを作成する場合は、Web サーバーにランダム ポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-174">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="fdf5c-175">アプリを実行する際には、別のポート番号が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-175">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="fdf5c-176">**[実行]** メニューから、デバッグ モードまたは非デバッグ モードでアプリを起動できます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-176">You can launch the app in debug or non-debug mode from the **Run** menu.</span></span>

------

* <span data-ttu-id="fdf5c-177">**[同意する]** を選択し、追跡に同意します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-177">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="fdf5c-178">このアプリでは個人情報は追跡されません。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-178">This app doesn't track personal information.</span></span> <span data-ttu-id="fdf5c-179">テンプレートで生成されたコードには、[一般的なデータ保護規制 (GDPR)](xref:security/gdpr) を満たす資産が含まれます。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-179">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![ホームまたはインデックス ページ](start-mvc/_static/privacy.png)

  <span data-ttu-id="fdf5c-181">次の図は、追跡に同意した後のアプリを示しています。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-181">The following image shows the app after accepting tracking:</span></span>

  ![ホームまたはインデックス ページ](start-mvc/_static/home2.2.png)

[!INCLUDE[](~/includes/vs-vsc-vsmac-help.md)]

<span data-ttu-id="fdf5c-183">このチュートリアルの次のパートでは、MVC について説明し、コードの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="fdf5c-183">In the next part of this tutorial, you learn about MVC and start writing some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fdf5c-184">次へ</span><span class="sxs-lookup"><span data-stu-id="fdf5c-184">Next</span></span>](adding-controller.md)  
