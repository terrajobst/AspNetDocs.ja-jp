---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-vb
title: ロールベースの承認 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、まず、ロールフレームワークによってユーザーのロールとセキュリティコンテキストがどのように関連付けられるかについて説明します。 次に、ロールベースの URL を適用する方法を調べます...
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 83b4f5a4-4f5a-4380-ba33-f0b5c5ac6a75
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: feb3e5eb992284033853e67bfab3872243cefe39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570558"
---
# <a name="role-based-authorization-vb"></a>ロールベースの承認 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.11.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_vb.pdf)

> このチュートリアルでは、まず、ロールフレームワークによってユーザーのロールとセキュリティコンテキストがどのように関連付けられるかについて説明します。 次に、ロールベースの URL 承認規則を適用する方法を調べます。 ここでは、表示されるデータと、ASP.NET ページによって提供される機能を変更するための、宣言型の方法とプログラムによる方法について説明します。

## <a name="introduction"></a>はじめに

<a id="_msoanchor_1"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)のチュートリアルでは、URL 承認を使用して、ユーザーが特定のページセットにアクセスできる内容を指定する方法を説明しました。 `Web.config`ではほんの少しのマークアップを使用して、認証されたユーザーのみがページにアクセスできるように ASP.NET に指示することができます。 または、ユーザーの Tito および Bob のみが許可されたこと、または、Sam 以外のすべての認証済みユーザーが許可されたことを示すこともできます。

URL 承認に加えて、表示されるデータを制御するための宣言型の手法とプログラムによる手法についても説明しました。 特に、現在のディレクトリの内容を一覧表示するページを作成しました。 だれでもこのページにアクセスできますが、ファイルの内容を表示できるのは認証されたユーザーのみで、ファイルを削除できるのは Tito だけでした。

ユーザーごとに承認規則を適用すると、簿記の悪夢になる可能性があります。 より保守しやすい方法は、ロールベースの承認を使用することです。 ユーザーアカウントの場合と同様に、承認規則を適用するためのツールはロールと同様に機能します。 URL 承認規則では、ユーザーの代わりにロールを指定できます。 認証されたユーザーと匿名ユーザーに対して異なる出力を表示する LoginView コントロールは、ログインしているユーザーのロールに基づいてさまざまなコンテンツを表示するように構成できます。 および Roles API には、ログインしているユーザーのロールを決定するためのメソッドが含まれています。

このチュートリアルでは、まず、ロールフレームワークによってユーザーのロールとセキュリティコンテキストがどのように関連付けられるかについて説明します。 次に、ロールベースの URL 承認規則を適用する方法を調べます。 ここでは、表示されるデータと、ASP.NET ページによって提供される機能を変更するための、宣言型の方法とプログラムによる方法について説明します。 では、始めましょう。

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>ロールがユーザーのセキュリティコンテキストにどのように関連付けられているかを理解する

要求が ASP.NET パイプラインに入るたびに、要求がセキュリティコンテキストに関連付けられます。これには、要求元を識別する情報が含まれます。 フォーム認証を使用する場合は、認証チケットが id トークンとして使用されます。 <a id="_msoanchor_2"> </a> [ *「フォーム認証*](../introduction/an-overview-of-forms-authentication-vb.md)と<a id="_msoanchor_3"> </a>[*フォーム認証構成と高度なトピック*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)の概要」のチュートリアルで説明したように、`FormsAuthenticationModule` は、 [`AuthenticateRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)中に実行される要求元の id を決定します。

有効期限が切れていない認証チケットが見つかった場合、`FormsAuthenticationModule` はそれをデコードして、要求元の id を確認します。 このメソッドは、新しい `GenericPrincipal` オブジェクトを作成し、これを `HttpContext.User` オブジェクトに割り当てます。 `GenericPrincipal`などのプリンシパルの目的は、認証されたユーザーの名前と自分が属しているロールを識別することです。 この目的は、すべてのプリンシパルオブジェクトに `Identity` プロパティと `IsInRole(roleName)` メソッドがあるという事実によって明らかになります。 ただし、`FormsAuthenticationModule`はロール情報の記録には関心がなく、作成した `GenericPrincipal` オブジェクトはロールを指定しません。

ロールフレームワークが有効になっている場合、`FormsAuthenticationModule` の後にの HTTP モジュールの手順が[`RoleManagerModule`](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx)され、`AuthenticateRequest` イベントの後に発生する、 [`PostAuthenticateRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)中に認証されたユーザーのロールが識別されます。 要求が認証されたユーザーからのものである場合、`RoleManagerModule` は `FormsAuthenticationModule` によって作成された `GenericPrincipal` オブジェクトを上書きし、 [`RolePrincipal` オブジェクト](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)に置き換えます。 `RolePrincipal` クラスは、Roles API を使用して、ユーザーが属するロールを決定します。

図1は、フォーム認証とロールフレームワークを使用する場合の ASP.NET パイプラインワークフローを示しています。 最初に `FormsAuthenticationModule` が実行され、認証チケットを介してユーザーが識別され、新しい `GenericPrincipal` オブジェクトが作成されます。 次に、の `RoleManagerModule` の手順を実行して、`GenericPrincipal` オブジェクトを `RolePrincipal` オブジェクトで上書きします。

匿名ユーザーがサイトにアクセスした場合、`FormsAuthenticationModule` も `RoleManagerModule` もプリンシパルオブジェクトを作成しません。

[フォーム認証とロールフレームワークを使用するときに認証されたユーザーの ASP.NET パイプラインイベントを ![する](role-based-authorization-vb/_static/image2.png)](role-based-authorization-vb/_static/image1.png)

**図 1**: フォーム認証とロールフレームワークを使用する場合の認証されたユーザーの ASP.NET パイプラインイベント ([クリックしてフルサイズのイメージを表示する](role-based-authorization-vb/_static/image3.png))

### <a name="caching-role-information-in-a-cookie"></a>Cookie のロール情報のキャッシュ

