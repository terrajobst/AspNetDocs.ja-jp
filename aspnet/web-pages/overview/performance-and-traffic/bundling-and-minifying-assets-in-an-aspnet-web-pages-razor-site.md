---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: バンドルと縮小の資産を ASP.NET web ページ (Razor) サイト |Microsoft Docs
author: microsoft
description: バンドルと縮小には、サイトを速く方法です。 バンドルで結合する複数の JavaScript (.js) ファイルまたは複数のスタイル シート (.
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400452"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3a519-104">ASP.NET Web ページ (Razor) サイトでアセットをバンドルし、小さくする</span><span class="sxs-lookup"><span data-stu-id="3a519-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="3a519-105">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3a519-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3a519-106">バンドルと縮小には、サイトを速く方法です。</span><span class="sxs-lookup"><span data-stu-id="3a519-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="3a519-107">複数の JavaScript を結合することができますのバンドル (*.js*) ファイルまたは複数のカスケード スタイル シート (*.css*) それらを一度に 1 つずつではなく、単位としてダウンロードできるようにします。</span><span class="sxs-lookup"><span data-stu-id="3a519-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="3a519-108">縮小では、空白を絞り出すし、他の種類のことがある小規模としてダウンロードしたファイルを作成するために圧縮を実行します。</span><span class="sxs-lookup"><span data-stu-id="3a519-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="3a519-109">ASP.NET Web Pages 2 の RC リリースはサポートしていませんバンドルと縮小に必要な要素を含むパッケージがまだ Microsoft WebMatrix では使用できないためです。</span><span class="sxs-lookup"><span data-stu-id="3a519-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="3a519-110">この不便をおかけして申し訳ありません。</span><span class="sxs-lookup"><span data-stu-id="3a519-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="3a519-111">パッケージは、ASP.NET Web ページ 2 と WebMatrix 2 の最終リリースで使用できることが必要です。</span><span class="sxs-lookup"><span data-stu-id="3a519-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
