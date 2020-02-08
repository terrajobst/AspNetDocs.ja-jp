---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x のパラメーターバインド
author: MikeWasson
description: Web API がパラメーターをバインドする方法と、ASP.NET 4.x でバインドプロセスをカスタマイズする方法について説明します。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 464cb9b45dc0b62c4da38b7cf612934808854d32
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074905"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="73d4f-103">ASP.NET Web API でのパラメーターバインド</span><span class="sxs-lookup"><span data-stu-id="73d4f-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="73d4f-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="73d4f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="73d4f-105">この記事では、Web API によるパラメーターのバインド方法と、バインドプロセスをカスタマイズする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="73d4f-106">Web API がコントローラー上でメソッドを呼び出す場合は、*バインド*と呼ばれるプロセスであるパラメーターの値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="73d4f-107">既定では、Web API は次の規則を使用してパラメーターをバインドします。</span><span class="sxs-lookup"><span data-stu-id="73d4f-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="73d4f-108">パラメーターが "simple" 型の場合、Web API は URI から値の取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="73d4f-109">単純型には、.NET[プリミティブ型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)(**int**、 **bool**、 **Double**など) に加えて、 **TimeSpan**、 **DateTime**、 **Guid**、 **decimal**、および**string**、および文字列から変換できる型コンバーターを*持つ任意の*型が含まれます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="73d4f-110">(後で型コンバーターについて詳しく説明します)。</span><span class="sxs-lookup"><span data-stu-id="73d4f-110">(More about type converters later.)</span></span>
- <span data-ttu-id="73d4f-111">複合型の場合、Web API は、[メディアの種類のフォーマッタ](media-formatters.md)を使用して、メッセージ本文から値の読み取りを試みます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="73d4f-112">たとえば、一般的な Web API コントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="73d4f-113">*Id*パラメーターは &quot;単純な&quot; 型であるため、Web API は要求 URI から値を取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="73d4f-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="73d4f-114">*Item*パラメーターは複合型であるため、Web API はメディア型フォーマッタを使用して、要求本文から値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="73d4f-115">URI から値を取得するために、Web API はルートデータと URI クエリ文字列を検索します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="73d4f-116">ルートデータは、ルーティングシステムが URI を解析し、それをルートと照合するときに設定されます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="73d4f-117">詳細については、「[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="73d4f-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="73d4f-118">この記事の残りの部分では、モデルバインドプロセスをカスタマイズする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="73d4f-119">ただし、複合型の場合は、可能な限りメディアの種類のフォーマッタを使用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="73d4f-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="73d4f-120">HTTP の重要な原則は、リソースがメッセージ本文で送信されることです。コンテンツネゴシエーションを使用してリソースの表現を指定します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="73d4f-121">メディアタイプのフォーマッタは、まさにこの目的のために設計されています。</span><span class="sxs-lookup"><span data-stu-id="73d4f-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="73d4f-122">[FromUri] を使用する</span><span class="sxs-lookup"><span data-stu-id="73d4f-122">Using [FromUri]</span></span>

<span data-ttu-id="73d4f-123">Web API で URI から複合型を強制的に読み取るには、 **[Fromuri]** 属性をパラメーターに追加します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="73d4f-124">次の例では、URI から `GeoPoint` を取得するコントローラーメソッドと共に `GeoPoint` 型を定義しています。</span><span class="sxs-lookup"><span data-stu-id="73d4f-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="73d4f-125">クライアントは、緯度と経度の値をクエリ文字列に含めることができ、Web API はそれらを使用して `GeoPoint`を作成します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="73d4f-126">例 :</span><span class="sxs-lookup"><span data-stu-id="73d4f-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="73d4f-127">[FromBody] を使用する</span><span class="sxs-lookup"><span data-stu-id="73d4f-127">Using [FromBody]</span></span>

