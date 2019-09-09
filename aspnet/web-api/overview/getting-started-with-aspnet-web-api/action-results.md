---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2 でのアクションの結果-ASP.NET 4.x
author: MikeWasson
description: ASP.NET Web API がコントローラーアクションから ASP.NET 4.x の HTTP 応答メッセージに戻り値を変換する方法について説明します。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 1eaaf8e87168096683212fa66d3ddf415ad6b22b
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000715"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="3a7a2-103">Web API 2 のアクションの結果</span><span class="sxs-lookup"><span data-stu-id="3a7a2-103">Action Results in Web API 2</span></span>

<span data-ttu-id="3a7a2-104">このトピックでは、ASP.NET Web API がコントローラーアクションからの戻り値を HTTP 応答メッセージに変換する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="3a7a2-105">Web API コントローラーアクションは、次のいずれかを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="3a7a2-106">void</span><span class="sxs-lookup"><span data-stu-id="3a7a2-106">void</span></span>
2. <span data-ttu-id="3a7a2-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="3a7a2-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="3a7a2-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="3a7a2-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="3a7a2-109">その他の型</span><span class="sxs-lookup"><span data-stu-id="3a7a2-109">Some other type</span></span>

<span data-ttu-id="3a7a2-110">これらのどちらが返されるかに応じて、Web API は異なるメカニズムを使用して HTTP 応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="3a7a2-111">戻り値の型</span><span class="sxs-lookup"><span data-stu-id="3a7a2-111">Return type</span></span> | <span data-ttu-id="3a7a2-112">Web API による応答の作成方法</span><span class="sxs-lookup"><span data-stu-id="3a7a2-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="3a7a2-113">void</span><span class="sxs-lookup"><span data-stu-id="3a7a2-113">void</span></span> | <span data-ttu-id="3a7a2-114">空の204を返す (コンテンツなし)</span><span class="sxs-lookup"><span data-stu-id="3a7a2-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="3a7a2-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="3a7a2-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="3a7a2-116">HTTP 応答メッセージに直接変換します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="3a7a2-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="3a7a2-117">**IHttpActionResult**</span></span> | <span data-ttu-id="3a7a2-118">**HttpResponseMessage**を作成して HTTP 応答メッセージに変換するには、 **executeasync**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="3a7a2-119">その他の型</span><span class="sxs-lookup"><span data-stu-id="3a7a2-119">Other type</span></span> | <span data-ttu-id="3a7a2-120">シリアル化された戻り値を応答本文に書き込みます。200 (OK) を返します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="3a7a2-121">このトピックの残りの部分では、各オプションについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="3a7a2-122">void</span><span class="sxs-lookup"><span data-stu-id="3a7a2-122">void</span></span>

<span data-ttu-id="3a7a2-123">戻り値の型が`void`の場合、Web API は、ステータスコード 204 (コンテンツなし) の空の HTTP 応答を単純に返します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="3a7a2-124">コントローラーの例:</span><span class="sxs-lookup"><span data-stu-id="3a7a2-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="3a7a2-125">HTTP 応答:</span><span class="sxs-lookup"><span data-stu-id="3a7a2-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="3a7a2-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="3a7a2-126">HttpResponseMessage</span></span>

<span data-ttu-id="3a7a2-127">アクションが[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)を返す場合、Web API は、 **HttpResponseMessage**オブジェクトのプロパティを使用して応答を設定し、戻り値を直接 HTTP 応答メッセージに変換します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="3a7a2-128">このオプションを使用すると、応答メッセージを細かく制御できます。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="3a7a2-129">たとえば、次のコントローラーアクションは Cache-control ヘッダーを設定します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="3a7a2-130">応答 :</span><span class="sxs-lookup"><span data-stu-id="3a7a2-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="3a7a2-131">ドメインモデルを**CreateResponse**メソッドに渡すと、Web API は[メディアフォーマッタ](../formats-and-model-binding/media-formatters.md)を使用して、シリアル化されたモデルを応答本文に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="3a7a2-132">Web API では、要求の Accept ヘッダーを使用してフォーマッタを選択します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="3a7a2-133">詳細については、「[コンテンツネゴシエーション](../formats-and-model-binding/content-negotiation.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="3a7a2-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="3a7a2-134">IHttpActionResult</span></span>

