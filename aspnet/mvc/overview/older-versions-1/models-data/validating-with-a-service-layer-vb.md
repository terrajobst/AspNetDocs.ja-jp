---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: サービス層を使用した検証 (VB) |Microsoft Docs
author: StephenWalther
description: コントローラーアクションから別のサービスレイヤーに検証ロジックを移動する方法について説明します。 このチュートリアルでは、Stephen Walther がその方法について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436576"
---
# <a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="0d32d-104">サービス層の検証 (VB)</span><span class="sxs-lookup"><span data-stu-id="0d32d-104">Validating with a Service Layer (VB)</span></span>

<span data-ttu-id="0d32d-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="0d32d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="0d32d-106">コントローラーアクションから別のサービスレイヤーに検証ロジックを移動する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="0d32d-107">このチュートリアルでは、Stephen Walther は、コントローラーレイヤーからサービス層を分離することによって、問題を明確に分離する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="0d32d-108">このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行する1つの方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="0d32d-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="0d32d-109">このチュートリアルでは、検証ロジックをコントローラーから別のサービス層に移動する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="0d32d-110">懸念事項の分離</span><span class="sxs-lookup"><span data-stu-id="0d32d-110">Separating Concerns</span></span>

<span data-ttu-id="0d32d-111">ASP.NET MVC アプリケーションをビルドする場合は、コントローラーアクション内にデータベースロジックを配置しないでください。</span><span class="sxs-lookup"><span data-stu-id="0d32d-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="0d32d-112">データベースとコントローラーのロジックを混在させると、時間の経過と共にアプリケーションの保守が困難になります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="0d32d-113">すべてのデータベースロジックを別のリポジトリレイヤーに配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0d32d-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="0d32d-114">たとえば、リスト1には、ProductRepository という名前の単純なリポジトリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="0d32d-115">製品リポジトリには、アプリケーションのすべてのデータアクセスコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="0d32d-116">この一覧には、製品リポジトリによって実装される IProductRepository インターフェイスも含まれています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="0d32d-117">**リスト 1-Models\ProductRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="0d32d-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="0d32d-118">リスト2のコントローラーは、Index () アクションと Create () アクションの両方でリポジトリレイヤーを使用します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="0d32d-119">このコントローラーには、データベースロジックが含まれていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0d32d-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="0d32d-120">リポジトリレイヤーを作成することで、問題の明確な分離を維持することができます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="0d32d-121">コントローラーはアプリケーションフロー制御ロジックを担当し、リポジトリはデータアクセスロジックを担当します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="0d32d-122">**リスト 2-アドオン (productコントローラー)**</span><span class="sxs-lookup"><span data-stu-id="0d32d-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="0d32d-123">サービス層の作成</span><span class="sxs-lookup"><span data-stu-id="0d32d-123">Creating a Service Layer</span></span>

