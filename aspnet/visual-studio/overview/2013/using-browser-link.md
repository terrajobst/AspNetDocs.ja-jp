---
uid: visual-studio/overview/2013/using-browser-link
title: Visual Studio 2013 | でブラウザーリンクを使用するMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505204"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="058ae-102">Visual Studio 2013 でブラウザーリンクを使用する</span><span class="sxs-lookup"><span data-stu-id="058ae-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="058ae-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="058ae-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="058ae-104">ブラウザーリンクは、開発環境と1つ以上の web ブラウザーの間の通信チャネルを作成する Visual Studio 2013 の新機能です。</span><span class="sxs-lookup"><span data-stu-id="058ae-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="058ae-105">ブラウザーリンクを使用すると、複数のブラウザーで一度に web アプリケーションを更新できます。これは、ブラウザー間のテストに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="058ae-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="058ae-106">ブラウザーの更新</span><span class="sxs-lookup"><span data-stu-id="058ae-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="058ae-107">ブラウザーリンクダッシュボードの表示</span><span class="sxs-lookup"><span data-stu-id="058ae-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="058ae-108">静的な HTML ファイルのブラウザーリンクを有効にする</span><span class="sxs-lookup"><span data-stu-id="058ae-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="058ae-109">ブラウザーリンクを無効にしています</span><span class="sxs-lookup"><span data-stu-id="058ae-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="058ae-110">どのように動作するのでしょうか。</span><span class="sxs-lookup"><span data-stu-id="058ae-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="058ae-111">ブラウザーの更新</span><span class="sxs-lookup"><span data-stu-id="058ae-111">Browser Refresh</span></span>

<span data-ttu-id="058ae-112">ブラウザーの更新では、ブラウザーリンクを使用して Visual Studio に接続されている複数のブラウザーを更新できます。</span><span class="sxs-lookup"><span data-stu-id="058ae-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="058ae-113">ブラウザーの更新を使用するには、まず、プロジェクトテンプレートのいずれかを使用して ASP.NET アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="058ae-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="058ae-114">F5 キーを押すか、ツールバーの矢印アイコンをクリックして、アプリケーションをデバッグします。</span><span class="sxs-lookup"><span data-stu-id="058ae-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="058ae-115">ドロップダウンを使用して、デバッグ用の特定のブラウザーを選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="058ae-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="058ae-116">複数のブラウザーでデバッグするには、 **[参照]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="058ae-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="058ae-117">**[参照]** ダイアログボックスで、CTRL キーを押しながら複数のブラウザーを選択します。</span><span class="sxs-lookup"><span data-stu-id="058ae-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="058ae-118">**[参照]** をクリックして、選択したブラウザーでデバッグします。</span><span class="sxs-lookup"><span data-stu-id="058ae-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="058ae-119">ブラウザーリンクは、Visual Studio の外部からブラウザーを起動し、アプリケーションの URL に移動した場合にも機能します。</span><span class="sxs-lookup"><span data-stu-id="058ae-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="058ae-120">ブラウザーリンクコントロールは、矢印アイコンが付いたドロップダウンリストにあります。</span><span class="sxs-lookup"><span data-stu-id="058ae-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="058ae-121">矢印アイコンは、 **[更新]** ボタンです。</span><span class="sxs-lookup"><span data-stu-id="058ae-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="058ae-122">接続されているブラウザーを確認するには、デバッグ中に **[更新]** ボタンの上にマウスポインターを置きます。</span><span class="sxs-lookup"><span data-stu-id="058ae-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="058ae-123">接続されているブラウザーは、ツールヒントウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="058ae-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="058ae-124">接続されているブラウザーを更新するには、 **[更新]** ボタンをクリックするか、CTRL + ALT + enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="058ae-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="058ae-125">たとえば、次のスクリーンショットは、MVC 5 プロジェクトテンプレートを使用して作成した ASP.NET プロジェクトを示しています。</span><span class="sxs-lookup"><span data-stu-id="058ae-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="058ae-126">アプリケーションは、上部にある2つのブラウザーで実行されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="058ae-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="058ae-127">一番下には、Visual Studio でプロジェクトが開いています。</span><span class="sxs-lookup"><span data-stu-id="058ae-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="058ae-128">Visual Studio で、ホームページの &lt;h1&gt; 見出しを変更しました。</span><span class="sxs-lookup"><span data-stu-id="058ae-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="058ae-129">**[更新]** ボタンをクリックすると、両方のブラウザーウィンドウに変更が表示されます。</span><span class="sxs-lookup"><span data-stu-id="058ae-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="058ae-130">**注**</span><span class="sxs-lookup"><span data-stu-id="058ae-130">**Notes**</span></span>

