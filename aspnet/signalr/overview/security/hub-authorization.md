---
uid: signalr/overview/security/hub-authorization
title: SignalR Hub の認証と承認 |Microsoft Docs
author: bradygaster
description: このトピックでは、ハブメソッドにアクセスできるユーザーまたはロールを制限する方法について説明します。 このトピックで使用されているソフトウェアのバージョン Visual Studio 2013 .NET 4.5 SignalR ve...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467512"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a>SignalR ハブの認証と承認

[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、ハブメソッドにアクセスできるユーザーまたはロールを制限する方法について説明します。
>
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

## <a name="overview"></a>概要

このトピックには、次のセクションが含まれます。

- [属性の承認](#authorizeattribute)
- [すべてのハブに認証を要求する](#requireauth)
- [カスタマイズされた承認](#custom)
- [クライアントに認証情報を渡す](#passauth)
- [.NET クライアントの認証オプション](#authoptions)

    - [フォーム認証を使用した Cookie](#cookie)
    - [[Windows 認証]](#windows)
    - [接続ヘッダー](#header)
    - [[MSSQLSERVER のプロトコルのプロパティ]](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>属性の承認

SignalR は、hub またはメソッドへのアクセス権を持つユーザーまたはロールを指定するための[承認](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性を提供します。 この属性は `Microsoft.AspNet.SignalR` 名前空間にあります。 `Authorize` 属性はハブのハブまたは特定のメソッドのいずれかに適用します。 `Authorize` 属性をハブクラスに適用すると、指定された承認要件がハブのすべてのメソッドに適用されます。 このトピックでは、適用できるさまざまな種類の承認要件の例を示します。 `Authorize` 属性を指定しない場合、接続されたクライアントはハブ上の任意のパブリックメソッドにアクセスできます。

Web アプリケーションで "Admin" という名前のロールを定義している場合は、次のコードを使用して、そのロールのユーザーのみがハブにアクセスできるように指定できます。

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

または、次に示すように、すべてのユーザーが使用できる1つのメソッドと、認証されたユーザーのみが使用できる2番目のメソッドをハブに含めるように指定できます。

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

次の例では、さまざまな承認シナリオに対処します。

- `[Authorize]`-認証されたユーザーのみ
- `[Authorize(Roles = "Admin,Manager")]`-指定したロール内の認証されたユーザーのみ
- `[Authorize(Users = "user1,user2")]` –指定されたユーザー名を持つ認証済みユーザーのみ
- `[Authorize(RequireOutgoing=false)]`: 認証されたユーザーのみがハブを呼び出すことができますが、サーバーからクライアントへの呼び出しは、特定のユーザーのみがメッセージを送信できるが、他のユーザーがメッセージを受信できる場合など、承認によって制限されません。 RequireOutgoing プロパティは、ハブ内の個々のメソッドではなく、ハブ全体にのみ適用できます。 RequireOutgoing が false に設定されていない場合、承認要件を満たすユーザーのみがサーバーから呼び出されます。

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>すべてのハブに認証を要求する

アプリケーションの起動時に[requireauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)メソッドを呼び出すことにより、アプリケーション内のすべてのハブおよびハブメソッドに対して認証を要求できます。 複数のハブがあり、そのすべてに対して認証要件を強制する場合は、この方法を使用できます。 この方法では、ロール、ユーザー、または送信の承認に関する要件を指定することはできません。 ハブメソッドへのアクセスが認証されたユーザーに制限されることのみを指定できます。 ただし、承認属性をハブまたはメソッドに適用して、追加の要件を指定することもできます。 属性で指定する要件は、認証の基本要件に追加されます。

次の例は、すべてのハブメソッドを認証されたユーザーに制限するスタートアップファイルを示しています。

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

SignalR 要求が処理された後に `RequireAuthentication()` メソッドを呼び出すと、SignalR は例外 `InvalidOperationException` をスローします。 SignalR は、パイプラインが呼び出された後にモジュールを HubPipeline に追加することはできないため、この例外をスローします。 前の例では、最初の要求を処理する前に1回実行される `Configuration` メソッドで `RequireAuthentication` メソッドを呼び出しています。

<a id="custom"></a>

## <a name="customized-authorization"></a>カスタマイズされた承認

承認を決定する方法をカスタマイズする必要がある場合は、`AuthorizeAttribute` から派生したクラスを作成し、 [userauthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)メソッドをオーバーライドできます。 SignalR は、要求ごとにこのメソッドを呼び出して、要求を完了する権限がユーザーに与えられているかどうかを確認します。 オーバーライドされたメソッドには、承認シナリオに必要なロジックを指定します。 次の例は、クレームベースの id を通じて承認を強制する方法を示しています。

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>クライアントに認証情報を渡す

場合によっては、クライアントで実行されるコードで認証情報を使用する必要があります。 クライアントでメソッドを呼び出すときに、必要な情報を渡します。 たとえば、次に示すように、チャットアプリケーションのメソッドは、メッセージを投稿する人のユーザー名をパラメーターとして渡すことができます。

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

または、次に示すように、認証情報を表すオブジェクトを作成し、そのオブジェクトをパラメーターとして渡すことができます。

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

悪意のあるユーザーがそのクライアントからの要求を模倣するために使用する可能性があるため、1つのクライアントの接続 id を他のクライアントに渡すことはできません。

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET クライアントの認証オプション

認証されたユーザーに限定されたハブと対話するコンソールアプリなどの .NET クライアントがある場合は、認証資格情報をクッキー、接続ヘッダー、または証明書に渡すことができます。 このセクションの例では、これらの異なる方法を使用してユーザーを認証する方法を示します。 これらは、完全に機能している SignalR アプリではありません。 SignalR を使用した .NET クライアントの詳細については、「 [HUB API Guide-.Net Client](../guide-to-the-api/hubs-api-guide-net-client.md)」を参照してください。

<a id="cookie"></a>

### <a name="cookie"></a>Cookie

ASP.NET Forms 認証を使用するハブと .NET クライアントが通信する場合、接続で認証 cookie を手動で設定する必要があります。 [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)オブジェクトの `CookieContainer` プロパティに cookie を追加します。 次の例は、web ページから認証クッキーを取得し、その cookie を接続に追加するコンソールアプリを示しています。

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

コンソールアプリによって資格情報が<strong>www.contoso.com/RemoteLogin</strong>にポストされ、次の分離コードファイルを含む空のページを参照できます。

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows 認証

Windows 認証を使用する場合は、 [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)プロパティを使用して、現在のユーザーの資格情報を渡すことができます。 接続の資格情報を DefaultCredentials の値に設定します。

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>接続ヘッダー

アプリケーションが cookie を使用していない場合は、接続ヘッダーにユーザー情報を渡すことができます。 たとえば、接続ヘッダーにトークンを渡すことができます。

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

次に、ハブでユーザーのトークンを確認します。

<a id="certificate"></a>

### <a name="certificate"></a>Certificate

ユーザーを確認するために、クライアント証明書を渡すことができます。 接続の作成時に証明書を追加します。 次の例では、クライアント証明書を接続に追加する方法のみを示します。完全なコンソールアプリは表示されません。 [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)クラスを使用して、証明書を作成するいくつかの異なる方法を提供します。

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
