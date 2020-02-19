---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 モバイル機能 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルの MVC 5 バージョンは、Azure Websites での ASP.NET MVC 5 モバイル Web アプリケーションのデプロイに関するページでコードサンプルと共に使用できます。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457649"
---
# <a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="2b8f9-103">ASP.NET MVC 4 のモバイル機能</span><span class="sxs-lookup"><span data-stu-id="2b8f9-103">ASP.NET MVC 4 Mobile Features</span></span>

<span data-ttu-id="2b8f9-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="2b8f9-105">このチュートリアルの MVC 5 バージョンは、 [Azure websites での ASP.NET MVC 5 モバイル Web アプリケーションのデプロイ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)に関するページでコードサンプルと共に使用できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>

<span data-ttu-id="2b8f9-106">このチュートリアルでは、ASP.NET MVC 4 Web アプリケーションでモバイル機能を使用する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="2b8f9-107">このチュートリアルでは、 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)または Visual web Developer 2010 Express Service Pack 1 (&quot;Visual web developer または vwd&quot;) を使用できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="2b8f9-108">既にお持ちの場合は、Visual Studio の professional バージョンを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="2b8f9-109">開始する前に、以下に示す前提条件がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="2b8f9-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (推奨) または Visual Studio Web DEVELOPER Express SP1。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="2b8f9-111">Visual Studio 2012 には ASP.NET MVC 4 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="2b8f9-112">Visual Web Developer 2010 を使用している場合は、 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="2b8f9-113">モバイル ブラウザー エミュレーターも必要です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="2b8f9-114">次のいずれでも動作します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-114">Any of the following will work:</span></span>

