---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: SignalR Tracing の有効化 |Microsoft Docs
author: bradygaster
description: このドキュメントでは、SignalR サーバーとクライアントのトレースを有効にして構成する方法について説明します。 トレースを使用すると、イベントに関する診断情報を表示できます...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467440"
---
# <a name="enabling-signalr-tracing"></a>SignalR トレースを有効にする

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、SignalR サーバーとクライアントのトレースを有効にして構成する方法について説明します。 トレースを使用すると、SignalR アプリケーションのイベントに関する診断情報を表示できます。
>
> このトピックは、最初は、パトリック Fletcher によって作成されました。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR バージョン2
>
>
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

トレースを有効にすると、SignalR アプリケーションによってイベントのログエントリが作成されます。 クライアントとサーバーの両方からイベントをログに記録できます。 サーバー上のトレースでは、接続、スケールアウトプロバイダー、およびメッセージバスイベントがログに記録されます。 クライアントでのトレースでは、接続イベントがログに記録されます。 SignalR 2.1 以降では、クライアントのトレースによってハブ呼び出しメッセージの完全な内容がログに記録されます。

## <a name="contents"></a>内容

- [サーバーでトレースを有効にする](#server)

    - [サーバーイベントをテキストファイルに記録する](#server_text)
    - [イベントログへのサーバーイベントのログ記録](#server_eventlog)
- [.NET クライアントでのトレースの有効化 (Windows デスクトップアプリ)](#net_client)

    - [コンソールへのデスクトップクライアントイベントのログ記録](#desktop_console)
    - [デスクトップクライアントのイベントをテキストファイルに記録する](#desktop_text)
- [Windows Phone 8 クライアントでトレースを有効にする](#phone)

    - [UI への Windows Phone クライアントイベントのログ記録](#phone_ui)
    - [デバッグコンソールへの Windows Phone クライアントイベントのログ記録](#phone_debug)
- [JavaScript クライアントでのトレースの有効化](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>サーバーでトレースを有効にする

アプリケーションの構成ファイル内のサーバーでトレースを有効にします (プロジェクトの種類に応じて App.config または web.config のいずれか)。ログに記録するイベントのカテゴリを指定します。 構成ファイルでは、 [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)の実装を使用して、イベントをテキストファイル、Windows イベントログ、またはカスタムログに記録するかどうかも指定します。

サーバーイベントカテゴリには、次のような種類のメッセージが含まれます。

| source | メッセージ |
| --- | --- |
| SignalR | SQL メッセージバスのスケールアウトプロバイダーのセットアップ、データベース操作、エラー、およびタイムアウトイベント |
| SignalR. ServiceBusMessageBus | Service bus スケールアウトプロバイダーのトピックの作成とサブスクリプション、エラー、およびメッセージングイベント |
| SignalR.RedisMessageBus | Redis スケールアウトプロバイダーの接続、切断、およびエラーイベント |
| SignalR.ScaleoutMessageBus | スケールアウトメッセージングイベント |
| SignalR.Transports.WebSocketTransport | WebSocket トランスポート接続、切断、メッセージング、およびエラーイベント |
| SignalR.Transports.ServerSentEventsTransport | Server送信イベントトランスポート接続、切断、メッセージング、およびエラーイベント |
| SignalR.Transports.ForeverFrameTransport | 事前にフレーム転送接続、切断、メッセージング、およびエラーイベントを送信する |
| SignalR.Transports.LongPollingTransport | LongPolling トランスポート接続、切断、メッセージング、およびエラーイベント |
| SignalR.Transports.TransportHeartBeat | Transport 接続、切断、および keepalive イベント |
| SignalR.ReflectedHubDescriptorProvider | ハブ検出イベント |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>サーバーイベントをテキストファイルに記録する

次のコードは、イベントの各カテゴリのトレースを有効にする方法を示しています。 このサンプルでは、イベントをテキストファイルに記録するようにアプリケーションを構成します。

**トレースを有効にするための XML サーバーコード**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

上記のコードでは、`SignalRSwitch` エントリは、指定されたログに送信されるイベントに使用される[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx)を指定します。 この場合、これは `Verbose` に設定されます。これは、すべてのデバッグメッセージとトレースメッセージがログに記録されることを意味します。

次の出力は、上の構成ファイルを使用するアプリケーションの `transports.log.txt` ファイルのエントリを示しています。 新しい接続、削除された接続、およびトランスポートハートビートイベントが表示されます。

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>イベントログへのサーバーイベントのログ記録

テキストファイルではなくイベントログにイベントを記録するには、[`sharedListeners`] ノードのエントリの値を変更します。 次のコードは、サーバーイベントをイベントログに記録する方法を示しています。

**イベントログにイベントを記録するための XML サーバーコード**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

次に示すように、イベントはアプリケーションログに記録され、イベントビューアーを通じて使用できます。

![SignalR ログを示すイベントビューアー](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> イベントログを使用する場合は、 **TraceLevel**を**Error**に設定して、メッセージの数を管理可能な状態にします。

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>.NET クライアントでのトレースの有効化 (Windows デスクトップアプリ)

.NET クライアントは、 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)の実装を使用して、イベントをコンソール、テキストファイル、またはカスタムログに記録できます。

.NET クライアントでログ記録を有効にするには、接続の `TraceLevel` プロパティを[TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx)値に設定し、`TraceWriter` プロパティを有効な[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)インスタンスに設定します。

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>コンソールへのデスクトップクライアントイベントのログ記録

次C#のコードは、.net クライアントのイベントをコンソールに記録する方法を示しています。

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>デスクトップクライアントのイベントをテキストファイルに記録する

次C#のコードは、.net クライアントのイベントをテキストファイルに記録する方法を示しています。

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

次の出力は、上の構成ファイルを使用するアプリケーションの `ClientLog.txt` ファイルのエントリを示しています。 サーバーに接続しているクライアントと、`addMessage`と呼ばれるクライアントメソッドを呼び出すハブが表示されます。

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Windows Phone 8 クライアントでトレースを有効にする

Windows Phone アプリ用の SignalR アプリケーションでは、デスクトップアプリと同じ .NET クライアントが使用されますが、[コンソールの Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)と、 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)を使用したファイルへの書き込みは使用できません。 代わりに、トレース用に[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)のカスタム実装を作成する必要があります。

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>UI への Windows Phone クライアントイベントのログ記録

[SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip)には、`TextBlockWriter`と呼ばれるカスタムの[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)実装を使用して、トレース出力を[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)に書き込む Windows Phone サンプルが含まれています。 このクラスは、 **samples/SignalR**プロジェクトにあります。このクラスは、WP8 プロジェクトにあります。 `TextBlockWriter`のインスタンスを作成するときに、現在の[SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)と、トレース出力に使用する[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)を作成する[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)を渡します。

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

次に、渡された[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)に作成された新しい[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)にトレース出力が書き込まれます。

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>デバッグコンソールへの Windows Phone クライアントイベントのログ記録

出力を UI ではなくデバッグコンソールに送信するには、[デバッグ] ウィンドウに書き込む[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)の実装を作成し、接続の[tracewriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx)プロパティに割り当てます。

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

トレース情報は、Visual Studio の [デバッグ] ウィンドウに書き込まれます。

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>JavaScript クライアントでのトレースの有効化

接続でクライアント側のログ記録を有効にするには、接続オブジェクトの `logging` プロパティを設定してから、`start` メソッドを呼び出して接続を確立します。

**ブラウザーコンソールへのトレースを有効にするためのクライアント JavaScript コード (生成されたプロキシを使用)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**ブラウザーコンソールへのトレースを有効にするためのクライアント JavaScript コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

トレースが有効になっている場合、JavaScript クライアントは、ブラウザーコンソールにイベントを記録します。 ブラウザーコンソールにアクセスするには、「 [Monitoring トランスポート](../getting-started/introduction-to-signalr.md#MonitoringTransports)」を参照してください。

次のスクリーンショットは、トレースが有効になっている SignalR JavaScript クライアントを示しています。 次の図は、ブラウザーコンソールでの接続とハブの呼び出しイベントを示しています。

![ブラウザーコンソールでの SignalR トレースイベント](enabling-signalr-tracing/_static/image4.png)
