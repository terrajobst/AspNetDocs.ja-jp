---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2 でのグローバルエラー処理-ASP.NET 4.x
author: davidmatson
description: ASP.NET 4.x の ASP.NET Web API 2 でのグローバルエラー処理の概要について説明します。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 94f2d6d31d0b37f9bb0077e6258c70a2dfb1918d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448966"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 でのグローバルエラー処理

[David Matson](https://github.com/davidmatson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)

このトピックでは、ASP.NET 4.x の ASP.NET Web API 2 でのグローバルエラー処理の概要について説明します。 現在、Web API では、エラーをグローバルに記録または処理する簡単な方法はありません。 一部のハンドルされない例外は[例外フィルター](exception-handling.md)を使用して処理できますが、例外フィルターが処理できないケースがいくつかあります。 次に例を示します。

1. コントローラー コンストラクターからスローされる例外。
2. メッセージ ハンドラーからスローされる例外。
3. ルーティング中にスローされる例外。
4. 応答コンテンツのシリアル化中にスローされる例外。

これらの例外をログに記録して処理するための、簡単で一貫性のある方法を提供したいと考えています。 

例外処理の主なケースとしては、エラー応答を送信できるケースと、例外をログに記録することだけが可能なケースがあります。 後者の場合の例として、ストリーミング応答コンテンツの途中で例外がスローされた場合があります。この場合は、状態コード、ヘッダー、部分的な内容が既にネットワーク経由で送信されているため、新しい応答メッセージを送信するには遅すぎます。そのため、単に接続を中止します。 新しい応答メッセージを生成するために例外を処理することはできませんが、例外のログ記録は引き続きサポートされています。 エラーを検出できる場合は、次に示すように、適切なエラー応答を返すことができます。

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>既存のオプション

[例外フィルター](exception-handling.md)に加えて、[メッセージハンドラー](../advanced/http-message-handlers.md)を使用して500レベルのすべての応答を確認できますが、元のエラーに関するコンテキストがないため、これらの応答に対して動作するのは困難です。 また、メッセージハンドラーには、処理できるケースに関する例外フィルターと同じ制限事項がいくつかあります。Web API には、エラー状態をキャプチャするトレースインフラストラクチャがありますが、トレースインフラストラクチャは診断のためのものであり、実稼働環境での実行には適していません。 グローバルな例外処理とログ記録は、運用中に実行できるサービスであり、既存の監視ソリューション ( [ELMAH](https://code.google.com/p/elmah/)など) に接続されている必要があります。

### <a name="solution-overview"></a>ソリューションの概要

 未処理の例外をログに記録して処理するために、 [Iexceptionlogger](../releases/whats-new-in-aspnet-web-api-21.md)と Iexceptionlogger という2つの新しいユーザー置き換え可能なサービスを提供しています。 これらのサービスは非常によく似ていますが、主に2つの違いがあります。

1. 複数の例外ロガーの登録はサポートしていますが、例外ハンドラーは1つだけです。
2. 接続を中止しようとしている場合でも、例外ロガーは常に呼び出されます。 例外ハンドラーは、送信する応答メッセージを選択できる場合にのみ呼び出されます。

どちらのサービスも、例外が検出されたポイントからの関連情報 (特に、 [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)、 [httprequestcontext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)、スローされた例外、例外ソース (以下の詳細) を含む) を含む例外コンテキストへのアクセスを提供します。

### <a name="design-principles"></a>設計原則

1. **互換性に影響する変更はありません**この機能はマイナーリリースで追加されているため、ソリューションに影響を与える重要な制約の1つは、コントラクトまたは動作に種類を指定するための重大な変更がないことです。 この制約は、例外を500の応答に変換する既存の catch ブロックの観点から実行する必要のあるクリーンアップを除外します。 この追加のクリーンアップは、後続のメジャーリリースで検討することができます。 これが重要な場合は、 [ASP.NET Web API ユーザーの声](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)で投票してください。
2. **WEB API コンストラクトとの一貫性の維持**Web API のフィルターパイプラインは、アクション固有のコントローラー固有またはグローバルスコープでロジックを適用する柔軟性により、横断的な懸念を処理する優れた方法です。 例外フィルターを含むフィルターには、グローバルスコープで登録されている場合でも、常にアクションおよびコントローラーコンテキストがあります。 このコントラクトはフィルターにとって理にかなっていますが、例外フィルターはグローバルにスコープが設定されている場合でも、メッセージハンドラーからの例外 (アクションやコントローラーコンテキストが存在しないなど) には適していないことを意味します。 例外処理のためにフィルターによる柔軟なスコープ設定を使用する場合でも、例外フィルターが必要です。 ただし、コントローラーコンテキストの外部で例外を処理する必要がある場合は、完全なグローバルエラー処理 (コントローラーコンテキストとアクションコンテキスト制約のないもの) に対して個別の構成要素も必要になります。

### <a name="when-to-use"></a>使用する場合

- 例外ロガーは、Web API でキャッチされた未処理の例外をすべて表示するためのソリューションです。
- 例外ハンドラーは、Web API でキャッチされた未処理の例外に対して可能なすべての応答をカスタマイズするためのソリューションです。
- 例外フィルターは、特定のアクションまたはコントローラーに関連するハンドルされない例外を処理するための最も簡単なソリューションです。

### <a name="service-details"></a>サービスの詳細

 例外ロガーとハンドラーサービスインターフェイスは、それぞれのコンテキストを取得する単純な非同期メソッドです。 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 また、これらのインターフェイスの両方に基本クラスを用意しています。 コア (同期または非同期) メソッドのオーバーライドは、推奨される時刻にログ記録または処理を行うために必要です。 ログ記録のために、`ExceptionLogger` の基本クラスでは、コアログメソッドが例外ごとに1回だけ呼び出されるようにします (後でコールスタックの上位に伝達して、再びキャッチする場合でも)。 `ExceptionHandler` 基底クラスは、呼び出し履歴の一番上にある例外に対してのみコア処理メソッドを呼び出し、従来の入れ子になった catch ブロックを無視します。 (これらの基本クラスの簡略化されたバージョンについては、以下の付録を参照してください)。`IExceptionLogger` と `IExceptionHandler` はどちらも `ExceptionContext`を介して例外に関する情報を受け取ります。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

フレームワークが例外ロガーまたは例外ハンドラーを呼び出すと、常に `Exception` と `Request`が提供されます。 単体テスト以外にも、常に `RequestContext`が提供されます。 `ControllerContext` と `ActionContext` が提供されることはほとんどありません (例外フィルターの catch ブロックからを呼び出す場合のみ)。 `Response`が提供されることはほとんどありません (応答を書き込もうとしているときに、特定の IIS の場合のみ)。 これらのプロパティの一部は `null` 可能性があるため、例外クラスのメンバーにアクセスする前に、コンシューマーが `null` を確認する必要があります。`CatchBlock` 例外を検出した catch ブロックを示す文字列を指定します。 Catch ブロック文字列は次のとおりです。

- HttpServer (SendAsync メソッド)
- Httpコントローラーディスパッチャー (SendAsync メソッド)
- HttpBatchHandler (SendAsync メソッド)
- IExceptionFilter (ExecuteAsync での例外フィルターパイプラインの ApiController の処理)
- ホストの OWIN:

    - HttpmessageBufferResponseContentAsync (出力のバッファリング用)
    - HttpmessageCopyResponseContentAsync (ストリーミング出力用)
- Web ホスト:

    - Httpsystem.web.http.webhost.httpcontrollerhandler.writebufferedresponsecontentasync (出力のバッファリング用)
    - Httpsystem.web.http.webhost.httpcontrollerhandler.writestreamedresponsecontentasync (出力のストリーミング用)
    - Httpsystem.web.http.webhost.httpcontrollerhandler.writeerrorresponsecontentasync (バッファー出力モードでのエラー復旧エラー用)

Catch ブロック文字列の一覧は、静的な読み取り専用プロパティでも使用できます。 (コア catch ブロック文字列は静的な System.web.http.exceptionhandling.exceptioncatchblocks.httpserver.sendasync 上にあります。剰余は、OWIN と web ホストのそれぞれに対して1つの静的クラスに表示されます)。`IsTopLevelCatchBlock` は、呼び出し履歴の一番上でのみ例外を処理することをお勧めします。 入れ子になった catch ブロックが発生するたびに例外を500応答に変換するのではなく、例外ハンドラーによって、ホストに表示されるまで例外を反映させることができます。

ロガーは、`ExceptionContext`に加えて、完全な `ExceptionLoggerContext`を介して1つ以上の情報を取得します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

2番目のプロパティである `CanBeHandled`を使用すると、処理できない例外を logger で識別できます。 接続を中止しようとしているときに、新しい応答メッセージを送信できない場合、ロガーは呼び出されますが、ハンドラーは呼び出さ***れず、*** logger はこのプロパティからこのシナリオを識別できます。

`ExceptionContext`に加えて、ハンドラーは、例外を処理するために、完全な `ExceptionHandlerContext` に設定できるもう1つのプロパティを取得します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

例外ハンドラーは、`Result` プロパティをアクションの結果 ( [Exceptionresult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx)、 [internalservererrorresult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)、 [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)、またはカスタム結果) に設定することによって例外を処理したことを示します。 `Result` プロパティが null の場合、例外は処理されないため、元の例外が再スローされます。

呼び出し履歴の一番上にある例外については、API 呼び出し元に対して応答が適切であることを確認するための追加の手順を実行しました。 例外がホストに伝達されると、呼び出し元には、死亡の黄色の画面、または通常は HTML であり、通常は適切な API エラー応答ではないその他のホスト提供の応答が表示されます。 このような場合、結果は null 以外の値から開始されます。また、カスタム例外ハンドラーが明示的に `null` (未処理) に設定した場合にのみ、例外がホストに反映されます。 このような場合に `Result` を `null` に設定すると、次の2つのシナリオで役に立ちます。

1. Web API の前/外側に登録されたカスタム例外処理ミドルウェアを使用して、OWIN にホストされる Web API を作成します。
2. ブラウザーを使用したローカルデバッグ。これは、実際には、ハンドルされない例外が発生した場合に、実際には、死亡の黄色い画面が役に立つ応答です。

例外ロガーと例外ハンドラーの両方について、logger またはハンドラー自体が例外をスローする場合、復旧するものはありません。 (例外が反映されないように、より適切な方法を使用している場合は、このページの下部にフィードバックを残してください。)例外ロガーとハンドラーのコントラクトは、例外が呼び出し元に伝達されないようにする必要があるということです。そうしないと、多くの場合、例外が伝達されます。これは、多くの場合、ホストに対して HTML エラー (ASP など) が発生します。ネットワークの黄色の画面) がクライアントに送り返されます (通常、JSON または XML を想定している API の呼び出し元では、このオプションは推奨されません)。

## <a name="examples"></a>例

### <a name="tracing-exception-logger"></a>トレース例外ロガー

次の例外ロガーは、構成されたトレースソース (Visual Studio の [デバッグ出力] ウィンドウを含む) に例外データを送信します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>カスタムエラーメッセージ例外ハンドラー

次の例では、サポートに連絡するための電子メールアドレスを含む、クライアントに対するカスタムエラー応答を生成します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>登録 (例外フィルターを)

"ASP.NET MVC 4 Web アプリケーション" プロジェクトテンプレートを使用してプロジェクトを作成する場合は、Web API 構成コードを `WebApiConfig` クラス内の*App/_Start*フォルダーに配置します。

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>付録: 基本クラスの詳細

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
