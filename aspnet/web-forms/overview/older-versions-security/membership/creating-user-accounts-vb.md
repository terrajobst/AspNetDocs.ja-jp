---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
title: ユーザーアカウントを作成する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、(SqlMembershipProvider を使用して) メンバーシップフレームワークを使用して新しいユーザーアカウントを作成する方法について説明します。 新しいお客様を作成する方法については、
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 9ef3e893-bebe-4b13-9fe5-8b71720dd85e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 01be198c329f372ddcd529ad8a369f2d3426a9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474286"
---
# <a name="creating-user-accounts-vb"></a>ユーザー アカウントを作成する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_vb.pdf)

> このチュートリアルでは、(SqlMembershipProvider を使用して) メンバーシップフレームワークを使用して新しいユーザーアカウントを作成する方法について説明します。 プログラムおよび ASP を使用して、新しいユーザーを作成する方法について説明します。NET の組み込みの CreateUserWizard コントロール。

## <a name="introduction"></a>はじめに

前の<a id="_msoanchor_1"> </a>[チュートリアル](creating-the-membership-schema-in-sql-server-vb.md)では、データベースにアプリケーションサービススキーマをインストールしました。これにより、`SqlMembershipProvider` と `SqlRoleProvider`に必要なテーブル、ビュー、およびストアドプロシージャが追加されました。 これにより、このシリーズのチュートリアルの残りの部分に必要なインフラストラクチャが作成されました。 このチュートリアルでは、(`SqlMembershipProvider`を使用して) メンバーシップフレームワークを使用して新しいユーザーアカウントを作成する方法について説明します。 プログラムおよび ASP を使用して、新しいユーザーを作成する方法について説明します。NET の組み込みの CreateUserWizard コントロール。

新しいユーザーアカウントを作成する方法を学習するだけでなく、フォーム認証 *<a id="_msoanchor_2"></a>[の概要](../introduction/an-overview-of-forms-authentication-vb.md)* に関するチュートリアルで最初に作成したデモ web サイトを更新し、 *<a id="_msoanchor_3"></a>[フォーム認証の構成と高度なトピック](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* のチュートリアルで強化する必要もあります。 デモ web アプリケーションには、ハードコーディングされたユーザー名とパスワードのペアに対してユーザーの資格情報を検証するログインページがあります。 さらに、`Global.asax` には、認証されたユーザーのカスタム `IPrincipal` と `IIdentity` オブジェクトを作成するコードが含まれています。 ログインページを更新して、メンバーシップフレームワークに対してユーザーの資格情報を検証し、カスタムプリンシパルと id ロジックを削除します。

作業開始

## <a name="the-forms-authentication-and-membership-checklist"></a>フォーム認証とメンバーシップのチェックリスト

メンバーシップフレームワークの使用を開始する前に、この時点までに実行した重要な手順を確認してみましょう。 フォームベースの認証シナリオでメンバーシップフレームワークを `SqlMembershipProvider` と共に使用する場合、web アプリケーションにメンバーシップ機能を実装する前に、次の手順を実行する必要があります。

1. **フォームベースの認証を有効にします。** *<a id="_msoanchor_4"></a>[フォーム認証の概要](../introduction/an-overview-of-forms-authentication-vb.md)* で説明したように、フォーム認証を有効にするには、`Web.config` を編集し、`<authentication>` 要素の `mode` 属性を `Forms`に設定します。 フォーム認証を有効にすると、受信した各要求が*フォーム認証チケット*(存在する場合) について確認され、要求元が識別されます。
2. **アプリケーションサービススキーマを適切なデータベースに追加します。** `SqlMembershipProvider` を使用する場合は、アプリケーションサービススキーマをデータベースにインストールする必要があります。 通常、このスキーマは、アプリケーションのデータモデルを保持する同じデータベースに追加されます。 *<a id="_msoanchor_5"></a>[SQL Server チュートリアルでメンバーシップスキーマを作成](creating-the-membership-schema-in-sql-server-vb.md)* する方法については、「`aspnet_regsql.exe` ツールを使用してこれを実現する」を参照してください。
3. **手順 2. のデータベースを参照するように Web アプリケーションの設定をカスタマイズします。** *SQL Server チュートリアルでメンバーシップスキーマを作成*するには、「手順 2: `LocalSqlServer` 接続文字列名を変更することによって、`SqlMembershipProvider` が選択したデータベースを使用するように web アプリケーションを構成する2つの方法を説明しました。または、新しい登録済みプロバイダーをメンバーシップフレームワークプロバイダーの一覧に追加し、手順2で作成したデータベースを使用するように新しいプロバイダーをカスタマイズします。

`SqlMembershipProvider` とフォームベースの認証を使用する web アプリケーションを構築する場合は、`Membership` クラスまたは ASP.NET Login Web コントロールを使用する前に、次の3つの手順を実行する必要があります。 前のチュートリアルでこれらの手順を既に実行していたため、メンバーシップフレームワークの使用を開始する準備ができました。

## <a name="step-1-adding-new-aspnet-pages"></a>手順 1:新しい ASP.NET ページの追加

このチュートリアルと次の3つでは、メンバーシップに関連するさまざまな関数と機能について説明します。 これらのチュートリアル全体で検討したトピックを実装するには、一連の ASP.NET ページが必要です。 これらのページを作成し、サイトマップファイル `(Web.sitemap)`を作成してみましょう。

まず、`Membership`という名前のプロジェクトに新しいフォルダーを作成します。 次に、5つの新しい ASP.NET ページを `Membership` フォルダーに追加し、各ページを `Site.master` マスターページとリンクします。 ページに名前を指定します。

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

この時点で、プロジェクトのソリューションエクスプローラーは、図1に示すスクリーンショットのようになります。

[![5 つの新しいページがメンバーシップフォルダーに追加されました](creating-user-accounts-vb/_static/image2.png)](creating-user-accounts-vb/_static/image1.png)

**図 1**:`Membership` フォルダーに新しいページが5つ追加されました ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image3.png)されます)

各ページには、この時点で2つのコンテンツコントロールが含まれている必要があります。1つは、`MainContent` と `LoginContent`の各マスターページの ContentPlaceHolders です。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample1.aspx)]