`RolePrincipal` オブジェクトの `IsInRole(roleName)` メソッドは `Roles`を呼び出します。`GetRolesForUser` ユーザーが*roleName*のメンバーであるかどうかを判断するために、ユーザーのロールを取得します。 この `SqlRoleProvider`を使用すると、ロールストアデータベースに対するクエリが実行されます。 ロールベースの URL 承認規則を使用する場合、ロールベースの URL 承認規則によって保護されているページへのすべての要求に対して、`RolePrincipal`の `IsInRole` メソッドが呼び出されます。 `Roles` framework には、すべての要求についてデータベース内のロール情報を参照する必要はなく、ユーザーのロールを cookie にキャッシュするオプションが用意されています。

ロールフレームワークが、ユーザーのロールを cookie にキャッシュするように構成されている場合、`RoleManagerModule` は、ASP.NET パイプラインの[`EndRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)中に cookie を作成します。 この cookie は、`PostAuthenticateRequest`内の後続の要求で使用されます。これは、`RolePrincipal` オブジェクトが作成されるときです。 Cookie が有効で有効期限が切れていない場合は、cookie 内のデータが解析され、ユーザーのロールを設定するために使用されます。これにより `RolePrincipal`、ユーザーのロールを決定するために `Roles` クラスを呼び出す必要がなくなります。 図2は、このワークフローを示しています。

[パフォーマンスを向上させるために、ユーザーのロール情報をクッキーに格納できる ![](role-based-authorization-vb/_static/image5.png)](role-based-authorization-vb/_static/image4.png)

**図 2**: ユーザーのロール情報は、パフォーマンスを向上させるためにクッキーに格納できます ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image6.png)されます)

既定では、ロールキャッシュクッキー機構は無効になっています。 これは、`<roleManager>`を通じて有効にすることができます。`Web.config`の構成マークアップ。 ここでは、 <a id="_msoanchor_4"> </a>[*ロールの作成と管理*](creating-and-managing-roles-vb.md)に関するチュートリアルで[`<roleManager>` 要素](https://msdn.microsoft.com/library/ms164660.aspx)を使用してロールプロバイダーを指定する方法について説明しました。したがって、この要素はアプリケーションの `Web.config` ファイル内に既に存在している必要があります。 ロールキャッシュ cookie の設定は、`<roleManager>`の属性として指定されます。要素、およびは表1にまとめられています。

> [!NOTE]
> 表1に示す構成設定では、結果として得られるロールキャッシュクッキーのプロパティを指定します。 Cookie、そのしくみ、およびさまざまなプロパティの詳細については、[この cookie](http://www.quirksmode.org/js/cookies.html)に関するチュートリアルを参照してください。

| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>説明</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              クッキーのキャッシュを使用するかどうかを示すブール値です。 既定値は `false` です。                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     ロールキャッシュクッキーの名前。 既定値は "です。ASPXROLES "。                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                ロール名のクッキーのパス。 パス属性を使用すると、開発者は cookie のスコープを特定のディレクトリ階層に限定できます。 既定値は "/" です。これは、ドメインに対して行われたすべての要求に認証チケットクッキーを送信するようブラウザーに通知します。                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               ロールキャッシュクッキーを保護するために使用される手法を示します。 使用できる値は、`All` (既定値) です。`Encryption`;`None`;および `Validation`ます。 これらの保護レベルの詳細に<a id="_anchor_5"></a>ついては、 [ *「フォーム認証の構成」および「高度なトピック*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)」の手順3を参照してください。                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   認証 cookie の送信に SSL 接続が必要かどうかを示すブール値。 既定値は `false`です。                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  シングルセッション中にユーザーがサイトにアクセスするたびに cookie のタイムアウトをリセットするかどうかを示すブール値です。 既定値は `false`です。 この値は、`createPersistentCookie` が `true`に設定されている場合にのみ関連します。                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         認証チケットのクッキーの有効期限が切れるまでの時間を分単位で指定します。 既定値は `30`です。 この値は、`createPersistentCookie` が `true`に設定されている場合にのみ関連します。                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   ロールキャッシュクッキーがセッション cookie であるか、永続的なクッキーであるかを指定するブール値です。 `false` (既定値) の場合、セッション cookie が使用されます。これは、ブラウザーを閉じたときに削除されます。 `true`場合は、永続的な cookie が使用されます。`cookieSlidingExpiration`の値によっては、作成後または前の訪問後に、`cookieTimeout` 期限切れになります。                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 Cookie のドメイン値を指定します。 既定値は空の文字列です。これにより、ブラウザーは発行元のドメイン (www.yourdomain.com など) を使用します。 この場合、admin.yourdomain.com などのサブドメインに要求を行うときに cookie は送信され<strong>ません</strong>。 Cookie をすべてのサブドメインに渡す必要がある場合は、`domain` 属性を "yourdomain.com" に設定してカスタマイズする必要があります。                                                                                                                                                 |
|    `maxCachedResults`     | クッキーにキャッシュされるロール名の最大数を指定します。 既定値は 25 です。 `RoleManagerModule` は、`maxCachedResults` のロールを超えるユーザーの cookie を作成しません。 その結果、`RolePrincipal` オブジェクトの `IsInRole` メソッドは、`Roles` クラスを使用してユーザーのロールを決定します。 `maxCachedResults` 存在する理由は、多くのユーザーエージェントが4096バイトを超える cookie を許可しないためです。 この上限は、このサイズ制限を超える可能性を低減することを目的としています。 ロール名が非常に長い場合は、より小さな `maxCachedResults` 値を指定することを検討してください。contrariwise、非常に短いロール名を使用している場合は、この値を増やすことができます。 |

**表 1**: ロールキャッシュクッキーの構成オプション

持続性のないロールキャッシュクッキーを使用するようにアプリケーションを構成してみましょう。 これを行うには、`Web.config` の `<roleManager>` 要素を更新して、次の cookie に関連する属性を追加します。

[!code-xml[Main](role-based-authorization-vb/samples/sample1.xml)]

`<roleManager>`を更新しました。要素には、`cacheRolesInCookie`、`createPersistentCookie`、および `cookieProtection`の3つの属性を追加します。 `cacheRolesInCookie` を `true`に設定することにより、`RoleManagerModule` は、各要求のユーザーのロール情報を参照するのではなく、ユーザーのロールを cookie に自動的にキャッシュするようになります。 `createPersistentCookie` と `cookieProtection` 属性をそれぞれ `false` および `All`に明示的に設定します。 技術的には、これらの属性を既定値に割り当てただけなので、これらの属性の値を指定する必要はありませんでしたが、永続的な cookie を使用していないこと、および cookie が暗号化および検証されていることを明示的に明確にするために、ここに配置しました。

必要な作業は以上です。 その後、ロールフレームワークはユーザーのロールを cookie にキャッシュします。 ユーザーのブラウザーで cookie がサポートされていない場合、または cookie が削除されたり失われたりした場合は、大きな問題はありません。 `RolePrincipal` オブジェクトは、cookie (または無効または有効期限が切れたもの) が使用できない場合にのみ、`Roles` クラスを使用します。

> [!NOTE]
> Microsoft のパターン &amp; プラクティスグループは、永続的なロールキャッシュクッキーの使用を推奨していません。 ロールキャッシュクッキーを所有しているため、ロールのメンバーシップを証明するには十分です。ハッカーが何らかの方法で有効なユーザーの cookie にアクセスできる場合は、そのユーザーを偽装できます。 Cookie がユーザーのブラウザーで永続化されている場合、このような事態が発生する可能性は高くなります。 このセキュリティの推奨事項とその他のセキュリティの問題の詳細については、 [ASP.NET 2.0 のセキュリティの質問リスト](https://msdn.microsoft.com/library/ms998375.aspx)を参照してください。

## <a name="step-1-defining-role-based-url-authorization-rules"></a>手順 1: ロールベースの URL 承認規則を定義する

<a id="_msoanchor_6"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)のチュートリアルで説明したように、URL 承認では、ユーザーごとまたはロールごとにページのセットへのアクセスを制限する手段が提供されます。 URL 承認規則は、`<allow>` と `<deny>` の子要素を持つ[`<authorization>` 要素](https://msdn.microsoft.com/library/8d82143t.aspx)を使用して、`Web.config` に記載されています。 前のチュートリアルで説明したユーザー関連の承認規則に加えて、各 `<allow>` および `<deny>` 子要素には次のものも含まれます。

- 特定のロール
- ロールのコンマ区切りの一覧

たとえば、URL 承認規則によって、管理者ロールとスーパーバイザーロールのユーザーにアクセス権が付与されますが、他のユーザーへのアクセスは拒否されます。

[!code-xml[Main](role-based-authorization-vb/samples/sample2.xml)]

上のマークアップの `<allow>` 要素は、管理者ロールとスーパーバイザーロールが許可されていることを示します。`<deny>`;要素は、*すべて*のユーザーが拒否されることを示します。

アプリケーションを構成して、`ManageRoles.aspx`、`UsersAndRoles.aspx`、および `CreateUserWizardWithRoles.aspx` の各ページが管理者ロールのユーザーのみにアクセスできるようにし、`RoleBasedAuthorization.aspx` のページにはすべての訪問者がアクセスできるようにします。

これを行うには、まず、`Roles` フォルダーに `Web.config` ファイルを追加します。

[Roles ディレクトリに web.config ファイルを追加 ![には](role-based-authorization-vb/_static/image8.png)](role-based-authorization-vb/_static/image7.png)

**図 3**: `Roles` ディレクトリに `Web.config` ファイルを追加する ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image9.png)されます)

次に、次の構成マークアップを `Web.config`に追加します。

[!code-xml[Main](role-based-authorization-vb/samples/sample3.xml)]

`<system.web>` セクションの `<authorization>` 要素は、管理者ロールのユーザーのみが `Roles` ディレクトリ内の ASP.NET リソースにアクセスできることを示します。 `<location>` 要素は、`RoleBasedAuthorization.aspx` ページの代替 URL 承認規則のセットを定義し、すべてのユーザーがそのページにアクセスできるようにします。

`Web.config`への変更を保存したら、管理者ロールに含まれていないユーザーとしてログインし、保護されたページのいずれかにアクセスします。 `UrlAuthorizationModule` は、要求されたリソースにアクセスするためのアクセス許可がないことを検出します。その結果、`FormsAuthenticationModule` によって、ログインページにリダイレクトされます。 ログインページが `UnauthorizedAccess.aspx` ページにリダイレクトされます (図4を参照)。 ログインページから `UnauthorizedAccess.aspx` へのこの最後のリダイレクトは、 <a id="_msoanchor_7"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)チュートリアルの手順 2. でログインページに追加したコードによって発生します。 特に、クエリ文字列に `ReturnUrl` パラメーターが含まれている場合、ログインページは、認証されたユーザーを `UnauthorizedAccess.aspx` に自動的にリダイレクトします。このパラメーターは、ユーザーが表示を許可されていないページを表示しようとした後に、ユーザーがログインページに到着したことを示します。

[管理者ロールのユーザーのみが保護されたページを表示できる ![](role-based-authorization-vb/_static/image11.png)](role-based-authorization-vb/_static/image10.png)

**図 4**: 管理者ロールのユーザーのみが保護されたページを表示できる ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image12.png)されます)

ログオフし、管理者ロールのユーザーとしてログインします。 これで、3つの保護されたページを表示できるようになります。

[UsersAndRoles ページにアクセスできるのは管理者ロールであるためです。 ![](role-based-authorization-vb/_static/image14.png)](role-based-authorization-vb/_static/image13.png)

**図 5**: `UsersAndRoles.aspx` ページにアクセスできるのは管理者ロールであるためです ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image15.png)されます)。

> [!NOTE]
> URL 承認規則を指定する場合–ロールまたはユーザーにとって、ルールは、上から順番に1つずつ分析されることに注意することが重要です。 一致が見つかるとすぐに、`<allow>` または `<deny>` 要素で一致が見つかったかどうかによって、ユーザーはアクセスを許可または拒否されます。 **一致するものが見つからない場合は、ユーザーにアクセス権が付与されます。** そのため、1つ以上のユーザーアカウントへのアクセスを制限する場合は、URL 承認構成の最後の要素として `<deny>` 要素を使用する必要があります。 **URL 承認規則に`<deny>`要素が含まれていない場合** **、すべてのユーザーにアクセス権が付与されます。** URL 承認規則の分析方法の詳細については、「 <a id="_msoanchor_8"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)のチュートリアル」の「`UrlAuthorizationModule` がアクセスを許可または拒否するための承認規則を使用する方法について」を参照してください。

## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>手順 2: 現在ログインしているユーザーのロールに基づいて機能を制限する

URL 承認を使用すると、許可されている id と、特定のページ (またはフォルダーとそのサブフォルダー内のすべてのページ) の表示が拒否されている id を示す粒度の粗い承認規則を簡単に指定できます。 ただし、場合によっては、すべてのユーザーがページにアクセスできるようにする必要がありますが、訪問しているユーザーのロールに基づいてページの機能を制限したい場合があります。 この場合、ユーザーのロールに基づいてデータを表示または非表示にしたり、特定のロールに属しているユーザーに追加の機能を提供したりすることがあります。

このような細かい粒度のロールベースの承認規則は、宣言によって、またはプログラムによって (または2つの組み合わせを使用して) 実装できます。 次のセクションでは、LoginView コントロールを使用して宣言的に細かい粒度の承認を実装する方法について説明します。 次に、プログラムによる手法について説明します。 ただし、細かい粒度の承認規則の適用については、まず、アクセスするユーザーの役割によって機能が異なるページを作成する必要があります。

GridView で、システム内のすべてのユーザーアカウントを一覧表示するページを作成してみましょう。 GridView には、ユーザーのユーザー名、電子メールアドレス、最後のログイン日、およびユーザーに関するコメントが含まれます。 GridView には、ユーザーの情報を表示するだけでなく、編集および削除機能も含まれています。 最初に、すべてのユーザーが編集および削除機能を使用できるように、このページを作成します。 「LoginView コントロールの使用」と「プログラムによる機能制限」のセクションでは、訪問しているユーザーのロールに基づいてこれらの機能を有効または無効にする方法について説明します。

> [!NOTE]
> ビルドしようとしている ASP.NET ページでは、GridView コントロールを使用してユーザーアカウントを表示します。 このチュートリアルシリーズでは、フォーム認証、承認、ユーザーアカウント、およびロールに焦点を当てているため、GridView コントロールの内部動作についてはあまり時間をかけたくありません。 このチュートリアルでは、このページを設定するための具体的な手順について説明しますが、特定の選択が行われた理由や、レンダリングされた出力に対する特定のプロパティの影響については詳しく説明しません。 GridView コントロールの詳細な調査については、「 *[ASP.NET 2.0 チュートリアルシリーズのデータを操作する」](../../data-access/index.md)* をご覧ください。

まず、`Roles` フォルダーの [`RoleBasedAuthorization.aspx`] ページを開きます。 GridView をページからデザイナーにドラッグし、その `ID` を `UserGrid`に設定します。 現時点では、`Membership`を呼び出すコードを記述します。`GetAllUsers` メソッドを作成し、生成された `MembershipUserCollection` オブジェクトを GridView にバインドします。 `MembershipUserCollection` には、システム内の各ユーザーアカウントの `MembershipUser` オブジェクトが含まれています。`MembershipUser` オブジェクトには、`UserName`、`Email`、`LastLoginDate` などのプロパティがあります。

ユーザーアカウントをグリッドにバインドするコードを記述する前に、まず GridView のフィールドを定義してみましょう。 GridView のスマートタグから、[列の編集] リンクをクリックして [フィールド] ダイアログボックスを起動します (図6を参照)。 ここで、左下隅にある [フィールドの自動生成] チェックボックスをオフにします。 この GridView に編集および削除機能を含めるためには、CommandField を追加し、その `ShowEditButton` と `ShowDeleteButton` プロパティを True に設定します。 次に、`UserName`、`Email`、`LastLoginDate`、および `Comment` の各プロパティを表示する4つのフィールドを追加します。 2つの編集可能なフィールド (`Email` と `Comment`) の2つの読み取り専用プロパティ (`UserName` と `LastLoginDate`) および TemplateFields には、BoundField を使用します。

最初の BoundField で `UserName` プロパティを表示します。`HeaderText` と `DataField` のプロパティを "UserName" に設定します。 このフィールドは編集できないので、[`ReadOnly`] プロパティを [True] に設定します。 `HeaderText` を "Last Login" に設定し、その `DataField` を "LastLoginDate" に設定して、`LastLoginDate` BoundField を構成します。 日付と時刻ではなく、日付のみが表示されるように、この BoundField の出力を書式設定してみましょう。 これを実現するには、この BoundField の `HtmlEncode` プロパティを False に設定し、その `DataFormatString` プロパティを "{0:d}" に設定します。 また、`ReadOnly` プロパティを True に設定します。

2つの TemplateFields の `HeaderText` プロパティを "Email" と "Comment" に設定します。

[![GridView のフィールドは、[フィールド] ダイアログボックスを使用して構成できます。](role-based-authorization-vb/_static/image17.png)](role-based-authorization-vb/_static/image16.png)

**図 6**: GridView のフィールドは、[フィールド] ダイアログボックスを使用して構成できます ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image18.png)されます)。

次に、"Email" および "Comment" TemplateFields の `ItemTemplate` と `EditItemTemplate` を定義する必要があります。 各 `ItemTemplates` にラベル Web コントロールを追加し、それぞれの `Text` プロパティを `Email` および `Comment` プロパティにそれぞれバインドします。

"Email" TemplateField の場合、`EditItemTemplate` に `Email` という名前のテキストボックスを追加し、双方向のデータバインディングを使用してその `Text` プロパティを `Email` プロパティにバインドします。 `EditItemTemplate` に RequiredFieldValidator と RegularExpressionValidator を追加して、Email プロパティを編集しているビジターが有効な電子メールアドレスを入力したことを確認します。 "Comment" TemplateField の場合は、`Comment` という名前の複数行のテキストボックスを `EditItemTemplate`に追加します。 TextBox の `Columns` と `Rows` の各プロパティをそれぞれ40と4に設定し、双方向のデータバインディングを使用して、その `Text` プロパティを `Comment` プロパティにバインドします。

これらの TemplateFields を構成した後、宣言型マークアップは次のようになります。

[!code-aspx[Main](role-based-authorization-vb/samples/sample4.aspx)]

ユーザーアカウントを編集または削除するときは、そのユーザーの `UserName` プロパティ値を把握しておく必要があります。 Gridview の `DataKeyNames` プロパティを "UserName" に設定して、GridView の `DataKeys` コレクションでこの情報を使用できるようにします。

最後に、ValidationSummary コントロールをページに追加し、その `ShowMessageBox` プロパティを True に設定し、その `ShowSummary` プロパティを False に設定します。 これらの設定を使用すると、ユーザーが不明または無効な電子メールアドレスを使用してユーザーアカウントを編集しようとした場合に、ValidationSummary にクライアント側のアラートが表示されます。

[!code-aspx[Main](role-based-authorization-vb/samples/sample5.aspx)]

これで、このページの宣言型マークアップが完了しました。 次のタスクでは、一連のユーザーアカウントを GridView にバインドします。 `Membership.GetAllUsers` によって返された `MembershipUserCollection` を `UserGrid` GridView にバインドする、`RoleBasedAuthorization.aspx` ページの分離コードクラスに `BindUserGrid` という名前のメソッドを追加します。 最初のページにアクセスしたときに、`Page_Load` イベントハンドラーからこのメソッドを呼び出します。

[!code-vb[Main](role-based-authorization-vb/samples/sample6.vb)]

このコードを配置したら、ブラウザーを使用してページにアクセスします。 図7に示すように、システム内の各ユーザーアカウントについて、GridView の一覧が表示されます。

[UserGrid GridView ![システム内の各ユーザーに関する情報を一覧表示する](role-based-authorization-vb/_static/image20.png)](role-based-authorization-vb/_static/image19.png)

**図 7**: `UserGrid` GridView は、システム内の各ユーザーに関する情報を一覧表示します ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image21.png)されます)。

> [!NOTE]
> `UserGrid` GridView では、非ページインターフェイス内のすべてのユーザーが一覧表示されます。 このシンプルなグリッドインターフェイスは、数十以上のユーザーが存在するシナリオには適していません。 1つの方法は、ページングを有効にするように GridView を構成することです。 `Membership.GetAllUsers` メソッドには、2つのオーバーロードがあります。1つは入力パラメーターを受け入れず、すべてのユーザーと、ページインデックスとページサイズに対して整数値を受け取るすべてのユーザーと、指定されたユーザーのサブセットのみを返します。 2番目のオーバーロードを使用すると、*すべて*のユーザーアカウントではなくユーザーアカウントの正確なサブセットだけが返されるため、ユーザーをより効率的にページ化できます。 何千ものユーザーアカウントがある場合は、フィルターベースのインターフェイスを検討してください。たとえば、ユーザー名が選択した文字で始まるユーザーのみを表示します。 [`Membership.FindUsersByName` 方法](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)は、フィルターベースのユーザーインターフェイスを構築する場合に最適です。 このようなインターフェイスの構築については、今後のチュートリアルで説明します。

GridView コントロールでは、SqlDataSource や ObjectDataSource など、適切に構成されたデータソースコントロールにコントロールがバインドされている場合に、組み込みの編集と削除のサポートが提供されます。 ただし、GridView の `UserGrid` には、プログラムによってデータがバインドされます。そのため、これら2つのタスクを実行するコードを記述する必要があります。 具体的には、gridview の `RowEditing`、`RowCancelingEdit`、`RowUpdating`、および `RowDeleting` イベントのイベントハンドラーを作成する必要があります。これは、ユーザーが GridView の [編集]、[キャンセル]、[更新]、または [削除] ボタンをクリックしたときに発生します。

まず、GridView の `RowEditing`、`RowCancelingEdit`、および `RowUpdating` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](role-based-authorization-vb/samples/sample7.vb)]

`RowEditing` イベントハンドラーと `RowCancelingEdit` イベントハンドラーは、GridView の `EditIndex` プロパティを設定し、ユーザーアカウントの一覧をグリッドに再バインドします。 注目すべきことは、`RowUpdating` イベントハンドラーです。 このイベントハンドラーは、データが有効であることを確認し、`DataKeys` コレクションから編集されたユーザーアカウントの `UserName` 値を取得することによって開始します。 2つの TemplateFields ' `EditItemTemplate` s 内の `Email` と `Comment` のテキストボックスが、プログラムによって参照されます。 `Text` のプロパティには、編集した電子メールアドレスとコメントが含まれています。

メンバーシップ API を使用してユーザーアカウントを更新するには、最初にユーザーの情報を取得する必要があります。そのためには、`Membership.GetUser(userName)`の呼び出しを使用します。 返された `MembershipUser` オブジェクトの `Email` と `Comment` プロパティは、編集インターフェイスから2つのテキストボックスに入力された値で更新されます。 最後に、これらの変更は[`Membership.UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)を呼び出すことによって保存されます。 `RowUpdating` イベントハンドラーは、GridView を編集前のインターフェイスに戻すことによって完了します。

