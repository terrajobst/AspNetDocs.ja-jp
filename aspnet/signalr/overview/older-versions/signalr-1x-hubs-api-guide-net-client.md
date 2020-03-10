---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR Hub API ガイド-.NET クライアント (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: このドキュメントでは、Windows ストア (WinRT)、WPF、Silverlight、短所など、.NET クライアントで SignalR バージョン2用のハブ API を使用する方法の概要を説明します。
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505972"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a>ASP.NET SignalR Hub API ガイド-.NET クライアント (SignalR 1.x)

[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、Windows ストア (WinRT)、WPF、Silverlight、コンソールアプリケーションなど、.NET クライアントで SignalR バージョン2用のハブ API を使用する方法の概要を説明します。
> 
> SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。 サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。 クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。 SignalR は、クライアントとサーバーのすべての組み込みを処理します。
> 
> SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。 SignalR、ハブ、および永続的な接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては、[はじめに SignalR](../getting-started/index.md)を参照してください。

## <a name="overview"></a>概要

このドキュメントは、次のトピックに分かれています。

- [クライアントのセットアップ](#clientsetup)
- [接続を確立する方法](#establishconnection)

    - [Silverlight クライアントからのクロスドメイン接続](#slcrossdomain)
- [接続を構成する方法](#configureconnection)

    - [WPF クライアントで同時接続の最大数を設定する方法](#maxconnections)
    - [クエリ文字列パラメーターを指定する方法](#querystring)
    - [トランスポート方法を指定する方法](#transport)
    - [HTTP ヘッダーを指定する方法](#httpheaders)
    - [クライアント証明書を指定する方法](#clientcertificate)
- [ハブプロキシの作成方法](#proxy)
- [サーバーが呼び出すことができるクライアント上のメソッドを定義する方法](#callclient)

    - [パラメーターのないメソッド](#clientmethodswithoutparms)
    - [パラメーターを持つメソッド、パラメーターの型の指定](#clientmethodswithparmtypes)
    - [パラメーターを持つメソッド (パラメーターの動的オブジェクトの指定)](#clientmethodswithdynamparms)
    - [ハンドラーを削除する方法](#removehandler)
- [クライアントからサーバーメソッドを呼び出す方法](#callserver)
- [接続の有効期間イベントの処理方法](#connectionlifetime)
- [エラーの処理方法](#handleerrors)
- [クライアント側のログ記録を有効にする方法](#logging)
- [サーバーが呼び出すことができるクライアントメソッドの WPF、Silverlight、コンソールアプリケーションのコードサンプル](#wpfsl)

.NET クライアントプロジェクトのサンプルについては、次のリソースを参照してください。

- [gustavo-SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com on (WinRT、Silverlight、コンソールアプリの例)。
- [DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GITHUB.COM (WPF の例)。
- [SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (コンソールアプリの例) を使用します。

サーバーまたは JavaScript クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。

- [SignalR Hub API ガイド-サーバー](../guide-to-the-api/hubs-api-guide-server.md)
- [SignalR Hub API ガイド-JavaScript クライアント](../guide-to-the-api/hubs-api-guide-javascript-client.md)

API リファレンストピックへのリンクは、.NET 4.5 バージョンの API です。 .NET 4 を使用している場合は、 [.net 4 バージョンの API に関するトピック](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)を参照してください。

<a id="clientsetup"></a>

## <a name="client-setup"></a>クライアントのセットアップ

[SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet パッケージをインストールします ( [SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)パッケージではありません)。 このパッケージは、.NET 4 と .NET 4.5 の両方に対して、WinRT、Silverlight、WPF、コンソールアプリケーション、および Windows Phone クライアントをサポートします。

クライアントにインストールされている SignalR のバージョンが、サーバー上のバージョンと異なる場合、SignalR は多くの場合、差分に適合することができます。 たとえば、SignalR バージョン2.0 がリリースされ、それをサーバーにインストールした場合、サーバーは、1.1 がインストールされているクライアントと、2.0 がインストールされているクライアントをサポートします。 サーバー上のバージョンとクライアントのバージョンの違いが大きすぎる場合、SignalR は、クライアントが接続を確立しようとしたときに `InvalidOperationException` 例外をスローします。 エラーメッセージは "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" です。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>接続を確立する方法

接続を確立するには、`HubConnection` オブジェクトを作成し、プロキシを作成する必要があります。 接続を確立するには、`HubConnection` オブジェクトの `Start` メソッドを呼び出します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> JavaScript クライアントの場合は、`Start` メソッドを呼び出して接続を確立する前に、少なくとも1つのイベントハンドラーを登録する必要があります。 これは、.NET クライアントには必要ありません。 JavaScript クライアントの場合、生成されたプロキシコードは、サーバー上に存在するすべてのハブのプロキシを自動的に作成し、ハンドラーを登録することは、クライアントが使用するハブを指定する方法です。 ただし、.NET クライアントの場合はハブプロキシを手動で作成するので、SignalR はプロキシを作成するハブを使用することを前提としています。

このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。 別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)」を参照してください。

`Start` メソッドは、非同期的に実行されます。 接続が確立されるまで後続のコード行が実行されないようにするには、ASP.NET 4.5 非同期メソッドで `await` を使用するか、同期メソッドで `.Wait()` します。 WinRT クライアントでは `.Wait()` を使用しないでください。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

`HubConnection` クラスはスレッド セーフです。

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight クライアントからのクロスドメイン接続

Silverlight クライアントからのクロスドメイン接続を有効にする方法については、「[ドメインの境界を越えてサービスを利用可能](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)にする」を参照してください。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>接続を構成する方法

接続を確立する前に、次のいずれかのオプションを指定できます。

- 同時接続数の制限。
- クエリ文字列パラメーター。
- トランスポートメソッド。
- HTTP ヘッダー。
- クライアント証明書。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF クライアントで同時接続の最大数を設定する方法

WPF クライアントでは、同時接続の最大数を既定値の2から増やすことが必要になる場合があります。 推奨値は10です。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

詳細については、「 [Servicepointmanager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)」を参照してください。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>クエリ文字列パラメーターを指定する方法

クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。 次の例は、クライアントコードでクエリ文字列パラメーターを設定する方法を示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

次の例は、サーバーコードでクエリ文字列パラメーターを読み取る方法を示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>トランスポート方法を指定する方法

接続プロセスの一環として、SignalR クライアントは、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定するために、通常はサーバーとネゴシエートします。 使用するトランスポートが既にわかっている場合は、このネゴシエーションプロセスを省略できます。 トランスポートメソッドを指定するには、トランスポートオブジェクトを Start メソッドに渡します。 次の例は、クライアントコードでトランスポートメソッドを指定する方法を示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)名前空間には、トランスポートを指定するために使用できる次のクラスが含まれています。

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (サーバーとクライアントの両方で .net 4.5 が使用されている場合にのみ使用可能)
- [Autotransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (クライアントとサーバーの両方でサポートされている最適なトランスポートを自動的に選択します。 これは既定のトランスポートです。 このを `Start` メソッドに渡すことは、何も渡していないのと同じ効果があります)。

このリストには、ブラウザーでのみ使用されているため、この一覧には、事前にフレームトランスポートが含まれていません。

サーバーコードでトランスポート方法を確認する方法については、「 [ASP.NET SignalR HUB API Guide-server-Context プロパティからクライアントに関する情報を取得する方法](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)」を参照してください。 トランスポートとフォールバックの詳細については、「 [SignalR とフォールバックの概要](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP ヘッダーを指定する方法

HTTP ヘッダーを設定するには、connection オブジェクトの `Headers` プロパティを使用します。 次の例は、HTTP ヘッダーを追加する方法を示しています。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>クライアント証明書を指定する方法

クライアント証明書を追加するには、接続オブジェクトの `AddClientCertificate` メソッドを使用します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>ハブプロキシの作成方法

ハブがサーバーから呼び出すことができるメソッドを定義し、サーバーのハブでメソッドを呼び出すためには、接続オブジェクトで `CreateHubProxy` を呼び出して、ハブのプロキシを作成します。 `CreateHubProxy` に渡す文字列は、ハブクラスの名前、またはサーバーで使用されていた場合は `HubName` 属性によって指定された名前です。 名前が一致するかどうかを判断する際、大文字と小文字は区別されません。

**サーバー上のハブクラス**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**ハブクラスのクライアントプロキシを作成する**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

`HubName` 属性を使用してハブクラスを装飾する場合は、その名前を使用します。

**サーバー上のハブクラス**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

**ハブクラスのクライアントプロキシを作成する**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

プロキシオブジェクトはスレッドセーフです。 実際、同じ `hubName`で複数回 `HubConnection.CreateHubProxy` を呼び出すと、キャッシュされた同じ `IHubProxy` オブジェクトが取得されます。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上のメソッドを定義する方法

サーバーが呼び出すことができるメソッドを定義するには、プロキシの `On` メソッドを使用してイベントハンドラーを登録します。

メソッド名の一致では、大文字と小文字が区別されません。 たとえば、サーバー上の `Clients.All.UpdateStockPrice` は、クライアントで `updateStockPrice`、`updatestockprice`、または `UpdateStockPrice` を実行します。

UI を更新するためのメソッドコードを記述する方法については、クライアントプラットフォームによって要件が異なります。 ここでは、WinRT (Windows ストア .NET) クライアントの例を示します。 WPF、Silverlight、コンソールアプリケーションの例については、[このトピックで後述する別のセクション](#wpfsl)で説明します。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>パラメーターのないメソッド

処理しているメソッドにパラメーターがない場合は、`On` メソッドの非ジェネリックオーバーロードを使用します。

**パラメーターを指定せずにクライアントメソッドを呼び出すサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**パラメーターのないサーバーから呼び出されるメソッドの WinRT クライアントコード ([このトピックで後述する「WPF と Silverlight の例」を参照してください](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>パラメーターを使用したメソッドとパラメーターの型の指定

処理中のメソッドにパラメーターがある場合は、`On` メソッドのジェネリック型としてパラメーターの型を指定します。 `On` メソッドの汎用的なオーバーロードによって、最大8個のパラメーター (Windows Phone 7 では 4) を指定できるようになります。 次の例では、1つのパラメーターが `UpdateStockPrice` メソッドに送信されます。

**パラメーターを使用してクライアントメソッドを呼び出すサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**パラメーターに使用されるストッククラス**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

**パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアントコード ([このトピックで後述する「WPF と Silverlight の例」を参照してください](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>パラメーターを持つメソッド (パラメーターの動的オブジェクトの指定)

`On` メソッドのジェネリック型としてパラメーターを指定する代わりに、パラメーターを動的オブジェクトとして指定することもできます。

**パラメーターを使用してクライアントメソッドを呼び出すサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**パラメーターに使用されるストッククラス**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

**パラメーターの動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアントコード ([このトピックで後述する「WPF と Silverlight の例」を参照](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>ハンドラーを削除する方法

ハンドラーを削除するには、その `Dispose` メソッドを呼び出します。

**サーバーから呼び出されるメソッドのクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**ハンドラーを削除するクライアントコード**

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>クライアントからサーバーメソッドを呼び出す方法

サーバーでメソッドを呼び出すには、ハブプロキシで `Invoke` メソッドを使用します。

サーバーメソッドに戻り値がない場合は、`Invoke` メソッドの非ジェネリックオーバーロードを使用します。

**戻り値のないメソッドのサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**戻り値を持たないメソッドを呼び出すクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

サーバーメソッドに戻り値がある場合は、`Invoke` メソッドのジェネリック型として戻り値の型を指定します。

**戻り値を持ち、複合型パラメーターを受け取るメソッドのサーバーコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**パラメーターと戻り値に使用されるストッククラス**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

**ASP.NET 4.5 async メソッドで戻り値を持ち、複合型パラメーターを取るメソッドを呼び出すクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**同期メソッドで戻り値を持ち、複合型パラメーターを受け取るメソッドを呼び出すクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

`Invoke` メソッドは非同期的に実行され、`Task` オブジェクトを返します。 `await` または `.Wait()`を指定しない場合は、呼び出すメソッドが実行を終了する前に、次のコード行が実行されます。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>接続の有効期間イベントの処理方法

SignalR は、次のように処理できる接続の有効期間イベントを提供します。

- `Received`: 接続でデータを受信したときに発生します。 受信したデータを提供します。
- `ConnectionSlow`: クライアントが低速または頻繁に切断される接続を検出したときに発生します。
- `Reconnecting`: 基になるトランスポートが再接続を開始したときに発生します。
- `Reconnected`: 基になるトランスポートが再接続されたときに発生します。
- `StateChanged`: 接続状態が変化したときに発生します。 以前の状態と新しい状態を提供します。 接続状態の値の詳細については、「 [Connectionstate 列挙型](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)」を参照してください。
- `Closed`: 接続が切断されたときに発生します。

たとえば、致命的ではないが、断続的な接続の問題 (パフォーマンスの低下や頻繁に接続の切断など) が発生した場合に、警告メッセージを表示するには、`ConnectionSlow` イベントを処理します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](../guide-to-the-api/handling-connection-lifetime-events.md)」を参照してください。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>エラーの処理方法

サーバーで詳細なエラーメッセージを明示的に有効にしないと、エラーに関する最小限の情報が、エラーの後に SignalR によって返される例外オブジェクトに含まれます。 たとえば、`newContosoChatMessage` の呼び出しが失敗した場合、エラーオブジェクトのエラーメッセージには、セキュリティ上の理由により、実稼働環境でクライアントに詳細なエラーメッセージを送信する "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" が含まれます。ただし、トラブルシューティングのために詳細なエラーメッセージを有効にする場合は、サーバーで次のコードを使用してください。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR が発生するエラーを処理するには、connection オブジェクトに `Error` イベントのハンドラーを追加します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

メソッドの呼び出しで発生したエラーを処理するには、try-catch ブロックでコードをラップします。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>クライアント側のログ記録を有効にする方法

クライアント側のログ記録を有効にするには、接続オブジェクトの `TraceLevel` と `TraceWriter` のプロパティを設定します。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアントメソッドの WPF、Silverlight、コンソールアプリケーションのコードサンプル

サーバーが呼び出すことができるクライアントメソッドを定義するために、前に示したコードサンプルは WinRT クライアントに適用されます。 次のサンプルは、WPF、Silverlight、およびコンソールアプリケーションクライアントの同等のコードを示しています。

### <a name="methods-without-parameters"></a>パラメーターのないメソッド

**パラメーターを指定せずにサーバーから呼び出されるメソッドの WPF クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**パラメーターを指定せずにサーバーから呼び出されるメソッドの Silverlight クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**パラメーターを指定せずにサーバーから呼び出されるメソッドのコンソールアプリケーションクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>パラメーターを使用したメソッドとパラメーターの型の指定

**パラメーターを使用してサーバーから呼び出されるメソッドの WPF クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**パラメーターを使用してサーバーから呼び出されるメソッドの Silverlight クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**パラメーターを使用してサーバーから呼び出されるメソッドのコンソールアプリケーションクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>パラメーターを持つメソッド (パラメーターの動的オブジェクトの指定)

**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WPF クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**パラメーターの動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの Silverlight クライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドのコンソールアプリケーションクライアントコード**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
