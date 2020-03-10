---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: カスタムルート制約を作成する (VB) |Microsoft Docs
author: StephenWalther
description: Stephen Walther は、カスタムルート制約を作成する方法を示しています。 ルートが一致しないようにする単純なカスタム制約を実装しています...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486790"
---
# <a name="creating-a-custom-route-constraint-vb"></a><span data-ttu-id="aef3e-104">カスタム ルート制約を作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="aef3e-104">Creating a Custom Route Constraint (VB)</span></span>

<span data-ttu-id="aef3e-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="aef3e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="aef3e-106">Stephen Walther は、カスタムルート制約を作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="aef3e-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="aef3e-107">リモートコンピューターからブラウザーの要求が行われたときに、ルートが一致しないようにする単純なカスタム制約を実装します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="aef3e-108">このチュートリアルの目的は、カスタムルート制約を作成する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="aef3e-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="aef3e-109">カスタムルート制約を使用すると、一部のカスタム条件に一致しない限り、ルートが一致しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="aef3e-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="aef3e-110">このチュートリアルでは、Localhost ルート制約を作成します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="aef3e-111">Localhost route 制約は、ローカルコンピューターからの要求のみと一致します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="aef3e-112">インターネット経由のリモート要求が一致しません。</span><span class="sxs-lookup"><span data-stu-id="aef3e-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="aef3e-113">カスタムルート制約を実装するには、IRouteConstraint インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="aef3e-114">これは、1つのメソッドを記述する非常に単純なインターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="aef3e-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="aef3e-115">メソッドはブール値を返します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-115">The method returns a Boolean value.</span></span> <span data-ttu-id="aef3e-116">False を返した場合、制約に関連付けられているルートはブラウザーの要求と一致しません。</span><span class="sxs-lookup"><span data-stu-id="aef3e-116">If you return False, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="aef3e-117">Localhost 制約は、リスト1に含まれています。</span><span class="sxs-lookup"><span data-stu-id="aef3e-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="aef3e-118">**リスト 1-LocalhostConstraint .vb**</span><span class="sxs-lookup"><span data-stu-id="aef3e-118">**Listing 1 - LocalhostConstraint.vb**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="aef3e-119">リスト1の制約では、HttpRequest クラスによって公開されている IsLocal プロパティを利用します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="aef3e-120">このプロパティは、要求の IP アドレスが127.0.0.1 であるか、要求の IP アドレスがサーバーの IP アドレスと同じである場合に true を返します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="aef3e-121">Global.asax ファイルで定義されているルート内でカスタム制約を使用します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="aef3e-122">リスト2の global.asax ファイルは Localhost 制約を使用して、ローカルサーバーから要求を行う場合を除き、だれでも管理ページを要求しないようにします。</span><span class="sxs-lookup"><span data-stu-id="aef3e-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="aef3e-123">たとえば、リモートサーバーからの/Admin/DeleteAll 要求は失敗します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="aef3e-124">**リスト 2-global.asax**</span><span class="sxs-lookup"><span data-stu-id="aef3e-124">**Listing 2 - Global.asax**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="aef3e-125">Localhost 制約は、管理ルートの定義で使用されます。</span><span class="sxs-lookup"><span data-stu-id="aef3e-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="aef3e-126">このルートは、リモートブラウザーの要求と一致しません。</span><span class="sxs-lookup"><span data-stu-id="aef3e-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="aef3e-127">ただし、global.asax で定義されている他のルートは、同じ要求と一致している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="aef3e-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="aef3e-128">制約は、グローバルな global.asax ファイルで定義されているすべてのルートではなく、特定のルートが要求と一致しないようにすることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="aef3e-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="aef3e-129">リスト2の global.asax ファイルから、既定のルートがコメントアウトされていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="aef3e-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="aef3e-130">既定のルートを含めると、既定のルートは管理コントローラーの要求と一致します。</span><span class="sxs-lookup"><span data-stu-id="aef3e-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="aef3e-131">その場合でも、リモートユーザーは、要求が管理者ルートと一致しない場合でも、管理コントローラーのアクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="aef3e-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aef3e-132">[[戻る]](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="aef3e-132">[Previous](creating-a-route-constraint-vb.md)</span></span>