次に、`RowDeleting` RowDeleting イベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](role-based-authorization-vb/samples/sample8.vb)]

上記のイベントハンドラーは、GridView の `DataKeys` コレクションから `UserName` 値を取得することによって開始されます。この `UserName` 値は、メンバーシップクラスの[`DeleteUser` メソッド](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)に渡されます。 `DeleteUser` メソッドは、関連するメンバーシップデータ (このユーザーが属するロールなど) を含む、システムからユーザーアカウントを削除します。 ユーザーを削除すると、グリッドの `EditIndex` が-1 に設定されます (ユーザーが [削除] をクリックしたときに、別の行が編集モードになっている場合)。 `BindUserGrid` メソッドが呼び出されます。

> [!NOTE]
> ユーザーアカウントを削除する前に、[削除] ボタンをクリックしても、ユーザーからの確認は必要ありません。 アカウントが誤って削除される可能性を減らすために、何らかの形式のユーザー確認を追加することをお勧めします。 アクションを確認する最も簡単な方法の1つは、クライアント側の [確認] ダイアログボックスを使用することです。 この手法の詳細については、「[削除時にクライアント側の確認を追加](https://asp.net/learn/data-access/tutorial-42-vb.aspx)する」を参照してください。

このページが想定どおりに機能することを確認します。 任意のユーザーの電子メールアドレスとコメントを編集できるだけでなく、すべてのユーザーアカウントを削除することもできます。 [`RoleBasedAuthorization.aspx`] ページはすべてのユーザーがアクセスできるので、匿名訪問者でも、このページにアクセスしてユーザーアカウントを編集および削除できます。 このページを更新して、スーパーバイザーロールと管理者ロールのユーザーのみがユーザーの電子メールアドレスとコメントを編集できるようにします。管理者のみがユーザーアカウントを削除できます。

「LoginView コントロールの使用」セクションでは、LoginView コントロールを使用して、ユーザーのロールに固有の命令を表示する方法について説明します。 管理者ロールのユーザーがこのページにアクセスする場合は、ユーザーを編集および削除する方法についての説明が表示されます。 スーパーバイザーロールのユーザーがこのページに到達した場合は、ユーザーを編集するための手順が表示されます。 また、ビジターが匿名であるか、スーパーバイザーまたは管理者ロールに含まれていない場合は、ユーザーアカウント情報を編集または削除できないことを説明するメッセージが表示されます。 「プログラムによって機能を制限する」セクションでは、ユーザーのロールに基づいて、[編集] ボタンと [削除] ボタンをプログラムで表示または非表示にするコードを記述します。

### <a name="using-the-loginview-control"></a>LoginView コントロールの使用

前のチュートリアルで説明したように、LoginView コントロールは、認証されたユーザーと匿名ユーザー用にさまざまなインターフェイスを表示する場合に便利ですが、LoginView コントロールを使用して、ユーザーのロールに基づいてさまざまなマークアップを表示することもできます。 LoginView コントロールを使用して、訪問しているユーザーのロールに基づいてさまざまな命令を表示してみましょう。

まず、`UserGrid` GridView の上に LoginView を追加します。 前に説明したように、LoginView コントロールには、`AnonymousTemplate` と `LoggedInTemplate`の2つの組み込みテンプレートがあります。 これらの両方のテンプレートに簡単なメッセージを入力して、ユーザー情報を編集または削除できないことをユーザーに通知します。

[!code-aspx[Main](role-based-authorization-vb/samples/sample9.aspx)]

LoginView コントロールには、`AnonymousTemplate` と `LoggedInTemplate`に加えて、ロール固有のテンプレートである*Rolegroups*を含めることができます。 各 RoleGroup には、`Roles`という1つのプロパティが含まれています。このプロパティは、RoleGroup が適用されるロールを指定します。 `Roles` プロパティは、1つのロール ("Administrators" など) に設定することも、ロールのコンマ区切りの一覧 ("管理者"、"スーパーバイザー" など) に設定することもできます。

RoleGroups を管理するには、コントロールのスマートタグから [RoleGroups の編集] リンクをクリックして、Rolegroups コレクションエディターを表示します。 2つの新しい RoleGroups を追加します。 最初の RoleGroup の `Roles` プロパティを "Administrators" に、2番目のを "スーパーバイザー" に設定します。

[RoleGroup コレクションエディターを使用して LoginView のロール固有テンプレートを管理 ![には](role-based-authorization-vb/_static/image23.png)](role-based-authorization-vb/_static/image22.png)

**図 8**: Rolegroup コレクションエディターを使用して LoginView のロール固有のテンプレートを管理[する (クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image24.png)されます)

[OK] をクリックして、RoleGroup コレクションエディターを閉じます。これにより、LoginView の宣言型マークアップが更新され、RoleGroup コレクションエディターで定義されている各 RoleGroup の `<asp:RoleGroup>` 子要素を含む `<RoleGroups>` セクションが追加されます。 さらに、LoginView のスマートタグの [Views] \ (ビュー \) ドロップダウンリストには、最初に `AnonymousTemplate` と `LoggedInTemplate` のみが表示され、追加された RoleGroups も含まれています。

RoleGroups を編集して、ユーザーアカウントの編集方法に関する指示がスーパーバイザーロールのユーザーに表示されるようにします。管理者ロールのユーザーには、編集および削除の手順が表示されます。 これらの変更を行った後、LoginView の宣言型マークアップは次のようになります。

[!code-aspx[Main](role-based-authorization-vb/samples/sample10.aspx)]

これらの変更を行った後、ページを保存し、ブラウザーを使用してアクセスします。 まず、匿名ユーザーとしてページにアクセスします。 "システムにログインしていません" というメッセージが表示されます。 そのため、ユーザー情報を編集または削除することはできません。 " 次に、認証されたユーザーとしてログインしますが、スーパーバイザーと管理者の両方のロールにはログインしません。 今度は、"スーパーバイザーまたは管理者ロールのメンバーではありません" というメッセージが表示されます。 そのため、ユーザー情報を編集または削除することはできません。 "

次に、スーパーバイザーロールのメンバーであるユーザーとしてログインします。 この時点で、スーパーバイザーのロール固有のメッセージが表示されます (図9を参照)。 また、管理者ロールのユーザーとしてログインすると、管理者ロール固有のメッセージが表示されます (図10を参照)。

[![は、スーパーバイザーロール固有のメッセージが表示されます。](role-based-authorization-vb/_static/image26.png)](role-based-authorization-vb/_static/image25.png)

**図 9**: スーパーバイザーのロール固有のメッセージが表示される ([クリックしてフルサイズの画像を表示する](role-based-authorization-vb/_static/image27.png))

[![Tito には、管理者の役割固有のメッセージが表示されます。](role-based-authorization-vb/_static/image29.png)](role-based-authorization-vb/_static/image28.png)

**図 10**: 管理者ロール固有のメッセージが表示されます ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image30.png)されます)

