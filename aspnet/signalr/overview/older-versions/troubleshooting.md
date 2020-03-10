---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR のトラブルシューティング (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: この記事では、SignalR アプリケーションの開発に関する一般的な問題について説明します。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468100"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR トラブルシューティング (SignalR 1.x)

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、SignalR に関する一般的なトラブルシューティングの問題について説明します。

このドキュメントには、次のセクションが含まれています。

- [クライアントとサーバーの間でメソッドをサイレントモードで呼び出すことができない](#connection)
- [その他の接続の問題](#other)
- [コンパイルとサーバー側のエラー](#server)
- [Visual Studio の問題](#vs)
- [インターネットインフォメーションサービスの問題](#iis)
- [Azure の問題](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>クライアントとサーバーの間でメソッドをサイレントモードで呼び出すことができない

ここでは、クライアントとサーバーの間でメソッド呼び出しが失敗し、意味のあるエラーメッセージが表示されない場合に発生する可能性のある原因について説明します。 SignalR アプリケーションでは、クライアントが実装するメソッドに関する情報はサーバーにありません。サーバーがクライアントメソッドを呼び出すと、メソッド名とパラメーターデータがクライアントに送信され、メソッドは、サーバーが指定した形式で存在する場合にのみ実行されます。 一致するメソッドがクライアントに見つからない場合は、何も起こりません。サーバーでエラーメッセージは生成されません。

呼び出されていないクライアントメソッドをさらに詳しく調査するには、ハブで start メソッドを呼び出してから、サーバーからの呼び出しを確認する前に、ログ記録を有効にすることができます。 JavaScript アプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (javascript クライアントバージョン)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)」を参照してください。 .NET クライアントアプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (.Net クライアントのバージョン)](../guide-to-the-api/hubs-api-guide-net-client.md#logging)」を参照してください。

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>間違った方法、不適切なメソッドシグネチャ、または間違ったハブ名

呼び出されたメソッドの名前またはシグネチャがクライアントの適切なメソッドと完全に一致しない場合、呼び出しは失敗します。 サーバーによって呼び出されたメソッド名がクライアント上のメソッドの名前と一致していることを確認します。 また、SignalR は、JavaScript に適した camel 形式のメソッドを使用してハブプロキシを作成します。そのため、サーバー上で `SendMessage` というメソッドをクライアントプロキシで `sendMessage` と呼びます。 サーバー側コードで `HubName` 属性を使用する場合は、使用されている名前が、クライアントでハブの作成に使用された名前と一致していることを確認します。 `HubName` 属性を使用しない場合は、JavaScript クライアントのハブの名前が camel 形式であることを確認します。たとえば、ChatHub の代わりに chatHub のようにします。

### <a name="duplicate-method-name-on-client"></a>クライアントでメソッド名が重複しています

大文字と小文字のみが異なる、クライアントに重複するメソッドがないことを確認します。 クライアントアプリケーションに `sendMessage`というメソッドがある場合は、`SendMessage` と呼ばれるメソッドも存在しないことを確認します。

### <a name="missing-json-parser-on-the-client"></a>クライアントに JSON パーサーがありません

SignalR を使用するには、サーバーとクライアント間の呼び出しをシリアル化するために JSON パーサーが存在する必要があります。 クライアントに組み込みの JSON パーサー (Internet Explorer 7 など) がない場合は、アプリケーションに1つを含める必要があります。 JSON パーサーは[こちら](http://nuget.org/packages/json2)からダウンロードできます。

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Hub と PersistentConnection 構文の混在

SignalR は、2つの通信モデル (ハブと PersistentConnections) を使用します。 これら2つの通信モデルを呼び出すための構文は、クライアントコードによって異なります。 サーバーコードにハブを追加した場合は、すべてのクライアントコードで適切なハブ構文が使用されていることを確認します。

**JavaScript クライアントで PersistentConnection を作成する JavaScript クライアントコード**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Javascript クライアントでハブプロキシを作成する JavaScript クライアントコード**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C#ルートを PersistentConnection にマップするサーバーコード**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C#ハブまたは複数のアプリケーションがある場合は複数のハブにルートをマップするサーバーコード**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>サブスクリプションが追加される前に接続が開始されました

サーバーから呼び出すことができるメソッドがプロキシに追加される前にハブの接続が開始されると、メッセージは受信されません。 次の JavaScript コードはハブを適切に起動しません。

**ハブメッセージの受信を許可しない JavaScript クライアントコードが正しくありません**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

代わりに、Start を呼び出す前にメソッドサブスクリプションを追加します。

**ハブにサブスクリプションを正しく追加する JavaScript クライアントコード**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>ハブプロキシにメソッド名がありません

サーバーで定義されているメソッドがクライアントでサブスクライブされていることを確認します。 サーバーによってメソッドが定義されている場合でも、クライアントプロキシに追加する必要があります。 メソッドは、次の方法でクライアントプロキシに追加できます (このメソッドは、ハブではなく、ハブの `client` メンバーに追加されることに注意してください)。

**ハブプロキシにメソッドを追加する JavaScript クライアントコード**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>ハブまたはハブのメソッドがパブリックとして宣言されていません

クライアントで表示されるようにするには、ハブの実装とメソッドを `public`として宣言する必要があります。

### <a name="accessing-hub-from-a-different-application"></a>別のアプリケーションからのハブへのアクセス

SignalR Hub にアクセスできるのは、SignalR クライアントを実装するアプリケーションのみです。 SignalR は、他の通信ライブラリ (SOAP や WCF web サービスなど) と相互運用することはできません。ターゲットプラットフォームに使用できる SignalR クライアントがない場合は、サーバーのエンドポイントに直接アクセスすることはできません。

### <a name="manually-serializing-data"></a>手動によるデータのシリアル化

SignalR は自動的に JSON を使用してメソッドのパラメーターをシリアル化します。自分で行う必要はありません。

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>OnDisconnected 関数のクライアントでリモートハブのメソッドが実行されませんでした

この動作は仕様です。 `OnDisconnected` が呼び出されると、ハブは既に `Disconnected` 状態に入っています。これにより、これ以上ハブメソッドを呼び出すことはできません。

**C#OnDisconnected イベントでコードを正しく実行するサーバーコード**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>接続数の上限に達しました

Windows 7 などのクライアントオペレーティングシステムで IIS の完全バージョンを使用する場合は、10接続の制限が適用されます。 クライアント OS を使用する場合は、この制限を回避するために、代わりに IIS Express を使用します。

### <a name="cross-domain-connection-not-set-up-properly"></a>ドメイン間接続が適切に設定されていません

ドメイン間接続 (SignalR URL がホスティングページと同じドメインにない接続) が正しく設定されていない場合、接続はエラーメッセージなしで失敗する可能性があります。 ドメイン間通信を有効にする方法については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>NTLM を使用した接続 (Active Directory) が .NET クライアントで動作しない

接続が正しく構成されていない場合、ドメインセキュリティを使用する .NET クライアントアプリケーションの接続が失敗することがあります。 ドメイン環境で SignalR を使用するには、必要な接続プロパティを次のように設定します。

**C#接続資格情報を実装するクライアントコード**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>その他の接続の問題

このセクションでは、接続中に発生する特定の現象またはエラーメッセージの原因と解決方法について説明します。

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"データを送信する前に開始する必要があります" エラー

このエラーは、接続が開始される前にコードが SignalR オブジェクトを参照する場合によく見られます。 サーバーで定義されているメソッドを呼び出すのと同様に、ハンドラーの wireup とを、接続の完了後に追加する必要があります。 `Start` の呼び出しが非同期であるため、呼び出しの後のコードを実行してから完了することができます。 接続が完全に開始された後にハンドラーを追加する最善の方法は、start メソッドにパラメーターとして渡されるコールバック関数にそれらを配置することです。

**SignalR オブジェクトを参照するイベントハンドラーを正しく追加する JavaScript クライアントコード**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

このエラーは、SignalR オブジェクトがまだ参照されている間に接続が停止した場合にも表示されます。

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 が永続的に移動されました" または "302 を一時的に移動" エラー

このエラーは、プロジェクトに SignalR という名前のフォルダーが含まれている場合に発生する可能性があります。これにより、自動的に作成されたプロキシが妨げられます。 このエラーを回避するには、アプリケーションで `SignalR` という名前のフォルダーを使用しないようにするか、自動プロキシ生成をオフにします。 [生成されたプロキシとその](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)詳細については、「」を参照してください。

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET または Silverlight クライアントで "403 の許可されていません" エラー

このエラーは、ドメイン間通信が正しく有効になっていないクロスドメイン環境で発生する可能性があります。 ドメイン間通信を有効にする方法については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。 Silverlight クライアントでドメイン間接続を確立する方法については、「 [silverlight クライアントからのクロスドメイン](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)接続」を参照してください。

### <a name="404-not-found-error"></a>"404 が見つかりません" エラー

この問題にはいくつかの原因があります。 次のすべてを確認します。

- **ハブプロキシアドレスの参照が正しくフォーマットされていません:** このエラーは、生成されたハブプロキシアドレスへの参照が正しく書式設定されていない場合によく発生します。 ハブアドレスへの参照が適切に作成されていることを確認します。 詳細について[は、「動的に生成されたプロキシを参照する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)」を参照してください。
- **ハブルートを追加する前に、アプリケーションにルートを追加します。** アプリケーションで他のルートを使用する場合は、追加された最初のルートが `MapHubs`の呼び出しであることを確認します。

### <a name="500-internal-server-error"></a>"500 内部サーバーエラー"

これは非常に一般的なエラーであり、さまざまな原因が考えられます。 エラーの詳細は、サーバーのイベントログに表示されるか、またはサーバーのデバッグによって検出されます。 詳細なエラー情報を取得するには、サーバーで詳細なエラーを有効にします。 詳細については、「 [Hub クラスでエラーを処理する方法](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)」を参照してください。

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt; が定義されていません" エラー

このエラーは、`MapHubs` の呼び出しが正しく行われない場合に発生します。 詳細について[は、「How to register The SignalR route」および「Configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) 」を参照してください。

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException がユーザーコードによって処理されませんでした

メソッドに送信するパラメーターに、シリアル化できない型 (ファイルハンドルやデータベース接続など) が含まれていないことを確認します。 クライアントに送信したくないサーバー側オブジェクト (セキュリティのため、またはシリアル化の理由) でメンバーを使用する必要がある場合は、`JSONIgnore` 属性を使用します。

### <a name="protocol-error-unknown-transport-error"></a>"プロトコルエラー: 不明なトランスポート" エラー

このエラーは、SignalR が使用するトランスポートをクライアントがサポートしていない場合に発生する可能性があります。 SignalR で使用できるブラウザーの詳細については[、「トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript Hub プロキシの生成が無効になりました。"

このエラーは、`signalr/hubs`で動的に生成されたプロキシへの参照も含め、`DisableJavaScriptProxies` が設定されている場合に発生します。 プロキシを手動で作成する方法の詳細については、「[生成されたプロキシとその機能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)」を参照してください。

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"接続 ID の形式が正しくありません" または "active SignalR 接続中にユーザー id を変更できません" というエラーが発生する

このエラーは、認証が使用されていて、接続が停止される前にクライアントがログアウトされている場合に発生する可能性があります。 この問題を解決するには、クライアントをログに記録する前に、SignalR 接続を停止します。

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"キャッチされていないエラー: SignalR: jQuery が見つかりません。 SignalR ファイルの前に jQuery が参照されていることを確認してください。 "エラー

SignalR JavaScript クライアントでは、jQuery を実行する必要があります。 JQuery への参照が正しいこと、使用されているパスが有効であること、および jQuery への参照が SignalR への参照の前にあることを確認します。

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"キャッチされていない TypeError: プロパティ '&lt;プロパティ&gt;' undefined ' エラーを読み取ることができません

このエラーは、jQuery またはハブプロキシが正しく参照されていない場合に発生します。 JQuery とハブプロキシへの参照が正しいこと、使用されているパスが有効であること、および jQuery への参照がハブプロキシへの参照の前にあることを確認します。 ハブプロキシへの既定の参照は、次のようになります。

**ハブプロキシを正しく参照する HTML クライアント側コード**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException はユーザーコードによって処理されませんでした" エラー

このエラーは、`Hub.On` の不適切なオーバーロードが使用されている場合に発生する可能性があります。 メソッドに戻り値がある場合は、戻り値の型をジェネリック型パラメーターとして指定する必要があります。

**クライアントで定義されたメソッド (生成されたプロキシを除く)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>接続 ID が一致していないか、ページ読み込み間の接続が壊れています

この動作は仕様です。 ハブオブジェクトはページオブジェクトでホストされるため、ページが更新されるとハブは破棄されます。 複数ページアプリケーションでは、ページの読み込み間で一貫性を保つために、ユーザーと接続 Id の間の関連付けを維持する必要があります。 接続 Id は、`ConcurrentDictionary` オブジェクトまたはデータベースのいずれかのサーバーに格納できます。

### <a name="value-cannot-be-null-error"></a>"値を null にすることはできません" エラー

オプションのパラメーターを使用したサーバー側のメソッドは、現在サポートされていません。省略可能なパラメーターを省略すると、メソッドは失敗します。 詳細については、「[省略可能なパラメーター](https://github.com/SignalR/SignalR/issues/324)」を参照してください。

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"&lt;のアドレス&gt;" Firefox ではサーバーへの接続を確立できません "というエラーが発生する

WebSocket トランスポートのネゴシエーションが失敗し、代わりに別のトランスポートが使用されている場合、このエラーメッセージは、消火バグで確認できます。 この動作は仕様です。

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>".NET クライアントアプリケーションの検証手順によると、リモート証明書が無効です" というエラーが発生する

サーバーにカスタムクライアント証明書が必要な場合は、要求が行われる前に接続に x509certificate を追加できます。 `Connection.AddClientCertificate`を使用して、証明書を接続に追加します。

### <a name="connection-drops-after-authentication-times-out"></a>認証のタイムアウト後に接続が切断する

この動作は仕様です。 接続がアクティブな間は、認証資格情報を変更できません。資格情報を更新するには、接続を停止して再起動する必要があります。

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>JQuery Mobile を使用すると、OnConnected が2回呼び出されます

jQuery Mobile の `initializePage` 関数は、各ページのスクリプトを強制的に再実行し、2つ目の接続を作成します。 この問題の解決策は次のとおりです。

- JavaScript ファイルの前に jQuery Mobile への参照を含めます。
- `$.mobile.autoInitializePage = false`を設定して、`initializePage` 関数を無効にします。
- 接続を開始する前に、ページの初期化が完了するのを待ちます。

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>Silverlight アプリケーションでは、サーバー送信イベントを使用してメッセージが遅延されます。

Silverlight でサーバー送信イベントを使用すると、メッセージが遅延します。 代わりに、長いポーリングを強制的に使用するには、接続を開始するときに次のようにします。

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>永続的フレームプロトコルを使用する "アクセス許可が拒否されました"

これは、[ここで](https://github.com/SignalR/SignalR/issues/1963)説明されている既知の問題です。 この現象は、最新の JQuery ライブラリを使用して表示される場合があります。この回避策は、アプリケーションを JQuery 1.8.2 にダウングレードすることです。

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>コンパイルとサーバー側のエラー

 次のセクションでは、コンパイラとサーバー側のランタイムエラーに対して考えられる解決策について説明します。 

### <a name="reference-to-hub-instance-is-null"></a>ハブインスタンスへの参照が null です

ハブインスタンスは接続ごとに作成されるため、自分でコード内にハブのインスタンスを作成することはできません。 ハブ自体の外部からハブのメソッドを呼び出す方法については、ハブコンテキストへの参照を取得する方法について、「[クライアントメソッドを呼び出し、ハブクラスの外部からグループを管理する方法](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)」を参照してください。

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext. Current. Session が null です

この動作は仕様です。 セッション状態を有効にすると双方向メッセージングが中断するため、SignalR は ASP.NET セッション状態をサポートしていません。

### <a name="no-suitable-method-to-override"></a>オーバーライドする適切なメソッドがありません

以前のドキュメントまたはブログのコードを使用している場合は、このエラーが表示されることがあります。 変更または非推奨とされたメソッド (`OnConnectedAsync`など) の名前を参照していないことを確認します。

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions. WebSocketServerUrl は null です

この動作は仕様です。 このメンバーは非推奨とされます。使用しないでください。

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"' Signalr ' という名前のルートは既にルートコレクションに含まれています" エラー

このエラーは、アプリケーションによって `MapHubs` が2回呼び出された場合に表示されます。 アプリケーションの例としては、グローバルアプリケーションファイル内で `MapHubs` 直接呼び出されるものがあります。他のユーザーは、ラッパークラスで呼び出しを行います。 アプリケーションで両方が実行されていないことを確認します。

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio の問題

このセクションでは、Visual Studio で発生した問題について説明します。

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>スクリプトドキュメントノードがソリューションエクスプローラーに表示されない

このチュートリアルの一部では、デバッグ中にソリューションエクスプローラーの [スクリプトドキュメント] ノードに移動します。 このノードは JavaScript デバッガーによって生成され、Internet Explorer でブラウザークライアントをデバッグしているときにのみ表示されます。Chrome または Firefox が使用されている場合、ノードは表示されません。 また、Silverlight デバッガーなど、別のクライアントデバッガーが実行されている場合も、JavaScript デバッガーは実行されません。

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR が Visual Studio 2008 以前で動作しない

この動作は仕様です。 SignalR には .NET Framework 4 以降が必要です。そのためには、Visual Studio 2010 以降で SignalR アプリケーションを開発する必要があります。

<a id="iis"></a>

## <a name="iis-issues"></a>IIS の問題

ここでは、インターネットインフォメーションサービスに関する問題について説明します。

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs 呼び出し後に Web サイトがクラッシュする

この問題は、最新バージョンの SignalR で修正されています。 NuGet を使用してインストールを更新し、SignalR の最新リリースバージョンを使用していることを確認します。

<a id="azure"></a>

## <a name="azure-issues"></a>Azure の問題

ここでは、Microsoft Azure に関する問題について説明します。

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>トピック名を変更した後、Azure バックプレーンでメッセージが受信されない

Azure バックプレーンで使用されるトピックは、ユーザーが構成できるようにするためのものではありません。
