---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: アクションを作成する (C#) |Microsoft Docs
author: microsoft
description: ASP.NET MVC のコント ローラーに新しいアクションを追加する方法について説明します。 メソッドを操作するための要件について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 243248ee30c6a2db7f102f7743d0393d4a6a9d24
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056129"
---
<a name="creating-an-action-c"></a><span data-ttu-id="492d6-104">アクションを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="492d6-104">Creating an Action (C#)</span></span>
====================
<span data-ttu-id="492d6-105">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="492d6-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="492d6-106">ASP.NET MVC のコント ローラーに新しいアクションを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="492d6-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="492d6-107">メソッドを操作するための要件について説明します。</span><span class="sxs-lookup"><span data-stu-id="492d6-107">Learn about the requirements for a method to be an action.</span></span>


<span data-ttu-id="492d6-108">このチュートリアルの目的では、新しいコント ローラーのアクションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="492d6-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="492d6-109">アクション メソッドの要件について説明します。</span><span class="sxs-lookup"><span data-stu-id="492d6-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="492d6-110">メソッドがアクションとして公開されないようにする方法を学びます。</span><span class="sxs-lookup"><span data-stu-id="492d6-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="492d6-111">コント ローラー アクションの追加</span><span class="sxs-lookup"><span data-stu-id="492d6-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="492d6-112">コント ローラーに新しいアクションを追加するには、コント ローラーに新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="492d6-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="492d6-113">たとえば、リスト 1 で、コント ローラーには、Index() という名前のアクションと SayHello() という名前のアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="492d6-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="492d6-114">どちらの方法は、アクションとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="492d6-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="492d6-115">**Listing 1 - Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="492d6-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="492d6-116">メソッドは、アクションとして universe に公開するために、特定の要件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="492d6-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="492d6-117">メソッドは、パブリックである必要があります。</span><span class="sxs-lookup"><span data-stu-id="492d6-117">The method must be public.</span></span>
- <span data-ttu-id="492d6-118">メソッドは、静的メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="492d6-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="492d6-119">メソッドは、拡張メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="492d6-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="492d6-120">メソッドは、コンス トラクター、getter、または set アクセス操作子にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="492d6-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="492d6-121">メソッドは、オープン ジェネリック型を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="492d6-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="492d6-122">メソッドは、コント ローラーの基本クラスのメソッドではありません。</span><span class="sxs-lookup"><span data-stu-id="492d6-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="492d6-123">メソッドを含めることはできません**ref**または**アウト**パラメーター。</span><span class="sxs-lookup"><span data-stu-id="492d6-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="492d6-124">コント ローラー アクションの戻り値の型に制限がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="492d6-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="492d6-125">コント ローラー アクションには、文字列、DateTime、void、Random クラスのインスタンスを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="492d6-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="492d6-126">ASP.NET MVC フレームワークはアクションの結果を文字列にではない戻り値の型を変換し、ブラウザーに文字列を表示します。</span><span class="sxs-lookup"><span data-stu-id="492d6-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="492d6-127">コント ローラーにこれらの要件に違反しない任意のメソッドを追加すると、メソッドは、コント ローラーのアクションとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="492d6-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="492d6-128">ここでも注意します。</span><span class="sxs-lookup"><span data-stu-id="492d6-128">Be careful here.</span></span> <span data-ttu-id="492d6-129">コント ローラーのアクションは、インターネットに接続されているすべてのユーザーが呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="492d6-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="492d6-130">DeleteMyWebsite() コント ローラーのアクションをたとえば、作成、操作を行います。</span><span class="sxs-lookup"><span data-stu-id="492d6-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="492d6-131">パブリック メソッドが呼び出されていることを防ぐ</span><span class="sxs-lookup"><span data-stu-id="492d6-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="492d6-132">コント ローラー クラスにパブリック メソッドを作成する必要があると、コント ローラーのアクションとしてメソッドを公開する場合は、[NonAction] 属性を使用して呼び出されているからメソッドを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="492d6-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="492d6-133">たとえば、リスト 2 でコント ローラーには、[NonAction] 属性で装飾した CompanySecrets() をという名前のパブリック メソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="492d6-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="492d6-134">**2 - Controllers\WorkController.cs を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="492d6-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="492d6-135">CompanySecrets() コント ローラーのアクションを起動するには、お使いのブラウザーのアドレス バーに/Work/CompanySecrets を入力しようとした場合は、図 1 で、エラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="492d6-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>


<span data-ttu-id="492d6-136">[![NonAction メソッドを呼び出す](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="492d6-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="492d6-137">**図 01**:NonAction メソッドを呼び出す ([フルサイズの画像を表示する をクリックします](creating-an-action-cs/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="492d6-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="492d6-138">[前へ](creating-a-controller-cs.md)
> [次へ](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="492d6-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
