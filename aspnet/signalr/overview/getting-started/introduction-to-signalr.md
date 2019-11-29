---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR | の概要Microsoft Docs
author: bradygaster
description: この記事では、SignalR の概要と、作成するように設計されたソリューションの一部について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 11b494b4839c646b018098c76a8a9ae0a2169757
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600490"
---
# <a name="introduction-to-signalr"></a>SignalR 入門

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、SignalR の概要と、作成するように設計されたソリューションの一部について説明します。 
> 
> ## <a name="questions-and-comments"></a>質問とコメント
> 
> このチュートリアルの気に入った点と、ページの下部にあるコメントで改善できることについて、フィードバックをお寄せください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)に投稿できます。

## <a name="what-is-signalr"></a>SignalR とは

ASP.NET SignalR は、リアルタイム web 機能をアプリケーションに追加するプロセスを簡略化する ASP.NET 開発者向けのライブラリです。 リアルタイム web 機能を使用すると、クライアントが新しいデータを要求するのをサーバーが待機するのではなく、接続されているクライアントにコンテンツをプッシュすることができるようになります。

SignalR を使用すると、ASP.NET アプリケーションに任意の種類の "リアルタイム" web 機能を追加できます。 多くの場合、チャットは例として使用されますが、さらに多くのことを行うことができます。 ユーザーが新しいデータを表示するために web ページを更新するたびに、またはページが[長いポーリング](http://en.wikipedia.org/wiki/Push_technology#Long_polling)を実装して新しいデータを取得すると、SignalR を使用することができます。 例としては、ダッシュボードとアプリケーションの監視、コラボレーションアプリケーション (ドキュメントの同時編集など)、ジョブの進行状況の更新、リアルタイムフォームなどがあります。

また、SignalR は、リアルタイムゲームなど、サーバーからの高頻度の更新を必要とする、まったく新しい種類の web アプリケーションを有効にします。

SignalR は、サーバーからクライアントへのリモートプロシージャコール (RPC) を作成するためのシンプルな API を提供します。この API は、クライアントブラウザー (およびその他のクライアントプラットフォーム) で、サーバー側の .NET コードから JavaScript 関数を呼び出します。 SignalR には、接続管理用の API (接続イベントや切断イベントなど) や、接続のグループ化も含まれます。

![SignalR を使用したメソッドの呼び出し](introduction-to-signalr/_static/image1.png)

SignalR は、接続管理を自動的に処理し、チャットルームなど、接続されているすべてのクライアントに同時にメッセージをブロードキャストすることができます。 また、特定のクライアントにメッセージを送信することもできます。 クライアントとサーバー間の接続は永続的です。これは、通信ごとに再確立される従来の HTTP 接続とは異なります。

SignalR では、"サーバープッシュ" 機能がサポートされています。この機能では、現在、web 上で共通の要求-応答モデルではなく、リモートプロシージャコール (RPC) を使用して、サーバーコードからブラウザーでクライアントコードを呼び出すことができます。

SignalR アプリケーションは、Service Bus、SQL Server または[Redis](http://redis.io)を使用して、数千のクライアントにスケールアウトできます。

SignalR はオープンソースであり、 [GitHub](https://github.com/signalr)を介してアクセスできます。

## <a name="signalr-and-websocket"></a>SignalR と WebSocket

SignalR は、使用可能な場合は新しい WebSocket トランスポートを使用し、必要に応じて古いトランスポートにフォールバックします。 確かに WebSocket を直接使用してアプリを記述することもできますが、SignalR を使用すると、実装する必要のある多くの追加機能が既に実行されていることを意味します。 最も重要なことは、これは、古いクライアント用に別のコードパスを作成することを心配することなく、WebSocket を利用するようにアプリをコーディングできることを意味します。 また、SignalR は、基になるトランスポートの変更をサポートするために SignalR が更新されるため、WebSocket のバージョン間の一貫性のあるインターフェイスをアプリケーションに提供するため、WebSocket の更新について心配する必要がなくなります。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>トランスポートとフォールバック

SignalR は、クライアントとサーバー間でリアルタイムの作業を行うために必要なトランスポートの一部を抽象化したものです。 SignalR 接続は HTTP として起動し、使用可能な場合は WebSocket 接続に昇格します。 WebSocket は、サーバーのメモリを最も効率的に使用し、待機時間が最も短く、最も基本的な機能 (クライアントとサーバー間の完全な双方向通信など) を備えているため、SignalR に最適なトランスポートですが、最も厳しい要件: WebSocket では、サーバーが Windows Server 2012 または Windows 8 を使用していること、および .NET Framework 4.5 が必要です。 これらの要件が満たされていない場合、SignalR は他のトランスポートを使用して接続を試行します。

### <a name="html-5-transports"></a>HTML 5 トランスポート

これらのトランスポートは、 [HTML 5](http://en.wikipedia.org/wiki/HTML5)のサポートに依存します。 クライアントのブラウザーが HTML 5 標準をサポートしていない場合は、古いトランスポートが使用されます。

- **Websocket** (サーバーとブラウザーの両方が websocket をサポートできることを示している場合)。 WebSocket は、クライアントとサーバーの間に真の永続的な双方向の接続を確立する唯一のトランスポートです。 ただし、WebSocket には、最も厳しい要件もあります。これは、最新バージョンの Microsoft Internet Explorer、Google Chrome、Mozilla Firefox でのみ完全にサポートされており、Opera や Safari などの他のブラウザーでは部分的な実装のみがあります。
- **サーバー送信イベント**。 EventSource とも呼ばれます (ブラウザーがサーバー送信イベントをサポートしている場合は、これは基本的に Internet Explorer を除くすべてのブラウザーです)。

### <a name="comet-transports"></a>コメットのトランスポート

次のトランスポートは、[コメット](http://en.wikipedia.org/wiki/Comet_(programming))web アプリケーションモデルに基づいています。このモデルでは、ブラウザーまたは他のクライアントが長い形式の HTTP 要求を保持しています。これは、サーバーがクライアントにデータをプッシュするために使用できます。

- **無期限フレーム**(Internet Explorer の場合のみ)。 永続的なフレームでは、未表示の IFrame が作成されます。これにより、サーバー上の完了していないエンドポイントへの要求が行われます。 サーバーは、直ちに実行されるクライアントに対してスクリプトを継続的に送信し、サーバーからクライアントへの一方向のリアルタイム接続を提供します。 クライアントからサーバーへの接続では、サーバーとクライアント間の接続を別々に使用します。標準の HTTP 要求と同様に、送信する必要があるデータごとに新しい接続が作成されます。
- **Ajax 長時間ポーリング**。 長いポーリングでは永続的な接続は作成されませんが、サーバーが応答するまで開いたままになっている要求を使用してサーバーをポーリングし、その時点で接続が閉じられ、新しい接続が直ちに要求されます。 これにより、接続がリセットされるまでの待機時間が発生する可能性があります。

構成でサポートされているトランスポートの詳細については、「[サポートされ](supported-platforms.md)ているプラットフォーム」を参照してください。

### <a name="transport-selection-process"></a>トランスポートの選択プロセス

次の一覧は、SignalR が使用するトランスポートを決定するために使用する手順を示しています。

1. ブラウザーが Internet Explorer 8 以前である場合は、長いポーリングが使用されます。
2. JSONP が構成されている場合 (つまり、接続が開始されたときに `jsonp` パラメーターが `true` に設定されている場合)、長いポーリングが使用されます。
3. クロスドメイン接続が行われている場合 (つまり、SignalR エンドポイントがホストページと同じドメインにない場合)、次の条件を満たす場合に WebSocket が使用されます。

   - クライアントは CORS (クロスオリジンリソース共有) をサポートしています。 CORS をサポートするクライアントの詳細については、「 [cors at caniuse.com](http://www.caniuse.com/CORS)」を参照してください。
   - クライアントが WebSocket をサポートする
   - サーバーは WebSocket をサポートします。

     これらの条件のいずれかが満たされていない場合は、長いポーリングが使用されます。 ドメイン間接続の詳細については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。
4. JSONP が構成されておらず、接続がドメインを越えていない場合は、クライアントとサーバーの両方でサポートされている場合、WebSocket が使用されます。
5. クライアントまたはサーバーのいずれかが WebSocket をサポートしていない場合は、サーバーの送信イベントが使用されます。
6. サーバー送信イベントが使用できない場合、永続的なフレームが試行されます。
7. 永続的なフレームが失敗した場合は、長いポーリングが使用されます。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>トランスポートの監視

ハブでログ記録を有効にし、ブラウザーでコンソールウィンドウを開くことによって、アプリケーションで使用されているトランスポートを特定できます。

ブラウザーでハブのイベントのログ記録を有効にするには、クライアントアプリケーションに次のコマンドを追加します。

`$.connection.hub.logging = true;`

- Internet Explorer で、F12 キーを押して開発者ツールを開き、[コンソール] タブをクリックします。

    ![Microsoft Internet Explorer のコンソール](introduction-to-signalr/_static/image2.png)
- Chrome で、Ctrl キーと Shift キーを押しながら J キーを押してコンソールを開きます。

    ![Google Chrome のコンソール](introduction-to-signalr/_static/image3.png)

コンソールを開いてログを有効にすると、SignalR によって使用されているトランスポートを確認できるようになります。

![WebSocket トランスポートが表示されている Internet Explorer のコンソール](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>トランスポートの指定

トランスポートをネゴシエートするには、一定の時間とクライアント/サーバーのリソースを必要とします。 クライアント機能が既知の場合は、クライアント接続が開始されたときにトランスポートを指定できます。 次のコードスニペットは、クライアントが他のプロトコルをサポートしていないことが判明した場合に使用されるように、Ajax の長いポーリングトランスポートを使用して接続を開始する方法を示しています。

`connection.start({ transport: 'longPolling' });`

クライアントが特定のトランスポートを順番に試行するようにする場合は、フォールバックの順序を指定できます。 次のコードスニペットは、WebSocket を試行し、それを失敗させて、長いポーリングに直接移動する方法を示しています。

`connection.start({ transport: ['webSockets','longPolling'] });`

トランスポートを指定するための文字列定数は、次のように定義されています。

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>接続とハブ

SignalR API には、クライアントとサーバー間の通信用に、永続的な接続とハブの2つのモデルが含まれています。

接続は、単一受信者、グループ化、またはブロードキャストメッセージを送信するための単純なエンドポイントを表します。 永続接続 API (.NET コードでは PersistentConnection クラスによって表されます) を使用すると、開発者は SignalR が公開する低レベル通信プロトコルに直接アクセスできます。 接続の通信モデルを使用すると、Windows Communication Foundation などの接続ベースの Api を使用している開発者にとってはなじみがありません。

ハブは、接続 API に基づいて構築されたより高度なパイプラインで、クライアントとサーバーが互いにメソッドを直接呼び出すことができます。 SignalR はマジックでの場合と同様にコンピューターの境界を越えたディスパッチを処理し、クライアントがローカルメソッドと同様に簡単にサーバー上のメソッドを呼び出すことができるようにします。また、その逆も可能です。 ハブ通信モデルを使用すると、.NET リモート処理などのリモート呼び出し Api を使用している開発者にとってなじみがあります。 ハブを使用すると、厳密に型指定されたパラメーターをメソッドに渡して、モデルバインドを有効にすることもできます。

### <a name="architecture-diagram"></a>アーキテクチャの図

次の図は、ハブ、永続的な接続、およびトランスポートに使用される基になるテクノロジの関係を示しています。

![Api、トランスポート、およびクライアントを示す SignalR アーキテクチャ図](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>ハブのしくみ

サーバー側のコードがクライアントでメソッドを呼び出すと、呼び出されるメソッドの名前とパラメーターを含むアクティブなトランスポート全体にパケットが送信されます (オブジェクトがメソッドパラメーターとして送信された場合は、JSON を使用してシリアル化されます)。 次に、クライアントは、メソッド名をクライアント側コードで定義されているメソッドと照合します。 一致するものがある場合は、逆シリアル化されたパラメーターデータを使用してクライアントメソッドが実行されます。

メソッドの呼び出しは、Fiddler などのツールを使用して監視でき[ます。](http://fiddler2.com/) 次の図は、Fiddler の [ログ] ウィンドウで SignalR サーバーから web ブラウザークライアントに送信されるメソッド呼び出しを示しています。 メソッド呼び出しは `MoveShapeHub`と呼ばれるハブから送信され、呼び出されるメソッドは `updateShape`と呼ばれます。

![SignalR トラフィックを示す Fiddler ログの表示](introduction-to-signalr/_static/image6.png)

この例では、ハブ名は `H` パラメーターで識別されます。メソッド名は `M` パラメーターで識別され、メソッドに送信されるデータは `A` パラメーターで識別されます。 このメッセージを生成したアプリケーションは、[高頻度のリアルタイム](tutorial-high-frequency-realtime-with-signalr.md)チュートリアルで作成されます。

### <a name="choosing-a-communication-model"></a>通信モデルの選択

ほとんどのアプリケーションでは、ハブ API を使用する必要があります。 Connections API は、次のような状況で使用できます。

- 実際に送信されるメッセージの形式を指定する必要があります。
- 開発者は、リモート呼び出しモデルではなく、メッセージングとディスパッチモデルを使用することを推奨しています。
- メッセージングモデルを使用する既存のアプリケーションは、SignalR を使用するように移植されています。
