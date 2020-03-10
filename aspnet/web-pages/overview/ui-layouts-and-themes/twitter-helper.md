---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET Web ページ | を含む Twitter ヘルパーMicrosoft Docs
author: Rick-Anderson
description: このトピックとアプリケーションでは、Twitter ヘルパーを WebMatrix 3 プロジェクトに追加する方法について説明します。 これには Twitter ヘルパーコードが含まれており、ヘルパーを呼び出す方法を示しています...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518620"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="2ae73-104">Twitter ヘルパーと ASP.NET Web ページ</span><span class="sxs-lookup"><span data-stu-id="2ae73-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="2ae73-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2ae73-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ae73-106">Twitter ヘルパーは互換性のために残されています。</span><span class="sxs-lookup"><span data-stu-id="2ae73-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="2ae73-107">Twitter の web サイト用エンゲージメントツールについては、「 [Web サイトの twitter の概要](https://developer.twitter.com/en/docs/twitter-for-websites/overview)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2ae73-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="2ae73-108">このトピックとアプリケーションでは、Twitter ヘルパーを WebMatrix 3 プロジェクトに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="2ae73-109">これには Twitter ヘルパーコードが含まれており、ヘルパーメソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2ae73-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="2ae73-110">Twitter ファイル用のこのコード**は、Microsoft によって開発**されました。</span><span class="sxs-lookup"><span data-stu-id="2ae73-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2ae73-111">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="2ae73-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="2ae73-112">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="2ae73-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="2ae73-113">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="2ae73-114">はじめに</span><span class="sxs-lookup"><span data-stu-id="2ae73-114">Introduction</span></span>

<span data-ttu-id="2ae73-115">このトピックでは、アプリケーションに Twitter ヘルパーを追加し、Razor 構文を使用してヘルパーメソッドを呼び出す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="2ae73-116">Twitter ヘルパーを使用すると、Twitter のボタンやウィジェットをアプリケーションに簡単に組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="2ae73-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="2ae73-117">ユーザーのタイムラインやハッシュタグの検索結果など、Twitter ウィジェットを使用するには、最初[に twitter でウィジェット](https://twitter.com/settings/widgets)を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ae73-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="2ae73-118">ウィジェットを作成すると、ウィジェット id が表示されます。ウィジェットを表示するヘルパーメソッドを呼び出すときに、このウィジェット id をパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="2ae73-119">このトピックは、バージョン1.1 の Twitter API 向けに作成されました。</span><span class="sxs-lookup"><span data-stu-id="2ae73-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="2ae73-120">Twitter のヘルパーコードをプロジェクトに直接追加することで、Twitter API が変更された場合にヘルパーコードを更新できます。</span><span class="sxs-lookup"><span data-stu-id="2ae73-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="2ae73-121">WebMatrix のインストールの詳細については、「 [ASP.NET Web ページ2はじめにの概要](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2ae73-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="2ae73-122">Twitter ヘルパーをプロジェクトに追加する</span><span class="sxs-lookup"><span data-stu-id="2ae73-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="2ae73-123">Twitter ヘルパーを追加するには、まず、 **App\_Code**という名前のフォルダーをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="2ae73-124">次に、 **Twitter**という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code フォルダー](twitter-helper/_static/image1.png)

<span data-ttu-id="2ae73-126">Twitter の既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2ae73-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="2ae73-127">Web ページから Twitter メソッドを呼び出す</span><span class="sxs-lookup"><span data-stu-id="2ae73-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="2ae73-128">次の例は、プロジェクトのページから Twitter ヘルパーメソッドを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2ae73-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="2ae73-129">プロジェクトでは、パラメーター値をニーズに関連する値に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ae73-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="2ae73-130">提供されたウィジェット id を使用して、メソッドの動作を調べることができますが、プロジェクト用に独自のウィジェットを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ae73-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="2ae73-131">以下に示すパラメーターのすべてが必要であるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="2ae73-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="2ae73-132">オプションのパラメーターは、ボタンまたはウィジェットの表示方法をカスタマイズするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="2ae73-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="2ae73-133">たとえば、[フォロー] ボタンをクリックする必要があるのはユーザー名のみですが、この例ではフォロワーの数を含める方法と、ボタンのサイズと言語を指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2ae73-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="2ae73-134">結果を確認する</span><span class="sxs-lookup"><span data-stu-id="2ae73-134">See the results</span></span>

<span data-ttu-id="2ae73-135">上記のコードでは、次のボタンとウィジェットが生成されます。</span><span class="sxs-lookup"><span data-stu-id="2ae73-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="2ae73-136">これらのボタンとウィジェットは、スクリーンショットではなく、完全に機能します。</span><span class="sxs-lookup"><span data-stu-id="2ae73-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="2ae73-137">Language パラメーターが**es**に設定されているため、[次へ] ボタンがスペイン語で表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ae73-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="2ae73-138">[フォロー] ボタン</span><span class="sxs-lookup"><span data-stu-id="2ae73-138">Follow Button</span></span>

<span data-ttu-id="2ae73-139">[@aspnetに従う)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="2ae73-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="2ae73-140">ツイートボタン</span><span class="sxs-lookup"><span data-stu-id="2ae73-140">Tweet Button</span></span>

<span data-ttu-id="2ae73-141">[ツイート](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="2ae73-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="2ae73-142">ユーザーのタイムライン (プロファイル)</span><span class="sxs-lookup"><span data-stu-id="2ae73-142">User Timeline (Profile)</span></span>

<span data-ttu-id="2ae73-143">[ツイート by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="2ae73-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="2ae73-144">お気に入り</span><span class="sxs-lookup"><span data-stu-id="2ae73-144">Favorites</span></span>

<span data-ttu-id="2ae73-145">[お気に入りのツイート by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="2ae73-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="2ae73-146">List</span><span class="sxs-lookup"><span data-stu-id="2ae73-146">List</span></span>

<span data-ttu-id="2ae73-147">[@Microsoft/MS\_コンシューマー\_バンドからのツイート](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="2ae73-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="2ae73-148">検索</span><span class="sxs-lookup"><span data-stu-id="2ae73-148">Search</span></span>

<span data-ttu-id="2ae73-149">[.Net&quot;#asp &quot;に関するツイート](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="2ae73-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
