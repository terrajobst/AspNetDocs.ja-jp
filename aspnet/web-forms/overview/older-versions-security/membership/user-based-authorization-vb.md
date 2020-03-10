---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-vb
title: ユーザーベースの承認 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ページへのアクセスを制限し、さまざまな手法によってページレベルの機能を制限する方法について説明します。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: bc937e9d-5c14-4fc4-aec7-440da924dd18
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: dfac0c6fa955e59c6ea996533f2447e89ec8d468
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516376"
---
# <a name="user-based-authorization-vb"></a>ユーザー ベースの承認 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_vb.pdf)

> このチュートリアルでは、ページへのアクセスを制限し、さまざまな手法によってページレベルの機能を制限する方法について説明します。

## <a name="introduction"></a>はじめに

ユーザーアカウントを提供するほとんどの web アプリケーションでは、特定の訪問者がサイト内の特定のページにアクセスできないように制限します。 ほとんどのオンラインの messageboard サイトでは、たとえば、すべてのユーザー (匿名および認証済み) は messageboard の投稿を表示できますが、web ページにアクセスして新しい投稿を作成できるのは、認証されたユーザーのみです。 また、特定のユーザー (または特定のユーザーのセット) だけがアクセスできる管理ページがある場合もあります。 さらに、ページレベルの機能はユーザーごとに異なる場合があります。 投稿の一覧を表示すると、認証されたユーザーには各投稿を評価するためのインターフェイスが表示されますが、このインターフェイスは匿名訪問者には使用できません。

ASP.NET を使用すると、ユーザーベースの承認規則を簡単に定義できます。 `Web.config`の単なるマークアップでは、特定の web ページまたはディレクトリ全体をロックダウンして、指定したユーザーのサブセットだけにアクセスできるようにすることができます。 ページレベルの機能は、現在ログインしているユーザーに基づいて、プログラムおよび宣言的な方法で有効または無効にすることができます。

このチュートリアルでは、ページへのアクセスを制限し、さまざまな手法によってページレベルの機能を制限する方法について説明します。 作業開始

## <a name="a-look-at-the-url-authorization-workflow"></a>URL 承認ワークフローの概要

[ *「フォーム認証の概要*](../introduction/an-overview-of-forms-authentication-vb.md)」のチュートリアルで説明したように、ASP.NET ランタイムが ASP.NET リソースの要求を処理すると、その要求によって、そのライフサイクル中に多数のイベントが発生します。 *HTTP モジュール*は、要求ライフサイクル内の特定のイベントに応答して実行されるコードを持つマネージクラスです。 ASP.NET には、バックグラウンドで重要なタスクを実行する多数の HTTP モジュールが付属しています。

このような HTTP モジュールの1つは[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)です。 前のチュートリアルで説明したように、`FormsAuthenticationModule` の主な機能は、現在の要求の id を特定することです。 これは、cookie に配置されているか、URL 内に埋め込まれているフォーム認証チケットを検査することで実現されます。 この id は[`AuthenticateRequest` イベントの発生](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)時に行われます。

もう1つの重要な HTTP モジュールは、 [`AuthorizeRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)(`AuthenticateRequest` イベントの後に発生する) に応答して発生する[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)です。 `UrlAuthorizationModule` は `Web.config` の構成マークアップを調べて、現在の id に指定されたページにアクセスする権限があるかどうかを判断します。 このプロセスは、 *URL 承認*と呼ばれます。

ここでは、手順 1. の URL 承認規則の構文について説明しますが、まず、要求が承認されているかどうかに応じて、`UrlAuthorizationModule` の動作を見てみましょう。 要求が承認されていることが `UrlAuthorizationModule` によって判断された場合は、何も実行されず、要求はそのライフサイクルを通じて続行されます。 ただし、要求が承認されて*いない*場合、`UrlAuthorizationModule` は、ライフサイクルを中止し、`Response` オブジェクトに対して[HTTP 401 の未承認](http://www.checkupdown.com/status/E401.html)ステータスを返すように指示します。 フォーム認証を使用する場合、この HTTP 401 ステータスはクライアントに返されません。これは、`FormsAuthenticationModule` が HTTP 401 の状態を検出した場合、はログインページに[リダイレクト 302](http://www.checkupdown.com/status/E302.html)されるためです。

図1は、承認されていない要求が到着したときの、ASP.NET パイプライン、`FormsAuthenticationModule`、`UrlAuthorizationModule` のワークフローを示しています。 特に、図1は `ProtectedPage.aspx`の匿名ビジターによる要求を示しています。これは、匿名ユーザーへのアクセスを拒否するページです。 ビジターが匿名であるため、`UrlAuthorizationModule` によって要求が中止され、HTTP 401 の未承認ステータスが返されます。 `FormsAuthenticationModule` は、401の状態を302リダイレクトにログインページに変換します。 ログインページを使用して認証されたユーザーは、`ProtectedPage.aspx`にリダイレクトされます。 今回は、`FormsAuthenticationModule` は自分の認証チケットに基づいてユーザーを識別します。 ビジターが認証されたので、`UrlAuthorizationModule` はページへのアクセスを許可します。

[フォーム認証と URL 承認ワークフローの ![](user-based-authorization-vb/_static/image2.png)](user-based-authorization-vb/_static/image1.png)

**図 1**: フォーム認証と URL 承認のワークフロー ([クリックすると、フルサイズのイメージが表示](user-based-authorization-vb/_static/image3.png)されます)

図1は、匿名ユーザーが匿名ユーザーには使用できないリソースにアクセスしようとしたときに発生する相互作用を示しています。 このような場合、匿名ビジターは、クエリ文字列で指定されたアクセスを試みたページでログインページにリダイレクトされます。 ユーザーが正常にログオンすると、最初に表示しようとしていたリソースに自動的にリダイレクトされます。

匿名ユーザーによって承認されていない要求が行われた場合、このワークフローは簡単であり、ユーザーが何が起こったかとその理由を簡単に把握できます。 ただし、認証されたユーザーによって要求が行われた場合でも、`FormsAuthenticationModule` によって、承認されていないユーザーがログインページ*にリダイレクトさ*れることに注意してください。 認証されたユーザーが権限を持っていないページにアクセスしようとすると、ユーザーエクスペリエンスが混乱する可能性があります。

Web サイトの URL 承認規則が構成されているとします。これにより、ASP.NET ページ `OnlyTito.aspx` が accessibly ではないようになりました。 ここで、Sam がサイトにアクセスし、ログオンして、`OnlyTito.aspx`にアクセスしようとするとします。 `UrlAuthorizationModule` は、要求のライフサイクルを停止し、HTTP 401 の許可されていない状態を返します。この状態は、`FormsAuthenticationModule` が検出し、ログインページに Sam をリダイレクトします。 Sam は既にログインしているため、ログインページに返送された理由を不思議に思うかもしれません。 ログイン資格情報がなんらかの理由で失われたか、または無効な資格情報を入力したことが考えられます。 Sam がログインページから資格情報を入力すると、その資格情報が再度ログオンし、`OnlyTito.aspx`にリダイレクトされます。 `UrlAuthorizationModule` は、Sam がこのページにアクセスできないことを検出し、ログインページに戻ります。

図2は、この混乱を招くワークフローを示しています。

[既定のワークフローを ![と、混乱を招く可能性があります。](user-based-authorization-vb/_static/image5.png)](user-based-authorization-vb/_static/image4.png)

**図 2**: 既定のワークフローが混乱を招く可能性があります ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image6.png)されます)

図2に示されているワークフローを使用すると、コンピューターの知識の高い訪問者でもすぐに befuddle ことができます。 ここでは、手順 2. で混乱を防ぐ方法について説明します。

> [!NOTE]
> ASP.NET は、URL 承認とファイル承認という2つのメカニズムを使用して、現在のユーザーが特定の web ページにアクセスできるかどうかを判断します。 ファイルの承認は[`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)によって実装され、要求されたファイルの acl をコンサルティングすることによって権限を決定します。 Acl は Windows アカウントに適用されるアクセス許可であるため、ファイル承認は Windows 認証で最も一般的に使用されます。 フォーム認証を使用する場合、すべてのオペレーティングシステムとファイルシステムレベルの要求は、サイトにアクセスしているユーザーに関係なく、同じ Windows アカウントによって実行されます。 このチュートリアルシリーズではフォーム認証に焦点を当てているため、ファイル承認については説明しません。