`LoginContent` ContentPlaceHolder の既定のマークアップによって、ユーザーが認証されているかどうかに応じて、サイトへのログオンまたはログオフを行うためのリンクが表示されることを思い出してください。 ただし、`Content2` コンテンツコントロールの存在は、マスターページの既定のマークアップよりも優先されます。 *<a id="_msoanchor_6"></a>[「フォーム認証チュートリアルの概要](../introduction/an-overview-of-forms-authentication-vb.md)* 」で説明したように、これは、左の列にログイン関連のオプションを表示しないページで役立ちます。

ただし、この5つのページでは、`LoginContent` ContentPlaceHolder のマスターページの既定のマークアップを表示します。 そのため、`Content2` コンテンツコントロールの宣言型マークアップを削除します。 その後、5ページの各マークアップには、コンテンツコントロールを1つだけ含める必要があります。

## <a name="step-2-creating-the-site-map"></a>手順 2:サイトマップの作成

最も単純な web サイト以外はすべて、何らかの形のナビゲーションユーザーインターフェイスを実装する必要があります。 ナビゲーションユーザーインターフェイスは、サイトのさまざまなセクションへのリンクの単純なリストである場合があります。 または、これらのリンクをメニューまたはツリービューに配置することもできます。 ページ開発者として、ナビゲーションユーザーインターフェイスを作成するのは、そのストーリーの半分にすぎません。 また、保守しやすく更新可能な方法でサイトの論理構造を定義するためにもいくつかの手段が必要です。 新しいページを追加したり、既存のページを削除したりすると、1つのソース (サイトマップ) を更新して、サイトのナビゲーションユーザーインターフェイス全体にその変更を反映させることができます。

サイトマップの定義とサイトマップに基づくナビゲーションユーザーインターフェイスの実装という2つのタスクは、サイトマップフレームワークや、ASP.NET バージョン2.0 で追加されたナビゲーション Web コントロールによって簡単に実現できます。 サイトマップフレームワークを使用すると、開発者はサイトマップを定義してから、プログラム API ( [`SiteMap` クラス](https://msdn.microsoft.com/library/system.web.sitemap.aspx)) を使用してアクセスできます。 組み込みのナビゲーション Web コントロールには、[メニューコントロール](https://msdn.microsoft.com/library/bz09dy46.aspx)、 [TreeView コントロール](https://msdn.microsoft.com/library/3eafky27.aspx)、および[SiteMapPath コントロール](https://msdn.microsoft.com/library/3eafky27.aspx)が含まれています。

メンバーシップとロールのフレームワークと同様に、サイトマップフレームワークは[プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)の上に構築されています。 サイトマッププロバイダークラスのジョブでは、XML ファイルやデータベーステーブルなどの永続データストアから `SiteMap` クラスによって使用されるメモリ内の構造を生成します。 .NET Framework には、XML ファイル ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)) からサイトマップデータを読み取る既定のサイトマッププロバイダーが付属しています。これは、このチュートリアルで使用するプロバイダーです。 代替のサイトマッププロバイダーの実装については、このチュートリアルの最後にある「参考資料」セクションを参照してください。

既定のサイトマッププロバイダーでは、`Web.sitemap` という名前の適切な形式の XML ファイルがルートディレクトリに存在することを想定しています。 この既定のプロバイダーを使用するため、このようなファイルを追加し、サイトマップの構造を適切な XML 形式で定義する必要があります。 ファイルを追加するには、ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] を選択します。 ダイアログボックスで、`Web.sitemap`という名前のサイトマップの種類のファイルを追加することを選択します。

[Web.config という名前のファイルをプロジェクトのルートディレクトリに追加 ![ます。](creating-user-accounts-vb/_static/image5.png)](creating-user-accounts-vb/_static/image4.png)

**図 2**:`Web.sitemap` という名前のファイルをプロジェクトのルートディレクトリに追加します ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image6.png)されます)

XML サイトマップファイルは、web サイトの構造を階層として定義します。 この階層関係は、`<siteMapNode>` 要素の先祖を通じて XML ファイルでモデル化されています。 `Web.sitemap` は、正確に1つの `<siteMapNode>` 子を持つ `<siteMap>` 親ノードで始める必要があります。 この最上位の `<siteMapNode>` 要素は、階層のルートを表し、任意の数の子孫ノードを持つことができます。 各 `<siteMapNode>` 要素には、`title` 属性を含める必要があります。また、必要に応じて、`url` と `description` の属性を含めることもできます。空ではない `url` 属性はそれぞれ一意である必要があります。

`Web.sitemap` ファイルに次の XML を入力します。

[!code-xml[Main](creating-user-accounts-vb/samples/sample2.xml)]

上記のサイトマップマークアップでは、図3に示す階層を定義します。

[サイトマップが階層ナビゲーション構造を表す ![](creating-user-accounts-vb/_static/image8.png)](creating-user-accounts-vb/_static/image7.png)

**図 3**:サイトマップは階層ナビゲーション構造を表します ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image9.png)されます)

## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>手順 3:ナビゲーションユーザーインターフェイスを含むようにマスターページを更新する

ASP.NET には、ユーザーインターフェイスを設計するためのナビゲーション関連のさまざまな Web コントロールが含まれています。 これには、メニュー、TreeView、および SiteMapPath コントロールが含まれます。 メニューコントロールと TreeView コントロールは、それぞれ1つのメニューまたはツリーにサイトマップ構造を表示します。一方、SiteMapPath には、現在アクセスしているノードとその先祖を示す階層リンクが表示されます。 サイトマップデータは、SiteMapDataSource を使用して他のデータ Web コントロールにバインドすることができ、`SiteMap` クラスを使用してプログラムからアクセスすることができます。

このチュートリアルシリーズでは、サイトマップフレームワークとナビゲーションコントロールの詳細については説明しません。そのため、独自のナビゲーションユーザーインターフェイスを作成するのではなく、「 *[ASP.NET 2.0](../../data-access/index.md)* チュートリアルシリーズのデータの操作」で使用されているものを借用します。このシリーズでは、図4に示すように、Repeater コントロールを使用して、

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>左の列に2レベルのリンクの一覧を追加する

