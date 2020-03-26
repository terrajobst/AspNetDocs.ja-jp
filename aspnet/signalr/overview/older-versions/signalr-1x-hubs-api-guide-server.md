---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR Hub API ガイド-サーバー (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: このドキュメントでは、SignalR バージョン1.1 用の ASP.NET SignalR Hub API のサーバー側のプログラミングの概要について説明します。コードサンプル demonstratin...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468130"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a>ASP.NET SignalR Hub API ガイド-サーバー (SignalR 1.x)

[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、SignalR バージョン1.1 用の ASP.NET SignalR Hub API のサーバー側のプログラミングの概要について説明し、一般的なオプションを示すコードサンプルを示します。
> 
> SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。 サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。 クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。 SignalR は、クライアントとサーバーのすべての組み込みを処理します。
> 
> SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。 SignalR、ハブ、および永続的な接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては、[はじめに SignalR](index.md)を参照してください。

## <a name="overview"></a>概要

このドキュメントは、次のトピックに分かれています。

- [SignalR ルートを登録して SignalR オプションを構成する方法](#route)

    - [/Signalr URL](#signalrurl)
    - [SignalR オプションの構成](#options)
- [ハブクラスを作成して使用する方法](#hubclass)

    - [ハブオブジェクトの有効期間](#transience)
    - [JavaScript クライアントでのハブ名の camel 形式](#hubnames)
    - [複数のハブ](#multiplehubs)
- [クライアントが呼び出すことのできるハブクラスのメソッドを定義する方法](#hubmethods)

    - [JavaScript クライアントでのメソッド名の camel 形式の表記](#methodnames)
    - [非同期的に実行する場合](#asyncmethods)
    - [オーバーロードの定義](#overloads)
- [ハブクラスからクライアントメソッドを呼び出す方法](#callfromhub)

    - [RPC を受信するクライアントを選択する](#selectingclients)
    - [メソッド名に対するコンパイル時の検証がありません](#dynamicmethodnames)
    - [大文字と小文字を区別しないメソッド名の一致](#caseinsensitive)
    - [非同期実行](#asyncclient)
- [ハブクラスからグループメンバーシップを管理する方法](#groupsfromhub)

    - [Add メソッドと Remove メソッドの非同期実行](#asyncgroupmethods)
    - [グループメンバーシップの永続化](#grouppersistence)
    - [シングルユーザーグループ](#singleusergroups)
- [ハブクラスで接続の有効期間イベントを処理する方法](#connectionlifetime)

    - [OnConnected、Onconnected、および Onconnected が呼び出されたとき](#onreconnected)
    - [呼び出し元の状態が設定されていません](#nocallerstate)
- [コンテキストプロパティからクライアントに関する情報を取得する方法](#contextproperty)
- [クライアントとハブクラスの間で状態を渡す方法](#passstate)
- [ハブクラスでエラーを処理する方法](#handleErrors)
- [ハブクラスの外部からクライアントメソッドを呼び出し、グループを管理する方法](#callfromoutsidehub)

    - [クライアントメソッドの呼び出し](#callingclientsoutsidehub)
    - [グループメンバーシップの管理](#managinggroupsoutsidehub)
- [トレースを有効にする方法](#tracing)
- [ハブパイプラインをカスタマイズする方法](#hubpipeline)

クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。

- [SignalR Hub API ガイド-JavaScript クライアント](index.md)
- [SignalR Hub API ガイド-.NET クライアント](index.md)

API リファレンストピックへのリンクは、.NET 4.5 バージョンの API です。 .NET 4 を使用している場合は、 [.net 4 バージョンの API に関するトピック](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)を参照してください。

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a>SignalR ルートを登録して SignalR オプションを構成する方法

クライアントがハブへの接続に使用するルートを定義するには、アプリケーションの起動時に[Maphubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx)メソッドを呼び出します。 `MapHubs` は、`System.Web.Routing.RouteCollection` クラスの[拡張メソッド](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)です。 次の例は、 *global.asax*ファイルで SignalR hub ルートを定義する方法を示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

SignalR 機能を ASP.NET MVC アプリケーションに追加する場合は、SignalR ルートが他のルートの前に追加されていることを確認してください。 詳しくは、「[チュートリアル: SignalR と MVC 4](index.md)ではじめにます。

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/Signalr URL

既定では、クライアントがハブへの接続に使用するルート URL は "/signalr" です。 (この URL は、自動的に生成された JavaScript ファイルの "/signalr/hubs" URL と混同しないでください。 生成されたプロキシの詳細については、「 [SignalR HUB API Guide-JavaScript Client-生成されたプロキシとその機能](index.md)」を参照してください。

このベース URL を SignalR で使用できないような状況が発生する可能性があります。たとえば、 *signalr*という名前のフォルダーがプロジェクトにあり、その名前を変更したくないとします。 その場合は、次の例に示すように、ベース URL を変更できます (サンプルコードの "/signalr" は目的の URL に置き換えてください)。

**URL を指定するサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

**URL (生成されたプロキシを含む) を指定する JavaScript クライアントコード**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

**URL (生成されたプロキシを除く) を指定する JavaScript クライアントコード**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

**URL を指定する .NET クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>SignalR オプションの構成

`MapHubs` メソッドのオーバーロードを使用すると、カスタム URL、カスタム依存関係競合回避モジュール、および次のオプションを指定できます。

- ブラウザークライアントからのクロスドメイン呼び出しを有効にします。

    通常、ブラウザーが `http://contoso.com`からページを読み込む場合、SignalR 接続は `http://contoso.com/signalr`の同じドメインにあります。 `http://contoso.com` のページが `http://fabrikam.com/signalr`に接続する場合は、ドメイン間接続が使用されます。 セキュリティ上の理由から、ドメイン間接続は既定で無効になっています。 詳細については、「 [ASP.NET SignalR HUB API Guide-JavaScript Client-クロスドメイン接続を確立する方法](index.md)」を参照してください。
- 詳細なエラーメッセージを有効にします。

    エラーが発生した場合、SignalR の既定の動作では、何が起こったかについての詳細がなくても、クライアントに通知メッセージが送信されます。 悪意のあるユーザーがアプリケーションに対する攻撃に関する情報を使用できる可能性があるため、実稼働環境では詳細なエラー情報をクライアントに送信することはお勧めできません。 トラブルシューティングのために、このオプションを使用して、より詳細なエラー報告を一時的に有効にすることができます。
- 自動的に生成された JavaScript プロキシファイルを無効にします。

    既定では、ハブクラスのプロキシを含む JavaScript ファイルが、URL "/signalr/hubs" への応答として生成されます。 JavaScript プロキシを使用しない場合、またはこのファイルを手動で生成してクライアント内の物理ファイルを参照する場合は、このオプションを使用してプロキシ生成を無効にすることができます。 詳細については、「 [SignalR HUB API Guide-JavaScript Client-SignalR によって生成されたプロキシの物理ファイルを作成する方法](index.md)」を参照してください。

次の例は、`MapHubs` メソッドの呼び出しで SignalR 接続 URL とこれらのオプションを指定する方法を示しています。 カスタム URL を指定するには、例の "/signalr" を使用する URL に置き換えます。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>ハブクラスを作成して使用する方法

ハブを作成するには、 [Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)から派生するクラスを作成します。 次の例は、チャットアプリケーションの単純なハブクラスを示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

この例では、接続されたクライアントが `NewContosoChatMessage` メソッドを呼び出すことができ、受信したデータは、接続されているすべてのクライアントにブロードキャストされます。

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>ハブオブジェクトの有効期間

ハブクラスをインスタンス化したり、サーバー上の独自のコードからそのメソッドを呼び出したりすることはありません。SignalR Hub パイプラインによって実行されるすべての処理です。 SignalR は、クライアントがサーバーへの接続、切断、またはメソッド呼び出しを行うときなどのハブ操作を処理する必要があるたびに、ハブクラスの新しいインスタンスを作成します。

ハブクラスのインスタンスは一時的なものであるため、次のメソッド呼び出しの状態を維持するためにそれらを使用することはできません。 サーバーがクライアントからメソッド呼び出しを受け取るたびに、ハブクラスの新しいインスタンスによってメッセージが処理されます。 複数の接続とメソッド呼び出しによって状態を維持するには、データベースなどの他のメソッド、またはハブクラスの静的変数、または `Hub`から派生していない別のクラスを使用します。 データをメモリに保持する場合、ハブクラスの静的変数などのメソッドを使用すると、アプリドメインがリサイクルされるときにデータが失われます。

ハブクラスの外部で実行されている独自のコードからクライアントにメッセージを送信する場合、ハブクラスのインスタンスをインスタンス化することはできませんが、ハブクラスの SignalR context オブジェクトへの参照を取得することで実行できます。 詳細については、このトピックで後述[する「クライアントメソッドを呼び出し、ハブクラスの外部からグループを管理する方法](#callfromoutsidehub)」を参照してください。

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>JavaScript クライアントでのハブ名の camel 形式

既定では、JavaScript クライアントは、camel 形式のクラス名を使用してハブを参照します。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。 前の例は、JavaScript コードでは `contosoChatHub` と呼ばれています。

**[サーバー]**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

クライアントに使用する別の名前を指定する場合は、`HubName` 属性を追加します。 `HubName` 属性を使用する場合、JavaScript クライアントでの camel 形式の変更はありません。

**[サーバー]**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>複数のハブ

アプリケーションでは、複数のハブクラスを定義できます。 これを行うと、接続は共有されますが、グループは分離されます。

- すべてのクライアントは、同じ URL を使用して、サービス ("/signalr" またはカスタム URL を指定した場合はカスタム URL) との SignalR 接続を確立し、サービスで定義されているすべてのハブに対してその接続が使用されます。

    1つのクラスですべてのハブ機能を定義する場合と比較して、複数のハブでパフォーマンスの違いはありません。
- すべてのハブは、同じ HTTP 要求情報を取得します。

    すべてのハブが同じ接続を共有するため、サーバーが取得する唯一の HTTP 要求情報は、SignalR 接続を確立する元の HTTP 要求に含まれるものです。 接続要求を使用してクエリ文字列を指定することによってクライアントからサーバーに情報を渡す場合、異なるハブに対して異なるクエリ文字列を指定することはできません。 すべてのハブは同じ情報を受け取ります。
- 生成された JavaScript プロキシファイルには、1つのファイル内のすべてのハブのプロキシが含まれます。

    JavaScript プロキシの詳細については、「 [SignalR HUB API Guide-Javascript Client-生成されたプロキシとその機能](index.md)」を参照してください。
- グループはハブ内で定義されます。

    SignalR では、接続されたクライアントのサブセットにブロードキャストする名前付きグループを定義できます。 グループは、ハブごとに個別に保持されます。 たとえば、"Administrators" という名前のグループには、`ContosoChatHub` クラスのクライアントセットが1つ含まれており、同じグループ名が `StockTickerHub` クラスの異なるクライアントセットを参照しています。

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>クライアントが呼び出すことのできるハブクラスのメソッドを定義する方法

クライアントから呼び出すことができるようにする、ハブのメソッドを公開するには、次の例に示すようにパブリックメソッドを宣言します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

任意の C# のメソッドの場合と同様に、戻り値の型とパラメーター (複合型や配列を含む) を指定できます。 パラメーターで受け取った、または呼び出し元に返されたすべてのデータは、JSON を使用してクライアントとサーバーの間で通信されます。また、SignalR は、複雑なオブジェクトとオブジェクトの配列のバインドを自動的に処理します。

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript クライアントでのメソッド名の camel 形式の表記

既定では、JavaScript クライアントは、camel 形式のメソッド名を使用してハブメソッドを参照します。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。

**[サーバー]**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

クライアントに使用する別の名前を指定する場合は、`HubMethodName` 属性を追加します。

**[サーバー]**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>非同期的に実行する場合

メソッドが長時間実行される場合、またはデータベースの参照や web サービスの呼び出しなどの待機が必要な処理を実行する必要がある場合は、[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (戻り値 `void` の型 `T` の代わりに) [タスク&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) オブジェクトを返すことによって、ハブメソッドを非同期にします。 メソッドから `Task` オブジェクトを返すと、SignalR は `Task` が完了するまで待機してから、ラップされていない結果をクライアントに返します。そのため、クライアントでメソッド呼び出しをコーディングする方法に違いはありません。

ハブメソッドを非同期にすると、WebSocket トランスポートを使用するときに接続がブロックされることが回避されます。 ハブメソッドが同期的に実行され、トランスポートが WebSocket の場合、同じクライアントからのハブでの後続のメソッドの呼び出しは、ハブメソッドが完了するまでブロックされます。

次の例は、同期的または非同期的に実行するようにコード化された同じメソッドと、いずれかのバージョンの呼び出しに使用できる JavaScript クライアントコードを示しています。

**式**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

**ASP.NET 4.5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5 で非同期メソッドを使用する方法の詳細については、「 [ASP.NET MVC 4 での非同期メソッドの使用](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)」を参照してください。

<a id="overloads"></a>

### <a name="defining-overloads"></a>オーバーロードの定義

メソッドのオーバーロードを定義する場合は、各オーバーロードのパラメーターの数が異なる必要があります。 異なるパラメーターの型を指定するだけでオーバーロードを区別する場合、ハブクラスはコンパイルされますが、クライアントがいずれかのオーバーロードを呼び出そうとすると、実行時に SignalR サービスによって例外がスローされます。

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>ハブクラスからクライアントメソッドを呼び出す方法

サーバーからクライアントメソッドを呼び出すには、ハブクラスのメソッドで `Clients` プロパティを使用します。 次の例は、すべての接続されたクライアントで `addNewMessageToPage` を呼び出すサーバーコードと、JavaScript クライアントでメソッドを定義するクライアントコードを示しています。

**[サーバー]**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

クライアントメソッドから戻り値を取得することはできません。`int x = Clients.All.add(1,1)` などの構文は機能しません。

パラメーターの複合型と配列を指定できます。 次の例では、メソッドパラメーターでクライアントに複合型を渡します。

**複合オブジェクトを使用してクライアントメソッドを呼び出すサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

**複合オブジェクトを定義するサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>RPC を受信するクライアントを選択する

Clients プロパティは、RPC を受信するクライアントを指定するためのいくつかのオプションを提供する[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)オブジェクトを返します。

- 接続されたすべてのクライアント。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- 呼び出し元のクライアントのみ。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- 呼び出し元のクライアントを除くすべてのクライアント。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- 接続 ID で識別される特定のクライアント。

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    この例では、呼び出し元のクライアントで `addContosoChatMessageToPage` を呼び出し、`Clients.Caller`を使用した場合と同じ効果があります。
- 指定したクライアントを除くすべての接続されているクライアント。接続 ID で識別されます。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- 指定したグループの接続されているすべてのクライアント。

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- 指定されたクライアントを除く、指定されたグループ内のすべての接続されているクライアント。接続 ID で識別されます。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- 呼び出し元のクライアントを除く、指定されたグループ内のすべての接続されているクライアント。

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>メソッド名に対するコンパイル時の検証がありません

指定したメソッド名は動的オブジェクトとして解釈されます。つまり、IntelliSense やコンパイル時の検証は行われません。 式は実行時に評価されます。 メソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。クライアントに名前と一致するメソッドがある場合、そのメソッドが呼び出され、パラメーター値が渡されます。 一致するメソッドがクライアントに見つからない場合、エラーは発生しません。 クライアントメソッドを呼び出すときに、SignalR がバックグラウンドでクライアントに送信するデータの形式の詳細については、「 [SignalR の概要](index.md)」を参照してください。

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>大文字と小文字を区別しないメソッド名の一致

メソッド名の一致では、大文字と小文字が区別されません。 たとえば、サーバー上の `Clients.All.addContosoChatMessageToPage` は、クライアントで `AddContosoChatMessageToPage`、`addcontosochatmessagetopage`、または `addContosoChatMessageToPage` を実行します。

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>非同期実行

呼び出すメソッドは、非同期的に実行されます。 クライアントへのメソッド呼び出しの後に来るコードは、SignalR がクライアントへのデータの転送を完了するまで待たずにすぐに実行されます。ただし、後続のコード行がメソッドの完了を待機するように指定した場合は除きます。 次のコード例は、2つのクライアントメソッドを順番に実行する方法を示しています。1つは .NET 4.5 で動作するコードを使用し、もう1つは .NET 4 で動作するコードを使用します。

**.NET 4.5 の例**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

**.NET 4 の例**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

`await` または `ContinueWith` を使用して、次のコード行が実行される前にクライアントメソッドが終了するまで待機する場合、次のコード行が実行される前にクライアントが実際にメッセージを受信するという意味ではありません。 クライアントメソッド呼び出しの "完了" は、SignalR がメッセージの送信に必要なすべての処理を実行したことを意味します。 クライアントがメッセージを受信したことを確認する必要がある場合は、自分でその機構をプログラミングする必要があります。 たとえば、ハブで `MessageReceived` メソッドをコーディングすることができます。 `addContosoChatMessageToPage` また、クライアントで実行する必要のある作業を行った後 `MessageReceived` を呼び出すことができます。 ハブの `MessageReceived` では、元のメソッド呼び出しの実際のクライアントの受信と処理によって、どのような作業を行うことができます。

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>文字列変数をメソッド名として使用する方法

文字列変数をメソッド名として使用してクライアントメソッドを呼び出す場合は、`Clients.All` (または `Clients.Others`、`Clients.Caller`など) を `IClientProxy` にキャストし、 [invoke (methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)を呼び出します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>ハブクラスからグループメンバーシップを管理する方法

SignalR のグループは、接続されたクライアントの指定したサブセットにメッセージをブロードキャストする方法を提供します。 グループには任意の数のクライアントを含めることができ、クライアントは任意の数のグループのメンバーになることができます。

グループメンバーシップを管理するには、ハブクラスの `Groups` プロパティによって提供される[Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)メソッドと[Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)メソッドを使用します。 次の例は、クライアントコードによって呼び出されるハブメソッドで使用される `Groups.Add` および `Groups.Remove` メソッドと、それらを呼び出す JavaScript クライアントコードを示しています。

**[サーバー]**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

**生成されたプロキシを使用する JavaScript クライアント**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

明示的にグループを作成する必要はありません。 実際には、`Groups.Add`への呼び出しで名前を初めて指定したときにグループが自動的に作成されます。このグループのメンバーシップから最後の接続を削除すると、グループが削除されます。

グループメンバーシップの一覧またはグループの一覧を取得するための API はありません。 SignalR は、 [pub/sub モデル](http://en.wikipedia.org/wiki/Publish/subscribe)に基づいてクライアントとグループにメッセージを送信します。サーバーは、グループまたはグループメンバーシップの一覧を保持しません。 これにより、web ファームにノードを追加するたびに、SignalR が保持するすべての状態を新しいノードに反映する必要があるため、スケーラビリティを最大化できます。

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Add メソッドと Remove メソッドの非同期実行

`Groups.Add` メソッドと `Groups.Remove` メソッドは、非同期的に実行されます。 クライアントをグループに追加し、グループを使用してすぐにメッセージをクライアントに送信する場合は、`Groups.Add` メソッドが最初に終了するようにする必要があります。 次のコード例では、.NET 4.5 で動作するコードを使用して1つ、.NET 4 で動作するコードを使用して、その方法を示しています。

**.NET 4.5 の例**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

**.NET 4 の例**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>グループメンバーシップの永続化

SignalR は、ユーザーではなく接続を追跡します。そのため、ユーザーが接続を確立するたびにユーザーが同じグループにいる場合は、ユーザーが新しい接続を確立するたびに `Groups.Add` を呼び出す必要があります。

接続が一時的に失われた後、SignalR が接続を自動的に復元できる場合があります。 この場合、SignalR は、新しい接続を確立するのではなく、同じ接続を復元するため、クライアントのグループメンバーシップは自動的に復元されます。 これは、サーバーの再起動または障害の結果として一時的な中断が発生した場合でも可能です。これは、グループメンバーシップを含む各クライアントの接続状態がクライアントに対してラウンドトリップされるためです。 接続がタイムアウトになる前にサーバーがダウンし、新しいサーバーに置き換えられた場合、クライアントは自動的に新しいサーバーに再接続し、メンバーであるグループに再登録することができます。

接続が切断された後、または接続がタイムアウトしたとき、またはクライアントが切断されたとき (たとえば、ブラウザーが新しいページに移動したとき) に接続が自動的に復元できない場合、グループのメンバーシップは失われます。 次回ユーザーが接続するときは、新しい接続になります。 同じユーザーが新しい接続を確立するときにグループメンバーシップを維持するには、ユーザーが新しい接続を確立するたびに、アプリケーションがユーザーとグループの間の関連付けを追跡し、グループメンバーシップを復元する必要があります。

接続と再接続の詳細については、このトピックで後述[する「ハブクラスで接続の有効期間イベントを処理する方法](#connectionlifetime)」を参照してください。

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>シングルユーザーグループ

SignalR を使用するアプリケーションは、通常、どのユーザーがメッセージを送信したか、どのユーザーがメッセージを受信する必要があるかを知るために、ユーザーと接続の間の関連付けを追跡する必要があります。 グループは、そのために一般的に使用される2つのパターンのいずれかで使用されます。

- シングルユーザーグループ。

    ユーザー名をグループ名として指定し、ユーザーが接続または再接続するたびに現在の接続 ID をグループに追加することができます。 グループに送信するユーザーにメッセージを送信します。 この方法の欠点は、ユーザーがオンラインであるかオフラインであるかを確認する方法がグループに提供されていないことです。
- ユーザー名と接続 Id の間の関連付けを追跡します。

    各ユーザー名と1つまたは複数の接続 Id の間の関連付けをディクショナリまたはデータベースに格納し、ユーザーが接続または切断するたびに格納されているデータを更新することができます。 ユーザーにメッセージを送信するには、接続 Id を指定します。 この方法の欠点は、より多くのメモリを必要とすることです。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>ハブクラスで接続の有効期間イベントを処理する方法

接続の有効期間イベントを処理する一般的な理由は、ユーザーが接続されているかどうかを追跡し、ユーザー名と接続 Id の関連付けを追跡することです。 クライアントが接続または切断したときに独自のコードを実行するには、次の例に示すように、ハブクラスの `OnConnected`、`OnDisconnected`、および `OnReconnected` の仮想メソッドをオーバーライドします。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>OnConnected、Onconnected、および Onconnected が呼び出されたとき

ブラウザーが新しいページに移動するたびに、新しい接続を確立する必要があります。つまり、SignalR は、`OnDisconnected` メソッドを実行し、その後に `OnConnected` メソッドを実行します。 SignalR は、新しい接続が確立されるときに常に新しい接続 ID を作成します。

SignalR メソッドは、接続が一時的に切断されたときに呼び出されます。これは、ケーブルが一時的に切断され、接続がタイムアウトする前に再接続された場合などです。 `OnReconnected``OnDisconnected` メソッドは、ブラウザーが新しいページに移動したときなど、クライアントが切断され、SignalR が自動的に再接続できない場合に呼び出されます。 したがって、特定のクライアントに対して考えられる一連のイベントは、`OnConnected`、`OnReconnected`、`OnDisconnected`です。または `OnConnected`、`OnDisconnected`ます。 特定の接続に対して、シーケンス `OnConnected`、`OnDisconnected`、`OnReconnected` は表示されません。

`OnDisconnected` メソッドは、サーバーがダウンしたときやアプリドメインがリサイクルされたときなど、一部のシナリオでは呼び出されません。 別のサーバーがオンラインになるか、アプリケーションドメインがリサイクルを完了すると、一部のクライアントが再接続して `OnReconnected` イベントを発生させることができる場合があります。

詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](index.md)」を参照してください。

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>呼び出し元の状態が設定されていません

接続の有効期間イベントハンドラーメソッドは、サーバーから呼び出されます。つまり、クライアントの `state` オブジェクトに格納されているすべての状態は、サーバーの `Caller` プロパティに設定されません。 `state` オブジェクトと `Caller` プロパティの詳細については、このトピックの「[クライアントとハブクラス間で状態を渡す方法](#passstate)」を参照してください。

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>コンテキストプロパティからクライアントに関する情報を取得する方法

クライアントに関する情報を取得するには、ハブクラスの `Context` プロパティを使用します。 `Context` プロパティは、次の情報へのアクセスを提供する[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)オブジェクトを返します。

- 呼び出し元クライアントの接続 ID。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    接続 ID は、SignalR によって割り当てられる GUID です (独自のコードで値を指定することはできません)。 接続ごとに1つの接続 ID があり、アプリケーションに複数のハブがある場合は、すべてのハブで同じ接続 ID が使用されます。
- HTTP ヘッダーデータ。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    `Context.Headers`から HTTP ヘッダーを取得することもできます。 同じことに対する複数の参照があるのは、`Context.Headers` が先に作成され、`Context.Request` プロパティが後で追加され、`Context.Headers` が旧バージョンとの互換性のために保持されているためです。
- 文字列データをクエリします。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    `Context.QueryString`からクエリ文字列データを取得することもできます。

    このプロパティで取得するクエリ文字列は、SignalR 接続を確立した HTTP 要求で使用されたクエリ文字列です。 クライアントにクエリ文字列パラメーターを追加するには、接続を構成します。これは、クライアントに関するデータをクライアントからサーバーに渡す便利な方法です。 次の例は、生成されたプロキシを使用するときに、JavaScript クライアントにクエリ文字列を追加する方法の1つを示しています。

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    クエリ文字列パラメーターの設定の詳細については、 [JavaScript](index.md)および[.NET](index.md)クライアントの API ガイドを参照してください。

    接続に使用されるトランスポートメソッドは、SignalR によって内部的に使用される他の値と共に、クエリ文字列データで確認できます。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    `transportMethod` の値は、"Websocket"、"Serverのイベント"、"" 前の Verframe "または" longPolling "になります。 `OnConnected` イベントハンドラーメソッドでこの値を確認した場合、一部のシナリオでは、最初に接続に対してネゴシエートされた最後のトランスポートメソッドではないトランスポート値が取得されることがあります。 その場合、メソッドは例外をスローし、最後のトランスポートメソッドが確立されると、後で再度呼び出されます。
- Cookie.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    `Context.RequestCookies`から cookie を取得することもできます。
- ユーザー情報。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- 要求の HttpContext オブジェクト:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    このメソッドは、SignalR 接続の `HttpContext` オブジェクトを取得するために `HttpContext.Current` を取得する代わりに使用します。

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>クライアントとハブクラスの間で状態を渡す方法

クライアントプロキシには `state` オブジェクトが用意されており、各メソッド呼び出しでサーバーに送信するデータを格納できます。 サーバーでは、クライアントによって呼び出されるハブメソッドの `Clients.Caller` プロパティで、このデータにアクセスできます。 `Clients.Caller` プロパティは、接続の有効期間イベントハンドラーメソッド `OnConnected`、`OnDisconnected`、および `OnReconnected`には設定されません。

`state` オブジェクトと `Clients.Caller` プロパティのデータの作成または更新は、双方向で機能します。 サーバーの値を更新して、クライアントに返されるようにすることができます。

次の例は、すべてのメソッド呼び出しを使用してサーバーに送信するための状態を格納する JavaScript クライアントコードを示しています。

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

次の例は、.NET クライアントの同等のコードを示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

ハブクラスでは、`Clients.Caller` プロパティでこのデータにアクセスできます。 次の例は、前の例で参照されている状態を取得するコードを示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> 状態を永続化するためのこのメカニズムは、大量のデータを対象としていません。これは、`state` または `Clients.Caller` プロパティに格納されているすべてのものが、すべてのメソッド呼び出しでラウンドトリップされるためです。 これは、ユーザー名やカウンターなどの小さな項目に便利です。

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>ハブクラスでエラーを処理する方法

ハブクラスのメソッドで発生したエラーを処理するには、次のいずれかまたは両方の方法を使用します。

- Try catch ブロックにメソッドコードをラップし、例外オブジェクトをログに記録します。 デバッグの目的でクライアントに例外を送信することはできますが、セキュリティ上の理由から、実稼働環境でクライアントに詳細情報を送信することはお勧めしません。
- [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)メソッドを処理するハブパイプラインモジュールを作成します。 次の例は、エラーをログに記録するパイプラインモジュールを示しています。その後、モジュールをハブパイプラインに挿入する global.asax 内のコードを示します。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

ハブパイプラインモジュールの詳細については、このトピックで後述[する「ハブパイプラインをカスタマイズする方法](#hubpipeline)」を参照してください。

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>トレースを有効にする方法

サーバー側のトレースを有効にするには、次の例に示すように、web.config ファイルに system.web 要素を追加します。

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

Visual Studio でアプリケーションを実行すると、 **[出力]** ウィンドウにログが表示されます。

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>ハブクラスの外部からクライアントメソッドを呼び出し、グループを管理する方法

ハブクラスとは異なるクラスからクライアントメソッドを呼び出すには、ハブの SignalR context オブジェクトへの参照を取得し、それを使用してクライアント上のメソッドを呼び出すか、グループを管理します。

次のサンプル `StockTicker` クラスは、context オブジェクトを取得し、それをクラスのインスタンスに格納し、そのクラスインスタンスを静的プロパティに格納します。また、シングルトンクラスインスタンスのコンテキストを使用して、`StockTickerHub`という名前のハブに接続されているクライアントで `updateStockPrice` メソッドを呼び出します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

有効期間が長いオブジェクトでコンテキストを複数回使用する必要がある場合は、参照を一度取得し、毎回再度取得するのではなく保存します。 コンテキストを一度取得すると、SignalR は、ハブメソッドがクライアントメソッドの呼び出しを行うのと同じ順序で、メッセージをクライアントに送信します。 ハブの SignalR コンテキストの使用方法を示すチュートリアルについては、「 [ASP.NET SignalR を使用したサーバーブロードキャスト](index.md)」を参照してください。

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>クライアントメソッドの呼び出し

どのクライアントが RPC を受信するかを指定できますが、ハブクラスからを呼び出す場合よりもオプションが少なくて済みます。 その理由は、コンテキストがクライアントからの特定の呼び出しに関連付けられていないため、`Clients.Others`、`Clients.Caller`、`Clients.OthersInGroup`など、現在の接続 ID に関する知識を必要とするメソッドが使用できないことです。 次のオプションを使用できます。

- 接続されたすべてのクライアント。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- 接続 ID で識別される特定のクライアント。

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- 指定したクライアントを除くすべての接続されているクライアント。接続 ID で識別されます。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- 指定したグループの接続されているすべてのクライアント。

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- 指定されたクライアントを除く、指定されたグループ内のすべての接続されているクライアント。接続 ID で識別されます。

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

ハブクラスのメソッドから非ハブクラスを呼び出す場合は、現在の接続 ID を渡し、それを `Clients.Client`、`Clients.AllExcept`、または `Clients.Group` と共に使用して、`Clients.Caller`、`Clients.Others`、または `Clients.OthersInGroup`をシミュレートすることができます。 次の例では、`MoveShapeHub` クラスが `Broadcaster` クラスに接続 ID を渡して、`Broadcaster` クラスが `Clients.Others`をシミュレートできるようにします。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>グループメンバーシップの管理

グループを管理する場合、ハブクラスの場合と同じオプションがあります。

- クライアントをグループに追加する

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- クライアントをグループから削除する

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>ハブパイプラインをカスタマイズする方法

SignalR を使用すると、独自のコードをハブパイプラインに挿入できます。 次の例は、クライアントから受信した各受信メソッド呼び出しとクライアントで呼び出された送信メソッド呼び出しをログに記録するカスタムハブパイプラインモジュールを示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

*Global.asax*ファイルの次のコードは、モジュールをハブパイプラインで実行するように登録します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

オーバーライド可能な方法は多数あります。 完全な一覧については、「 [HubPipelineModule メソッド](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)」を参照してください。
