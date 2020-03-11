---
uid: signalr/overview/security/introduction-to-security
title: SignalR Security | の概要Microsoft Docs
author: bradygaster
description: SignalR アプリケーションの開発時に考慮する必要があるセキュリティの問題について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450076"
---
# <a name="introduction-to-signalr-security"></a>SignalR セキュリティ入門

[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、SignalR アプリケーションの開発時に考慮する必要があるセキュリティの問題について説明します。
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

このドキュメントは、次のトピックに分かれています。

- [SignalR のセキュリティの概念](#concepts)

    - [認証と権限承認](#authentication)
    - [接続トークン](#connectiontoken)
    - [再接続時にグループを再参加](#rejoingroup)
- [SignalR がクロスサイトリクエストの偽造を防止する方法](#csrf)
- [SignalR のセキュリティに関する推奨事項](#recommendations)

    - [Secure Socket Layer (SSL) プロトコル](#ssl)
    - [セキュリティメカニズムとしてグループを使用しない](#groupsecurity)
    - [クライアントからの入力を安全に処理する](#input)
    - [アクティブな接続を使用したユーザーステータスの変更の調整](#reconcile)
    - [自動的に生成された JavaScript プロキシファイル](#autogen)
    - [例外](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR のセキュリティの概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>認証と権限承認

SignalR には、ユーザーを認証するための機能は用意されていません。 代わりに、SignalR 機能をアプリケーションの既存の認証構造に統合します。 アプリケーションで通常どおりユーザーを認証し、SignalR コードで認証の結果を操作します。 たとえば、ASP.NET フォーム認証を使用してユーザーを認証した後、ハブで、メソッドを呼び出すことが許可されているユーザーまたはロールを強制することができます。 ハブでは、ユーザー名やユーザーがロールに属しているかどうかなどの認証情報をクライアントに渡すこともできます。

SignalR は、どのユーザーがハブまたはメソッドにアクセスできるかを指定するための[承認](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性を提供します。 承認属性はハブのハブまたは特定のメソッドのいずれかに適用します。 承認属性を使用しない場合、ハブに接続されているクライアントは、ハブのすべてのパブリックメソッドを使用できます。 ハブの詳細については、「 [SignalR hub の認証と承認](hub-authorization.md)」を参照してください。

`Authorize` 属性はハブに適用しますが、永続的な接続は適用しません。 `PersistentConnection` を使用するときに承認規則を適用するには、`AuthorizeRequest` メソッドをオーバーライドする必要があります。 永続的な接続の詳細については、「 [Authentication And Authorization For SignalR Persistent connections](persistent-connection-authorization.md)」を参照してください。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>接続トークン

SignalR は、送信者の id を検証することによって、悪意のあるコマンドを実行するリスクを軽減します。 要求ごとに、クライアントとサーバーは、認証されたユーザーの接続 id とユーザー名を含む接続トークンを渡します。 接続 id は、接続されている各クライアントを一意に識別します。 サーバーは、新しい接続が作成されるときに接続 id をランダムに生成し、接続の間、その id を保持します。 Web アプリケーションの認証メカニズムによって、ユーザー名が提供されます。 SignalR は、暗号化とデジタル署名を使用して接続トークンを保護します。

![](introduction-to-security/_static/image2.png)

サーバーは、要求ごとにトークンの内容を検証して、要求が指定されたユーザーから送信されていることを確認します。 ユーザー名は接続 id に対応している必要があります。SignalR は、接続 id とユーザー名の両方を検証することで、悪意のあるユーザーが別のユーザーを簡単に偽装できないようにします。 サーバーが接続トークンを検証できない場合、要求は失敗します。

![](introduction-to-security/_static/image4.png)

接続 id は検証プロセスの一部であるため、1人のユーザーの接続 id を他のユーザーに公開したり、cookie などのクライアントに値を格納したりしないでください。

#### <a name="connection-tokens-vs-other-token-types"></a>接続トークンとその他のトークンの種類

接続トークンは、セッショントークンまたは認証トークンであるように見えるため、セキュリティツールによってフラグが設定されることがあります。これにより、公開された場合にリスクが生じます。

SignalR の接続トークンは認証トークンではありません。 この要求を行うユーザーが、接続を作成したユーザーと同じであることを確認するために使用されます。 ASP.NET SignalR ではサーバー間で接続を移動できるため、接続トークンが必要です。 このトークンは、接続を特定のユーザーに関連付けますが、要求を行っているユーザーの id をアサートしません。 SignalR 要求が適切に認証されるためには、cookie またはベアラートークンなど、ユーザーの id をアサートするその他のトークンが必要です。 ただし、接続トークン自体は、そのユーザーによって要求が行われたという要求を行いません。トークンに含まれる接続 ID は、そのユーザーに関連付けられているだけです。

接続トークンは独自の認証要求を提供しないため、"セッション" または "認証" トークンとは見なされません。 特定のユーザーの接続トークンを取得し、別のユーザー (または認証されていない要求) として認証された要求でそれを再生すると、要求のユーザー id とトークンに格納されている id が一致しないため、失敗します。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>再接続時にグループを再参加

既定では、接続がタイムアウトになる前に接続が切断され、再確立された場合など、一時的な中断から再接続するときに、SignalR アプリケーションによって自動的に適切なグループにユーザーが再割り当てされます。再接続すると、クライアントは接続 id と割り当てられたグループを含むグループトークンを渡します。 グループトークンはデジタル署名され、暗号化されています。 再接続後もクライアントは同じ接続 id を保持します。そのため、再接続されたクライアントから渡される接続 id は、クライアントで使用される以前の接続 id と一致する必要があります。 この検証により、悪意のあるユーザーが、再接続時に承認されていないグループへの参加要求を渡すことを防止できます

ただし、グループトークンの有効期限が切れないことに注意することが重要です。 ユーザーが過去にグループに属していても、そのグループから禁止されていた場合、そのユーザーは禁止されたグループを含むグループトークンを模倣できる可能性があります。 どのユーザーがどのグループに属しているかを安全に管理する必要がある場合は、データベースなどのサーバーにそのデータを格納する必要があります。 次に、ユーザーがグループに属しているかどうかをサーバーで確認するロジックをアプリケーションに追加します。 グループメンバーシップを確認する例については、「[グループの操作](../guide-to-the-api/working-with-groups.md)」を参照してください。

自動再参加グループは、一時的な中断後に接続が再接続された場合にのみ適用されます。 アプリケーションから移動してユーザーの接続を切断した場合、またはアプリケーションを再起動した場合、アプリケーションは、適切なグループにそのユーザーを追加する方法を処理する必要があります。 詳細については、「[グループの操作](../guide-to-the-api/working-with-groups.md)」を参照してください。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR がクロスサイトリクエストの偽造を防止する方法

クロスサイト要求偽造 (CSRF) は、ユーザーが現在ログインしている脆弱なサイトに、悪意のあるサイトから要求を送信する攻撃です。 SignalR は、悪意のあるサイトが SignalR アプリケーションに対して有効な要求を作成しないようにすることで CSRF を防ぐことができます。

### <a name="description-of-csrf-attack"></a>CSRF 攻撃の説明

CSRF 攻撃の例を次に示します。

1. [www.example.com](www.example.com) にユーザーが、フォーム認証の使用します。
2. サーバーは、ユーザーを認証します。 サーバーからの応答には、認証クッキーが含まれています。
3. ログオフしないと、ユーザーは悪意のある web サイトにアクセスします。 この悪意のあるサイトには、次の HTML フォームが含まれています。

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   フォームアクションは、悪意のあるサイトではなく、脆弱なサイトに投稿されることに注意してください。 これは、CSRF の "cross-site" の一部です。
4. ユーザーが [送信] ボタンをクリックします。 ブラウザーには、要求と共に認証クッキーが含まれます。
5. 要求は、ユーザーの認証コンテキストを使用して example.com サーバー上で実行され、認証されたユーザーが実行できるすべての操作を実行できます。

この例では、ユーザーがフォームボタンをクリックする必要がありますが、悪意のあるページは、AJAX 要求を SignalR アプリケーションに送信するスクリプトを実行するのと同じくらい簡単です。 また、悪意のあるサイトが "https://" 要求を送信できるため、SSL を使用しても CSRF 攻撃を防ぐことはできません。

通常、ブラウザーでは、関連するすべての cookie が送信先の web サイトに送信されるため、認証に cookie を使用する web サイトに対しては CSRF 攻撃を行うことができます。 ただし、CSRF 攻撃は cookie を利用することに限定されません。 例えば、ベーシック認証やダイジェスト認証も脆弱です。 ユーザーが基本認証またはダイジェスト認証を使用してログインすると、セッションが終了するまで、ブラウザーは資格情報を自動的に送信します。

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR によって実行される CSRF 軽減策

SignalR は、悪意のあるサイトがアプリケーションに対して有効な要求を作成できないようにするために、次の手順を実行します。 既定では、SignalR はこれらの手順を実行します。コード内でアクションを実行する必要はありません。

- **クロスドメイン要求を無効にする**SignalR は、ユーザーが外部ドメインから SignalR エンドポイントを呼び出さないようにするために、クロスドメイン要求を無効にします。 SignalR は、外部ドメインからの要求が無効であると見なし、要求をブロックします。 この既定の動作をそのまま使用することをお勧めします。そうしないと、悪意のあるサイトによってユーザーがサイトにコマンドを送信する可能性があります。 ドメイン間要求を使用する必要がある場合は、「[ドメイン間接続を確立する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)」を参照してください。
- **Cookie ではなくクエリ文字列に接続トークンを渡す**SignalR は、cookie としてではなく、クエリ文字列値として接続トークンを渡します。 悪意のあるコードが検出された場合、ブラウザーが誤って接続トークンを転送できるため、接続トークンをクッキーに格納することは安全ではありません。 また、接続トークンをクエリ文字列に渡すことで、接続トークンが現在の接続を超えて保持されるのを防ぐことができます。 そのため、悪意のあるユーザーが別のユーザーの認証資格情報で要求を行うことはできません。
- **接続トークンの確認**「[接続トークン](#connectiontoken)」セクションで説明したように、サーバーは、認証された各ユーザーに関連付けられている接続 id を認識します。 サーバーは、ユーザー名と一致しない接続 id の要求を処理しません。 悪意のあるユーザーが、ユーザー名と現在ランダムに生成されている接続 id を知る必要があるため、悪意のあるユーザーが有効な要求を推測できる可能性はほとんどありません。接続が終了すると、その接続 id はすぐに無効になります。 匿名ユーザーは、機密情報にアクセスできないようにする必要があります。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR のセキュリティに関する推奨事項

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Secure Socket Layer (SSL) プロトコル

SSL プロトコルは、暗号化を使用して、クライアントとサーバー間のデータの転送をセキュリティで保護します。 SignalR アプリケーションがクライアントとサーバーの間で機密情報を送信する場合は、トランスポートに SSL を使用します。 SSL の設定の詳細については、「 [IIS 7 で ssl を設定する方法](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)」を参照してください。

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>セキュリティメカニズムとしてグループを使用しない

グループは、関連するユーザーを収集するための便利な方法ですが、機密情報へのアクセスを制限するための安全なメカニズムではありません。 これは特に、再接続中にユーザーが自動的にグループを再参加させる場合に当てはまります。 代わりに、特権を持つユーザーをロールに追加し、ハブメソッドへのアクセスをそのロールのメンバーのみに制限することを検討してください。 ロールに基づいてアクセスを制限する例については、「 [SignalR hub の認証と承認](hub-authorization.md)」を参照してください。 再接続時にグループへのユーザーアクセスを確認する例については、「[グループの操作](../guide-to-the-api/working-with-groups.md)」を参照してください。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>クライアントからの入力を安全に処理する

悪意のあるユーザーが他のユーザーにスクリプトを送信しないようにするには、他のクライアントへのブロードキャストを目的としたクライアントからのすべての入力をエンコードする必要があります。 SignalR アプリケーションにはさまざまな種類のクライアントが存在する可能性があるため、サーバーではなく受信側のクライアントでメッセージをエンコードする必要があります。 そのため、HTML エンコードは web クライアントに対しては機能しますが、他の種類のクライアントには使用できません。 たとえば、チャットメッセージを表示する web クライアントメソッドは、`html()` 関数を呼び出すことによって、ユーザー名とメッセージを安全に処理します。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>アクティブな接続を使用したユーザーステータスの変更の調整

アクティブな接続が存在している間にユーザーの認証状態が変化すると、"active SignalR 接続中にユーザー id を変更することはできません。" というエラーがユーザーに表示されます。 その場合は、アプリケーションがサーバーに再接続して、接続 id とユーザー名が連携していることを確認する必要があります。 たとえば、アプリケーションで、アクティブな接続が存在するときにユーザーがログアウトできるようにした場合、接続のユーザー名は、次の要求で渡された名前と一致しなくなります。 ユーザーがログアウトする前に接続を停止してから、再起動する必要があります。

ただし、ほとんどのアプリケーションでは、接続を手動で停止して開始する必要がないことに注意してください。 アプリケーションが、ログオフ後にユーザーを別のページにリダイレクトした場合 (Web フォームアプリケーションや MVC アプリケーションの既定の動作など)、またはログアウト後に現在のページを更新すると、アクティブな接続は自動的に切断され、追加のアクションが必要です。

次の例では、ユーザーの状態が変化したときに接続を停止および開始する方法を示します。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

または、ユーザーの認証状態が、サイトでフォーム認証でスライディング有効期限が使用されていて、認証クッキーを有効な状態に保つためのアクティビティがない場合にも変更される可能性があります。 この場合、ユーザーはログアウトされ、ユーザー名は接続トークンのユーザー名と一致しなくなります。 この問題を解決するには、認証クッキーを有効な状態に保つために、web サーバー上のリソースを定期的に要求するスクリプトを追加します。 次の例は、30分ごとにリソースを要求する方法を示しています。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自動的に生成された JavaScript プロキシファイル

各ユーザーの JavaScript プロキシファイルにすべてのハブとメソッドを含めない場合は、ファイルの自動生成を無効にすることができます。 複数のハブとメソッドがあり、すべてのユーザーにすべてのメソッドを認識させたくない場合は、このオプションを選択できます。 自動生成を無効にするには、 **EnableJavaScriptProxies**を**false**に設定します。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript プロキシファイルの詳細については、[生成されたプロキシとその機能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)に関する情報を参照してください。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外

オブジェクトがクライアントに機密情報を公開する可能性があるため、例外オブジェクトをクライアントに渡すことは避ける必要があります。 代わりに、関連するエラーメッセージを表示するメソッドをクライアントで呼び出します。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
