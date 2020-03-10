---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[操作方法:] HTTP ヘッダーの情報に基づいて ASP.NET ページをキャッシュする |Microsoft Docs'
author: rick-anderson
description: このビデオでは、ページの HTTP ヘッダーの情報に基づいて、ページを ASP.NET 出力キャッシュに保持する方法を示しています。 最初に、可能性のある HTTP hea...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506974"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="9d61e-104">[操作方法:] HTTP ヘッダーの情報に基づいて ASP.NET ページをキャッシュする</span><span class="sxs-lookup"><span data-stu-id="9d61e-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="9d61e-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="9d61e-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="9d61e-106">このビデオでは、ページの HTTP ヘッダーの情報に基づいて、ページを ASP.NET 出力キャッシュに保持する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9d61e-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="9d61e-107">まず、可能性のある HTTP ヘッダー値を確認します。</span><span class="sxs-lookup"><span data-stu-id="9d61e-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="9d61e-108">次に、サンプルページが作成され、OutputCache ディレクティブが VaryByHeader 属性と共に使用されます。この属性には、ユーザーのブラウザーの言語に基づいてキャッシュを制御するための値 "accept-language" (HTTP ヘッダー) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9d61e-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="9d61e-109">サンプルページは、英語に設定されている IE で表示され、FireFox ではフランス語を使用するように設定されています。</span><span class="sxs-lookup"><span data-stu-id="9d61e-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="9d61e-110">最後に、キャッシュ定義を web.config ファイルの CacheProfile に移動するオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9d61e-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="9d61e-111">&#9654;ビデオを見る (12 分)</span><span class="sxs-lookup"><span data-stu-id="9d61e-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