図9と10のスクリーンショットでは、複数のテンプレートが適用されている場合でも、LoginView は1つのテンプレートのみをレンダリングします。 LoginView は両方ともユーザーにログインしていますが、では `LoggedInTemplate`なく、一致する RoleGroup のみがレンダリングされます。 さらに、Tito は Administrators ロールと監修者ロールの両方に属していますが、LoginView コントロールは、スーパーバイザーではなく、管理者ロール固有のテンプレートを表示します。

図11は、レンダリングするテンプレートを決定するために LoginView コントロールによって使用されるワークフローを示しています。 複数の RoleGroup が指定されている場合、LoginView テンプレートは、に一致する*最初*の rolegroup をレンダリングします。 つまり、スーパーバイザー RoleGroup を最初の RoleGroup として、管理者を2番目のロールグループとして配置した場合、このページにアクセスすると、スーパーバイザーメッセージが表示されます。

[表示するテンプレートを決定するための LoginView コントロールのワークフローの ![](role-based-authorization-vb/_static/image32.png)](role-based-authorization-vb/_static/image31.png)

**図 11**: レンダリングするテンプレートを決定するための LoginView コントロールのワークフロー ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image33.png)されます)

### <a name="programmatically-limiting-functionality"></a>プログラムによる機能制限

LoginView コントロールでは、ページにアクセスしているユーザーのロールに基づいてさまざまな命令が表示されますが、[編集] ボタンと [キャンセル] ボタンはすべて表示されます。 管理者ロールと管理者ロールのいずれにも属していない匿名の訪問者とユーザーの編集ボタンと削除ボタンは、プログラムによって非表示にする必要があります。 管理者ではないすべてのユーザーに対して、[削除] ボタンを非表示にする必要があります。 これを実現するために、コードを記述して、CommandField の [編集] および [削除] リンクボタンをプログラムで参照し、必要に応じて `Visible` プロパティを `False`に設定します。

