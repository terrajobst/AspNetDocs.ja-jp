---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: カスタムルートを作成C#する () |Microsoft Docs
author: microsoft
description: ASP.NET MVC アプリケーションにカスタムルートを追加する方法について説明します。 このチュートリアルでは、global.asax ファイルの既定のルートテーブルを変更する方法について説明します。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 58f72e390f0053d136ef00ddbda0b071ba225d98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486724"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="6aa41-104">カスタム ルートを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="6aa41-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="6aa41-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6aa41-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6aa41-106">ASP.NET MVC アプリケーションにカスタムルートを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="6aa41-107">このチュートリアルでは、global.asax ファイルの既定のルートテーブルを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="6aa41-108">このチュートリアルでは、ASP.NET MVC アプリケーションにカスタムルートを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="6aa41-109">Global.asax ファイルの既定のルートテーブルをカスタムルートで変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="6aa41-110">多くの単純な ASP.NET MVC アプリケーションでは、既定のルートテーブルは正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="6aa41-111">ただし、特化されたルーティングニーズがあることがわかります。</span><span class="sxs-lookup"><span data-stu-id="6aa41-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="6aa41-112">その場合は、カスタムルートを作成できます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="6aa41-113">たとえば、ブログアプリケーションを作成する場合を考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="6aa41-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="6aa41-114">次のような受信要求を処理することができます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="6aa41-115">/アーカイブ/月3日</span><span class="sxs-lookup"><span data-stu-id="6aa41-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="6aa41-116">ユーザーがこの要求を入力すると、12/25/2009 日付に対応するブログエントリが返されます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="6aa41-117">この種類の要求を処理するには、カスタムルートを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6aa41-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="6aa41-118">リスト1の global.asax ファイルには、"ブログ" という名前の新しいカスタムルートが含まれています。このルートは、/アーカイブ/*エントリ日付*のような要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="6aa41-119">**リスト 1-global.asax (カスタムルートを使用)**</span><span class="sxs-lookup"><span data-stu-id="6aa41-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="6aa41-120">ルートテーブルに追加するルートの順序は重要です。</span><span class="sxs-lookup"><span data-stu-id="6aa41-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="6aa41-121">新しいカスタムブログルートは、既存の既定のルートの前に追加されます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="6aa41-122">順序を逆にした場合、既定のルートは常にカスタムルートではなく呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="6aa41-123">カスタムブログルートは、/Archive/. で始まるすべての要求と一致します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="6aa41-124">そのため、これは次のすべての Url と一致します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="6aa41-125">/アーカイブ/月3日</span><span class="sxs-lookup"><span data-stu-id="6aa41-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="6aa41-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="6aa41-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="6aa41-127">/アーカイブ/apple</span><span class="sxs-lookup"><span data-stu-id="6aa41-127">/Archive/apple</span></span>

<span data-ttu-id="6aa41-128">カスタムルートは、受信要求を Archive という名前のコントローラーにマップし、Entry () アクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="6aa41-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="6aa41-129">Entry () メソッドが呼び出されると、エントリ日付は entryDate という名前のパラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="6aa41-130">リスト2のコントローラーで、ブログカスタムルートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6aa41-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="6aa41-131">**リスト 2-ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="6aa41-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="6aa41-132">リスト2の Entry () メソッドでは、DateTime 型のパラメーターを受け取ることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6aa41-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="6aa41-133">MVC フレームワークは、URL のエントリ日付を DateTime 値に自動的に変換するのに十分なスマートです。</span><span class="sxs-lookup"><span data-stu-id="6aa41-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="6aa41-134">URL のエントリ日付パラメーターを DateTime に変換できない場合は、エラーが発生します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="6aa41-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="6aa41-135">**図 1-パラメーターの変換エラー**</span><span class="sxs-lookup"><span data-stu-id="6aa41-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="6aa41-136">[[新しいプロジェクト] ダイアログボックスの ![](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6aa41-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="6aa41-137">**図 01**: パラメーターの変換時のエラー ([クリックすると、フルサイズの画像が表示](creating-custom-routes-cs/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="6aa41-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="6aa41-138">まとめ</span><span class="sxs-lookup"><span data-stu-id="6aa41-138">Summary</span></span>

<span data-ttu-id="6aa41-139">このチュートリアルの目的は、カスタムルートを作成する方法を説明することでした。</span><span class="sxs-lookup"><span data-stu-id="6aa41-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="6aa41-140">ブログエントリを表す global.asax ファイルのルートテーブルにカスタムルートを追加する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="6aa41-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="6aa41-141">ブログエントリの要求を、ArchiveController という名前のコントローラーと、Entry () という名前のコントローラーアクションにマップする方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="6aa41-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6aa41-142">[前へ](aspnet-mvc-controllers-overview-cs.md)
> [次へ](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6aa41-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
