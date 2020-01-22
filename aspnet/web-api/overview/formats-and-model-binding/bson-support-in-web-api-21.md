---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1 での BSON のサポート-ASP.NET 4.x
author: MikeWasson
description: Web API コントローラー (サーバー側) と ASP.NET 4.x 用の .NET クライアントアプリで、BSON を使用する方法について説明します。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519332"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="a10b3-103">ASP.NET Web API 2.1 での BSON のサポート</span><span class="sxs-lookup"><span data-stu-id="a10b3-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="a10b3-104">作成者 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a10b3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a10b3-105">このトピックでは、Web API コントローラー (サーバー側) と .NET クライアントアプリで BSON を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="a10b3-106">Web API 2.1 では、BSON のサポートが導入されています。</span><span class="sxs-lookup"><span data-stu-id="a10b3-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="a10b3-107">BSON とは</span><span class="sxs-lookup"><span data-stu-id="a10b3-107">What is BSON?</span></span>

<span data-ttu-id="a10b3-108">[Bson](http://bsonspec.org/)は、バイナリシリアル化形式です。</span><span class="sxs-lookup"><span data-stu-id="a10b3-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="a10b3-109">"BSON" は "Binary JSON" を表しますが、BSON と JSON はまったく異なる方法でシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="a10b3-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="a10b3-110">BSON は、JSON に似た名前と値のペアで表されるため、"JSON に似ています" です。</span><span class="sxs-lookup"><span data-stu-id="a10b3-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="a10b3-111">JSON とは異なり、数値データ型は文字列ではなくバイトとして格納されます。</span><span class="sxs-lookup"><span data-stu-id="a10b3-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="a10b3-112">BSON は、軽量で、スキャンが容易で、エンコード/デコードが高速になるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="a10b3-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="a10b3-113">BSON のサイズは JSON に相当します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="a10b3-114">データによっては、BSON ペイロードのサイズが、JSON ペイロードより増減する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a10b3-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="a10b3-115">画像ファイルなどのバイナリデータをシリアル化する場合、バイナリデータは base64 でエンコードされないため、BSON は JSON よりも小さくなります。</span><span class="sxs-lookup"><span data-stu-id="a10b3-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="a10b3-116">要素には長さフィールドが付いているため、BSON ドキュメントは簡単にスキャンできます。そのため、パーサーは、要素をデコードせずにスキップできます。</span><span class="sxs-lookup"><span data-stu-id="a10b3-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="a10b3-117">数値データ型は文字列ではなく数値として格納されるため、エンコードとデコードは効率的です。</span><span class="sxs-lookup"><span data-stu-id="a10b3-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="a10b3-118">.NET クライアントアプリなどのネイティブクライアントでは、JSON や XML などのテキストベースの形式の代わりに BSON を使用するとメリットが得られます。</span><span class="sxs-lookup"><span data-stu-id="a10b3-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="a10b3-119">ブラウザークライアントの場合は、json を使用することをお勧めします。これは、JavaScript が JSON ペイロードを直接変換できるためです。</span><span class="sxs-lookup"><span data-stu-id="a10b3-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="a10b3-120">幸いなことに、Web API では[コンテンツネゴシエーション](content-negotiation.md)が使用されるため、API は両方の形式をサポートし、クライアントが選択できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="a10b3-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="a10b3-121">サーバーでの BSON の有効化</span><span class="sxs-lookup"><span data-stu-id="a10b3-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="a10b3-122">Web API 構成で、フォーマッタコレクションに**BsonMediaTypeFormatter**を追加します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="a10b3-123">これで、クライアントが "application/bson" を要求した場合、Web API は BSON フォーマッタを使用します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="a10b3-124">BSON を他のメディアの種類と関連付けるには、SupportedMediaTypes コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="a10b3-125">次のコードでは、サポートされているメディアの種類に "application/vnd. contoso" を追加します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="a10b3-126">HTTP セッションの例</span><span class="sxs-lookup"><span data-stu-id="a10b3-126">Example HTTP Session</span></span>

<span data-ttu-id="a10b3-127">この例では、次のモデルクラスと単純な Web API コントローラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="a10b3-128">クライアントは、次の HTTP 要求を送信する場合があります。</span><span class="sxs-lookup"><span data-stu-id="a10b3-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="a10b3-129">応答を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="a10b3-130">ここでは、バイナリデータを &quot;に置き換えました。&quot; 文字。</span><span class="sxs-lookup"><span data-stu-id="a10b3-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="a10b3-131">Fiddler の次のスクリーンショットは、生の16進値を示しています。</span><span class="sxs-lookup"><span data-stu-id="a10b3-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="a10b3-132">HttpClient での BSON の使用</span><span class="sxs-lookup"><span data-stu-id="a10b3-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="a10b3-133">.NET クライアントアプリでは、 **Httpclient**で bson formatter を使用できます。</span><span class="sxs-lookup"><span data-stu-id="a10b3-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="a10b3-134">**Httpclient**の詳細については、「 [.net クライアントからの Web API の呼び出し](../advanced/calling-a-web-api-from-a-net-client.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a10b3-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="a10b3-135">次のコードは、BSON を受け入れる GET 要求を送信し、応答の BSON ペイロードを逆シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="a10b3-136">サーバーからの BSON を要求するには、Accept ヘッダーを "application/bson" に設定します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="a10b3-137">応答本文を逆シリアル化するには、 **BsonMediaTypeFormatter**を使用します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="a10b3-138">このフォーマッタは、既定のフォーマッタコレクションに含まれていないため、応答本文を読み取るときに指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a10b3-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="a10b3-139">次の例では、BSON を含む POST 要求を送信する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="a10b3-140">このコードの大部分は、前の例と同じです。</span><span class="sxs-lookup"><span data-stu-id="a10b3-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="a10b3-141">しかし、 **Postasync**メソッドでは、フォーマッタとして**BsonMediaTypeFormatter**を指定します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="a10b3-142">最上位レベルのプリミティブ型のシリアル化</span><span class="sxs-lookup"><span data-stu-id="a10b3-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="a10b3-143">各 BSON ドキュメントは、キーと値のペアの一覧です。BSON 仕様では、整数や文字列など、1つの生の値をシリアル化するための構文は定義されていません。</span><span class="sxs-lookup"><span data-stu-id="a10b3-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="a10b3-144">この制限を回避するために、 **BsonMediaTypeFormatter**はプリミティブ型を特殊なケースとして扱います。</span><span class="sxs-lookup"><span data-stu-id="a10b3-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="a10b3-145">シリアル化する前に、キー "Value" を使用して値をキーと値のペアに変換します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="a10b3-146">たとえば、API コントローラーから整数が返されるとします。</span><span class="sxs-lookup"><span data-stu-id="a10b3-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="a10b3-147">シリアル化する前に、BSON フォーマッタはこれを次のキーと値のペアに変換します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="a10b3-148">逆シリアル化すると、フォーマッタはデータを元の値に変換します。</span><span class="sxs-lookup"><span data-stu-id="a10b3-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="a10b3-149">ただし、web API から生の値が返された場合、別の BSON パーサーを使用するクライアントはこのケースを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a10b3-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="a10b3-150">一般に、未加工の値ではなく、構造化されたデータを返すことを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a10b3-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a10b3-151">その他の資料</span><span class="sxs-lookup"><span data-stu-id="a10b3-151">Additional Resources</span></span>

[<span data-ttu-id="a10b3-152">Web API の BSON サンプル</span><span class="sxs-lookup"><span data-stu-id="a10b3-152">Web API BSON Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[<span data-ttu-id="a10b3-153">メディアフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="a10b3-153">Media Formatters</span></span>](media-formatters.md)
