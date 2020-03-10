---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 での ASP.NET と Web 開発の新機能 |Microsoft Docs
author: rick-anderson
description: 新しいバージョンの Visual Studio では、Web テクノロジを使用する際のエクスペリエンスとパフォーマンスの向上に焦点を合わせた多くの拡張機能が導入されています。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422098"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="0955b-103">Visual Studio 2012 の ASP.NET と Web 開発の新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>

<span data-ttu-id="0955b-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="0955b-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="0955b-105">新しいバージョンの Visual Studio では、Web テクノロジを使用する際のエクスペリエンスとパフォーマンスの向上に焦点を合わせた多くの拡張機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="0955b-106">CSS、JavaScript、HTML 用の Visual Studio エディターは、IntelliSense や自動インデントなど、最も多くのオンデマンドコード機能を含むように完全に改良されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="0955b-107">パフォーマンスに関しては、バンドルと縮小が組み込み機能として統合され、ページの読み込み時間を短縮できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="0955b-108">Visual Studio では、最新の web サイトテクノロジを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="0955b-109">クロスブラウザーの CSS3 スニペットを使用すると、新しい HTML5 の要素と機能を利用しながら、クライアントプラットフォームに関係なく、サイトが機能することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="0955b-110">この Visual Studio のバージョンでは、JavaScript コードの記述とプロファイルを簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="0955b-111">IntelliSense の一覧、統合された XML ドキュメントおよびナビゲーション機能を JavaScript コードで使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="0955b-112">これで、JavaScript カタログをすぐに使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="0955b-113">さらに、スクリプトに対する ECMAScript5 の準拠を確認し、初期段階で構文エラーを検出することもできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="0955b-114">最新ではありませんが、この Visual Studio のバージョンでは、組み込みのバンドルと縮小が実装されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="0955b-115">スクリプトファイルとスタイルシートは、サイトの実行速度が速くなるように、パックされて圧縮されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="0955b-116">このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="0955b-117">すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="0955b-118">目標</span><span class="sxs-lookup"><span data-stu-id="0955b-118">Objectives</span></span>

<span data-ttu-id="0955b-119">この実習では、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="0955b-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="0955b-120">CSS エディターでの新機能と強化された機能の使用</span><span class="sxs-lookup"><span data-stu-id="0955b-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="0955b-121">HTML エディターでの新機能と強化された機能の使用</span><span class="sxs-lookup"><span data-stu-id="0955b-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="0955b-122">JavaScript エディターの新機能と機能強化を使用する</span><span class="sxs-lookup"><span data-stu-id="0955b-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="0955b-123">バンドルと縮小の構成と使用</span><span class="sxs-lookup"><span data-stu-id="0955b-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="0955b-124">前提条件</span><span class="sxs-lookup"><span data-stu-id="0955b-124">Prerequisites</span></span>

- <span data-ttu-id="0955b-125">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="0955b-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="0955b-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (セットアップスクリプトの場合-windows 8 および windows Server 2008 R2 に既にインストールされています)</span><span class="sxs-lookup"><span data-stu-id="0955b-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="0955b-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home)または HTML5 に準拠したブラウザー</span><span class="sxs-lookup"><span data-stu-id="0955b-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="0955b-128">手順</span><span class="sxs-lookup"><span data-stu-id="0955b-128">Exercises</span></span>

