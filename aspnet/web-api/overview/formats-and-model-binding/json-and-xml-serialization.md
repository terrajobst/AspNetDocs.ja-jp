---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API での JSON および XML シリアル化-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API の JSON および XML フォーマッタについて説明します。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449128"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="77aeb-103">ASP.NET Web API での JSON および XML シリアル化</span><span class="sxs-lookup"><span data-stu-id="77aeb-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="77aeb-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="77aeb-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="77aeb-105">この記事では、ASP.NET Web API の JSON フォーマッタと XML フォーマッタについて説明します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="77aeb-106">ASP.NET Web API の*メディアタイプフォーマッタ*は、次のことが可能なオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="77aeb-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="77aeb-107">HTTP メッセージ本文から CLR オブジェクトを読み取る</span><span class="sxs-lookup"><span data-stu-id="77aeb-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="77aeb-108">CLR オブジェクトを HTTP メッセージ本文に書き込む</span><span class="sxs-lookup"><span data-stu-id="77aeb-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="77aeb-109">Web API は、JSON と XML の両方のメディアタイプフォーマッタを提供します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="77aeb-110">フレームワークは、これらのフォーマッタを既定でパイプラインに挿入します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="77aeb-111">クライアントは、HTTP 要求の Accept ヘッダーに JSON または XML のいずれかを要求できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="77aeb-112">内容</span><span class="sxs-lookup"><span data-stu-id="77aeb-112">Contents</span></span>

