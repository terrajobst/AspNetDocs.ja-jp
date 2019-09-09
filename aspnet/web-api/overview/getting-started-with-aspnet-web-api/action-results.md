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
# <a name="action-results-in-web-api-2"></a>Web API 2 のアクションの結果

このトピックでは、ASP.NET Web API がコントローラーアクションからの戻り値を HTTP 応答メッセージに変換する方法について説明します。

Web API コントローラーアクションは、次のいずれかを返すことができます。

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. その他の型

これらのどちらが返されるかに応じて、Web API は異なるメカニズムを使用して HTTP 応答を作成します。

| 戻り値の型 | Web API による応答の作成方法 |
| --- | --- |
| void | 空の204を返す (コンテンツなし) |
| **HttpResponseMessage** | HTTP 応答メッセージに直接変換します。 |
| **IHttpActionResult** | **HttpResponseMessage**を作成して HTTP 応答メッセージに変換するには、 **executeasync**を呼び出します。 |
| その他の型 | シリアル化された戻り値を応答本文に書き込みます。200 (OK) を返します。 |

このトピックの残りの部分では、各オプションについて詳しく説明します。

## <a name="void"></a>void

戻り値の型が`void`の場合、Web API は、ステータスコード 204 (コンテンツなし) の空の HTTP 応答を単純に返します。

コントローラーの例:

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP 応答:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

アクションが[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)を返す場合、Web API は、 **HttpResponseMessage**オブジェクトのプロパティを使用して応答を設定し、戻り値を直接 HTTP 応答メッセージに変換します。

このオプションを使用すると、応答メッセージを細かく制御できます。 たとえば、次のコントローラーアクションは Cache-control ヘッダーを設定します。

[!code-csharp[Main](action-results/samples/sample3.cs)]

応答 :

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

ドメインモデルを**CreateResponse**メソッドに渡すと、Web API は[メディアフォーマッタ](../formats-and-model-binding/media-formatters.md)を使用して、シリアル化されたモデルを応答本文に書き込みます。

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API では、要求の Accept ヘッダーを使用してフォーマッタを選択します。 詳細については、「[コンテンツネゴシエーション](../formats-and-model-binding/content-negotiation.md)」を参照してください。

## <a name="ihttpactionresult"></a>IHttpActionResult

**Ihttpactionresult**インターフェイスは、Web API 2 で導入されました。 基本的には、 **HttpResponseMessage**ファクトリを定義します。 **Ihttpactionresult**インターフェイスを使用すると、次のような利点があります。

- コントローラーの[単体テスト](../testing-and-debugging/unit-testing-controllers-in-web-api.md)を簡略化します。
- HTTP 応答を作成するための共通のロジックを別のクラスに移動します。
- 応答を構築するための下位レベルの詳細を非表示にすることにより、コントローラーアクションの目的を明確にします。

**Ihttpactionresult**には、 **executeasync**という1つのメソッドが含まれています。このメソッドは、非同期的に**HttpResponseMessage**インスタンスを作成します。

[!code-csharp[Main](action-results/samples/sample6.cs)]

コントローラーアクションが**Ihttpactionresult**を返す場合、Web API は**executeasync**メソッドを呼び出して**HttpResponseMessage**を作成します。 次に、 **HttpResponseMessage**を HTTP 応答メッセージに変換します。

次に示すのは、プレーンテキスト応答を作成する**Ihttpactionresult**の単純な実装です。

[!code-csharp[Main](action-results/samples/sample7.cs)]

コントローラーアクションの例:

[!code-csharp[Main](action-results/samples/sample8.cs)]

応答 :

[!code-console[Main](action-results/samples/sample9.cmd)]

多くの場合、名前空間に定義されている**Ihttpactionresult**実装を使用 **[します。](https://msdn.microsoft.com/library/system.web.http.results.aspx)** **ApiController**クラスは、これらの組み込みアクションの結果を返すヘルパーメソッドを定義します。

次の例では、要求が既存の製品 ID と一致しない場合、コントローラーは[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)を呼び出して 404 (見つかりません) 応答を作成します。 それ以外の場合、コントローラーは ApiController を呼び出します。これにより、製品を含む 200 (OK) の応答が作成され[ます。](https://msdn.microsoft.com/library/dn314591.aspx)

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>その他の戻り値の型

その他のすべての戻り値の型では、Web API は[メディアフォーマッタ](../formats-and-model-binding/media-formatters.md)を使用して戻り値をシリアル化します。 Web API は、シリアル化された値を応答本文に書き込みます。 応答状態コードは 200 (OK) です。

[!code-csharp[Main](action-results/samples/sample11.cs)]

この方法の欠点は、404などのエラーコードを直接返すことができないことです。 ただし、エラーコードの**HttpResponseException**をスローすることはできます。 詳細については、「 [ASP.NET Web API での例外処理](../error-handling/exception-handling.md)」を参照してください。

Web API では、要求の Accept ヘッダーを使用してフォーマッタを選択します。 詳細については、「[コンテンツネゴシエーション](../formats-and-model-binding/content-negotiation.md)」を参照してください。

要求の例

[!code-console[Main](action-results/samples/sample12.cmd)]

応答の例

[!code-console[Main](action-results/samples/sample13.cmd)]
