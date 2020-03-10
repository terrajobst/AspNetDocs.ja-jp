---
uid: signalr/overview/older-versions/handling-connection-lifetime-events
title: SignalR 1.x | での接続の有効期間イベントについて理解し、処理するMicrosoft Docs
author: bradygaster
description: この記事では、ハブ API によって公開されるイベントの使用方法について説明します。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: e608e263-264d-448b-b0eb-6eeb77713b22
msc.legacyurl: /signalr/overview/older-versions/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 2fb671e730a1d41c07b350bf1d64ac1d0b1be55c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431500"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr-1x"></a>SignalR 1.x での接続の有効期間イベントについて理解し、処理する

[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、処理可能な SignalR 接続、再接続、切断イベントの概要と、構成できるタイムアウトと keepalive の設定について説明します。
> 
> この記事では、SignalR と接続の有効期間イベントに関する知識を既に持っていることを前提としています。 SignalR の概要については、「 [SignalR-はじめに](index.md)」を参照してください。 接続の有効期間イベントの一覧については、次のリソースを参照してください。
> 
> - [ハブクラスで接続の有効期間イベントを処理する方法](index.md)
> - [JavaScript クライアントで接続の有効期間イベントを処理する方法](index.md)
> - [.NET クライアントで接続の有効期間イベントを処理する方法](index.md)

## <a name="overview"></a>概要

このトピックの内容は次のとおりです。

- [接続の有効期間に関する用語とシナリオ](#terminology)

    - [SignalR 接続、トランスポート接続、および物理接続](#signalrvstransport)
    - [トランスポート切断のシナリオ](#transportdisconnect)
    - [クライアント切断のシナリオ](#clientdisconnect)
    - [サーバー切断のシナリオ](#serverdisconnect)
- [タイムアウトと keepalive の設定](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [タイムアウトと keepalive の設定を変更する方法](#changetimeout)
- [切断についてユーザーに通知する方法](#notifydisconnect)
- [継続的に再接続する方法](#continuousreconnect)
- [サーバーコードでクライアントを切断する方法](#disconnectclientfromserver)

API リファレンストピックへのリンクは、.NET 4.5 バージョンの API です。 .NET 4 を使用している場合は、 [.net 4 バージョンの API に関するトピック](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)を参照してください。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>接続の有効期間に関する用語とシナリオ

SignalR Hub 内の `OnReconnected` イベントハンドラーは、`OnConnected` の後に直接実行できますが、特定のクライアントに対して `OnDisconnected` 後に実行することはできません。 切断せずに再接続できる理由として、SignalR で "接続" という語が使用される方法がいくつかあります。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 接続、トランスポート接続、および物理接続

この記事では、 *SignalR 接続*、*トランスポート接続*、および*物理接続*を区別します。

- **SignalR connection**は、SignalR API によって管理され、接続 ID によって一意に識別される、クライアントとサーバーの URL の間の論理関係を指します。 このリレーションシップに関するデータは SignalR によって保持され、トランスポート接続を確立するために使用されます。 クライアントが `Stop` メソッドを呼び出したとき、または SignalR が失われたトランスポート接続を再確立しようとしている間にタイムアウト制限に達した場合、リレーションシップは終了し、SignalR によって破棄されます。
- **トランスポート接続**とは、クライアントとサーバーの間の論理関係を指します。これは、websocket、サーバー送信イベント、永続的なフレーム、または長いポーリングの4つのトランスポート api のいずれかによって管理されます。 SignalR はトランスポート API を使用してトランスポート接続を作成します。トランスポート API は、トランスポート接続を作成するための物理ネットワーク接続が存在するかどうかに依存します。 トランスポート接続は、SignalR が終了したとき、またはトランスポート API が物理的な接続が切断されたことを検出したときに終了します。
- **物理接続**とは、クライアントコンピューターとサーバーコンピューター間の通信を容易にする物理的なネットワークリンク (ワイヤ、ワイヤレス信号、ルーターなど) を指します。 SignalR 接続を確立するには、転送接続を確立するために、物理的な接続が存在している必要があります。 ただし、このトピックの後半で説明するように、物理的な接続が切断されても、常にトランスポート接続または SignalR 接続が終了するとは限りません。

次の図では、SignalR 接続はハブ API と PersistentConnection API SignalR レイヤーによって表され、トランスポート接続はトランスポート層によって表され、物理接続はサーバー間の線で表されます。とクライアントです。

![SignalR アーキテクチャの図](handling-connection-lifetime-events/_static/image1.png)

SignalR クライアントで `Start` メソッドを呼び出すと、サーバーへの物理的な接続を確立するために必要なすべての情報が SignalR クライアントコードに提供されます。 SignalR クライアントコードは、この情報を使用して HTTP 要求を行い、4つのトランスポートメソッドのいずれかを使用する物理的な接続を確立します。 トランスポート接続が失敗した場合、またはサーバーで障害が発生した場合、クライアントには、同じ SignalR URL への新しいトランスポート接続を自動的に再確立するために必要な情報が残っているので、SignalR 接続はすぐには消えません。 このシナリオでは、ユーザーアプリケーションからの介入は関係しません。 SignalR クライアントコードが新しいトランスポート接続を確立しても、新しい SignalR 接続は開始されません。 SignalR 接続の継続性は、`Start` メソッドを呼び出したときに作成される接続 ID が変更されないという事実に反映されます。

転送接続が失われた後に自動的に再確立されると、ハブの `OnReconnected` イベントハンドラーが実行されます。 `OnDisconnected` イベントハンドラーは、SignalR 接続の最後に実行されます。 SignalR 接続は、次のいずれかの方法で終了できます。

- クライアントが `Stop` メソッドを呼び出すと、サーバーに停止メッセージが送信され、クライアントとサーバーの両方が SignalR 接続を直ちに終了します。
- クライアントとサーバー間の接続が失われると、クライアントは再接続を試み、サーバーはクライアントが再接続するのを待ちます。 再接続の試行が失敗し、切断のタイムアウト期間が終了した場合、クライアントとサーバーの両方が SignalR 接続を終了します。 クライアントは再接続を停止し、サーバーは SignalR 接続の表現を破棄します。
- `Stop` メソッドを呼び出すことなくクライアントが実行を停止した場合、サーバーはクライアントが再接続するのを待ってから、切断のタイムアウト期間後に SignalR 接続を終了します。
- サーバーの実行が停止した場合、クライアントは再接続 (トランスポート接続の再作成) を試行し、切断のタイムアウト期間後に SignalR 接続を終了します。

接続の問題がなく、ユーザーアプリケーションが `Stop` メソッドを呼び出すことによって SignalR 接続を終了すると、SignalR 接続とトランスポート接続の開始と終了がほぼ同時に行われます。 以下のセクションでは、その他のシナリオについて詳しく説明します。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>トランスポート切断のシナリオ

物理接続が低速であるか、接続が中断している可能性があります。 中断の長さなどの要因によっては、トランスポート接続が切断される可能性があります。 SignalR は、トランスポート接続の再確立を試みます。 場合によっては、トランスポート接続 API によって中断が検出され、トランスポート接続が切断されることがあります。 SignalR は、接続が失われたことをすぐに検出します。 その他のシナリオでは、接続が失われても、トランスポート接続 API も SignalR もすぐには認識されません。 長いポーリング以外のすべてのトランスポートでは、SignalR クライアントは*keepalive*という機能を使用して、トランスポート API が検出できない接続が失われていないかどうかを確認します。 長いポーリング接続の詳細については、このトピックで後述する「 [Timeout および keepalive の設定](#timeoutkeepalive)」を参照してください。

接続が非アクティブになると、サーバーは定期的にキープアライブパケットをクライアントに送信します。 この記事が書かれている日付の場合、既定の頻度は10秒ごとになります。 これらのパケットをリッスンすることによって、クライアントは接続に問題があるかどうかを判断できます。 必要に応じて keepalive パケットが受信されない場合、クライアントは短時間で、パフォーマンスの低下や中断などの接続の問題があると想定します。 長い時間が経過しても keepalive が受信されない場合、クライアントは接続が切断されたと想定し、再接続を開始します。

次の図は、トランスポート API によってすぐに認識されない物理接続に問題がある場合に、一般的なシナリオで発生するクライアントとサーバーのイベントを示しています。 この図は、次のような場合に適用されます。

- トランスポートは、Websocket、永続的なフレーム、またはサーバーから送信されたイベントです。
- 物理ネットワーク接続には、さまざまな中断期間があります。
- トランスポート API は中断を認識しないため、SignalR は keepalive 機能に依存して検出します。

![トランスポートの切断](handling-connection-lifetime-events/_static/image2.png)

クライアントが再接続モードになっても、切断のタイムアウト制限内にトランスポート接続を確立できない場合、サーバーは SignalR 接続を終了します。 この場合、サーバーはハブの `OnDisconnected` メソッドを実行し、クライアントが後で接続を管理する場合に、クライアントに送信する切断メッセージをキューに入れます。 クライアントが再接続すると、切断コマンドを受信し、`Stop` メソッドを呼び出します。 このシナリオでは、クライアントの再接続時に `OnReconnected` は実行されず、クライアントが `Stop`を呼び出すと `OnDisconnected` は実行されません。 次の図は、このシナリオを示しています。

![トランスポートの中断-サーバーのタイムアウト](handling-connection-lifetime-events/_static/image3.png)

クライアントで発生する可能性のある SignalR 接続の有効期間イベントは、次のとおりです。

- `ConnectionSlow` クライアントイベント。

    最後のメッセージまたは keepalive ping を受信してから、keepalive タイムアウト期間の事前設定された割合が経過したときに発生します。 Keepalive タイムアウトの既定の警告期間は、keepalive timeout の2/3 です。 Keepalive timeout は20秒であるため、警告は約13秒で発生します。

    既定では、サーバーは10秒ごとに keepalive ping を送信し、クライアントは2秒ごとに keepalive ping を確認します (keepalive timeout 値と keepalive timeout 警告値の3番目の差の1つ)。

    トランスポート API が切断を認識した場合、SignalR は、keepalive タイムアウト警告期間が経過する前に切断が通知されることがあります。 この場合、`ConnectionSlow` イベントは発生せず、SignalR は `Reconnecting` イベントに直接進みます。
- `Reconnecting` クライアントイベント。

    (A) トランスポート API が接続が失われたことを検出した場合、または (b) 最後のメッセージまたは keepalive ping を受信してから keepalive タイムアウト期間が経過した場合に発生します。 SignalR クライアントコードが再接続を開始しようとします。 トランスポート接続が失われたときにアプリケーションで何らかのアクションを実行する場合は、このイベントを処理できます。 既定の keepalive タイムアウト期間は現在20秒です。

    SignalR が再接続モードのときにクライアントコードがハブメソッドを呼び出そうとすると、SignalR はコマンドの送信を試みます。 ほとんどの場合、このような試行は失敗しますが、状況によっては成功する可能性があります。 サーバー送信イベント、永続的なフレーム、および長いポーリングトランスポートの場合、SignalR は2つの通信チャネルを使用します。1つは、クライアントがメッセージを送信するために使用し、もう1つはメッセージを受信するために使用します。 受信に使用されるチャネルは、永続的に開いているチャネルであり、物理接続が中断されたときに閉じられます。 送信に使用されるチャネルは使用可能なままであるため、物理接続が復元された場合、受信チャネルが再確立される前に、クライアントからサーバーへのメソッド呼び出しが正常に行われる可能性があります。 SignalR が受信に使用されたチャネルを再度開くまで、戻り値は受信されません。
- `Reconnected` クライアントイベント。

    トランスポート接続が再確立されたときに発生します。 ハブの `OnReconnected` イベントハンドラーが実行されます。
- `Closed` クライアントイベント (JavaScript の`disconnected` イベント)。

    SignalR クライアントコードがトランスポート接続を失うと再接続を試行している間に、切断のタイムアウト期間が経過したときに発生します。 既定の切断タイムアウトは30秒です。 (このイベントは、`Stop` メソッドが呼び出されるため、接続が終了したときにも発生します)。

トランスポート API によって検出されないトランスポート接続の中断が発生して、keepalive timeout 警告期間より長くサーバーからの keepalive ping の受信が遅れることはないため、接続の有効期間イベントが発生しない可能性があります。

ネットワーク環境によっては、アイドル状態の接続が意図的に閉じられる場合があります。また、keepalive パケットのもう1つの機能は、SignalR 接続が使用中であることをこれらのネットワークに知らせることによって、これを回避するため 極端なケースでは、keepalive ping の既定の頻度が、閉じた接続を防ぐには不十分である可能性があります。 その場合は、keepalive ping をより頻繁に送信するように構成できます。 詳細については、このトピックで後述する「[タイムアウトと keepalive の設定](#timeoutkeepalive)」を参照してください。

> [!NOTE] 
> 
> [!IMPORTANT]
> ここで説明する一連のイベントは保証されていません。 SignalR は、このスキームに従って、予測可能な方法で接続の有効期間イベントを発生させようとしますが、ネットワークイベントには多くのバリエーションがあり、多くの方法で、トランスポート Api などの基になる通信フレームワークがそれらを処理します。 たとえば、クライアントの再接続時には `Reconnected` イベントが発生しない場合や、接続の確立に失敗したときにサーバー上の `OnConnected` ハンドラーが実行される場合があります。 このトピックでは、通常、特定の一般的な状況で生成される効果についてのみ説明します。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>クライアント切断のシナリオ

ブラウザークライアントでは、SignalR 接続を維持する SignalR クライアントコードが、web ページの JavaScript コンテキストで実行されます。 このため、あるページから別のページに移動するときに SignalR 接続を終了する必要があるので、複数のブラウザーウィンドウまたはタブから接続する場合、複数の接続 Id を持つ接続が複数あるのです。 ユーザーがブラウザーウィンドウまたはタブを閉じたり、新しいページに移動したり、ページを更新したりすると、SignalR 接続はすぐに終了します。これは、SignalR クライアントコードがそのブラウザーイベントを処理し、`Stop` メソッドを呼び出すためです。 これらのシナリオでは、または任意のクライアントプラットフォームで、アプリケーションが `Stop` メソッドを呼び出すと、`OnDisconnected` イベントハンドラーがサーバー上ですぐに実行され、クライアントによって `Closed` イベントが発生します (イベントは JavaScript では `disconnected` という名前が付けられます)。

クライアントアプリケーションまたはコンピューターが実行されているコンピューターがクラッシュした場合、またはスリープ状態になった場合 (ユーザーがラップトップを終了した場合など)、サーバーには何が起こったかが通知されません。 サーバーが認識している限り、クライアントの損失は接続の中断が原因である可能性があり、クライアントは再接続を試みている可能性があります。 そのため、このようなシナリオでは、サーバーはクライアントに再接続する機会を与えます。 `OnDisconnected` は、切断のタイムアウト期間 (既定では約30秒) が経過するまで実行されません。 次の図は、このシナリオを示しています。

![クライアントコンピューターの障害](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>サーバー切断のシナリオ

サーバーがオフラインになると、再起動、失敗、アプリドメインのリサイクルなどが行われます。その結果、接続が失われた場合や、トランスポート API と SignalR によってサーバーが失われたことがすぐにわかります。また、SignalR が `ConnectionSlow` イベントを発生させずに再接続しようとする可能性があります。 クライアントが再接続モードになった場合、切断のタイムアウト期間が経過する前にサーバーが回復または再起動した場合、または新しいサーバーがオンラインになった場合、クライアントは復元されたサーバーまたは新しいサーバーに再接続します。 この場合、クライアントで SignalR 接続が続行され、`Reconnected` イベントが発生します。 最初のサーバーでは、`OnDisconnected` は実行されず、新しいサーバーでは、`OnReconnected` が実行されますが、そのサーバー上のそのクライアントに対して `OnConnected` が実行されることはありません。 (再起動またはアプリケーションドメインのリサイクル後にクライアントが同じサーバーに再接続する場合と同じ効果があります。これは、サーバーの再起動時に、前の接続アクティビティのメモリがなくなるためです)。次の図は、トランスポート API が失われた接続をすぐに認識し、`ConnectionSlow` イベントが発生しないことを前提としています。

![サーバーの障害と再接続](handling-connection-lifetime-events/_static/image5.png)

切断のタイムアウト期間内にサーバーが使用できなくなった場合、SignalR 接続は終了します。 このシナリオでは、`Closed` イベント (JavaScript クライアントでは`disconnected`) がクライアントで発生しますが、サーバー上で `OnDisconnected` は呼び出されません。 次の図は、トランスポート API が失われた接続を認識しないことを前提としています。そのため、SignalR keepalive 機能によって検出され、`ConnectionSlow` イベントが発生します。

![サーバーの障害とタイムアウト](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>タイムアウトと keepalive の設定

既定の `ConnectionTimeout`、`DisconnectTimeout`、および `KeepAlive` の値はほとんどのシナリオに適していますが、環境に特別なニーズがある場合は変更できます。 たとえば、ネットワーク環境で、5秒間アイドル状態の接続を閉じる場合は、keepalive の値を小さくすることが必要になる場合があります。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

この設定は、トランスポート接続を開いたまま、応答を待機してから、新しい接続を開くまでの時間を表します。 既定値は110秒です。

この設定は、keepalive 機能が無効になっている場合にのみ適用されます。通常は、長いポーリングトランスポートにのみ適用されます。 次の図は、この設定が長いポーリングトランスポート接続に与える影響を示しています。

![長いポーリングによるトランスポート接続](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

この設定は、`Disconnected` イベントを発生させる前に、トランスポート接続が失われた後に待機する時間を表します。 既定値は 30 秒です。 `DisconnectTimeout`を設定すると、`KeepAlive` は `DisconnectTimeout` 値の1/3 に自動的に設定されます。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

この設定は、アイドル状態の接続で keepalive パケットを送信するまでの待機時間を表します。 既定値は 10 秒です。 この値は、`DisconnectTimeout` 値の1/3 を超えることはできません。

`DisconnectTimeout` と `KeepAlive`の両方を設定する場合は、`DisconnectTimeout`後に `KeepAlive` を設定します。 それ以外の場合、`DisconnectTimeout` がタイムアウト値の1/3 に自動的に `KeepAlive` 設定されると、`KeepAlive` 設定は上書きされます。

Keepalive 機能を無効にする場合は、`KeepAlive` を null に設定します。 長いポーリングトランスポートでは、Keepalive 機能は自動的に無効になります。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>タイムアウトと keepalive の設定を変更する方法

これらの設定の既定値を変更するには、次の例に示すように、 *global.asax*ファイルの `Application_Start` で設定します。 サンプルコードに示されている値は、既定値と同じです。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>切断についてユーザーに通知する方法

アプリケーションによっては、接続の問題が発生したときに、ユーザーにメッセージを表示することが必要になる場合があります。 これを行う方法とタイミングには、いくつかのオプションがあります。 次のコードサンプルは、生成されたプロキシを使用する JavaScript クライアントを対象としています。

- SignalR が接続の問題を認識してから、再接続モードになる前に、すぐにメッセージを表示するために `connectionSlow` イベントを処理します。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- SignalR が切断を認識し、再接続モードになるとメッセージを表示するには、`reconnecting` イベントを処理します。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 再接続の試行がタイムアウトしたときにメッセージを表示するために `disconnected` イベントを処理します。このシナリオでは、サーバーとの接続を再確立する唯一の方法は、`Start` メソッドを呼び出して SignalR 接続を再起動することです。これにより、新しい接続 ID が作成されます。 次のコードサンプルでは、フラグを使用して、再接続のタイムアウト後にのみ通知を発行するようにしています。これは、`Stop` メソッドを呼び出すことによって発生した SignalR 接続の通常の終了後ではありません。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>継続的に再接続する方法

一部のアプリケーションでは、接続が失われ、再接続の試行がタイムアウトした後に、自動的に接続を再確立することが必要になる場合があります。これを行うには、`Closed` イベントハンドラー (JavaScript クライアントの`disconnected` イベントハンドラー) から `Start` メソッドを呼び出すことができます。 サーバーまたは物理接続が使用できない場合に、この処理が頻繁に行われないようにするために、`Start` を呼び出す前にしばらく待つことをお勧めします。 次のコードサンプルは、生成されたプロキシを使用する JavaScript クライアントを対象としています。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

モバイルクライアントで発生する可能性のある問題は、サーバーまたは物理接続が使用できないときに、連続した再接続を試行すると、不要なバッテリ消耗が発生する可能性があることです。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>サーバーコードでクライアントを切断する方法

SignalR バージョン1.1.1 には、クライアントを切断するための組み込みのサーバー API がありません。 [今後、この機能を追加する予定](https://github.com/SignalR/SignalR/issues/2101)があります。 現在の SignalR リリースでは、サーバーからクライアントを切断する最も簡単な方法は、クライアントで disconnect メソッドを実装し、そのメソッドをサーバーから呼び出すことです。 次のコードサンプルは、生成されたプロキシを使用する JavaScript クライアントの切断メソッドを示しています。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> セキュリティ-クライアントと提案された組み込み API を切断するこの方法では、悪意のあるコードを実行しているハッキングされたクライアントのシナリオに対処します。これは、クライアントが再接続したり、ハッキングされたコードが `stopClient` メソッドを削除したり、その動作を変更したりする可能性があるためです。 ステートフルなサービス拒否 (DOS) 保護を実装するための適切な場所は、フレームワークまたはサーバー層ではなく、フロントエンドインフラストラクチャにあります。
