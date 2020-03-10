---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hub API ガイド-JavaScript Client |Microsoft Docs
author: bradygaster
description: このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなどの JavaScript クライアントで SignalR バージョン2用のハブ API を使用する方法の概要を説明します。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431290"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR Hub API ガイド-JavaScript クライアント

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなど、JavaScript クライアントで SignalR version 2 用のハブ API を使用する方法の概要を説明します。
>
> SignalR Hub API を使用すると、サーバーから接続されたクライアントおよびクライアントからサーバーへのリモートプロシージャコール (Rpc) を行うことができます。 サーバーコードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行するメソッドを呼び出すことができます。 クライアントコードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出すことができます。 SignalR は、クライアントとサーバーのすべての組み込みを処理します。
>
> SignalR には、永続的な接続と呼ばれる下位レベルの API も用意されています。 SignalR、ハブ、および永続的な接続の概要については、「 [SignalR の概要](../getting-started/introduction-to-signalr.md)」を参照してください。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

## <a name="overview"></a>概要

このドキュメントは、次のトピックに分かれています。

- [生成されたプロキシとその機能](#genproxy)

    - [生成されたプロキシを使用する場合](#cantusegenproxy)
- [クライアントのセットアップ](#clientsetup)

    - [動的に生成されたプロキシを参照する方法](#dynamicproxy)
    - [SignalR によって生成されたプロキシの物理ファイルを作成する方法](#manualproxy)
- [接続を確立する方法](#establishconnection)

    - [$ hubConnection () によって作成されるオブジェクトと同じです。](#connequivalence)
    - [Start メソッドの非同期実行](#asyncstart)
- [ドメイン間接続を確立する方法](#crossdomain)
- [接続を構成する方法](#configureconnection)

    - [クエリ文字列パラメーターを指定する方法](#querystring)
    - [トランスポート方法を指定する方法](#transport)
- [ハブクラスのプロキシを取得する方法](#getproxy)
- [サーバーが呼び出すことができるクライアント上のメソッドを定義する方法](#callclient)
- [クライアントからサーバーメソッドを呼び出す方法](#callserver)
- [接続の有効期間イベントの処理方法](#connectionlifetime)
- [エラーの処理方法](#handleerrors)
- [クライアント側のログ記録を有効にする方法](#logging)

サーバーまたは .NET クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。

- [SignalR Hub API ガイド-サーバー](hubs-api-guide-server.md)
- [SignalR Hub API ガイド-.NET クライアント](hubs-api-guide-net-client.md)

SignalR 2 サーバーコンポーネントは .NET 4.5 でのみ使用できます (ただし、.net 4.0 の SignalR 2 用の .NET クライアントはあります)。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>生成されたプロキシとその機能

SignalR が生成するプロキシを使用して、または使用せずに、SignalR サービスと通信するように JavaScript クライアントをプログラミングできます。 プロキシでは、接続に使用するコードの構文を簡略化し、サーバーが呼び出すメソッドを記述して、サーバーでメソッドを呼び出すことができます。

サーバーメソッドを呼び出すためのコードを記述すると、生成されたプロキシによって、ローカル関数を実行しているかのような構文を使用できるようになります。 `invoke('serverMethod', arg1, arg2)`ではなく `serverMethod(arg1, arg2)` を記述できます。 また、生成されたプロキシ構文では、サーバーメソッド名を誤って指定した場合に、即時および intelligible のクライアント側エラーが有効になります。 また、プロキシを定義するファイルを手動で作成した場合は、サーバーメソッドを呼び出すコードを記述するための IntelliSense サポートを取得することもできます。

たとえば、サーバーに次のハブクラスがあるとします。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

次のコード例は、サーバーで `NewContosoChatMessage` メソッドを呼び出し、サーバーから `addContosoChatMessageToPage` メソッドの呼び出しを受信するための JavaScript コードを示しています。

**生成されたプロキシを使用する**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**生成されたプロキシを使用しない場合**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>生成されたプロキシを使用する場合

サーバーが呼び出すクライアントメソッドに対して複数のイベントハンドラーを登録する場合、生成されたプロキシを使用することはできません。 それ以外の場合は、コーディングの設定に基づいて、生成されたプロキシを使用するかどうかを選択できます。 使用しない場合は、クライアントコードの `script` 要素で "signalr/hub" URL を参照する必要はありません。

<a id="clientsetup"></a>

## <a name="client-setup"></a>クライアントのセットアップ

JavaScript クライアントには、jQuery および SignalR core JavaScript ファイルへの参照が必要です。 JQuery バージョンは、1.6.4、または1.7.2、1.8.2、1.9.1 などのメジャー以降のバージョンである必要があります。 生成されたプロキシを使用する場合は、SignalR によって生成されるプロキシ JavaScript ファイルへの参照も必要です。 次の例は、生成されたプロキシを使用する HTML ページで参照がどのように見えるかを示しています。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

これらの参照は、jQuery first、SignalR core、および SignalR proxy last という順序で指定する必要があります。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>動的に生成されたプロキシを参照する方法

前の例では、SignalR によって生成されるプロキシへの参照は、物理的なファイルではなく、動的に生成された JavaScript コードに対して行われます。 SignalR は、プロキシの JavaScript コードをその場で作成し、"/signalr/hubs" URL に応答してクライアントに提供します。 `MapSignalR` メソッドでサーバーの SignalR 接続に別のベース URL を指定した場合、動的に生成されるプロキシファイルの URL は、"/hub" が追加されたカスタム URL になります。

> [!NOTE]
> Windows 8 (Windows ストア) JavaScript クライアントの場合は、動的に生成されたファイルではなく、物理プロキシファイルを使用します。 詳細については、このトピックの「 [SignalR generated プロキシの物理ファイルを作成する方法](#manualproxy)」を参照してください。

ASP.NET MVC 4 または 5 Razor ビューで、チルダを使用して、プロキシファイルの参照でアプリケーションルートを参照します。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

MVC 5 での SignalR の使用の詳細については、「 [With SignalR AND MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」を参照してはじめにください。

ASP.NET MVC 3 Razor ビューでは、プロキシファイル参照に `Url.Content` を使用します。

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

ASP.NET Web フォームアプリケーションでは、プロキシファイル参照に `ResolveClientUrl` を使用するか、アプリルートの相対パス (チルダから始まる) を使用して ScriptManager で登録します。

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

一般的な規則として、CSS または JavaScript ファイルに使用する "/signalr/hubs" URL を指定する場合にも同じ方法を使用します。 チルダを使用せずに URL を指定した場合、シナリオによっては IIS Express を使用して Visual Studio でテストしたときにアプリケーションが正常に動作しますが、完全な IIS に配置すると、404エラーで失敗します。 詳細については、MSDN サイトの「 [Visual Studio での Web サーバーでの ASP.NET Web プロジェクトの](https://msdn.microsoft.com/library/58wxa9w5.aspx)**ルートレベルリソースへの参照の解決**」を参照してください。

Visual Studio 2017 でデバッグモードで web プロジェクトを実行するときに、ブラウザーとして Internet Explorer を使用すると、 **[スクリプト]** の下の**ソリューションエクスプローラー**にプロキシファイルが表示されます。

ファイルの内容を表示するには、 **[ハブ]** をダブルクリックします。 Visual Studio 2012 または2013と Internet Explorer を使用していない場合、またはデバッグモードになっていない場合は、"/signalR/hubs" URL を参照してファイルの内容を取得することもできます。 たとえば、サイトが `http://localhost:56699`で実行されている場合は、ブラウザーで `http://localhost:56699/SignalR/hubs` にアクセスします。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR によって生成されたプロキシの物理ファイルを作成する方法

動的に生成されたプロキシの代わりに、プロキシコードを持つ物理ファイルを作成し、そのファイルを参照することもできます。 キャッシュやバンドル動作を制御したり、サーバーメソッドへの呼び出しをコーディングするときに IntelliSense を使用したりすることができます。

プロキシファイルを作成するには、次の手順を実行します。

1. [SignalR](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet パッケージをインストールします。
2. コマンドプロンプトを開き、SignalR ファイルが格納されている*tools*フォルダーに移動します。 Tools フォルダーは次の場所にあります。

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 次のコマンドを入力します。

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.Dll*へのパスは、通常、プロジェクトフォルダー内の*bin*フォルダーです。

    このコマンドは、 *signalr*と同じフォルダーに、 *node.js*という名前のファイルを作成します。
4. *サーバー .js*ファイルをプロジェクト内の適切なフォルダーに配置し、アプリケーションに合わせて名前を変更し、"signalr/hub" 参照の代わりに参照を追加します。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>接続を確立する方法

接続を確立するには、接続オブジェクトを作成し、プロキシを作成して、サーバーから呼び出すことができるメソッドのイベントハンドラーを登録する必要があります。 プロキシとイベントハンドラーがセットアップされたら、`start` メソッドを呼び出して接続を確立します。

生成されたプロキシを使用している場合は、独自のコードで接続オブジェクトを作成する必要はありません。これは、生成されたプロキシコードによって自動的に行われるためです。

<a id="nogenconnection"></a>

**(生成されたプロキシを使用して) 接続を確立します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**(生成されたプロキシを使用せずに) 接続を確立します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。 別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)」を参照してください。

既定では、ハブの場所は現在のサーバーです。別のサーバーに接続している場合は、次の例に示すように、`start` メソッドを呼び出す前に URL を指定します。

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 通常は、`start` メソッドを呼び出して接続を確立する前に、イベントハンドラーを登録します。 接続の確立後にいくつかのイベントハンドラーを登録する場合は、これを行うことができますが、`start` メソッドを呼び出す前に、少なくとも1つのイベントハンドラーを登録する必要があります。 その理由の1つは、アプリケーションに多数のハブが存在する可能性がありますが、そのうちの1つだけを使用する場合は、すべてのハブで `OnConnected` イベントをトリガーしないことです。 接続が確立されると、ハブのプロキシにクライアントメソッドが存在することによって、`OnConnected` イベントをトリガーするように SignalR に指示します。 `start` メソッドを呼び出す前にイベントハンドラーを登録しないと、ハブでメソッドを呼び出すことができますが、ハブの `OnConnected` メソッドは呼び出されず、サーバーからクライアントメソッドは呼び出されません。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$ hubConnection () によって作成されるオブジェクトと同じです。

例からわかるように、生成されたプロキシを使用すると、`$.connection.hub` は接続オブジェクトを参照します。 これは、生成されたプロキシを使用していない場合に `$.hubConnection()` を呼び出すことによって得られるオブジェクトと同じです。 生成されたプロキシコードは、次のステートメントを実行して、接続を作成します。

![生成されたプロキシファイルでの接続の作成](hubs-api-guide-javascript-client/_static/image3.png)

生成されたプロキシを使用している場合は、生成されたプロキシを使用していないときに接続オブジェクトで実行できる `$.connection.hub` で何でも実行できます。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Start メソッドの非同期実行

`start` メソッドは、非同期的に実行されます。 [JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。これは、`pipe`、`done`、`fail`などのメソッドを呼び出すことによってコールバック関数を追加できることを意味します。 サーバーメソッドの呼び出しなど、接続が確立された後に実行するコードがある場合は、そのコードをコールバック関数に配置するか、コールバック関数から呼び出します。 `.done` のコールバックメソッドは、接続が確立された後、サーバーの `OnConnected` イベントハンドラーメソッドにあるコードの実行が完了した後に実行されます。

前の例の "現在接続されている" ステートメントを、(`.done` コールバックではなく) `start` メソッド呼び出しの後の次のコード行として配置すると、次の例に示すように、接続が確立される前に `console.log` 行が実行されます。

![接続が確立された後に実行されるコードを記述する方法が正しくありません](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>ドメイン間接続を確立する方法

通常、ブラウザーが `http://contoso.com`からページを読み込む場合、SignalR 接続は `http://contoso.com/signalr`の同じドメインにあります。 `http://contoso.com` のページが `http://fabrikam.com/signalr`に接続する場合は、ドメイン間接続が使用されます。 セキュリティ上の理由から、ドメイン間接続は既定で無効になっています。

SignalR 1.x では、クロスドメイン要求は単一の EnableCrossDomain フラグによって制御されていました。 このフラグは、JSONP 要求と CORS 要求の両方を制御します。 柔軟性を高めるため、すべての CORS サポートは SignalR のサーバーコンポーネントから削除されています (ブラウザーがサポートしていることが検出された場合、JavaScript クライアントは引き続き CORS を使用します)。また、これらのシナリオをサポートするために新しい OWIN ミドルウェアを利用できるようになりました。

クライアントで JSONP が必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、次に示すように、`HubConfiguration` オブジェクトの `EnableJSONP` を `true`に設定して、明示的に有効にする必要があります。 JSONP は、CORS よりも安全性が低いため、既定では無効になっています。

**プロジェクトに Owin を追加し**ます。このライブラリをインストールするには、パッケージマネージャーコンソールで次のコマンドを実行します。

`Install-Package Microsoft.Owin.Cors`

このコマンドにより、2.1.0 バージョンのパッケージがプロジェクトに追加されます。

### <a name="calling-usecors"></a>UseCors の呼び出し

 次のコードスニペットは、SignalR 2 でドメイン間接続を実装する方法を示しています。

**SignalR 2 でのクロスドメイン要求の実装**

次のコードは、SignalR 2 プロジェクトで CORS または JSONP を有効にする方法を示しています。 このコードサンプルでは、`MapSignalR`ではなく `Map` と `RunSignalR` を使用して、CORS ミドルウェアが、cors のサポートを必要とする SignalR 要求 (`MapSignalR`で指定されたパスのすべてのトラフィックではなく) に対してのみ実行されるようにします。マップは、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要があるその他のミドルウェアにも使用できます。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - コードで `jQuery.support.cors` を true に設定しないでください。
>
>     ![JQuery. サポートを true に設定しない](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR は CORS の使用を処理します。 `jQuery.support.cors` を true に設定すると、ブラウザーが CORS をサポートしていると SignalR が想定するため、JSONP は無効になります。
> - Localhost URL に接続している場合、Internet Explorer 10 はドメイン間接続を考慮しないため、サーバーでドメイン間接続を有効にしていない場合でも、アプリケーションは IE 10 でローカルに動作します。
> - Internet Explorer 9 でドメイン間接続を使用する方法の詳細については、[この StackOverflow スレッド](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)を参照してください。
> - Chrome でのクロスドメイン接続の使用の詳細については、[この StackOverflow スレッド](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)を参照してください。
> - このサンプルコードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。 別のベース URL を指定する方法については、「 [ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)」を参照してください。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>接続を構成する方法

接続を確立する前に、クエリ文字列パラメーターを指定することも、トランスポートメソッドを指定することもできます。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>クエリ文字列パラメーターを指定する方法

クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。 次の例は、クライアントコードでクエリ文字列パラメーターを設定する方法を示しています。

**(生成されたプロキシを使用して) start メソッドを呼び出す前に、クエリ文字列の値を設定します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**Start メソッドを呼び出す前に (生成されたプロキシを使用せずに) クエリ文字列の値を設定する**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

次の例は、サーバーコードでクエリ文字列パラメーターを読み取る方法を示しています。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>トランスポート方法を指定する方法

接続プロセスの一環として、SignalR クライアントは、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定するために、通常はサーバーとネゴシエートします。 使用するトランスポートが既にわかっている場合は、`start` メソッドを呼び出すときにトランスポートメソッドを指定することで、このネゴシエーションプロセスを省略できます。

**(生成されたプロキシを使用して) トランスポートメソッドを指定するクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**トランスポートメソッド (生成されたプロキシを除く) を指定するクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

別の方法として、複数のトランスポートメソッドを SignalR で試行する順序で指定することもできます。

**カスタムトランスポートフォールバックスキーム (生成されたプロキシを含む) を指定するクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**カスタムトランスポートフォールバックスキームを指定するクライアントコード (生成されたプロキシを除く)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

次の値を使用して、トランスポート方法を指定できます。

- "webSockets"
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

次の例は、接続で使用されているトランスポートメソッドを調べる方法を示しています。

**接続で使用されるトランスポートメソッド (生成されたプロキシを含む) を表示するクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**(生成されたプロキシを使用せずに) 接続で使用されるトランスポートメソッドを表示するクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

サーバーコードでトランスポート方法を確認する方法については、「 [ASP.NET SignalR HUB API Guide-server-Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。 トランスポートとフォールバックの詳細については、「 [SignalR とフォールバックの概要](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>ハブクラスのプロキシを取得する方法

作成した各接続オブジェクトは、1つ以上のハブクラスを含む SignalR サービスへの接続に関する情報をカプセル化します。 ハブクラスと通信するには、自分で作成したプロキシオブジェクト (生成されたプロキシを使用していない場合) または生成されたプロキシオブジェクトを使用します。

クライアントでは、プロキシ名はハブクラス名の camel 形式のバージョンです。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。

**サーバー上のハブクラス**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**ハブに対して生成されたクライアントプロキシへの参照を取得します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**ハブクラスのクライアントプロキシを作成します (プロキシを生成しません)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

`HubName` 属性を使用してハブクラスを装飾する場合は、大文字小文字を変更せずに正確な名前を使用します。

**HubName 属性を持つサーバーのハブクラス**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**ハブに対して生成されたクライアントプロキシへの参照を取得します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**ハブクラスのクライアントプロキシを作成します (プロキシを生成しません)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上のメソッドを定義する方法

サーバーがハブから呼び出すことができるメソッドを定義するには、生成されたプロキシの `client` プロパティを使用してハブプロキシにイベントハンドラーを追加するか、生成されたプロキシを使用しない場合は `on` メソッドを呼び出します。 パラメーターには、複雑なオブジェクトを指定できます。

`start` メソッドを呼び出して接続を確立する前に、イベントハンドラーを追加します。 (`start` メソッドを呼び出した後にイベントハンドラーを追加する場合は、このドキュメントの「[接続を確立する方法](#establishconnection)」のメモを参照し、生成されたプロキシを使用せずにメソッドを定義するために示されている構文を使用します)。

メソッド名の一致では、大文字と小文字が区別されません。 たとえば、サーバー上の `Clients.All.addContosoChatMessageToPage` は、クライアントで `AddContosoChatMessageToPage`、`addContosoChatMessageToPage`、または `addcontosochatmessagetopage` を実行します。

**クライアントで (生成されたプロキシを使用して) メソッドを定義します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**クライアントでメソッドを定義する別の方法 (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**クライアントでメソッドを定義します (生成されたプロキシを使用しない場合、または start メソッドを呼び出した後にを追加する場合)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**クライアントメソッドを呼び出すサーバーコード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

次の例には、メソッドパラメーターとしての複合オブジェクトが含まれています。

**(生成されたプロキシを使用して) 複雑なオブジェクトを受け取るクライアントのメソッドを定義します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**複合オブジェクト (生成されたプロキシを使用しない) を受け取るクライアントのメソッドを定義します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**複合オブジェクトを定義するサーバーコード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**複合オブジェクトを使用してクライアントメソッドを呼び出すサーバーコード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>クライアントからサーバーメソッドを呼び出す方法

クライアントからサーバーメソッドを呼び出すには、生成されたプロキシを使用していない場合は、生成されたプロキシの `server` プロパティを使用するか、ハブプロキシで `invoke` メソッドを使用します。 戻り値またはパラメーターは、複雑なオブジェクトにすることができます。

ハブのメソッド名の camel 形式のバージョンを渡します。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。

次の例は、戻り値を持たないサーバーメソッドを呼び出す方法と、戻り値を持つサーバーメソッドを呼び出す方法を示しています。

**HubMethodName 属性のないサーバーメソッド**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**パラメーターで渡される複合オブジェクトを定義するサーバーコード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

`HubMethodName` 属性を使用してハブメソッドを修飾した場合は、大文字小文字を変更せずにその名前を使用します。

HubMethodName 属性を持つ**サーバーメソッド**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

前の例は、戻り値を持たないサーバーメソッドを呼び出す方法を示しています。 次の例は、戻り値を持つサーバーメソッドを呼び出す方法を示しています。

**戻り値を持つメソッドのサーバーコード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

戻り値**に使用されるストッククラス**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**(生成されたプロキシを使用して) サーバーメソッドを呼び出すクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**(生成されたプロキシを使用せずに) サーバーメソッドを呼び出すクライアントコード**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>接続の有効期間イベントの処理方法

SignalR は、次のように処理できる接続の有効期間イベントを提供します。

- `starting`: 接続を介してデータが送信される前に発生します。
- `received`: 接続でデータを受信したときに発生します。 受信したデータを提供します。
- `connectionSlow`: クライアントが低速または頻繁に切断される接続を検出したときに発生します。
- `reconnecting`: 基になるトランスポートが再接続を開始したときに発生します。
- `reconnected`: 基になるトランスポートが再接続されたときに発生します。
- `stateChanged`: 接続状態が変化したときに発生します。 以前の状態と新しい状態 (接続、接続、再接続、または切断) を提供します。
- `disconnected`: 接続が切断されたときに発生します。

たとえば、遅延が発生する可能性がある接続の問題が発生した場合に警告メッセージを表示するには、`connectionSlow` イベントを処理します。

**(生成されたプロキシを使用して) connectionSlow イベントを処理します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**(生成されたプロキシを使用せずに) connectionSlow イベントを処理する**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>エラーの処理方法

SignalR JavaScript クライアントには、ハンドラーを追加できる `error` イベントが用意されています。 また、fail メソッドを使用して、サーバーメソッド呼び出しによって発生するエラーのハンドラーを追加することもできます。

サーバーで詳細なエラーメッセージを明示的に有効にしないと、エラーに関する最小限の情報が、エラーの後に SignalR によって返される例外オブジェクトに含まれます。 たとえば、`newContosoChatMessage` の呼び出しが失敗した場合、エラーオブジェクトのエラーメッセージには、セキュリティ上の理由により、実稼働環境でクライアントに詳細なエラーメッセージを送信する "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" が含まれます。ただし、トラブルシューティングのために詳細なエラーメッセージを有効にする場合は、サーバーで次のコードを使用してください。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

次の例は、エラーイベントのハンドラーを追加する方法を示しています。

**(生成されたプロキシを使用して) エラーハンドラーを追加します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**(生成されたプロキシを使用せずに) エラーハンドラーを追加します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

次の例は、メソッドの呼び出しからエラーを処理する方法を示しています。

**メソッドの呼び出し (生成されたプロキシを使用) からのエラーを処理する**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**(生成されたプロキシを使用せずに) メソッド呼び出しからのエラーを処理する**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

メソッドの呼び出しが失敗した場合は、`error` イベントも発生します。そのため、`error` メソッドハンドラー内のコードと `.fail` メソッドのコールバックが実行されます。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>クライアント側のログ記録を有効にする方法

接続でクライアント側のログ記録を有効にするには、接続オブジェクトの `logging` プロパティを設定してから、`start` メソッドを呼び出して接続を確立します。

**(生成されたプロキシを使用して) ログ記録を有効にする**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**(生成されたプロキシを使用しない) ログ記録を有効にする**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

ログを表示するには、ブラウザーの開発者ツールを開き、[コンソール] タブにアクセスします。これを行う方法を示す詳細な手順とスクリーンショットを示すチュートリアルについては、「 [ASP.NET Signalr を使用したサーバーブロードキャスト-ログ記録を有効](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)にする」を参照してください。