CommandField 内のコントロールをプログラムで参照する最も簡単な方法は、最初に、テンプレートをテンプレートに変換することです。 これを実現するには、GridView のスマートタグから [列の編集] リンクをクリックし、現在のフィールドの一覧から CommandField を選択して、[このフィールドを TemplateField に変換する] リンクをクリックします。 これにより、`ItemTemplate` と `EditItemTemplate`を持つ TemplateField に CommandField が変換されます。 `ItemTemplate` には、[更新] ボタンと [キャンセル] ボタンが格納されて `EditItemTemplate` いるときに、[編集] および [削除] リンクボタンが含まれています。

[CommandField を TemplateField に変換 ![には](role-based-authorization-vb/_static/image35.png)](role-based-authorization-vb/_static/image34.png)

**図 12**: Commandfield を TemplateField に変換する ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image36.png)されます)

`ItemTemplate`の [編集] および [削除] リンクボタンを更新し、それぞれの `ID` プロパティを `EditButton` と `DeleteButton`の値にそれぞれ設定します。

[!code-aspx[Main](role-based-authorization-vb/samples/sample11.aspx)]

GridView にデータがバインドされるたびに、GridView は `DataSource` プロパティ内のレコードを列挙し、対応する `GridViewRow` オブジェクトを生成します。 `GridViewRow` オブジェクトが作成されるたびに、`RowCreated` イベントが発生します。 承認されていないユーザーの [編集] ボタンと [削除] ボタンを非表示にするには、このイベントのイベントハンドラーを作成し、プログラムを使用して [リンクの編集と削除] ボタンを参照し、`Visible` プロパティを適宜設定する必要があります。