<span data-ttu-id="0d32d-124">そのため、アプリケーションフロー制御ロジックはコントローラーに属し、データアクセスロジックはリポジトリに属します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="0d32d-125">その場合は、検証ロジックをどこに配置すればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="0d32d-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="0d32d-126">1つの方法として、検証ロジックを*サービス層*に配置する方法があります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="0d32d-127">サービスレイヤーは、コントローラーとリポジトリレイヤー間の通信を仲介する ASP.NET MVC アプリケーションの追加レイヤーです。</span><span class="sxs-lookup"><span data-stu-id="0d32d-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="0d32d-128">サービス層にはビジネスロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-128">The service layer contains business logic.</span></span> <span data-ttu-id="0d32d-129">特に、検証ロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="0d32d-130">たとえば、リスト3の product service レイヤーには CreateProduct () メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="0d32d-131">CreateProduct () メソッドは、製品リポジトリに製品を渡す前に、ValidateProduct () メソッドを呼び出して新しい製品を検証します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="0d32d-132">**リスト 3-Modelproductservice. vb**</span><span class="sxs-lookup"><span data-stu-id="0d32d-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="0d32d-133">製品コントローラーは、リポジトリレイヤーではなくサービスレイヤーを使用するように、リスト4で更新されています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="0d32d-134">コントローラーレイヤーは、サービスレイヤーと通信します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="0d32d-135">サービス層は、リポジトリレイヤーと通信します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="0d32d-136">各レイヤーには個別の責任があります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="0d32d-137">**リスト 4-コントローラーの一覧表示 (vb)**</span><span class="sxs-lookup"><span data-stu-id="0d32d-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="0d32d-138">Product service が product controller コンストラクターに作成されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0d32d-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="0d32d-139">製品サービスが作成されると、モデル状態ディクショナリがサービスに渡されます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="0d32d-140">製品サービスは、モデルの状態を使用して、検証エラーメッセージをコントローラーに返します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="0d32d-141">サービス層の分離</span><span class="sxs-lookup"><span data-stu-id="0d32d-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="0d32d-142">コントローラー層とサービス層を1つの観点で分離できませんでした。</span><span class="sxs-lookup"><span data-stu-id="0d32d-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="0d32d-143">コントローラー層とサービス層は、モデルの状態を介して通信します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="0d32d-144">つまり、サービスレイヤーは、ASP.NET MVC フレームワークの特定の機能に依存しています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="0d32d-145">サービス層は、可能な限りコントローラーレイヤーから分離する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="0d32d-146">理論的には、ASP.NET MVC アプリケーションだけでなく、あらゆる種類のアプリケーションでサービスレイヤーを使用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="0d32d-147">たとえば、将来的には、アプリケーションの WPF フロントエンドを構築することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="0d32d-148">サービスレイヤーから ASP.NET MVC モデルの状態に対する依存関係を削除する方法が見つかります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="0d32d-149">リスト5では、サービス層が更新され、モデルの状態が使用されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="0d32d-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="0d32d-150">代わりに、IValidationDictionary インターフェイスを実装する任意のクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="0d32d-151">**リスト 5-modelproductservicevb (分離)**</span><span class="sxs-lookup"><span data-stu-id="0d32d-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="0d32d-152">IValidationDictionary インターフェイスは、リスト6で定義されています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="0d32d-153">この単純なインターフェイスには、1つのメソッドと1つのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="0d32d-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="0d32d-154">**リスト 6-modelivalidationdictionary, cs**</span><span class="sxs-lookup"><span data-stu-id="0d32d-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="0d32d-155">リスト7のクラス (ModelStateWrapper クラス) には、IValidationDictionary インターフェイスが実装されています。</span><span class="sxs-lookup"><span data-stu-id="0d32d-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="0d32d-156">モデル状態ディクショナリをコンストラクターに渡すことによって、ModelStateWrapper クラスをインスタンス化できます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="0d32d-157">**リスト 7-Models\ModelStateWrapper.vb**</span><span class="sxs-lookup"><span data-stu-id="0d32d-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="0d32d-158">最後に、リスト8の更新されたコントローラーは、コンストラクターでサービス層を作成するときに ModelStateWrapper を使用します。</span><span class="sxs-lookup"><span data-stu-id="0d32d-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="0d32d-159">**リスト 8-コントローラーの一覧表示 (vb)**</span><span class="sxs-lookup"><span data-stu-id="0d32d-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="0d32d-160">IValidationDictionary インターフェイスと ModelStateWrapper クラスを使用すると、サービスレイヤーをコントローラーレイヤーから完全に分離することができます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="0d32d-161">サービス層は、モデルの状態に依存しなくなりました。</span><span class="sxs-lookup"><span data-stu-id="0d32d-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="0d32d-162">IValidationDictionary インターフェイスを実装する任意のクラスをサービス層に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="0d32d-163">たとえば、WPF アプリケーションでは、単純なコレクションクラスを使用して IValidationDictionary インターフェイスを実装できます。</span><span class="sxs-lookup"><span data-stu-id="0d32d-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="0d32d-164">まとめ</span><span class="sxs-lookup"><span data-stu-id="0d32d-164">Summary</span></span>

<span data-ttu-id="0d32d-165">このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行する方法の1つについて説明することでした。</span><span class="sxs-lookup"><span data-stu-id="0d32d-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="0d32d-166">このチュートリアルでは、すべての検証ロジックをコントローラーから別のサービス層に移動する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="0d32d-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="0d32d-167">また、ModelStateWrapper クラスを作成して、コントローラーレイヤーからサービス層を分離する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="0d32d-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0d32d-168">[前へ](validating-with-the-idataerrorinfo-interface-vb.md)
> [次へ](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0d32d-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>
