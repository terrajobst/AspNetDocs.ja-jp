---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: ASP.NET Web ページ (Razor) サイトでマップを表示する |Microsoft Docs
author: Rick-Anderson
description: この記事では、Bing、Google、Ma... によって提供されるマッピングサービスに基づいて、ASP.NET Web ページ (Razor) web サイトのページに対話型マップを表示する方法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518722"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="ad57f-103">ASP.NET Web ページ (Razor) サイトでマップを表示する</span><span class="sxs-lookup"><span data-stu-id="ad57f-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="ad57f-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ad57f-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ad57f-105">この記事では、Bing、Google、MapQuest、および Yahoo が提供するマッピングサービスに基づいて、ASP.NET Web ページ (Razor) web サイトのページに対話型マップを表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="ad57f-106">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="ad57f-107">アドレスに基づいてマップを生成する方法。</span><span class="sxs-lookup"><span data-stu-id="ad57f-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="ad57f-108">緯度と経度の座標に基づいてマップを生成する方法。</span><span class="sxs-lookup"><span data-stu-id="ad57f-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="ad57f-109">Bing maps 開発者アカウントを登録し、Bing Maps で使用するキーを取得する方法。</span><span class="sxs-lookup"><span data-stu-id="ad57f-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="ad57f-110">この記事で導入された ASP.NET 機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ad57f-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="ad57f-111">`Maps` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="ad57f-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ad57f-112">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="ad57f-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ad57f-113">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="ad57f-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="ad57f-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="ad57f-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="ad57f-115">このチュートリアルでは、WebMatrix 3 も使用できます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="ad57f-116">Web ページでは、`Maps` ヘルパーを使用してページにマップを表示できます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="ad57f-117">マップは、アドレスに基づいて生成することも、経度と緯度の座標のセットに基づいて生成することもできます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="ad57f-118">`Maps` クラスを使用すると、Bing、Google、MapQuest、Yahoo などの一般的なマップエンジンを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="ad57f-119">ページにマッピングを追加する手順は、どのマップエンジンを呼び出すかに関係なく同じです。</span><span class="sxs-lookup"><span data-stu-id="ad57f-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="ad57f-120">ここでは、使用可能なメソッドを作成してマップを表示する JavaScript ファイル参照を追加し、`Maps` ヘルパーのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="ad57f-121">使用する `Maps` ヘルパーメソッドに基づいてマップサービスを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="ad57f-122">次のいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="ad57f-123">必要なコンポーネントをインストールする</span><span class="sxs-lookup"><span data-stu-id="ad57f-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="ad57f-124">マップを表示するには、次の要素が必要です。</span><span class="sxs-lookup"><span data-stu-id="ad57f-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="ad57f-125">`Maps` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="ad57f-125">The `Maps` helper.</span></span> <span data-ttu-id="ad57f-126">このヘルパーは、ASP.NET Web ヘルパーライブラリのバージョン2に含まれています。</span><span class="sxs-lookup"><span data-stu-id="ad57f-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="ad57f-127">まだライブラリを追加していない場合は、NuGet パッケージとしてサイトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="ad57f-128">詳細については、「 [ASP.NET Web ページサイトへのヘルパーのインストール](https://go.microsoft.com/fwlink/?LinkId=252372)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad57f-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="ad57f-129">(ギャラリーで、`microsoft-web-helpers` パッケージを検索します)。</span><span class="sxs-lookup"><span data-stu-id="ad57f-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="ad57f-130">JQuery ライブラリ。</span><span class="sxs-lookup"><span data-stu-id="ad57f-130">The jQuery library.</span></span> <span data-ttu-id="ad57f-131">いくつかの WebMatrix サイトテンプレートには既に、jQuery ライブラリが*スクリプト*フォルダーに含まれています。</span><span class="sxs-lookup"><span data-stu-id="ad57f-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="ad57f-132">これらのライブラリがない場合は、 [jQuery.org](http://jQuery.org)サイトから直接、最新の jQuery ライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="ad57f-133">または、テンプレート (**スターターサイト**テンプレートなど) を使用して新しいサイトを作成し、そのサイトから現在のサイトに jQuery ファイルをコピーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="ad57f-134">最後に、Bing maps を使用する場合は、最初に (無料) アカウントを作成し、キーを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad57f-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="ad57f-135">キーを取得するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="ad57f-136">[Bing Maps 開発者アカウント](https://www.microsoft.com/maps/developers/web.aspx)でアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="ad57f-137">Microsoft アカウント (Windows Live ID) も必要です。</span><span class="sxs-lookup"><span data-stu-id="ad57f-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="ad57f-138">**評価/テスト**にキーを使用するように指定できます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="ad57f-139">WebMatrix と IIS Express を使用して自分のコンピューターでマッピング関数をテストする場合は、**サイト**のワークスペースにアクセスし、サイトの URL をメモします (`http://localhost:50408`たとえば、ポート番号は異なる場合があります)。</span><span class="sxs-lookup"><span data-stu-id="ad57f-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="ad57f-140">この*localhost*アドレスは、登録時にサイトとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="ad57f-141">アカウントの登録が完了したら、Bing Maps アカウントセンターにアクセスし、 **[キーの作成または表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ad57f-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![マッピング-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="ad57f-143">Bing が作成するキーを記録します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="ad57f-144">アドレスに基づくマップの作成 (Google を使用)</span><span class="sxs-lookup"><span data-stu-id="ad57f-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="ad57f-145">次の例では、住所に基づいてマップを表示するページを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="ad57f-146">この例では、Google Maps の使用方法を示します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="ad57f-147">サイトのルートに*Mapaddress. cshtml*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="ad57f-148">このページでは、渡されたアドレスに基づいてマップが生成されます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="ad57f-149">次のコードをファイルにコピーして、既存のコンテンツを上書きします。</span><span class="sxs-lookup"><span data-stu-id="ad57f-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="ad57f-150">このページの次の機能に注意してください。</span><span class="sxs-lookup"><span data-stu-id="ad57f-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="ad57f-151">`<head>` 要素内の `<script>` 要素。</span><span class="sxs-lookup"><span data-stu-id="ad57f-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="ad57f-152">この例では、`<script>` 要素は*jquery-1.6.4*ファイルを参照します。これは、jquery ライブラリバージョン1.6.4 の縮小版 (圧縮された) バージョンです。</span><span class="sxs-lookup"><span data-stu-id="ad57f-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="ad57f-153">参照では、 *.js*ファイルがサイトの*Scripts*フォルダーにあることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="ad57f-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="ad57f-154">別のバージョンの jQuery ライブラリを使用している場合は、そのバージョンが正しく参照されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="ad57f-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="ad57f-155">ページの本文内の `@Maps.GetGoogleHtml` への呼び出し。</span><span class="sxs-lookup"><span data-stu-id="ad57f-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="ad57f-156">アドレスをマップするには、アドレス文字列を渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad57f-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="ad57f-157">他のマップエンジンのメソッドは、同様の方法 (`@Maps.GetYahooHtml`、`@Maps.GetMapQuestHtml`) で動作します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="ad57f-158">ページを実行し、アドレスを入力します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-158">Run the page and enter an address.</span></span> <span data-ttu-id="ad57f-159">ページには、指定した場所を示す、Google Maps に基づくマップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![マッピング-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="ad57f-161">緯度と経度の座標に基づくマップの作成 (Bing を使用)</span><span class="sxs-lookup"><span data-stu-id="ad57f-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="ad57f-162">この例では、座標に基づいてマップを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="ad57f-163">この例では、Bing maps の使用方法と、Bing キーを含める方法を示します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="ad57f-164">(Bing キーを使用せずに、他のマップエンジンを使用して座標に基づいてマップを作成することもできます)。</span><span class="sxs-lookup"><span data-stu-id="ad57f-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="ad57f-165">サイトのルートに*Mapcoordinates*という名前のファイルを作成し、既存の内容を次のコードとマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="ad57f-166">`your-key-here` を、前に生成した Bing Maps キーに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="ad57f-167">Mapcoordinates の [] ページを実行し、緯度と経度の座標を入力して、**マップ**をクリックし*ます。*</span><span class="sxs-lookup"><span data-stu-id="ad57f-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="ad57f-168">ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad57f-168">button.</span></span> <span data-ttu-id="ad57f-169">(座標がわからない場合は、次の操作を試してください。</span><span class="sxs-lookup"><span data-stu-id="ad57f-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="ad57f-170">これは、Microsoft Redmond キャンパス上の場所です)。</span><span class="sxs-lookup"><span data-stu-id="ad57f-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="ad57f-171">緯度: 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="ad57f-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="ad57f-172">経度:-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="ad57f-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="ad57f-173">指定した座標を使用してページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad57f-173">The page is displayed using the coordinates that you specified.</span></span>

     ![マッピング-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ad57f-175">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="ad57f-175">Additional Resources</span></span>

[<span data-ttu-id="ad57f-176">Microsoft Maps API リファレンス</span><span class="sxs-lookup"><span data-stu-id="ad57f-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