`RowCreated` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](role-based-authorization-vb/samples/sample12.vb)]

`RowCreated` イベントは、ヘッダー、フッター、ページャーインターフェイスなど、*すべて*の GridView 行に対して発生することに注意してください。 編集モードではないデータ行を処理している場合は、編集および削除のリンクボタンをプログラムで参照するだけです (編集モードの行には、編集と削除の代わりに [更新] ボタンと [キャンセル] ボタンがあるため)。 このチェックは、`If` ステートメントによって処理されます。

編集モードになっていないデータ行を処理している場合は、[編集] および [削除] LinkButtons が参照され、`User` オブジェクトの `IsInRole(roleName)` メソッドによって返されるブール値に基づいて `Visible` プロパティが設定されます。 `User` オブジェクトは、`RoleManagerModule`によって作成されたプリンシパルを参照します。その結果、`IsInRole(roleName)` メソッドは Roles API を使用して、現在のビジターが*roleName*に属しているかどうかを判断します。

> [!NOTE]
> Roles クラスを直接使用して、`User.IsInRole(roleName)` への呼び出しを[`Roles.IsUserInRole(roleName)` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)の呼び出しに置き換えることもできました。 ここでは、Roles API を直接使用するよりも効率的であるため、この例では principal オブジェクトの `IsInRole(roleName)` メソッドを使用することにしました。 このチュートリアルの前半では、ユーザーのロールを cookie にキャッシュするようにロールマネージャーを構成しました。 このキャッシュされた cookie データは、プリンシパルの `IsInRole(roleName)` メソッドが呼び出された場合にのみ使用されます。Roles API を直接呼び出すには、常にロールストアへのトリップが伴います。 ロールが cookie にキャッシュされていない場合でも、通常、プリンシパルオブジェクトの `IsInRole(roleName)` メソッドを呼び出すと、要求中に最初に呼び出されたときに結果がキャッシュされるため、通常より効率的になります。 一方、ロール API はキャッシュを実行しません。 `RowCreated` イベントは GridView 内のすべての行に対して1回発生するため、`User.IsInRole(roleName)` を使用すると、ロールストアへのトリップが1回だけ行われます。一方、`Roles.IsUserInRole(roleName)` には*n*回のトリップが必要です。ここで、 *n*はグリッドに表示されるユーザーアカウントの数です。

