---
uid: mvc/overview/older-versions-1/controllers-and-routing/index
title: コント ローラーとルーティング |Microsoft Docs
author: rick-anderson
description: このチュートリアルのセットについて説明します、ASP.NET のルーティングの ASP.NET MVC コント ローラー アクションへのブラウザーの要求をマップします。
ms.author: riande
ms.date: 09/28/2011
ms.assetid: 124df537-428c-4861-b6c2-4830c094fe0c
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing
msc.type: chapter
ms.openlocfilehash: 62e8c3c7451373829e2e8fbf65e37a14cfea54df
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123305"
---
# <a name="controllers-and-routing"></a><span data-ttu-id="fa029-103">コントローラーとルーティング</span><span class="sxs-lookup"><span data-stu-id="fa029-103">Controllers and Routing</span></span>

> <span data-ttu-id="fa029-104">このチュートリアルのセットについて説明します、ASP.NET のルーティングの ASP.NET MVC コント ローラー アクションへのブラウザーの要求をマップします。</span><span class="sxs-lookup"><span data-stu-id="fa029-104">In this tutorial set, you learn about ASP.NET routing, which maps browser requests to ASP.NET MVC controller actions.</span></span>

- [<span data-ttu-id="fa029-105">ASP.NET MVC ルーティング概要 (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-105">ASP.NET MVC Routing Overview (C#)</span></span>](asp-net-mvc-routing-overview-cs.md)
- [<span data-ttu-id="fa029-106">アクション フィルターについて理解する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-106">Understanding Action Filters (C#)</span></span>](understanding-action-filters-cs.md)
- [<span data-ttu-id="fa029-107">出力キャッシュでパフォーマンスを改善する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-107">Improving Performance with Output Caching (C#)</span></span>](improving-performance-with-output-caching-cs.md)
- [<span data-ttu-id="fa029-108">キャッシュされたページに動的コンテンツを追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-108">Adding Dynamic Content to a Cached Page (C#)</span></span>](adding-dynamic-content-to-a-cached-page-cs.md)
- [<span data-ttu-id="fa029-109">コントローラーを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-109">Creating a Controller (C#)</span></span>](creating-a-controller-cs.md)
- [<span data-ttu-id="fa029-110">アクションを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-110">Creating an Action (C#)</span></span>](creating-an-action-cs.md)
- [<span data-ttu-id="fa029-111">ASP.NET MVC ルーティング概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-111">ASP.NET MVC Routing Overview (VB)</span></span>](asp-net-mvc-routing-overview-vb.md)
- [<span data-ttu-id="fa029-112">アクション フィルターについて理解する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-112">Understanding Action Filters (VB)</span></span>](understanding-action-filters-vb.md)
- [<span data-ttu-id="fa029-113">出力キャッシュでパフォーマンスを改善する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-113">Improving Performance with Output Caching (VB)</span></span>](improving-performance-with-output-caching-vb.md)
- [<span data-ttu-id="fa029-114">キャッシュされたページに動的コンテンツを追加する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-114">Adding Dynamic Content to a Cached Page (VB)</span></span>](adding-dynamic-content-to-a-cached-page-vb.md)
- [<span data-ttu-id="fa029-115">コントローラーを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-115">Creating a Controller (VB)</span></span>](creating-a-controller-vb.md)
- [<span data-ttu-id="fa029-116">アクションを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-116">Creating an Action (VB)</span></span>](creating-an-action-vb.md)
- [<span data-ttu-id="fa029-117">ASP.NET MVC コントローラーの概要 (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-117">ASP.NET MVC Controller Overview (C#)</span></span>](aspnet-mvc-controllers-overview-cs.md)
- [<span data-ttu-id="fa029-118">カスタム ルートを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-118">Creating Custom Routes (C#)</span></span>](creating-custom-routes-cs.md)
- [<span data-ttu-id="fa029-119">ルート制約を作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-119">Creating a Route Constraint (C#)</span></span>](creating-a-route-constraint-cs.md)
- [<span data-ttu-id="fa029-120">カスタム ルート制約を作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="fa029-120">Creating a Custom Route Constraint (C#)</span></span>](creating-a-custom-route-constraint-cs.md)
- [<span data-ttu-id="fa029-121">ASP.NET MVC コントローラーの概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-121">ASP.NET MVC Controller Overview (VB)</span></span>](asp-net-mvc-controller-overview-vb.md)
- [<span data-ttu-id="fa029-122">カスタム ルートを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-122">Creating Custom Routes (VB)</span></span>](creating-custom-routes-vb.md)
- [<span data-ttu-id="fa029-123">ルート制約を作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-123">Creating a Route Constraint (VB)</span></span>](creating-a-route-constraint-vb.md)
- [<span data-ttu-id="fa029-124">カスタム ルート制約を作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="fa029-124">Creating a Custom Route Constraint (VB)</span></span>](creating-a-custom-route-constraint-vb.md)
