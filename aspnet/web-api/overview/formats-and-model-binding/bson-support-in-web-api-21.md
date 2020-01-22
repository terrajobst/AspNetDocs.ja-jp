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
# <a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1 での BSON のサポート

作成者 [Mike Wasson](https://github.com/MikeWasson)

このトピックでは、Web API コントローラー (サーバー側) と .NET クライアントアプリで BSON を使用する方法について説明します。 Web API 2.1 では、BSON のサポートが導入されています。 

## <a name="what-is-bson"></a>BSON とは

[Bson](http://bsonspec.org/)は、バイナリシリアル化形式です。 "BSON" は "Binary JSON" を表しますが、BSON と JSON はまったく異なる方法でシリアル化されます。 BSON は、JSON に似た名前と値のペアで表されるため、"JSON に似ています" です。 JSON とは異なり、数値データ型は文字列ではなくバイトとして格納されます。

BSON は、軽量で、スキャンが容易で、エンコード/デコードが高速になるように設計されています。

- BSON のサイズは JSON に相当します。 データによっては、BSON ペイロードのサイズが、JSON ペイロードより増減する可能性があります。 画像ファイルなどのバイナリデータをシリアル化する場合、バイナリデータは base64 でエンコードされないため、BSON は JSON よりも小さくなります。
- 要素には長さフィールドが付いているため、BSON ドキュメントは簡単にスキャンできます。そのため、パーサーは、要素をデコードせずにスキップできます。
- 数値データ型は文字列ではなく数値として格納されるため、エンコードとデコードは効率的です。

.NET クライアントアプリなどのネイティブクライアントでは、JSON や XML などのテキストベースの形式の代わりに BSON を使用するとメリットが得られます。 ブラウザークライアントの場合は、json を使用することをお勧めします。これは、JavaScript が JSON ペイロードを直接変換できるためです。

幸いなことに、Web API では[コンテンツネゴシエーション](content-negotiation.md)が使用されるため、API は両方の形式をサポートし、クライアントが選択できるようにすることができます。

## <a name="enabling-bson-on-the-server"></a>サーバーでの BSON の有効化

Web API 構成で、フォーマッタコレクションに**BsonMediaTypeFormatter**を追加します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

これで、クライアントが "application/bson" を要求した場合、Web API は BSON フォーマッタを使用します。

BSON を他のメディアの種類と関連付けるには、SupportedMediaTypes コレクションに追加します。 次のコードでは、サポートされているメディアの種類に "application/vnd. contoso" を追加します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>HTTP セッションの例

この例では、次のモデルクラスと単純な Web API コントローラーを使用します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

クライアントは、次の HTTP 要求を送信する場合があります。

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

応答を次に示します。

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

ここでは、バイナリデータを &quot;に置き換えました。&quot; 文字。 Fiddler の次のスクリーンショットは、生の16進値を示しています。

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>HttpClient での BSON の使用

.NET クライアントアプリでは、 **Httpclient**で bson formatter を使用できます。 **Httpclient**の詳細については、「 [.net クライアントからの Web API の呼び出し](../advanced/calling-a-web-api-from-a-net-client.md)」を参照してください。

次のコードは、BSON を受け入れる GET 要求を送信し、応答の BSON ペイロードを逆シリアル化します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

サーバーからの BSON を要求するには、Accept ヘッダーを "application/bson" に設定します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

応答本文を逆シリアル化するには、 **BsonMediaTypeFormatter**を使用します。 このフォーマッタは、既定のフォーマッタコレクションに含まれていないため、応答本文を読み取るときに指定する必要があります。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

次の例では、BSON を含む POST 要求を送信する方法を示します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

このコードの大部分は、前の例と同じです。 しかし、 **Postasync**メソッドでは、フォーマッタとして**BsonMediaTypeFormatter**を指定します。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>最上位レベルのプリミティブ型のシリアル化

各 BSON ドキュメントは、キーと値のペアの一覧です。BSON 仕様では、整数や文字列など、1つの生の値をシリアル化するための構文は定義されていません。

この制限を回避するために、 **BsonMediaTypeFormatter**はプリミティブ型を特殊なケースとして扱います。 シリアル化する前に、キー "Value" を使用して値をキーと値のペアに変換します。 たとえば、API コントローラーから整数が返されるとします。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

シリアル化する前に、BSON フォーマッタはこれを次のキーと値のペアに変換します。

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

逆シリアル化すると、フォーマッタはデータを元の値に変換します。 ただし、web API から生の値が返された場合、別の BSON パーサーを使用するクライアントはこのケースを処理する必要があります。 一般に、未加工の値ではなく、構造化されたデータを返すことを検討する必要があります。

## <a name="additional-resources"></a>その他の資料

[Web API の BSON サンプル](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[メディアフォーマッタ](media-formatters.md)
