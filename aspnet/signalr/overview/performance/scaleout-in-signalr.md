---
uid: signalr/overview/performance/scaleout-in-signalr
title: SignalR のスケールアウトの概要 |Microsoft Docs
author: bradygaster
description: この Visual Studio 2013 トピックで使用されているソフトウェアのバージョンについては、このトピックの以前のバージョンの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14dc22f99a43b566903c59fb23b7d419350f4a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467782"
---
# <a name="introduction-to-scaleout-in-signalr"></a>SignalR のスケールアウト入門

[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

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

一般に、web アプリケーションを拡張するには、*スケールアップ*と*スケールアウト*の2つの方法があります。

- スケールアップとは、より大規模なサーバー (またはより大きな VM) を使用して、より多くの RAM、Cpu などを使用することです。
- Scale out は、負荷を処理するためにサーバーを追加することを意味します。

スケールアップの問題は、コンピューターのサイズの上限に達することです。 それ以外の場合は、スケールアウトする必要があります。ただし、スケールアウトすると、クライアントは別のサーバーにルーティングされる可能性があります。 1つのサーバーに接続されているクライアントは、別のサーバーから送信されたメッセージを受信しません。

![](scaleout-in-signalr/_static/image1.png)

1つの解決策は、*バックプレーン*と呼ばれるコンポーネントを使用して、サーバー間でメッセージを転送することです。 バックプレーンが有効になっている場合、各アプリケーションインスタンスはバックプレーンにメッセージを送信し、バックプレーンはそれらを他のアプリケーションインスタンスに転送します。 (エレクトロニクスでは、バックプレーンは並列コネクタのグループです。 例えとして、SignalR バックプレーンは複数のサーバーを接続します)。

![](scaleout-in-signalr/_static/image2.png)

現在、SignalR には次の3つの背面があります。

- **Azure Service Bus**。 Service Bus は、疎結合された方法でコンポーネントがメッセージを送信できるようにするメッセージングインフラストラクチャです。
- **Redis**。 Redis は、メモリ内のキーと値のストアです。 Redis は、メッセージを送信するためのパブリッシュ/サブスクライブ ("pub/sub") パターンをサポートしています。
- **SQL Server**。 SQL Server バックプレーンは、SQL テーブルにメッセージを書き込みます。 バックプレーンは、効率的なメッセージングのために Service Broker を使用します。 ただし、Service Broker が有効になっていない場合にも機能します。

アプリケーションを Azure にデプロイする場合は、 [Azure Redis Cache](https://azure.microsoft.com/services/cache/)を使用した Redis バックプレーンの使用を検討してください。 独自のサーバーファームにデプロイする場合は、SQL Server または Redis 背面を検討してください。

次のトピックには、各バックプレーンの手順に関するチュートリアルが含まれています。

- [Azure Service Bus による SignalR スケールアウト](scaleout-with-windows-azure-service-bus.md)
- [Redis による SignalR スケールアウト](scaleout-with-redis.md)
- [SQL Server による SignalR スケールアウト](scaleout-with-sql-server.md)

## <a name="implementation"></a>実装

SignalR では、すべてのメッセージがメッセージバスを介して送信されます。 メッセージバスは、パブリッシュ/サブスクライブの抽象化を提供する[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)インターフェイスを実装します。 背面は、既定の**IMessageBus**をそのバックプレーン用に設計されたバスに置き換えることによって機能します。 たとえば、Redis のメッセージバスは[Redismessagebus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)で、redis [pub/sub](http://redis.io/topics/pubsub)メカニズムを使用してメッセージを送受信します。

各サーバーインスタンスは、バスを介してバックプレーンに接続します。 メッセージが送信されると、バックプレーンに送られ、バックプレーンがすべてのサーバーに送信します。 サーバーがバックプレーンからメッセージを取得すると、メッセージはローカルキャッシュに格納されます。 サーバーは、ローカルキャッシュからクライアントにメッセージを配信します。

クライアント接続ごとに、カーソルを使用して、メッセージストリームの読み取りにおけるクライアントの進行状況が追跡されます。 (カーソルはメッセージストリーム内の位置を表します)。クライアントが切断された後に再接続すると、クライアントのカーソル値の後に到着したメッセージをバスに要求します。 接続で[長いポーリング](../getting-started/introduction-to-signalr.md#transports)が使用されている場合も同じことが起こります。 長いポーリング要求が完了すると、クライアントは新しい接続を開き、カーソルの後に到着したメッセージを要求します。

カーソルメカニズムは、再接続時にクライアントが別のサーバーにルーティングされている場合でも機能します。 バックプレーンは、すべてのサーバーを認識しており、クライアントが接続しているサーバーには関係ありません。

## <a name="limitations"></a>制限事項

バックプレーンを使用する場合、最大メッセージスループットは、クライアントが単一のサーバーノードに直接通信する場合よりも低くなります。 これは、バックプレーンがすべてのメッセージをすべてのノードに転送するため、バックプレーンがボトルネックになる可能性があるためです。 この制限が問題になるかどうかは、アプリケーションによって異なります。 たとえば、一般的な SignalR シナリオを次に示します。

- [サーバーブロードキャスト](../getting-started/tutorial-server-broadcast-with-signalr.md)(stock ティッカーなど): 背面は、このシナリオに適しています。これは、サーバーがメッセージの送信速度を制御するためです。
- [クライアント対クライアント](../getting-started/tutorial-getting-started-with-signalr.md)(チャットなど): このシナリオでは、メッセージの数がクライアントの数に合わせてスケーリングされる場合、バックプレーンはボトルネックになる可能性があります。これは、より多くのクライアントが参加したときにメッセージの割合が増加した場合に発生します。
- [高頻度リアル](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)タイム (リアルタイムゲームなど): このシナリオでは、バックプレーンはお勧めできません。

## <a name="enabling-tracing-for-signalr-scaleout"></a>SignalR のスケールアウトのトレースを有効にする

背面のトレースを有効にするには、次のセクションを web.config ファイルのルート**構成**要素の下に追加します。

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