- <span data-ttu-id="058ae-131">ブラウザーリンクを有効にするには、プロジェクトの Web.config ファイルの[&lt;コンパイル&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)要素に `debug=true` を設定します。</span><span class="sxs-lookup"><span data-stu-id="058ae-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="058ae-132">アプリケーションが localhost で実行されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="058ae-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="058ae-133">アプリケーションは、.NET 4.0 以降を対象とする必要があります。</span><span class="sxs-lookup"><span data-stu-id="058ae-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="058ae-134">ブラウザーリンクダッシュボードの表示</span><span class="sxs-lookup"><span data-stu-id="058ae-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="058ae-135">ブラウザーリンクダッシュボードには、ブラウザーリンクの接続に関する情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="058ae-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="058ae-136">ダッシュボードを表示するには、ブラウザーリンク ドロップダウンメニュー (**更新** ボタンの横にある小さな矢印) を選択します。</span><span class="sxs-lookup"><span data-stu-id="058ae-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="058ae-137">次に、 **[ブラウザーリンクダッシュボード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="058ae-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="058ae-138">ダッシュボードには、接続されているブラウザーと、各ブラウザーがナビゲートした URL が一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="058ae-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="058ae-139">**[前提条件]** セクションには、そのプロジェクトのブラウザーリンクを有効にするために必要なすべての手順が表示されます。</span><span class="sxs-lookup"><span data-stu-id="058ae-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="058ae-140">たとえば、次のスクリーンショットは、web.config ファイルで "debug" が false に設定されているプロジェクトを示しています。</span><span class="sxs-lookup"><span data-stu-id="058ae-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="058ae-141">静的な HTML ファイルのブラウザーリンクを有効にする</span><span class="sxs-lookup"><span data-stu-id="058ae-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="058ae-142">静的な HTML ファイルの Browser リンクを有効にするには、web.config ファイルに次のを追加します。</span><span class="sxs-lookup"><span data-stu-id="058ae-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="058ae-143">パフォーマンス上の理由から、プロジェクトを発行するときにこの設定を削除します。</span><span class="sxs-lookup"><span data-stu-id="058ae-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="058ae-144">ブラウザーリンクを無効にしています</span><span class="sxs-lookup"><span data-stu-id="058ae-144">Disabling Browser Link</span></span>

<span data-ttu-id="058ae-145">ブラウザーリンクは既定で有効になっています。</span><span class="sxs-lookup"><span data-stu-id="058ae-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="058ae-146">無効にするには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="058ae-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="058ae-147">ブラウザーのリンクのドロップダウンメニューで、 **[ブラウザーリンクを有効にする]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="058ae-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="058ae-148">Web.config ファイルで、appSettings セクションに "vs: EnableBrowserLink" という名前のキーを値 "false" で追加します。</span><span class="sxs-lookup"><span data-stu-id="058ae-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="058ae-149">Web.config ファイルで、debug を false に設定します。</span><span class="sxs-lookup"><span data-stu-id="058ae-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="058ae-150">どのように動作するのでしょうか。</span><span class="sxs-lookup"><span data-stu-id="058ae-150">How Does It Work?</span></span>

<span data-ttu-id="058ae-151">ブラウザーリンクは、 [SignalR](../../../signalr/index.md)を使用して、Visual Studio とブラウザーの間の通信チャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="058ae-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="058ae-152">ブラウザーリンクが有効になっている場合、Visual Studio は複数のクライアント (ブラウザー) が接続できる SignalR サーバーとして機能します。</span><span class="sxs-lookup"><span data-stu-id="058ae-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="058ae-153">ブラウザーリンクでは、HTTP モジュールを ASP.NET に登録することもできます。</span><span class="sxs-lookup"><span data-stu-id="058ae-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="058ae-154">このモジュールは、サーバーからのすべてのページ要求に、特別な &lt;スクリプト&gt; 参照を挿入します。</span><span class="sxs-lookup"><span data-stu-id="058ae-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="058ae-155">スクリプト参照を表示するには、ブラウザーで [ソースの表示] を選択します。</span><span class="sxs-lookup"><span data-stu-id="058ae-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="058ae-156">ソースファイルは変更されません。</span><span class="sxs-lookup"><span data-stu-id="058ae-156">Your source files are not modified.</span></span> <span data-ttu-id="058ae-157">HTTP モジュールは、スクリプト参照を動的に挿入します。</span><span class="sxs-lookup"><span data-stu-id="058ae-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="058ae-158">ブラウザー側のコードはすべて JavaScript であるため、 [SignalR がサポート](../../../signalr/overview/getting-started/supported-platforms.md)しているすべてのブラウザーで機能します。ブラウザープラグインは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="058ae-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
