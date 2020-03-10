---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: '操作方法: ASP.NET Routing で Url を操作する | Microsoft Docs'
author: rick-anderson
description: このビデオでは、ASP.NET ルーティングを利用する web サイトで Url を指定する方法について説明します。 まず、web サイトを作成し、そのルーティングを Gl...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: eb1060fd9cc9469dc2b1d2e918823316c36840cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455692"
---
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a><span data-ttu-id="0ec40-105">操作方法: ASP.NET Routing で Url を操作する</span><span class="sxs-lookup"><span data-stu-id="0ec40-105">How Do I: Work with URLs in ASP.NET Routing?</span></span>

<span data-ttu-id="0ec40-106">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="0ec40-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="0ec40-107">このビデオでは、ASP.NET ルーティングを利用する web サイトで Url を指定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0ec40-107">In this video Chris Pels shows how to specify URLs in a web site that utilizes ASP.NET routing.</span></span> <span data-ttu-id="0ec40-108">まず、web サイトを作成し、グローバルアプリケーションクラス (global.asax) でルーティングを定義します。</span><span class="sxs-lookup"><span data-stu-id="0ec40-108">First, a web site is created and routing is defined in the Global Application Class (.asax).</span></span> <span data-ttu-id="0ec40-109">次に、サンプルの web ページが作成され、定義されたルートに基づく URL が、"ハードコーディングされた標準" アプローチ (たとえば、"~/Stats/訪問者") を使用してページに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0ec40-109">Next, a sample web page is created and a URL based upon a defined route is added to the page using the standard "hard coded" approach, e.g., "~/Stats/Visitors".</span></span> <span data-ttu-id="0ec40-110">もう1つのリンクがページに追加されます。このページでは、ルート名とパラメーターを受け取る RouteValue メソッドを使用して、マークアップで同じ URL を動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="0ec40-110">Another link is then added to the page which dynamically generates the same URL in markup using the RouteValue method which accepts the route name and parameters.</span></span> <span data-ttu-id="0ec40-111">同じ URL は、マークアップではなく、コードを使用してページに直接実装されます。</span><span class="sxs-lookup"><span data-stu-id="0ec40-111">The same URL is then implemented using code rather than markup directly in the page.</span></span> <span data-ttu-id="0ec40-112">次に、元のルートと物理的なページの場所が変更されるため、ハードコーディングされたリンクは動作しなくなり、動的に生成されたリンクはどちらも正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="0ec40-112">The original route and physical page location are then changed, resulting in the hard coded link no longer working whereas both dynamically generated links function properly.</span></span> <span data-ttu-id="0ec40-113">最後に、動的に生成されたリンクの値について説明します。</span><span class="sxs-lookup"><span data-stu-id="0ec40-113">Finally, the value of dynamically generated links is then discussed.</span></span>

[<span data-ttu-id="0ec40-114">&#9654;ビデオを見る (20 分)</span><span class="sxs-lookup"><span data-stu-id="0ec40-114">&#9654; Watch video (20 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> <span data-ttu-id="0ec40-115">[[戻る]](how-do-i-use-routing-with-aspnet-web-forms.md)</span><span class="sxs-lookup"><span data-stu-id="0ec40-115">[Previous](how-do-i-use-routing-with-aspnet-web-forms.md)</span></span>
