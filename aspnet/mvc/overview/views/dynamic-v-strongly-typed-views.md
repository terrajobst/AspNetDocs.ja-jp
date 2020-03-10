---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動的に型指定されたビューと 厳密に型指定されたビュー |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432574"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="5ce32-103">動的に型指定されたビューと</span><span class="sxs-lookup"><span data-stu-id="5ce32-103">Dynamic v.</span></span> <span data-ttu-id="5ce32-104">厳密に型指定されたビュー</span><span class="sxs-lookup"><span data-stu-id="5ce32-104">Strongly Typed Views</span></span>

<span data-ttu-id="5ce32-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5ce32-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="5ce32-106">コントローラーから ASP.NET MVC 3 のビューに情報を渡すには、次の3つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="5ce32-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="5ce32-107">厳密に型指定されたモデルオブジェクトとして。</span><span class="sxs-lookup"><span data-stu-id="5ce32-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="5ce32-108">動的な型として (@model 動的に使用)</span><span class="sxs-lookup"><span data-stu-id="5ce32-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="5ce32-109">ViewBag を使用する</span><span class="sxs-lookup"><span data-stu-id="5ce32-109">Using the ViewBag</span></span>

<span data-ttu-id="5ce32-110">ここでは、動的および厳密に型指定されたビューを比較対照する、簡単な MVC 3 のブログアプリケーションを作成しました。</span><span class="sxs-lookup"><span data-stu-id="5ce32-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="5ce32-111">コントローラーは、ブログの単純なリストから開始します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="5ce32-112">IndexNotStonglyTyped () メソッドを右クリックし、Razor ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="5ce32-113">[![8475 NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5ce32-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="5ce32-114">[厳密に**型指定されたビューを作成する**] チェックボックスがオフになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="5ce32-115">結果のビューには、あまり多くのものが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="5ce32-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="5ce32-116">厳密に型指定されたビューではなく、動的なを使用しているので、intellisense は役に立ちません。</span><span class="sxs-lookup"><span data-stu-id="5ce32-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="5ce32-117">完成したコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="5ce32-118">[![NotStronglyTypedView_5F00_IE 6646 [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5ce32-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="5ce32-119">次に、厳密に型指定されたビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="5ce32-120">コントローラーに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="5ce32-121">まったく同じ戻り値のビュー (topBlogs) であることに注意してください。厳密に型指定されていないビューとしてを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="5ce32-122">*StonglyTypedIndex ()* の内側を右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="5ce32-123">今度は、**ブログ**モデルクラスを選択し、スキャフォールディングテンプレートとして **[List]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5ce32-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="5ce32-124">[![5658 StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5ce32-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="5ce32-125">新しいビューテンプレート内では、intellisense がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5ce32-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="5ce32-126">[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5ce32-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="5ce32-127">C# プロジェクトは[こちら](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="5ce32-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
