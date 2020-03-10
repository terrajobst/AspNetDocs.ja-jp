---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor) |Microsoft Docs
author: Rick-Anderson
description: この付録では、Visual Studio 2010 または Visual Web Developer 2010 Express を使用して、Razor 構文で ASP.NET Web ページをプログラミングする方法について説明します。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514294"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="7201b-103">Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor)</span><span class="sxs-lookup"><span data-stu-id="7201b-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="7201b-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7201b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7201b-105">この記事では、Visual Studio または Visual Web Developer Express を使用して ASP.NET Web ページ (Razor) web サイトをプログラミングする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7201b-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="7201b-106">学習内容</span><span class="sxs-lookup"><span data-stu-id="7201b-106">What you'll learn</span></span>
>
> - <span data-ttu-id="7201b-107">お使いのバージョンの Visual Studio で ASP.NET Web ページを操作するために必要なもの (ある場合)。</span><span class="sxs-lookup"><span data-stu-id="7201b-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="7201b-108">Visual Web Developer 2010 Express に ASP.NET Web ページのサポートを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7201b-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="7201b-109">Visual Studio の機能を使用して、IntelliSense やデバッガーなどの ASP.NET Razor ページを操作する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7201b-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7201b-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="7201b-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="7201b-111">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="7201b-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="7201b-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7201b-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="7201b-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7201b-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="7201b-114">このチュートリアルは、ASP.NET Web ページ2、Visual Studio 2012、Visual Studio 2010、および WebMatrix 2 でも動作します。</span><span class="sxs-lookup"><span data-stu-id="7201b-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="7201b-115">WebMatrix または他の多くのコードエディターを使用して Razor 構文で ASP.NET Web ページをプログラミングできます。</span><span class="sxs-lookup"><span data-stu-id="7201b-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="7201b-116">Microsoft Visual Studio を使用することもできます。これは、web サイトだけではなく、さまざまな種類のアプリケーションを作成するための強力なツールセットを提供する、フル機能の統合開発環境 (IDE) です。</span><span class="sxs-lookup"><span data-stu-id="7201b-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="7201b-117">ASP.NET Razor ページを操作するには、 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="7201b-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="7201b-118">ASP.NET Razor web ページを使用したプログラミングのために Visual Studio が提供する、次の2つの便利な機能があります。</span><span class="sxs-lookup"><span data-stu-id="7201b-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="7201b-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="7201b-119">*IntelliSense*.</span></span> <span data-ttu-id="7201b-120">Visual Studio に組み込まれている IntelliSense 機能は、WebMatrix の IntelliSense よりも包括的です。</span><span class="sxs-lookup"><span data-stu-id="7201b-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="7201b-121">*デバッガー*。</span><span class="sxs-lookup"><span data-stu-id="7201b-121">*Debugger*.</span></span> <span data-ttu-id="7201b-122">デバッガーを使用すると、実行中のプログラムを停止したり、変数を調べたり、コードを行ごとにステップ実行したりして、コードのトラブルシューティングを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7201b-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="7201b-123">異なるバージョンの ASP.NET Web ページでの Visual Studio の使用</span><span class="sxs-lookup"><span data-stu-id="7201b-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="7201b-124">Visual Studio 2017 で ASP.NET web アプリを開発するには、 **ASP.NET と web 開発**ワークロードをインストールします。</span><span class="sxs-lookup"><span data-stu-id="7201b-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="7201b-125">Visual Studio 2012 および Visual Studio 2013 には ASP.NET Web ページのサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7201b-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="7201b-126">(ASP.NET Web ページをサポートするために必要なパッケージは、Visual Studio のインストール時にインストールされます)。</span><span class="sxs-lookup"><span data-stu-id="7201b-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="7201b-127">Visual Studio 2010 では、ASP.NET Web ページの既定のサポートは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="7201b-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="7201b-128">Visual Studio 2010 で ASP.NET Web ページを使用するには、ASP.NET MVC パッケージをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7201b-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="7201b-129">ASP.NET Web ページ2を取得するには、ASP.NET MVC 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="7201b-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="7201b-130">次の表は、さまざまなバージョンの Visual Studio での ASP.NET Web ページのサポートをまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="7201b-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="7201b-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="7201b-131">Visual Studio 2010</span></span> | <span data-ttu-id="7201b-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="7201b-132">Visual Studio 2012</span></span> | <span data-ttu-id="7201b-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7201b-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7201b-134">**ASP.NET Web ページ2**</span><span class="sxs-lookup"><span data-stu-id="7201b-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="7201b-135">ASP.NET MVC 4 をインストールする</span><span class="sxs-lookup"><span data-stu-id="7201b-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="7201b-136">含める</span><span class="sxs-lookup"><span data-stu-id="7201b-136">(Included)</span></span> | <span data-ttu-id="7201b-137">含める</span><span class="sxs-lookup"><span data-stu-id="7201b-137">(Included)</span></span> |
| <span data-ttu-id="7201b-138">**ASP.NET Web ページ3**</span><span class="sxs-lookup"><span data-stu-id="7201b-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="7201b-139">NuGet を使用して ASP.NET Web ページ3に更新する</span><span class="sxs-lookup"><span data-stu-id="7201b-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="7201b-140">含める</span><span class="sxs-lookup"><span data-stu-id="7201b-140">(Included)</span></span> |

