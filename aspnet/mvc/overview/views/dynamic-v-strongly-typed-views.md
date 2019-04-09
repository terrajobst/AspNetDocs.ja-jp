---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動的に型指定されたビューと ビューを厳密に型指定 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3235fc58fbf93cb87946f8ebd4a478eff7ce80e3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59386139"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="5daef-103">動的に型指定されたビューと</span><span class="sxs-lookup"><span data-stu-id="5daef-103">Dynamic v.</span></span> <span data-ttu-id="5daef-104">厳密に型指定されたビュー</span><span class="sxs-lookup"><span data-stu-id="5daef-104">Strongly Typed Views</span></span>

<span data-ttu-id="5daef-105">によって[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="5daef-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="5daef-106">ASP.NET MVC 3 でビュー コント ローラーから情報を渡すための 3 つの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="5daef-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="5daef-107">厳密に型指定されたモデル オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="5daef-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="5daef-108">動的な型として (を使用して@model動的)</span><span class="sxs-lookup"><span data-stu-id="5daef-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="5daef-109">ViewBag を使用します。</span><span class="sxs-lookup"><span data-stu-id="5daef-109">Using the ViewBag</span></span>

<span data-ttu-id="5daef-110">動的かつ厳密に型指定されたビューを比較して単純な MVC 3 上位ブログ アプリケーション作成しました。</span><span class="sxs-lookup"><span data-stu-id="5daef-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="5daef-111">ブログの単純なリストから始まって、コント ローラー。</span><span class="sxs-lookup"><span data-stu-id="5daef-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="5daef-112">IndexNotStonglyTyped() メソッド内を右クリックし、Razor ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="5daef-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

[![8<span data-ttu-id="5daef-113">475.NotStronglyTypedView[1]]</span><span class="sxs-lookup"><span data-stu-id="5daef-113">475.NotStronglyTypedView[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

<span data-ttu-id="5daef-114">確認、**厳密に型指定されたビューを作成**ボックスがオンになっていません。</span><span class="sxs-lookup"><span data-stu-id="5daef-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="5daef-115">結果のビューには、ほとんどが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="5daef-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="5daef-116">動的なと厳密に型指定されたビューではなくを使用するため、intellisense が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5daef-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="5daef-117">完成したコードは、以下に示します。</span><span class="sxs-lookup"><span data-stu-id="5daef-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6<span data-ttu-id="5daef-118">646.NotStronglyTypedView_5F00_IE[1]]</span><span class="sxs-lookup"><span data-stu-id="5daef-118">646.NotStronglyTypedView_5F00_IE[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

<span data-ttu-id="5daef-119">厳密に型指定されたビューを追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="5daef-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="5daef-120">コント ローラーには、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="5daef-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


<span data-ttu-id="5daef-121">正確に、同じ戻り View(topBlogs); に注目してください。非厳密に型指定されたビューとして呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5daef-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="5daef-122">内側を右クリックして*StonglyTypedIndex()* 選択**ビューの追加**します。</span><span class="sxs-lookup"><span data-stu-id="5daef-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="5daef-123">この時間を選択、**ブログ**モデル クラスと選択**一覧**スキャフォールディング テンプレートとして。</span><span class="sxs-lookup"><span data-stu-id="5daef-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

[![5<span data-ttu-id="5daef-124">658.StrongView[1]]</span><span class="sxs-lookup"><span data-stu-id="5daef-124">658.StrongView[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

<span data-ttu-id="5daef-125">新しいビュー テンプレートの内部では、intellisense サポートを取得します。</span><span class="sxs-lookup"><span data-stu-id="5daef-125">Inside the new view template we get intellisense support.</span></span>

[![7<span data-ttu-id="5daef-126">002.IntelliSense[1]]</span><span class="sxs-lookup"><span data-stu-id="5daef-126">002.IntelliSense[1]]</span></span>(dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

<span data-ttu-id="5daef-127">C# プロジェクトをダウンロードできます[ここ](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)します。</span><span class="sxs-lookup"><span data-stu-id="5daef-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