このインターフェイスを作成するには、次の宣言型マークアップを `Site.master` マスターページの左の列に追加します。このテキストは TODO:メニューがここに表示されます...現在は存在します。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample3.aspx)]

上のマークアップは、`menu` という名前のリピータコントロールを、`Web.sitemap`で定義されたサイトマップ階層を返す SiteMapDataSource にバインドします。 SiteMapDataSource コントロールの[`ShowStartingNode` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)は False に設定されているため、ホームノードの子孫で始まるサイトマップの階層が返され始めます。 リピータは、これらの各ノード (現時点ではメンバーシップ) を `<li>` 要素に表示します。 もう1つの内部リピータは、入れ子になった順序なしリストに現在のノードの子を表示します。

図4に、上記のマークアップのレンダリング出力と、手順2で作成したサイトマップ構造を示します。 リピータは、バニラの順序なしリストマークアップをレンダリングします。`Styles.css` で定義されているカスケードスタイルシートルールは、見た目のあるレイアウトを担当します。 上記のマークアップの動作の詳細については、「[マスターページとサイトナビゲーション](https://asp.net/learn/data-access/tutorial-03-vb.aspx)のチュートリアル」を参照してください。

[ナビゲーションユーザーインターフェイスが、入れ子になった順序なしリストを使用して表示される ![](creating-user-accounts-vb/_static/image11.png)](creating-user-accounts-vb/_static/image10.png)

**図 4**:ナビゲーションユーザーインターフェイスは、入れ子になった順序なしリストを使用してレンダリングされます ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image12.png)されます)

### <a name="adding-breadcrumb-navigation"></a>階層リンクナビゲーションの追加

左の列のリンクの一覧に加えて、各ページに[階層リンク](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)が表示されます。 階層リンクとは、ユーザーがサイト階層内の現在の位置をすばやく表示するナビゲーションユーザーインターフェイス要素です。 SiteMapPath コントロールは、サイトマップフレームワークを使用して、サイトマップ内の現在のページの場所を判断し、この情報に基づいて階層リンクを表示します。

具体的には、`<span>` 要素をマスターページのヘッダー `<div>` 要素に追加し、新しい `<span>` 要素の `class` 属性を階層リンクに設定します。 (`Styles.css` クラスには、階層リンククラスの規則が含まれています)。次に、この新しい `<span>` 要素に SiteMapPath を追加します。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample4.aspx)]

図5に、`~/Membership/CreatingUserAccounts.aspx`にアクセスしたときの SiteMapPath の出力を示します。

[階層リンクの ![、現在のページとその先祖がサイトマップに表示されます。](creating-user-accounts-vb/_static/image14.png)](creating-user-accounts-vb/_static/image13.png)

**図 5**:階層リンクには、現在のページとその先祖がサイトマップに表示されます ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image15.png)されます)

## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>手順 4:カスタムプリンシパルと Id ロジックの削除

*<a id="_msoanchor_7"></a>[フォーム認証構成と高度なトピック](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* のチュートリアルでは、カスタムプリンシパルオブジェクトと id オブジェクトを認証されたユーザーに関連付ける方法について説明しました。 これを実現するには、アプリケーションの `PostAuthenticateRequest` イベントのイベントハンドラーを `Global.asax` で作成します。これは、`FormsAuthenticationModule` がユーザーを認証した後に発生します。 このイベントハンドラーでは、`FormsAuthenticationModule` によって追加された `GenericPrincipal` と `FormsIdentity` オブジェクトを、そのチュートリアルで作成した `CustomPrincipal` および `CustomIdentity` のオブジェクトに置き換えました。

カスタムプリンシパルオブジェクトと id オブジェクトは特定のシナリオで役に立ちますが、ほとんどの場合、`GenericPrincipal` オブジェクトと `FormsIdentity` オブジェクトで十分です。 そのため、既定の動作に戻すことができると思います。 この変更を行うには、`PostAuthenticateRequest` イベントハンドラーを削除するかコメントアウトするか、`Global.asax` ファイルを完全に削除します。

> [!NOTE]
> `Global.asax`のコードをコメント化または削除したら、`User.Identity` プロパティを `CustomIdentity` インスタンスにキャストする `Default.aspx's` コードビハインドクラスのコードをコメントアウトする必要があります。

## <a name="step-5-programmatically-creating-a-new-user"></a>手順 5:プログラムによる新しいユーザーの作成

メンバーシップフレームワークを使用して新しいユーザーアカウントを作成するには、`Membership` クラスの[`CreateUser` メソッド](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)を使用します。 このメソッドには、ユーザー名、パスワード、およびその他のユーザー関連フィールドの入力パラメーターがあります。 呼び出し時に、構成されたメンバーシッププロバイダーに新しいユーザーアカウントの作成を委任した後、作成されたユーザーアカウントのみを表す[`MembershipUser` オブジェクト](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)を返します。

`CreateUser` メソッドには4つのオーバーロードがあり、それぞれが異なる数の入力パラメーターを受け入れます。

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

これらの4つのオーバーロードは、収集される情報の量によって異なります。 たとえば、最初のオーバーロードでは、新しいユーザーアカウントのユーザー名とパスワードのみが必要ですが、2つ目のオーバーロードでは、ユーザーの電子メールアドレスも必要です。

新しいユーザーアカウントを作成するために必要な情報は、メンバーシッププロバイダーの構成設定によって異なるため、これらのオーバーロードが存在します。 SQL Server チュートリアル *<a id="_msoanchor_8"></a>[でメンバーシップスキーマを作成する方法](creating-the-membership-schema-in-sql-server-vb.md)* については、`Web.config`でメンバーシッププロバイダーの構成設定を指定する方法について説明します。 表2に、構成設定の完全な一覧を示します。

使用できる `CreateUser` のオーバーロードに影響を与えるメンバーシッププロバイダーの構成設定の1つに、`requiresQuestionAndAnswer` の設定があります。 `requiresQuestionAndAnswer` が `true` (既定値) に設定されている場合は、新しいユーザーアカウントを作成するときに、セキュリティの質問と回答を指定する必要があります。 この情報は、ユーザーがパスワードをリセットまたは変更する必要がある場合に、後で使用されます。 具体的には、その時点でセキュリティの質問が表示され、パスワードをリセットまたは変更するために正しい回答を入力する必要があります。 その結果、`requiresQuestionAndAnswer` が `true` に設定されている場合、最初の2つの `CreateUser` オーバーロードのいずれかを呼び出すと、セキュリティの質問と回答がないため、例外が発生します。 現在、アプリケーションはセキュリティの質問と回答を要求するように構成されているため、プログラムでユーザーを作成する場合は、後者の2つのオーバーロードのいずれかを使用する必要があります。

`CreateUser` メソッドの使用方法を示すために、ユーザーインターフェイスを作成して、ユーザーに名前、パスワード、電子メール、事前定義されたセキュリティの質問への回答を入力するように指示します。 `Membership` フォルダーの [`CreatingUserAccounts.aspx`] ページを開き、次の Web コントロールをコンテンツコントロールに追加します。

- `Username` という名前のテキストボックス
- `TextMode` プロパティがに設定されている `Password`という名前のテキストボックス `Password`
- `Email` という名前のテキストボックス
- `Text` プロパティがクリアされた `SecurityQuestion` という名前のラベル
- `SecurityAnswer` という名前のテキストボックス
- `Text` プロパティがユーザーアカウントを作成するように設定されている `CreateAccountButton` という名前のボタン
- `Text` プロパティがクリアされた `CreateAccountResults` という名前のラベルコントロール

この時点で、画面は図6に示すスクリーンショットのようになります。

[[![] ページにさまざまな Web コントロールを追加する](creating-user-accounts-vb/_static/image17.png)](creating-user-accounts-vb/_static/image16.png)

**図 6**:さまざまな Web コントロールを `CreatingUserAccounts.aspx Page` に追加します ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image18.png)されます)