### <a name="the-scope-of-url-authorization"></a>URL 承認のスコープ

`UrlAuthorizationModule` は、ASP.NET ランタイムの一部であるマネージコードです。 Microsoft の[インターネットインフォメーションサービス (iis)](https://www.iis.net/) web サーバーのバージョン7より前では、IIS の HTTP パイプラインと ASP.NET ランタイムのパイプラインの間には個別のバリアがありました。 つまり、IIS 6 以前の ASP では、NET の `UrlAuthorizationModule` は、要求が IIS から ASP.NET ランタイムに委任された場合にのみ実行されます。 既定では、IIS は静的なコンテンツ自体 (HTML ページ、CSS、JavaScript、イメージファイルなど) を処理し、`.aspx`、`.asmx`、または `.ashx` の拡張機能を持つページが要求された場合にのみ、ASP.NET ランタイムに要求を渡します。

ただし、IIS 7 では、IIS と ASP.NET の統合パイプラインを使用できます。 いくつかの構成設定を使用して、IIS 7 をセットアップして*すべて*の要求の `UrlAuthorizationModule` を呼び出すことができます。つまり、URL 承認規則を任意の種類のファイルに対して定義できます。 さらに、IIS 7 には、独自の URL 承認エンジンも含まれています。 ASP.NET 統合と IIS 7 のネイティブ URL 承認機能の詳細については、「 [IIS7 Url 承認につい](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)て」を参照してください。 ASP.NET と IIS 7 の統合の詳細については、Shahram Khosravi の書籍、 *PROFESSIONAL IIS 7、ASP.NET Integrated プログラミング*(ISBN: 978-0470152539) のコピーを参照してください。

簡単に言うと、IIS 7 より前のバージョンでは、URL 承認規則は ASP.NET ランタイムによって処理されるリソースにのみ適用されます。 ただし、IIS 7 では、IIS のネイティブ URL 承認機能を使用することも、ASP を統合することもできます。NET は IIS の HTTP パイプラインに `UrlAuthorizationModule` し、この機能をすべての要求に拡張します。

> [!NOTE]
> ASP の方法には、いくつかの重要な相違点があります。NET の `UrlAuthorizationModule` および IIS 7 の URL 承認機能によって、承認規則が処理されます。 このチュートリアルでは、IIS 7 の URL 承認機能や、`UrlAuthorizationModule`と比較して承認規則を解析する方法の違いについては説明しません。 これらのトピックの詳細については、MSDN または[www.iis.net](https://www.iis.net/)の IIS 7 のドキュメントを参照してください。

## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>手順 1:`Web.config` で URL 承認規則を定義する

`UrlAuthorizationModule` は、アプリケーションの構成で定義されている URL 承認規則に基づいて、特定の id に対して要求されたリソースへのアクセスを許可するか拒否するかを決定します。 承認規則は、`<allow>` と `<deny>` の子要素の形式で[`<authorization>` 要素](https://msdn.microsoft.com/library/8d82143t.aspx)に記載されています。 各 `<allow>` および `<deny>` 子要素は、次の項目を指定できます。

- 特定のユーザー
- コンマで区切られたユーザーの一覧
- すべての匿名ユーザー (疑問符 (?) で示される)
- アスタリスク (\*) で示されるすべてのユーザー

次のマークアップは、URL 承認規則を使用して、ユーザーに Tito と Scott を許可し、他のすべての操作を拒否できるようにする方法を示しています。

[!code-xml[Main](user-based-authorization-vb/samples/sample1.xml)]

`<allow>` 要素は、ユーザーが許可されているユーザー (Tito と Scott-) を定義します。一方、`<deny>` 要素は、*すべて*のユーザーを拒否するように指示します。

> [!NOTE]
> `<allow>` 要素と `<deny>` 要素では、ロールの承認規則を指定することもできます。 ロールベースの承認については、今後のチュートリアルで確認します。

次の設定は、Sam 以外のユーザー (匿名訪問者を含む) へのアクセスを許可します。

[!code-xml[Main](user-based-authorization-vb/samples/sample2.xml)]

認証されたユーザーのみを許可するには、次の構成を使用します。これにより、すべての匿名ユーザーへのアクセスが拒否されます。

[!code-xml[Main](user-based-authorization-vb/samples/sample3.xml)]

承認規則は `Web.config` の `<system.web>` 要素内で定義され、web アプリケーション内のすべての ASP.NET リソースに適用されます。 多くの場合、アプリケーションには異なるセクションに対して異なる承認規則があります。 たとえば、e コマースサイトでは、すべての訪問者が製品を調べたり、製品レビューを参照したり、カタログを検索したりすることができます。 ただし、認証されたユーザーのみがチェックアウトに到着したり、1つの出荷履歴を管理するためのページが表示されたりする可能性があります。 また、サイトの一部が、サイト管理者などの選択したユーザーのみがアクセスできるようになる場合もあります。

ASP.NET を使用すると、サイト内のさまざまなファイルやフォルダーに対して異なる承認規則を簡単に定義できます。 ルートフォルダーの `Web.config` ファイルに指定されている承認規則は、サイト内のすべての ASP.NET リソースに適用されます。 ただし、これらの既定の承認設定は、`<authorization>` セクションを持つ `Web.config` を追加することで、特定のフォルダーに対してオーバーライドできます。

認証されたユーザーのみが `Membership` フォルダー内の ASP.NET ページにアクセスできるように web サイトを更新してみましょう。 これを行うには、`Membership` フォルダーに `Web.config` ファイルを追加し、その承認設定を匿名ユーザーを拒否するように設定する必要があります。 ソリューションエクスプローラーで `Membership` フォルダーを右クリックし、コンテキストメニューの [新しい項目の追加] メニューをクリックして、`Web.config`という名前の新しい Web 構成ファイルを追加します。

[メンバーシップフォルダーに web.config ファイルを追加 ![には](user-based-authorization-vb/_static/image8.png)](user-based-authorization-vb/_static/image7.png)

**図 3**: `Membership` フォルダーに `Web.config` ファイルを追加する ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image9.png)されます)

この時点で、プロジェクトには2つの `Web.config` ファイルが含まれている必要があります。1つはルートディレクトリに、もう1つは `Membership` フォルダーにあります。

[アプリケーションに2つの web.config ファイルが含まれるようになった ![](user-based-authorization-vb/_static/image11.png)](user-based-authorization-vb/_static/image10.png)

**図 4**: アプリケーションに2つの `Web.config` ファイルが含まれるようにする ([クリックしてフルサイズのイメージを表示する](user-based-authorization-vb/_static/image12.png))

`Membership` フォルダー内の構成ファイルを更新して、匿名ユーザーへのアクセスを禁止します。

[!code-xml[Main](user-based-authorization-vb/samples/sample4.xml)]

これですべて完了です。

この変更をテストするには、ブラウザーでホームページにアクセスし、ログアウトしていることを確認してください。ASP.NET アプリケーションの既定の動作ではすべての訪問者が許可されるため、ルートディレクトリの `Web.config` ファイルに対して承認を変更しなかったため、ルートディレクトリ内のファイルに匿名ビジターとしてアクセスできるようになります。

左側の列にある [ユーザーアカウントの作成] リンクをクリックします。 これにより、`~/Membership/CreatingUserAccounts.aspx`に移動します。 `Membership` フォルダー内の `Web.config` ファイルでは、匿名アクセスを禁止する承認規則が定義されているため、`UrlAuthorizationModule` は要求を中止し、HTTP 401 の未承認ステータスを返します。 `FormsAuthenticationModule` はこれを302リダイレクトステータスに変更し、ログインページに送信します。 アクセスしようとしていたページ (`CreatingUserAccounts.aspx`) は、`ReturnUrl` querystring パラメーターを使用してログインページに渡されることに注意してください。

[![URL 承認規則によって匿名アクセスが禁止されているため、ログインページにリダイレクトされます](user-based-authorization-vb/_static/image14.png)](user-based-authorization-vb/_static/image13.png)

**図 5**: URL 承認規則によって匿名アクセスが禁止されているため、ログインページにリダイレクトされます ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image15.png)されます)