<span data-ttu-id="7201b-141">Visual Studio 2010 を使用するには、「 [Visual studio 2010 での ASP.NET Web ページのサポートのインストール](#vs2010support)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7201b-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="7201b-142">WebMatrix からの Visual Studio の起動</span><span class="sxs-lookup"><span data-stu-id="7201b-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="7201b-143">WebMatrix でプロジェクトを開始し、Visual Studio に切り替えたい場合は、Visual Studio で簡単にプロジェクトを開くためのボタンが WebMatrix に用意されています。</span><span class="sxs-lookup"><span data-stu-id="7201b-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="7201b-144">このボタンを有効にするには、コンピューターに Visual Studio がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7201b-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="7201b-145">次の図は、WebMatrix のボタンを示しています。</span><span class="sxs-lookup"><span data-stu-id="7201b-145">The following image shows the button in WebMatrix.</span></span>

![Visual Studio を起動する](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="7201b-147">このボタンをクリックすると、Visual Studio でプロジェクトが開きます。</span><span class="sxs-lookup"><span data-stu-id="7201b-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="7201b-148">WebMatrix と Visual Studio は、問題なく切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="7201b-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="7201b-149">他の環境でファイルが変更された場合は通知されます。最新の変更を取得するには、ファイルを再読み込みする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7201b-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="7201b-150">Visual Studio での ASP.NET Razor サイトの作成</span><span class="sxs-lookup"><span data-stu-id="7201b-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="7201b-151">Visual Studio で ASP.NET Razor web サイトを作成するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="7201b-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="7201b-152">Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="7201b-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="7201b-153">**[ファイル]** メニューの **[新しい Web サイト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7201b-153">In the **File** menu, click **New Web Site**.</span></span>

    ![新しい web サイトの作成](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="7201b-155">**[新しい Web サイト]** ダイアログボックスで、使用する言語 (ビジュアルC#または Visual Basic) を選択します。</span><span class="sxs-lookup"><span data-stu-id="7201b-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="7201b-156">**[ASP.NET Web Site (Razor)]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="7201b-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor サイト](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="7201b-158">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7201b-158">Click **OK**.</span></span>

<span data-ttu-id="7201b-159">新しいプロジェクトが存在し、作業を開始するのに役立ついくつかの既定の web ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7201b-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="7201b-160">IntelliSense の使用</span><span class="sxs-lookup"><span data-stu-id="7201b-160">Using IntelliSense</span></span>

<span data-ttu-id="7201b-161">サイトを作成したので、Visual Studio での IntelliSense の動作を確認できます。</span><span class="sxs-lookup"><span data-stu-id="7201b-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="7201b-162">先ほど作成した web サイトで、既定の [ *cshtml* ] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="7201b-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="7201b-163">ページの `<h3>` タグの後に、「`@ServerInfo.` (ドットを含む)」と入力します。</span><span class="sxs-lookup"><span data-stu-id="7201b-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="7201b-164">IntelliSense によって、`ServerInfo` ヘルパーの使用可能なメソッドがドロップダウンリストに表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7201b-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="7201b-166">一覧から `GetHtml` メソッドを選択し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="7201b-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="7201b-167">IntelliSense は、メソッドを自動的に入力します。</span><span class="sxs-lookup"><span data-stu-id="7201b-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="7201b-168">(のC#メソッドと同様に、メソッドの後に `()` 文字を追加する必要があります)。`GetHtml` メソッドの完成したコードは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="7201b-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="7201b-169">Ctrl キーを押しながら F5 キーを押して、ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="7201b-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="7201b-170">ブラウザーに表示された場合、ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7201b-170">This is what the page looks like when displayed in a browser:</span></span>

    ![ブラウザーの既定のページ](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="7201b-172">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="7201b-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="7201b-173">デバッガーの使用</span><span class="sxs-lookup"><span data-stu-id="7201b-173">Using the Debugger</span></span>

1. <span data-ttu-id="7201b-174">*既定の cshtml*ページの先頭で、`Page.Title`で始まる行の後に、次のコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="7201b-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="7201b-175">コードの左側にあるエディターの灰色の余白で、*ブレークポイント*を追加するために、この新しい行の横をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7201b-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="7201b-176">ブレークポイントは、その時点でプログラムの実行を停止するようにデバッガーに指示するマーカーで、何が起こっているかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7201b-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![ブレークポイントの設定](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="7201b-178">`ServerInfo.GetHtml` メソッドの呼び出しを削除し、その場所に `@myTime` 変数の呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="7201b-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="7201b-179">この呼び出しでは、新しいコード行によって返される現在の時刻値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7201b-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="7201b-180">F5 キーを押して、デバッガーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="7201b-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="7201b-181">設定したブレークポイントでページが停止します。</span><span class="sxs-lookup"><span data-stu-id="7201b-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="7201b-182">次の図は、エディターでのページの表示とブレークポイント (黄色) を示しています。</span><span class="sxs-lookup"><span data-stu-id="7201b-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![ブレークポイントのデバッグ](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="7201b-184">デバッグ ツールバーで、**ステップイン** ボタンをクリックするか、F11 キーを押して次のコード行を実行します。</span><span class="sxs-lookup"><span data-stu-id="7201b-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="7201b-185">このボタンをクリックするたびに、実行を次のコード行に進めます。</span><span class="sxs-lookup"><span data-stu-id="7201b-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![[ステップイン] ボタン](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="7201b-187">`myTime` 変数の値を確認するには、マウスポインターをその上に置くか、 **[ローカル]** ウィンドウと **[呼び出し履歴]** ウィンドウに表示されている値を調べます。</span><span class="sxs-lookup"><span data-stu-id="7201b-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="7201b-188">Visual Studio では、変数の値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7201b-188">Visual Studio display the value of the variable.</span></span>

    ![時間値の表示](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="7201b-190">変数を調べてコードをステップ実行したら、F5 キーを押して、各行で停止することなくページの実行を続けます。</span><span class="sxs-lookup"><span data-stu-id="7201b-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="7201b-191">すべてのコードのステップ実行が完了すると、ブラウザーにページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7201b-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="7201b-192">デバッガーの詳細と、Visual Studio でコードをデバッグする方法の詳細については、「[チュートリアル: Visual Web Developer での Web ページのデバッグ](https://msdn.microsoft.com/library/z9e7w6cs.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7201b-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="7201b-193">Visual Studio での ASP.NET MVC プロジェクトでの Razor の使用</span><span class="sxs-lookup"><span data-stu-id="7201b-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="7201b-194">Razor 構文は、ASP.NET MVC プロジェクトでも広く使用されています。</span><span class="sxs-lookup"><span data-stu-id="7201b-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="7201b-195">MVC は、動的な web サイトを構築するための強力なパターンベースの方法です。</span><span class="sxs-lookup"><span data-stu-id="7201b-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="7201b-196">ASP.NET Web ページサイトの保守が困難になった場合は、ASP.NET MVC アプリケーションに変換することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="7201b-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="7201b-197">MVC アプリケーションを作成する例については、「[はじめに with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7201b-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="7201b-198">Visual Studio 2010 での ASP.NET Web ページのサポートのインストール</span><span class="sxs-lookup"><span data-stu-id="7201b-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="7201b-199">このセクションでは、Visual Web Developer Express 2010 と ASP.NET Web ページ Tools for Visual Studio をインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7201b-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="7201b-200">Web Platform Installer をまだ持っていない場合は、次の URL からダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="7201b-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="7201b-201">Web Platform Installer を実行します。</span><span class="sxs-lookup"><span data-stu-id="7201b-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="7201b-202">**[製品]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7201b-202">Click the **Products** tab.</span></span>

    ![WebPI 製品タブ](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="7201b-204">**ASP.NET MVC 4** (ASP.NET Web ページ 2) を検索し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7201b-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="7201b-205">これらの製品には、ASP.NET Razor web サイトをビルドするための Visual Studio ツールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7201b-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi インストールオプション](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="7201b-207">**[インストール]** をクリックしてインストールを完了します。</span><span class="sxs-lookup"><span data-stu-id="7201b-207">Click **Install** to complete the installation.</span></span>
