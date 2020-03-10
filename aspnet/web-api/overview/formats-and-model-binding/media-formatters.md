---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2-ASP.NET 4.x のメディアフォーマッタ
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API で、追加のメディア形式をサポートする方法を示します。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448942"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="7718e-103">ASP.NET Web API 2 のメディアフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="7718e-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="7718e-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7718e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7718e-105">このチュートリアルでは、ASP.NET Web API で追加のメディア形式をサポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7718e-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="7718e-106">インターネットメディアの種類</span><span class="sxs-lookup"><span data-stu-id="7718e-106">Internet Media Types</span></span>

<span data-ttu-id="7718e-107">メディアの種類は、MIME の種類とも呼ばれ、データの形式を識別します。</span><span class="sxs-lookup"><span data-stu-id="7718e-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="7718e-108">HTTP では、メディアの種類によってメッセージ本文の形式が記述されます。</span><span class="sxs-lookup"><span data-stu-id="7718e-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="7718e-109">メディアの種類は、型とサブタイプの2つの文字列で構成されます。</span><span class="sxs-lookup"><span data-stu-id="7718e-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="7718e-110">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="7718e-110">For example:</span></span>

- <span data-ttu-id="7718e-111">text/html</span><span class="sxs-lookup"><span data-stu-id="7718e-111">text/html</span></span>
- <span data-ttu-id="7718e-112">image/png</span><span class="sxs-lookup"><span data-stu-id="7718e-112">image/png</span></span>
- <span data-ttu-id="7718e-113">application/json</span><span class="sxs-lookup"><span data-stu-id="7718e-113">application/json</span></span>

<span data-ttu-id="7718e-114">HTTP メッセージにエンティティ本体が含まれている場合、Content-type ヘッダーはメッセージ本文の形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="7718e-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="7718e-115">これにより、メッセージ本文の内容を解析する方法を受信側に通知します。</span><span class="sxs-lookup"><span data-stu-id="7718e-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="7718e-116">たとえば、HTTP 応答に PNG 画像が含まれている場合、応答には次のヘッダーが含まれる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7718e-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="7718e-117">クライアントは、要求メッセージを送信するときに Accept ヘッダーを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="7718e-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="7718e-118">Accept ヘッダーは、クライアントがサーバーから要求するメディアの種類をサーバーに通知します。</span><span class="sxs-lookup"><span data-stu-id="7718e-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="7718e-119">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="7718e-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="7718e-120">このヘッダーは、クライアントが HTML、XHTML、XML のいずれかを必要としていることをサーバーに通知します。</span><span class="sxs-lookup"><span data-stu-id="7718e-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="7718e-121">メディアの種類によって、Web API が HTTP メッセージ本文をシリアル化および逆シリアル化する方法が決まります。</span><span class="sxs-lookup"><span data-stu-id="7718e-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="7718e-122">Web API には、XML、JSON、BSON、およびフォーム url エンコードデータのサポートが組み込まれており、*メディアフォーマッタ*を作成することにより、追加のメディアの種類をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="7718e-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="7718e-123">メディアフォーマッタを作成するには、次のいずれかのクラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="7718e-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="7718e-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7718e-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="7718e-125">このクラスは、非同期の読み取りおよび書き込みメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="7718e-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="7718e-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7718e-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="7718e-127">このクラスは**MediaTypeFormatter**から派生しますが、同期読み取り/書き込みメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="7718e-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="7718e-128">非同期コードは存在しないため、 **BufferedMediaTypeFormatter**からの派生はより簡単ですが、i/o 中に呼び出し元のスレッドがブロックできることも意味します。</span><span class="sxs-lookup"><span data-stu-id="7718e-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="7718e-129">例: CSV メディアフォーマッタの作成</span><span class="sxs-lookup"><span data-stu-id="7718e-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="7718e-130">次の例は、製品オブジェクトをコンマ区切り値 (CSV) 形式にシリアル化できるメディアの種類のフォーマッタを示しています。</span><span class="sxs-lookup"><span data-stu-id="7718e-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="7718e-131">この例では、「チュートリアル」で定義されている製品の種類を使用して、 [CRUD 操作をサポートする WEB API を作成](../older-versions/creating-a-web-api-that-supports-crud-operations.md)します。</span><span class="sxs-lookup"><span data-stu-id="7718e-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="7718e-132">製品オブジェクトの定義を次に示します。</span><span class="sxs-lookup"><span data-stu-id="7718e-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="7718e-133">CSV フォーマッタを実装するには、 **BufferedMediaTypeFormatter**から派生するクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="7718e-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="7718e-134">コンストラクターで、フォーマッタがサポートするメディアの種類を追加します。</span><span class="sxs-lookup"><span data-stu-id="7718e-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="7718e-135">この例では、フォーマッタは、1つのメディアの種類 &quot;text/csv&quot;をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7718e-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="7718e-136">**Canwritetype**メソッドをオーバーライドして、フォーマッタがシリアル化できる型を指定します。</span><span class="sxs-lookup"><span data-stu-id="7718e-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="7718e-137">この例では、フォーマッタは、単一の `Product` オブジェクトおよび `Product` オブジェクトのコレクションをシリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="7718e-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="7718e-138">同様に、 **Canreadtype**メソッドをオーバーライドして、フォーマッタが逆シリアル化できる型を指定します。</span><span class="sxs-lookup"><span data-stu-id="7718e-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="7718e-139">この例では、フォーマッタは逆シリアル化をサポートしていないので、メソッドは単に**false**を返します。</span><span class="sxs-lookup"><span data-stu-id="7718e-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="7718e-140">最後に、 **Writetostream**メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="7718e-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="7718e-141">このメソッドは、ストリームに書き込み、型をシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="7718e-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="7718e-142">フォーマッタが逆シリアル化をサポートしている場合は、 **Readfromstream**メソッドもオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="7718e-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="7718e-143">Web API パイプラインへのメディアフォーマッタの追加</span><span class="sxs-lookup"><span data-stu-id="7718e-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="7718e-144">メディアの種類のフォーマッタを Web API パイプラインに追加するには、 **Httpconfiguration**オブジェクトの**フォーマッタ**プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="7718e-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="7718e-145">文字エンコード</span><span class="sxs-lookup"><span data-stu-id="7718e-145">Character Encodings</span></span>

<span data-ttu-id="7718e-146">必要に応じて、メディアフォーマッタは、UTF-8 や ISO 8859-1 などの複数の文字エンコーディングをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="7718e-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="7718e-147">コンストラクターで、 **SupportedEncodings**コレクションに1つまたは複数の system.string[の種類を追加します](https://msdn.microsoft.com/library/system.text.encoding.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7718e-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="7718e-148">最初に既定のエンコードを指定します。</span><span class="sxs-lookup"><span data-stu-id="7718e-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="7718e-149">**Writetostream**メソッドと**readfromstream**メソッドで、 [MediaTypeFormatter エンコーディング](https://msdn.microsoft.com/library/hh969054.aspx)を呼び出して、優先する文字エンコードを選択します。</span><span class="sxs-lookup"><span data-stu-id="7718e-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="7718e-150">このメソッドは、要求ヘッダーを、サポートされているエンコーディングの一覧と照合します。</span><span class="sxs-lookup"><span data-stu-id="7718e-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="7718e-151">ストリームから読み取りまたは書き込みを行うときは、返された**エンコーディング**を使用します。</span><span class="sxs-lookup"><span data-stu-id="7718e-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
