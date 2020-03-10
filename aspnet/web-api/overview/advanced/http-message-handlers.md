---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API の HTTP メッセージハンドラー-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API での HTTP メッセージハンドラーの概要
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504928"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API の HTTP メッセージハンドラー

[Mike Wasson](https://github.com/MikeWasson)

*メッセージハンドラー*は、http 要求を受け取り、http 応答を返すクラスです。 メッセージハンドラーは、抽象**Httpmessagehandler**クラスから派生します。

通常、一連のメッセージハンドラーが連結されます。 最初のハンドラーは HTTP 要求を受け取り、何らかの処理を行い、次のハンドラーに要求を渡します。 ある時点で、応答が作成され、チェーンがバックアップされます。 このパターンは、*デリゲート*ハンドラーと呼ばれます。

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>サーバー側のメッセージハンドラー

サーバー側では、Web API パイプラインはいくつかの組み込みメッセージハンドラーを使用します。

- **HttpServer**は、ホストから要求を取得します。
- **HttpRoutingDispatcher**は、ルートに基づいて要求をディスパッチします。
- **Httpcontroller ディスパッチャー**は、要求を Web API コントローラーに送信します。

パイプラインにカスタムハンドラーを追加できます。 メッセージハンドラーは、(コントローラーアクションではなく) HTTP メッセージレベルで動作する横断的な懸念に適しています。 たとえば、次のようなメッセージハンドラーがあるとします。

- 要求ヘッダーを読み取りまたは変更します。
- 応答ヘッダーを応答に追加します。
- コントローラーに到着する前に、要求を検証します。

次の図は、パイプラインに挿入された2つのカスタムハンドラーを示しています。

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> クライアント側では、HttpClient はメッセージハンドラーも使用します。 詳細については、「 [Httpclient メッセージハンドラー](httpclient-message-handlers.md)」を参照してください。

## <a name="custom-message-handlers"></a>カスタムメッセージハンドラー

カスタムメッセージハンドラーを作成するには、 **DelegatingHandler**から派生させ、 **sendasync**メソッドをオーバーライドします。 このメソッドのシグネチャは次のとおりです。

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

このメソッドは、 **HttpRequestMessage**を入力として受け取り、非同期的に**HttpResponseMessage**を返します。 一般的な実装では、次のことを行います。

1. 要求メッセージを処理します。
2. `base.SendAsync` を呼び出して、要求を内部ハンドラーに送信します。
3. 内部ハンドラーは、応答メッセージを返します。 (この手順は非同期です)。
4. 応答を処理し、呼び出し元に返します。

単純な例を次に示します。

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> `base.SendAsync` の呼び出しは非同期です。 この呼び出しの後でハンドラーが何らかの処理を実行する場合は、次に示すように**await**キーワードを使用します。

デリゲートハンドラーは、内部ハンドラーをスキップし、直接応答を作成することもできます。

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

デリゲートハンドラーが `base.SendAsync`を呼び出さずに応答を作成した場合、要求はパイプラインの残りの部分をスキップします。 これは、要求を検証するハンドラー (エラー応答の作成) に役立ちます。

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>パイプラインへのハンドラーの追加

サーバー側にメッセージハンドラーを追加するには、ハンドラーを**Httpconfiguration. messagehandlers**コレクションに追加します。 "ASP.NET MVC 4 Web アプリケーション" テンプレートを使用してプロジェクトを作成した場合は、 **webapiconfig.cs**クラス内でこれを行うことができます。

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

メッセージハンドラーは、 **messagehandlers**コレクションに表示される順序と同じ順序で呼び出されます。 入れ子になっているため、応答メッセージは別の方向に移動します。 つまり、最後のハンドラーは、応答メッセージを取得するための最初のハンドラーです。

内部ハンドラーを設定する必要がないことに注意してください。Web API フレームワークは、メッセージハンドラーを自動的に接続します。

[自己ホスト](../older-versions/self-host-a-web-api.md)している場合は、 **Httpselfhostconfiguration**クラスのインスタンスを作成し、そのハンドラーを**messagehandlers**コレクションに追加します。

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

次に、カスタムメッセージハンドラーの例をいくつか見てみましょう。

## <a name="example-x-http-method-override"></a>例: X-y-Override

-HTTP メソッドオーバーライドは、非標準の HTTP ヘッダーです。 これは、PUT や DELETE など、特定の種類の HTTP 要求を送信できないクライアント向けに設計されています。 代わりに、クライアントは POST 要求を送信し、X-y-Override ヘッダーを目的のメソッドに設定します。 次に例を示します。

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

次に示すのは、X-HTTP メソッドオーバーライドのサポートを追加するメッセージハンドラーです。

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

**Sendasync**メソッドでは、ハンドラーは、要求メッセージが POST 要求であるかどうか、およびそのメッセージに HTTP メソッドオーバーライドヘッダーが含まれているかどうかを確認します。 その場合は、ヘッダー値を検証してから、要求メソッドを変更します。 最後に、ハンドラーは `base.SendAsync` を呼び出して、メッセージを次のハンドラーに渡します。

要求が**Httpコントローラーディスパッチャー**クラスに到達すると、 **httpコントローラーディスパッチャー**は、更新された要求メソッドに基づいて要求をルーティングします。

## <a name="example-adding-a-custom-response-header"></a>例: カスタム応答ヘッダーの追加

次に示すのは、すべての応答メッセージにカスタムヘッダーを追加するメッセージハンドラーです。

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

まず、ハンドラーは `base.SendAsync` を呼び出して、要求を内部メッセージハンドラーに渡します。 内部ハンドラーは応答メッセージを返しますが、**タスク&lt;t&gt;** オブジェクトを使用して非同期的に処理します。 応答メッセージは、`base.SendAsync` が非同期に完了するまで使用できません。

この例では、 **await**キーワードを使用して `SendAsync` の完了後に非同期に作業を実行します。 .NET Framework 4.0 を対象としている場合は、&lt;T&gt;**タスク**を使用し**ます。System.threading.tasks.task.continuewith**メソッド:

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>例: API キーの確認

一部の web サービスでは、クライアントが要求に API キーを含める必要があります。 次の例は、メッセージハンドラーが有効な API キーの要求を確認する方法を示しています。

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

このハンドラーは、URI クエリ文字列内の API キーを検索します。 (この例では、キーが静的な文字列であると想定しています。 実際の実装では、より複雑な検証を使用する可能性があります)。クエリ文字列にキーが含まれている場合、ハンドラーは内部ハンドラーに要求を渡します。

要求に有効なキーがない場合、ハンドラーは状態が403である応答メッセージを作成します。 この場合、ハンドラーは `base.SendAsync`を呼び出さないため、内部ハンドラーは要求を受信せず、コントローラーも受け入れません。 したがって、コントローラーは、すべての受信要求に有効な API キーがあると見なすことができます。

> [!NOTE]
> API キーが特定のコントローラーアクションにのみ適用される場合は、メッセージハンドラーの代わりにアクションフィルターを使用することを検討してください。 アクションフィルターは、URI ルーティングが実行された後に実行されます。

## <a name="per-route-message-handlers"></a>ルートごとのメッセージハンドラー

**Httpconfiguration. MessageHandlers**コレクション内のハンドラーはグローバルに適用されます。

または、ルートを定義するときに、特定のルートにメッセージハンドラーを追加することもできます。

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

この例では、要求 URI が "Route2" に一致する場合、要求は `MessageHandler2`にディスパッチされます。 次の図は、これらの2つのルートのパイプラインを示しています。

![](http-message-handlers/_static/image4.png)

既定の**Httpコントローラーディスパッチャー**が `MessageHandler2` に置き換わることに注意してください。 この例では、`MessageHandler2` によって応答が作成され、"Route2" に一致する要求はコントローラーに送られません。 これにより、Web API コントローラーのメカニズム全体を独自のカスタムエンドポイントに置き換えることができます。

もう1つの方法として、ルートごとのメッセージハンドラーは**httpcontroller ディスパッチャー**に委任できます。これにより、コントローラーにディスパッチされます。

![](http-message-handlers/_static/image5.png)

次のコードは、このルートを構成する方法を示しています。

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