`SecurityQuestion` ラベルと `SecurityAnswer` テキストボックスは、事前に定義されたセキュリティの質問を表示し、ユーザーの回答を収集することを目的としています。 セキュリティの質問と回答はユーザーごとに保存されるので、各ユーザーが独自のセキュリティの質問を定義できるようにすることができます。 ただし、この例では、ユニバーサルセキュリティの質問を使用することにしました。好きな色は何ですか。

この事前定義されたセキュリティの質問を実装するには、`passwordQuestion`という名前のページの分離コードクラスに定数を追加し、それにセキュリティの質問を割り当てます。 次に、`Page_Load` イベントハンドラーで、この定数を `SecurityQuestion` ラベルの `Text` プロパティに割り当てます。

[!code-vb[Main](creating-user-accounts-vb/samples/sample5.vb)]

次に、`CreateAccountButton'` s `Click` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](creating-user-accounts-vb/samples/sample6.vb)]

`Click` イベントハンドラーは、 [`MembershipCreateStatus`](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)型の `createStatus` という名前の変数を定義することによって開始されます。 `MembershipCreateStatus` は、`CreateUser` 操作の状態を示す列挙体です。 たとえば、ユーザーアカウントが正常に作成された場合、結果の `MembershipCreateStatus` インスタンスは `Success;` の値に設定されます。ただし、同じユーザー名を持つユーザーが既に存在するために操作が失敗した場合は、`DuplicateUserName`の値に設定されます。 使用する `CreateUser` オーバーロードでは、`MembershipCreateStatus` インスタンスをメソッドに渡す必要があります。 このパラメーターは `CreateUser` メソッド内の適切な値に設定され、メソッド呼び出しの後でその値を調べて、ユーザーアカウントが正常に作成されたかどうかを確認できます。

`createStatus`を渡して `CreateUser`を呼び出した後、`Select Case` ステートメントを使用して、`createStatus`に割り当てられた値に応じて適切なメッセージを出力します。 図7は、新しいユーザーが正常に作成されたときの出力を示しています。 図8と9は、ユーザーアカウントが作成されていない場合の出力を示しています。 図8では、ビジターは5文字のパスワードを入力しました。このパスワードは、メンバーシッププロバイダーの構成設定に記載されているパスワードの強度の要件を満たしていません。 図9では、ビジターが既存のユーザー名 (図7で作成したもの) を使用してユーザーアカウントを作成しようとしています。

[新しいユーザーアカウントが正常に作成された ![](creating-user-accounts-vb/_static/image20.png)](creating-user-accounts-vb/_static/image19.png)

**図 7**:新しいユーザーアカウントが正常に作成されました ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image21.png)されます)

[指定されたパスワードが不十分であるため、ユーザーアカウントが作成され ![](creating-user-accounts-vb/_static/image23.png)](creating-user-accounts-vb/_static/image22.png)

**図 8**:指定されたパスワードが不十分なため、ユーザーアカウントは作成されません ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image24.png)されます)

[ユーザー名が既に使用されているため、ユーザーアカウントが作成され ![](creating-user-accounts-vb/_static/image26.png)](creating-user-accounts-vb/_static/image25.png)

**図 9**:ユーザー名が既に使用されているため、ユーザーアカウントは作成されません ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image27.png)されます)

> [!NOTE]
> 最初の2つの `CreateUser` メソッドオーバーロードのいずれかを使用した場合に成功または失敗を判断する方法について疑問があるかもしれませんが、どちらも `MembershipCreateStatus`型のパラメーターを持っていません。 これらの最初の2つのオーバーロードは、エラー発生時に[`MembershipCreateUserException` 例外](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx)をスローします。これには `MembershipCreateStatus`型の[`StatusCode` プロパティ](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx)が含まれます。

いくつかのユーザーアカウントを作成した後、`SecurityTutorials.mdf` データベースの `aspnet_Users` テーブルと `aspnet_Membership` テーブルの内容を一覧表示して、アカウントが作成されていることを確認します。 図10に示すように、`CreatingUserAccounts.aspx` のページを使用して2人のユーザーを追加しました。Tito としています。

メンバーシップユーザーストアに2人のユーザーがいる ![[ます。Tito および](creating-user-accounts-vb/_static/image29.png)](creating-user-accounts-vb/_static/image28.png)