ログインに成功すると、`CreatingUserAccounts.aspx` ページにリダイレクトされます。 今回は、匿名ではなくなったため、`UrlAuthorizationModule` がページへのアクセスを許可します。

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>特定の場所への URL 承認規則の適用

`Web.config` の `<system.web>` セクションで定義されている承認設定は、そのディレクトリとそのサブディレクトリ内のすべての ASP.NET リソース (他の `Web.config` ファイルによってオーバーライドされるまで) に適用されます。 ただし、場合によっては、特定のディレクトリ内のすべての ASP.NET リソースに特定の承認構成が必要になることがあります (1 つまたは2つの特定のページを除く)。 これを実現するには、`Web.config`に `<location>` 要素を追加し、承認規則が異なるファイルを参照して、その固有の承認規則を定義します。

`<location>` 要素を使用して特定のリソースの構成設定を上書きする方法を示すために、承認設定をカスタマイズして、Tito が `CreatingUserAccounts.aspx`にアクセスできるようにします。 これを行うには、`Membership` フォルダーの `Web.config` ファイルに `<location>` 要素を追加し、次のようにマークアップを更新します。

[!code-xml[Main](user-based-authorization-vb/samples/sample5.xml)]

`<system.web>` の `<authorization>` 要素は、`Membership` フォルダーとそのサブフォルダー内の ASP.NET リソースに対する既定の URL 承認規則を定義します。 `<location>` 要素を使用すると、特定のリソースに対してこれらのルールをオーバーライドできます。 上のマークアップでは、`<location>` 要素は `CreatingUserAccounts.aspx` ページを参照し、などの承認規則を指定して Tito を許可し、他のすべてのユーザーを拒否します。

この承認変更をテストするには、まず、匿名ユーザーとして web サイトにアクセスします。 `UserBasedAuthorization.aspx`など、`Membership` フォルダー内のページにアクセスしようとすると、`UrlAuthorizationModule` によって要求が拒否され、ログインページにリダイレクトされます。 Scott などとしてログインした後、`Membership` フォルダー内の任意のページにアクセスできます (`CreatingUserAccounts.aspx`を*除く*)。 `CreatingUserAccounts.aspx` ログオンしようとすると、不正なアクセスが試行され、ログインページにリダイレクトされます。

