---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: SignalR 接続密度テスト (クランク) |Microsoft Docs
author: bradygaster
description: Crank による SignalR 接続密度テスト
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 901e039fbb81651ed18d560c99745b7e7f716e01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449872"
---
# <a name="signalr-connection-density-testing-with-crank"></a>Crank による SignalR 接続密度テスト

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、クランクツールを使用して、複数のシミュレートされたクライアントでアプリケーションをテストする方法について説明します。

アプリケーションがホスト環境 (Azure web ロール、IIS、または Owin を使用して自己ホスト型) で実行されている場合は、クランクツールを使用して、アプリケーションの応答を高レベルの接続密度に対してテストできます。 ホスティング環境には、インターネットインフォメーションサービス (IIS) サーバー、Owin ホスト、または Azure web ロールを指定できます。 (注: パフォーマンスカウンターは Azure App Service Web Apps では使用できないため、接続密度テストからパフォーマンスデータを取得することはできません)。

接続密度とは、サーバー上で確立できる同時 TCP 接続の数を指します。 TCP 接続ごとに独自のオーバーヘッドが発生し、アイドル状態の接続を多数開くと、最終的にメモリのボトルネックが生じます。

[SignalR Codebase には、](https://github.com/signalr/signalr) **クランク**と呼ばれるロードテストツールが含まれています。 最新バージョンのクランクは、GitHub の[Dev ブランチ](https://github.com/SignalR/signalr/tree/dev)にあります。 [ここで](https://github.com/SignalR/SignalR/archive/dev.zip)は、SignalR Codebase の Dev ブランチの Zip アーカイブをダウンロードできます。

クランクを使用すると、サーバーハードウェアで可能なアイドル状態の接続の合計数を計算するために、サーバーのメモリを完全に飽和させることができます。 または、クランクを使用して、特定の数または特定のメモリのしきい値に達するまで接続を増やして、特定の量のメモリ負荷でサーバーの負荷テストを行うこともできます。

テスト時には、リモートクライアントを使用してリソース (TCP 接続やメモリなど) の競合を回避することが重要です。 クライアントを監視して、サーバーが完全な容量 (メモリまたは CPU) に到達できない可能性のあるボトルネックに達していないことを確認します。 サーバーを完全に読み込むには、クライアントの数を増やすことが必要になる場合があります。

### <a name="running-a-connection-density-test"></a>接続密度テストの実行

このセクションでは、SignalR アプリケーションで接続密度テストを実行するために必要な手順について説明します。

1. [SignalR codebase の Dev ブランチ](https://github.com/SignalR/SignalR/archive/dev.zip)をダウンロードしてビルドします。 コマンドプロンプトで、&lt;プロジェクトディレクトリ&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug. に移動します。
2. 目的のホスティング環境にアプリケーションをデプロイします。 アプリケーションで使用するエンドポイントをメモしておきます。たとえば、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションでは、エンドポイントが `http://<yourhost>:8080/signalr`ます。
3. [SignalR パフォーマンスカウンター](signalr-performance.md#perfcounters)をサーバーにインストールします。 アプリケーションが Azure で実行されている場合は、「 [azure の Web ロールでの SignalR パフォーマンスカウンターの使用](using-signalr-performance-counters-in-an-azure-web-role.md)」を参照してください。

コードベースをダウンロードしてビルドし、ホストにインストールされたパフォーマンスカウンターをインストールすると、[`src\Microsoft.AspNet.SignalR.Crank\bin\Debug`] フォルダーにクランクコマンドラインツールが表示されます。

クランクツールで使用可能なオプションは次のとおりです。

- **/?** : ヘルプ画面が表示されます。 使用可能なオプションは、 **Url**パラメーターを省略した場合にも表示されます。
- **/Url**: SignalR 接続の Url。 このパラメーターは必須です。 既定のマッピングを使用する SignalR アプリケーションでは、パスは "/signalr" で終了します。
- **/Transport**: 使用されるトランスポートの名前。 既定値は `auto`です。これにより、使用可能なプロトコルが選択されます。 オプションには `WebSockets`、`ServerSentEvents`、`LongPolling` があります (Internet Explorer ではなく .NET クライアントが使用されているため、`ForeverFrame` は、クランクのオプションではありません)。 SignalR がトランスポートを選択する方法の詳細については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。
- **/BatchSize**: 各バッチに追加されたクライアントの数。 既定値は 50 です。
- **/Connectinterval**: 接続を追加する間隔をミリ秒単位で指定します。 既定値は 500 です。
- **/接続**: アプリケーションのロードテストに使用される接続の数。 既定値は10万です。
- **/Connecttimeout**: テストを中止するまでの秒単位のタイムアウト。 既定値は300です。
- **Minservermbytes**: 最小サーバーメガバイト数。 既定値は 500 です。
- **Sendbytes**: サーバーに送信されるペイロードのサイズ (バイト単位)。 既定値は 0 です。
- **Sendinterval**: サーバーへのメッセージ間の遅延 (ミリ秒単位)。 既定値は 500 です。
- **Sendtimeout**: サーバーへのメッセージのタイムアウト (ミリ秒)。 既定値は300です。
- コントローラーの**url**: 1 つのクライアントがコントローラーハブをホストする url。 既定値は null (コントローラーハブなし) です。 コントローラーハブは、クランクセッションが開始されると開始されます。コントローラーハブとクランクの間には、それ以上の接続は行われません。
- **Numclients**: アプリケーションに接続するシミュレートされたクライアントの数。 既定値は1です。
- **Logfile**: テストの実行のログファイルのファイル名。 既定では、 `crank.csv`です。
- **Sampleinterval**: パフォーマンスカウンターサンプル間のミリ秒単位の時間です。 既定値は 1000 です。
- **Signalrinstance**: サーバー上のパフォーマンスカウンターのインスタンス名。 既定では、クライアント接続状態が使用されます。

### <a name="example"></a>例

次のコマンドは、100接続を使用して、ポート8080でアプリケーションをホストする Azure 上の `pfsignalr` という名前のサイトをテストします。

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