**図 10**:メンバーシップユーザーストアには、次の2人のユーザーがいます。Tito および ([クリックしてフルサイズの画像を表示](creating-user-accounts-vb/_static/image30.png))

メンバーシップユーザーストアには、お客様のアカウント情報が含まれるようになりましたが、サイトへのログオンを可能にする機能をまだ実装していません。 現時点では、`Login.aspx` ユーザーの資格情報をハードコーディングされたユーザー名とパスワードの組み合わせに対して検証します。メンバーシップフレームワークに対して指定された資格情報を検証し*ません*。 ここでは、`aspnet_Users` テーブルと `aspnet_Membership` テーブルの新しいユーザーアカウントに十分な権限があることを確認します。 次のチュートリアル「 *<a id="_msoanchor_9"></a>[メンバーシップユーザーストアに対してユーザー資格情報を検証](validating-user-credentials-against-the-membership-user-store-vb.md)* する」では、メンバーシップストアに対して検証するためにログインページを更新します。

> [!NOTE]
> `SecurityTutorials.mdf` データベースにユーザーが表示されない場合は、web アプリケーションが既定のメンバーシッププロバイダーである `AspNetSqlMembershipProvider`を使用していることが原因である可能性があります。このプロバイダーは、`ASPNETDB.mdf` データベースをユーザーストアとして使用しています。 これが問題かどうかを判断するには、ソリューションエクスプローラーの [更新] ボタンをクリックします。 `ASPNETDB.mdf` という名前のデータベースが `App_Data` フォルダーに追加されている場合は、この問題が発生します。 メンバーシッププロバイダーを適切に構成する方法については、 *<a id="_msoanchor_10"></a>[SQL Server チュートリアルの「メンバーシップスキーマの作成」](creating-the-membership-schema-in-sql-server-vb.md)* の手順4に戻ります。

ほとんどのユーザーアカウントの作成シナリオでは、ユーザー名、パスワード、電子メール、その他の重要な情報を入力するためのインターフェイスがビジターに提示され、その時点で新しいアカウントが作成されます。 このステップでは、このようなインターフェイスを手動で構築し、`Membership.CreateUser` メソッドを使用して、ユーザーの入力に基づいて新しいユーザーアカウントをプログラムで追加する方法を見てきました。 ただし、このコードは新しいユーザーアカウントを作成しただけです。 作成したユーザーアカウントでのサイトへのユーザーのログイン、ユーザーへの確認メールの送信など、フォローアップのアクションは実行されませんでした。 これらの追加の手順では、ボタンの `Click` イベントハンドラーに追加のコードが必要になります。

ASP.NET には CreateUserWizard コントロールが付属しています。このコントロールは、新しいユーザーアカウントを作成するためのユーザーインターフェイスを表示したり、メンバーシップフレームワークでアカウントを作成したり、後でアカウントを実行したりするために、ユーザーアカウントの作成プロセスを処理するように設計されています。作成タスク。確認メールを送信し、作成したユーザーをサイトに記録します。 CreateUserWizard コントロールの使用は、CreateUserWizard コントロールをツールボックスからページにドラッグし、いくつかのプロパティを設定するだけで簡単に行うことができます。 ほとんどの場合、1行のコードを記述する必要はありません。 この素晴らしいコントロールについては、手順 6. で詳しく説明します。

新しいユーザーアカウントが通常のアカウント作成 web ページでのみ作成されている場合は、CreateUserWizard コントロールがニーズを満たす可能性があるため、`CreateUser` メソッドを使用するコードを記述することが必要になる可能性はほとんどありません。 ただし、`CreateUser` 方法は、高度にカスタマイズされたアカウントのユーザーエクスペリエンスが必要な場合や、別のインターフェイスを使用してプログラムによって新しいユーザーアカウントを作成する必要がある場合に便利です。 たとえば、ユーザーが他のアプリケーションからのユーザー情報を含む XML ファイルをアップロードできるページがあるとします。 このページでは、アップロードされた XML ファイルの内容を解析し、`CreateUser` メソッドを呼び出すことによって、XML で表されるユーザーごとに新しいアカウントを作成できます。

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>手順 6:CreateUserWizard コントロールを使用して新しいユーザーを作成する

ASP.NET には、多数のログイン Web コントロールが付属しています。 これらのコントロールは、多くの一般的なユーザーアカウントおよびログイン関連のシナリオに役立ちます。 [CreateUserWizard コントロール](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)は、メンバーシップフレームワークに新しいユーザーアカウントを追加するためのユーザーインターフェイスを提供するように設計されたコントロールの1つです。

他の多くのログイン関連 Web コントロールと同様に、1行のコードも記述せずに CreateUserWizard を使用できます。 直感的には、メンバーシッププロバイダーの構成設定に基づいてユーザーインターフェイスを提供し、ユーザーが必要な情報を入力して [ユーザーの作成] ボタンをクリックした後に `Membership` クラスの `CreateUser` メソッドを呼び出します。 CreateUserWizard コントロールは、非常にカスタマイズが可能です。 アカウント作成プロセスのさまざまな段階で発生するイベントのホストがあります。 必要に応じてイベントハンドラーを作成して、アカウント作成ワークフローにカスタムロジックを挿入できます。 さらに、CreateUserWizard の外観は非常に柔軟です。 既定のインターフェイスの外観を定義するプロパティがいくつかあります。必要に応じて、コントロールをテンプレートに変換したり、追加のユーザー登録手順を追加したりすることができます。

まず、CreateUserWizard コントロールの既定のインターフェイスと動作の使用方法を見てみましょう。 次に、コントロールのプロパティとイベントを使用して外観をカスタマイズする方法について説明します。

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>CreateUserWizard の既定のインターフェイスと動作を調べる

`Membership` フォルダーの [`CreatingUserAccounts.aspx`] ページに戻り、デザインモードまたは分割モードに切り替えて、ページの上部に CreateUserWizard コントロールを追加します。 CreateUserWizard コントロールは、ツールボックスの [ログインコントロール] セクションに登録されています。 コントロールを追加した後、その `ID` プロパティを `RegisterUser`に設定します。 図11のスクリーンショットに示すように、CreateUserWizard は、新しいユーザーのユーザー名、パスワード、電子メールアドレス、およびセキュリティの質問と回答のテキストボックスを含むインターフェイスをレンダリングします。

