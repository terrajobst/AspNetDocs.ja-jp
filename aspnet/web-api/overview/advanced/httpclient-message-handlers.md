---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API の HttpClient メッセージハンドラー-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x で ASP.NET Web API 用のカスタムメッセージハンドラーを作成する
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449278"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 内の HttpClient メッセージハンドラー

[Mike Wasson](https://github.com/MikeWasson)

*メッセージハンドラー*は、http 要求を受け取り、http 応答を返すクラスです。

通常、一連のメッセージハンドラーが連結されます。 最初のハンドラーは HTTP 要求を受け取り、何らかの処理を行い、次のハンドラーに要求を渡します。 ある時点で、応答が作成され、チェーンがバックアップされます。 このパターンは、*デリゲート*ハンドラーと呼ばれます。

![](httpclient-message-handlers/_static/image1.png)

クライアント側では、 **Httpclient**クラスはメッセージハンドラーを使用して要求を処理します。 既定のハンドラーは**Httpclienthandler**であり、ネットワーク経由で要求を送信し、サーバーからの応答を取得します。 クライアントパイプラインにカスタムメッセージハンドラーを挿入できます。

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> ASP.NET Web API は、サーバー側でもメッセージハンドラーを使用します。 詳細については、「 [HTTP メッセージハンドラー](http-message-handlers.md)」を参照してください。

## <a name="custom-message-handlers"></a>カスタムメッセージハンドラー

カスタムメッセージハンドラーを作成するには、 **DelegatingHandler**から派生させ、 **sendasync**メソッドをオーバーライドします。 このメソッド シグネチャを次に示します。

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

このメソッドは、 **HttpRequestMessage**を入力として受け取り、非同期的に**HttpResponseMessage**を返します。 一般的な実装では、次のことを行います。

1. 要求メッセージを処理します。
2. `base.SendAsync` を呼び出して、要求を内部ハンドラーに送信します。
3. 内部ハンドラーは、応答メッセージを返します。 (この手順は非同期です)。
4. 応答を処理し、呼び出し元に返します。

次の例は、送信要求にカスタムヘッダーを追加するメッセージハンドラーを示しています。

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

`base.SendAsync` の呼び出しは非同期です。 この呼び出しの後でハンドラーが何らかの処理を実行する場合は、 **await**キーワードを使用して、メソッドの完了後に実行を再開します。 次の例は、エラーコードをログに記録するハンドラーを示しています。 ログ自体はあまり興味深いものではありませんが、この例では、ハンドラー内の応答を取得する方法を示しています。

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>クライアントパイプラインへのメッセージハンドラーの追加

**Httpclient**にカスタムハンドラーを追加するには、 **HttpClientFactory**メソッドを使用します。

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

メッセージハンドラーは、 **Create**メソッドに渡す順序で呼び出されます。 ハンドラーは入れ子になっているため、応答メッセージは別の方向に移動します。 つまり、最後のハンドラーは、応答メッセージを取得するための最初のハンドラーです。
