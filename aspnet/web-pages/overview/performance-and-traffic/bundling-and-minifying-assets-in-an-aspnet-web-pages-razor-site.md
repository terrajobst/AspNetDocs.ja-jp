---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: ASP.NET Web ページ (Razor) サイトでの資産のバンドルと縮小 |Microsoft Docs
author: microsoft
description: バンドルと縮小は、サイトをより迅速に作成する方法です。 バンドルを使用すると、複数の JavaScript (.js) ファイルまたは複数のカスケードスタイルシート (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516178"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a613b-104">ASP.NET Web ページ (Razor) サイトでアセットをバンドルし、小さくする</span><span class="sxs-lookup"><span data-stu-id="a613b-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="a613b-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a613b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a613b-106">バンドルと縮小は、サイトをより迅速に作成する方法です。</span><span class="sxs-lookup"><span data-stu-id="a613b-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="a613b-107">バンドルを使用すると、複数の JavaScript ( *.js*) ファイルまたは複数のカスケードスタイルシート ( *.css*) ファイルを結合して、一度に1つずつではなく、1つの単位としてダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a613b-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="a613b-108">縮小 squeezes は空白を除外し、他の種類の圧縮を実行して、ダウンロードされたファイルを可能な限り小さくします。</span><span class="sxs-lookup"><span data-stu-id="a613b-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="a613b-109">ASP.NET Web ページ2の RC リリースでは、必要な要素を含むパッケージが Microsoft WebMatrix ではまだ使用できないため、バンドルと縮小はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a613b-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="a613b-110">ご不便をおかけして申し訳ありません。</span><span class="sxs-lookup"><span data-stu-id="a613b-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="a613b-111">パッケージは、ASP.NET Web ページ2および WebMatrix 2 の最終リリースで使用できることが想定されています。</span><span class="sxs-lookup"><span data-stu-id="a613b-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