[編集] ボタンの `Visible` プロパティは、このページにアクセスするユーザーが管理者またはスーパーバイザーロールにある場合は `True` に設定されます。それ以外の場合は、`False`に設定されます。 [削除] ボタンの `Visible` プロパティは、ユーザーが管理者ロールにある場合にのみ `True` に設定されます。

ブラウザーを使用してこのページをテストします。 匿名ビジターまたはスーパーバイザーでも管理者でもないユーザーとしてページを閲覧すると、CommandField は空になります。これはまだ存在していますが、[編集] または [削除] ボタンのない細いスリーバーです。

> [!NOTE]
> 監修者以外の管理者がページにアクセスしているときに、CommandField を完全に非表示にすることができます。 この作業をリーダーの演習として残しておきます。

[[編集] ボタンと [削除] ボタンが非スーパーバイザーと非管理者に対して非表示に ![](role-based-authorization-vb/_static/image38.png)](role-based-authorization-vb/_static/image37.png)

**図 13**: [編集] ボタンと [削除] ボタンが非スーパーバイザーと非管理者に対して非表示になる ([クリックしてフルサイズの画像を表示する](role-based-authorization-vb/_static/image39.png))

スーパーバイザーロールに属していても管理者ロールに属していないユーザーがアクセスした場合、[編集] ボタンのみが表示されます。

