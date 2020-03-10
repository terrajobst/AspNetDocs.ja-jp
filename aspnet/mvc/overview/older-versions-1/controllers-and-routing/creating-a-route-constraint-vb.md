---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: ルート制約を作成する (VB) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、正規表現を使用してルート制約を作成することによって、ルートがどのように一致するかを制御する方法を示しています。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486772"
---
# <a name="creating-a-route-constraint-vb"></a><span data-ttu-id="32f41-103">ルート制約を作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="32f41-103">Creating a Route Constraint (VB)</span></span>

<span data-ttu-id="32f41-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="32f41-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="32f41-105">このチュートリアルでは、Stephen Walther は、正規表現を使用してルート制約を作成することによって、ルートがどのように一致するかを制御する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32f41-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="32f41-106">ルート制約は、特定のルートに一致するブラウザー要求を制限するために使用します。</span><span class="sxs-lookup"><span data-stu-id="32f41-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="32f41-107">正規表現を使用して、ルート制約を指定することができます。</span><span class="sxs-lookup"><span data-stu-id="32f41-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="32f41-108">たとえば、リスト1のルートが global.asax ファイルに定義されているとします。</span><span class="sxs-lookup"><span data-stu-id="32f41-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="32f41-109">**リスト 1-global.asax**</span><span class="sxs-lookup"><span data-stu-id="32f41-109">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="32f41-110">リスト1には、Product という名前のルートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="32f41-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="32f41-111">製品ルートを使用して、リスト2に含まれる ProductController にブラウザーの要求をマップできます。</span><span class="sxs-lookup"><span data-stu-id="32f41-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="32f41-112">**リスト 2-アドオン (productコントローラー)**</span><span class="sxs-lookup"><span data-stu-id="32f41-112">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="32f41-113">Product コントローラーによって公開されている Details () アクションでは、productId という名前の1つのパラメーターを受け取ることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="32f41-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="32f41-114">このパラメーターは整数のパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="32f41-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="32f41-115">リスト1で定義されているルートは、次の Url のいずれかと一致します。</span><span class="sxs-lookup"><span data-stu-id="32f41-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="32f41-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="32f41-116">/Product/23</span></span>
- <span data-ttu-id="32f41-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="32f41-117">/Product/7</span></span>

<span data-ttu-id="32f41-118">残念ながら、ルートは次の Url とも一致します。</span><span class="sxs-lookup"><span data-stu-id="32f41-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="32f41-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="32f41-119">/Product/blah</span></span>
- <span data-ttu-id="32f41-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="32f41-120">/Product/apple</span></span>

<span data-ttu-id="32f41-121">Details () アクションには整数のパラメーターが必要であるため、整数値以外を含む要求を行うと、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="32f41-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="32f41-122">たとえば、ブラウザーに「/Product/apple」と入力すると、図1のエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="32f41-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="32f41-123">[[新しいプロジェクト] ダイアログボックスの ![](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="32f41-123">[![The New Project dialog box](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span></span>

<span data-ttu-id="32f41-124">**図 01**: ページの爆発を[確認する (クリックすると、フルサイズの画像が表示](creating-a-route-constraint-vb/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="32f41-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>

<span data-ttu-id="32f41-125">実際に必要なのは、productId が適切な整数を含む Url だけです。</span><span class="sxs-lookup"><span data-stu-id="32f41-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="32f41-126">ルートを定義するときに、ルートに一致する Url を制限するための制約を使用できます。</span><span class="sxs-lookup"><span data-stu-id="32f41-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="32f41-127">リスト3の変更された製品ルートには、整数のみに一致する正規表現制約が含まれています。</span><span class="sxs-lookup"><span data-stu-id="32f41-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="32f41-128">**リスト 3-global.asax**</span><span class="sxs-lookup"><span data-stu-id="32f41-128">**Listing 3 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="32f41-129">正規表現 \d + は、1つ以上の整数に一致します。</span><span class="sxs-lookup"><span data-stu-id="32f41-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="32f41-130">この制約により、製品ルートは次の Url と一致します。</span><span class="sxs-lookup"><span data-stu-id="32f41-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="32f41-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="32f41-131">/Product/3</span></span>
- <span data-ttu-id="32f41-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="32f41-132">/Product/8999</span></span>

<span data-ttu-id="32f41-133">ただし、次の Url はありません。</span><span class="sxs-lookup"><span data-stu-id="32f41-133">But not the following URLs:</span></span>

- <span data-ttu-id="32f41-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="32f41-134">/Product/apple</span></span>
- <span data-ttu-id="32f41-135">/Product</span><span class="sxs-lookup"><span data-stu-id="32f41-135">/Product</span></span>

<span data-ttu-id="32f41-136">これらのブラウザー要求は別のルートによって処理されます。一致するルートがない場合は、*リソースが見つからない*というエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="32f41-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32f41-137">[前へ](creating-custom-routes-vb.md)
> [次へ](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="32f41-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>
