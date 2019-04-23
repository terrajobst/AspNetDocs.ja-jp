---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: パラメーター バインドでは、ASP.NET Web API - ASP.NET 4.x
author: MikeWasson
description: Web API がパラメーターをバインドする方法と ASP.NET でバインディングのプロセスをカスタマイズする方法について説明します 4.x です。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f121f12ce689a079412bbd5392fde4fea863ff1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59401973"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="4338f-103">ASP.NET Web API のパラメーター バインド</span><span class="sxs-lookup"><span data-stu-id="4338f-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="4338f-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4338f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4338f-105">この記事では、Web API が、パラメーターをバインドする方法と、バインディング プロセスをカスタマイズする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4338f-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="4338f-106">呼ばれるプロセス パラメーターの値を設定する必要があります Web API コント ローラーのメソッドを呼び出す、*バインド*します。</span><span class="sxs-lookup"><span data-stu-id="4338f-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span> 

<span data-ttu-id="4338f-107">既定では、Web API は、次の規則を使用して、パラメーターをバインドします。</span><span class="sxs-lookup"><span data-stu-id="4338f-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="4338f-108">パラメーターが「単純な」型の場合、Web API は、URI から値を取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="4338f-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="4338f-109">単純な種類には、.NET[プリミティブ型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)(**int**、 **bool**、**二重**など)、plus **TimeSpan**、 **DateTime**、 **Guid**、 **decimal**、および**文字列**、 *plus*任意文字列から変換できる型コンバーターを使用して入力します。</span><span class="sxs-lookup"><span data-stu-id="4338f-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="4338f-110">(詳細については後での型コンバーター。)</span><span class="sxs-lookup"><span data-stu-id="4338f-110">(More about type converters later.)</span></span>
- <span data-ttu-id="4338f-111">複合型、Web API では、メッセージ本文から値を読み取るしようとして、使用して、[メディア タイプ フォーマッタ](media-formatters.md)します。</span><span class="sxs-lookup"><span data-stu-id="4338f-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="4338f-112">たとえば、一般的な Web API コント ローラー メソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4338f-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="4338f-113">*Id*パラメーターは、&quot;単純&quot;型であるため、Web API は要求 URI の値を取得しようとしています。</span><span class="sxs-lookup"><span data-stu-id="4338f-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="4338f-114">*項目*パラメーターが、複雑な型、Web API は、メディアの種類のフォーマッタを使用して、要求本文から値を読み取るようにします。</span><span class="sxs-lookup"><span data-stu-id="4338f-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="4338f-115">URI から値を取得するには、Web API は、ルート データと、URI クエリ文字列で検索します。</span><span class="sxs-lookup"><span data-stu-id="4338f-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="4338f-116">ルーティング システムは、URI を解析し、ルートに一致する場合は、ルート データが設定されます。</span><span class="sxs-lookup"><span data-stu-id="4338f-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="4338f-117">詳細については、次を参照してください。[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)します。</span><span class="sxs-lookup"><span data-stu-id="4338f-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="4338f-118">この記事の残りの部分で、モデル バインディング プロセスをカスタマイズする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="4338f-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="4338f-119">複合型は、ただし、可能であれば、メディア タイプ フォーマッタを使用してを考慮します。</span><span class="sxs-lookup"><span data-stu-id="4338f-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="4338f-120">HTTP の重要な原則は、リソースは、コンテンツ ネゴシエーションを使用して、リソースの表現を指定する、メッセージの本文で送信されます。</span><span class="sxs-lookup"><span data-stu-id="4338f-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="4338f-121">メディア タイプ フォーマッタは、正確に、この目的用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="4338f-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="4338f-122">[FromUri] を使用します。</span><span class="sxs-lookup"><span data-stu-id="4338f-122">Using [FromUri]</span></span>

