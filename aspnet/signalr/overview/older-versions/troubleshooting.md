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
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="a5ccb-103">SignalR トラブルシューティング (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="a5ccb-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="a5ccb-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="a5ccb-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a5ccb-105">このドキュメントでは、SignalR に関する一般的なトラブルシューティングの問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="a5ccb-106">このドキュメントには、次のセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="a5ccb-107">クライアントとサーバーの間でメソッドをサイレントモードで呼び出すことができない</span><span class="sxs-lookup"><span data-stu-id="a5ccb-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="a5ccb-108">その他の接続の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="a5ccb-109">コンパイルとサーバー側のエラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="a5ccb-110">Visual Studio の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="a5ccb-111">インターネットインフォメーションサービスの問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="a5ccb-112">Azure の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="a5ccb-113">クライアントとサーバーの間でメソッドをサイレントモードで呼び出すことができない</span><span class="sxs-lookup"><span data-stu-id="a5ccb-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="a5ccb-114">ここでは、クライアントとサーバーの間でメソッド呼び出しが失敗し、意味のあるエラーメッセージが表示されない場合に発生する可能性のある原因について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="a5ccb-115">SignalR アプリケーションでは、クライアントが実装するメソッドに関する情報はサーバーにありません。サーバーがクライアントメソッドを呼び出すと、メソッド名とパラメーターデータがクライアントに送信され、メソッドは、サーバーが指定した形式で存在する場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="a5ccb-116">一致するメソッドがクライアントに見つからない場合は、何も起こりません。サーバーでエラーメッセージは生成されません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="a5ccb-117">呼び出されていないクライアントメソッドをさらに詳しく調査するには、ハブで start メソッドを呼び出してから、サーバーからの呼び出しを確認する前に、ログ記録を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="a5ccb-118">JavaScript アプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (javascript クライアントバージョン)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="a5ccb-119">.NET クライアントアプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (.Net クライアントのバージョン)](../guide-to-the-api/hubs-api-guide-net-client.md#logging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="a5ccb-120">間違った方法、不適切なメソッドシグネチャ、または間違ったハブ名</span><span class="sxs-lookup"><span data-stu-id="a5ccb-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="a5ccb-121">呼び出されたメソッドの名前またはシグネチャがクライアントの適切なメソッドと完全に一致しない場合、呼び出しは失敗します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="a5ccb-122">サーバーによって呼び出されたメソッド名がクライアント上のメソッドの名前と一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="a5ccb-123">また、SignalR は、JavaScript に適した camel 形式のメソッドを使用してハブプロキシを作成します。そのため、サーバー上で `SendMessage` というメソッドをクライアントプロキシで `sendMessage` と呼びます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="a5ccb-124">サーバー側コードで `HubName` 属性を使用する場合は、使用されている名前が、クライアントでハブの作成に使用された名前と一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="a5ccb-125">`HubName` 属性を使用しない場合は、JavaScript クライアントのハブの名前が camel 形式であることを確認します。たとえば、ChatHub の代わりに chatHub のようにします。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="a5ccb-126">クライアントでメソッド名が重複しています</span><span class="sxs-lookup"><span data-stu-id="a5ccb-126">Duplicate method name on client</span></span>

<span data-ttu-id="a5ccb-127">大文字と小文字のみが異なる、クライアントに重複するメソッドがないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="a5ccb-128">クライアントアプリケーションに `sendMessage`というメソッドがある場合は、`SendMessage` と呼ばれるメソッドも存在しないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="a5ccb-129">クライアントに JSON パーサーがありません</span><span class="sxs-lookup"><span data-stu-id="a5ccb-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="a5ccb-130">SignalR を使用するには、サーバーとクライアント間の呼び出しをシリアル化するために JSON パーサーが存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="a5ccb-131">クライアントに組み込みの JSON パーサー (Internet Explorer 7 など) がない場合は、アプリケーションに1つを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="a5ccb-132">JSON パーサーは[こちら](http://nuget.org/packages/json2)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="a5ccb-133">Hub と PersistentConnection 構文の混在</span><span class="sxs-lookup"><span data-stu-id="a5ccb-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="a5ccb-134">SignalR は、2つの通信モデル (ハブと PersistentConnections) を使用します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="a5ccb-135">これら2つの通信モデルを呼び出すための構文は、クライアントコードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="a5ccb-136">サーバーコードにハブを追加した場合は、すべてのクライアントコードで適切なハブ構文が使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="a5ccb-137">**JavaScript クライアントで PersistentConnection を作成する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="a5ccb-138">**Javascript クライアントでハブプロキシを作成する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="a5ccb-139">**C#ルートを PersistentConnection にマップするサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="a5ccb-140">**C#ハブまたは複数のアプリケーションがある場合は複数のハブにルートをマップするサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="a5ccb-141">サブスクリプションが追加される前に接続が開始されました</span><span class="sxs-lookup"><span data-stu-id="a5ccb-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="a5ccb-142">サーバーから呼び出すことができるメソッドがプロキシに追加される前にハブの接続が開始されると、メッセージは受信されません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="a5ccb-143">次の JavaScript コードはハブを適切に起動しません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="a5ccb-144">**ハブメッセージの受信を許可しない JavaScript クライアントコードが正しくありません**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="a5ccb-145">代わりに、Start を呼び出す前にメソッドサブスクリプションを追加します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="a5ccb-146">**ハブにサブスクリプションを正しく追加する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="a5ccb-147">ハブプロキシにメソッド名がありません</span><span class="sxs-lookup"><span data-stu-id="a5ccb-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="a5ccb-148">サーバーで定義されているメソッドがクライアントでサブスクライブされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="a5ccb-149">サーバーによってメソッドが定義されている場合でも、クライアントプロキシに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="a5ccb-150">メソッドは、次の方法でクライアントプロキシに追加できます (このメソッドは、ハブではなく、ハブの `client` メンバーに追加されることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="a5ccb-151">**ハブプロキシにメソッドを追加する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="a5ccb-152">ハブまたはハブのメソッドがパブリックとして宣言されていません</span><span class="sxs-lookup"><span data-stu-id="a5ccb-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="a5ccb-153">クライアントで表示されるようにするには、ハブの実装とメソッドを `public`として宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="a5ccb-154">別のアプリケーションからのハブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="a5ccb-154">Accessing hub from a different application</span></span>

<span data-ttu-id="a5ccb-155">SignalR Hub にアクセスできるのは、SignalR クライアントを実装するアプリケーションのみです。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="a5ccb-156">SignalR は、他の通信ライブラリ (SOAP や WCF web サービスなど) と相互運用することはできません。ターゲットプラットフォームに使用できる SignalR クライアントがない場合は、サーバーのエンドポイントに直接アクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="a5ccb-157">手動によるデータのシリアル化</span><span class="sxs-lookup"><span data-stu-id="a5ccb-157">Manually serializing data</span></span>

<span data-ttu-id="a5ccb-158">SignalR は自動的に JSON を使用してメソッドのパラメーターをシリアル化します。自分で行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="a5ccb-159">OnDisconnected 関数のクライアントでリモートハブのメソッドが実行されませんでした</span><span class="sxs-lookup"><span data-stu-id="a5ccb-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="a5ccb-160">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-160">This behavior is by design.</span></span> <span data-ttu-id="a5ccb-161">`OnDisconnected` が呼び出されると、ハブは既に `Disconnected` 状態に入っています。これにより、これ以上ハブメソッドを呼び出すことはできません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="a5ccb-162">**C#OnDisconnected イベントでコードを正しく実行するサーバーコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="a5ccb-163">接続数の上限に達しました</span><span class="sxs-lookup"><span data-stu-id="a5ccb-163">Connection limit reached</span></span>

<span data-ttu-id="a5ccb-164">Windows 7 などのクライアントオペレーティングシステムで IIS の完全バージョンを使用する場合は、10接続の制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="a5ccb-165">クライアント OS を使用する場合は、この制限を回避するために、代わりに IIS Express を使用します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="a5ccb-166">ドメイン間接続が適切に設定されていません</span><span class="sxs-lookup"><span data-stu-id="a5ccb-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="a5ccb-167">ドメイン間接続 (SignalR URL がホスティングページと同じドメインにない接続) が正しく設定されていない場合、接続はエラーメッセージなしで失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="a5ccb-168">ドメイン間通信を有効にする方法については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="a5ccb-169">NTLM を使用した接続 (Active Directory) が .NET クライアントで動作しない</span><span class="sxs-lookup"><span data-stu-id="a5ccb-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="a5ccb-170">接続が正しく構成されていない場合、ドメインセキュリティを使用する .NET クライアントアプリケーションの接続が失敗することがあります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="a5ccb-171">ドメイン環境で SignalR を使用するには、必要な接続プロパティを次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="a5ccb-172">**C#接続資格情報を実装するクライアントコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="a5ccb-173">その他の接続の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-173">Other connection issues</span></span>

<span data-ttu-id="a5ccb-174">このセクションでは、接続中に発生する特定の現象またはエラーメッセージの原因と解決方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="a5ccb-175">"データを送信する前に開始する必要があります" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="a5ccb-176">このエラーは、接続が開始される前にコードが SignalR オブジェクトを参照する場合によく見られます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="a5ccb-177">サーバーで定義されているメソッドを呼び出すのと同様に、ハンドラーの wireup とを、接続の完了後に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="a5ccb-178">`Start` の呼び出しが非同期であるため、呼び出しの後のコードを実行してから完了することができます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="a5ccb-179">接続が完全に開始された後にハンドラーを追加する最善の方法は、start メソッドにパラメーターとして渡されるコールバック関数にそれらを配置することです。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="a5ccb-180">**SignalR オブジェクトを参照するイベントハンドラーを正しく追加する JavaScript クライアントコード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="a5ccb-181">このエラーは、SignalR オブジェクトがまだ参照されている間に接続が停止した場合にも表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="a5ccb-182">"301 が永続的に移動されました" または "302 を一時的に移動" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="a5ccb-183">このエラーは、プロジェクトに SignalR という名前のフォルダーが含まれている場合に発生する可能性があります。これにより、自動的に作成されたプロキシが妨げられます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="a5ccb-184">このエラーを回避するには、アプリケーションで `SignalR` という名前のフォルダーを使用しないようにするか、自動プロキシ生成をオフにします。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="a5ccb-185">[生成されたプロキシとその](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)詳細については、「」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="a5ccb-186">.NET または Silverlight クライアントで "403 の許可されていません" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="a5ccb-187">このエラーは、ドメイン間通信が正しく有効になっていないクロスドメイン環境で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="a5ccb-188">ドメイン間通信を有効にする方法については、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="a5ccb-189">Silverlight クライアントでドメイン間接続を確立する方法については、「 [silverlight クライアントからのクロスドメイン](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)接続」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="a5ccb-190">"404 が見つかりません" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-190">"404 Not Found" error</span></span>

<span data-ttu-id="a5ccb-191">この問題にはいくつかの原因があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-191">There are several causes for this issue.</span></span> <span data-ttu-id="a5ccb-192">次のすべてを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-192">Verify all of the following:</span></span>

- <span data-ttu-id="a5ccb-193">**ハブプロキシアドレスの参照が正しくフォーマットされていません:** このエラーは、生成されたハブプロキシアドレスへの参照が正しく書式設定されていない場合によく発生します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="a5ccb-194">ハブアドレスへの参照が適切に作成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="a5ccb-195">詳細について[は、「動的に生成されたプロキシを参照する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="a5ccb-196">**ハブルートを追加する前に、アプリケーションにルートを追加します。** アプリケーションで他のルートを使用する場合は、追加された最初のルートが `MapHubs`の呼び出しであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="a5ccb-197">"500 内部サーバーエラー"</span><span class="sxs-lookup"><span data-stu-id="a5ccb-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="a5ccb-198">これは非常に一般的なエラーであり、さまざまな原因が考えられます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="a5ccb-199">エラーの詳細は、サーバーのイベントログに表示されるか、またはサーバーのデバッグによって検出されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="a5ccb-200">詳細なエラー情報を取得するには、サーバーで詳細なエラーを有効にします。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="a5ccb-201">詳細については、「 [Hub クラスでエラーを処理する方法](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="a5ccb-202">"TypeError: &lt;hubType&gt; が定義されていません" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="a5ccb-203">このエラーは、`MapHubs` の呼び出しが正しく行われない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="a5ccb-204">詳細について[は、「How to register The SignalR route」および「Configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="a5ccb-205">JsonSerializationException がユーザーコードによって処理されませんでした</span><span class="sxs-lookup"><span data-stu-id="a5ccb-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="a5ccb-206">メソッドに送信するパラメーターに、シリアル化できない型 (ファイルハンドルやデータベース接続など) が含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="a5ccb-207">クライアントに送信したくないサーバー側オブジェクト (セキュリティのため、またはシリアル化の理由) でメンバーを使用する必要がある場合は、`JSONIgnore` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="a5ccb-208">"プロトコルエラー: 不明なトランスポート" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="a5ccb-209">このエラーは、SignalR が使用するトランスポートをクライアントがサポートしていない場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="a5ccb-210">SignalR で使用できるブラウザーの詳細については[、「トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="a5ccb-211">"JavaScript Hub プロキシの生成が無効になりました。"</span><span class="sxs-lookup"><span data-stu-id="a5ccb-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="a5ccb-212">このエラーは、`signalr/hubs`で動的に生成されたプロキシへの参照も含め、`DisableJavaScriptProxies` が設定されている場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="a5ccb-213">プロキシを手動で作成する方法の詳細については、「[生成されたプロキシとその機能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="a5ccb-214">"接続 ID の形式が正しくありません" または "active SignalR 接続中にユーザー id を変更できません" というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="a5ccb-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="a5ccb-215">このエラーは、認証が使用されていて、接続が停止される前にクライアントがログアウトされている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="a5ccb-216">この問題を解決するには、クライアントをログに記録する前に、SignalR 接続を停止します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="a5ccb-217">"キャッチされていないエラー: SignalR: jQuery が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="a5ccb-218">SignalR ファイルの前に jQuery が参照されていることを確認してください。 "エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="a5ccb-219">SignalR JavaScript クライアントでは、jQuery を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="a5ccb-220">JQuery への参照が正しいこと、使用されているパスが有効であること、および jQuery への参照が SignalR への参照の前にあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="a5ccb-221">"キャッチされていない TypeError: プロパティ '&lt;プロパティ&gt;' undefined ' エラーを読み取ることができません</span><span class="sxs-lookup"><span data-stu-id="a5ccb-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="a5ccb-222">このエラーは、jQuery またはハブプロキシが正しく参照されていない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="a5ccb-223">JQuery とハブプロキシへの参照が正しいこと、使用されているパスが有効であること、および jQuery への参照がハブプロキシへの参照の前にあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="a5ccb-224">ハブプロキシへの既定の参照は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="a5ccb-225">**ハブプロキシを正しく参照する HTML クライアント側コード**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="a5ccb-226">"RuntimeBinderException はユーザーコードによって処理されませんでした" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="a5ccb-227">このエラーは、`Hub.On` の不適切なオーバーロードが使用されている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="a5ccb-228">メソッドに戻り値がある場合は、戻り値の型をジェネリック型パラメーターとして指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="a5ccb-229">**クライアントで定義されたメソッド (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="a5ccb-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="a5ccb-230">接続 ID が一致していないか、ページ読み込み間の接続が壊れています</span><span class="sxs-lookup"><span data-stu-id="a5ccb-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="a5ccb-231">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-231">This behavior is by design.</span></span> <span data-ttu-id="a5ccb-232">ハブオブジェクトはページオブジェクトでホストされるため、ページが更新されるとハブは破棄されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="a5ccb-233">複数ページアプリケーションでは、ページの読み込み間で一貫性を保つために、ユーザーと接続 Id の間の関連付けを維持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="a5ccb-234">接続 Id は、`ConcurrentDictionary` オブジェクトまたはデータベースのいずれかのサーバーに格納できます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="a5ccb-235">"値を null にすることはできません" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-235">"Value cannot be null" error</span></span>

<span data-ttu-id="a5ccb-236">オプションのパラメーターを使用したサーバー側のメソッドは、現在サポートされていません。省略可能なパラメーターを省略すると、メソッドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="a5ccb-237">詳細については、「[省略可能なパラメーター](https://github.com/SignalR/SignalR/issues/324)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="a5ccb-238">"&lt;のアドレス&gt;" Firefox ではサーバーへの接続を確立できません "というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="a5ccb-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="a5ccb-239">WebSocket トランスポートのネゴシエーションが失敗し、代わりに別のトランスポートが使用されている場合、このエラーメッセージは、消火バグで確認できます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="a5ccb-240">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="a5ccb-241">".NET クライアントアプリケーションの検証手順によると、リモート証明書が無効です" というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="a5ccb-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="a5ccb-242">サーバーにカスタムクライアント証明書が必要な場合は、要求が行われる前に接続に x509certificate を追加できます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="a5ccb-243">`Connection.AddClientCertificate`を使用して、証明書を接続に追加します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="a5ccb-244">認証のタイムアウト後に接続が切断する</span><span class="sxs-lookup"><span data-stu-id="a5ccb-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="a5ccb-245">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-245">This behavior is by design.</span></span> <span data-ttu-id="a5ccb-246">接続がアクティブな間は、認証資格情報を変更できません。資格情報を更新するには、接続を停止して再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="a5ccb-247">JQuery Mobile を使用すると、OnConnected が2回呼び出されます</span><span class="sxs-lookup"><span data-stu-id="a5ccb-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="a5ccb-248">jQuery Mobile の `initializePage` 関数は、各ページのスクリプトを強制的に再実行し、2つ目の接続を作成します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="a5ccb-249">この問題の解決策は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="a5ccb-250">JavaScript ファイルの前に jQuery Mobile への参照を含めます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="a5ccb-251">`$.mobile.autoInitializePage = false`を設定して、`initializePage` 関数を無効にします。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="a5ccb-252">接続を開始する前に、ページの初期化が完了するのを待ちます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="a5ccb-253">Silverlight アプリケーションでは、サーバー送信イベントを使用してメッセージが遅延されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="a5ccb-254">Silverlight でサーバー送信イベントを使用すると、メッセージが遅延します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="a5ccb-255">代わりに、長いポーリングを強制的に使用するには、接続を開始するときに次のようにします。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="a5ccb-256">永続的フレームプロトコルを使用する "アクセス許可が拒否されました"</span><span class="sxs-lookup"><span data-stu-id="a5ccb-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="a5ccb-257">これは、[ここで](https://github.com/SignalR/SignalR/issues/1963)説明されている既知の問題です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="a5ccb-258">この現象は、最新の JQuery ライブラリを使用して表示される場合があります。この回避策は、アプリケーションを JQuery 1.8.2 にダウングレードすることです。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="a5ccb-259">コンパイルとサーバー側のエラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="a5ccb-260">次のセクションでは、コンパイラとサーバー側のランタイムエラーに対して考えられる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="a5ccb-261">ハブインスタンスへの参照が null です</span><span class="sxs-lookup"><span data-stu-id="a5ccb-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="a5ccb-262">ハブインスタンスは接続ごとに作成されるため、自分でコード内にハブのインスタンスを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="a5ccb-263">ハブ自体の外部からハブのメソッドを呼び出す方法については、ハブコンテキストへの参照を取得する方法について、「[クライアントメソッドを呼び出し、ハブクラスの外部からグループを管理する方法](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="a5ccb-264">HTTPContext. Current. Session が null です</span><span class="sxs-lookup"><span data-stu-id="a5ccb-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="a5ccb-265">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-265">This behavior is by design.</span></span> <span data-ttu-id="a5ccb-266">セッション状態を有効にすると双方向メッセージングが中断するため、SignalR は ASP.NET セッション状態をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="a5ccb-267">オーバーライドする適切なメソッドがありません</span><span class="sxs-lookup"><span data-stu-id="a5ccb-267">No suitable method to override</span></span>

<span data-ttu-id="a5ccb-268">以前のドキュメントまたはブログのコードを使用している場合は、このエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="a5ccb-269">変更または非推奨とされたメソッド (`OnConnectedAsync`など) の名前を参照していないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="a5ccb-270">HostContextExtensions. WebSocketServerUrl は null です</span><span class="sxs-lookup"><span data-stu-id="a5ccb-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="a5ccb-271">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-271">This behavior is by design.</span></span> <span data-ttu-id="a5ccb-272">このメンバーは非推奨とされます。使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="a5ccb-273">"' Signalr ' という名前のルートは既にルートコレクションに含まれています" エラー</span><span class="sxs-lookup"><span data-stu-id="a5ccb-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="a5ccb-274">このエラーは、アプリケーションによって `MapHubs` が2回呼び出された場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="a5ccb-275">アプリケーションの例としては、グローバルアプリケーションファイル内で `MapHubs` 直接呼び出されるものがあります。他のユーザーは、ラッパークラスで呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="a5ccb-276">アプリケーションで両方が実行されていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="a5ccb-277">Visual Studio の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-277">Visual Studio issues</span></span>

<span data-ttu-id="a5ccb-278">このセクションでは、Visual Studio で発生した問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="a5ccb-279">スクリプトドキュメントノードがソリューションエクスプローラーに表示されない</span><span class="sxs-lookup"><span data-stu-id="a5ccb-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="a5ccb-280">このチュートリアルの一部では、デバッグ中にソリューションエクスプローラーの [スクリプトドキュメント] ノードに移動します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="a5ccb-281">このノードは JavaScript デバッガーによって生成され、Internet Explorer でブラウザークライアントをデバッグしているときにのみ表示されます。Chrome または Firefox が使用されている場合、ノードは表示されません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="a5ccb-282">また、Silverlight デバッガーなど、別のクライアントデバッガーが実行されている場合も、JavaScript デバッガーは実行されません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="a5ccb-283">SignalR が Visual Studio 2008 以前で動作しない</span><span class="sxs-lookup"><span data-stu-id="a5ccb-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="a5ccb-284">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-284">This behavior is by design.</span></span> <span data-ttu-id="a5ccb-285">SignalR には .NET Framework 4 以降が必要です。そのためには、Visual Studio 2010 以降で SignalR アプリケーションを開発する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="a5ccb-286">IIS の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-286">IIS issues</span></span>

<span data-ttu-id="a5ccb-287">ここでは、インターネットインフォメーションサービスに関する問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="a5ccb-288">MapHubs 呼び出し後に Web サイトがクラッシュする</span><span class="sxs-lookup"><span data-stu-id="a5ccb-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="a5ccb-289">この問題は、最新バージョンの SignalR で修正されています。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="a5ccb-290">NuGet を使用してインストールを更新し、SignalR の最新リリースバージョンを使用していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="a5ccb-291">Azure の問題</span><span class="sxs-lookup"><span data-stu-id="a5ccb-291">Azure issues</span></span>

<span data-ttu-id="a5ccb-292">ここでは、Microsoft Azure に関する問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="a5ccb-293">トピック名を変更した後、Azure バックプレーンでメッセージが受信されない</span><span class="sxs-lookup"><span data-stu-id="a5ccb-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="a5ccb-294">Azure バックプレーンで使用されるトピックは、ユーザーが構成できるようにするためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="a5ccb-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