<span data-ttu-id="73d4f-128">Web API で要求本文から単純型を強制的に読み取るには、 **[Frombody]** 属性をパラメーターに追加します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="73d4f-129">この例では、Web API はメディアタイプフォーマッタを使用して、要求本文から*名前*の値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="73d4f-130">クライアント要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="73d4f-131">パラメーターに [FromBody] がある場合、Web API は Content-type ヘッダーを使用してフォーマッタを選択します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="73d4f-132">この例では、コンテンツタイプは application/json&quot; &quot;、要求本文は JSON オブジェクトではなく生の JSON 文字列です。</span><span class="sxs-lookup"><span data-stu-id="73d4f-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="73d4f-133">メッセージ本文からの読み取りは、最大で1つのパラメーターで許可されます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="73d4f-134">これは機能しません。</span><span class="sxs-lookup"><span data-stu-id="73d4f-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="73d4f-135">このルールの理由は、要求本文は、一度しか読み取ることができないバッファーストリームに格納されている可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="73d4f-136">型コンバーター</span><span class="sxs-lookup"><span data-stu-id="73d4f-136">Type Converters</span></span>

<span data-ttu-id="73d4f-137">Web API によって、クラスを単純型として扱うことができます (これにより、Web API は、 **TypeConverter**を作成し、文字列変換を提供することで、URI からのバインドを試行します)。</span><span class="sxs-lookup"><span data-stu-id="73d4f-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="73d4f-138">次のコードは、地理的ポイントを表す `GeoPoint` クラス、および文字列から `GeoPoint` インスタンスに変換する**TypeConverter**を示しています。</span><span class="sxs-lookup"><span data-stu-id="73d4f-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="73d4f-139">`GeoPoint` クラスは、型コンバーターを指定するために、 **[TypeConverter]** 属性で修飾されます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="73d4f-140">(この例は、Mike ストールのブログ投稿で、 [MVC/WebAPI のアクションシグネチャのカスタムオブジェクトにバインドする方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)を示していました)。</span><span class="sxs-lookup"><span data-stu-id="73d4f-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="73d4f-141">これで、Web API は `GeoPoint` を単純型として扱います。つまり、URI から `GeoPoint` パラメーターをバインドしようとします。</span><span class="sxs-lookup"><span data-stu-id="73d4f-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="73d4f-142">パラメーターに **[Fromuri]** を含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="73d4f-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="73d4f-143">クライアントは、次のような URI を使用してメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="73d4f-144">モデル バインダー</span><span class="sxs-lookup"><span data-stu-id="73d4f-144">Model Binders</span></span>

<span data-ttu-id="73d4f-145">型コンバーターよりも柔軟なオプションは、カスタムモデルバインダーを作成することです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="73d4f-146">モデルバインダーを使用すると、HTTP 要求、アクションの説明、ルートデータからの生の値などにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="73d4f-147">モデルバインダーを作成するには、 **Imodelbinder**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="73d4f-148">このインターフェイスは、 **Bindmodel**という1つのメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="73d4f-149">`GeoPoint` オブジェクトのモデルバインダーを次に示します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="73d4f-150">モデルバインダーは、*値プロバイダー*から生の入力値を取得します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="73d4f-151">この設計では、次の2つの異なる関数を分離します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="73d4f-152">値プロバイダーは、HTTP 要求を受け取り、キーと値のペアのディクショナリを設定します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="73d4f-153">モデルバインダーは、このディクショナリを使用してモデルにデータを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="73d4f-154">Web API の既定値プロバイダーは、ルートデータとクエリ文字列から値を取得します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="73d4f-155">たとえば、URI が `http://localhost/api/values/1?location=48,-122`場合、値プロバイダーは次のキーと値のペアを作成します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="73d4f-156">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="73d4f-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="73d4f-157">location = &quot;48122&quot;</span><span class="sxs-lookup"><span data-stu-id="73d4f-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="73d4f-158">(既定のルートテンプレートは &quot;api/{controller}/{id}&quot;と想定しています)。</span><span class="sxs-lookup"><span data-stu-id="73d4f-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="73d4f-159">バインドするパラメーターの名前は、 **ModelName**プロパティに格納されます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="73d4f-160">モデルバインダーは、ディクショナリ内のこの値を持つキーを検索します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="73d4f-161">値が存在し、`GeoPoint`に変換できる場合、モデルバインダーは、バインドされた値を**ModelBindingContext**プロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="73d4f-162">モデルバインダーは単純型変換に限定されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="73d4f-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="73d4f-163">この例では、モデルバインダーは、まず既知の場所のテーブルを検索し、失敗した場合は型変換を使用します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="73d4f-164">**モデルバインダーの設定**</span><span class="sxs-lookup"><span data-stu-id="73d4f-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="73d4f-165">モデルバインダーを設定するには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="73d4f-166">最初に、パラメーターに **[Modelbinder]** 属性を追加できます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="73d4f-167">また、 **[Modelbinder]** 属性を型に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="73d4f-168">Web API は、指定されたモデルバインダーをその型のすべてのパラメーターに使用します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="73d4f-169">最後に、 **Httpconfiguration**にモデルバインダープロバイダーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="73d4f-170">モデルバインダープロバイダーは、単にモデルバインダーを作成するファクトリクラスです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="73d4f-171">プロバイダーを作成するには、 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)クラスから派生させます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="73d4f-172">ただし、モデルバインダーが1つの型を処理する場合は、この目的のために設計された組み込みの**SimpleModelBinderProvider**を使用する方が簡単です。</span><span class="sxs-lookup"><span data-stu-id="73d4f-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="73d4f-173">この方法を次のコードに示します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="73d4f-174">モデルバインディングプロバイダーを使用する場合は、 **[modelbinder]** 属性をパラメーターに追加して、メディアタイプのフォーマッタではなくモデルバインダーを使用する必要があることを Web API に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="73d4f-175">ただし、ここでは、属性でモデルバインダーの種類を指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="73d4f-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="73d4f-176">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="73d4f-176">Value Providers</span></span>