<span data-ttu-id="4338f-123">URI から複合型を読み取る Web API を強制的には、追加、 **[FromUri]** 属性をパラメーター。</span><span class="sxs-lookup"><span data-stu-id="4338f-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="4338f-124">次の例では、定義、`GeoPoint`と共に取得するコント ローラー メソッドの型、 `GeoPoint` URI から。</span><span class="sxs-lookup"><span data-stu-id="4338f-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="4338f-125">クライアントは、クエリ文字列で、緯度と経度の値を配置することができ、Web API を構築を使用してそれらが、`GeoPoint`します。</span><span class="sxs-lookup"><span data-stu-id="4338f-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="4338f-126">例えば:</span><span class="sxs-lookup"><span data-stu-id="4338f-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="4338f-127">[FromBody] を使用します。</span><span class="sxs-lookup"><span data-stu-id="4338f-127">Using [FromBody]</span></span>

<span data-ttu-id="4338f-128">要求本文から単純型を読み取る Web API を強制的には、追加、 **[FromBody]** パラメーターに属性します。</span><span class="sxs-lookup"><span data-stu-id="4338f-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="4338f-129">この例では、Web API は、の値を読み取るメディア タイプ フォーマッタを使用が*名前*要求本文から。</span><span class="sxs-lookup"><span data-stu-id="4338f-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="4338f-130">クライアント要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4338f-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="4338f-131">パラメーターでは、[FromBody] が持つ、Web API は、Content-type ヘッダーを使用して、フォーマッタを選択します。</span><span class="sxs-lookup"><span data-stu-id="4338f-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="4338f-132">この例では、コンテンツの種類は&quot;、application/json&quot;要求本文で、未加工の JSON 文字列 (JSON オブジェクトではありません)。</span><span class="sxs-lookup"><span data-stu-id="4338f-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="4338f-133">メッセージ本文から読み取る最大で 1 つのパラメーターが許可されます。</span><span class="sxs-lookup"><span data-stu-id="4338f-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="4338f-134">したがってこれは機能しません。</span><span class="sxs-lookup"><span data-stu-id="4338f-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="4338f-135">このルールの理由では、1 回だけ読み取り可能な非バッファー ストリームで、要求本文を格納する可能性があること。</span><span class="sxs-lookup"><span data-stu-id="4338f-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="4338f-136">型コンバーター</span><span class="sxs-lookup"><span data-stu-id="4338f-136">Type Converters</span></span>

<span data-ttu-id="4338f-137">(Web API は、URI からバインドを試みます) するために、単純型としてクラスを扱う Web API を作成して行うことができます、 **TypeConverter**と文字列の変換を提供します。</span><span class="sxs-lookup"><span data-stu-id="4338f-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="4338f-138">次のコードは、 `GeoPoint` 、地理的ポイントを表すクラスと**TypeConverter**の文字列に変換する`GeoPoint`インスタンス。</span><span class="sxs-lookup"><span data-stu-id="4338f-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="4338f-139">`GeoPoint`クラスがで修飾された、 **[TypeConverter]** 属性を型コンバーターを指定します。</span><span class="sxs-lookup"><span data-stu-id="4338f-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="4338f-140">(この例は、Mike Stall のブログの投稿によって考え出されました[MVC/WebAPI のアクション シグネチャでのカスタム オブジェクトにバインドする方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx))。</span><span class="sxs-lookup"><span data-stu-id="4338f-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="4338f-141">Web API を扱うようになりました`GeoPoint`として単純型、つまりバインドを試みます`GeoPoint`URI からのパラメーター。</span><span class="sxs-lookup"><span data-stu-id="4338f-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="4338f-142">含める必要はありません **[FromUri]** パラメーターにします。</span><span class="sxs-lookup"><span data-stu-id="4338f-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="4338f-143">クライアントは、このような URI を持つメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="4338f-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="4338f-144">モデル バインダー</span><span class="sxs-lookup"><span data-stu-id="4338f-144">Model Binders</span></span>