[CreateUserWizard コントロールが汎用作成ユーザーインターフェイスをレンダリング ![](creating-user-accounts-vb/_static/image32.png)](creating-user-accounts-vb/_static/image31.png)

**図 11**:CreateUserWizard コントロールは、汎用の作成ユーザーインターフェイスを表示します ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image33.png)されます)

CreateUserWizard コントロールによって生成される既定のユーザーインターフェイスと、手順 5. で作成したインターフェイスを比較してみましょう。 初心者は、CreateUserWizard コントロールを使用して、ビジターがセキュリティの質問と回答の両方を指定できるようになります。一方、手動で作成されたインターフェイスでは、事前に定義されたセキュリティの質問が使用されていました。 CreateUserWizard コントロールのインターフェイスには検証コントロールも含まれていますが、インターフェイスのフォームフィールドに検証を実装しています。 また、CreateUserWizard コントロールインターフェイスには、[パスワードの確認入力] テキストボックスと [パスワードの比較] ボックスが同じであることを確認するための CompareValidator が含まれています。

興味深いのは、CreateUserWizard コントロールは、ユーザーインターフェイスをレンダリングするときに、メンバーシッププロバイダーの構成設定を調べることです。 たとえば、セキュリティの質問と回答のテキストボックスは、`requiresQuestionAndAnswer` が True に設定されている場合にのみ表示されます。 同様に、CreateUserWizard は RegularExpressionValidator コントロールを自動的に追加して、パスワードの強度の要件が満たされていることを確認し、`minRequiredPasswordLength`、`minRequiredNonalphanumericCharacters`、および `passwordStrengthRegularExpression` の構成設定に基づいて、`ErrorMessage` と `ValidationExpression` のプロパティを設定します。

CreateUserWizard コントロールは、その名前が示すように、[ウィザードコントロール](https://msdn.microsoft.com/library/s2etd1ek.aspx)から派生します。 ウィザードコントロールは、複数ステップのタスクを完了するためのインターフェイスを提供するように設計されています。 ウィザードコントロールには、任意の数の `WizardSteps`を含めることができます。各テンプレートは、その手順の HTML コントロールと Web コントロールを定義するテンプレートです。 ウィザードコントロールは、最初の `WizardStep`と、ユーザーが1つのステップから次のステップに進むことができるナビゲーションコントロール、または前の手順に戻ることを許可するナビゲーションコントロールを最初に表示します。

図11の宣言型マークアップが示すように、CreateUserWizard コントロールの既定のインターフェイスには2つの `WizardStep` が含まれています。

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) ? 新しいユーザーアカウントを作成するための情報を収集するためのインターフェイスをレンダリングします。 これは、図11に示す手順です。
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) ? アカウントが正常に作成されたことを示すメッセージを表示します。

CreateUserWizard の外観と動作は、これらの手順のいずれかをテンプレートに変換するか、独自の `WizardStep` を追加することによって変更できます。 *追加のユーザー情報を格納*するチュートリアルでは、登録インターフェイスに `WizardStep` を追加する方法について説明します。

CreateUserWizard コントロールの動作を見てみましょう。 ブラウザーを使用して `CreatingUserAccounts.aspx` のページにアクセスします。 まず、CreateUserWizard のインターフェイスに無効な値を入力します。 パスワードの強度の要件に準拠していないパスワードを入力するか、[ユーザー名] ボックスを空のままにしてください。 CreateUserWizard に、適切なエラーメッセージが表示されます。 図12は、強力なパスワードを使用してユーザーを作成しようとした場合の出力を示しています。

[CreateUserWizard が検証コントロールを自動的に挿入する ![](creating-user-accounts-vb/_static/image35.png)](creating-user-accounts-vb/_static/image34.png)

**図 12**:CreateUserWizard は、自動的に検証コントロールを挿入します ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image36.png)されます)

次に、CreateUserWizard に適切な値を入力し、[ユーザーの作成] ボタンをクリックします。 必須フィールドが入力され、パスワードの強度が十分であると仮定すると、CreateUserWizard はメンバーシップフレームワークを使用して新しいユーザーアカウントを作成し、`CompleteWizardStep`のインターフェイスを表示します (図13を参照)。 CreateUserWizard は、バックグラウンドで、手順5で行ったのと同じように `Membership.CreateUser` メソッドを呼び出します。

[新しいユーザーアカウントが正常に作成された ![](creating-user-accounts-vb/_static/image38.png)](creating-user-accounts-vb/_static/image37.png)

**図 13**:新しいユーザーアカウントが正常に作成されました ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image39.png)されます)

> [!NOTE]
> 図13に示すように、`CompleteWizardStep`のインターフェイスには [続行] ボタンがあります。 ただし、この時点でクリックするだけでポストバックが実行され、ビジターは同じページに残ります。 「CreateUserWizard の外観と動作をカスタマイズする」セクションでは、このボタンを使用して訪問者を `Default.aspx` (またはその他のページ) に送信する方法について説明します。

新しいユーザーアカウントを作成した後、Visual Studio に戻り、図10のような `aspnet_Users` と `aspnet_Membership` のテーブルを調べて、アカウントが正常に作成されたことを確認します。

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>プロパティを使用して CreateUserWizard の動作と外観をカスタマイズする

CreateUserWizard は、プロパティ、`WizardStep` s、イベントハンドラーなど、さまざまな方法でカスタマイズできます。 このセクションでは、プロパティを使用してコントロールの外観をカスタマイズする方法について説明します。次のセクションでは、イベントハンドラーによってコントロールの動作を拡張する方法について説明します。