<span data-ttu-id="73d4f-177">ここでは、モデルバインダーが値プロバイダーから値を取得することを説明しました。</span><span class="sxs-lookup"><span data-stu-id="73d4f-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="73d4f-178">カスタム値プロバイダーを作成するには、 **Ivalueprovider**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="73d4f-179">要求の cookie から値をプルする例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="73d4f-180">また、 **Valueproviderfactory**クラスから派生することによって、値プロバイダーファクトリを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="73d4f-181">次のように、 **Httpconfiguration**に値プロバイダーファクトリを追加します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="73d4f-182">Web API はすべての値プロバイダーを結合するため、モデルバインダーが**valueprovider. GetValue**を呼び出すと、モデルバインダーは、その値を生成できる最初の値プロバイダーから値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="73d4f-183">または、次のように、 **valueprovider**属性を使用して、値プロバイダーファクトリをパラメーターレベルで設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="73d4f-184">これは、指定された値プロバイダーファクトリでモデルバインディングを使用するように Web API に指示します。他の登録済みの値プロバイダーは使用しません。</span><span class="sxs-lookup"><span data-stu-id="73d4f-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="73d4f-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="73d4f-185">HttpParameterBinding</span></span>

<span data-ttu-id="73d4f-186">モデルバインダーは、より一般的なメカニズムの特定のインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="73d4f-187">**[Modelbinder]** 属性を確認すると、抽象**parameterbindingattribute**クラスから派生したことがわかります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="73d4f-188">このクラスは、 **Httpparameterbinding**オブジェクトを返す、 **getbinding**という1つのメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="73d4f-189">**Httpparameterbinding**は、パラメーターを値にバインドする役割を担います。</span><span class="sxs-lookup"><span data-stu-id="73d4f-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="73d4f-190">**[Modelbinder]** の場合、属性は、 **imodelbinder**を使用して実際のバインドを実行する**httpparameterbinding**実装を返します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="73d4f-191">独自の**Httpparameterbinding**を実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="73d4f-192">たとえば、要求で `if-match` と `if-none-match` ヘッダーから Etag を取得するとします。</span><span class="sxs-lookup"><span data-stu-id="73d4f-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="73d4f-193">まず、Etag を表すクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="73d4f-194">また、`if-match` ヘッダーまたは `if-none-match` ヘッダーから ETag を取得するかどうかを示す列挙も定義します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="73d4f-195">次に示すのは、目的のヘッダーから ETag を取得し、それを ETag 型のパラメーターにバインドする**Httpparameterbinding**です。</span><span class="sxs-lookup"><span data-stu-id="73d4f-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="73d4f-196">**Executebindingasync**メソッドは、バインディングを行います。</span><span class="sxs-lookup"><span data-stu-id="73d4f-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="73d4f-197">このメソッド内で、 **Httpactioncontext**の**actionargument**ディクショナリにバインドされたパラメーター値を追加します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-198">**Executebindingasync**メソッドが要求メッセージの本文を読み取る場合は、によって**true が返されるよう**にします。</span><span class="sxs-lookup"><span data-stu-id="73d4f-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="73d4f-199">要求本文は、1回だけ読み取ることができるバッファーなしのストリームである可能性があるため、Web API は、最大1つのバインディングでメッセージ本文を読み取ることができる規則を適用します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="73d4f-200">カスタム**Httpparameterbinding**を適用するには、 **parameterbindingattribute**から派生した属性を定義します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="73d4f-201">`ETagParameterBinding`には、2つの属性を定義します。1つは `if-match` ヘッダー用で、もう1つは `if-none-match` ヘッダー用です。</span><span class="sxs-lookup"><span data-stu-id="73d4f-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="73d4f-202">どちらも抽象基本クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="73d4f-203">`[IfNoneMatch]` 属性を使用するコントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="73d4f-204">**Parameterbindingattribute**に加えて、カスタム**httpparameterbinding**を追加するための別のフックもあります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="73d4f-205">**Httpconfiguration**オブジェクトでは、 **Parameterbindingrules**種類の匿名関数 (**Httpparameterdescriptor** -&gt; **httpparameterbinding**) のコレクションです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="73d4f-206">たとえば、GET メソッドの任意の ETag パラメーターが `if-none-match`で `ETagParameterBinding` を使用するという規則を追加できます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="73d4f-207">関数は、バインドが適用されないパラメーターの `null` を返します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="73d4f-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="73d4f-208">IActionValueBinder</span></span>

