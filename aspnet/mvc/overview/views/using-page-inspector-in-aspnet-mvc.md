---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC での Page Inspector の使用 |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。 統合ブラウザーで任意の要素を選択し、Page Inspector します...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432454"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="2255c-104">ASP.NET MVC フォーム内での Page Inspector の使用</span><span class="sxs-lookup"><span data-stu-id="2255c-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="2255c-105">Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="2255c-105">by Tim Ammann</span></span>

> <span data-ttu-id="2255c-106">Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。</span><span class="sxs-lookup"><span data-stu-id="2255c-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="2255c-107">統合ブラウザーで任意の要素を選択すると、Page Inspector 要素のソースと CSS が瞬時に強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="2255c-108">任意の MVC ビューを参照したり、表示されているマークアップのソースをすばやく検索したり、Visual Studio 環境内でブラウザーツールを使用したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="2255c-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="2255c-109">ビデオを見る</span><span class="sxs-lookup"><span data-stu-id="2255c-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="2255c-110">このチュートリアルでは、検査モードを有効にし、web プロジェクト内でマークアップと CSS をすばやく検索して編集する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2255c-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="2255c-111">このチュートリアルでは MVC プロジェクトを使用しますが、 [Web フォーム](https://go.microsoft.com/?linkid=9802001)や他の ASP.NET アプリケーションには Page Inspector を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2255c-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="2255c-112">このチュートリアルには、次のセクションがあります。</span><span class="sxs-lookup"><span data-stu-id="2255c-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="2255c-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="2255c-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="2255c-114">Web アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="2255c-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="2255c-115">Page Inspector を使用してビューを参照する</span><span class="sxs-lookup"><span data-stu-id="2255c-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="2255c-116">検査モードを有効にする</span><span class="sxs-lookup"><span data-stu-id="2255c-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="2255c-117">Page Inspector を使用してマークアップを変更する</span><span class="sxs-lookup"><span data-stu-id="2255c-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="2255c-118">検査モードと HTML ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="2255c-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - <span data-ttu-id="2255c-119">[[スタイル] ウィンドウでの CSS の変更のプレビュー](#_7_previewing_css)</span><span class="sxs-lookup"><span data-stu-id="2255c-119">[Preview CSS Changes in the Styles window](#_7_previewing_css)</span></span>
> - [<span data-ttu-id="2255c-120">CSS 自動同期</span><span class="sxs-lookup"><span data-stu-id="2255c-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="2255c-121">CSS カラーピッカーの使用</span><span class="sxs-lookup"><span data-stu-id="2255c-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="2255c-122">動的ページ要素の JavaScript へのマッピング</span><span class="sxs-lookup"><span data-stu-id="2255c-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="2255c-123">前提条件</span><span class="sxs-lookup"><span data-stu-id="2255c-123">Prerequisites</span></span>

- <span data-ttu-id="2255c-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11)または[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="2255c-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="2255c-125">最新バージョンの Page Inspector を取得するには、 [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)を使用して WINDOWS Azure SDK for .net 2.0 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="2255c-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="2255c-126">Page Inspector は Microsoft Web Developer Tools にバンドルされています。</span><span class="sxs-lookup"><span data-stu-id="2255c-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="2255c-127">最新バージョンは1.3 です。</span><span class="sxs-lookup"><span data-stu-id="2255c-127">The latest version is 1.3.</span></span> <span data-ttu-id="2255c-128">使用しているバージョンを確認するには、Visual Studio を実行し、 **[ヘルプ]** メニューから バージョン **[情報 Microsoft Visual Studio]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="2255c-129">Web アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="2255c-129">Create a Web Application</span></span>

<span data-ttu-id="2255c-130">まず、で Page Inspector 使用する web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="2255c-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="2255c-131">Visual Studio で、[**ファイル**&gt;**新しいプロジェクト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="2255c-132">左側で **[ C#ビジュアル]** を展開し、 **[Web]** を選択して、 **[ASP.NET MVC4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![新しい ASP.NET MVC アプリケーション](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="2255c-134">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-134">Click **OK**.</span></span>

<span data-ttu-id="2255c-135">**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="2255c-136">既定のビューエンジンとして**Razor**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="2255c-136">Leave **Razor** as the default view engine.</span></span>

![New ASP.NET MVC プロジェクト-インターネットアプリケーション](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="2255c-138">アプリケーションが**ソース**ビューで開きます。</span><span class="sxs-lookup"><span data-stu-id="2255c-138">The application opens in **Source** view.</span></span>

![ソースビューの新しい ASP.NET MVC アプリケーション](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="2255c-140">アプリケーションを操作できるようになったので、Page Inspector を使用して確認し、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="2255c-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="2255c-141">Page Inspector を使用してビューを参照する</span><span class="sxs-lookup"><span data-stu-id="2255c-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="2255c-142">Visual Studio 2012 では、プロジェクト内の任意のビューを右クリックして **[Page Inspector で表示]** を選択すると、ルートが Page Inspector 表示され、ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="2255c-143">**ソリューションエクスプローラー**で、 **Views**フォルダーを展開し、 **[ホーム]** フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="2255c-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="2255c-144">Index. cshtml ファイルを右クリックし、 **[Page Inspector で表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Page Inspector でのインデックスの表示](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="2255c-146">既定では、Page Inspector は、Visual Studio 環境の左側にウィンドウとしてドッキングされます。</span><span class="sxs-lookup"><span data-stu-id="2255c-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="2255c-147">必要に応じて、他の場所にドッキングしたり、ウィンドウをドッキング解除したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="2255c-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="2255c-148">「[方法: ウィンドウを整列およびドッキングする](https://msdn.microsoft.com/library/z4y0hsax.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2255c-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="2255c-149">[Page Inspector] ウィンドウの上部ペインに、ブラウザーウィンドウに現在のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="2255c-150">下部のペインには、HTML マークアップのページと、ページのさまざまな側面を調べるためのタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="2255c-151">下のウィンドウは、Internet Explorer の[F12 開発者ツール](https://msdn.microsoft.com/ie/aa740478)に似ています。</span><span class="sxs-lookup"><span data-stu-id="2255c-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Page Inspector での ASP.NET MVC アプリケーション](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="2255c-153">このチュートリアルでは、 **[HTML]** タブと **[スタイル]** タブを使用してすばやく移動し、アプリケーションに変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="2255c-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="2255c-154">EnableInspection モード</span><span class="sxs-lookup"><span data-stu-id="2255c-154">EnableInspection Mode</span></span>

<span data-ttu-id="2255c-155">Page Inspector を検査モードに配置するには、 **[検査]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="2255c-156">検査モードでは、表示されるページの任意の部分にマウスポインターを置くと、対応するソースマークアップまたはコードが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![検査モードの切り替え](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="2255c-158">次に、Page Inspector 内のページのさまざまな部分にマウスを移動します。</span><span class="sxs-lookup"><span data-stu-id="2255c-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="2255c-159">この操作を行うと、マウスポインターが大きなプラス記号に変わり、下の要素が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div にカーソルを合わせる-ラッパー](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="2255c-161">マウスポインターを移動すると、Visual Studio によって、ソースファイル内の対応する Razor 構文が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="2255c-162">HTML 要素が別のソースファイルから取得された場合は、Visual Studio によってファイルが自動的に開きます。</span><span class="sxs-lookup"><span data-stu-id="2255c-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="2255c-163">Page Inspector では、Razor 構文から生成された HTML が **[html]** タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="2255c-164">マウスポインターを移動すると、HTML 要素が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="2255c-165">**[スタイル]** タブには、要素の CSS ルールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="2255c-166">Page Inspector を使用してマークアップを変更する</span><span class="sxs-lookup"><span data-stu-id="2255c-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="2255c-167">Page Inspector を使用すると、場所が明確でないマークアップを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="2255c-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="2255c-168">その後、マークアップを変更し、結果の変更を確認できます。</span><span class="sxs-lookup"><span data-stu-id="2255c-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="2255c-169">これを表示するには、**検査** をクリックし、Page Inspector ウィンドウでページの一番下までスクロールします。</span><span class="sxs-lookup"><span data-stu-id="2255c-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="2255c-170">マウスポインターをフッター領域に移動すると、Page Inspector によって \_Layout ファイルが開き、選択したレイアウトページのセクションが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="2255c-171">ご覧のように、フッターはレイアウトファイルで定義されており、ビュー自体では定義されていません。</span><span class="sxs-lookup"><span data-stu-id="2255c-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![フッター](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="2255c-173">次に、著作権<a id="a"></a>に関する通知を使用して、マウスポインターを行の上に移動します。</span><span class="sxs-lookup"><span data-stu-id="2255c-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="2255c-174">\_Layout ページで、対応する行が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![フッターの著作権線が強調表示されます](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="2255c-176">\_Layout. cshtml ファイル内の行の末尾にテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="2255c-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="2255c-177">&lt;p&gt;&amp;コピーです。@DateTime.Now.Year-マイ ASP.NET MVC アプリケーションは、&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="2255c-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="2255c-178">ここで、Ctrl + Alt + Enter キーを押すか、更新バーをクリックして Page Inspector ブラウザーウィンドウに結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="2255c-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![私の ASP.NET アプリケーションは岩を持っています。](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="2255c-180">このフッターは、Index. cshtml で定義されているように思われるかもしれませんが、\_Layout. cshtml に入っているので、Page Inspector 見つかりました。</span><span class="sxs-lookup"><span data-stu-id="2255c-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="2255c-181">検査モードと HTML ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="2255c-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="2255c-182">次に、HTML ウィンドウと、要素をどのようにマップするかを簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="2255c-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="2255c-183">**[検査]** をクリックして、検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="2255c-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="2255c-184">ページの一番上の部分をクリックします。 [ここにロゴを入力してください] と表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="2255c-185">特定の要素を詳細に調べているため、マウスポインターを移動しても、ブラウザーウィンドウの表示が変更されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="2255c-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="2255c-186">次に、マウスポインターを**HTML**ウィンドウに移動します。</span><span class="sxs-lookup"><span data-stu-id="2255c-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="2255c-187">マウスポインターを移動すると、Page Inspector **HTML**ウィンドウ内の要素のアウトラインが表示され、ブラウザーウィンドウ内の対応する要素が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML ウィンドウ](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="2255c-189">以前と同様に、Page Inspector は、一時タブで \_Layout ファイルを開きます。 [\_Layout] をクリックすると、対応するマークアップが &lt;ヘッダー&gt; セクションで強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![強調表示されたマークアップ](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="2255c-191">[スタイル] ウィンドウでの CSS の変更のプレビュー</span><span class="sxs-lookup"><span data-stu-id="2255c-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="2255c-192">次に、[Page Inspector**スタイル**] ウィンドウを使用して、CSS の変更をプレビューします。</span><span class="sxs-lookup"><span data-stu-id="2255c-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="2255c-193">**[検査]** をクリックして、検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="2255c-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="2255c-194">Page Inspector ブラウザーウィンドウで、ホームページ セクションの上にマウスポインターを移動し、 **div** と表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="2255c-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Div にカーソルを合わせる-ラッパー](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="2255c-196">Div のコンテンツラッパーセクション内を1回クリックし、マウスポインターを **[スタイル]** ウィンドウに移動します。</span><span class="sxs-lookup"><span data-stu-id="2255c-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="2255c-197">**[スタイル]** ウィンドウには、この要素のすべての CSS ルールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="2255c-198">下にスクロールして、... コンテンツラッパークラスセレクターを見つけます。</span><span class="sxs-lookup"><span data-stu-id="2255c-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="2255c-199">次に、[背景色] プロパティのチェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="2255c-199">Now clear the checkbox for the background-color property.</span></span>

![背景色のクリア](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="2255c-201">Page Inspector ブラウザーウィンドウに変更がすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="2255c-202">もう一度チェックボックスをオンにし、プロパティ値をダブルクリックして、赤に変更します。</span><span class="sxs-lookup"><span data-stu-id="2255c-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="2255c-203">変更はすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-203">The change shows immediately:</span></span>

![赤の背景色](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="2255c-205">**[スタイル]** ウィンドウを使用すると、スタイルシート自体に変更をコミットする前に、CSS の変更を簡単にテストおよびプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="2255c-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="2255c-206">CSS 自動同期</span><span class="sxs-lookup"><span data-stu-id="2255c-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="2255c-207">この機能には Page Inspector のバージョン1.3 が必要です。</span><span class="sxs-lookup"><span data-stu-id="2255c-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="2255c-208">CSS 自動同期機能を使用すると、CSS ファイルを直接編集し、Page Inspector ブラウザーですぐに変更を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="2255c-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="2255c-209">**[検査]** をクリックして、検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="2255c-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="2255c-210">Page Inspector ブラウザーで、[ホームページ] セクションの上にマウスポインターを移動**します。このラベルが**表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="2255c-211">この要素を選択するには、[1 回] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-211">Click once to select this element.</span></span>

<span data-ttu-id="2255c-212">**[スタイル]** ウィンドウには、この要素のすべての CSS ルールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="2255c-213">下にスクロールして、... コンテンツラッパークラスセレクターを見つけます。</span><span class="sxs-lookup"><span data-stu-id="2255c-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="2255c-214">[... コンテンツ-ラッパー] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="2255c-215">Page Inspector によって、このスタイル (.css) を定義する CSS ファイルが開き、対応する CSS スタイルが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="2255c-216">次に、`background-color` の値を "red" に変更します。</span><span class="sxs-lookup"><span data-stu-id="2255c-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="2255c-217">変更は、Page Inspector ブラウザーに直ちに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="2255c-218">CSS カラーピッカーの使用</span><span class="sxs-lookup"><span data-stu-id="2255c-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="2255c-219">Visual Studio 2012 の CSS エディターには、色の選択と挿入を簡単に行うことができるカラーピッカーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2255c-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="2255c-220">カラーピッカーには標準の色パレットが含まれており、標準の色の名前、ハッシュコード、RGB、RGBA、HSL、および HSLA の色をサポートし、ドキュメントで最近使用した色の一覧を保持します。</span><span class="sxs-lookup"><span data-stu-id="2255c-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="2255c-221">前のセクションでは、`background-color` プロパティの値を変更しました。</span><span class="sxs-lookup"><span data-stu-id="2255c-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="2255c-222">カラーピッカーを呼び出すには、プロパティ名の後に挿入ポイントを置き、 **#** または**rgb (** ) を入力します。</span><span class="sxs-lookup"><span data-stu-id="2255c-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS カラーピッカーバー](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="2255c-224">色をクリックして選択するか、下方向キーを押して、左方向キーと右方向キーを使用して色を走査します。</span><span class="sxs-lookup"><span data-stu-id="2255c-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="2255c-225">色にアクセスすると、対応する16進値がプレビューされます。</span><span class="sxs-lookup"><span data-stu-id="2255c-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![背景色のプロパティ値のプレビュー](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="2255c-227">カラーバーに必要な色が設定されていない場合は、カラーピッカーのポップアップを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2255c-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="2255c-228">これを開くには、カラーバーの右端にある二重シェブロンをクリックするか、キーボードの下方向キーを1回または2回押します。</span><span class="sxs-lookup"><span data-stu-id="2255c-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS カラーピッカーのポップアップ](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="2255c-230">右側の垂直バーから色をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="2255c-231">これにより、メインウィンドウにその色のグラデーションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="2255c-232">Enter キーを押して縦棒から直接色を選択するか、メインウィンドウ内の任意のポイントをクリックして有効桁数を高くします。</span><span class="sxs-lookup"><span data-stu-id="2255c-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="2255c-233">使用する色がコンピューターの画面に表示される場合は (Visual Studio のユーザーインターフェイス内に存在する必要はありません)、右下にあるスポイトツールを使用して値をキャプチャできます。</span><span class="sxs-lookup"><span data-stu-id="2255c-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="2255c-234">カラーピッカーの下部にあるスライダーを動かすことで、色の不透明度を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="2255c-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="2255c-235">これにより色の値が RGBA 値に変更されます。 RGBA 形式は不透明度を表す可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="2255c-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="2255c-236">色を選択したら、enter キーを押し、セミコロンを入力して、*サイトの .css*ファイルの背景色のエントリを完成させます。</span><span class="sxs-lookup"><span data-stu-id="2255c-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="2255c-237">Page Inspector 更新バー</span><span class="sxs-lookup"><span data-stu-id="2255c-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="2255c-238">Page Inspector は、直ちに*サイトの .css*ファイルへの変更を検出し、更新バーにアラートを表示します。</span><span class="sxs-lookup"><span data-stu-id="2255c-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![更新バー](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="2255c-240">すべてのファイルを保存して Page Inspector ブラウザーを更新するには、Ctrl + Alt + Enter キーを押すか、更新バーをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="2255c-241">強調表示色の変更がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="2255c-242">動的ページ要素の JavaScript へのマッピング</span><span class="sxs-lookup"><span data-stu-id="2255c-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="2255c-243">最新の web アプリケーションでは、多くの場合、ページ内の要素が JavaScript で動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="2255c-244">つまり、これらのページ要素に対応する静的マークアップ (HTML または Razor) はありません。</span><span class="sxs-lookup"><span data-stu-id="2255c-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="2255c-245">バージョン1.3 では、Page Inspector は、ページに動的に追加された項目を対応する JavaScript コードにマップできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2255c-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="2255c-246">この機能を説明するために、[シングルページアプリケーション (SPA) テンプレート](../../../single-page-application/overview/introduction/knockoutjs-template.md)を使用します。</span><span class="sxs-lookup"><span data-stu-id="2255c-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2255c-247">SPA テンプレートには、 [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650)の更新プログラムが必要です。</span><span class="sxs-lookup"><span data-stu-id="2255c-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="2255c-248">Visual Studio で、[**ファイル**&gt;**新しいプロジェクト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="2255c-249">左側で **[ C#ビジュアル]** を展開し、 **[Web]** を選択して、 **[ASP.NET MVC4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="2255c-250">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-250">Click **OK**.</span></span>

<span data-ttu-id="2255c-251">**[新しい ASP.NET MVC 4 プロジェクト]** ダイアログで、 **[シングルページアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="2255c-252">ソリューションエクスプローラーで、 **Views**フォルダーを展開し、 **[ホーム]** フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="2255c-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="2255c-253">Index. cshtml ファイルを右クリックし、 **[Page Inspector で表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2255c-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="2255c-254">Page Inspector ブラウザーに最初に表示されるのは、ログインページです。</span><span class="sxs-lookup"><span data-stu-id="2255c-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="2255c-255">[サインアップ] をクリックし、ユーザー名とパスワードを作成します。</span><span class="sxs-lookup"><span data-stu-id="2255c-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="2255c-256">サインアップすると、アプリケーションがログインし、いくつかのサンプル項目を含む to do リストを作成します。</span><span class="sxs-lookup"><span data-stu-id="2255c-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="2255c-257">**[検査]** をクリックして、検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="2255c-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="2255c-258">Page Inspector ブラウザーで、to do 項目の1つをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2255c-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="2255c-259">青で強調表示されるのではなく、要素がオレンジ色で強調表示され、要素名の横に "JS" が付いていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2255c-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="2255c-260">これは、要素がスクリプトによって動的に作成されたことを示します。</span><span class="sxs-lookup"><span data-stu-id="2255c-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="2255c-261">さらに、 **[呼び出し履歴]** タブにはオレンジ色の下線が表示されます。これは、 **[呼び出し履歴]** ウィンドウに要素に関する詳細情報が含まれていることを示します。</span><span class="sxs-lookup"><span data-stu-id="2255c-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="2255c-262">**[呼び出し履歴]** タブをクリックします。 **[呼び出し履歴]** ウィンドウには、要素を作成した JavaScript 呼び出しの呼び出し履歴が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="2255c-263">JQuery などの外部ライブラリへの呼び出しは折りたたまれているので、アプリケーションスクリプトの呼び出しを簡単に確認できます。</span><span class="sxs-lookup"><span data-stu-id="2255c-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="2255c-264">外部ライブラリの呼び出しを含め、完全なスタックを表示するには、"外部ライブラリ" というラベルが付いたノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="2255c-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="2255c-265">呼び出し履歴の項目をクリックすると、Visual Studio によってコードファイルが開き、対応するスクリプトが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="2255c-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="2255c-266">参照</span><span class="sxs-lookup"><span data-stu-id="2255c-266">See Also</span></span>

<span data-ttu-id="2255c-267">[Visual Studio での ASP.NET MVC 4 の概要](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)(ASP.net web サイト)</span><span class="sxs-lookup"><span data-stu-id="2255c-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="2255c-268">[Page Inspector の概要](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/)(Channel 9 ビデオ)</span><span class="sxs-lookup"><span data-stu-id="2255c-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="2255c-269">[Page Inspector のエラーメッセージ](https://go.microsoft.com/?linkid=9813062)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="2255c-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