> [!NOTE]
> `<location>` 要素は、構成の `<system.web>` 要素の外に置く必要があります。 承認設定を上書きするリソースごとに個別の `<location>` 要素を使用する必要があります。

### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>`UrlAuthorizationModule`が承認規則を使用してアクセスを許可または拒否する方法を確認する

`UrlAuthorizationModule` は、1つの URL 承認規則を1つずつ分析して、特定の URL の特定の id を承認するかどうかを決定します。 一致が見つかるとすぐに、`<allow>` または `<deny>` 要素で一致が見つかったかどうかによって、ユーザーはアクセスを許可または拒否されます。 <strong>一致するものが見つからない場合は、ユーザーにアクセス権が付与されます。</strong> そのため、アクセスを制限する場合は、URL 承認構成の最後の要素として `<deny>` 要素を使用する必要があります。 `<deny>`要素を<strong>省略すると</strong> <strong>、すべてのユーザーにアクセス権が付与されます。</strong>

`UrlAuthorizationModule` が使用するプロセスについて理解を深めるには、この手順の前半で説明した URL 承認規則の例を参照してください。 最初の規則は、Tito と Scott へのアクセスを許可する `<allow>` 要素です。 2番目の規則は、すべてのユーザーへのアクセスを拒否する `<deny>` 要素です。 匿名ユーザーがアクセスした場合、`UrlAuthorizationModule` は、Scott または Tito に匿名であるかどうかを確認してから開始しますか? もちろん、答えは「いいえ」であるため、2番目のルールに進みます。 全員が匿名であるか。 ここでの答えは "はい" であるため、`<deny>` の規則は有効になり、ビジターはログインページにリダイレクトされます。 同様に、Jisun がアクセスしている場合は、`UrlAuthorizationModule`、Jisun は Scott または Tito ですか。 私はそうではないので、`UrlAuthorizationModule` は2番目の質問に進みます。 アクセスは拒否されています。 最後に、アクセスする場合は、`UrlAuthorizationModule` によって最初に行われる質問が肯定的な回答であるため、Tito にはアクセス権が付与されます。

`UrlAuthorizationModule` は、上から順に承認規則を処理するので、すべての一致を停止します。そのため、より具体的な規則よりも具体的な規則を指定することが重要です。 つまり、Jisun と匿名ユーザーを禁止し、他のすべての認証済みユーザーを許可する承認規則を定義するには、最も限定的な規則から開始します (Jisun に影響を与える規則と、それ以外の規則を許可する規則に従います)。認証されたユーザー。ただし、すべての匿名ユーザーを拒否します。 次の URL 承認規則では、最初に Jisun を拒否し、匿名ユーザーを拒否することによって、このポリシーを実装します。 Jisun 以外の認証されたユーザーには、これらの `<deny>` ステートメントのどちらも一致しないため、アクセスが許可されます。

[!code-xml[Main](user-based-authorization-vb/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>手順 2: 承認されていない認証済みユーザーのワークフローを修正する

このチュートリアルで既に説明したように、「URL Authorization Workflow」セクションでは、承認されていない要求を発生するたびに、要求が中止され、HTTP 401 `UrlAuthorizationModule` の未承認ステータスが返されます。 この401状態は、`FormsAuthenticationModule` によって、ユーザーをログインページに送信する302リダイレクトステータスに変更されます。 このワークフローは、ユーザーが認証されている場合でも、承認されていない要求に対して発生します。

認証されたユーザーをログインページに返すことは、システムに既にログインしているため、ユーザーが混乱する可能性があります。 少しの作業で、承認されていない要求を行う認証済みユーザーを、制限されたページにアクセスしようとしたことを示すページにリダイレクトすることで、このワークフローを改善できます。

まず、`UnauthorizedAccess.aspx`という名前の web アプリケーションのルートフォルダーに新しい ASP.NET ページを作成します。このページを `Site.master` マスターページに必ず関連付けるようにしてください。 このページを作成した後、マスターページの既定のコンテンツが表示されるように、`LoginContent` ContentPlaceHolder を参照するコンテンツコントロールを削除します。 次に、状況を説明するメッセージを追加します。つまり、ユーザーが保護されたリソースにアクセスしようとしたことを示します。 このようなメッセージを追加すると、`UnauthorizedAccess.aspx` ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](user-based-authorization-vb/samples/sample7.aspx)]

次に、認証されたユーザーによって承認されていない要求が実行されると、ログインページではなく `UnauthorizedAccess.aspx` ページに送信されるように、ワークフローを変更する必要があります。 ログインページに承認されていない要求をリダイレクトするロジックは、`FormsAuthenticationModule` クラスのプライベートメソッド内に埋もれているので、この動作をカスタマイズすることはできません。 ただし、必要に応じて、ユーザーを `UnauthorizedAccess.aspx`にリダイレクトするログインページに独自のロジックを追加することもできます。

`FormsAuthenticationModule` が権限のないユーザーをログインページにリダイレクトすると、要求された承認されていない URL が `ReturnUrl`という名前のクエリ文字列に追加されます。 たとえば、承認されていないユーザーが `OnlyTito.aspx`にアクセスしようとすると、`FormsAuthenticationModule` によって `Login.aspx?ReturnUrl=OnlyTito.aspx`にリダイレクトされます。 したがって、認証されたユーザーが `ReturnUrl` パラメーターを含むクエリ文字列を使用してログインページに到達した場合は、この認証されていないユーザーが閲覧を許可されていないページにアクセスしようとしただけであることがわかります。 このような場合は、`UnauthorizedAccess.aspx`にリダイレクトする必要があります。

これを実現するには、ログインページの `Page_Load` イベントハンドラーに次のコードを追加します。

[!code-vb[Main](user-based-authorization-vb/samples/sample8.vb)]