<span data-ttu-id="73d4f-209">パラメーターバインドプロセス全体は、プラグ可能なサービスである**Iactionvaluebinder**によって制御されます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="73d4f-210">**Iactionvaluebinder**の既定の実装では、次のことが実行されます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="73d4f-211">パラメーターで**Parameterbindingattribute**を探します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="73d4f-212">これには、 **[Frombody]** 、 **[frombody]** 、 **[modelbinder]** 、またはカスタム属性が含まれます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="73d4f-213">それ以外の場合は、 **Httpconfiguration. ParameterBindingRules** 、null 以外の**httpparameterbinding**を返す関数を探します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="73d4f-214">それ以外の場合は、前に説明した既定の規則を使用します。</span><span class="sxs-lookup"><span data-stu-id="73d4f-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="73d4f-215">パラメーターの型が "simple" であるか、型コンバーターを持っている場合は、URI からバインドします。</span><span class="sxs-lookup"><span data-stu-id="73d4f-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="73d4f-216">これは、パラメーターに **[Fromuri]** 属性を配置することと同じです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="73d4f-217">それ以外の場合は、メッセージ本文からパラメーターを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="73d4f-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="73d4f-218">これは、パラメーターに **[Frombody]** を配置することと同じです。</span><span class="sxs-lookup"><span data-stu-id="73d4f-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="73d4f-219">必要に応じて、 **Iactionvaluebinder**サービス全体をカスタム実装に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="73d4f-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73d4f-220">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="73d4f-220">Additional Resources</span></span>

[<span data-ttu-id="73d4f-221">カスタムパラメーターバインディングのサンプル</span><span class="sxs-lookup"><span data-stu-id="73d4f-221">Custom Parameter Binding Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

<span data-ttu-id="73d4f-222">Mike ストールは、Web API パラメーターのバインドに関する一連のブログ投稿を作成しました。</span><span class="sxs-lookup"><span data-stu-id="73d4f-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="73d4f-223">Web API がパラメーターのバインドを行う方法</span><span class="sxs-lookup"><span data-stu-id="73d4f-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="73d4f-224">Web API の MVC スタイルパラメーターのバインド</span><span class="sxs-lookup"><span data-stu-id="73d4f-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="73d4f-225">MVC/Web API でアクションシグネチャのカスタムオブジェクトにバインドする方法</span><span class="sxs-lookup"><span data-stu-id="73d4f-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="73d4f-226">Web API でカスタム値プロバイダーを作成する方法</span><span class="sxs-lookup"><span data-stu-id="73d4f-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="73d4f-227">内部の Web API パラメーターのバインド</span><span class="sxs-lookup"><span data-stu-id="73d4f-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
