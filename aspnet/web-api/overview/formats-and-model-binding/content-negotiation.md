---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API でのコンテンツネゴシエーション-ASP.NET 4.x
author: MikeWasson
description: ASP.NET Web API が、ASP.NET 4.x の HTTP コンテンツネゴシエーションを実装する方法について説明します。
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504658"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="fdb72-103">ASP.NET Web API でのコンテンツネゴシエーション</span><span class="sxs-lookup"><span data-stu-id="fdb72-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="fdb72-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fdb72-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fdb72-105">この記事では、ASP.NET Web API が ASP.NET 4.x のコンテンツネゴシエーションを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="fdb72-106">HTTP 仕様 (RFC 2616) は、"使用可能な複数の表現がある場合に、特定の応答に対して最適な表現を選択するプロセス" としてコンテンツネゴシエーションを定義します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="fdb72-107">HTTP でのコンテンツネゴシエーションの主要なメカニズムは、次の要求ヘッダーです。</span><span class="sxs-lookup"><span data-stu-id="fdb72-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="fdb72-108">**同意:** 応答で許容されるメディアの種類 ("application/json"、"application/xml" など)、または &quot;application/vnd などのカスタムメディアの種類。例 + xml&quot;</span><span class="sxs-lookup"><span data-stu-id="fdb72-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="fdb72-109">**Accept-Charset:** UTF-8 や ISO 8859-1 など、許容される文字セットを指定します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="fdb72-110">**Accept-Encoding:** Gzip など、許容されるコンテンツエンコーディング。</span><span class="sxs-lookup"><span data-stu-id="fdb72-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="fdb72-111">**Accept-言語:** 適切な自然言語 ("en-us" など)。</span><span class="sxs-lookup"><span data-stu-id="fdb72-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="fdb72-112">サーバーは、HTTP 要求の他の部分を確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="fdb72-113">たとえば、要求に、AJAX 要求を示す "X 要求-With" ヘッダーが含まれている場合、Accept ヘッダーがない場合、サーバーでは既定で JSON が使用される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fdb72-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="fdb72-114">この記事では、Web API が Accept ヘッダーと Accept 文字セットヘッダーを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="fdb72-115">(現時点では、受け入れエンコードまたは受け入れ言語の組み込みサポートはありません)。</span><span class="sxs-lookup"><span data-stu-id="fdb72-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="fdb72-116">シリアル化</span><span class="sxs-lookup"><span data-stu-id="fdb72-116">Serialization</span></span>

