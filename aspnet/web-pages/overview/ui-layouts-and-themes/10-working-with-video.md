---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: ASP.NET Web ページ (Razor) サイトでビデオを表示する |Microsoft Docs
author: Rick-Anderson
description: この章では、Razor 構文ページを使用して ASP.NET Web ページにビデオを表示する方法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510382"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c5aec-103">ASP.NET Web ページ (Razor) サイトでビデオを表示する</span><span class="sxs-lookup"><span data-stu-id="c5aec-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c5aec-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c5aec-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c5aec-105">この記事では、ASP.NET Web ページ (Razor) web サイトでビデオ (メディア) プレーヤーを使用して、サイトに保存されているビデオをユーザーが表示できるようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="c5aec-106">ASP.NET Web ページ Razor 構文では、Flash (*swf*)、Media Player ( *.wmv*)、および Silverlight ( *.xap*) のビデオを再生できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="c5aec-107">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c5aec-108">ビデオプレーヤーを選択する方法。</span><span class="sxs-lookup"><span data-stu-id="c5aec-108">How to choose a video player.</span></span>
> - <span data-ttu-id="c5aec-109">Web ページにビデオを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="c5aec-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="c5aec-110">ビデオプレーヤーの属性を設定する方法。</span><span class="sxs-lookup"><span data-stu-id="c5aec-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="c5aec-111">この記事で紹介する ASP.NET Razor ページ機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="c5aec-112">`Video` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="c5aec-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c5aec-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="c5aec-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c5aec-114">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="c5aec-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="c5aec-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="c5aec-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="c5aec-116">このチュートリアルでは、WebMatrix 3 も使用できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="c5aec-117">はじめに</span><span class="sxs-lookup"><span data-stu-id="c5aec-117">Introduction</span></span>

<span data-ttu-id="c5aec-118">サイトにビデオを表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-118">You might want to display a video on your site.</span></span> <span data-ttu-id="c5aec-119">これを行う1つの方法は、既にビデオがあるサイト (YouTube など) にリンクすることです。</span><span class="sxs-lookup"><span data-stu-id="c5aec-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="c5aec-120">これらのサイトからのビデオを自分のページに直接埋め込む場合は、通常、サイトから HTML マークアップを取得して、ページにコピーすることができます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="c5aec-121">たとえば、次の例は YouTube ビデオを埋め込む方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="c5aec-122">自分の web サイトにあるビデオを (公共のビデオ共有サイトではなく) 再生する場合、このような埋め込みマークアップを使用して直接リンクすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c5aec-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="c5aec-123">ただし、`Video` ヘルパーを使用してサイトからビデオを再生できます。このヘルパーは、メディアプレーヤーをページに直接レンダリングします。</span><span class="sxs-lookup"><span data-stu-id="c5aec-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="c5aec-124">ビデオプレーヤーの選択</span><span class="sxs-lookup"><span data-stu-id="c5aec-124">Choosing a Video Player</span></span>

<span data-ttu-id="c5aec-125">ビデオファイルには多くの形式があり、各形式には通常、別のプレーヤーが必要で、プレーヤーを構成する別の方法が必要です。</span><span class="sxs-lookup"><span data-stu-id="c5aec-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="c5aec-126">ASP.NET Razor ページでは、`Video` ヘルパーを使用して web ページでビデオを再生できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="c5aec-127">`Video` ヘルパーは、ビデオを web ページに埋め込むプロセスを簡略化します。これは、ビデオをページに追加するために通常使用される `object` と `embed` HTML 要素を自動的に生成するためです。</span><span class="sxs-lookup"><span data-stu-id="c5aec-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="c5aec-128">`Video` helper では、次のメディアプレーヤーがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="c5aec-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="c5aec-129">Adobe Flash</span></span>
- <span data-ttu-id="c5aec-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="c5aec-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="c5aec-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="c5aec-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="c5aec-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="c5aec-132">The Flash Player</span></span>

<span data-ttu-id="c5aec-133">`Video` ヘルパーの `Flash` プレーヤーを使用すると、web ページで Flash ビデオ (*swf*ファイル) を再生できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="c5aec-134">少なくとも、ビデオファイルへのパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="c5aec-135">パスだけを指定した場合、player は現在のバージョンの Flash で設定されている既定値を使用します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="c5aec-136">一般的な既定の設定は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c5aec-136">Typical default settings are:</span></span>

- <span data-ttu-id="c5aec-137">ビデオは、既定の幅と高さを使用して、背景色なしで表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="c5aec-138">ビデオは、ページが読み込まれるときに自動的に再生されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="c5aec-139">ビデオは、明示的に停止されるまで継続的にループされます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="c5aec-140">ビデオは、特定のサイズに合わせてビデオをトリミングするのではなく、すべてのビデオを表示するようにスケーリングされています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="c5aec-141">ビデオがウィンドウで再生されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="c5aec-142">MediaPlayer プレーヤー</span><span class="sxs-lookup"><span data-stu-id="c5aec-142">The MediaPlayer Player</span></span>