- [<span data-ttu-id="77aeb-113">JSON メディアタイプフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="77aeb-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="77aeb-114">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="77aeb-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="77aeb-115">制約</span><span class="sxs-lookup"><span data-stu-id="77aeb-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="77aeb-116">インデント</span><span class="sxs-lookup"><span data-stu-id="77aeb-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="77aeb-117">Camel 形式の文字種</span><span class="sxs-lookup"><span data-stu-id="77aeb-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="77aeb-118">厳密に型指定されていない匿名のオブジェクト</span><span class="sxs-lookup"><span data-stu-id="77aeb-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="77aeb-119">XML メディア型フォーマッタ</span><span class="sxs-lookup"><span data-stu-id="77aeb-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="77aeb-120">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="77aeb-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="77aeb-121">制約</span><span class="sxs-lookup"><span data-stu-id="77aeb-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="77aeb-122">インデント</span><span class="sxs-lookup"><span data-stu-id="77aeb-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="77aeb-123">型ごとの XML シリアライザーの設定</span><span class="sxs-lookup"><span data-stu-id="77aeb-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="77aeb-124">JSON または XML フォーマッタの削除</span><span class="sxs-lookup"><span data-stu-id="77aeb-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="77aeb-125">循環オブジェクト参照の処理</span><span class="sxs-lookup"><span data-stu-id="77aeb-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="77aeb-126">オブジェクトのシリアル化のテスト</span><span class="sxs-lookup"><span data-stu-id="77aeb-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="77aeb-127">JSON メディアタイプフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="77aeb-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="77aeb-128">JSON 形式は、 **JsonMediaTypeFormatter**クラスによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="77aeb-129">既定では、 **JsonMediaTypeFormatter**は[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)ライブラリを使用してシリアル化を実行します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="77aeb-130">Json.NET は、サードパーティのオープンソースプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="77aeb-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="77aeb-131">必要に応じて、Json.NET ではなく**DataContractJsonSerializer**を使用するように**JsonMediaTypeFormatter**クラスを構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="77aeb-132">これを行うには、 **UseDataContractJsonSerializer**プロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="77aeb-133">JSON シリアル化</span><span class="sxs-lookup"><span data-stu-id="77aeb-133">JSON Serialization</span></span>

<span data-ttu-id="77aeb-134">このセクションでは、既定の[Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer を使用して、JSON フォーマッタの特定の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="77aeb-135">これは、Json.NET ライブラリの包括的なドキュメントではありません。詳細については、 [Json.NET のドキュメント](http://james.newtonking.com/projects/json/help/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="77aeb-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="77aeb-136">シリアル化の対象</span><span class="sxs-lookup"><span data-stu-id="77aeb-136">What Gets Serialized?</span></span>

<span data-ttu-id="77aeb-137">既定では、すべてのパブリックプロパティとパブリックフィールドが、シリアル化された JSON に含まれます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="77aeb-138">プロパティまたはフィールドを省略するには、 **Jsonignore**属性で装飾します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="77aeb-139">&quot;オプトイン&quot; 方法を使用する場合は、 **DataContract**属性でクラスを装飾します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="77aeb-140">この属性が存在する場合、メンバーは、 **DataMember**を持っている場合を除き、無視されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="77aeb-141">また、 **DataMember**を使用してプライベートメンバーをシリアル化することもできます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="77aeb-142">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="77aeb-142">Read-Only Properties</span></span>

<span data-ttu-id="77aeb-143">読み取り専用プロパティは、既定でシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="77aeb-144">日付</span><span class="sxs-lookup"><span data-stu-id="77aeb-144">Dates</span></span>

<span data-ttu-id="77aeb-145">既定では、Json.NET は[ISO 8601](http://www.w3.org/TR/NOTE-datetime)形式で日付を書き込みます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="77aeb-146">UTC (協定世界時) の日付は、サフィックス "Z" を使用して書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="77aeb-147">現地時刻の日付には、タイムゾーンオフセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="77aeb-148">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="77aeb-149">既定では、Json.NET はタイムゾーンを保持します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="77aeb-150">これをオーバーライドするには、DateTimeZoneHandling プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="77aeb-151">ISO 8601 ではなく[MICROSOFT JSON 日付形式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)(`"\/Date(ticks)\/"`) を使用する場合は、シリアライザー設定の**DateFormatHandling**プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="77aeb-152">インデント</span><span class="sxs-lookup"><span data-stu-id="77aeb-152">Indenting</span></span>

<span data-ttu-id="77aeb-153">インデントされた JSON を書き込むには、**書式**設定を書式設定に設定**します。インデント**:</span><span class="sxs-lookup"><span data-stu-id="77aeb-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="77aeb-154">Camel 形式の文字種</span><span class="sxs-lookup"><span data-stu-id="77aeb-154">Camel Casing</span></span>

<span data-ttu-id="77aeb-155">データモデルを変更せずに camel 形式の JSON プロパティ名を書き込むには、シリアライザーで**CamelCasePropertyNamesContractResolver**を設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="77aeb-156">厳密に型指定されていない匿名のオブジェクト</span><span class="sxs-lookup"><span data-stu-id="77aeb-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="77aeb-157">アクションメソッドは、匿名オブジェクトを返し、それを JSON にシリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="77aeb-158">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="77aeb-159">応答メッセージの本文には、次の JSON が含まれます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="77aeb-160">Web API がクライアントから緩やかに構造化された JSON オブジェクトを受信する場合は、要求本文を**Newtonsoft. Linq オブジェクト**型に逆シリアル化できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="77aeb-161">ただし、通常は、厳密に型指定されたデータオブジェクトを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="77aeb-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="77aeb-162">その後、データを自分で解析する必要がなく、モデルの検証の利点が得られます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="77aeb-163">XML シリアライザーは、匿名型または**Jobject**インスタンスをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="77aeb-164">これらの機能を JSON データに使用する場合は、この記事の後半で説明するように、パイプラインから XML フォーマッタを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="77aeb-165">XML メディア型フォーマッタ</span><span class="sxs-lookup"><span data-stu-id="77aeb-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="77aeb-166">XML の書式設定は、 **XmlMediaTypeFormatter**クラスによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="77aeb-167">既定では、 **XmlMediaTypeFormatter**は**DataContractSerializer**クラスを使用してシリアル化を実行します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="77aeb-168">必要に応じて、 **DataContractSerializer**ではなく**XmlSerializer**を使用するように**XmlMediaTypeFormatter**を構成できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="77aeb-169">これを行うには、 **UseXmlSerializer**プロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="77aeb-170">**XmlSerializer**クラスでは、 **DataContractSerializer**よりも狭い種類の型がサポートされていますが、結果の XML はより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="77aeb-171">既存の XML スキーマに一致する必要がある場合は、 **XmlSerializer**の使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="77aeb-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="77aeb-172">XML シリアル化</span><span class="sxs-lookup"><span data-stu-id="77aeb-172">XML Serialization</span></span>

<span data-ttu-id="77aeb-173">このセクションでは、既定の**DataContractSerializer**を使用して、XML フォーマッタの特定の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="77aeb-174">既定では、DataContractSerializer は次のように動作します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="77aeb-175">パブリックの読み取り/書き込みプロパティとフィールドはすべてシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="77aeb-176">プロパティまたはフィールドを省略するには、 **Ignoredatamember**属性で装飾します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="77aeb-177">プライベートメンバーとプロテクトメンバーはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="77aeb-178">読み取り専用プロパティはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="77aeb-179">(ただし、読み取り専用コレクションプロパティの内容はシリアル化されます)。</span><span class="sxs-lookup"><span data-stu-id="77aeb-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="77aeb-180">クラス名とメンバー名は、クラス宣言に出現するとおりに XML で記述されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="77aeb-181">既定の XML 名前空間が使用されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-181">A default XML namespace is used.</span></span>

<span data-ttu-id="77aeb-182">シリアル化をさらに制御する必要がある場合は、 **DataContract**属性を使用してクラスを装飾できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="77aeb-183">この属性が存在する場合、クラスは次のようにシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="77aeb-184">&quot;オプトイン&quot; 方法: 既定では、プロパティとフィールドはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="77aeb-185">プロパティまたはフィールドをシリアル化するには、 **DataMember**属性で装飾します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="77aeb-186">プライベートメンバーまたはプロテクトメンバーをシリアル化するには、 **DataMember**属性で装飾します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="77aeb-187">読み取り専用プロパティはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="77aeb-188">XML でのクラス名の表示方法を変更するには、 **DataContract**属性の*name*パラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="77aeb-189">XML でのメンバー名の表示方法を変更するには、 **DataMember**属性に*name*パラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="77aeb-190">XML 名前空間を変更するには、 **DataContract**クラスの*namespace*パラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="77aeb-191">読み取り専用プロパティ</span><span class="sxs-lookup"><span data-stu-id="77aeb-191">Read-Only Properties</span></span>

<span data-ttu-id="77aeb-192">読み取り専用プロパティはシリアル化されません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="77aeb-193">読み取り専用プロパティにバッキングプライベートフィールドがある場合は、 **DataMember**属性を使用してプライベートフィールドをマークできます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="77aeb-194">この方法では、クラスの**DataContract**属性が必要です。</span><span class="sxs-lookup"><span data-stu-id="77aeb-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="77aeb-195">日付</span><span class="sxs-lookup"><span data-stu-id="77aeb-195">Dates</span></span>

<span data-ttu-id="77aeb-196">日付は ISO 8601 形式で記述されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="77aeb-197">たとえば、&quot;2012-05-23T20:21: 37.9116538 Z&quot;のようになります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="77aeb-198">インデント</span><span class="sxs-lookup"><span data-stu-id="77aeb-198">Indenting</span></span>

<span data-ttu-id="77aeb-199">インデントされた XML を書き込むには、 **[インデント]** プロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="77aeb-200">型ごとの XML シリアライザーの設定</span><span class="sxs-lookup"><span data-stu-id="77aeb-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="77aeb-201">異なる CLR 型に対して異なる XML シリアライザーを設定できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="77aeb-202">たとえば、旧バージョンとの互換性のために**XmlSerializer**を必要とする特定のデータオブジェクトがある場合があります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="77aeb-203">このオブジェクトに**XmlSerializer**を使用して、他の型に対して**DataContractSerializer**を引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="77aeb-204">特定の型の XML シリアライザーを設定するには、 **Setserializer**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="77aeb-205">**XmlSerializer**または**XmlObjectSerializer**から派生した任意のオブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="77aeb-206">JSON または XML フォーマッタの削除</span><span class="sxs-lookup"><span data-stu-id="77aeb-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="77aeb-207">フォーマッタを使用しない場合は、フォーマッタの一覧から JSON フォーマッタまたは XML フォーマッタを削除できます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="77aeb-208">これを行う主な理由は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="77aeb-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="77aeb-209">Web API の応答を特定のメディアの種類に制限する。</span><span class="sxs-lookup"><span data-stu-id="77aeb-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="77aeb-210">たとえば、JSON 応答のみをサポートし、XML フォーマッタを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="77aeb-211">既定のフォーマッタをカスタムフォーマッタに置き換える場合は。</span><span class="sxs-lookup"><span data-stu-id="77aeb-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="77aeb-212">たとえば、json フォーマッタを JSON フォーマッタの独自のカスタム実装に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="77aeb-213">次のコードは、既定のフォーマッタを削除する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="77aeb-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="77aeb-214">このメソッドは、global.asax で定義された**開始メソッド\_アプリケーション**から呼び出します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="77aeb-215">循環オブジェクト参照の処理</span><span class="sxs-lookup"><span data-stu-id="77aeb-215">Handling Circular Object References</span></span>

<span data-ttu-id="77aeb-216">既定では、JSON および XML フォーマッタはすべてのオブジェクトを値として書き込みます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="77aeb-217">2つのプロパティが同じオブジェクトを参照している場合、またはコレクション内で同じオブジェクトが2回出現する場合、フォーマッタはオブジェクトを2回シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="77aeb-218">これは、オブジェクトグラフに循環が含まれている場合の問題です。これは、シリアライザーがグラフ内でループを検出したときに例外をスローするためです。</span><span class="sxs-lookup"><span data-stu-id="77aeb-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="77aeb-219">次のオブジェクトモデルとコントローラーを考えてみます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="77aeb-220">このアクションを呼び出すと、フォーマッタによって例外がスローされ、クライアントへのステータスコード 500 (内部サーバーエラー) 応答に変換されます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="77aeb-221">JSON でオブジェクト参照を保持するには、次のコードを、global.asax ファイルの**Application\_Start**メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="77aeb-222">これで、コントローラーアクションは次のような JSON を返します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="77aeb-223">シリアライザーによって &quot;$id&quot; プロパティが両方のオブジェクトに追加されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="77aeb-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="77aeb-224">また、Employee. Department プロパティによってループが作成されていることが検出されるため、値は {&quot;$ref&quot;:&quot;1&quot;} というオブジェクト参照に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="77aeb-225">オブジェクト参照は JSON では標準ではありません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="77aeb-226">この機能を使用する前に、クライアントが結果を解析できるかどうかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="77aeb-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="77aeb-227">グラフからサイクルを削除するだけでよい場合もあります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="77aeb-228">たとえば、この例では、従業員から部署へのリンクは実際には必要ありません。</span><span class="sxs-lookup"><span data-stu-id="77aeb-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="77aeb-229">XML でオブジェクト参照を保持するには、2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="77aeb-230">より簡単な方法は、モデルクラスに `[DataContract(IsReference=true)]` を追加することです。</span><span class="sxs-lookup"><span data-stu-id="77aeb-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="77aeb-231">*IsReference*パラメーターを使用すると、オブジェクト参照が有効になります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="77aeb-232">**DataContract**ではシリアル化がオプトインされているため、プロパティに**DataMember**属性を追加する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="77aeb-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="77aeb-233">これで、フォーマッタは次のような XML を生成します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="77aeb-234">モデルクラスで属性を使用しない場合は、別のオプションがあります。新しい型固有の**DataContractSerializer**インスタンスを作成し、コンストラクターで*preserveObjectReferences*を**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="77aeb-235">次に、このインスタンスを XML メディア型フォーマッタの型ごとのシリアライザーとして設定します。</span><span class="sxs-lookup"><span data-stu-id="77aeb-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="77aeb-236">次のコードは、これを行う方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="77aeb-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="77aeb-237">オブジェクトのシリアル化のテスト</span><span class="sxs-lookup"><span data-stu-id="77aeb-237">Testing Object Serialization</span></span>

<span data-ttu-id="77aeb-238">Web API を設計する際には、データオブジェクトがどのようにシリアル化されるかをテストすると便利です。</span><span class="sxs-lookup"><span data-stu-id="77aeb-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="77aeb-239">これは、コントローラーを作成したり、コントローラーアクションを呼び出したりせずに行うことができます。</span><span class="sxs-lookup"><span data-stu-id="77aeb-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
