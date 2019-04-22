---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[How Do i:]コントロールのカスタム情報に基づいて ASP.NET ページのキャッシュ |Microsoft Docs'
author: rick-anderson
description: このビデオの Chris Pels では、カスタム情報に基づいて ASP.NET ページをキャッシュするための条件を制御する方法を示します。 サンプル ページの作成と O. し.
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59381407"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="2e064-104">[How Do i:]コントロールのカスタム情報に基づいて ASP.NET ページのキャッシュ</span><span class="sxs-lookup"><span data-stu-id="2e064-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="2e064-105">によって[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="2e064-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="2e064-106">このビデオの Chris Pels では、カスタム情報に基づいて ASP.NET ページをキャッシュするための条件を制御する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2e064-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="2e064-107">サンプル ページが作成され、カスタム値を含む VaryByCustom 属性を持つ、OutputCache ディレクティブを使用します。</span><span class="sxs-lookup"><span data-stu-id="2e064-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="2e064-108">次に、カスタム属性の処理を提供する global.asax モジュールで GetVaryCustomByString() メソッドがオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="2e064-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="2e064-109">メソッドには、ページのキャッシュされたバージョンを一意に識別する文字列が返されます。</span><span class="sxs-lookup"><span data-stu-id="2e064-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="2e064-110">最後は、使用方法についてカスタム値を使用して、キャッシュできるいくつかの方法で web サイトの説明です。</span><span class="sxs-lookup"><span data-stu-id="2e064-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="2e064-111">&#9654;(12 分) のビデオを見る</span><span class="sxs-lookup"><span data-stu-id="2e064-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