CreateUserWizard コントロールの既定のユーザーインターフェイスに表示されるテキストは、事実上、大量のプロパティを使用してカスタマイズできます。 たとえば、テキストボックスの左側に表示される [ユーザー名]、[パスワード]、[パスワードの確認]、[電子メール]、[セキュリティの質問]、および [セキュリティの回答] のラベルは、それぞれ[`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx)、 [`PasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx)、 [`ConfirmPasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx)、 [`EmailLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx)、 [`QuestionLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)、および[`AnswerLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx)の各プロパティでカスタマイズできます。 同様に、`CreateUserWizardStep` と `CompleteWizardStep`で [ユーザーの作成] および [続行] ボタンのテキストを指定するためのプロパティと、これらのボタンがボタン、リンクボタン、または ImageButtons として表示されるかどうかも指定されています。

色、罫線、フォント、およびその他のビジュアル要素は、スタイルプロパティのホストを使用して構成できます。 CreateUserWizard コントロール自体には、一般的な Web コントロールスタイルプロパティ (`BackColor`、`BorderStyle`、`CssClass`、`Font`など) があります。また、CreateUserWizard のインターフェイスの特定のセクションの外観を定義するためのスタイルプロパティがいくつかあります。 たとえば、 [`TextBoxStyle` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx)は `CreateUserWizardStep`内のテキストボックスのスタイルを定義し、 [`TitleTextStyle` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx)はタイトルのスタイルを定義します (新しいアカウントにサインアップします)。

外観に関連するプロパティに加えて、CreateUserWizard コントロールの動作に影響を与えるプロパティがいくつかあります。 [ `DisplayCancelButton`プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)場合、true の場合、表示する (既定値は False)、ユーザーの作成ボタンの横の [キャンセル] ボタンを設定します。 [キャンセル] ボタンを表示する場合は、[キャンセル] をクリックした後にユーザーが送信されるページを指定する[`CancelDestinationPageUrl` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)も設定してください。 前のセクションで説明したように、`CompleteWizardStep`のインターフェイスの [続行] ボタンをクリックするとポストバックが発生しますが、ビジターは同じページに残ります。 [続行] ボタンをクリックした後に他のページにビジターを送信するには、 [`ContinueDestinationPageUrl` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)で URL を指定するだけです。

[キャンセル] ボタンまたは [続行] ボタンがクリックされたときに `Default.aspx` を表示するように `RegisterUser` CreateUserWizard コントロールを更新してみましょう。 これを行うには、`DisplayCancelButton` プロパティを True に設定し、`CancelDestinationPageUrl` と `ContinueDestinationPageUrl` の両方のプロパティを ~/Default. aspxに設定します。 図14に、ブラウザーで表示したときの更新された CreateUserWizard を示します。

[Createuserwizardstep.contenttemplate はに [キャンセル] ボタンが含まれている ![](creating-user-accounts-vb/_static/image41.png)](creating-user-accounts-vb/_static/image40.png)

**図 14**:`CreateUserWizardStep` には [キャンセル] ボタンが含まれています ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image42.png)されます)

ビジターがユーザー名、パスワード、電子メールアドレス、およびセキュリティの質問と回答を入力し、[ユーザーの作成] をクリックすると、新しいユーザーアカウントが作成され、そのユーザーが新しく作成したユーザーとしてログインします。 ページにアクセスしているユーザーが自分用の新しいアカウントを作成していると仮定した場合、これは望ましい動作です。 ただし、管理者が新しいユーザーアカウントを追加できるようにすることもできます。 これにより、ユーザーアカウントが作成されますが、管理者は管理者としてログインしたままになります (新しく作成されたアカウントとしてではありません)。 この動作は、ブール値の[`LoginCreatedUser` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)を使用して変更できます。

メンバーシップフレームワークのユーザーアカウントには、承認済みフラグが含まれています。承認されていないユーザーは、サイトにログインできません。 既定では、新しく作成されたアカウントは承認済みとしてマークされ、ユーザーはすぐにサイトにログインできます。 ただし、新しいユーザーアカウントを未承認としてマークすることもできます。 場合によっては、ログインする前に、管理者が手動で新しいユーザーを承認しなければならないことがあります。または、サインアップ時に入力した電子メールアドレスが有効であることを確認してから、ユーザーにログオンを許可することもできます。 どのような場合でも、CreateUserWizard コントロールの[`DisableCreatedUser` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)を True (既定値は False) に設定することで、新しく作成されたユーザーアカウントを未承認としてマークすることができます。

その他の動作関連のプロパティには、`AutoGeneratePassword` および `MailDefinition`が含まれます。 場合、 [ `AutoGeneratePassword`プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx)を True に設定されている、`CreateUserWizardStep`パスワードとパスワードの確認テキスト ボックスで; には表示されません代わりに、新しく作成したユーザーのパスワードが自動的に生成を使用して、 `Membership`クラスの[`GeneratePassword`メソッド](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)です。 `GeneratePassword` メソッドは、指定された長さのパスワードを作成し、構成されているパスワード強度要件を満たすのに十分な数の英数字以外の文字を作成します。

