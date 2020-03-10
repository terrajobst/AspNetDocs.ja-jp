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
# <a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API でのコンテンツネゴシエーション

[Mike Wasson](https://github.com/MikeWasson)

この記事では、ASP.NET Web API が ASP.NET 4.x のコンテンツネゴシエーションを実装する方法について説明します。

HTTP 仕様 (RFC 2616) は、"使用可能な複数の表現がある場合に、特定の応答に対して最適な表現を選択するプロセス" としてコンテンツネゴシエーションを定義します。 HTTP でのコンテンツネゴシエーションの主要なメカニズムは、次の要求ヘッダーです。

- **同意:** 応答で許容されるメディアの種類 ("application/json"、"application/xml" など)、または &quot;application/vnd などのカスタムメディアの種類。例 + xml&quot;
- **Accept-Charset:** UTF-8 や ISO 8859-1 など、許容される文字セットを指定します。
- **Accept-Encoding:** Gzip など、許容されるコンテンツエンコーディング。
- **Accept-言語:** 適切な自然言語 ("en-us" など)。

サーバーは、HTTP 要求の他の部分を確認することもできます。 たとえば、要求に、AJAX 要求を示す "X 要求-With" ヘッダーが含まれている場合、Accept ヘッダーがない場合、サーバーでは既定で JSON が使用される可能性があります。

この記事では、Web API が Accept ヘッダーと Accept 文字セットヘッダーを使用する方法について説明します。 (現時点では、受け入れエンコードまたは受け入れ言語の組み込みサポートはありません)。

## <a name="serialization"></a>シリアル化

Web API コントローラーがリソースを CLR 型として返す場合、パイプラインは戻り値をシリアル化し、それを HTTP 応答の本文に書き込みます。

たとえば、次のコントローラーアクションを考えてみます。

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

クライアントは、次の HTTP 要求を送信する場合があります。

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

応答として、サーバーから次のメッセージが送信される可能性があります。

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

この例では、クライアントが JSON、Javascript、または "何か" を要求しました (\*/\*)。 サーバーが `Product` オブジェクトの JSON 表現で応答しました。 応答の Content-type ヘッダーが &quot;application/json&quot;に設定されていることに注意してください。

コントローラーは、 **HttpResponseMessage**オブジェクトを返すこともできます。 応答本文に CLR オブジェクトを指定するには、 **CreateResponse**拡張メソッドを呼び出します。

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

このオプションを使用すると、応答の詳細をより詳細に制御できます。 ステータスコードの設定、HTTP ヘッダーの追加などを行うことができます。

リソースをシリアル化するオブジェクトは、*メディアフォーマッタ*と呼ばれます。 メディアフォーマッタは、 **MediaTypeFormatter**クラスから派生します。 Web API には、XML および JSON 用のメディアフォーマッタが用意されています。また、他のメディアの種類をサポートするカスタムフォーマッタを作成することもできます。 カスタムフォーマッタの記述の詳細については、「[メディアフォーマッタ](media-formatters.md)」を参照してください。

## <a name="how-content-negotiation-works"></a>コンテンツネゴシエーションのしくみ

まず、パイプラインは**Httpconfiguration**オブジェクトから**IContentNegotiator**サービスを取得します。 また、 **Httpconfiguration. フォーマッタ**コレクションからメディアフォーマッタの一覧を取得します。

次に、パイプラインは**IContentNegotiator**を呼び出し、を渡します。

- シリアル化するオブジェクトの型。
- メディアフォーマッタのコレクション
- HTTP 要求

**Negotiate**メソッドは、次の2つの情報を返します。

- 使用するフォーマッタ
- 応答のメディアの種類

フォーマッタが見つからない場合、 **Negotiate**メソッドは**null**を返し、クライアントは HTTP エラー406を受信します (許容できません)。

次のコードは、コントローラーがコンテンツネゴシエーションを直接呼び出す方法を示しています。

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

このコードは、パイプラインによって自動的に行われる処理に相当します。

## <a name="default-content-negotiator"></a>既定のコンテンツ Negotiator

**DefaultContentNegotiator**クラスは、 **IContentNegotiator**の既定の実装を提供します。 複数の条件を使用してフォーマッタを選択します。

最初に、フォーマッタは型をシリアル化できる必要があります。 これは、 **MediaTypeFormatter**を呼び出すことによって検証されます。

次に、コンテンツ negotiator は各フォーマッタを確認し、HTTP 要求にどの程度一致しているかを評価します。 一致を評価するために、コンテンツ negotiator はフォーマッタに関して次の2つの点を確認します。

- **SupportedMediaTypes** collection。サポートされているメディアの種類の一覧が含まれています。 コンテンツ negotiator は、このリストを要求 Accept ヘッダーと照合しようとします。 Accept ヘッダーには範囲を含めることができることに注意してください。 たとえば、"text/plain" は、text/\* または \*/\*に一致します。
- **MediaTypeMappings** Collection。 **MediaTypeMapping**オブジェクトの一覧が含まれています。 **MediaTypeMapping**クラスは、HTTP 要求をメディアの種類と照合するための汎用的な方法を提供します。 たとえば、カスタム HTTP ヘッダーを特定のメディアの種類にマップすることができます。

複数の一致がある場合は、最高品質係数との一致が優先されます。 次に例を示します。

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

この例では、application/json には1.0 という暗黙の品質係数があるため、application/xml よりも優先されます。

一致するものが見つからない場合、コンテンツ negotiator は、要求本文のメディアの種類 (存在する場合) との照合を試みます。 たとえば、要求に JSON データが含まれている場合、コンテンツ negotiator は JSON フォーマッタを検索します。

一致するものがない場合、コンテンツ negotiator は、単純にその型をシリアル化できる最初のフォーマッタを選択します。

## <a name="selecting-a-character-encoding"></a>文字エンコードの選択

フォーマッタを選択すると、コンテンツ negotiator はフォーマッタの**SupportedEncodings**プロパティを確認し、要求のヘッダー (存在する場合) と照合することで、最適な文字エンコーディングを選択します。