上記のコードは、認証された承認されていないユーザーを `UnauthorizedAccess.aspx` ページにリダイレクトします。 このロジックが動作していることを確認するには、匿名ビジターとしてサイトにアクセスし、左側の列にある [ユーザーアカウントの作成] リンクをクリックします。 これにより、[`~/Membership/CreatingUserAccounts.aspx`] ページに移動します。手順 1. では、Tito へのアクセスのみを許可するように構成されています。 匿名ユーザーは禁止されているため、`FormsAuthenticationModule` はログインページにリダイレクトします。

この時点では匿名であるため、`Request.IsAuthenticated` は `False` を返し、`UnauthorizedAccess.aspx`にはリダイレクトされません。 代わりに、ログインページが表示されます。 たとえば、Tito 以外のユーザーとしてログインします。 適切な資格情報を入力すると、ログインページが `~/Membership/CreatingUserAccounts.aspx`にリダイレクトされます。 ただし、このページにアクセスできるのは Tito だけなので、このページを表示する権限はありませんので、すぐにログインページに戻ります。 ただし、今度は `Request.IsAuthenticated` が返され `True` (と `ReturnUrl` querystring パラメーターが存在する) ため、`UnauthorizedAccess.aspx` ページにリダイレクトされます。

[認証され ![認証されていないユーザーは、UnauthorizedAccess .aspx にリダイレクトされます。](user-based-authorization-vb/_static/image17.png)](user-based-authorization-vb/_static/image16.png)

**図 6**: 認証された承認されていないユーザーが `UnauthorizedAccess.aspx` にリダイレクトされる ([クリックしてフルサイズの画像を表示する](user-based-authorization-vb/_static/image18.png))

このカスタマイズされたワークフローは、図2に示すサイクルを簡単に示すことで、より合理的でわかりやすいユーザーエクスペリエンスを提供します。

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>手順 3: 現在ログインしているユーザーに基づいて機能を制限する

URL 承認を使用すると、粒度の粗い承認規則を簡単に指定できます。 手順 1. で説明したように、URL 承認を使用すると、許可される id と、フォルダー内の特定のページまたはすべてのページを表示する際に拒否される id を簡潔に把握できます。 ただし、特定のシナリオでは、すべてのユーザーがページにアクセスできるようにする必要がありますが、ページにアクセスするユーザーに基づいてページの機能を制限することもできます。

認証された訪問者が製品をレビューできる e コマース web サイトのケースを考えてみましょう。 匿名ユーザーが製品のページにアクセスすると、製品情報だけが表示され、レビューを終了する機会は与えられません。 ただし、認証されたユーザーが同じページにアクセスすると、[確認] インターフェイスが表示されます。 認証されたユーザーがこの製品をまだ確認していない場合、インターフェイスによってレビューを送信できるようになります。それ以外の場合は、以前に送信したレビューが表示されます。 このシナリオをさらに進めるために、製品ページには追加情報が記載されています。また、e コマース会社で利用できるユーザーのための拡張機能を提供しています。 たとえば、製品ページに在庫の一覧が表示され、従業員がアクセスしたときに製品の価格と説明を編集するためのオプションが含まれている場合があります。

このような細かい粒度の承認規則は、宣言によって、またはプログラムによって (または2つの組み合わせを使用して) 実装できます。 次のセクションでは、LoginView コントロールを使用して細かい粒度承認を実装する方法について説明します。 次に、プログラムによる手法について説明します。 ただし、綿密な粒度の承認規則の適用を確認する前に、まず、アクセスするユーザーによって機能が異なるページを作成する必要があります。

GridView 内の特定のディレクトリ内のファイルを一覧表示するページを作成してみましょう。 GridView には、各ファイルの名前、サイズ、およびその他の情報を一覧表示すると共に、リンクボタンの2つの列が含まれます。1つはタイトル付きビューで、もう1つは Delete というタイトルです。 ビュー LinkButton がクリックされると、選択したファイルの内容が表示されます。Delete LinkButton がクリックされると、ファイルは削除されます。 最初にこのページを作成して、すべてのユーザーがそのビューおよび削除機能を使用できるようにしましょう。 「LoginView コントロールの使用」および「プログラムによる機能の制限」では、ページにアクセスしているユーザーに基づいてこれらの機能を有効または無効にする方法について説明します。

> [!NOTE]
> ビルドしようとしている ASP.NET ページでは、GridView コントロールを使用してファイルの一覧を表示します。 このチュートリアルシリーズでは、フォーム認証、承認、ユーザーアカウント、およびロールに焦点を当てているため、GridView コントロールの内部動作についてはあまり時間をかけたくありません。 このチュートリアルでは、このページを設定するための具体的な手順について説明しますが、特定の選択が行われた理由や、レンダリングされた出力に対する特定のプロパティの影響については詳しく説明しません。 GridView コントロールの詳細な調査については、「 *[ASP.NET 2.0 チュートリアルシリーズのデータの操作」](../../data-access/index.md)* を参照してください。

まず、`Membership` フォルダー内の `UserBasedAuthorization.aspx` ファイルを開いて、`FilesGrid`という名前のページに GridView コントロールを追加します。 GridView のスマートタグから、[列の編集] リンクをクリックして [フィールド] ダイアログボックスを開きます。 ここで、左下隅にある [フィールドの自動生成] チェックボックスをオフにします。 次に、左上隅にある [選択] ボタン、[削除] ボタン、および2つの連結フィールドを追加します ([選択] ボタンと [削除] ボタンは CommandField 型の下にあります)。 [選択] ボタンの `SelectText` プロパティを [表示] に設定し、最初の BoundField の `HeaderText` と [`DataField` のプロパティ] を [名前] に設定します。 2番目の BoundField の `HeaderText` プロパティをバイト単位のサイズに設定し、その `DataField` プロパティを長さに、その `DataFormatString` プロパティを {0:N0} に設定し、その `HtmlEncode` プロパティを False に設定します。

GridView の列を構成したら、[OK] をクリックして [フィールド] ダイアログボックスを閉じます。 プロパティウィンドウから、GridView の `DataKeyNames` プロパティを `FullName`に設定します。 この時点で、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](user-based-authorization-vb/samples/sample9.aspx)]

GridView のマークアップを作成したら、特定のディレクトリにあるファイルを取得して GridView にバインドするコードを記述する準備ができました。 ページの `Page_Load` イベントハンドラーに次のコードを追加します。