<span data-ttu-id="4338f-145">型コンバーターよりもより柔軟なオプションでは、カスタム モデル バインダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="4338f-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="4338f-146">モデル バインダーを使用ルート データからなど、HTTP 要求、アクションの説明および生の値にアクセス権があります。</span><span class="sxs-lookup"><span data-stu-id="4338f-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="4338f-147">モデル バインダーを作成するには、実装、 **IModelBinder**インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="4338f-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="4338f-148">このインターフェイスは、1 つのメソッドを定義します**BindModel**:。</span><span class="sxs-lookup"><span data-stu-id="4338f-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="4338f-149">ここでは、モデル バインダーを`GeoPoint`オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="4338f-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="4338f-150">モデル バインダーからの生の入力値を取得する、*値プロバイダー*します。</span><span class="sxs-lookup"><span data-stu-id="4338f-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="4338f-151">この設計では、2 つの異なる機能を分離します。</span><span class="sxs-lookup"><span data-stu-id="4338f-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="4338f-152">値プロバイダーは、HTTP 要求を受け取り、キー/値ペアのディクショナリを設定します。</span><span class="sxs-lookup"><span data-stu-id="4338f-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="4338f-153">モデル バインダーでは、このディクショナリを使用してモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="4338f-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="4338f-154">Web API の既定値のプロバイダーは、ルート データとクエリ文字列から値を取得します。</span><span class="sxs-lookup"><span data-stu-id="4338f-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="4338f-155">たとえば、URI は、 `http://localhost/api/values/1?location=48,-122`、値プロバイダーが次のキー/値ペアを作成します。</span><span class="sxs-lookup"><span data-stu-id="4338f-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="4338f-156">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="4338f-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="4338f-157">location = &quot;48,122&quot;</span><span class="sxs-lookup"><span data-stu-id="4338f-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="4338f-158">(これは既定のルート テンプレートを前提に話&quot;api/{controller}/{id}&quot;)。</span><span class="sxs-lookup"><span data-stu-id="4338f-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="4338f-159">バインドするパラメーターの名前が格納されている、 **ModelBindingContext.ModelName**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="4338f-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="4338f-160">モデル バインダー ディクショナリ内でこの値を持つキーを探します。</span><span class="sxs-lookup"><span data-stu-id="4338f-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="4338f-161">値が存在しに変換できる場合、 `GeoPoint`、モデル バインダーにバインドされている値を割り当てます、 **ModelBindingContext.Model**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="4338f-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="4338f-162">モデル バインダーは単純型の変換に限定されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4338f-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="4338f-163">この例では、モデル バインダーは、既知の場所のテーブルで最初にし、型変換を使用して失敗した場合。</span><span class="sxs-lookup"><span data-stu-id="4338f-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="4338f-164">**モデル バインダーの設定**</span><span class="sxs-lookup"><span data-stu-id="4338f-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="4338f-165">モデル バインダーを設定するいくつかの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="4338f-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="4338f-166">最初に、追加、 **[拡大する ModelBinder]** 属性をパラメーター。</span><span class="sxs-lookup"><span data-stu-id="4338f-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="4338f-167">追加することも、 **[拡大する ModelBinder]** 属性を型にします。</span><span class="sxs-lookup"><span data-stu-id="4338f-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="4338f-168">Web API は、その型のすべてのパラメーターの指定したモデル バインダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="4338f-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="4338f-169">最後にモデル バインダー プロバイダーを追加することができます、 **HttpConfiguration**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="4338f-170">モデル バインダー プロバイダーは、単に、モデル バインダーを作成するファクトリ クラスです。</span><span class="sxs-lookup"><span data-stu-id="4338f-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="4338f-171">派生することによって、プロバイダーを作成することができます、 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)クラス。</span><span class="sxs-lookup"><span data-stu-id="4338f-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="4338f-172">ただし、モデル バインダーは、1 つの型を処理する場合は、組み込みの使いやすい**SimpleModelBinderProvider**、これはこの目的に設計されています。</span><span class="sxs-lookup"><span data-stu-id="4338f-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="4338f-173">この方法を次のコードに示します。</span><span class="sxs-lookup"><span data-stu-id="4338f-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="4338f-174">モデル バインド プロバイダーでは、使用する必要がありますを追加、 **[拡大する ModelBinder]** 属性をモデル バインダーとメディア タイプ フォーマッタではないのどちらを使用することを Web API に指示する、パラメーター。</span><span class="sxs-lookup"><span data-stu-id="4338f-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="4338f-175">これで、属性でモデル バインダーの型を指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4338f-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="4338f-176">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="4338f-176">Value Providers</span></span>

