---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[操作方法:]カスタム情報に基づいて ASP.NET ページのキャッシュを制御する |Microsoft Docs'
author: rick-anderson
description: このビデオでは、ASP.NET ページをカスタム情報に基づいてキャッシュするための条件を制御する方法について説明します。 サンプルページが作成され、その後に...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506770"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="7358c-104">[操作方法:]カスタム情報に基づいて ASP.NET ページのキャッシュを制御する</span><span class="sxs-lookup"><span data-stu-id="7358c-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="7358c-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="7358c-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="7358c-106">このビデオでは、ASP.NET ページをカスタム情報に基づいてキャッシュするための条件を制御する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7358c-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="7358c-107">サンプルページが作成された後、OutputCache ディレクティブが、カスタム値を含む VaryByCustom 属性と共に使用されます。</span><span class="sxs-lookup"><span data-stu-id="7358c-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="7358c-108">次に、GetVaryCustomByString () メソッドは、カスタム属性の処理を提供する global.asax モジュールでオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="7358c-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="7358c-109">このメソッドでは、ページのキャッシュされたバージョンを一意に識別する文字列が返されます。</span><span class="sxs-lookup"><span data-stu-id="7358c-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="7358c-110">最後に、web サイトのいくつかの方法でカスタム値を使用したキャッシュを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7358c-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="7358c-111">&#9654;ビデオを見る (12 分)</span><span class="sxs-lookup"><span data-stu-id="7358c-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