- <span data-ttu-id="2b8f9-115">[Windows 7 Phone エミュレーター](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="2b8f9-116">(これは、このチュートリアルのほとんどのスクリーンショットで使用されるエミュレーターです)。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="2b8f9-117">IPhone をエミュレートするようにユーザーエージェント文字列を変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="2b8f9-118">[この](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)ブログエントリを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="2b8f9-119">Opera Mobile エミュレーター</span><span class="sxs-lookup"><span data-stu-id="2b8f9-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="2b8f9-120">ユーザーエージェントが iPhone に設定されている[Apple Safari](http://www.apple.com/safari/download/) 。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="2b8f9-121">Safari のユーザーエージェントを "iPhone" に設定する方法については、David Alison のブログで[safari でその IE を使用する方法](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)に関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="2b8f9-122">次のトピック用に、C# のソース コードを使用した Visual Studio プロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="2b8f9-123">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="2b8f9-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="2b8f9-124">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="2b8f9-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="2b8f9-125">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="2b8f9-125">What You'll Build</span></span>

<span data-ttu-id="2b8f9-126">このチュートリアルでは、[スタートプロジェクト](https://go.microsoft.com/fwlink/?LinkId=228307)に用意されている単純な会議一覧アプリケーションにモバイル機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="2b8f9-127">次のスクリーンショットは、 [Windows 7 Phone エミュレーター](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)での完成したアプリケーションの [タグ] ページを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="2b8f9-128">キーボード入力を簡略化するには、「 [Windows Phone Emulator のキーボードマップ](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="2b8f9-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="2b8f9-130">Internet Explorer バージョン9または10、FireFox、または Chrome を使用して、[ユーザーエージェント文字列](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)を設定することにより、モバイルアプリケーションを開発できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="2b8f9-131">次の図は、iPhone をエミュレートする Internet Explorer を使用した完成したチュートリアルを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="2b8f9-132">Internet Explorer の開発者用ツールと[Fiddler ツール](http://www.fiddler2.com/fiddler2/)を使用すると、アプリケーションのデバッグに役立てることができます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="2b8f9-133">学習内容</span><span class="sxs-lookup"><span data-stu-id="2b8f9-133">Skills You'll Learn</span></span>

<span data-ttu-id="2b8f9-134">ここでは次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="2b8f9-135">ASP.NET MVC 4 テンプレートで HTML5 `viewport` 属性とアダプティブレンダリングを使用してモバイルデバイスの表示を向上させる方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="2b8f9-136">モバイル専用のビューを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="2b8f9-137">ユーザーがモバイルビューとアプリケーションのデスクトップビューを切り替えることができるビュースイッチャーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="2b8f9-138">作業の開始</span><span class="sxs-lookup"><span data-stu-id="2b8f9-138">Getting Started</span></span>

<span data-ttu-id="2b8f9-139">次のリンクを使用して、スタートプロジェクトのカンファレンスリストアプリケーションを[ダウンロードします。](https://go.microsoft.com/fwlink/?LinkId=228307)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="2b8f9-140">次に、Windows エクスプローラーで*Mvcmobile .zip*ファイルを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="2b8f9-141">**[Mvcmobile. .zip のプロパティ]** ダイアログボックスで、 **[ブロック解除]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="2b8f9-142">(ブロックを解除すると、Web からダウンロードした *.zip* ファイルを使おうとしたときに表示されるセキュリティに関する警告を回避できます)。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="2b8f9-144">*Mvcmobile .zip*ファイルを右クリックし、 **[すべて展開]** を選択して、ファイルを解凍します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="2b8f9-145">Visual Studio で、 *Mvcmobile .sln*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="2b8f9-146">CTRL キーを押しながら F5 キーを押してアプリケーションを実行すると、アプリケーションがデスクトップブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="2b8f9-147">モバイルブラウザーエミュレーターを起動し、会議アプリケーションの URL をエミュレーターにコピーして、 **[タグで参照]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="2b8f9-148">Windows Phone Emulator を使用している場合は、URL バー内をクリックし、Pause キーを押して、キーボードアクセスを取得します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="2b8f9-149">次の画像は、( **[タグで参照]** を選択した) *alltags*ビューを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="2b8f9-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="2b8f9-151">モバイル デバイス上でも読みやすい表示になっています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="2b8f9-152">[ASP.NET] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="2b8f9-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="2b8f9-154">ASP.NET タグビューが非常に乱雑になっています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="2b8f9-155">たとえば、**日付**列の読み取りが非常に困難です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="2b8f9-156">このチュートリアルの後半では、モバイルブラウザー専用の*Alltags*ビューのバージョンを作成します。これにより、ディスプレイが読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="2b8f9-157">注: 現在、モバイルキャッシュエンジンにはバグが存在します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="2b8f9-158">実稼働アプリケーションの場合は、[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget パッケージをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="2b8f9-159">修正の詳細については、「 [ASP.NET MVC 4 Mobile Cache Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="2b8f9-160">CSS メディアクエリ</span><span class="sxs-lookup"><span data-stu-id="2b8f9-160">CSS Media Queries</span></span>

<span data-ttu-id="2b8f9-161">[Css メディアクエリ](http://www.w3.org/TR/css3-mediaqueries/)は、メディアの種類に対する css の拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="2b8f9-162">特定のブラウザー (ユーザーエージェント) の既定の CSS 規則を上書きする規則を作成できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="2b8f9-163">モバイルブラウザーを対象とする CSS の一般的な規則は、画面の最大サイズを定義することです。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="2b8f9-164">新しい ASP.NET MVC 4 インターネットプロジェクトを作成するときに作成される*Contentsite.css*ファイルには、次のメディアクエリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="2b8f9-165">ブラウザーウィンドウが850ピクセル幅以下である場合は、このメディアブロック内の CSS ルールが使用されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="2b8f9-166">このような CSS メディアクエリを使用すると、デスクトップブラウザーの幅が広くなるように設計された既定の CSS 規則よりも小さいブラウザー (モバイルブラウザーなど) で HTML コンテンツをより適切に表示できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="2b8f9-167">ビューポートメタタグ</span><span class="sxs-lookup"><span data-stu-id="2b8f9-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="2b8f9-168">ほとんどのモバイルブラウザーでは、モバイルデバイスの実際の幅よりはるかに大きい仮想ブラウザーウィンドウの幅 (*ビューポート*) が定義されています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="2b8f9-169">これにより、モバイルブラウザーは web ページ全体を仮想ディスプレイ内に収めることができます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="2b8f9-170">ユーザーは、興味深いコンテンツにズームインできます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="2b8f9-171">ただし、ビューポートの幅を実際のデバイスの幅に設定した場合、コンテンツがモバイルブラウザーに収まるため、ズームは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="2b8f9-172">ASP.NET MVC 4 レイアウトファイルのビューポート `<meta>` タグによって、ビューポートがデバイスの幅に設定されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="2b8f9-173">次の行は、ASP.NET MVC 4 レイアウトファイルのビューポート `<meta>` タグを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="2b8f9-174">CSS メディアクエリとビューポートメタタグの効果を調べる</span><span class="sxs-lookup"><span data-stu-id="2b8f9-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="2b8f9-175">エディターで*Views\Shared\\_Layout*ファイルを開き、ビューポート `<meta>` タグをコメントアウトします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="2b8f9-176">次のマークアップは、コメントアウトされた行を示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="2b8f9-177">エディターで*MvcMobile\Content\Site.css*ファイルを開き、メディアクエリの最大の幅を0ピクセルに変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="2b8f9-178">これにより、モバイルブラウザーで CSS ルールが使用されなくなります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="2b8f9-179">次の行は、変更されたメディアクエリを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="2b8f9-180">変更を保存し、モバイルブラウザーエミュレーターで会議アプリケーションを参照します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="2b8f9-181">次の図の小さなテキストは、ビューポート `<meta>` タグを削除した結果です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="2b8f9-182">ビューポート `<meta>` タグがない場合、ブラウザーは既定のビューポートの幅 (ほとんどのモバイルブラウザーでは850ピクセル以上) にズームアウトします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="2b8f9-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="2b8f9-184">変更を元に戻して、レイアウトファイルのビューポート `<meta>` タグのコメントを解除し、メディアクエリを*サイト .css*ファイルの850ピクセルに復元します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="2b8f9-185">変更を保存し、モバイルブラウザーを最新の状態に更新して、モバイル対応のディスプレイが復元されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="2b8f9-186">ビューポート `<meta>` タグと CSS メディアクエリは ASP.NET MVC 4 に固有のものではなく、すべての web アプリケーションでこれらの機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="2b8f9-187">ただし、新しい ASP.NET MVC 4 プロジェクトを作成するときに生成されるファイルに組み込まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="2b8f9-188">ビューポート `<meta>` タグの詳細については、「 [tale of two」の2つのビューポート](http://www.quirksmode.org/mobile/viewports2.html)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="2b8f9-189">次のセクションでは、モバイル ブラウザー専用ビューを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="2b8f9-190">ビュー、レイアウト、および部分ビューのオーバーライド</span><span class="sxs-lookup"><span data-stu-id="2b8f9-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="2b8f9-191">ASP.NET MVC 4 の重要な新機能は、モバイルブラウザー全般、個々のモバイルブラウザー、または特定のブラウザーに対して、すべてのビュー (レイアウトと部分ビューを含む) を上書きできる単純なメカニズムです。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="2b8f9-192">モバイル専用ビューを用意するには、ビュー ファイルをコピーして *.Mobile* をファイル名に追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="2b8f9-193">たとえば、モバイル*インデックス*ビューを作成するには、 *Views\Home\Index.cshtml*を*Views\Home\Index.Mobile.cshtml*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="2b8f9-194">このセクションでは、モバイル専用のレイアウト ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="2b8f9-195">開始するには、 *Views\Shared\\_Layout*を*Views\Shared\\_Layout*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="2b8f9-196">*\_Layout*を開き、 **MVC4 カンファレンス**から**カンファレンス (Mobile)** にタイトルを変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="2b8f9-197">各 `Html.ActionLink` 呼び出しで、各リンク*html.actionlink*の "Browse by" を削除します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="2b8f9-198">次のコードは、モバイルレイアウトファイルの完成した body セクションを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="2b8f9-199">*Views\Home\AllTags.cshtml*ファイルを*Views\Home\AllTags.Mobile.cshtml*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="2b8f9-200">新しいファイルを開き、次のように `<h2>` 要素を「Tags」から「Tags (M)」に変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="2b8f9-201">デスクトップ ブラウザー、および、モバイル ブラウザー エミュレーターを使用してタグ ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="2b8f9-202">モバイルブラウザーエミュレーターには、2つの変更が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="2b8f9-203">[![p2m_layoutTags](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="2b8f9-204">これに対して、デスクトップの表示は変更されていません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="2b8f9-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="2b8f9-206">ブラウザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="2b8f9-206">Browser-Specific Views</span></span>

<span data-ttu-id="2b8f9-207">モバイル専用のビューやデスクトップ専用のビューに加え、個別のブラウザーに対してビューを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="2b8f9-208">たとえば、iPhone ブラウザー専用のビューを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="2b8f9-209">このセクションでは、iPhone ブラウザーと iPhone バージョンの *AllTags* ビュー用のレイアウトを作成します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="2b8f9-210">*Global.asax*ファイルを開き、次のコードを `Application_Start` メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="2b8f9-211">このコードでは、"iPhone" という表示モードを定義し、受信された各要求をその定義に対して照合します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="2b8f9-212">受信された要求が定義した条件に一致する場合 (つまり、ユーザー エージェントに "iPhone" という文字列が含まれている場合)、"iPhone" というサフィックスが含まれる名前のビューが ASP.NET MVC によって検索されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="2b8f9-213">コードで、`DefaultDisplayMode` を右クリックし、 **[解決]** 、`using System.Web.WebPages;` の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="2b8f9-214">`System.Web.WebPages` 型と `DisplayModes` 型が定義されている `DefaultDisplayMode` 名前空間に参照が追加されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="2b8f9-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="2b8f9-216">別の方法として、単純にファイルの `using` セクションに、次の行を手動で追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="2b8f9-217">*Global.asax*ファイルの完全な内容を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="2b8f9-218">変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-218">Save the changes.</span></span> <span data-ttu-id="2b8f9-219">*MvcMobile\Views\Shared\\_Layout* *\\_Layout*にコピーします。このファイルは、MvcMobile\Views\Shared にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="2b8f9-220">新しいファイルを開き、`h1` 見出しを `Conference (Mobile)` から `Conference (iPhone)`に変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="2b8f9-221">*MvcMobile\Views\Home\AllTags.Mobile.cshtml*ファイルを*MvcMobile\Views\Home\AllTags.iPhone.cshtml*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="2b8f9-222">新しいファイルで、 `<h2>` 要素を "Tags (M)" から "Tags (iPhone)" に変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="2b8f9-223">アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-223">Run the application.</span></span> <span data-ttu-id="2b8f9-224">モバイル ブラウザー エミュレーターを実行し、ユーザー エージェントが "iPhone" に設定されていることを確認して、 *AllTags* ビューにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="2b8f9-225">次のスクリーンショットは、 [Safari](http://www.apple.com/safari/download/)ブラウザーに表示される*alltags*ビューを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="2b8f9-226">Windows 用 Safari は[こちら](https://support.apple.com/kb/DL1531)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="2b8f9-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="2b8f9-228">このセクションでは、モバイル レイアウトとビューの作成方法および iPhone などの特定のデバイス専用のレイアウトとビューの作成方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="2b8f9-229">次のセクションでは、より説得力のあるモバイルビューに jQuery Mobile を活用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="2b8f9-230">JQuery Mobile の使用</span><span class="sxs-lookup"><span data-stu-id="2b8f9-230">Using jQuery Mobile</span></span>

<span data-ttu-id="2b8f9-231">[JQuery mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)ライブラリには、すべての主要なモバイルブラウザーで動作するユーザーインターフェイスフレームワークが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="2b8f9-232">jQuery Mobile は、CSS と JavaScript をサポートするモバイルブラウザーに*プログレッシブ拡張機能*を適用します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="2b8f9-233">プログレッシブ拡張機能を使用すると、すべてのブラウザーが web ページの基本コンテンツを表示できるようになります。一方、より強力なブラウザーやデバイスでは、より豊富な表示を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="2b8f9-234">JQuery Mobile のスタイルに含まれる JavaScript ファイルと CSS ファイルは、マークアップを変更することなく、モバイルブラウザーに合わせて多数の要素に対応しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="2b8f9-235">このセクションでは、jquery Mobile とビュースイッチャーウィジェットをインストールする*jquery*の NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="2b8f9-236">最初に、前の手順で作成した*共有\\_Layout* 、_Layout、および*共有\\* を削除します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="2b8f9-237">*Views\Home\AllTags.Mobile.cshtml*ファイルと*Views\Home\AllTags.iPhone.cshtml*ファイルの名前を*Views\Home\AllTags.iPhone.cshtml.hide*と*Views\Home\AllTags.Mobile.cshtml.hide*に変更します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="2b8f9-238">ファイルに*は拡張子が*付いていないため、ASP.NET MVC ランタイムで*alltags*ビューを表示するために使用されることはありません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="2b8f9-239">次の手順に従って、 *jQuery. Mobile. MVC* NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="2b8f9-240">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-240">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="2b8f9-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="2b8f9-242">**パッケージマネージャーコンソール**で、「」と入力し `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span><span class="sxs-lookup"><span data-stu-id="2b8f9-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="2b8f9-243">次の図は、NuGet jQuery. Mobile. MVC パッケージによって追加され、MvcMobile プロジェクトに変更されたファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="2b8f9-244">追加されるファイルには、ファイル名の後に [add] が追加されています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="2b8f9-245">この画像では、*コンテンツ \ イメージ*フォルダーに追加された GIF ファイルと PNG ファイルは表示されません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="2b8f9-246">JQuery の NuGet パッケージでは、次のものがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="2b8f9-247">*アプリ\_Start\BundleMobileConfig.cs*ファイル。これは、追加された jQuery JAVASCRIPT と CSS ファイルを参照するために必要です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="2b8f9-248">次の手順に従って、このファイルで定義されているモバイルバンドルを参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="2b8f9-249">jQuery Mobile CSS ファイル。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="2b8f9-250">`ViewSwitcher` コントローラーウィジェット (コントローラー \*ビュー\*)。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="2b8f9-251">jQuery Mobile JavaScript ファイル。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="2b8f9-252">JQuery モバイルスタイルのレイアウトファイル (*Views\Shared\\_Layout*)。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="2b8f9-253">ビュースイッチャー部分ビュー *(MvcMobile\Views\Shared\\_ViewSwitcher*)。デスクトップビューからモバイルビューに切り替えるためのリンクが各ページの上部に表示されます。逆の場合も同様です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="2b8f9-254"><em>Content¥ images</em>フォルダー内のいくつかの<em>.png</em>および<em>.gif</em>画像ファイル。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-254">Several<em>.png</em> and <em>.gif</em> image files in the <em>Content\images</em> folder.</span></span>

<span data-ttu-id="2b8f9-255">*Global.asax*ファイルを開き、`Application_Start` メソッドの最後の行として次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="2b8f9-256">次のコードは、完全な*global.asax*ファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="2b8f9-257">Internet Explorer 9 を使用していて、上に黄色の強調表示されている `BundleMobileConfig` が表示されていない場合は、IE の [![互換表示] ボタン (オフ) の](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[互換表示] ボタンの画像 (オフ)")[[互換](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)表示] ボタンの画像をクリックして、[互換表示![] ボタン (オフ) のアウトライン画像](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[互換表示] ボタンの画像 (オフ)")から [互換![表示] ボタン (オン) の](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "[互換表示] ボタンの画像 (オン)")純色の画像に</span><span class="sxs-lookup"><span data-stu-id="2b8f9-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="2b8f9-258">または、このチュートリアルを FireFox または Chrome で表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>

<span data-ttu-id="2b8f9-259">*MvcMobile\Views\Shared\\_Layout*を開き、`Html.Partial` の呼び出しの直後に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="2b8f9-260">完全な*MvcMobile\Views\Shared\\_Layout*を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="2b8f9-261">アプリケーションをビルドし、モバイルブラウザーエミュレーターで*Alltags*ビューを参照します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="2b8f9-262">次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-262">You see the following:</span></span>

<span data-ttu-id="2b8f9-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="2b8f9-264">モバイル固有のコードをデバッグするには、IE または Chrome の[ユーザーエージェント文字列](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)を iPhone に設定してから、F-12 開発者ツールを使用します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="2b8f9-265">モバイルブラウザーに **[ホーム]** 、 **[スピーカー]** 、 **[タグ]** 、 **[日付]** の各リンクがボタンとして表示されない場合、jQuery モバイルスクリプトと CSS ファイルへの参照が正しくない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>

<span data-ttu-id="2b8f9-266">スタイルの変更に加えて、 **[モバイルビュー]** と、モバイルビューからデスクトップビューに切り替えるためのリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="2b8f9-267">**[デスクトップビュー]** リンクをクリックすると、デスクトップビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="2b8f9-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="2b8f9-269">デスクトップビューには、モバイルビューに直接移動する方法は用意されていません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="2b8f9-270">これを修正します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-270">You'll fix that now.</span></span> <span data-ttu-id="2b8f9-271">*Views\Shared\\_Layout*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="2b8f9-272">Page `body` 要素のすぐ下に、ビュースイッチャーウィジェットをレンダリングする次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="2b8f9-273">モバイルブラウザーで*Alltags*ビューを更新します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="2b8f9-274">デスクトップビューとモバイルビュー間を移動できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="2b8f9-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="2b8f9-276">デバッグメモ: Views\Shared\\_ViewSwitcher の末尾に次のコードを追加すると、ユーザーエージェント文字列がモバイルデバイスに設定されているブラウザーを使用しているときに、ビューのデバッグに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> <span data-ttu-id="2b8f9-277">次の見出しを*Views\Shared\\_Layout*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

<span data-ttu-id="2b8f9-278">デスクトップブラウザーで*Alltags*ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="2b8f9-279">ビュースイッチャーウィジェットは、モバイルレイアウトページにのみ追加されるため、デスクトップブラウザーには表示されません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="2b8f9-280">このチュートリアルの後半では、ビュースイッチャーウィジェットをデスクトップビューに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="2b8f9-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="2b8f9-282">スピーカーリストを改善する</span><span class="sxs-lookup"><span data-stu-id="2b8f9-282">Improving the Speakers List</span></span>

<span data-ttu-id="2b8f9-283">モバイル ブラウザーで **[Speakers]** リンクをタップします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="2b8f9-284">モバイルビュー (*Allspeakers. cshtml*) がないため、既定のスピーカー表示 (*allspeakers. cshtml*) は、モバイルレイアウトビュー ( *\_layout*) を使用してレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="2b8f9-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="2b8f9-286">既定の (非モバイル) ビューをグローバルに無効にするには、次のように、`RequireConsistentDisplayMode` を設定して、 *_ViewStart ファイル\\ビュー*で `true` に設定します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="2b8f9-287">`RequireConsistentDisplayMode` が `true`に設定されている場合、モバイルレイアウト (<em>\_layout</em>) はモバイルビューにのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (<em>\_Layout.Mobile.cshtml</em>) is used only for mobile views.</span></span> <span data-ttu-id="2b8f9-288">(つまり、ビューファイルの形式は<em>\* \* ViewName</em><em>です。Mobile.</em>) モバイルレイアウトが非モバイルビューでうまく機能しない場合は、`RequireConsistentDisplayMode` を `true` に設定します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-288">(That is, the view file is of the form <em>\*\*ViewName</em><em>.Mobile.cshtml</em>.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="2b8f9-289">次のスクリーンショットは `RequireConsistentDisplayMode` が `true`に設定されている場合に、<em>スピーカー</em>ページがどのようにレンダリングされるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-289">The screenshot below shows how the <em>Speakers</em> page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="2b8f9-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="2b8f9-291">ビューファイルで `false` に `RequireConsistentDisplayMode` を設定すると、ビューの一貫した表示モードを無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="2b8f9-292">*Views\Home\AllSpeakers.cshtml*ファイル内の次のマークアップは、`RequireConsistentDisplayMode` を `false`に設定します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="2b8f9-293">モバイルスピーカービューの作成</span><span class="sxs-lookup"><span data-stu-id="2b8f9-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="2b8f9-294">いま見たように、 *Speakers* ビューは読み取れますが、リンクが小さく、モバイル デバイスではタップが困難です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="2b8f9-295">このセクションでは、最新のモバイルアプリケーションのようなモバイル固有の*スピーカー*ビューを作成します。これには、大規模でタップしやすいリンクが表示され、スピーカーをすばやく見つけるための検索ボックスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="2b8f9-296">*Allspeakers. cshtml*を*Allspeakers. Mobile. cshtml*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="2b8f9-297">*Allspeakers の cshtml*ファイルを開き、`<h2>` の見出し要素を削除します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="2b8f9-298">`<ul>` タグに `data-role` 属性を追加し、その値を `listview`に設定します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="2b8f9-299">他の[`data-*` 属性](http://html5doctor.com/html5-custom-data-attributes/)と同様に、`data-role="listview"` は大きなリストアイテムをタップしやすくなります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="2b8f9-300">完成したマークアップは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="2b8f9-301">モバイル ブラウザーの表示を更新します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-301">Refresh the mobile browser.</span></span> <span data-ttu-id="2b8f9-302">更新されたビューは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-302">The updated view looks like this:</span></span>

<span data-ttu-id="2b8f9-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="2b8f9-304">モバイルビューは改善されていますが、スピーカーの長い一覧を移動するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="2b8f9-305">この問題を解決するには、`<ul>` タグで `data-filter` 属性を追加し、`true`に設定します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="2b8f9-306">次のコードは、`ul` マークアップを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="2b8f9-307">次の図は、`data-filter` 属性によって生成されるページの上部にある検索フィルターボックスを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="2b8f9-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="2b8f9-309">検索ボックスに各文字を入力すると、次の図に示すように、jQuery Mobile によって表示される一覧がフィルター処理されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="2b8f9-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="2b8f9-311">タグリストの改良</span><span class="sxs-lookup"><span data-stu-id="2b8f9-311">Improving the Tags List</span></span>

<span data-ttu-id="2b8f9-312">既定の*スピーカー*ビューと同様に、[*タグ*] ビューは読み取り可能ですが、リンクは小さく、モバイルデバイスではタップが困難です。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="2b8f9-313">このセクションでは、[*スピーカー* ] ビューを固定するのと同じ方法で*タグ*ビューを修正します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="2b8f9-314">名前が*Views\Home\AllTags.Mobile.cshtml*になるように、 *Views\Home\AllTags.Mobile.cshtml.hide*ファイルの&quot; サフィックス &quot;を削除します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-314">Remove the &quot;hide&quot; suffix to the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="2b8f9-315">名前を変更したファイルを開き、`<h2>` 要素を削除します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="2b8f9-316">次に示すように、`data-role` 属性と `data-filter` 属性を `<ul>` タグに追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="2b8f9-317">次の画像は、`J`文字にフィルターを適用するタグページを示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="2b8f9-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="2b8f9-319">日付の一覧の改善</span><span class="sxs-lookup"><span data-stu-id="2b8f9-319">Improving the Dates List</span></span>

<span data-ttu-id="2b8f9-320">[*日付*] ビューは、モバイルデバイスで使用しやすくするために、*スピーカー*や*タグ*の表示を改善した場合と同様に改善できます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="2b8f9-321">*Views\Home\AllDates.cshtml*ファイルを*Views\Home\AllDates.Mobile.cshtml*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="2b8f9-322">新しいファイルを開き、`<h2>` 要素を削除します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="2b8f9-323">次のように、`data-role="listview"` を `<ul>` タグに追加します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="2b8f9-324">次の図は、`data-role` の属性が設定された**日付**ページの外観を示しています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="2b8f9-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)*Views\Home\AllDates.Mobile.cshtml*ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="2b8f9-326">このコードは、すべてのセッションを日単位でグループ化します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-326">This code groups all sessions by days.</span></span> <span data-ttu-id="2b8f9-327">これにより、新しい日ごとにリストの区分線が作成され、各日のすべてのセッションが区分線の下に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="2b8f9-328">このコードを実行すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="2b8f9-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="2b8f9-330">SessionsTable ビューの向上</span><span class="sxs-lookup"><span data-stu-id="2b8f9-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="2b8f9-331">このセクションでは、セッションのモバイル固有のビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="2b8f9-332">ここで行った変更は、作成した他のビューよりも広くなります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="2b8f9-333">モバイルブラウザーで、 **[スピーカー]** ボタンをタップし、[検索] ボックスに「`Sc`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="2b8f9-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="2b8f9-335">**Scott マン Selman**リンクをタップします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="2b8f9-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="2b8f9-337">ご覧のように、モバイルブラウザーで表示するのは簡単ではありません。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="2b8f9-338">日付列が読みにくく、タグ列がビューから外れています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="2b8f9-339">この問題を解決するには、 *Views\Home\SessionsTable.cshtml*を*Views\Home\SessionsTable.Mobile.cshtml*にコピーし、ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="2b8f9-340">このコードでは、ルームとタグ列を削除し、タイトル、スピーカー、および日付を縦に書式設定して、すべての情報がモバイルブラウザーで読み取れるようにします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="2b8f9-341">次の図にはコードの変更が反映されています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="2b8f9-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="2b8f9-343">SessionByCode ビューの向上</span><span class="sxs-lookup"><span data-stu-id="2b8f9-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="2b8f9-344">最後に、 *Sessionbycode*ビューのモバイル専用ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="2b8f9-345">モバイルブラウザーで、 **[スピーカー]** ボタンをタップし、[検索] ボックスに「`Sc`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="2b8f9-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="2b8f9-347">**Scott マン Selman**リンクをタップします。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="2b8f9-348">Scott マン Selman のセッションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="2b8f9-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="2b8f9-350">**MS Web スタック**の [お気に入り] リンクの概要を選択します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="2b8f9-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="2b8f9-352">既定のデスクトップビューは問題ありませんが、改善することができます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="2b8f9-353">*Views\Home\SessionByCode.cshtml*を*Views\Home\SessionByCode.Mobile.cshtml*にコピーし、 *Views\Home\SessionByCode.Mobile.cshtml*ファイルの内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="2b8f9-354">新しいマークアップでは、`data-role` 属性を使用して、ビューのレイアウトを改善します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="2b8f9-355">モバイル ブラウザーの表示を更新します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-355">Refresh the mobile browser.</span></span> <span data-ttu-id="2b8f9-356">次の図には行ったコードの変更が反映されています。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="2b8f9-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="2b8f9-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="2b8f9-358">Wrapup とレビュー</span><span class="sxs-lookup"><span data-stu-id="2b8f9-358">Wrapup and Review</span></span>

<span data-ttu-id="2b8f9-359">このチュートリアルでは、ASP.NET MVC 4 Developer Preview の新しいモバイル機能を紹介しました。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="2b8f9-360">モバイル機能には次のものがあります。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-360">The mobile features include:</span></span>

- <span data-ttu-id="2b8f9-361">レイアウト、ビュー、部分ビューをグローバルと個々のビューの両方でオーバーライドする機能。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="2b8f9-362">`RequireConsistentDisplayMode` プロパティを使用してレイアウトと部分オーバーライドの適用を制御します。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="2b8f9-363">モバイルビューのビュー切り替えウィジェットは、デスクトップビューに表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="2b8f9-364">IPhone ブラウザーなど、特定のブラウザーをサポートするためのサポート。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b8f9-365">参照</span><span class="sxs-lookup"><span data-stu-id="2b8f9-365">See Also</span></span>

- <span data-ttu-id="2b8f9-366">[JQuery モバイル](http://jquerymobile.com)サイト。</span><span class="sxs-lookup"><span data-stu-id="2b8f9-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="2b8f9-367">jQuery Mobile の概要</span><span class="sxs-lookup"><span data-stu-id="2b8f9-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="2b8f9-368">W3C 勧告: モバイル Web アプリケーションのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="2b8f9-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="2b8f9-369">W3C のメディア クエリに関する勧告候補</span><span class="sxs-lookup"><span data-stu-id="2b8f9-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