<span data-ttu-id="3a7a2-135">**Ihttpactionresult**インターフェイスは、Web API 2 で導入されました。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="3a7a2-136">基本的には、 **HttpResponseMessage**ファクトリを定義します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="3a7a2-137">**Ihttpactionresult**インターフェイスを使用すると、次のような利点があります。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="3a7a2-138">コントローラーの[単体テスト](../testing-and-debugging/unit-testing-controllers-in-web-api.md)を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="3a7a2-139">HTTP 応答を作成するための共通のロジックを別のクラスに移動します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="3a7a2-140">応答を構築するための下位レベルの詳細を非表示にすることにより、コントローラーアクションの目的を明確にします。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="3a7a2-141">**Ihttpactionresult**には、 **executeasync**という1つのメソッドが含まれています。このメソッドは、非同期的に**HttpResponseMessage**インスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="3a7a2-142">コントローラーアクションが**Ihttpactionresult**を返す場合、Web API は**executeasync**メソッドを呼び出して**HttpResponseMessage**を作成します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="3a7a2-143">次に、 **HttpResponseMessage**を HTTP 応答メッセージに変換します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="3a7a2-144">次に示すのは、プレーンテキスト応答を作成する**Ihttpactionresult**の単純な実装です。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="3a7a2-145">コントローラーアクションの例:</span><span class="sxs-lookup"><span data-stu-id="3a7a2-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="3a7a2-146">応答 :</span><span class="sxs-lookup"><span data-stu-id="3a7a2-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="3a7a2-147">多くの場合、名前空間に定義されている**Ihttpactionresult**実装を使用 **[します。](https://msdn.microsoft.com/library/system.web.http.results.aspx)**</span><span class="sxs-lookup"><span data-stu-id="3a7a2-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="3a7a2-148">**ApiController**クラスは、これらの組み込みアクションの結果を返すヘルパーメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="3a7a2-149">次の例では、要求が既存の製品 ID と一致しない場合、コントローラーは[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)を呼び出して 404 (見つかりません) 応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="3a7a2-150">それ以外の場合、コントローラーは ApiController を呼び出します。これにより、製品を含む 200 (OK) の応答が作成され[ます。](https://msdn.microsoft.com/library/dn314591.aspx)</span><span class="sxs-lookup"><span data-stu-id="3a7a2-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="3a7a2-151">その他の戻り値の型</span><span class="sxs-lookup"><span data-stu-id="3a7a2-151">Other Return Types</span></span>

<span data-ttu-id="3a7a2-152">その他のすべての戻り値の型では、Web API は[メディアフォーマッタ](../formats-and-model-binding/media-formatters.md)を使用して戻り値をシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="3a7a2-153">Web API は、シリアル化された値を応答本文に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="3a7a2-154">応答状態コードは 200 (OK) です。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="3a7a2-155">この方法の欠点は、404などのエラーコードを直接返すことができないことです。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="3a7a2-156">ただし、エラーコードの**HttpResponseException**をスローすることはできます。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="3a7a2-157">詳細については、「 [ASP.NET Web API での例外処理](../error-handling/exception-handling.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="3a7a2-158">Web API では、要求の Accept ヘッダーを使用してフォーマッタを選択します。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="3a7a2-159">詳細については、「[コンテンツネゴシエーション](../formats-and-model-binding/content-negotiation.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3a7a2-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="3a7a2-160">要求の例</span><span class="sxs-lookup"><span data-stu-id="3a7a2-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="3a7a2-161">応答の例</span><span class="sxs-lookup"><span data-stu-id="3a7a2-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
