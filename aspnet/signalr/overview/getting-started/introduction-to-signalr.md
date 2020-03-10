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
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431098"
---
# <a name="introduction-to-signalr"></a>SignalR 入門

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、SignalR の概要と、作成するように設計されたソリューションの一部について説明します。 
> 
> ## <a name="questions-and-comments"></a>質問とコメント
> 
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)に投稿できます。

## <a name="what-is-signalr"></a>SignalR とは何か

ASP.NET SignalR は、リアルタイム Web 機能をアプリケーションに追加するプロセスを簡素化する ASP.NET 開発者向けのライブラリです。 リアルタイム Web 機能とは、サーバーがクライアントからの新しいデータ要求を待つのではなく、サーバー コードが接続クライアントに対して利用可能になったコンテンツを瞬時にプッシュできる機能です。

SignalR は、ASP.NET アプリケーションに何らかの「リアルタイム」Web 機能を追加するために使用することができます。 よくチャットが例として使用されますが、もっと多くのことを行うことができます。 ユーザーが新しいデータを表示するために web ページを更新するたびに、またはページが[長いポーリング](http://en.wikipedia.org/wiki/Push_technology#Long_polling)を実装して新しいデータを取得すると、SignalR を使用することができます。 サンプルとしては、ダッシュ ボード アプリケーションや監視アプリケーション、コラボレーション アプリケーション (ドキュメントの同時編集など)、ジョブの進行状況の更新プログラム、およびリアルタイム フォームが含まれます。

SignalR はリアルタイム ゲームなど、サーバーから高頻度で更新を必要とするまったく新しいタイプの Web アプリケーションを有効にできます。

SignalR は、サーバー側の .NET コードからクライアント ブラウザー (およびその他のクライアント プラットフォーム) に JavaScript 関数を呼び出す、サーバーからクライアントへのリモート プロシージャ コール (RPC) を作成するための単純な API を提供します。 SignalR には、接続管理 (イベントの接続や切断など) やグループ接続のための API も含まれます。

![SignalR を使用したメソッドの呼び出し](introduction-to-signalr/_static/image1.png)

SignalR では、自動的に接続管理を処理し、チャット ルームのように、接続されているすべてのクライアントへのメッセージを同時に配信できます。 また、特定のクライアントにメッセージを送信することもできます。 クライアントとサーバー間の接続は、通信ごとに再確立される従来の HTTP 接続とは異なり永続的です。

SignalR は「サーバー プッシュ」機能をサポートしています。この機能では、現在 Web において一般的な要求 - 応答モデルではなく、リモート プロシージャ コール (RPC) を使用して、サーバー コードによってブラウザー内のクライアント コードを呼び出すことができます。

SignalR アプリケーションは、組み込みの、サードパーティのスケールアウトプロバイダーを使用して、何千ものクライアントにスケールアウトできます。

組み込みプロバイダーには次のものがあります。
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

サードパーティプロバイダーには次のものがあります。
* [Ncache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。

SignalR はオープンソースであり、 [GitHub](https://github.com/signalr)を介してアクセスできます。

## <a name="signalr-and-websocket"></a>SignalR と WebSocket

SignalR では、使用可能な場合は新しい WebSocket トランスポートを使用し、必要に応じて、古いトランスポートにフォールバックします。 WebSocket を直接使用してアプリを作成することはできますが、SignalR を使用するメリットは、実装する必要のある他の機能の多くが既に作成されているという点です。 これにより、最も重要な事ととして、古いクライアントのために個別のコード パスを作成することなく、WebSocket を活用できるようにアプリをコーディングすることができます。 SignalR は基本トランスポートの変更をサポートするために更新され、異なるバージョンの WebSocket でもアプリケーションにおいて一貫したインターフェイスが提供されるため、SignalR は WebSocket の更新に関する心配からユーザーを解放します。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>トランスポートとフォールバック

SignalR は、クライアントとサーバー間のリアルタイムの作業を行うために必要なトランスポートの一部を抽象化したものです。 SignalR 接続は HTTP として起動し、WebSocket 接続が可能な場合は WebSocket 接続となります。 WebSocket は、サーバーのメモリを最も効率的に使用し、待機時間が最も短く、最も基本的な機能 (クライアントとサーバー間の全二重通信など) が備わっているため、SignalR の理想的なトランスポートですが、細かい要件があります。WebSocket では、Windows Server 2012 または Windows 8、および .NET Framework 4.5 を使用するサーバーが必要です。 これらの要件が満たされない場合、SignalR は、接続するために他のトランスポートの使用を試みます。

### <a name="html-5-transports"></a>HTML 5 トランスポート

これらのトランスポートは、 [HTML 5](http://en.wikipedia.org/wiki/HTML5)のサポートに依存します。 クライアントのブラウザーが HTML 5 標準をサポートしていない場合は、古いトランスポートが使用されます。

- **Websocket** (サーバーとブラウザーの両方が websocket をサポートできることを示している場合)。 WebSocket は、クライアントとサーバー間の通信における真に永続的な双方向接続を確立するためのトランスポートです。 ただし、WebSocket には細かい要件もあります。WebSocket は Microsoft Internet Explorer、Google Chrome、Mozilla Firefox の最新のバージョンでのみ完全にサポートされ、Opera や Safari などの他のブラウザーでは部分的にしか実装されません。
- **サーバー送信イベント**。 EventSource とも呼ばれます (ブラウザーがサーバー送信イベントをサポートしている場合は、これは基本的に Internet Explorer を除くすべてのブラウザーです)。

### <a name="comet-transports"></a>コメットのトランスポート

次のトランスポートは、[コメット](http://en.wikipedia.org/wiki/Comet_(programming))web アプリケーションモデルに基づいています。このモデルでは、ブラウザーまたは他のクライアントが長い形式の HTTP 要求を保持しています。これは、サーバーがクライアントにデータをプッシュするために使用できます。

- **無期限フレーム**(Internet Explorer の場合のみ)。 Forever Frame は、サーバー上のエンドポイントへの要求が完了しない非表示の IFrame を作成します。 サーバーは、すぐに実行されるスクリプトを継続的にクライアントに送信し、サーバーからクライアントへの一方向のリアルタイム接続を提供します。 クライアントからサーバーへの接続は、サーバーからクライアントとは異なる接続を使用し、標準の HTTP 要求のように、送信する必要のあるデータがあるたびに新しい接続が作成されます。
- **Ajax 長時間ポーリング**。 Long Polling では永続的な接続は作成されませんが、サーバーが応答を完了するまで開いたままの要求でサーバーをポーリングします。接続が閉じられたら即座に新しい接続が要求されます。 これにより、接続がリセットされるまでの待機時間が発生する可能性があります。

構成でサポートされているトランスポートの詳細については、「[サポートされ](supported-platforms.md)ているプラットフォーム」を参照してください。

### <a name="transport-selection-process"></a>トランスポート選択のプロセス

SignalR が使用するトランスポートを決定する手順を以下に示します。

1. ブラウザーが Internet Explorer 8 またはそれ以前の場合は、Long Polling が使用されます。
2. JSONP が構成されている場合 (つまり、接続が開始されたときに `jsonp` パラメーターが `true` に設定されている場合)、長いポーリングが使用されます。
3. クロス ドメイン接続が確立されている場合 (つまり、SignalR エンドポイントが、ホスティング ページと同じドメインにない)、次の条件が満たされた場合に WebSocket が使用されます。

   - クライアントが CORS (クロス オリジン リソース共有) をサポートしている。 CORS をサポートするクライアントの詳細については、「 [cors at caniuse.com](http://www.caniuse.com/CORS)」を参照してください。
   - クライアントが WebSocket をサポートしている。
   - サーバーが WebSocket をサポートしている。

     これらの条件のいずれかが満たされていない場合は、Long Polling が使用されます。 ドメイン間接続の詳細については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。
4. JSONP が設定されておらず、ドメイン間接続でない場合は WebSocket が使用されます (クライアントとサーバーの両方がサポートしている場合)。
5. クライアントまたはサーバーのいずれかが WebSocket をサポートしていない場合は Server Sent Events が使用されます (利用可能に場合)。
6. サーバー送信イベントが使用できない場合、永続的なフレームが試行されます。
7. 永続的なフレームが失敗した場合は、長いポーリングが使用されます。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>トランスポートの監視

ハブでログを有効にし、ブラウザーでコンソール ウィンドウを開くことによって、アプリケーションで使用されているトランスポートを特定できます。

ブラウザーでハブのイベントのログ記録を有効にするには、クライアントアプリケーションに次のコマンドを追加します。

`$.connection.hub.logging = true;`

- Internet Explorer で、F12 キーを押して開発者ツールを開き、[コンソール] タブをクリックします。

    ![Microsoft Internet Explorer のコンソール](introduction-to-signalr/_static/image2.png)
- Chrome で、Ctrl キーと Shift キーを押しながら J キーを押してコンソールを開きます。

    ![Google Chrome のコンソール](introduction-to-signalr/_static/image3.png)

コンソールが開いた状態で、ログが有効な場合は、SignalR で利用されているトランスポートを確認することができます。

![WebSocket トランスポートが表示されている Internet Explorer のコンソール](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>トランスポートの指定

トランスポートのネゴシエートには一定の時間を要し、クライアントとサーバーの一定量のリソースを使用します。 クライアントの機能が分かっている場合は、クライアント接続が開始された時点でトランスポートを指定することができます。 次のコード スニペットでは、クラインが他のプロトコルをサポートしていないことが分かっている場合にも使用される、Ajax Long Polling のトランスポートを使用して接続を開始する方法を示しています。

`connection.start({ transport: 'longPolling' });`

クライアントが特定のトランスポートを順番に試行するようにする場合は、フォールバック順序を指定できます。 次のコード スニペットは、WebSocket を試し、失敗した場合、Long Polling に直接移行する例を示します。

`connection.start({ transport: ['webSockets','longPolling'] });`

トランスポートを指定するための文字列定数は、次のように定義されています。

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>接続とハブ

SignalR API には、クライアントとサーバー間の通信用に、永続的な接続とハブの2つのモデルが含まれています。

接続は、単一受信者メッセージ、グループ化メッセージ、またはブロードキャスト メッセージを送信するための単純なエンドポイントを表します。 固定接続 API (PersistentConnection クラスによって .NET コードで表される) は、SignalR が公開している低レベルの通信プロトコルへの直接アクセスを開発者に提供します。 接続の通信モデルは、Windows Communication Foundation などの接続に基づく API を使用したことのある開発者にとって使いやすいものです。

ハブは、クライアントとサーバーが相互に直接メソッドを呼び出すことができるようにする接続 API に基づいて構築されたより高度なパイプラインです。 SignalR は、マシンの境界でのディスパッチを魔法のように行い、クライアントがローカルのメソッドのように簡単にサーバーでメソッドを呼び出せるようにします (またはその逆)。 ハブ通信モデルは、.NET Remoting などのリモート呼び出し API を使用したことのある開発者にとって使いやすいものです。 また、ハブを使用すると、厳密に型指定されたパラメーターをメソッドに渡すことができ、モデルのバインディングが可能になります。

### <a name="architecture-diagram"></a>アーキテクチャの図

次の図は、ハブ、永続的な接続、およびトランスポートに使用される基になるテクノロジの関係を示しています。

![Api、トランスポート、およびクライアントを示す SignalR アーキテクチャ図](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>ハブのしくみ

サーバー側コードでは、クライアントでメソッドを呼び出すと、呼び出されるメソッドの名前とパラメーターを含むパケットがアクティブなトランスポート経由で送信されます (オブジェクトがメソッド パラメーターとして送信される場合、JSON を使用してシリアル化されます)。 次にクライアントは、メソッド名をクライアント側のコードで定義されているメソッドと一致させます。 一致するものがある場合は、逆シリアル化されたパラメーターデータを使用してクライアントメソッドが実行されます。

メソッドの呼び出しは、Fiddler などのツールを使用して監視でき[ます。](http://fiddler2.com/) 次のイメージは、Fiddler の [ログ] ウィンドウで、SignalR サーバーから Web ブラウザー クライアントに送信されたメソッドの呼び出しを示します。 メソッド呼び出しは `MoveShapeHub`と呼ばれるハブから送信され、呼び出されるメソッドは `updateShape`と呼ばれます。

![SignalR トラフィックを示す Fiddler ログの表示](introduction-to-signalr/_static/image6.png)

この例では、ハブ名は `H` パラメーターで識別されます。メソッド名は `M` パラメーターで識別され、メソッドに送信されるデータは `A` パラメーターで識別されます。 このメッセージを生成したアプリケーションは、[高頻度のリアルタイム](tutorial-high-frequency-realtime-with-signalr.md)チュートリアルで作成されます。

### <a name="choosing-a-communication-model"></a>通信モデルの選択

ほとんどのアプリケーションでは、ハブ API を使用する必要があります。 接続 API は次の状況で使用できます。

- 実際の送信メッセージの形式を指定する必要がある
- 開発者が、リモート呼び出しモデルではなく、メッセージおよびディスパッチ モデルを利用する事を推奨している
- メッセージングモデルを使用する既存のアプリケーションが SignalR を使用するように移植されている