[!code-vb[Main](user-based-authorization-vb/samples/sample10.vb)]

上記のコードでは、 [`DirectoryInfo` クラス](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx)を使用して、アプリケーションのルートフォルダー内のファイルの一覧を取得します。 [`GetFiles()` メソッド](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx)は、ディレクトリ内のすべてのファイルを[`FileInfo` オブジェクト](https://msdn.microsoft.com/library/system.io.fileinfo.aspx)の配列として返します。このオブジェクトは、GridView にバインドされます。 `FileInfo` オブジェクトには、`Name`、`Length`、`IsReadOnly`など、さまざまなプロパティがあります。 宣言型マークアップからわかるように、GridView には `Name` と `Length` のプロパティだけが表示されます。

> [!NOTE]
> `DirectoryInfo` クラスと `FileInfo` クラスは、 [`System.IO` 名前空間](https://msdn.microsoft.com/library/system.io.aspx)にあります。 したがって、これらのクラス名の先頭には名前空間名を付けるか、または名前空間をクラスファイルにインポートする必要があります (`Imports System.IO`)。

ブラウザーを使用してこのページにアクセスしてください。 これにより、アプリケーションのルートディレクトリに存在するファイルの一覧が表示されます。 ビューまたは削除リンクボタンのいずれかをクリックするとポストバックが発生しますが、必要なイベントハンドラーをまだ作成していないため、アクションは発生しません。

[GridView に ![、Web アプリケーションのルートディレクトリにあるファイルが一覧表示されます。](user-based-authorization-vb/_static/image20.png)](user-based-authorization-vb/_static/image19.png)

**図 7**: GridView によって、Web アプリケーションのルートディレクトリ内のファイルが一覧表示されます ([クリックすると、フルサイズのイメージが表示](user-based-authorization-vb/_static/image21.png)されます)

選択したファイルの内容を表示するための手段が必要です。 Visual Studio に戻り、GridView の上に `FileContents` という名前のテキストボックスを追加します。 `TextMode` プロパティを `MultiLine` に設定し、`Columns` と `Rows` プロパティをそれぞれ95% と10に設定します。

[!code-aspx[Main](user-based-authorization-vb/samples/sample11.aspx)]

次に、GridView の[`SelectedIndexChanged` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx)のイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](user-based-authorization-vb/samples/sample12.vb)]

このコードでは、GridView の `SelectedValue` プロパティを使用して、選択したファイルの完全なファイル名を確認します。 内部的には、`SelectedValue`を取得するために `DataKeys` コレクションが参照されているため、この手順の前半で説明したように、GridView の `DataKeyNames` プロパティを Name に設定する必要があります。 [`File` クラス](https://msdn.microsoft.com/library/system.io.file.aspx)は、選択したファイルの内容を文字列に読み取るために使用されます。この文字列は、`FileContents` テキストボックスの `Text` プロパティに割り当てられます。これにより、選択したファイルの内容がページ上に表示されます。

[選択したファイルの内容をテキストボックスに表示 ![](user-based-authorization-vb/_static/image23.png)](user-based-authorization-vb/_static/image22.png)

**図 8**: 選択したファイルの内容がテキストボックスに表示される ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image24.png)されます)

> [!NOTE]
> HTML マークアップが含まれているファイルの内容を表示し、ファイルを表示または削除しようとすると、`HttpRequestValidationException` エラーが表示されます。 これは、ポストバック時に TextBox の内容が web サーバーに送り返されるためです。 既定では、HTML マークアップなどの危険なポストバックコンテンツが検出されると、ASP.NET は `HttpRequestValidationException` エラーを発生させます。 このエラーが発生しないようにするには、`@Page` ディレクティブに `ValidateRequest="false"` を追加して、ページの要求の検証を無効にします。 要求の検証の利点と、それを無効にするときに行う必要がある対策の詳細については、「[要求の検証-スクリプト攻撃の防止](https://asp.net/learn/whitepapers/request-validation/)」を参照してください。

最後に、GridView の[`RowDeleting` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)の次のコードを使用して、イベントハンドラーを追加します。

[!code-vb[Main](user-based-authorization-vb/samples/sample13.vb)]

このコードは、ファイルを実際に削除する*ことなく*、`FileContents` テキストボックスで削除するファイルの完全な名前を表示するだけです。

[[削除] ボタンをクリックしても、ファイルは実際には削除されません ![](user-based-authorization-vb/_static/image26.png)](user-based-authorization-vb/_static/image25.png)

**図 9**: [削除] ボタンをクリックしてもファイルが削除されない ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image27.png)されます)

手順1では、匿名ユーザーが `Membership` フォルダー内のページを表示できないように、URL 承認規則を構成しました。 きめ細かな認証をより適切に行うために、匿名ユーザーが `UserBasedAuthorization.aspx` ページにアクセスできるようにしますが、機能は制限されています。 すべてのユーザーがアクセスできるようにこのページを開くには、次の `<location>` 要素を `Membership` フォルダー内の `Web.config` ファイルに追加します。

[!code-xml[Main](user-based-authorization-vb/samples/sample14.xml)]

この `<location>` 要素を追加した後、サイトからログアウトして、新しい URL 承認規則をテストします。 匿名ユーザーは、`UserBasedAuthorization.aspx` ページにアクセスすることが許可されている必要があります。

現在、認証されたユーザーまたは匿名ユーザーは、`UserBasedAuthorization.aspx` ページにアクセスして、ファイルを表示または削除できます。 認証されたユーザーのみがファイルの内容を表示できるようにし、ファイルを削除できるのは Tito です。 このような細かい粒度の承認規則は、プログラムによって、または両方の方法を組み合わせて適用できます。 宣言型の方法を使用して、ファイルの内容を表示できるユーザーを制限してみましょう。プログラムによる方法を使用して、ファイルを削除できるユーザーを制限します。

### <a name="using-the-loginview-control"></a>LoginView コントロールの使用

