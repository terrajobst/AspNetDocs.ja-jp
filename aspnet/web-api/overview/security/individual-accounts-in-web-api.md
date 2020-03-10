---
uid: web-api/overview/security/individual-accounts-in-web-api
title: ASP.NET Web API 2.2 | で個別のアカウントとローカルログインを使用して Web API をセキュリティで保護するMicrosoft Docs
author: MikeWasson
description: このトピックでは、OAuth2 を使用して web API をセキュリティで保護し、メンバーシップデータベースに対して認証する方法について説明します。 このチュートリアルで使用されているソフトウェアのバージョンは、Visual Studio 201...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447178"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>ASP.NET Web API 2.2 で個別のアカウントとローカルログインを使用して Web API をセキュリティで保護する

[Mike Wasson](https://github.com/MikeWasson)

[サンプルアプリのダウンロード](https://github.com/MikeWasson/LocalAccountsApp)

> このトピックでは、OAuth2 を使用して web API をセキュリティで保護し、メンバーシップデータベースに対して認証する方法について説明します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - [Visual Studio 2013 Update 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [Web API 2.2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Identity 2.1](../../../identity/index.md)

Visual Studio 2013 の Web API プロジェクトテンプレートでは、次の3つの認証オプションが提供されています。

- **個々のアカウント。** アプリはメンバーシップデータベースを使用します。
- **組織アカウント。** ユーザーは、Azure Active Directory、Office 365、またはオンプレミス Active Directory の資格情報でサインインします。
- **Windows 認証。** このオプションは、イントラネットアプリケーションを対象としており、Windows 認証 IIS モジュールを使用します。

これらのオプションの詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)」を参照してください。

個々のアカウントは、ユーザーがログインするための2つの方法を提供します。

- **ローカルログイン**。 ユーザーは、サイトにユーザー名とパスワードを入力して登録します。 アプリは、メンバーシップデータベースにパスワードハッシュを格納します。 ユーザーがログインすると、ASP.NET Identity システムによってパスワードが検証されます。
- **ソーシャルログイン**。 ユーザーは、Facebook、Microsoft、Google などの外部サービスを使用してサインインします。 アプリでは、メンバーシップデータベースにユーザーのエントリが作成されますが、資格情報は保存されません。 ユーザーは、外部サービスにサインインすることによって認証されます。

この記事では、ローカルログインのシナリオについて説明します。 ローカルログインとソーシャルログインの両方で、Web API は OAuth2 を使用して要求を認証します。 ただし、ローカルとソーシャルのログインでは、資格情報のフローは異なります。

この記事では、ユーザーがログインし、認証された AJAX 呼び出しを web API に送信できるようにする簡単なアプリについて説明します。 サンプルコードは[こちら](https://github.com/MikeWasson/LocalAccountsApp)からダウンロードできます。 この readme では、Visual Studio でサンプルをゼロから作成する方法について説明しています。

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

サンプルアプリでは、データバインディングにはノックアウトを使用し、AJAX 要求を送信するには jQuery を使用します。 ここでは AJAX 呼び出しについて説明します。そのため、この記事では、ノックアウトを知る必要はありません。

その過程で、次のことについて説明します。

- クライアント側でアプリが何をしているか。
- サーバーで何が起こっているか。
- 中間の HTTP トラフィック。

まず、いくつかの OAuth2 用語を定義する必要があります。

- *リソース*。 保護できるデータの一部。
- *リソースサーバー*。 リソースをホストするサーバー。
- *リソース所有者*。 リソースへのアクセス許可を付与できるエンティティ。 (通常はユーザーです)。
- *Client*: リソースへのアクセスを必要とするアプリ。 この記事では、クライアントは web ブラウザーです。
- *アクセストークン*。 リソースへのアクセスを許可するトークン。
- *ベアラートークン*。 任意のユーザーがトークンを使用できるプロパティを持つ、特定の種類のアクセストークン。 つまり、クライアントは、ベアラートークンを使用するために暗号化キーまたはその他のシークレットを必要としません。 そのため、ベアラートークンは HTTPS 経由でのみ使用する必要があり、有効期限が比較的短くなっている必要があります。
- *承認サーバー*。 アクセストークンを提供するサーバー。

アプリケーションは、承認サーバーとリソースサーバーの両方として機能することができます。 Web API プロジェクトテンプレートは、このパターンに従います。

## <a name="local-login-credential-flow"></a>ローカルログイン資格情報のフロー

ローカルログインの場合、Web API は OAuth2 で定義されている[リソース所有者のパスワードフロー](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)を使用します。

1. ユーザーは、クライアントに名前とパスワードを入力します。
2. クライアントは、これらの資格情報を承認サーバーに送信します。
3. 承認サーバーは、資格情報を認証し、アクセストークンを返します。
4. 保護されたリソースにアクセスするために、クライアントは、HTTP 要求の Authorization ヘッダーにアクセストークンを含めます。

![](individual-accounts-in-web-api/_static/image3.png)

Web API プロジェクトテンプレートで**個別のアカウント**を選択すると、プロジェクトには、ユーザーの資格情報を検証してトークンを発行する承認サーバーが含まれます。 次の図は、Web API コンポーネントと同じ資格情報フローを示しています。

![](individual-accounts-in-web-api/_static/image4.png)

このシナリオでは、Web API コントローラーはリソースサーバーとして機能します。 認証フィルターはアクセストークンを検証し、 **[承認]** 属性はリソースを保護するために使用されます。 コントローラーまたはアクションに **[承認]** 属性がある場合、そのコントローラーまたはアクションに対するすべての要求を認証する必要があります。 それ以外の場合は、承認が拒否され、Web API は 401 (未承認) エラーを返します。

承認サーバーと認証フィルターは両方とも、OAuth2 の詳細を処理する[OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)コンポーネントを呼び出します。 設計については、このチュートリアルの後半で詳しく説明します。

## <a name="sending-an-unauthorized-request"></a>承認されていない要求の送信

まず、アプリを実行し、[API の**呼び出し**] ボタンをクリックします。 要求が完了すると、 **[結果]** ボックスにエラーメッセージが表示されます。 これは、要求にアクセストークンが含まれていないため、要求が承認されていないためです。

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

**[Api の呼び出し]** ボタンは、Web API コントローラーアクションを呼び出す AJAX 要求を ~/の値に送信します。 ここでは、AJAX 要求を送信する JavaScript コードのセクションについて説明します。 サンプルアプリでは、すべての JavaScript アプリコードは、スクリプトファイルに含まれています。

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

ユーザーがログインするまで、ベアラートークンは存在しないため、要求に Authorization ヘッダーはありません。 これにより、要求で401エラーが返されます。

HTTP 要求を次に示します。 (私は[Fiddler](http://www.telerik.com/fiddler)を使用して HTTP トラフィックをキャプチャしました)。

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

HTTP 応答:

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

応答には、チャレンジがベアラーに設定された Www 認証ヘッダーが含まれていることに注意してください。 これは、サーバーがベアラートークンを必要とすることを示します。

## <a name="register-a-user"></a>ユーザーを登録する

アプリの **[登録]** セクションで、電子メールとパスワードを入力し、 **[登録]** ボタンをクリックします。

このサンプルでは有効な電子メールアドレスを使用する必要はありませんが、実際のアプリではアドレスが確認されます。 (「[ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)」を参照してください)。パスワードには、大文字、小文字、数字、英数字以外の文字を含む "Password1!" のようなものを使用します。 アプリを単純にするために、クライアント側の検証を省略しました。そのため、パスワード形式に問題がある場合は、400 (Bad Request) エラーが発生します。

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

**[登録]** ボタンをクリックすると、POST 要求が ~/api/Account/Register/. に送信されます。 要求本文は、名前とパスワードを保持する JSON オブジェクトです。 要求を送信する JavaScript コードを次に示します。

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

HTTP 要求:

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

HTTP 応答:

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

この要求は `AccountController` クラスによって処理されます。 内部的には、`AccountController` は ASP.NET Identity を使用してメンバーシップデータベースを管理します。

アプリを Visual Studio からローカルで実行する場合、ユーザーアカウントは LocalDB の AspNetUsers テーブルに格納されます。 Visual Studio でテーブルを表示するには、 **[表示]** メニューの **[サーバーエクスプローラー]** をクリックし、 **[データ接続]** を展開します。

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>アクセストークンを取得する

これまでは OAuth は実行されていませんでしたが、アクセストークンを要求すると、OAuth 承認サーバーが動作していることがわかります。 サンプルアプリの **[ログイン]** 領域で、電子メールとパスワードを入力し、 **[ログイン]** をクリックします。

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

**[ログイン]** ボタンをクリックすると、要求がトークンエンドポイントに送信されます。 要求の本文には、次の形式の url エンコードされたデータが含まれています。

- grant\_type: "password"
- ユーザー名: ユーザーの電子メール&gt; &lt;
- パスワード: &lt;パスワード&gt;

AJAX 要求を送信する JavaScript コードを次に示します。

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

要求が成功した場合、承認サーバーは応答本文にアクセストークンを返します。 API に要求を送信するときに、後で使用するために、トークンはセッションストレージに格納されていることに注意してください。 一部の認証形式 (cookie ベースの認証など) とは異なり、ブラウザーでは後続の要求にアクセストークンが自動的に含まれません。 アプリケーションは明示的に行う必要があります。 [Csrf の脆弱性](preventing-cross-site-request-forgery-csrf-attacks.md)が制限されるため、これは良いことです。

HTTP 要求:

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

要求にユーザーの資格情報が含まれていることを確認できます。 トランスポート層のセキュリティを提供するには、HTTPS を使用する*必要があり*ます。

HTTP 応答:

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

読みやすくするために、JSON をインデントし、アクセストークンを切り詰めました。これは非常に長いです。

`access_token`、`token_type`、および `expires_in` の各プロパティは、OAuth2 仕様によって定義されます。その他のプロパティ (`userName`、`.issued`、および `.expires`) は単なる情報を提供するためのものです。 これらの追加のプロパティを追加するコードについては、/Providers/ApplicationOAuthProvider.cs ファイルの `TokenEndpoint` メソッドを参照してください。

## <a name="send-an-authenticated-request"></a>認証済みの要求を送信する

ベアラートークンがあるので、API に対して認証された要求を行うことができます。 これを行うには、要求で Authorization ヘッダーを設定します。 このことを確認するには、 **[API の呼び出し]** ボタンをもう一度クリックします。

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

HTTP 要求:

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

HTTP 応答:

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>ログアウト

ブラウザーでは資格情報またはアクセストークンがキャッシュされないため、ログアウトは、セッションストレージからトークンを削除することによって、トークンを "忘れる" だけです。

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>個々のアカウントプロジェクトテンプレートについて

ASP.NET Web アプリケーションプロジェクトテンプレートで**個別のアカウント**を選択すると、プロジェクトには次のものが含まれます。

- OAuth2 承認サーバー。
- ユーザーアカウントを管理するための Web API エンドポイント
- ユーザーアカウントを格納するための EF モデル。

これらの機能を実装する主なアプリケーションクラスを次に示します。

- [https://login.microsoftonline.com/consumers/](`AccountController`) には、ユーザーアカウントを管理するための Web API エンドポイントが用意されています。 このチュートリアルで使用したのは、`Register` アクションだけです。 クラスの他のメソッドは、パスワードのリセット、ソーシャルログイン、およびその他の機能をサポートしています。
- `ApplicationUser`、/Models/IdentityModels.cs. で定義されています。 このクラスは、メンバーシップデータベース内のユーザーアカウントの EF モデルです。
- `ApplicationUserManager`、/\_アプリで定義されています。このクラスは、 [Usermanager](https://msdn.microsoft.com/library/dn613290.aspx)から派生し、ユーザーアカウント (新しいユーザーの作成、パスワードの検証など) に対する操作を実行し、データベースへの変更を自動的に保持します。
- [https://login.microsoftonline.com/consumers/](`ApplicationOAuthProvider`) このオブジェクトは、OWIN ミドルウェアに接続し、ミドルウェアによって発生したイベントを処理します。 [Oauthauthorizationserverprovider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)から派生します。

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>承認サーバーを構成する

StartupAuth.cs では、次のコードで OAuth2 authorization サーバーを構成します。

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

`TokenEndpointPath` プロパティは、承認サーバーエンドポイントへの URL パスです。 これは、アプリがベアラートークンを取得するために使用する URL です。

`Provider` プロパティは、OWIN ミドルウェアに接続するプロバイダーを指定し、ミドルウェアによって発生するイベントを処理します。

アプリでトークンを取得する場合の基本的なフローを次に示します。

1. アクセストークンを取得するために、アプリは ~/tokenに要求を送信します。
2. OAuth ミドルウェアは、プロバイダーの `GrantResourceOwnerCredentials` を呼び出します。
3. プロバイダーは `ApplicationUserManager` を呼び出して資格情報を検証し、クレーム id を作成します。
4. 成功した場合は、トークンの生成に使用される認証チケットがプロバイダーによって作成されます。

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

OAuth ミドルウェアでは、ユーザーアカウントについて何も知られていません。 プロバイダーはミドルウェアと ASP.NET Identity 間で通信します。 承認サーバーの実装の詳細については、「 [OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)」を参照してください。

### <a name="configuring-web-api-to-use-bearer-tokens"></a>ベアラートークンを使用するように Web API を構成する

`WebApiConfig.Register` メソッドでは、次のコードによって Web API パイプラインの認証が設定されます。

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

**Hostauthenticationfilter**クラスは、ベアラートークンを使用した認証を有効にします。

**Config.suppressdefaulthostauthentication**メソッドは、IIS または OWIN ミドルウェアによって、要求が web api パイプラインに到達する前に発生する認証を無視するように web api に指示します。 そのため、ベアラー トークンを使用する場合にのみ認証するように Web API を制限することができます。

> [!NOTE]
> 特に、アプリの MVC 部分では、資格情報を cookie に格納するフォーム認証を使用する場合があります。 Cookie ベースの認証では、CSRF 攻撃を防ぐために、偽造防止トークンを使用する必要があります。 これは web api の場合に問題になります。これは、web API が偽造防止トークンをクライアントに送信するための便利な方法がないためです。 (この問題の背景の詳細については、「 [WEB API での CSRF 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください)。**Config.suppressdefaulthostauthentication**を呼び出すと、cookie に格納されている資格情報から Web API が csrf 攻撃に対して脆弱ではないことが保証されます。

クライアントが保護されたリソースを要求した場合、Web API パイプラインでは次の処理が行われます。

1. **Hostauthentication**フィルターは、OAuth ミドルウェアを呼び出してトークンを検証します。
2. ミドルウェアは、トークンを要求 id に変換します。
3. この時点で、要求は*認証*されていますが*承認*されていません。
4. 承認フィルターは、要求 id を調べます。 要求がそのリソースのユーザーを承認すると、要求は承認されます。 既定では、 **[承認]** 属性は、認証されたすべての要求を承認します。 ただし、ロールまたは他の要求によって承認することができます。 詳細については、「 [WEB API での認証と承認](authentication-and-authorization-in-aspnet-web-api.md)」を参照してください。
5. 前の手順が成功した場合、コントローラーは保護されたリソースを返します。 それ以外の場合、クライアントは 401 (未承認) のエラーを受け取ります。

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>その他のリソース

- [ASP.NET Identity](../../../identity/index.md)
- [VS2013 RC 用の SPA テンプレートのセキュリティ機能について](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)説明します。 Hongye Sun による MSDN ブログ投稿。
- [WEB API の個々のアカウントテンプレートを解説する–パート 2: ローカルアカウント](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。 Dominick Baier によるブログ投稿。
- [OWIN で認証と WEB API をホスト](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)します。 Brock Allen による `SuppressDefaultHostAuthentication` と `HostAuthenticationFilter` についてのよくある説明です。
- [VS 2013 テンプレートでの ASP.NET Identity でのプロファイル情報のカスタマイズ](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。 Pranav Rastogi による MSDN のブログ投稿。
- [ASP.NET Identity の UserManager クラスの要求ごとの有効期間管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。 Suhas Suhas の MSDN ブログ投稿には、`UserManager` クラスの詳細が掲載されています。
