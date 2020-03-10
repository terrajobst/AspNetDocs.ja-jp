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
# <a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 のメディアフォーマッタ

[Mike Wasson](https://github.com/MikeWasson)

このチュートリアルでは、ASP.NET Web API で追加のメディア形式をサポートする方法について説明します。

## <a name="internet-media-types"></a>インターネットメディアの種類

メディアの種類は、MIME の種類とも呼ばれ、データの形式を識別します。 HTTP では、メディアの種類によってメッセージ本文の形式が記述されます。 メディアの種類は、型とサブタイプの2つの文字列で構成されます。 次に例を示します。

- text/html
- image/png
- application/json

HTTP メッセージにエンティティ本体が含まれている場合、Content-type ヘッダーはメッセージ本文の形式を指定します。 これにより、メッセージ本文の内容を解析する方法を受信側に通知します。

たとえば、HTTP 応答に PNG 画像が含まれている場合、応答には次のヘッダーが含まれる可能性があります。

[!code-console[Main](media-formatters/samples/sample1.cmd)]

クライアントは、要求メッセージを送信するときに Accept ヘッダーを含めることができます。 Accept ヘッダーは、クライアントがサーバーから要求するメディアの種類をサーバーに通知します。 次に例を示します。

[!code-console[Main](media-formatters/samples/sample2.cmd)]

このヘッダーは、クライアントが HTML、XHTML、XML のいずれかを必要としていることをサーバーに通知します。

メディアの種類によって、Web API が HTTP メッセージ本文をシリアル化および逆シリアル化する方法が決まります。 Web API には、XML、JSON、BSON、およびフォーム url エンコードデータのサポートが組み込まれており、*メディアフォーマッタ*を作成することにより、追加のメディアの種類をサポートできます。

メディアフォーマッタを作成するには、次のいずれかのクラスから派生します。

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。 このクラスは、非同期の読み取りおよび書き込みメソッドを使用します。
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。 このクラスは**MediaTypeFormatter**から派生しますが、同期読み取り/書き込みメソッドを使用します。

非同期コードは存在しないため、 **BufferedMediaTypeFormatter**からの派生はより簡単ですが、i/o 中に呼び出し元のスレッドがブロックできることも意味します。

## <a name="example-creating-a-csv-media-formatter"></a>例: CSV メディアフォーマッタの作成

次の例は、製品オブジェクトをコンマ区切り値 (CSV) 形式にシリアル化できるメディアの種類のフォーマッタを示しています。 この例では、「チュートリアル」で定義されている製品の種類を使用して、 [CRUD 操作をサポートする WEB API を作成](../older-versions/creating-a-web-api-that-supports-crud-operations.md)します。 製品オブジェクトの定義を次に示します。

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

CSV フォーマッタを実装するには、 **BufferedMediaTypeFormatter**から派生するクラスを定義します。

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

コンストラクターで、フォーマッタがサポートするメディアの種類を追加します。 この例では、フォーマッタは、1つのメディアの種類 &quot;text/csv&quot;をサポートしています。

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

**Canwritetype**メソッドをオーバーライドして、フォーマッタがシリアル化できる型を指定します。

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

この例では、フォーマッタは、単一の `Product` オブジェクトおよび `Product` オブジェクトのコレクションをシリアル化できます。

同様に、 **Canreadtype**メソッドをオーバーライドして、フォーマッタが逆シリアル化できる型を指定します。 この例では、フォーマッタは逆シリアル化をサポートしていないので、メソッドは単に**false**を返します。

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

最後に、 **Writetostream**メソッドをオーバーライドします。 このメソッドは、ストリームに書き込み、型をシリアル化します。 フォーマッタが逆シリアル化をサポートしている場合は、 **Readfromstream**メソッドもオーバーライドします。

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>Web API パイプラインへのメディアフォーマッタの追加

メディアの種類のフォーマッタを Web API パイプラインに追加するには、 **Httpconfiguration**オブジェクトの**フォーマッタ**プロパティを使用します。

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>文字エンコード

必要に応じて、メディアフォーマッタは、UTF-8 や ISO 8859-1 などの複数の文字エンコーディングをサポートできます。

コンストラクターで、 **SupportedEncodings**コレクションに1つまたは複数の system.string[の種類を追加します](https://msdn.microsoft.com/library/system.text.encoding.aspx)。 最初に既定のエンコードを指定します。

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

**Writetostream**メソッドと**readfromstream**メソッドで、 [MediaTypeFormatter エンコーディング](https://msdn.microsoft.com/library/hh969054.aspx)を呼び出して、優先する文字エンコードを選択します。 このメソッドは、要求ヘッダーを、サポートされているエンコーディングの一覧と照合します。 ストリームから読み取りまたは書き込みを行うときは、返された**エンコーディング**を使用します。

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