これまでのチュートリアルで説明したように、LoginView コントロールは、認証されたユーザーと匿名ユーザー用にさまざまなインターフェイスを表示する場合に便利です。また、匿名ユーザーがアクセスできない機能を簡単に隠すことができます。 匿名ユーザーがファイルを表示または削除することはできないため、認証されたユーザーがページにアクセスしたときにのみ、`FileContents` テキストボックスを表示する必要があります。 これを実現するには、LoginView コントロールをページに追加し `LoginViewForFileContentsTextBox`という名前を指定し、`FileContents` TextBox の宣言型マークアップを LoginView コントロールの `LoggedInTemplate`に移動します。

[!code-aspx[Main](user-based-authorization-vb/samples/sample15.aspx)]

LoginView のテンプレート内の Web コントロールは、分離コードクラスから直接アクセスできなくなりました。 たとえば、`FilesGrid` GridView の `SelectedIndexChanged` および `RowDeleting` イベントハンドラーは、現在、次のようなコードを使用して `FileContents` TextBox コントロールを参照します。

[!code-aspx[Main](user-based-authorization-vb/samples/sample16.aspx)]

ただし、このコードは有効ではなくなりました。 `FileContents` TextBox を `LoggedInTemplate` に移動すると、テキストボックスに直接アクセスできなくなります。 代わりに、`FindControl("controlId")` メソッドを使用して、プログラムでコントロールを参照する必要があります。 次のように、テキストボックスを参照するように `FilesGrid` イベントハンドラーを更新します。

[!code-vb[Main](user-based-authorization-vb/samples/sample17.vb)]

TextBox を LoginView の `LoggedInTemplate` に移動し、`FindControl("controlId")` パターンを使用してテキストボックスを参照するようにページのコードを更新した後は、匿名ユーザーとしてページにアクセスします。 図10に示すように、[`FileContents`] ボックスは表示されません。 ただし、ビュー LinkButton は引き続き表示されます。

[LoginView コントロールでは、認証されたユーザーの FileContents TextBox のみがレンダリングされます。 ![](user-based-authorization-vb/_static/image29.png)](user-based-authorization-vb/_static/image28.png)

**図 10**: LoginView コントロールでは、認証されたユーザーの `FileContents` テキストボックスのみがレンダリングされます ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image30.png)されます)

匿名ユーザーの [表示] ボタンを非表示にする方法の1つとして、GridView フィールドを TemplateField に変換する方法があります。 これにより、ビュー LinkButton の宣言型マークアップを含むテンプレートが生成されます。 次に、LoginView コントロールを TemplateField に追加し、LoginView の `LoggedInTemplate`内に LinkButton を配置します。これにより、匿名訪問者から表示ボタンが非表示になります。 これを行うには、GridView のスマートタグから [列の編集] リンクをクリックして、[フィールド] ダイアログボックスを起動します。 次に、左下隅にある一覧から [選択] ボタンを選択し、[このフィールドを TemplateField に変換する] リンクをクリックします。 これにより、次のようにフィールドの宣言マークアップが変更されます。

[!code-aspx[Main](user-based-authorization-vb/samples/sample18.aspx)]

 変更後: 

[!code-aspx[Main](user-based-authorization-vb/samples/sample19.aspx)]

 この時点で、TemplateField に LoginView を追加できます。 次のマークアップは、認証されたユーザーに対してのみビュー LinkButton を表示します。 

[!code-aspx[Main](user-based-authorization-vb/samples/sample20.aspx)]

図11に示すように、最終的な結果は、列内のビューリンクボタンが非表示になっていても、ビュー列が引き続き表示されるという点ではありません。 次のセクションでは、(LinkButton だけでなく) GridView 列全体を非表示にする方法について説明します。

[LoginView コントロールを ![すると、匿名訪問者のビューリンクボタンが非表示になります。](user-based-authorization-vb/_static/image32.png)](user-based-authorization-vb/_static/image31.png)

**図 11**: LoginView コントロールは、匿名の訪問者のビューリンクボタンを非表示にします ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image33.png)されます)

### <a name="programmatically-limiting-functionality"></a>プログラムによる機能制限

場合によっては、ページに機能を制限するための宣言型手法が不十分です。 たとえば、ページにアクセスするユーザーが匿名または認証されているかどうかに関係なく、特定のページ機能の可用性が条件に依存している場合があります。 このような場合は、プログラムによって、さまざまなユーザーインターフェイス要素を表示または非表示にすることができます。

プログラムによって機能を制限するために、次の2つのタスクを実行する必要があります。

1. ページにアクセスしているユーザーが機能にアクセスできるかどうかを判断します。
2. ユーザーが問題の機能にアクセスできるかどうかに基づいて、プログラムによってユーザーインターフェイスを変更します。

これらの2つのタスクの適用を示すために、GridView からのファイルの削除のみを許可してみましょう。 最初のタスクは、ページにアクセスする必要があるかどうかを判断することです。 確認したら、GridView の Delete 列を非表示 (または表示) する必要があります。 GridView の列には、`Columns` プロパティを使用してアクセスできます。列が表示されるのは、その `Visible` プロパティが `True` (既定値) に設定されている場合のみです。

データを GridView にバインドする前に、`Page_Load` イベントハンドラーに次のコードを追加します。

[!code-vb[Main](user-based-authorization-vb/samples/sample21.vb)]

[ *「フォーム認証の概要」* ](../introduction/an-overview-of-forms-authentication-vb.md)チュートリアルで説明したように、`User.Identity.Name` は id の名前を返します。 これは、ログインコントロールに入力されたユーザー名に対応します。 ページにアクセスする必要がある場合、GridView の2番目の列の `Visible` プロパティは `True`に設定されます。それ以外の場合は、`False`に設定されます。 結果として、他のユーザーがページにアクセスしたときに、別の認証済みユーザーまたは匿名ユーザーのいずれかが表示されない場合、削除列はレンダリングされません (図12を参照)。ただし、このページにアクセスするときは、[削除] 列が表示されます (図13を参照)。

[[削除] 列が Tito 以外のユーザーによって閲覧されたときにはレンダリングされません (例 ![)。](user-based-authorization-vb/_static/image35.png)](user-based-authorization-vb/_static/image34.png)

**図 12**: [削除] 列が Tito 以外のユーザーによって閲覧されたときに表示されない (たとえば、[クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image36.png)されます)

[削除列が Tito に表示さ ![](user-based-authorization-vb/_static/image38.png)](user-based-authorization-vb/_static/image37.png)

