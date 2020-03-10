---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API でのモデル検証-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API でのモデル検証の概要について説明します。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448930"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="f9db5-103">ASP.NET Web API でのモデル検証</span><span class="sxs-lookup"><span data-stu-id="f9db5-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="f9db5-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f9db5-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f9db5-105">この記事では、モデルに注釈を付け、データ検証に注釈を使用して、web API で検証エラーを処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="f9db5-106">クライアントが web API にデータを送信する場合、多くの場合、処理を行う前にデータを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9db5-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="f9db5-107">データの注釈</span><span class="sxs-lookup"><span data-stu-id="f9db5-107">Data Annotations</span></span>

<span data-ttu-id="f9db5-108">ASP.NET Web API では、 [system.componentmodel](/dotnet/api/system.componentmodel.dataannotations)名前空間の属性を使用して、モデルのプロパティの検証規則を設定できます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="f9db5-109">次のモデルがあるとします。</span><span class="sxs-lookup"><span data-stu-id="f9db5-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="f9db5-110">ASP.NET MVC でモデルの検証を使用したことがある場合は、このことを理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9db5-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="f9db5-111">**Required**属性では、`Name` プロパティを null にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="f9db5-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="f9db5-112">**Range**属性では、`Weight` が0から999の間である必要があることが示されます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="f9db5-113">クライアントが POST 要求を次の JSON 表現で送信するとします。</span><span class="sxs-lookup"><span data-stu-id="f9db5-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="f9db5-114">クライアントには、必須としてマークされている `Name` プロパティが含まれていないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="f9db5-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="f9db5-115">Web API が JSON を `Product` インスタンスに変換すると、検証属性に対して `Product` が検証されます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="f9db5-116">コントローラーアクションでは、モデルが有効かどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="f9db5-117">モデルの検証では、クライアントデータが安全であることは保証されません。</span><span class="sxs-lookup"><span data-stu-id="f9db5-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="f9db5-118">アプリケーションの他の層では、追加の検証が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f9db5-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="f9db5-119">(たとえば、データ層によって外部キー制約が適用される場合があります)。[WEB API と Entity Framework を使用し](../data/using-web-api-with-entity-framework/part-1.md)たチュートリアルでは、これらの問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="f9db5-120">**"投稿中"** : クライアントがいくつかのプロパティを除外した場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="f9db5-121">たとえば、クライアントが次のものを送信するとします。</span><span class="sxs-lookup"><span data-stu-id="f9db5-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="f9db5-122">ここでは、クライアントは `Price` または `Weight`の値を指定しませんでした。</span><span class="sxs-lookup"><span data-stu-id="f9db5-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="f9db5-123">JSON フォーマッタは、不足しているプロパティに既定値の0を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="f9db5-124">モデルの状態は有効です。これは、これらのプロパティの値が0であるためです。</span><span class="sxs-lookup"><span data-stu-id="f9db5-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="f9db5-125">これが問題かどうかは、実際のシナリオによって異なります。</span><span class="sxs-lookup"><span data-stu-id="f9db5-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="f9db5-126">たとえば、更新操作では、"zero" と "not set" の区別が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f9db5-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="f9db5-127">強制的にクライアントが値を設定するようにするには、プロパティを nullable にし、 **Required**属性を設定します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="f9db5-128">**"過剰ポスト"** : クライアントは、予想よりも*多く*のデータを送信できます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="f9db5-129">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="f9db5-130">ここでは、JSON には、`Product` モデルに存在しないプロパティ ("Color") が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f9db5-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="f9db5-131">この場合、JSON フォーマッタは単にこの値を無視します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="f9db5-132">(XML フォーマッタは同じように動作します)。モデルに読み取り専用のプロパティが含まれている場合、過剰なポストによって問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="f9db5-133">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="f9db5-134">ユーザーが `IsAdmin` プロパティを更新し、自身を管理者に昇格させたくない。</span><span class="sxs-lookup"><span data-stu-id="f9db5-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="f9db5-135">最も安全な方法は、クライアントが送信できるものと完全に一致するモデルクラスを使用することです。</span><span class="sxs-lookup"><span data-stu-id="f9db5-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="f9db5-136">Brad Wilson のブログ投稿「[ASP.NET MVC での入力検証とモデル検証」で](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)は、投稿と過剰投稿についてよく説明しています。</span><span class="sxs-lookup"><span data-stu-id="f9db5-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="f9db5-137">この投稿は ASP.NET MVC 2 に関するものですが、問題は引き続き Web API に関連しています。</span><span class="sxs-lookup"><span data-stu-id="f9db5-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="f9db5-138">検証エラーの処理</span><span class="sxs-lookup"><span data-stu-id="f9db5-138">Handling Validation Errors</span></span>

<span data-ttu-id="f9db5-139">検証が失敗した場合、Web API からクライアントに自動的にエラーが返されることはありません。</span><span class="sxs-lookup"><span data-stu-id="f9db5-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="f9db5-140">モデルの状態を確認し、適切に応答するには、コントローラーアクションが必要です。</span><span class="sxs-lookup"><span data-stu-id="f9db5-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="f9db5-141">また、アクションフィルターを作成して、コントローラーアクションが呼び出される前にモデルの状態を確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="f9db5-142">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="f9db5-143">モデルの検証が失敗した場合、このフィルターは検証エラーを含む HTTP 応答を返します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="f9db5-144">その場合、コントローラーアクションは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="f9db5-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="f9db5-145">このフィルターをすべての Web API コントローラーに適用するには、構成時にフィルターのインスタンスを**Httpconfiguration. Filters**コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="f9db5-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="f9db5-146">別の方法として、フィルターを個々のコントローラーまたはコントローラーアクションの属性として設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="f9db5-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