<span data-ttu-id="fdb72-117">Web API コントローラーがリソースを CLR 型として返す場合、パイプラインは戻り値をシリアル化し、それを HTTP 応答の本文に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="fdb72-118">たとえば、次のコントローラーアクションを考えてみます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="fdb72-119">クライアントは、次の HTTP 要求を送信する場合があります。</span><span class="sxs-lookup"><span data-stu-id="fdb72-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="fdb72-120">応答として、サーバーから次のメッセージが送信される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fdb72-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="fdb72-121">この例では、クライアントが JSON、Javascript、または "何か" を要求しました (\*/\*)。</span><span class="sxs-lookup"><span data-stu-id="fdb72-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="fdb72-122">サーバーが `Product` オブジェクトの JSON 表現で応答しました。</span><span class="sxs-lookup"><span data-stu-id="fdb72-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="fdb72-123">応答の Content-type ヘッダーが &quot;application/json&quot;に設定されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="fdb72-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="fdb72-124">コントローラーは、 **HttpResponseMessage**オブジェクトを返すこともできます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="fdb72-125">応答本文に CLR オブジェクトを指定するには、 **CreateResponse**拡張メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="fdb72-126">このオプションを使用すると、応答の詳細をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="fdb72-127">ステータスコードの設定、HTTP ヘッダーの追加などを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="fdb72-128">リソースをシリアル化するオブジェクトは、*メディアフォーマッタ*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="fdb72-129">メディアフォーマッタは、 **MediaTypeFormatter**クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="fdb72-130">Web API には、XML および JSON 用のメディアフォーマッタが用意されています。また、他のメディアの種類をサポートするカスタムフォーマッタを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="fdb72-131">カスタムフォーマッタの記述の詳細については、「[メディアフォーマッタ](media-formatters.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fdb72-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="fdb72-132">コンテンツネゴシエーションのしくみ</span><span class="sxs-lookup"><span data-stu-id="fdb72-132">How Content Negotiation Works</span></span>

<span data-ttu-id="fdb72-133">まず、パイプラインは**Httpconfiguration**オブジェクトから**IContentNegotiator**サービスを取得します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="fdb72-134">また、 **Httpconfiguration. フォーマッタ**コレクションからメディアフォーマッタの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="fdb72-135">次に、パイプラインは**IContentNegotiator**を呼び出し、を渡します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="fdb72-136">シリアル化するオブジェクトの型。</span><span class="sxs-lookup"><span data-stu-id="fdb72-136">The type of object to serialize</span></span>
- <span data-ttu-id="fdb72-137">メディアフォーマッタのコレクション</span><span class="sxs-lookup"><span data-stu-id="fdb72-137">The collection of media formatters</span></span>
- <span data-ttu-id="fdb72-138">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="fdb72-138">The HTTP request</span></span>

<span data-ttu-id="fdb72-139">**Negotiate**メソッドは、次の2つの情報を返します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="fdb72-140">使用するフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="fdb72-140">Which formatter to use</span></span>
- <span data-ttu-id="fdb72-141">応答のメディアの種類</span><span class="sxs-lookup"><span data-stu-id="fdb72-141">The media type for the response</span></span>

<span data-ttu-id="fdb72-142">フォーマッタが見つからない場合、 **Negotiate**メソッドは**null**を返し、クライアントは HTTP エラー406を受信します (許容できません)。</span><span class="sxs-lookup"><span data-stu-id="fdb72-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="fdb72-143">次のコードは、コントローラーがコンテンツネゴシエーションを直接呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="fdb72-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="fdb72-144">このコードは、パイプラインによって自動的に行われる処理に相当します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="fdb72-145">既定のコンテンツ Negotiator</span><span class="sxs-lookup"><span data-stu-id="fdb72-145">Default Content Negotiator</span></span>

<span data-ttu-id="fdb72-146">**DefaultContentNegotiator**クラスは、 **IContentNegotiator**の既定の実装を提供します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="fdb72-147">複数の条件を使用してフォーマッタを選択します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="fdb72-148">最初に、フォーマッタは型をシリアル化できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="fdb72-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="fdb72-149">これは、 **MediaTypeFormatter**を呼び出すことによって検証されます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="fdb72-150">次に、コンテンツ negotiator は各フォーマッタを確認し、HTTP 要求にどの程度一致しているかを評価します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="fdb72-151">一致を評価するために、コンテンツ negotiator はフォーマッタに関して次の2つの点を確認します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="fdb72-152">**SupportedMediaTypes** collection。サポートされているメディアの種類の一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="fdb72-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="fdb72-153">コンテンツ negotiator は、このリストを要求 Accept ヘッダーと照合しようとします。</span><span class="sxs-lookup"><span data-stu-id="fdb72-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="fdb72-154">Accept ヘッダーには範囲を含めることができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="fdb72-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="fdb72-155">たとえば、"text/plain" は、text/\* または \*/\*に一致します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="fdb72-156">**MediaTypeMappings** Collection。 **MediaTypeMapping**オブジェクトの一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="fdb72-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="fdb72-157">**MediaTypeMapping**クラスは、HTTP 要求をメディアの種類と照合するための汎用的な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="fdb72-158">たとえば、カスタム HTTP ヘッダーを特定のメディアの種類にマップすることができます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="fdb72-159">複数の一致がある場合は、最高品質係数との一致が優先されます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="fdb72-160">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="fdb72-161">この例では、application/json には1.0 という暗黙の品質係数があるため、application/xml よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="fdb72-162">一致するものが見つからない場合、コンテンツ negotiator は、要求本文のメディアの種類 (存在する場合) との照合を試みます。</span><span class="sxs-lookup"><span data-stu-id="fdb72-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="fdb72-163">たとえば、要求に JSON データが含まれている場合、コンテンツ negotiator は JSON フォーマッタを検索します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="fdb72-164">一致するものがない場合、コンテンツ negotiator は、単純にその型をシリアル化できる最初のフォーマッタを選択します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="fdb72-165">文字エンコードの選択</span><span class="sxs-lookup"><span data-stu-id="fdb72-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="fdb72-166">フォーマッタを選択すると、コンテンツ negotiator はフォーマッタの**SupportedEncodings**プロパティを確認し、要求のヘッダー (存在する場合) と照合することで、最適な文字エンコーディングを選択します。</span><span class="sxs-lookup"><span data-stu-id="fdb72-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
