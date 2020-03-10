---
uid: signalr/overview/performance/signalr-performance
title: SignalR Performance |Microsoft Docs
author: bradygaster
description: SignalR パフォーマンス
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449860"
---
# <a name="signalr-performance"></a>SignalR パフォーマンス

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、SignalR アプリケーションのパフォーマンスを設計、測定、および向上させる方法について説明します。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR バージョン2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>このトピックの前のバージョン
>
> 以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

SignalR のパフォーマンスとスケーリングに関する最新のプレゼンテーションについては、「 [ASP.NET SignalR を使用したリアルタイム Web のスケーリング](https://channel9.msdn.com/Events/Build/2013/3-502)」を参照してください。

このトピックには、次のセクションが含まれます。

- [設計上の考慮事項](#design)
- [パフォーマンスを向上するための SignalR サーバーのチューニング](#tuning)
- [パフォーマンスの問題のトラブルシューティング](#troubleshooting)
- [SignalR パフォーマンスカウンターの使用](#perfcounters)
- [その他のパフォーマンスカウンターの使用](#othercounters)
- [その他のリソース](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>設計上の考慮事項

このセクションでは、不要なネットワークトラフィックを生成することによってパフォーマンスが阻害されないように、SignalR アプリケーションの設計時に実装できるパターンについて説明します。

### <a name="throttling-message-frequency"></a>メッセージ頻度の調整

高頻度 (リアルタイムゲームアプリケーションなど) でメッセージを送信するアプリケーションでも、ほとんどのアプリケーションでは、1秒間に数個を超えるメッセージを送信する必要がありません。 各クライアントによって生成されるトラフィックの量を減らすために、メッセージループを実装して、メッセージをキューに配置し、一定の頻度よりも頻繁にメッセージを送信しないようにすることができます (つまり、その時間内にメッセージがある場合は、1秒ごとにメッセージが送信されます)。送信される terval。 クライアントとサーバーの両方から特定の速度にメッセージを調整するサンプルアプリケーションについては、「 [SignalR を使用した高頻度のリアルタイム](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。

### <a name="reducing-message-size"></a>メッセージサイズの縮小

シリアル化されたオブジェクトのサイズを小さくすることで、SignalR メッセージのサイズを小さくすることができます。 サーバーコードで、送信する必要のないプロパティを含むオブジェクトを送信する場合は、`JsonIgnore` 属性を使用してこれらのプロパティをシリアル化できないようにします。 プロパティの名前もメッセージに格納されます。プロパティの名前は、`JsonProperty` 属性を使用して短縮できます。 次のコードサンプルは、プロパティをクライアントに送信しないようにする方法と、プロパティ名を短縮する方法を示しています。

**クライアントに送信されるデータから除外する JsonIgnore 属性と、メッセージサイズを減らすための Jsonignore 属性を示す .NET サーバーコード**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

クライアントコードで読みやすさと保守性を維持するために、省略されたプロパティ名は、メッセージの受信後にわかりやすい名前に再マップできます。 次のコードサンプルでは、メッセージコントラクト (マッピング) を定義し、`reMap` 関数を使用して最適化されたメッセージクラスにコントラクトを適用することによって、短い名前を長いものに再マップする方法の1つを示します。

**短縮されたプロパティ名を人間が判読できる名前に再マップするクライアント側の JavaScript コード**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

同じ方法を使用して、クライアントからサーバーへのメッセージでも名前を短縮できます。

メッセージオブジェクトのメモリフットプリント (つまり、メッセージに使用されるメモリの量) を減らすことで、パフォーマンスを向上させることもできます。 たとえば、`int` の範囲全体が不要な場合は、代わりに `short` または `byte` を使用できます。

メッセージはサーバーメモリ内のメッセージバスに格納されるため、メッセージのサイズを小さくすると、サーバーのメモリの問題に対処することもできます。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>パフォーマンスを向上するための SignalR サーバーのチューニング

SignalR アプリケーションでパフォーマンスを向上させるために、次の構成設定を使用してサーバーをチューニングできます。 ASP.NET アプリケーションのパフォーマンスを向上させる方法に関する一般的な情報については、「 [ASP.NET パフォーマンスの向上](https://msdn.microsoft.com/library/ff647787.aspx)」を参照してください。

**SignalR の構成設定**

- **Defaultmessagebuffersize**: 既定では、SignalR は、接続ごとに1000のメッセージを各ハブのメモリに保持します。 サイズの大きいメッセージが使用されている場合は、この値を小さくすることで緩和できるメモリの問題が発生する可能性があります。 この設定は、ASP.NET アプリケーションの `Application_Start` イベントハンドラー、または自己ホスト型アプリケーションの OWIN startup クラスの `Configuration` メソッドで設定できます。 次のサンプルでは、使用されるサーバーメモリの量を減らすために、アプリケーションのメモリフットプリントを削減するために、この値を小さくする方法を示します。

    **既定のメッセージバッファーサイズを減らすための Startup.cs の .NET サーバーコード**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 構成の設定**

- **アプリケーションあたりの最大同時要求**数: 同時 IIS 要求の数を増やすと、要求の処理に使用できるサーバーリソースが増加します。 既定値は5000です。この設定を増やすには、管理者特権のコマンドプロンプトで次のコマンドを実行します。

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: これは、アプリケーションプールの http.sys キューに対する要求の最大数です。 キューがいっぱいになると、新しい要求は 503 "サービスを利用できません" という応答を受信します。 既定値は 1000 です。

    アプリケーションをホストするアプリケーションプールでワーカープロセスのキューの長さを短くすると、メモリリソースが節約されます。 詳細については、「[アプリケーションプールの管理、チューニング、および構成](https://technet.microsoft.com/library/cc745955.aspx)」を参照してください。

**ASP.NET の構成設定**

このセクションには、`aspnet.config` ファイルで設定できる構成設定が含まれています。 このファイルは、プラットフォームに応じて、次の2つの場所のいずれかにあります。

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR のパフォーマンスを向上させる ASP.NET 設定には、次のようなものがあります。

- **CPU あたりの最大同時要求数**: この設定を増やすと、パフォーマンスのボトルネックが軽減される可能性があります。 この設定を増やすには、次の構成設定を `aspnet.config` ファイルに追加します。

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **要求キューの制限**: 接続の合計数が `maxConcurrentRequestsPerCPU` 設定を超えると、ASP.NET はキューを使用して要求の調整を開始します。 キューのサイズを大きくするには、`requestQueueLimit` 設定を大きくします。 これを行うには、次の構成設定を `config/machine.config` の `processModel` ノードに追加します (`aspnet.config`ではありません)。

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>パフォーマンスに関する問題のトラブルシューティング

ここでは、アプリケーションのパフォーマンスのボトルネックを検出する方法について説明します。

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket が使用されていることを確認しています

SignalR ではクライアントとサーバー間の通信にさまざまなトランスポートを使用できますが、WebSocket ではパフォーマンスが大幅に向上します。クライアントとサーバーがそれをサポートする場合は、この機能を使用する必要があります。 クライアントとサーバーが WebSocket の要件を満たしているかどうかを判断するには、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。 アプリケーションで使用されているトランスポートを確認するには、ブラウザー開発者ツールを使用し、ログを調べて、接続に使用されているトランスポートを確認します。 Internet Explorer と Chrome でブラウザー開発ツールを使用する方法の詳細については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR パフォーマンスカウンターの使用

このセクションでは、`Microsoft.AspNet.SignalR.Utils` パッケージに含まれる SignalR パフォーマンスカウンターを有効にして使用する方法について説明します。

### <a name="installing-signalrexe"></a>Signalr のインストール

パフォーマンスカウンターは、SignalR というユーティリティを使用してサーバーに追加できます。 このユーティリティをインストールするには、次の手順を実行します。

1. Visual Studio で、 **[ツール]**  >  **[nuget パッケージマネージャー]**  >  **[ソリューションの nuget パッケージの管理]** を選択します。
2. **Signalr**を検索し、[インストール] を選択します。

    ![](signalr-performance/_static/image1.png)
3. 使用許諾契約書に同意して、パッケージをインストールします。
4. SignalR は `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`にインストールされます。

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR を使用したパフォーマンスカウンターのインストール

SignalR パフォーマンスカウンターをインストールするには、管理者特権のコマンドプロンプトで次のパラメーターを使用して SignalR を実行します。

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR パフォーマンスカウンターを削除するには、管理者特権のコマンドプロンプトで次のパラメーターを使用して SignalR を実行します。

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR パフォーマンスカウンター

ユーティリティパッケージでは、次のパフォーマンスカウンターがインストールされます。 "Total" カウンターは、最後のアプリケーションプールまたはサーバーの再起動以降に発生したイベントの数を計測します。

**接続メトリック**

次のメトリックは、発生した接続の有効期間イベントを測定します。 詳細については、「[接続の有効期間イベントの理解と処理](../guide-to-the-api/handling-connection-lifetime-events.md)」を参照してください。

- **接続された接続**
- **再接続した接続**
- **切断された接続**
- **現在の接続**

**メッセージメトリック**

次のメトリックは、SignalR によって生成されるメッセージトラフィックを測定します。

- **受信した接続メッセージの合計**
- **送信された接続メッセージの合計**
- **1秒あたりの受信接続メッセージ数**
- **送信された接続メッセージ数/秒**

**メッセージバスメトリック**

次のメトリックは、内部 SignalR メッセージバスを通過するトラフィックを測定します。このキューは、すべての受信および送信 SignalR メッセージが配置されます。 メッセージは、送信またはブロードキャストされるときに**公開**されます。 このコンテキストの**サブスクライバー**は、メッセージバスのサブスクリプションです。これは、クライアントの数にサーバー自体を加えた数と同じである必要があります。 **割り当てら**れたワーカーは、アクティブな接続にデータを送信するコンポーネントです。**ビジー状態のワーカー**は、メッセージをアクティブに送信しているものです。

- **メッセージバスメッセージ受信合計数**
- **1秒あたりのメッセージバスメッセージ受信数**
- **メッセージバスメッセージの公開総数**
- **公開されたメッセージバスメッセージ数/秒**
- **現在のメッセージバスサブスクライバー**
- **メッセージバスサブスクライバーの合計**
- **メッセージバスサブスクライバー数/秒**
- **メッセージバスで割り当てられたワーカー**
- **メッセージバスビジーワーカー**
- **現在のメッセージバストピック**

**エラーのメトリック**

次のメトリックは、SignalR メッセージトラフィックによって生成されるエラーを測定します。 ハブの**解決**エラーは、ハブまたはハブのメソッドを解決できない場合に発生します。 ハブの**呼び出し**エラーは、ハブメソッドの呼び出し中にスローされる例外です。 **トランスポート**エラーは、HTTP 要求または応答の間にスローされた接続エラーです。

- **エラー: すべての合計**
- **エラー: すべて/秒**
- **エラー: ハブの解決の合計**
- **エラー: 1 秒あたりのハブの解決**
- **エラー: ハブ呼び出しの合計**
- **エラー: 1 秒あたりのハブ呼び出し数**
- **エラー: トランスポートの合計**
- **エラー: トランスポート/秒**

<a id="scaleout_metrics"></a>

**スケールアウトメトリック**

次のメトリックは、スケールアウトプロバイダーによって生成されたトラフィックとエラーを測定します。 このコンテキストの**ストリーム**は、スケールアウトプロバイダーによって使用されるスケール単位です。これは、SQL Server が使用されている場合はテーブル、Service Bus が使用されている場合はトピック、Redis が使用されている場合はサブスクリプションです。 各ストリームは、順次読み取りおよび書き込み操作を保証します。1つのストリームは、スケールのボトルネックとなる可能性があるため、そのボトルネックを減らすために、ストリームの数を増やすことができます。 複数のストリームが使用されている場合、SignalR は、特定の接続から送信されたメッセージが順番になるように、これらのストリーム間でメッセージを自動的に分散します。

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定は、SignalR によって管理されるスケールアウト送信キューの長さを制御します。 0より大きい値に設定すると、送信キュー内のすべてのメッセージが、構成済みのメッセージングバックプレーンに一度に1つずつ送信されます。 キューのサイズが構成された長さを超えた場合、キュー内のメッセージの数が再度設定されるまで、その後の送信の呼び出しはすぐに[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)で失敗します。 実装された背面には、通常独自のキューまたはフロー制御が設定されているため、既定では、キューは無効になっています。 SQL Server の場合、接続プールは、一度に行われる送信の数を効果的に制限します。

既定では、SQL Server と Redis には1つのストリームのみが使用され、Service Bus には5つのストリームが使用され、キューは無効になりますが、SQL Server と Service Bus で構成を使用してこれらの設定を変更できます。

**SQL Server バックプレーンのテーブル数とキューの長さを構成するための .NET サーバーコード**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Service Bus バックプレーンのトピック数とキューの長さを構成するための .NET サーバーコード**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**バッファリング**ストリームは、エラー状態になったストリームです。ストリームが faulted 状態の場合、バックプレーンに送信されるすべてのメッセージは、ストリームがエラーにならなくなるまで直ちに失敗します。 **送信キューの長さ**は、投稿されているがまだ送信されていないメッセージの数です。

- **スケールアウトされたメッセージバスメッセージ受信数/秒**
- **スケールアウトストリームの合計**
- **スケールアウトストリームを開く**
- **スケールアウトストリームのバッファリング**
- **スケールアウトエラーの合計**
- **スケールアウトエラー/秒**
- **スケールアウト送信キューの長さ**

これらのカウンターで測定される内容の詳細については、「 [SignalR のスケールアウトと Azure Service Bus](scaleout-with-windows-azure-service-bus.md)」を参照してください。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>その他のパフォーマンスカウンターの使用

次のパフォーマンスカウンターは、アプリケーションのパフォーマンスの監視にも役立ちます。

**[メモリ]**

- .NET CLR メモリ\\すべてのヒープ内のバイト数 (w3wp.exe 用)

**ASP.NET**

- ASP.NET\Requests Current
- ASP.NET\Queued
- ASP.NET\Rejected

**CPU**

- プロセッサ情報、プロセッサ時間

**TCP/IP**

- 確立された TCPv6/接続
- 確立された TCPv4/接続

**Web サービス**

- Web サービス \ 現在の接続
- Web サービス \ 最大接続数

**スレッド化**

- .NET CLR ロックとスレッド\\現在の論理スレッドの数
- .NET CLR ロックとスレッド\\現在の物理スレッドの数

<a id="otherresources"></a>

## <a name="other-resources"></a>その他のリソース

ASP.NET のパフォーマンスの監視とチューニングの詳細については、次のトピックを参照してください。

- [ASP.NET のパフォーマンスの概要](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5、IIS 7.0、および IIS 6.0 での ASP.NET スレッドの使用](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; 要素 (Web 設定)](https://msdn.microsoft.com/library/dd560842.aspx)
