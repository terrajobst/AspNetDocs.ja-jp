---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: アクションを作成するC#() |Microsoft Docs
author: microsoft
description: ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションとして使用するための要件について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470200"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="4a6cb-104">アクションを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="4a6cb-104">Creating an Action (C#)</span></span>

<span data-ttu-id="4a6cb-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4a6cb-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4a6cb-106">ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="4a6cb-107">メソッドをアクションとして使用するための要件について説明します。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="4a6cb-108">このチュートリアルの目的は、新しいコントローラーアクションを作成する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="4a6cb-109">アクションメソッドの要件について説明します。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="4a6cb-110">また、メソッドがアクションとして公開されないようにする方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="4a6cb-111">コントローラーへのアクションの追加</span><span class="sxs-lookup"><span data-stu-id="4a6cb-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="4a6cb-112">コントローラーに新しいアクションを追加するには、コントローラーに新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="4a6cb-113">たとえば、リスト1のコントローラーには、Index () という名前のアクションと、SayHello () という名前のアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="4a6cb-114">どちらのメソッドもアクションとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="4a6cb-115">**リスト 1-Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="4a6cb-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="4a6cb-116">アクションとして universe に公開するには、メソッドが特定の要件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="4a6cb-117">メソッドはパブリックである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-117">The method must be public.</span></span>
- <span data-ttu-id="4a6cb-118">メソッドを静的メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="4a6cb-119">メソッドを拡張メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="4a6cb-120">メソッドをコンストラクター、getter、または setter にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="4a6cb-121">メソッドにオープンジェネリック型を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="4a6cb-122">このメソッドは、コントローラーの基本クラスのメソッドではありません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="4a6cb-123">メソッドに**ref**パラメーターまたは**out**パラメーターを含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="4a6cb-124">コントローラーアクションの戻り値の型に制限がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="4a6cb-125">コントローラーアクションは、文字列、日時、ランダムクラスのインスタンス、または void を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="4a6cb-126">ASP.NET MVC フレームワークは、アクションの結果ではない戻り値の型を文字列に変換し、その文字列をブラウザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="4a6cb-127">これらの要件に違反しないメソッドをコントローラーに追加すると、そのメソッドはコントローラーアクションとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="4a6cb-128">ここで注意してください。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-128">Be careful here.</span></span> <span data-ttu-id="4a6cb-129">コントローラーアクションは、インターネットに接続されているすべてのユーザーが呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="4a6cb-130">たとえば、DeleteMyWebsite () コントローラーアクションを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="4a6cb-131">パブリックメソッドが呼び出されないようにする</span><span class="sxs-lookup"><span data-stu-id="4a6cb-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="4a6cb-132">コントローラークラスでパブリックメソッドを作成する必要があり、そのメソッドをコントローラーアクションとして公開しない場合は、[非アクション] 属性を使用してメソッドが呼び出されないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="4a6cb-133">たとえば、リスト2のコントローラーには、[非アクション] 属性で修飾された、企業秘密 () という名前のパブリックメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="4a6cb-134">**リスト 2-コントローラー (& c)**</span><span class="sxs-lookup"><span data-stu-id="4a6cb-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="4a6cb-135">ブラウザーのアドレスバーに「/職場/会社のシークレット」と入力して、会社のシークレット () コントローラーの操作を呼び出そうとすると、図1のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4a6cb-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="4a6cb-136">[非アクションメソッドを呼び出す ![](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4a6cb-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="4a6cb-137">**図 01**: 非アクションメソッドの呼び出し ([クリックすると、フルサイズの画像が表示](creating-an-action-cs/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="4a6cb-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4a6cb-138">[前へ](creating-a-controller-cs.md)
> [次へ](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4a6cb-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