[`MailDefinition` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)は、アカウントの作成処理中に指定された電子メールアドレスに電子メールを送信する場合に便利です。 `MailDefinition` プロパティには、構築された電子メールメッセージに関する情報を定義するための一連のサブプロパティが含まれています。 これらのサブプロパティには、`Subject`、`Priority`、`IsBodyHtml`、`From`、`CC`、`BodyFileName`などのオプションが含まれます。 [`BodyFileName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)は、電子メールメッセージの本文を含むテキストまたは HTML ファイルを指します。 本文は、`<%UserName%>` と `<%Password%>`の2つの定義済みプレースホルダーをサポートしています。 これらのプレースホルダーは、`BodyFileName` ファイルに存在する場合は、作成されたユーザーの名前とパスワードに置き換えられます。

> [!NOTE]
> `CreateUserWizard` コントロールの `MailDefinition` プロパティは、新しいアカウントが作成されたときに送信される電子メールメッセージの詳細を指定するだけです。 これには、電子メールメッセージの実際の送信方法 (SMTP サーバーまたはメールドロップディレクトリが使用されているかどうか、認証情報など) に関する詳細は含まれません。 これらの低レベルの詳細は、`Web.config`の `<system.net>` セクションで定義する必要があります。 これらの構成設定の詳細および ASP.NET 2.0 からの電子メールの送信の詳細については、 [SystemNetMail.com](http://www.systemnetmail.com/)と my の記事「 [ASP.NET 2.0 で電子メールを送信](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)する」を参照してください。

### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>イベントハンドラーを使用した CreateUserWizard の動作の拡張

CreateUserWizard コントロールは、ワークフローの実行中に多数のイベントを発生させます。 たとえば、ビジターがユーザー名、パスワード、およびその他の関連情報を入力し、[Create User] ボタンをクリックすると、CreateUserWizard コントロールによって[`CreatingUser` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)が発生します。 作成プロセス中に問題が発生した場合は、 [`CreateUserError` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx)が発生します。ただし、ユーザーが正常に作成された場合は、 [`CreatedUser` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)が発生します。 CreateUserWizard コントロールイベントが発生することがありますが、これらは3つの最も連動があります。

特定のシナリオでは、CreateUserWizard ワークフローを使用することもできます。これは、適切なイベントのイベントハンドラーを作成することによって行うことができます。 これを説明するために、ユーザー名とパスワードにカスタム検証を含めるように `RegisterUser` CreateUserWizard コントロールを強化しましょう。 特に、CreateUserWizard を拡張して、ユーザー名に先頭または末尾のスペースを含めることはできず、ユーザー名はパスワード内の任意の場所に置くことができません。 簡潔に言えば、"Scott" のようなユーザー名を作成したり、Scott や Scott. 1234 などのユーザー名とパスワードの組み合わせを作成したりできないようにしたいと考えています。

これを実現するには、追加の検証チェックを実行するために、`CreatingUser` イベントのイベントハンドラーを作成します。 指定されたデータが有効でない場合は、作成プロセスを取り消す必要があります。 また、ラベル Web コントロールをページに追加して、ユーザー名またはパスワードが無効であることを示すメッセージを表示する必要もあります。 まず、CreateUserWizard コントロールの下にラベルコントロールを追加し、その `ID` プロパティを `InvalidUserNameOrPasswordMessage` に設定し、その `ForeColor` プロパティを `Red`に設定します。 `Text` プロパティをオフにし、その `EnableViewState` と `Visible` プロパティを False に設定します。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample7.aspx)]

次に、CreateUserWizard コントロールの `CreatingUser` イベントのイベントハンドラーを作成します。 イベントハンドラーを作成するには、デザイナーでコントロールを選択し、プロパティウィンドウにアクセスします。 そこから、稲妻のアイコンをクリックし、該当するイベントをダブルクリックしてイベントハンドラーを作成します。

`CreatingUser` イベント ハンドラーに次のコードを追加します。

[!code-vb[Main](creating-user-accounts-vb/samples/sample8.vb)]

CreateUserWizard コントロールに入力したユーザー名とパスワードは、それぞれ[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)と[`Password` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)で使用できます。 上記のイベントハンドラーでこれらのプロパティを使用して、指定したユーザー名に先頭または末尾のスペースが含まれているかどうか、およびユーザー名がパスワード内にあるかどうかを確認します。 これらのいずれかの条件が満たされると、エラーメッセージが `InvalidUserNameOrPasswordMessage` ラベルに表示され、イベントハンドラーの `e.Cancel` プロパティが `True`に設定されます。 `e.Cancel` が `True`に設定されている場合、CreateUserWizard はそのワークフローをショートサーキットし、ユーザーアカウントの作成プロセスを効果的に取り消します。

図15は、ユーザーが先頭のスペースを持つユーザー名を入力したときに `CreatingUserAccounts.aspx` のスクリーンショットを示しています。

[先頭または末尾にスペースが含まれているユーザー名は使用できません ![](creating-user-accounts-vb/_static/image44.png)](creating-user-accounts-vb/_static/image43.png)

**図 15**:先頭または末尾にスペースが含まれているユーザー名は使用できません ([クリックすると、フルサイズの画像が表示](creating-user-accounts-vb/_static/image45.png)されます)

> [!NOTE]
> CreateUserWizard コントロールの `CreatedUser` イベントを使用する例については、 *<a id="_msoanchor_11"></a>[「追加のユーザー情報の格納](storing-additional-user-information-vb.md)* 」のチュートリアルを参照してください。

## <a name="summary"></a>まとめ

`Membership` クラスの `CreateUser` メソッドによって、メンバーシップフレームワークに新しいユーザーアカウントが作成されます。 これは、構成されたメンバーシッププロバイダーの呼び出しを委任することによって行われます。 `SqlMembershipProvider`の場合、`CreateUser` メソッドは `aspnet_Users` および `aspnet_Membership` データベーステーブルにレコードを追加します。

新しいユーザーアカウントはプログラムで作成できますが (手順 5. で説明したように)、CreateUserWizard コントロールを使用する方法がより高速で簡単です。 このコントロールは、ユーザー情報を収集し、メンバーシップフレームワークで新しいユーザーを作成するための複数ステップのユーザーインターフェイスをレンダリングします。 内部的には、このコントロールは手順 5. と同じ `Membership.CreateUser` メソッドを使用しますが、コントロールはユーザーインターフェイスと検証コントロールを作成し、ユーザーアカウントの作成エラーに応答します。コードを記述する必要はありません。

この時点で、新しいユーザーアカウントを作成するための機能が用意されています。 ただし、ログインページでは、2番目のチュートリアルで指定したハードコーディングされた資格情報に対して検証が行われます。 <a id="_msoanchor_12"> </a>[次のチュートリアル](validating-user-credentials-against-the-membership-user-store-vb.md)では、メンバーシップフレームワークに対してユーザーが指定した資格情報を検証するために `Login.aspx` を更新します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [`CreateUser` 技術ドキュメント](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard コントロールの概要](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [ファイルシステムベースのサイトマッププロバイダーの作成](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [ASP.NET 2.0 Wizard コントロールを使用したステップバイステップのユーザーインターフェイスの作成](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [ASP.NET 2.0 のサイトナビゲーションを調べる](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [マスターページとサイトナビゲーション](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [待機している SQL サイトマッププロバイダー](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](creating-the-membership-schema-in-sql-server-vb.md)
> [次へ](validating-user-credentials-against-the-membership-user-store-vb.md)