**図 13**: Delete 列が Tito に表示される ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image39.png)されます)

## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>手順 4: クラスとメソッドに承認規則を適用する

手順3では、匿名ユーザーがファイルの内容を表示できないようにし、すべてのユーザーがファイルを削除することを禁止しています。 これは、認証されていない訪問者に関連付けられたユーザーインターフェイス要素を、宣言型およびプログラムによって非表示にすることによって実現 単純な例では、ユーザーインターフェイス要素を適切に非表示にするのは簡単ですが、同じ機能を実行するためのさまざまな方法がある複雑なサイトについてはどうでしょうか。 この機能を承認されていないユーザーに制限する際、適用可能なすべてのユーザーインターフェイス要素を非表示にしたり、無効にしたりした場合はどうなりますか。

権限のないユーザーが特定の機能にアクセスできないようにする簡単な方法は、そのクラスまたはメソッドを[`PrincipalPermission` 属性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)で修飾することです。 .NET ランタイムでクラスを使用する場合、またはメソッドのいずれかを実行する場合は、現在のセキュリティコンテキストにクラスを使用するか、メソッドを実行するアクセス許可があるかどうかがチェックされます。 `PrincipalPermission` 属性は、これらの規則を定義できるメカニズムを提供します。

GridView の `SelectedIndexChanged` および `RowDeleting` イベントハンドラーの `PrincipalPermission` 属性を使用して、Tito 以外の匿名ユーザーとユーザーによる実行を禁止する方法を説明します。 それぞれの関数定義の上に適切な属性を追加するだけで十分です。

[!code-vb[Main](user-based-authorization-vb/samples/sample22.vb)]

`SelectedIndexChanged` イベントハンドラーの属性は、認証されたユーザーのみがイベントハンドラーを実行できることを指定します。この場合、`RowDeleting` イベントハンドラーの属性によって実行が Tito に制限されます。

> [!NOTE]
> 属性は、クラス、メソッド、プロパティ、またはイベントに適用できます。 属性を追加するときは、クラス、メソッド、プロパティ、またはイベント宣言ステートメントの一部である必要があります。 Visual Basic では、ステートメントの区切り記号として改行を使用するため、属性は宣言と同じ行に記述するか、または行連結文字 (アンダースコア) で直接指定する必要があります。 上記のコードスニペットでは、行連結文字を使用して、属性を1行に、メソッド宣言を別の行に配置しています。

場合によっては、Tito 以外のユーザーが `RowDeleting` イベントハンドラーを実行しようとするか、認証されていないユーザーが `SelectedIndexChanged` イベントハンドラーを実行しようとすると、.NET ランタイムによって `SecurityException`が発生します。

[![、セキュリティコンテキストにメソッドの実行が許可されていない場合は、SecurityException がスローされます。](user-based-authorization-vb/_static/image41.png)](user-based-authorization-vb/_static/image40.png)

**図 14**: セキュリティコンテキストにメソッドの実行が許可されていない場合は、`SecurityException` がスローされます ([クリックすると、フルサイズの画像が表示](user-based-authorization-vb/_static/image42.png)されます)

> [!NOTE]
> 複数のセキュリティコンテキストでクラスまたはメソッドにアクセスできるようにするには、各セキュリティコンテキストの `PrincipalPermission` 属性を使用して、クラスまたはメソッドを装飾します。 つまり、Tito と `RowDeleting` の両方のイベントハンドラーを実行できるようにするには、次の*2 つ*の `PrincipalPermission` 属性を追加します。

[!code-vb[Main](user-based-authorization-vb/samples/sample23.vb)]

ASP.NET ページに加えて、多くのアプリケーションには、ビジネスロジックやデータアクセス層などのさまざまなレイヤーを含むアーキテクチャもあります。 これらのレイヤーは、通常、クラスライブラリとして実装され、ビジネスロジックおよびデータに関連する機能を実行するためのクラスとメソッドを提供します。 `PrincipalPermission` 属性は、これらのレイヤーに承認規則を適用する場合に便利です。

`PrincipalPermission` 属性を使用してクラスとメソッドの承認規則を定義する方法の詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログ記事「 [`PrincipalPermissionAttributes`を使用したビジネス層およびデータ層への承認規則の追加](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)」を参照してください。

## <a name="summary"></a>まとめ

このチュートリアルでは、ユーザーベースの承認規則を適用する方法を説明しました。 ASP の概要について説明しました。NET の URL 承認フレームワーク。 各要求で、ASP.NET エンジンの `UrlAuthorizationModule` は、アプリケーションの構成で定義されている URL 承認規則を検査して、要求されたリソースへのアクセスが id に許可されているかどうかを判断します。 つまり、URL 承認を使用すると、特定のページまたは特定のディレクトリ内のすべてのページに対して承認規則を簡単に指定できます。

URL 承認フレームワークは、ページ単位で承認規則を適用します。 URL 承認では、要求元の id が特定のリソースへのアクセスを承認されているかどうかを示します。 ただし、多くのシナリオでは、より細かい粒度の承認規則が呼び出されます。 ページにアクセスできるユーザーを定義するのではなく、すべてのユーザーにページへのアクセスを許可し、別のデータを表示したり、ページにアクセスするユーザーに応じて異なる機能を提供したりすることが必要になる場合があります。 通常、ページレベルの承認では、許可されていないユーザーが禁止された機能にアクセスするのを防ぐために、特定のユーザーインターフェイス要素を非表示にします。 また、属性を使用して、クラスへのアクセスを制限したり、特定のユーザーに対してメソッドを実行したりすることができます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [`PrincipalPermissionAttributes` を使用したビジネス層およびデータ層への承認規則の追加](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 承認](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IIS6 と IIS7 のセキュリティ間の変更](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [特定のファイルとサブディレクトリの構成](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [ユーザーに基づいてデータ変更機能を制限する](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb.md)
- [LoginView コントロールのクイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [IIS7 URL 承認について](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 技術ドキュメント](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [ASP.NET 2.0 でのデータの操作](../../data-access/index.md)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](validating-user-credentials-against-the-membership-user-store-vb.md)
> [次へ](storing-additional-user-information-vb.md)