<span data-ttu-id="0955b-129">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="0955b-130">演習 1: CSS エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="0955b-131">演習 2: HTML エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="0955b-132">演習 3: JavaScript エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="0955b-133">演習 4: バンドルと縮小</span><span class="sxs-lookup"><span data-stu-id="0955b-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="0955b-134">このラボの推定所要時間: **60 分**。</span><span class="sxs-lookup"><span data-stu-id="0955b-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="0955b-135">演習 1: CSS エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="0955b-136">Web 開発者は、CSS 編集に関連する多くの問題に精通している必要があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="0955b-137">CSS スタイルの最大の問題の1つは、ブラウザー間の互換性です。</span><span class="sxs-lookup"><span data-stu-id="0955b-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="0955b-138">場合によっては、サイトにスタイルを適用した後で、別のブラウザーやデバイスでそのスタイルを開いたときに表示が変わることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="0955b-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="0955b-139">そのため、これらの視覚的な問題を修正するにはかなりの時間がかかることがあります。これは、最終的に1つのブラウザーで動作していると、他のブラウザーでは動作しなくなったことを認識します。</span><span class="sxs-lookup"><span data-stu-id="0955b-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="0955b-140">Visual Studio には、開発者が CSS スタイルシートに効果的にアクセスし、作業し、整理するのに役立つ機能が含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="0955b-141">この演習では、有効な組織とエディションの新機能に加え、ブラウザー間の互換性のための CSS3 コードスニペットを使用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="0955b-142">タスク 1-新しいエディター機能</span><span class="sxs-lookup"><span data-stu-id="0955b-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="0955b-143">このタスクでは、CSS エディターの新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="0955b-144">この新しいエディターでは、新しいスマートインデント、強化されたコードコメント、および拡張された IntelliSense リストを利用して生産性を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="0955b-145">**Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="0955b-146">ソリューションエクスプローラーで、 **[スタイル]** フォルダーの下にある**サイトの .css**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="0955b-147">ツールバーに **[テキストエディター]** ツールが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="0955b-148">これを行うには、[ | **ツールバー**の**表示**] メニューオプションを選択し、 **[テキストエディター]** オプションをオンにします。</span><span class="sxs-lookup"><span data-stu-id="0955b-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="0955b-149">この新しいバージョンでは、 **[コメント]** ボタン (![コメントボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) と [コメント解除] ボタン (![コメント**解除ボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)\*\* ) が CSS エディターでも有効になっていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="0955b-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="0955b-150">![エディターと CSS ツールの有効化](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "エディターと CSS ツールの有効化")</span><span class="sxs-lookup"><span data-stu-id="0955b-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="0955b-151">*エディターと CSS ツールの有効化*</span><span class="sxs-lookup"><span data-stu-id="0955b-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="0955b-152">コードをスクロールし、任意の CSS クラス定義を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="0955b-153">**コメント**(![コメントボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) ボタンをクリックして、選択した行にコメントをコメントします。</span><span class="sxs-lookup"><span data-stu-id="0955b-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="0955b-154">次に、**コメント**解除ボタン (![コメント解除ボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)) をクリックして、変更を元に戻します。</span><span class="sxs-lookup"><span data-stu-id="0955b-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="0955b-155">**[折りたたみ]** (![折りたたみ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)) をクリックし、テキストの左余白にある [(![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) 展開)] ボタンを**展開**します。</span><span class="sxs-lookup"><span data-stu-id="0955b-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="0955b-156">これで、使用していないスタイルを表示しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="0955b-157">![CSS クラスの折りたたみ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "CSS クラスの折りたたみ")</span><span class="sxs-lookup"><span data-stu-id="0955b-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="0955b-158">*CSS クラスの折りたたみ*</span><span class="sxs-lookup"><span data-stu-id="0955b-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="0955b-159">スマートインデント機能が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="0955b-160">[**ツール** | **オプション**] メニューオプションを選択し、画面の左側のウィンドウにある **[テキストエディター]**  | [ **CSS** | **書式設定**] ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="0955b-161">**[階層インデント]** オプションをオンにします。</span><span class="sxs-lookup"><span data-stu-id="0955b-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="0955b-162">![階層インデントの有効化](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "階層インデントの有効化")</span><span class="sxs-lookup"><span data-stu-id="0955b-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="0955b-163">*階層インデントの有効化*</span><span class="sxs-lookup"><span data-stu-id="0955b-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="0955b-164">メインクラス定義 (. main) を見つけて、div 要素にスタイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="0955b-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="0955b-165">このコードは自動的に調整されるので、ユーザーは親クラスを一目で確認できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="0955b-166">CSS</span><span class="sxs-lookup"><span data-stu-id="0955b-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="0955b-167">![CSS での階層的な配置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS での階層的な配置")</span><span class="sxs-lookup"><span data-stu-id="0955b-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="0955b-168">*CSS での階層的な配置*</span><span class="sxs-lookup"><span data-stu-id="0955b-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="0955b-169">**Main div**クラスの中で、境界の最後にある**0px;** カーソルを探し、 **enter**キーを押して、IntelliSense の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="0955b-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="0955b-170">「 **Top** 」と入力すると、入力に応じて一覧がどのようにフィルター処理されるかがわかります。</span><span class="sxs-lookup"><span data-stu-id="0955b-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="0955b-171">この一覧には、単語の任意の部分に**top**が含まれている要素が表示されます (以前のバージョンの Visual Studio では、一覧は用語で*始まる*項目によってフィルター処理されます)。</span><span class="sxs-lookup"><span data-stu-id="0955b-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="0955b-172">![CSS における IntelliSense の機能強化](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS における IntelliSense の機能強化")</span><span class="sxs-lookup"><span data-stu-id="0955b-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="0955b-173">*CSS における IntelliSense の機能強化*</span><span class="sxs-lookup"><span data-stu-id="0955b-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="0955b-174">タスク 2-カラーピッカー</span><span class="sxs-lookup"><span data-stu-id="0955b-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="0955b-175">このタスクでは、Visual Studio IntelliSense に統合された新しい CSS カラーピッカーを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="0955b-176">**.Css**で、ヘッダークラス定義 (. header) を見つけて、 **[背景色]** 属性の横にカーソルを置きます。 &quot;:&quot; と &quot;、**そのコード行**の &quot; 文字を #します。</span><span class="sxs-lookup"><span data-stu-id="0955b-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="0955b-177">![カーソルを検索する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "カーソルを検索する")</span><span class="sxs-lookup"><span data-stu-id="0955b-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="0955b-178">*カーソルを検索する*</span><span class="sxs-lookup"><span data-stu-id="0955b-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="0955b-179">**コロン**(:) を削除します。カラーピッカーを表示するには、もう一度書き込みます。</span><span class="sxs-lookup"><span data-stu-id="0955b-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="0955b-180">最初に表示される色は、サイトで最も頻繁に使用される色です。</span><span class="sxs-lookup"><span data-stu-id="0955b-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="0955b-181">白い色をクリックすると、その HTML カラーコード (#fff) によって、スタイルシート内の現在のカラーコードが置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="0955b-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="0955b-182">![カラーピッカー](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span><span class="sxs-lookup"><span data-stu-id="0955b-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="0955b-183">*カラーピッカー*</span><span class="sxs-lookup"><span data-stu-id="0955b-183">*Color picker*</span></span>
3. <span data-ttu-id="0955b-184">カラーピッカーの**展開**(![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) ボタンを押して色のグラデーションを表示し、グラデーションカーソルをドラッグして別の色を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="0955b-185">その後、**スポイト**ボタンをクリックし、画面から任意の色を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="0955b-186">カーソルを移動すると、背景色の値が動的に変化することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="0955b-187">![カラーピッカーのグラデーション](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "カラーピッカーのグラデーション")</span><span class="sxs-lookup"><span data-stu-id="0955b-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="0955b-188">*カラーピッカーのグラデーション*</span><span class="sxs-lookup"><span data-stu-id="0955b-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="0955b-189">**不透明度**スライダーで、セレクターをバーの中央に移動して不透明度を下げます。</span><span class="sxs-lookup"><span data-stu-id="0955b-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="0955b-190">背景色の値が、そのスケールが RGBA に変わることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="0955b-191">![カラーピッカーの不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "カラーピッカーの不透明度")</span><span class="sxs-lookup"><span data-stu-id="0955b-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="0955b-192">*カラーピッカーの不透明度*</span><span class="sxs-lookup"><span data-stu-id="0955b-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-193">CSS3 で RGBA (赤、緑、青、アルファ) の色の定義を使用すると、1つの項目の色の不透明度を定義できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="0955b-194">**不透明度**とは異なり、同様の CSS 属性 **-** RGBA 色も最新のブラウザーと互換性があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="0955b-195">タスク 3-CSS と互換性のあるコードスニペット</span><span class="sxs-lookup"><span data-stu-id="0955b-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="0955b-196">このタスクでは、web サイトにいくつかの機能を実装するために、ブラウザーと互換性のある CSS3 スニペットを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="0955b-197">サイトの **.css**ファイルで、**ヘッダー**の css クラス定義 (. header) を見つけて、 **/\*罫線の半径\*/** プレースホルダーの下にカーソルを置き、新しいスニペットを追加します。</span><span class="sxs-lookup"><span data-stu-id="0955b-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="0955b-198">Enter キーを押して、IntelliSense の一覧を表示し、「 **Radius** **」** と入力してリストをフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="0955b-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="0955b-199">リストから **[罫線-半径]** オプションをダブルクリックして選択し、 **tab**キーを押してスニペットを挿入します。</span><span class="sxs-lookup"><span data-stu-id="0955b-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="0955b-200">次に、半径のサイズをピクセル単位で**入力し、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="0955b-201">たとえば、「 **15px**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="0955b-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="0955b-202">スニペットによって追加された CSS3 属性は、Mozilla および WebKit ベースのブラウザーを含むほとんどの HTML5 準拠ブラウザーで、丸みのある境界線を表示します。</span><span class="sxs-lookup"><span data-stu-id="0955b-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="0955b-203">![境界線を使用する-半径スニペット](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "境界線を使用する-半径スニペット")</span><span class="sxs-lookup"><span data-stu-id="0955b-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="0955b-204">*境界線を使用する-半径スニペット*</span><span class="sxs-lookup"><span data-stu-id="0955b-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="0955b-205">ページスタイル (. ページ) に同じ**罫線**スニペットを適用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="0955b-206">CSS</span><span class="sxs-lookup"><span data-stu-id="0955b-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="0955b-207">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0955b-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="0955b-208">各ページの罫線が丸くなっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="0955b-209">![角の丸み](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "角の丸み")</span><span class="sxs-lookup"><span data-stu-id="0955b-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="0955b-210">*角の丸み*</span><span class="sxs-lookup"><span data-stu-id="0955b-210">*Rounded corners*</span></span>
4. <span data-ttu-id="0955b-211">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="0955b-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="0955b-212">**[スタイル]** フォルダーの下にある**カスタム .css**ファイルを開き、div 内にカーソルを置き**ます。 ul li img**クラスの定義。</span><span class="sxs-lookup"><span data-stu-id="0955b-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="0955b-213">Enter キーを押して IntelliSense の一覧を表示し、「 **box-Shadow** 」と入力し、 **TAB**キーを2回押して、クラス定義内に既定のシャドウコードスニペットを挿入します。</span><span class="sxs-lookup"><span data-stu-id="0955b-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="0955b-214">Shadow 値を**10px 10px 5px #888**に設定します。</span><span class="sxs-lookup"><span data-stu-id="0955b-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="0955b-215">次に、「 **border-radius** 」と入力し、コードスニペットを挿入します。</span><span class="sxs-lookup"><span data-stu-id="0955b-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="0955b-216">「 **15px** 」と入力して半径のサイズを設定し、 **enter**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="0955b-217">![影付きの角の丸み](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "影付きの角の丸み")</span><span class="sxs-lookup"><span data-stu-id="0955b-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="0955b-218">*影付きの角の丸み*</span><span class="sxs-lookup"><span data-stu-id="0955b-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-219">現時点では、Mozilla と Webkit (Chrome、Safari、Konkeror) ブラウザーをサポートするために、対応するプレフィックス (moz、webkit、o) を使用して shadow 属性が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="0955b-220">新しいクラスの div を作成**します。 images ul li img:** **div**の下にマウスポインターを移動し、その中にカーソルを**置きます。**</span><span class="sxs-lookup"><span data-stu-id="0955b-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="0955b-221">CSS</span><span class="sxs-lookup"><span data-stu-id="0955b-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="0955b-222">変換スニペットを挿入するには、「 **transform** 」と入力し、 **tab**キーを2回押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="0955b-223">次に、[**回転] (-15deg)** を入力して、イメージがホバーされるときの回転角度の値を変更します。</span><span class="sxs-lookup"><span data-stu-id="0955b-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="0955b-224">CSS</span><span class="sxs-lookup"><span data-stu-id="0955b-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="0955b-225">**F5**キーを押してソリューションを実行し、CSS3 ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="0955b-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="0955b-226">画像の角が丸く、ボックスの影が付いていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="0955b-227">画像の上にマウスポインターを移動し、回転します。</span><span class="sxs-lookup"><span data-stu-id="0955b-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="0955b-228">![イメージを回転する Transform スニペット](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "イメージを回転する Transform スニペット")</span><span class="sxs-lookup"><span data-stu-id="0955b-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="0955b-229">*イメージを回転する Transform スニペット*</span><span class="sxs-lookup"><span data-stu-id="0955b-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-230">Internet Explorer 10 を使用していて、影が表示されない場合は、ドキュメントモードが IE10 標準に設定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="0955b-231">**F12**キーを押して Internet Explorer 開発者ツールを開き、 **[ドキュメントモード]** をクリックして IE10 標準に変更します。</span><span class="sxs-lookup"><span data-stu-id="0955b-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![about-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="0955b-233">演習 2: HTML エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="0955b-234">Visual Studio には、HTML エディターが強化されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="0955b-235">このバージョンに含まれる機能強化の一部は、HTML ドキュメントのスマートインデント、HTML5 スニペット、HTML 開始タグと終了タグの一致、および HTML 検証です。</span><span class="sxs-lookup"><span data-stu-id="0955b-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="0955b-236">この演習では、web サイトマークアップで作業するときに、これらの変更によって自在がどのように改善されるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="0955b-237">CSS エディターと同様に、HTML エディターも改善されました。</span><span class="sxs-lookup"><span data-stu-id="0955b-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="0955b-238">これらの改善点のほとんどは、Web 開発者の作業が容易になる小さなものです。</span><span class="sxs-lookup"><span data-stu-id="0955b-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="0955b-239">HTML ドキュメント DOCTYPE を対象とする編集や検証を行うときに、HTML5、スマートインデント、一致する開始タグと終了タグのようなものもありますが、これらの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="0955b-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="0955b-240">タスク 1-DOCTYPE 検証の機能強化</span><span class="sxs-lookup"><span data-stu-id="0955b-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="0955b-241">HTML エディターでは、マスターページに定義が存在する場合でも、ページの DOCTYPE をチェックできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="0955b-242">ページの DOCTYPE に応じて、HTML エディターは正しい規則セットで検証し、DOCTYPE 要素を考慮して IntelliSense リストをフィルター処理します。</span><span class="sxs-lookup"><span data-stu-id="0955b-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="0955b-243">このタスクでは、ページの DOCTYPE を変更して、HTML エディターの動作がそれに応じてどのように変化するかを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="0955b-244">まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="0955b-245">**[.Master]** ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="0955b-246">検証ツールバーのターゲットスキーマに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="0955b-247">HTML エディターがどのように動作するか (検証、IntelliSense など) は、Doctype が選択された場合に適切に変更されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="0955b-248">![HTML ソース編集ツールバーで Doctype を使用する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML ソース編集ツールバーで Doctype を使用する")</span><span class="sxs-lookup"><span data-stu-id="0955b-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="0955b-249">*HTML ソース編集ツールバーで Doctype を使用する*</span><span class="sxs-lookup"><span data-stu-id="0955b-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="0955b-250">ターゲットスキーマを HTML 4.01 に変更します。</span><span class="sxs-lookup"><span data-stu-id="0955b-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="0955b-251">![HTML ソース編集ツールバーでの Doctype の変更](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML ソース編集ツールバーでの Doctype の変更")</span><span class="sxs-lookup"><span data-stu-id="0955b-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="0955b-252">*HTML ソース編集ツールバーでの Doctype の変更*</span><span class="sxs-lookup"><span data-stu-id="0955b-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="0955b-253">**Body**要素の下にカーソルを置き、HTML5 要素の名前 ( **video**など) の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="0955b-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="0955b-254">この要素は、IntelliSense の一覧では使用できないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="0955b-255">![HTML5 要素が一覧に含まれていません](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 要素が一覧に含まれていません")</span><span class="sxs-lookup"><span data-stu-id="0955b-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="0955b-256">*HTML5 要素が一覧に含まれていません*</span><span class="sxs-lookup"><span data-stu-id="0955b-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="0955b-257">検証ツールバーのターゲットスキーマへの変更を元に戻します。ドロップダウンリストから [DOCTYPE: XHTML5] を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="0955b-258">![HTML ソース編集ツールバーで Doctype を使用する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML ソース編集ツールバーで Doctype を使用する")</span><span class="sxs-lookup"><span data-stu-id="0955b-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="0955b-259">*HTML ソース編集ツールバーで Doctype をリセットする*</span><span class="sxs-lookup"><span data-stu-id="0955b-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="0955b-260">**Body**要素の下にカーソルを置き、HTML5 要素の入力を開始します (**ビデオ**など)。</span><span class="sxs-lookup"><span data-stu-id="0955b-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="0955b-261">HTML5 要素が IntelliSense の一覧で使用できるようになったことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="0955b-262">![表示されている HTML5 要素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "表示されている HTML5 要素")</span><span class="sxs-lookup"><span data-stu-id="0955b-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="0955b-263">*表示されている HTML5 要素*</span><span class="sxs-lookup"><span data-stu-id="0955b-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="0955b-264">タスク 2-開始タグと終了タグの自動更新</span><span class="sxs-lookup"><span data-stu-id="0955b-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="0955b-265">Visual Studio で、編集中の要素の HTML の開始タグまたは終了タグが相互に一致するように更新されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="0955b-266">この新機能により、HTML タグを編集するときの生産性が向上します。</span><span class="sxs-lookup"><span data-stu-id="0955b-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="0955b-267">**Default.aspx**ページで、タイトルを含む**H3**要素 (たとえば、Visual Studio 2012 の岩!) を追加します。</span><span class="sxs-lookup"><span data-stu-id="0955b-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="0955b-268">**H3**タグを変更し、「 **H2** 」または「H1」と入力し**ます。**</span><span class="sxs-lookup"><span data-stu-id="0955b-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="0955b-269">終了タグが自動的に更新されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="0955b-270">また、終了タグを変更して、それに応じて開始タグが更新されていることを確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="0955b-271">![終了タグの自動更新](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "終了タグの自動更新")</span><span class="sxs-lookup"><span data-stu-id="0955b-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="0955b-272">*終了タグの自動更新*</span><span class="sxs-lookup"><span data-stu-id="0955b-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="0955b-273">タスク 3-新しい HTML5 コードスニペット</span><span class="sxs-lookup"><span data-stu-id="0955b-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="0955b-274">Visual Studio に HTML5 コードスニペットがいくつか追加されました。</span><span class="sxs-lookup"><span data-stu-id="0955b-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="0955b-275">このタスクでは、これらのスニペットのいくつかを使用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="0955b-276">Web サイトフォルダーのルートに、 **audio**という名前の新しいフォルダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="0955b-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="0955b-277">Windows エクスプローラーを開き、 **WhatsNewASPNET**ソリューションの**オーディオ**フォルダーにオーディオファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="0955b-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="0955b-278">**Default.aspx**ページで、Web11 の下にあるカーソルを探します。</span><span class="sxs-lookup"><span data-stu-id="0955b-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="0955b-279">ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="0955b-279">Header.</span></span> <span data-ttu-id="0955b-280">「 **AUDIO** 」と入力し、tab キーを押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="0955b-281">新しい HTML エディターには、HTML5 コンテンツ用のコードスニペットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="0955b-282">HTML5 スニペットを有効にするには、必ず適切な DOCTYPE 定義を使用するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="0955b-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="0955b-283">![HTML5 コードスニペットの挿入](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 コードスニペットの挿入")</span><span class="sxs-lookup"><span data-stu-id="0955b-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="0955b-284">*HTML5 コードスニペットの挿入*</span><span class="sxs-lookup"><span data-stu-id="0955b-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="0955b-285">既存のオーディオファイルを指すようにオーディオソースを更新します。</span><span class="sxs-lookup"><span data-stu-id="0955b-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="0955b-286">この場合、オーディオファイルをソリューションに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="0955b-287">**F5**キーを押してサイトを実行し、オーディオを再生します。</span><span class="sxs-lookup"><span data-stu-id="0955b-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="0955b-288">![オーディオコントロールの実行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "オーディオコントロールの実行")</span><span class="sxs-lookup"><span data-stu-id="0955b-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="0955b-289">*オーディオコントロールの実行*</span><span class="sxs-lookup"><span data-stu-id="0955b-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-290">また、Visual Studio に含まれているその他のスニペット (ビデオ、図など) を試すこともできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="0955b-291">次に、ページの一部にコントロールを挿入してみます。</span><span class="sxs-lookup"><span data-stu-id="0955b-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="0955b-292">たとえば、 **GridView**コントロールを挿入しようとしますが、 **&lt;合わせるを**入力するのではなく、 **&lt;GV**の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="0955b-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="0955b-293">IntelliSense の一覧に**asp: GridView**コントロールが表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="0955b-294">HTML エディターの IntelliSense では、タイトルの大文字と小文字の区別と、部分的な一致 (用語を含むすべての要素の取得) が提供されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="0955b-295">![IntelliSense リストを使用した GridView の挿入](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense リストを使用した GridView の挿入")</span><span class="sxs-lookup"><span data-stu-id="0955b-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="0955b-296">*IntelliSense リストを使用した GridView の挿入*</span><span class="sxs-lookup"><span data-stu-id="0955b-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="0955b-297">**&lt;grid**と入力すると、用語に一致するすべての項目が表示されますが、Visual Studio は**gridview**コントロールを提案します。</span><span class="sxs-lookup"><span data-stu-id="0955b-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="0955b-298">![IntelliSense リストと部分一致を含む GridView の挿入](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense リストと部分一致を含む GridView の挿入")</span><span class="sxs-lookup"><span data-stu-id="0955b-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="0955b-299">*IntelliSense リストと部分一致を含む GridView の挿入*</span><span class="sxs-lookup"><span data-stu-id="0955b-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="0955b-300">タスク 4-HTML エディターのスマートタグ</span><span class="sxs-lookup"><span data-stu-id="0955b-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="0955b-301">HTML エディターのもう1つの改良点は、スマートタグ機能です。</span><span class="sxs-lookup"><span data-stu-id="0955b-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="0955b-302">スマートタグを使用すると、一般的な開発タスクや繰り返し発生する開発タスクを、コントロールごとに簡単に実行できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="0955b-303">この機能は、html デザイナーでは既に使用可能ですが、HTML エディターでは使用できませんでした。</span><span class="sxs-lookup"><span data-stu-id="0955b-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="0955b-304">**[.Master]** を開き、[ **Asp: Menu]** 要素を探します。</span><span class="sxs-lookup"><span data-stu-id="0955b-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="0955b-305">開始タグにカーソルを置き、要素の下部に表示されている小さなグリフをクリックして、[スマートタスク] メニューを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="0955b-306">メニューコントロールに関連する一部のタスクにすばやくアクセスできることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="0955b-307">![メニューコントロールのスマートタスク](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "メニューコントロールのスマートタスク")</span><span class="sxs-lookup"><span data-stu-id="0955b-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="0955b-308">*メニューコントロールのスマートタスク*</span><span class="sxs-lookup"><span data-stu-id="0955b-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="0955b-309">タスク 5-スマートインデント</span><span class="sxs-lookup"><span data-stu-id="0955b-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="0955b-310">HTML のベストプラクティスの1つは、コードを読みやすくするために、入れ子になった要素をインデントすることです。</span><span class="sxs-lookup"><span data-stu-id="0955b-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="0955b-311">Visual Studio 2012 では、コードの記述中にエディターによって要素が自動的にインデントされることがわかります。</span><span class="sxs-lookup"><span data-stu-id="0955b-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="0955b-312">以前のバージョンの Visual Studio では、スマートインデントは XML エディターでは使用できましたが、HTML エディターでは使用できませんでした。</span><span class="sxs-lookup"><span data-stu-id="0955b-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>

1. <span data-ttu-id="0955b-313">HTML エディターのインデントの構成がスマートインデントに設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="0955b-314">これを行うには、[ツール] を選択します。 **[オプション**] メニューオプションをクリックし、[テキストエディター] を選択します。 **HTML |** 画面の左側のウィンドウにある [タブ] ページ。</span><span class="sxs-lookup"><span data-stu-id="0955b-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="0955b-315">[スマートインデント] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="0955b-316">![HTML エディターの設定](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML エディターの設定")</span><span class="sxs-lookup"><span data-stu-id="0955b-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="0955b-317">*HTML エディターの設定*</span><span class="sxs-lookup"><span data-stu-id="0955b-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="0955b-318">**Default.aspx**ページで、audio 要素の下にあるすべてのコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="0955b-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="0955b-319">開いている**オーディオ**要素の末尾にカーソルを置き、 **ENTER キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="0955b-320">カーソルの新しい位置にインデントレベルが追加されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="0955b-321">![HTML エディターでのスマートインデント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML エディターでのスマートインデント")</span><span class="sxs-lookup"><span data-stu-id="0955b-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="0955b-322">*HTML エディターでのスマートインデント*</span><span class="sxs-lookup"><span data-stu-id="0955b-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="0955b-323">削除したコンテンツを使用してオーディオタグを復元するか、変更を保存せずに**default.aspx**を閉じます。</span><span class="sxs-lookup"><span data-stu-id="0955b-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="0955b-324">タスク 6-ユーザーコントロールに抽出する</span><span class="sxs-lookup"><span data-stu-id="0955b-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="0955b-325">コードの一部を関数に抽出するなど、Visual Studio に含まれるリファクタリングツールは、改善を促進し、既存のコードをリファクタリングするための優れた機能です。</span><span class="sxs-lookup"><span data-stu-id="0955b-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="0955b-326">ASP.NET ページに対応するのは、ユーザーコントロールへの HTML コードの抽出です。</span><span class="sxs-lookup"><span data-stu-id="0955b-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="0955b-327">手動で実行するには、新しいユーザーコントロールの作成、ユーザーコントロールへのコードセクションの移動、ユーザーコントロールのタグプレフィックスの登録、最後にページ上のユーザーコントロールのインスタンス化など、いくつかの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="0955b-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="0955b-328">これで、*ユーザーコントロールへ*の新しい Extract ツールによって、これらのすべての手順が自動的に実行されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="0955b-329">このタスクでは、新しい Extract to User Control コンテキスト操作を使用して、選択したコードから新しいユーザーコントロールを生成します。</span><span class="sxs-lookup"><span data-stu-id="0955b-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="0955b-330">**Default.aspx**ページで、 **H2**要素と**audio**要素を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="0955b-331">右クリックして **[ユーザーコントロールに展開]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="0955b-332">![[ユーザーコントロールに展開] メニューオプション](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "[ユーザーコントロールに展開] メニューオプション")</span><span class="sxs-lookup"><span data-stu-id="0955b-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="0955b-333">*[ユーザーコントロールに展開] メニューオプション*</span><span class="sxs-lookup"><span data-stu-id="0955b-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="0955b-334">新しいユーザーコントロールの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="0955b-334">Type a name for the new user control.</span></span> <span data-ttu-id="0955b-335">たとえば、「 **Jukebox**」と入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="0955b-336">![抽出されたユーザーコントロールを保存しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "抽出されたユーザーコントロールを保存しています")</span><span class="sxs-lookup"><span data-stu-id="0955b-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="0955b-337">*抽出されたユーザーコントロールを保存しています*</span><span class="sxs-lookup"><span data-stu-id="0955b-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="0955b-338">選択したコードがユーザーコントロールに抽出され、選択したコードの元の場所が新しいユーザーコントロールのインスタンスに置き換えられたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="0955b-339">![新しいユーザーコントロールを使用するために自動的に更新されたページ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "新しいユーザーコントロールを使用するために自動的に更新されたページ")</span><span class="sxs-lookup"><span data-stu-id="0955b-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="0955b-340">*新しいユーザーコントロールを使用するために自動的に更新されたページ*</span><span class="sxs-lookup"><span data-stu-id="0955b-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="0955b-341">**F5**キーを押してページを実行し、コントロールが動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="0955b-342">演習 3: JavaScript エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="0955b-343">JavaScript コードの記述や編集は、特にアプリケーションのサイズが大きくなり、長いファイルや数百の関数を扱う場合には、簡単なタスクではありません。</span><span class="sxs-lookup"><span data-stu-id="0955b-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="0955b-344">通常、スクリプト開発者は、コードの読みやすさを維持し、ファイル間を移動するために、余分な作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="0955b-345">JQuery のような JavaScript ライブラリが含まれているので、コードの長さが原因でスクリプトナビゲーションが困難になっています。</span><span class="sxs-lookup"><span data-stu-id="0955b-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="0955b-346">Visual Studio によって JavaScript エディターが更新され、コードモードをアクセス可能にして整理できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="0955b-347">または VB エディターにC#既に存在していた Visual Studio の多くの機能は、JavaScript エディターで実装されるようになりました。 [定義へ]、[自動インデント]、[ドキュメントと検証] を記述するときに使用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="0955b-348">IntelliSense の一覧を更新すると、JavaScript 関数カタログをすぐに使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="0955b-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="0955b-349">この演習では、JavaScript エディターの新機能と改善点について学習します。</span><span class="sxs-lookup"><span data-stu-id="0955b-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="0955b-350">ここでは、サンプルファイルを参照し、Visual Studio 2012 内で JavaScript プログラミングをより効率的にするための新しい各特性について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="0955b-351">タスク 1-JavaScript エディターの新機能</span><span class="sxs-lookup"><span data-stu-id="0955b-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="0955b-352">このタスクでは、コードの整理とユーザーエクスペリエンスの向上に重点を置いた、JavaScript エディターの新機能の一部を紹介します。</span><span class="sxs-lookup"><span data-stu-id="0955b-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="0955b-353">まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="0955b-354">**F5**キーを押してアプリケーションを実行し、ナビゲーションバーの JavaScript リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="0955b-355">ページを何度も更新して、カウンターの増加を確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="0955b-356">![ページカウンター](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "ページカウンター")</span><span class="sxs-lookup"><span data-stu-id="0955b-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="0955b-357">*ページカウンター*</span><span class="sxs-lookup"><span data-stu-id="0955b-357">*Page counter*</span></span>
3. <span data-ttu-id="0955b-358">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="0955b-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="0955b-359">**Default.aspx**ページを開き、 **&lt;スクリプト&gt;** ブロック (下図参照) を探します。</span><span class="sxs-lookup"><span data-stu-id="0955b-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="0955b-360">次のコードでは、HTML5 ローカルストレージを使用して、現在のユーザーがページにアクセスした回数を格納する*Pageloadcount*変数を格納します。</span><span class="sxs-lookup"><span data-stu-id="0955b-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="0955b-361">ローカルストレージは、HTML5 標準で導入されたクライアント側のキー値データベースです。</span><span class="sxs-lookup"><span data-stu-id="0955b-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="0955b-362">データは、ユーザーのブラウザー内のローカルコンピューターに保存されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="0955b-363">次の手順に進む前に、DOCTYPE が XHTML5 に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="0955b-364">コードを編集します。 JavaScript 用の IntelliSense には、ローカルストレージやその内部メソッドなどの HTML5 機能が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="0955b-365">![HTML5 JavaScript の javascript 機能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript の javascript 機能")</span><span class="sxs-lookup"><span data-stu-id="0955b-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="0955b-366">*HTML5 JavaScript の javascript 機能*</span><span class="sxs-lookup"><span data-stu-id="0955b-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="0955b-367">スクリプトコードから左中かっこ ( **{** ) をクリックすると、角かっこが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="0955b-368">![角かっこが強調表示される](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "角かっこが強調表示される")</span><span class="sxs-lookup"><span data-stu-id="0955b-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="0955b-369">*角かっこが強調表示される*</span><span class="sxs-lookup"><span data-stu-id="0955b-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="0955b-370">関数**Testautoalign ()** をコメント解除します (3 行を選択すると、 **CTRL** + **K**を使用できます。**CTRL** + **U**) を押して、関数コード内でカーソルを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="0955b-371">2行目を追加するには、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-371">Press enter to append a second line.</span></span> <span data-ttu-id="0955b-372">コードが**アラ**インされ、**自動インデント**されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="0955b-373">![JavaScript コードは自動的にアラインされます](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript コードは自動的にアラインされます")</span><span class="sxs-lookup"><span data-stu-id="0955b-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="0955b-374">*JavaScript コードは自動的にアラインされます*</span><span class="sxs-lookup"><span data-stu-id="0955b-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="0955b-375">タスク 2-JavaScript の検証</span><span class="sxs-lookup"><span data-stu-id="0955b-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="0955b-376">このタスクでは、ECMAScript5 標準の新しい JavaScript 検証について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="0955b-377">この機能を使用すると、準拠している JavaScript コードを記述しながら、サイトを展開する前にスクリプトの問題を回避できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="0955b-378">Visual Studio 2010 では ECMAStript3 準拠が実装されていますが、Visual Studio 2012 では ECMAScript5 準拠が提供されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>

1. <span data-ttu-id="0955b-379">**スクリプト \ カスタム**プロジェクトフォルダーの下にある**ECMA5script5 を**開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="0955b-380">次に、ECMAScript5 standard の検証をテストします。</span><span class="sxs-lookup"><span data-stu-id="0955b-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="0955b-381">ファイルの最初の行で**strict** &quot; direction &quot; 使用して、ECMAScript5 **strict モード**を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="0955b-382">このモードは、過去のエディションのあいまいさを明確にする言語のサブセットで構成され、getter や setter、JSON のライブラリサポート、オブジェクトのプロパティに対する完全なリフレクションなど、いくつかの新機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="0955b-383">まだ開いていない場合は**エラー一覧**を開きます ( **[表示]** メニュー |**エラー一覧**)。</span><span class="sxs-lookup"><span data-stu-id="0955b-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="0955b-384">**関数**の宣言に下線が引かれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="0955b-385">これは、ECMA5 標準関数を言語構造体内で入れ子にすることができないためです。</span><span class="sxs-lookup"><span data-stu-id="0955b-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="0955b-386">下の [エラー一覧] には、警告の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="0955b-387">![JavaScript の検証エラーメッセージ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript の検証エラーメッセージ")</span><span class="sxs-lookup"><span data-stu-id="0955b-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="0955b-388">*JavaScript の検証エラーメッセージ*</span><span class="sxs-lookup"><span data-stu-id="0955b-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="0955b-389">厳密な&quot;方向を**使用する&quot;** をコメントアウトすると、エラーが消えますが、警告は残ります。</span><span class="sxs-lookup"><span data-stu-id="0955b-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="0955b-390">ファイルの最後の行に **&quot;test&quot;** のような文字列を記述します (文字列として指定するには引用符を含めます)。</span><span class="sxs-lookup"><span data-stu-id="0955b-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="0955b-391">文字列の横にピリオドを書き込んで、IntelliSense の一覧を表示し、 **[トリム]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="0955b-392">ECMAScript5 standard では、文字列値と変数にも、trim、大文字、検索、置換などの文字列メソッドが定義されています。</span><span class="sxs-lookup"><span data-stu-id="0955b-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="0955b-393">![JavaScript での IntelliSense の一覧](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript での IntelliSense の一覧")</span><span class="sxs-lookup"><span data-stu-id="0955b-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="0955b-394">*JavaScript での IntelliSense の一覧*</span><span class="sxs-lookup"><span data-stu-id="0955b-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="0955b-395">タスク 3-JavaScript の XML ドキュメント</span><span class="sxs-lookup"><span data-stu-id="0955b-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="0955b-396">このタスクでは、Visual Studio の JavaScript での XML ドキュメントの機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="0955b-397">JavaScript IntelliSense の一覧に、各関数の XML ドキュメントが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="0955b-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="0955b-398">さらに、JavaScript のナビゲーション機能についても説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="0955b-399">[**スクリプト]/[カスタム**プロジェクトフォルダー] にある、 **XMLDoc**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="0955b-400">このファイルには、各 JavaScript 関数に関する XML ドキュメントが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="0955b-401">![IntelliSense に統合された JavaScript XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "IntelliSense に統合された JavaScript XML ドキュメント")</span><span class="sxs-lookup"><span data-stu-id="0955b-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="0955b-402">*IntelliSense に統合された JavaScript XML ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="0955b-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="0955b-403">次に、 **XMLDoc**ファイルの関数を**追加**し、 **test**という名前の新しい関数を作成します。</span><span class="sxs-lookup"><span data-stu-id="0955b-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="0955b-404">**テスト**関数で、2つのパラメーターを受け取る**乗算**関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0955b-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="0955b-405">[ツールヒント] ボックスに、**乗算**関数のドキュメントが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="0955b-406">![JavaScript 関数の XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 関数の XML ドキュメント")</span><span class="sxs-lookup"><span data-stu-id="0955b-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="0955b-407">*JavaScript 関数の XML ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="0955b-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="0955b-408">関数呼び出しステートメントを完了し、*ドット*を入力して、戻り値の IntelliSense リストを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="0955b-409">Visual Studio では、値を数値として扱うドキュメント内の**戻り**値が検出されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="0955b-410">![戻り値の型に関する XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "戻り値の型に関する XML ドキュメント")</span><span class="sxs-lookup"><span data-stu-id="0955b-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="0955b-411">*戻り値の型に関する XML ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="0955b-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="0955b-412">次に、add 関数の呼び出しを挿入します。</span><span class="sxs-lookup"><span data-stu-id="0955b-412">Now, insert a call to add function.</span></span> <span data-ttu-id="0955b-413">JavaScript エディターが関数のオーバーロードをサポートするようになったことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="0955b-414">関数名を記述する場合は、ドキュメントで指定されている使用可能なオーバーロードのいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="0955b-415">![オーバーロードに関する XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "オーバーロードに関する XML ドキュメント")</span><span class="sxs-lookup"><span data-stu-id="0955b-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="0955b-416">*オーバーロードに関する XML ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="0955b-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="0955b-417">**GotoDefinition**ファイルを開き、 **$ () .html ()** 関数呼び出しを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="0955b-418">**Html**でカーソルを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="0955b-419">**F12**キーを押して、定義に移動します。</span><span class="sxs-lookup"><span data-stu-id="0955b-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="0955b-420">**検索**ツールを使用せずに、JavaScript コードにアクセスして閲覧できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0955b-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="0955b-421">コードファイルの一番下にあるシグネチャブロックの前にある jQuery 命令でカーソルを探します。</span><span class="sxs-lookup"><span data-stu-id="0955b-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="0955b-422">**F12**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-422">Press **F12**.</span></span> <span data-ttu-id="0955b-423">JQuery ライブラリファイルに移動します。</span><span class="sxs-lookup"><span data-stu-id="0955b-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="0955b-424">また、 **F12 キー**を使用して jQuery ファイル間を移動することもできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="0955b-425">![JQuery 定義への移動](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "JQuery 定義への移動")</span><span class="sxs-lookup"><span data-stu-id="0955b-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="0955b-426">*JQuery 定義への移動*</span><span class="sxs-lookup"><span data-stu-id="0955b-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="0955b-427">ファイルを保存する前に、GotoDefinition に構文エラーがないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="0955b-428">演習 4: バンドルと縮小</span><span class="sxs-lookup"><span data-stu-id="0955b-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="0955b-429">Web サイトに複数の JavaScript または CSS ファイルが含まれている回数</span><span class="sxs-lookup"><span data-stu-id="0955b-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="0955b-430">これは、バンドルと縮小によってファイルサイズを縮小し、サイトのパフォーマンスを向上させるために役立つ、非常に一般的なシナリオです。</span><span class="sxs-lookup"><span data-stu-id="0955b-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="0955b-431">ASP.NET 4.5 の新しいバンドル機能は、一連の JS または CSS ファイルを1つの要素にパックし、コンテンツを縮小することによってサイズを縮小します (つまり、不要な空白を削除したり、コメントを削除したり、識別子を減らしたりします)。</span><span class="sxs-lookup"><span data-stu-id="0955b-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="0955b-432">ASP.NET 4.5 でのバンドルと縮小は実行時に実行されるため、プロセスでユーザーエージェント (たとえば、IE、Mozilla など) を識別できます。したがって、ユーザーブラウザーを対象にして圧縮を改善します (たとえば、Mozilla 固有のものを削除するなど)。要求が IE から取得された場合)。</span><span class="sxs-lookup"><span data-stu-id="0955b-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="0955b-433">この演習では、ASP.NET 4.5 でさまざまな種類のバンドルと縮小を有効にして使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="0955b-434">タスク 1-NuGet からのバンドルと縮小パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="0955b-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="0955b-435">まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="0955b-436">NuGet パッケージマネージャーコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="0955b-437">そのためには、メニュー**ビュー** | **その他の Windows** | **パッケージマネージャーコンソール**を使用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="0955b-438">![パッケージマネージャー file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole を開く](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "パッケージマネージャーコンソールを開く")</span><span class="sxs-lookup"><span data-stu-id="0955b-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="0955b-439">*パッケージマネージャーコンソールを開く*</span><span class="sxs-lookup"><span data-stu-id="0955b-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="0955b-440">**パッケージマネージャーコンソールで、** 「 **Install-Package Microsoft web.config** 」と入力し、 **enter**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="0955b-441">タスク 2-既定のバンドル</span><span class="sxs-lookup"><span data-stu-id="0955b-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="0955b-442">バンドルと縮小を使用する最も簡単な方法は、既定のバンドルを有効にすることです。</span><span class="sxs-lookup"><span data-stu-id="0955b-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="0955b-443">この方法では、規則を使用して、フォルダー内の JS ファイルと CSS ファイルのバンドルされたバージョンと縮小版を参照できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="0955b-444">このタスクでは、バンドルされた、縮小された JS および CSS ファイルを有効にして参照し、結果の出力を表示する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="0955b-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="0955b-445">まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="0955b-446">**ソリューションエクスプローラー**で、**スタイル**、**スクリプト**作成、および**スクリプト**作成フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="0955b-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="0955b-447">アプリケーションで複数の CSS および JS ファイルが使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="0955b-448">![アプリケーション内の複数のスタイルシートと JavaScript ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "アプリケーション内の複数のスタイルシートと JavaScript ファイル")</span><span class="sxs-lookup"><span data-stu-id="0955b-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="0955b-449">*アプリケーション内の複数のスタイルシートと JavaScript ファイル*</span><span class="sxs-lookup"><span data-stu-id="0955b-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="0955b-450">**Global.asax.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="0955b-451">新しい**web.config**名前空間がファイルの先頭でコメントアウトされていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="0955b-452">Using ディレクティブをコメント解除して、バンドル機能と縮小機能を含めます。</span><span class="sxs-lookup"><span data-stu-id="0955b-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="0955b-453">**Application\_Start**メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="0955b-454">このメソッドでは、次のスニペットに示すように、EnableDefaultBundles の呼び出しをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="0955b-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="0955b-455">これにより、そのフォルダーへのパス、および &quot;CSS&quot; または &quot;JS&quot; サフィックスを使用して、フォルダー内の CSS ファイルのバンドルされたコレクションを参照できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="0955b-456">**最適化 .aspx**ファイルを開き、**コンテンツのヘッド**のコンテンツコントロールを探します。</span><span class="sxs-lookup"><span data-stu-id="0955b-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="0955b-457">CSS ファイルと JS ファイルに参照されるタグが1つあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="0955b-458">このコードはデモを目的としています。</span><span class="sxs-lookup"><span data-stu-id="0955b-458">This code is for demo purposes.</span></span> <span data-ttu-id="0955b-459">サイトのマスターファイルでバンドルを参照するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="0955b-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="0955b-460">このサンプルコードでは、一部のバンドルファイルも、この最後の参照が冗長になるように、サイトのマスターファイルによって参照されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="0955b-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="0955b-461">リンクは**href**属性でバンドル規則を使用して、スタイルとスクリプト \ カスタムフォルダーからすべての CSS または JS ファイルを取得することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="0955b-462">次に示すように、path **scripts/custom/JS**を使用して、**スクリプト/カスタム**フォルダー内のすべての JS ファイルのバンドルと縮小を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="0955b-463">これは、既定のバンドルでの既定の動作です。</span><span class="sxs-lookup"><span data-stu-id="0955b-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="0955b-464">**Styles\Site.css**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="0955b-465">元の CSS ファイルには、インデントされたコード、空白、およびファイルを拡大するコメントが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="0955b-466">(JavaScript ファイルにも空白とコメントが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="0955b-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="0955b-467">![Scripts フォルダー内の元の CSS ファイルの1つ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts フォルダー内の元の CSS ファイルの1つ")</span><span class="sxs-lookup"><span data-stu-id="0955b-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="0955b-468">*Scripts フォルダー内の元の CSS ファイルの1つ*</span><span class="sxs-lookup"><span data-stu-id="0955b-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="0955b-469">**F5**キーを押してアプリケーションを実行し、 **[最適化]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="0955b-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="0955b-470">**[CSS バンドル]** リンクをクリックして、ファイルをダウンロードして開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="0955b-471">バンドルされている縮小されたファイルを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-471">Check out the minified bundled file.</span></span> <span data-ttu-id="0955b-472">空白、コメント、およびインデントの文字がすべて削除され、より小さなファイルが生成されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="0955b-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="0955b-473">![バンドルの CSS ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "バンドルの CSS ファイル")</span><span class="sxs-lookup"><span data-stu-id="0955b-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="0955b-474">*バンドルの CSS ファイル*</span><span class="sxs-lookup"><span data-stu-id="0955b-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="0955b-475">次に、 **[JS バンドル]** リンクをクリックして、JavaScript のバンドルファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="0955b-476">エクスプローラーの警告は無視してかまいません。</span><span class="sxs-lookup"><span data-stu-id="0955b-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="0955b-477">**カスタム**フォルダーにある JavaScript ファイルもバンドルされ、縮小されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="0955b-478">![バンドルした JavaScript ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "バンドルした JavaScript ファイル")</span><span class="sxs-lookup"><span data-stu-id="0955b-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="0955b-479">*バンドルした JavaScript ファイル*</span><span class="sxs-lookup"><span data-stu-id="0955b-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="0955b-480">CSS または JS ファイルの圧縮を有効にすることは、以前の ASP.NET バージョンでははるかに複雑でした。</span><span class="sxs-lookup"><span data-stu-id="0955b-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="0955b-481">ここでは、 *global.asax*ファイルに1行を追加して、バンドルを有効にした後、サイトからバンドルされたファイルを参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="0955b-482">タスク 3-静的なバンドル</span><span class="sxs-lookup"><span data-stu-id="0955b-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="0955b-483">静的なバンドルアプローチでは、バンドルするファイルのセット、参照、および使用される縮小方法をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="0955b-484">このタスクでは、バンドルおよび縮小する特定のファイルセットを定義するように、静的なバンドルを構成します。</span><span class="sxs-lookup"><span data-stu-id="0955b-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="0955b-485">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="0955b-485">Close the browser.</span></span>
2. <span data-ttu-id="0955b-486">**Global.asax.cs**ファイルを開き、 **Application\_Start**メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="0955b-487">次のコードに示すように、静的バンドルコードのコメントを解除します。</span><span class="sxs-lookup"><span data-stu-id="0955b-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="0955b-488">&quot; **~/staticバンドル**&quot; 仮想パスで参照される静的バンドルを定義し、 **addfile**メソッドを使用して指定されたすべてのファイルを縮小するために**JsMinify**を使用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="0955b-489">最後に、静的なバンドルを**bundletable.enableoptimization とき**に追加し、それを有効にします。</span><span class="sxs-lookup"><span data-stu-id="0955b-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="0955b-490">ファイルが同じ場所に配置されていないことに注意してください。これは、既定のバンドルを超えるもう1つの利点です。</span><span class="sxs-lookup"><span data-stu-id="0955b-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="0955b-491">**最適化 .aspx**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="0955b-492">**静的 JS バンドル**へのリンクでは、Global.asax.cs ファイルで静的バンドルを構成したときに宣言したパスが使用されていることに注意してください: **/staticバンドル**。</span><span class="sxs-lookup"><span data-stu-id="0955b-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="0955b-493">**F5**キーを押してアプリケーションを実行し、 **[最適化]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="0955b-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="0955b-494">**[静的な JS バンドル]** リンクをクリックして、ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="0955b-495">バンドルされている縮小された JavaScript ファイルが、パス &quot;/staticバンドル&quot;の下にある静的バンドルファイルに構成されているすべての JavaScript ファイルの出力になっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="0955b-496">![静的な JavaScript ファイルバンドル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "静的な JavaScript ファイルバンドル")</span><span class="sxs-lookup"><span data-stu-id="0955b-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="0955b-497">*静的な JavaScript ファイルバンドル*</span><span class="sxs-lookup"><span data-stu-id="0955b-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="0955b-498">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="0955b-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="0955b-499">タスク 4-動的なフォルダーバンドル</span><span class="sxs-lookup"><span data-stu-id="0955b-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="0955b-500">このタスクでは、動的フォルダーバンドルを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="0955b-501">動的バンドルの機能として、静的な JavaScript を含めることができます。また、JavaScript にコンパイルされる言語の他のファイルも含めることができるため、バンドルを実行する前に処理が必要になります。</span><span class="sxs-lookup"><span data-stu-id="0955b-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="0955b-502">この例では、 **Dynamicfolderbundle**クラスを使用して、CofeeScript で記述されたファイルの動的バンドルを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="0955b-503">CofeeScript は javascript にコンパイルされるプログラミング言語で、javascript コードを記述するための簡単な構文を提供し、JavaScript の簡潔さと読みやすさを強化します。</span><span class="sxs-lookup"><span data-stu-id="0955b-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="0955b-504">**Global.asax.cs**ファイルを開き、 **Application\_Start**メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="0955b-505">次のコードに示すように、動的バンドルコードのコメントを解除します。</span><span class="sxs-lookup"><span data-stu-id="0955b-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="0955b-506">**CoffeeMinify**カスタム縮小プロセッサを使用する動的フォルダーバンドルを定義します **。** これは、&quot;の&quot; 拡張機能 (CoffeeScript files) を持つファイルにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="0955b-507">検索パターンを使用して、フォルダー内にバンドルするファイルを選択することができます。たとえば、"\*. コーヒー" のようにします。</span><span class="sxs-lookup"><span data-stu-id="0955b-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="0955b-508">NuGet パッケージマネージャーコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="0955b-509">そのためには、メニュー**ビュー** | **その他の Windows** | **パッケージマネージャーコンソール**を使用します。</span><span class="sxs-lookup"><span data-stu-id="0955b-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="0955b-510">**パッケージマネージャーコンソールで、** 「 **CoffeeSharp** 」と入力し、 **enter**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="0955b-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="0955b-511">**[ソリューションエクスプローラー]** ウィンドウの **[すべてのファイルを表示]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="0955b-512">![すべてのファイルを表示](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "すべてのファイルを表示")</span><span class="sxs-lookup"><span data-stu-id="0955b-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="0955b-513">*すべてのファイルを表示*</span><span class="sxs-lookup"><span data-stu-id="0955b-513">*Showing all files*</span></span>
6. <span data-ttu-id="0955b-514">**ソリューションエクスプローラー**で**CoffeeMinify.cs**ファイルを右クリックし、 **[プロジェクトに含める]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="0955b-515">![CoffeeMinify.cs ファイルをプロジェクトに含める](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "CoffeeMinify.cs ファイルをプロジェクトに含める")</span><span class="sxs-lookup"><span data-stu-id="0955b-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="0955b-516">*CoffeeMinify.cs ファイルをプロジェクトに含める*</span><span class="sxs-lookup"><span data-stu-id="0955b-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="0955b-517">**CoffeeMinify.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="0955b-518">このクラスは、JsMinify から継承して、CoffeeScript コードのコンパイルによって生成される JavaScript 出力を縮小します。</span><span class="sxs-lookup"><span data-stu-id="0955b-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="0955b-519">まず、CoffeeScript コンパイラを呼び出して JavaScript コードを生成します。次に、そのコードを JsMinify メソッドに送信して、結果のコードを縮小します。</span><span class="sxs-lookup"><span data-stu-id="0955b-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="0955b-520">**Scripts/バンドル**フォルダーから**Script1**ファイルと**Script2**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="0955b-521">これらのファイルには、CoffeeMinify クラスでのバンドルの実行中にコンパイルされる CoffeScript コードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0955b-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="0955b-522">わかりやすくするために、提供される CoffeeScript ファイルには CoffeeScript サンプルコードのみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="0955b-523">コメントは JsMinify プロセスによって除外されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="0955b-524">![CoffeeScript ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript ファイル")</span><span class="sxs-lookup"><span data-stu-id="0955b-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="0955b-525">*CoffeeScript ファイル*</span><span class="sxs-lookup"><span data-stu-id="0955b-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-526">[CofeeScript](https://github.com/jashkenas/coffeescript/)は、javascript コードを記述したり、javascript の簡潔さと読みやすさを強化したり、配列の認識やパターンマッチングなどの他の機能を追加したりするための、より単純な構文を提供します。</span><span class="sxs-lookup"><span data-stu-id="0955b-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="0955b-527">**最適化 .aspx**ファイルを開き、バンドルリンクを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0955b-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="0955b-528">動的な**JS バンドル**へのリンクは、動的フォルダーバンドル用に構成した **/コーヒー**サフィックスを使用して、 **Scripts/バンドル**フォルダーを参照していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="0955b-529">**F5**キーを押してアプリケーションを実行し、 **[最適化]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="0955b-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="0955b-530">**[動的 JS バンドル]** リンクをクリックして、生成されたファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="0955b-531">このバンドルに含まれていたコンテンツには、**コーヒー**ファイルのみが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0955b-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="0955b-532">CoffeeScript コードが JavaScript にコンパイルされ、コメントアウトされた行が削除されていることを確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="0955b-533">![動的 JS ファイルバンドル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "動的 JS ファイルバンドル")</span><span class="sxs-lookup"><span data-stu-id="0955b-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="0955b-534">*動的 JS ファイルバンドル*</span><span class="sxs-lookup"><span data-stu-id="0955b-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="0955b-535">また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="0955b-536">まとめ</span><span class="sxs-lookup"><span data-stu-id="0955b-536">Summary</span></span>

<span data-ttu-id="0955b-537">このラボでは、Visual Studio 2012 の ASP.NET および Web 開発の新機能と、Visual Studio 2012 のさまざまな拡張機能を活用する方法を理解することができます。</span><span class="sxs-lookup"><span data-stu-id="0955b-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="0955b-538">このハンズオンラボでは、CSS、JavaScript、HTML 用に Visual Studio 2012 エディターの新機能と機能強化を使用する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="0955b-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="0955b-539">また、Visual Studio 2012 が組み込みのバンドルと縮小を実装する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="0955b-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="0955b-540">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="0955b-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="0955b-541">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="0955b-542">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="0955b-543">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="0955b-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="0955b-544">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="0955b-545">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-545">Click on **Install Now**.</span></span> <span data-ttu-id="0955b-546">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="0955b-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="0955b-547">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="0955b-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="0955b-548">![Visual Studio Express のインストール](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="0955b-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="0955b-549">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="0955b-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="0955b-550">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="0955b-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="0955b-552">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="0955b-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="0955b-553">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="0955b-553">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="0955b-555">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="0955b-555">*Installation progress*</span></span>
6. <span data-ttu-id="0955b-556">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-556">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="0955b-558">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="0955b-558">*Installation completed*</span></span>
7. <span data-ttu-id="0955b-559">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="0955b-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="0955b-560">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="0955b-562">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="0955b-562">*VS Express for Web tile*</span></span>

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0955b-563">付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="0955b-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="0955b-564">この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="0955b-565">タスク 1-Windows Azure ポータルから新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="0955b-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="0955b-566">[Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="0955b-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-567">Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="0955b-568">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-568">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="0955b-569">![Windows Azure portal にログオンします。](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="0955b-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="0955b-570">*Windows Azure 管理ポータルにログオンします。*</span><span class="sxs-lookup"><span data-stu-id="0955b-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="0955b-571">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="0955b-572">![新しい Web サイトの作成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="0955b-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="0955b-573">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="0955b-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="0955b-574">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="0955b-575">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="0955b-576">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-577">Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="0955b-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="0955b-578">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="0955b-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="0955b-579">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="0955b-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="0955b-580">![簡易作成を使用した新しい Web サイトの作成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="0955b-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="0955b-581">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="0955b-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="0955b-582">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="0955b-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="0955b-583">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="0955b-584">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="0955b-585">![新しい web サイトを参照しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="0955b-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="0955b-586">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="0955b-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="0955b-587">![実行中の Web サイト](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="0955b-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="0955b-588">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="0955b-588">*Web site running*</span></span>
6. <span data-ttu-id="0955b-589">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="0955b-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="0955b-590">![Web サイトの管理ページを開く](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="0955b-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="0955b-591">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="0955b-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="0955b-592">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-593">*発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="0955b-594">発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0955b-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="0955b-595">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="0955b-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="0955b-596">![Web サイト発行プロファイルをダウンロードしています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="0955b-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="0955b-597">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="0955b-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="0955b-598">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0955b-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="0955b-599">この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0955b-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="0955b-600">![発行プロファイルファイルを保存しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="0955b-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="0955b-601">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="0955b-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="0955b-602">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="0955b-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="0955b-603">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="0955b-604">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="0955b-605">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="0955b-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="0955b-606">サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="0955b-607">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="0955b-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="0955b-608">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="0955b-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="0955b-609">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="0955b-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="0955b-610">![SQL Database サーバーダッシュボード](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="0955b-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="0955b-611">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="0955b-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="0955b-612">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0955b-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="0955b-613">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** から ip アドレスを選択して、 **[開始 Ip アドレス]** および **[終了 ip アドレス]** ボックスに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="0955b-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="0955b-614">規則の名前を入力し、[![の追加]](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="0955b-616">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="0955b-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="0955b-617">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="0955b-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="0955b-619">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="0955b-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0955b-620">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="0955b-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="0955b-621">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="0955b-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="0955b-622">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0955b-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="0955b-623">![アプリケーションの発行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="0955b-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="0955b-624">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="0955b-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="0955b-625">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="0955b-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="0955b-626">![発行プロファイルをインポートしています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="0955b-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="0955b-627">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="0955b-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="0955b-628">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-628">Click **Validate Connection**.</span></span> <span data-ttu-id="0955b-629">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0955b-630">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="0955b-631">![接続の検証](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="0955b-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="0955b-632">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="0955b-632">*Validating connection*</span></span>
4. <span data-ttu-id="0955b-633">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="0955b-634">![Web deploy の構成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="0955b-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="0955b-635">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="0955b-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="0955b-636">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="0955b-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="0955b-637">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="0955b-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="0955b-638">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="0955b-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="0955b-639">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="0955b-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="0955b-640">新しいデータベース名を入力します (例: *MVC4SampleDB*)。</span><span class="sxs-lookup"><span data-stu-id="0955b-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="0955b-641">![変換先の接続文字列を構成しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="0955b-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="0955b-642">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="0955b-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="0955b-643">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="0955b-643">Then click **OK**.</span></span> <span data-ttu-id="0955b-644">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="0955b-645">![データベースの作成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="0955b-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="0955b-646">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="0955b-646">*Creating the database*</span></span>
7. <span data-ttu-id="0955b-647">Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="0955b-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="0955b-648">続けて、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-648">Then click **Next**.</span></span>

    <span data-ttu-id="0955b-649">![SQL Database を指す接続文字列](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="0955b-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="0955b-650">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="0955b-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="0955b-651">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0955b-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="0955b-652">![Web アプリケーションの発行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="0955b-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="0955b-653">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="0955b-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="0955b-654">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="0955b-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="0955b-655">![Windows Azure に発行されたアプリケーション](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure に発行されたアプリケーション")</span><span class="sxs-lookup"><span data-stu-id="0955b-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="0955b-656">*Windows Azure に発行されたアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="0955b-656">*Application published to Windows Azure*</span></span>