<span data-ttu-id="4338f-177">モデル バインダーが値プロバイダーから値を取得することをお話しします。</span><span class="sxs-lookup"><span data-stu-id="4338f-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="4338f-178">カスタム値プロバイダーを作成するには、実装、 **IValueProvider**インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="4338f-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="4338f-179">要求の cookie の値を取得する例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4338f-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="4338f-180">派生することによって、値プロバイダー ファクトリを作成する必要も、 **ValueProviderFactory**クラス。</span><span class="sxs-lookup"><span data-stu-id="4338f-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="4338f-181">追加する値プロバイダー ファクトリ、 **HttpConfiguration**次のようにします。</span><span class="sxs-lookup"><span data-stu-id="4338f-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="4338f-182">Web API がすべて、値プロバイダーのために合成モデル バインダーを呼び出すと**ValueProvider.GetValue**、モデル バインダーは、生成できる最初の値プロバイダーから値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="4338f-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="4338f-183">使用して、パラメーターのレベルで、値プロバイダー ファクトリを設定することができます、 **ValueProvider**属性は、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="4338f-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="4338f-184">これは、Web API で、指定した値プロバイダー ファクトリ モデル バインドを使用して、その他の登録済みの値プロバイダーを使用しないことを示します。</span><span class="sxs-lookup"><span data-stu-id="4338f-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="4338f-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="4338f-185">HttpParameterBinding</span></span>

<span data-ttu-id="4338f-186">モデル バインダーは、特定のインスタンスの全般的なメカニズムです。</span><span class="sxs-lookup"><span data-stu-id="4338f-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="4338f-187">確認する場合、 **[拡大する ModelBinder]** 属性が表示されます、抽象型から派生すること**ParameterBindingAttribute**クラス。</span><span class="sxs-lookup"><span data-stu-id="4338f-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="4338f-188">このクラスは、1 つのメソッドを定義します**GetBinding**、返された、 **HttpParameterBinding**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="4338f-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="4338f-189">**HttpParameterBinding**パラメーターを値にバインドを担当します。</span><span class="sxs-lookup"><span data-stu-id="4338f-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="4338f-190">場合に **[拡大する ModelBinder]**、属性を返します、 **HttpParameterBinding**を使用して実装する**IModelBinder**実際のバインドを実行します。</span><span class="sxs-lookup"><span data-stu-id="4338f-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="4338f-191">独自に実装することも**HttpParameterBinding**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="4338f-192">たとえばから Etag を取得する`if-match`と`if-none-match`要求のヘッダー。</span><span class="sxs-lookup"><span data-stu-id="4338f-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="4338f-193">Etag を表すクラスの定義から始めます。</span><span class="sxs-lookup"><span data-stu-id="4338f-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="4338f-194">ETag を取得するかどうかを示す列挙体も定義します、`if-match`ヘッダーまたは`if-none-match`ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="4338f-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="4338f-195">ここでは、 **HttpParameterBinding** ETag 型のパラメーターにバインドされますを目的のヘッダーから ETag を取得します。</span><span class="sxs-lookup"><span data-stu-id="4338f-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="4338f-196">**ExecuteBindingAsync**メソッドは、バインドします。</span><span class="sxs-lookup"><span data-stu-id="4338f-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="4338f-197">このメソッド内にバインドされたパラメーター値を追加、 **ActionArgument**ディクショナリで、 **HttpActionContext**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="4338f-198">場合、 **ExecuteBindingAsync**メソッドは、要求メッセージの本文を読み取り、上書き、 **WillReadBody**プロパティが true を返します。</span><span class="sxs-lookup"><span data-stu-id="4338f-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="4338f-199">要求本文には、読み取りしか実行 1 回、Web API 規則を適用する 1 つだけにバインドするようにするバッファリングされていないストリームは、メッセージ本文を読み取ることができます可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4338f-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>