<span data-ttu-id="c5aec-143">`Video` ヘルパーの `MediaPlayer` プレーヤーを使用すると、web ページで Windows Media ビデオ ( *.wmv*ファイル)、windows media audio ( *.wma*ファイル)、および mp3 ( *.mp3*ファイル) を再生できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="c5aec-144">再生するメディアファイルのパスを含める必要があります。その他のパラメーターはすべて省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c5aec-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="c5aec-145">パスのみを指定した場合、windows media player では、次のように、現在のバージョンの MediaPlayer によって設定された既定の設定が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="c5aec-146">ビデオは、既定の幅と高さを使用して表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="c5aec-147">ビデオは、ページが読み込まれるときに自動的に再生されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="c5aec-148">ビデオは1回再生されます (ループしません)。</span><span class="sxs-lookup"><span data-stu-id="c5aec-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="c5aec-149">プレーヤーには、ユーザーインターフェイスのすべてのコントロールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="c5aec-150">ビデオがウィンドウで再生されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="c5aec-151">Silverlight プレーヤー</span><span class="sxs-lookup"><span data-stu-id="c5aec-151">The Silverlight Player</span></span>

<span data-ttu-id="c5aec-152">`Video` ヘルパーの `Silverlight` プレーヤーを使用すると、Windows Media ビデオ ( *.wmv*ファイル)、Windows media Audio ( *.wma*ファイル)、mp3 ( *.mp3*ファイル) を再生できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="c5aec-153">Silverlight ベースのアプリケーションパッケージ ( *.xap*ファイル) を指すように path パラメーターを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="c5aec-154">また、幅と高さのパラメーターも設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="c5aec-155">その他のパラメーターはすべて省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c5aec-155">All other parameters are optional.</span></span> <span data-ttu-id="c5aec-156">Silverlight プレーヤーをビデオに使用する場合、必要なパラメーターのみを設定すると、Silverlight プレーヤーは背景色なしでビデオを表示します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="c5aec-157">Silverlight をまだ理解していない場合、 *.xap*ファイルは圧縮されたファイルで*あり、.xaml*ファイル、アセンブリ内のマネージコード、およびオプションのリソースのレイアウト命令が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="c5aec-158">Silverlight アプリケーションプロジェクトとして、Visual Studio で *.xap*ファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="c5aec-159">`Silverlight` video player は、windows media player 用に指定した設定と *.xap*ファイルで提供されている設定の両方を使用します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="c5aec-160">MIME の種類</span><span class="sxs-lookup"><span data-stu-id="c5aec-160">MIME Types</span></span>
> 
> <span data-ttu-id="c5aec-161">ブラウザーがファイルをダウンロードすると、ファイルの種類が、表示されるドキュメントに指定されている MIME の種類と一致することが確認されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="c5aec-162">MIME の種類は、ファイルのコンテンツの種類またはメディアの種類です。</span><span class="sxs-lookup"><span data-stu-id="c5aec-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="c5aec-163">`Video` helper は、次の MIME の種類を使用します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="c5aec-164">Flash (swf) ビデオの再生</span><span class="sxs-lookup"><span data-stu-id="c5aec-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="c5aec-165">この手順では、*サンプルの swf*という名前の Flash ビデオを再生する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="c5aec-166">この手順では、サイトに*Media*という名前のフォルダーがあり、そのフォルダーに*swf*ファイルがあることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="c5aec-167">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。</span><span class="sxs-lookup"><span data-stu-id="c5aec-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="c5aec-168">Web サイトで、ページを追加し、 *FlashVideo*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="c5aec-169">次のマークアップをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="c5aec-170">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-170">Run the page in a browser.</span></span> <span data-ttu-id="c5aec-171">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。ページが表示され、ビデオが自動的に再生されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="c5aec-172">![絵](10-working-with-video/_static/image1.jpg "ch08_video-1")</span><span class="sxs-lookup"><span data-stu-id="c5aec-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="c5aec-173">Flash ビデオの `quality` パラメーターは、`low`、`autolow`、`autohigh`、`medium`、`high`、および `best`に設定できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="c5aec-174">`scale` パラメーターを使用して、特定のサイズで再生するように Flash ビデオを変更することができます。これは、次のように設定できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="c5aec-175">[https://login.microsoftonline.com/consumers/](`showall`)</span><span class="sxs-lookup"><span data-stu-id="c5aec-175">`showall`.</span></span> <span data-ttu-id="c5aec-176">これにより、元の縦横比を維持しながらビデオ全体が表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="c5aec-177">ただし、右端に境界線が表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="c5aec-178">[https://login.microsoftonline.com/consumers/](`noorder`)</span><span class="sxs-lookup"><span data-stu-id="c5aec-178">`noorder`.</span></span> <span data-ttu-id="c5aec-179">これにより、元の縦横比を維持しながらビデオが拡大縮小されますが、トリミングされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="c5aec-180">[https://login.microsoftonline.com/consumers/](`exactfit`)</span><span class="sxs-lookup"><span data-stu-id="c5aec-180">`exactfit`.</span></span> <span data-ttu-id="c5aec-181">これにより、元の縦横比を維持せずにビデオ全体が表示されるようになりますが、歪みが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="c5aec-182">`scale` パラメーターを指定しない場合、ビデオ全体が表示され、元の縦横比はトリミングされることなく維持されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="c5aec-183">次の例では、`scale` パラメーターを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="c5aec-184">Flash player では、`windowMode`という名前のビデオモード設定がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="c5aec-185">これを `window`、`opaque`、および `transparent`に設定できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="c5aec-186">既定では、`windowMode` は `window`に設定されます。これにより、ビデオが web ページ上の別のウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="c5aec-187">`opaque` の設定は、web ページ上のビデオの背後にあるすべてを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="c5aec-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="c5aec-188">`transparent` 設定を使用すると、ビデオの一部が透明であると想定して、web ページの背景をビデオに表示できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="c5aec-189">MediaPlayer ( *.wmv*) ビデオの再生</span><span class="sxs-lookup"><span data-stu-id="c5aec-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="c5aec-190">次の手順は、 *media*フォルダーにある*サンプル .wmv*という名前のウィンドウメディアビデオを再生する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c5aec-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="c5aec-191">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。</span><span class="sxs-lookup"><span data-stu-id="c5aec-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="c5aec-192">*MediaPlayerVideo*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="c5aec-193">次のマークアップをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="c5aec-194">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-194">Run the page in a browser.</span></span> <span data-ttu-id="c5aec-195">ビデオが自動的に読み込まれ、再生されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="c5aec-196">![絵](10-working-with-video/_static/image2.jpg "ch08_video-2")</span><span class="sxs-lookup"><span data-stu-id="c5aec-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="c5aec-197">`playCount` は、ビデオを自動的に再生する回数を示す整数に設定できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="c5aec-198">`uiMode` パラメーターを使用すると、ユーザーインターフェイスに表示されるコントロールを指定できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="c5aec-199">`uiMode` は、`invisible`、`none`、`mini`、または `full`に設定できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="c5aec-200">`uiMode` パラメーターを指定しない場合は、ビデオウィンドウに加えて、ステータスウィンドウ、シークバー、コントロールボタン、およびボリュームコントロールと共にビデオが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="c5aec-201">プレーヤーを使用してオーディオファイルを再生する場合も、これらのコントロールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="c5aec-202">`uiMode` パラメーターを使用する方法の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="c5aec-203">既定では、オーディオはビデオが再生されるときにオンになります。</span><span class="sxs-lookup"><span data-stu-id="c5aec-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="c5aec-204">オーディオをミュートするには、`mute` パラメーターを true に設定します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="c5aec-205">`volume` パラメーターを 0 ~ 100 の値に設定することにより、MediaPlayer ビデオのオーディオレベルを制御できます。</span><span class="sxs-lookup"><span data-stu-id="c5aec-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="c5aec-206">既定値は 50 です。</span><span class="sxs-lookup"><span data-stu-id="c5aec-206">The default value is 50.</span></span> <span data-ttu-id="c5aec-207">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="c5aec-208">Silverlight ビデオの再生</span><span class="sxs-lookup"><span data-stu-id="c5aec-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="c5aec-209">この手順では、 *Media*という名前のフォルダーにある、Silverlight *.xap*ページに含まれているビデオを再生する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="c5aec-210">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。</span><span class="sxs-lookup"><span data-stu-id="c5aec-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="c5aec-211">*SilverlightVideo*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="c5aec-212">次のマークアップをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="c5aec-213">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="c5aec-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="c5aec-214">![絵](10-working-with-video/_static/image3.jpg "ch08_video-3")</span><span class="sxs-lookup"><span data-stu-id="c5aec-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c5aec-215">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="c5aec-215">Additional Resources</span></span>

<span data-ttu-id="c5aec-216">[Silverlight の概要](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="c5aec-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="c5aec-217">Flash オブジェクトと埋め込みタグ属性</span><span class="sxs-lookup"><span data-stu-id="c5aec-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="c5aec-218">[Windows Media Player 11 SDK PARAM タグ](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="c5aec-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