[![スーパーバイザーで [編集] ボタンが使用可能な場合、[削除] ボタンは非表示になります。](role-based-authorization-vb/_static/image41.png)](role-based-authorization-vb/_static/image40.png)

**図 14**: スーパーバイザーで [編集] ボタンを使用できても、[削除] ボタンは非表示になります ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image42.png)されます)

また、管理者がアクセスした場合は、[編集] ボタンと [削除] ボタンの両方にアクセスできます。

[[編集] ボタンと [削除] ボタンは、管理者に対してのみ使用でき ![](role-based-authorization-vb/_static/image44.png)](role-based-authorization-vb/_static/image43.png)

**図 15**: [編集] ボタンと [削除] ボタンは、管理者に対してのみ使用できます ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image45.png)されます)

## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>手順 3: クラスおよびメソッドへのロールベースの承認規則の適用

手順 2. では、スーパーバイザーおよび管理者ロールのユーザーに編集機能を制限し、管理者のみに機能を削除します。 これは、承認されていないユーザーに関連付けられたユーザーインターフェイス要素をプログラムによって隠すことで実現されました。 このようなメジャーは、許可されていないユーザーが特権アクションを実行できないことを保証しません。 後で追加されたユーザーインターフェイス要素や、承認されていないユーザーに対して非表示にし忘れたユーザーインターフェイス要素がある可能性があります。 または、ASP.NET ページを取得して目的のメソッドを実行する他の方法をハッカーが発見することがあります。

権限のないユーザーが特定の機能にアクセスできないようにする簡単な方法は、そのクラスまたはメソッドを[`PrincipalPermission` 属性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)で修飾することです。 .NET ランタイムでクラスを使用するか、またはメソッドのいずれかを実行すると、現在のセキュリティコンテキストにアクセス許可があるかどうかがチェックされます。 `PrincipalPermission` 属性は、これらの規則を定義できるメカニズムを提供します。

ここでは、 <a id="_msoanchor_9"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)チュートリアルで `PrincipalPermission` 属性を使用する方法について説明しました。 具体的には、GridView の `SelectedIndexChanged` と `RowDeleting` イベントハンドラーを、それぞれ authenticated users および Tito によってのみ実行できるように装飾する方法を説明しました。 `PrincipalPermission` 属性は、ロールと同様に機能します。

GridView の `RowUpdating` および `RowDeleting` イベントハンドラーの `PrincipalPermission` 属性を使用して、承認されていないユーザーの実行を禁止する方法を説明します。 それぞれの関数定義の上に適切な属性を追加するだけで十分です。

[!code-vb[Main](role-based-authorization-vb/samples/sample13.vb)]

`RowUpdating` イベントハンドラーの属性は、管理者ロールまたはスーパーバイザーロールのユーザーのみがイベントハンドラーを実行できることを指定します。この場合、`RowDeleting` イベントハンドラーの属性は、管理者ロールのユーザーに対して実行を制限します。

> [!NOTE]
> `PrincipalPermission` 属性は、`System.Security.Permissions` 名前空間のクラスとして表されます。 この名前空間をインポートするには、分離コードクラスファイルの先頭に `Imports System.Security.Permissions` ステートメントを追加してください。

管理者以外の担当者が `RowDeleting` イベントハンドラーを実行しようとした場合、または管理者以外の管理者が `RowUpdating` イベントハンドラーを実行しようとした場合、.NET ランタイムは `SecurityException`を発生させます。

[![、セキュリティコンテキストにメソッドの実行が許可されていない場合は、SecurityException がスローされます。](role-based-authorization-vb/_static/image47.png)](role-based-authorization-vb/_static/image46.png)

**図 16**: セキュリティコンテキストにメソッドの実行が許可されていない場合は、`SecurityException` がスローされます ([クリックすると、フルサイズの画像が表示](role-based-authorization-vb/_static/image48.png)されます)

ASP.NET ページに加えて、多くのアプリケーションには、ビジネスロジックやデータアクセス層などのさまざまなレイヤーを含むアーキテクチャもあります。 これらのレイヤーは、通常、クラスライブラリとして実装され、ビジネスロジックおよびデータに関連する機能を実行するためのクラスとメソッドを提供します。 `PrincipalPermission` 属性は、これらのレイヤーに承認規則を適用する場合にも役立ちます。

`PrincipalPermission` 属性を使用してクラスとメソッドの承認規則を定義する方法の詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログ記事「 [`PrincipalPermissionAttributes`を使用したビジネス層およびデータ層への承認規則の追加](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)」を参照してください。

## <a name="summary"></a>要約

このチュートリアルでは、ユーザーのロールに基づいて粒度の粗い粒度の承認規則を指定する方法について説明しました。 ASP.NET の URL 承認機能を使用すると、ページの開発者は、ページへのアクセスを許可または拒否する id を指定できます。 <a id="_msoanchor_10"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)のチュートリアルで説明したように、URL 承認規則はユーザーごとに適用できます。 また、このチュートリアルの手順1で見たように、ロールごとにロールを適用することもできます。

粒度の細かい承認規則は、宣言によって、またはプログラムによって適用できます。 手順 2. では、LoginView コントロールの RoleGroups 機能を使用して、訪問しているユーザーのロールに基づいて異なる出力を表示する方法を見てきました。 また、ユーザーが特定のロールに属しているかどうかをプログラムで判断する方法と、それに応じてページの機能を調整する方法についても説明しました。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [`PrincipalPermissionAttributes` を使用したビジネス層およびデータ層への承認規則の追加](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 2.0 のメンバーシップ、ロール、およびプロファイルの検証: ロールの操作](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2.0 のセキュリティの質問リスト](https://msdn.microsoft.com/library/ms998375.aspx)
- [`<roleManager>` 要素の技術ドキュメント](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者には、Suchi Teresa Erjee と Murphy が含まれています。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](assigning-roles-to-users-vb.md)