<span data-ttu-id="4338f-200">カスタムを適用する**HttpParameterBinding**から派生した属性を定義する**ParameterBindingAttribute**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="4338f-201">`ETagParameterBinding`、1 つずつ、2 つの属性を定義します`if-match`ヘッダーと 1 つずつ`if-none-match`ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="4338f-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="4338f-202">抽象基本クラスから派生させます。</span><span class="sxs-lookup"><span data-stu-id="4338f-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="4338f-203">使用するコント ローラー メソッドを次に示します、`[IfNoneMatch]`属性。</span><span class="sxs-lookup"><span data-stu-id="4338f-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="4338f-204">それに**ParameterBindingAttribute**、カスタムを追加するための別のフック**HttpParameterBinding**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="4338f-205">**HttpConfiguration**オブジェクト、 **ParameterBindingRules**プロパティが型の匿名関数のコレクション (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**)。</span><span class="sxs-lookup"><span data-stu-id="4338f-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="4338f-206">たとえば、ETag のパラメーターを GET メソッドを使用するルールを追加できます`ETagParameterBinding`で`if-none-match`:</span><span class="sxs-lookup"><span data-stu-id="4338f-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="4338f-207">関数が返す必要があります`null`のパラメーターのバインドは適用されません。</span><span class="sxs-lookup"><span data-stu-id="4338f-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="4338f-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="4338f-208">IActionValueBinder</span></span>

<span data-ttu-id="4338f-209">パラメーター バインディング プロセス全体が、プラグ可能なサービスによって制御される**IActionValueBinder**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="4338f-210">既定の実装**IActionValueBinder**は次の処理します。</span><span class="sxs-lookup"><span data-stu-id="4338f-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="4338f-211">探して、 **ParameterBindingAttribute**パラメーターにします。</span><span class="sxs-lookup"><span data-stu-id="4338f-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="4338f-212">これが含まれています **[FromBody]**、 **[FromUri]**、および **[拡大する ModelBinder]**、またはカスタム属性。</span><span class="sxs-lookup"><span data-stu-id="4338f-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="4338f-213">それ以外の場合、ファイルの場所**HttpConfiguration.ParameterBindingRules**を null 以外を返す関数の**HttpParameterBinding**します。</span><span class="sxs-lookup"><span data-stu-id="4338f-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="4338f-214">それ以外の場合、先ほど説明した既定の規則を使用します。</span><span class="sxs-lookup"><span data-stu-id="4338f-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="4338f-215">パラメーターの型が「簡単」した場合、または型コンバーターが場合は、URI からバインドします。</span><span class="sxs-lookup"><span data-stu-id="4338f-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="4338f-216">これは配置することに相当、 **[FromUri]** パラメーターの属性。</span><span class="sxs-lookup"><span data-stu-id="4338f-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="4338f-217">それ以外の場合、メッセージ本文からパラメーターの読み取りを再試行してください。</span><span class="sxs-lookup"><span data-stu-id="4338f-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="4338f-218">これは配置することに相当 **[FromBody]** パラメーターにします。</span><span class="sxs-lookup"><span data-stu-id="4338f-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="4338f-219">全体を置き換えることができる場合は、 **IActionValueBinder**カスタム実装サービス。</span><span class="sxs-lookup"><span data-stu-id="4338f-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4338f-220">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="4338f-220">Additional Resources</span></span>

[<span data-ttu-id="4338f-221">カスタム パラメーター バインドのサンプル</span><span class="sxs-lookup"><span data-stu-id="4338f-221">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="4338f-222">Mike Stall は、Web API のパラメーター バインディングの適切な一連のブログを作成しました。</span><span class="sxs-lookup"><span data-stu-id="4338f-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="4338f-223">どのように Web API は、パラメーターのバインド</span><span class="sxs-lookup"><span data-stu-id="4338f-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="4338f-224">Web API の MVC スタイルのパラメーターのバインド</span><span class="sxs-lookup"><span data-stu-id="4338f-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="4338f-225">MVC または Web API でのアクション シグネチャでのカスタム オブジェクトにバインドする方法</span><span class="sxs-lookup"><span data-stu-id="4338f-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="4338f-226">Web API でカスタム値プロバイダーを作成する方法</span><span class="sxs-lookup"><span data-stu-id="4338f-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="4338f-227">内部的には web API パラメーターのバインド</span><span class="sxs-lookup"><span data-stu-id="4338f-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
