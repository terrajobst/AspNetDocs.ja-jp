---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
title: フォーム認証構成と高度なトピック (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、さまざまなフォーム認証設定を確認し、forms 要素を使用して変更する方法を確認します。 詳細情報...
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 829d2f56-5c48-445b-b826-3418a450c788
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
msc.type: authoredcontent
ms.openlocfilehash: 4d77816a489a4fa16cd70ec4214cd2f8ee563029
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518134"
---
# <a name="forms-authentication-configuration-and-advanced-topics-vb"></a>フォーム認証構成と高度なトピック (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_vb.pdf)

> このチュートリアルでは、さまざまなフォーム認証設定を確認し、forms 要素を使用して変更する方法を確認します。 これには、フォーム認証チケットのタイムアウト値のカスタマイズ、カスタム URL (login.aspx ではなくサインインなど) を使用したログインページの使用、およびクッキーレスフォーム認証チケットの使用の詳細が含まれます。

## <a name="introduction"></a>はじめに

前の[チュートリアル](an-overview-of-forms-authentication-vb.md)では、ASP.NET アプリケーションでフォーム認証を実装するために必要な手順を確認しました。これには、web.config で構成設定を指定し、認証されたユーザーと匿名ユーザーのさまざまなコンテンツを表示するためのログインページを作成します。 フォーム認証を使用するように web サイトを構成したことを思い出してください。 &lt;authentication&gt; 要素の mode 属性を Forms に設定します。 &lt;authentication&gt; 要素には、必要に応じて、フォーム認証設定の構成を指定できる、&lt;のフォーム&gt; 子要素を含めることができます。

このチュートリアルでは、さまざまなフォーム認証設定を確認し、&lt;forms&gt; 要素を使用して変更する方法を説明します。 これには、フォーム認証チケットのタイムアウト値のカスタマイズ、カスタム URL (login.aspx ではなくサインインなど) を使用したログインページの使用、およびクッキーレスフォーム認証チケットの使用の詳細が含まれます。 また、フォーム認証チケットのデータをより詳細に調査し、チケットのデータが検査や改ざんから安全であることを確認するために ASP.NET が講じる予防措置についても説明します。 最後に、フォーム認証チケットに追加のユーザーデータを格納する方法と、カスタムプリンシパルオブジェクトを使用してこのデータをモデル化する方法について説明します。

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>手順 1: &lt;フォーム&gt; 構成設定を調べる

ASP.NET フォーム認証システムは、アプリケーションごとにカスタマイズ可能な構成設定のいくつかあります。 これには、フォーム認証チケットの有効期間などの設定が含まれます。チケットにはどのような種類の保護が適用されますか。cookie なしの認証チケットが使用される条件を次に示します。ログインページへのパスです。その他の情報もあります。 既定値を変更するには、 [&lt;authentication&gt; 要素](https://msdn.microsoft.com/library/532aee0e.aspx)の子として[&lt;forms&gt; 要素](https://msdn.microsoft.com/library/1d3t3c61.aspx)を追加し、次のように XML 属性としてカスタマイズするプロパティ値を指定します。

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample1.xml)]

表1は、&lt;forms&gt; 要素を使用してカスタマイズできるプロパティをまとめたものです。 Web.config は XML ファイルであるため、左の列の属性名では大文字と小文字が区別されます。

| <strong>属性</strong> |                                                                                                                                                                                                                                     <strong>説明</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         cookieless         |                                                                                                                この属性は、URL に埋め込まれていると、cookie にどのような条件下で、認証チケットが格納されているを指定します。 使用可能な値: 既定値です。UseUri;自動検出します。値 (既定)。 手順 2 では、さらに詳しくは、この設定を検証します。                                                                                                                |
|         defaultUrl         |                                                                                                                                                         クエリ文字列に RedirectUrl 値が指定されていない場合に、ログインページからサインインした後にユーザーがリダイレクトされる URL を示します。 既定値は default.aspx です。                                                                                                                                                         |
|           domain           | Cookie ベースの認証チケットを使用する場合、この設定は、Cookie の domain の値を指定します。 既定値は、空の文字列です。そのため、ブラウザは発行元のドメイン (www.yourdomain.com) などを使用します。 この場合、admin.yourdomain.com などのサブドメインに要求を行うときに cookie は送信され<strong>ません</strong>。 すべてのサブドメインに渡される Cookie が必要な場合は、yourdomain.com に設定すると、 domain 属性をカスタマイズする必要があります。 |
|  enableCrossAppRedirects   |                                                                                                                                                                   同じサーバー上の他の web アプリケーションの Url にリダイレクトされたときに、認証されたユーザーを記憶するかどうかを示すブール値。 既定値は false です。                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      ログインページの URL です。 既定値は login.aspx です。                                                                                                                                                                                                                      |
|            name            |                                                                                                                                                                                                   Cookie ベースの認証チケットを使用する場合は、cookie の名前。 既定値はです.ASPXAUTH です.                                                                                                                                                                                                   |
|            path            |                                                                             Cookie ベースの認証チケットを使用する場合、この設定は、クッキーのパス属性を指定します。 Path 属性は、開発者は特定のディレクトリ階層のクッキーのスコープを制限できます。 既定値は/で、domain に対して行われた要求に認証チケットの Cookie を送信するようブラウザに通知します。                                                                              |
|         protection         |                                                                                                                                            フォーム認証チケットの保護にどのような手法を使用することを示します。 使用可能な値: すべて (既定)。暗号化。None;および検証します。 これらの設定は、手順 3 で詳しく説明します。                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                認証 cookie の送信に SSL 接続が必要かどうかを示すブール値。 既定値は false です。                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 シングルセッション中にユーザーがサイトにアクセスするたびに、認証 cookie のタイムアウトをリセットするかどうかを示すブール値。 既定値は、true です。 認証チケットタイムアウトポリシーの詳細については、「チケット s タイムアウト値の指定」セクションを参照してください。                                                                                                 |
|          timeout           |                                                                                                                               認証チケットのクッキーの有効期限が切れるまでの分、時間を指定します。 既定値は 30 です。 認証チケットタイムアウトポリシーの詳細については、「チケット s タイムアウト値の指定」セクションを参照してください。                                                                                                                               |

**表 1**: &lt;フォーム&gt; 要素の属性の概要

ASP.NET 2.0 以降では、既定のフォーム認証値は、.NET Framework のフォーム Authenticationconfiguration クラスにハードコーディングされています。 変更は、web.config ファイルでアプリケーションごとに適用する必要があります。 これは ASP.NET 1.x とは異なり、既定のフォーム認証値は machine.config ファイルに格納されています (したがって、machine.config の編集によって変更できます)。 ASP.NET のトピックで説明することは、1.x では、さまざまなフォーム認証システムの設定がある ASP.NET 2.0 では、異なる既定値の ASP.NET よりも拡張 1.x します。 ASP.NET 1.x 環境からアプリケーションを移行する場合は、これらの違いに注意することが重要です。 相違点の一覧について[は、&lt;forms&gt; 要素の技術ドキュメント](https://msdn.microsoft.com/library/1d3t3c61.aspx)を参照してください。

> [!NOTE]
> timeout、domain、および、path など、いくつかのフォーム認証設定は、結果として得られるフォーム認証チケット Cookie の詳細を指定します。 Cookie、そのしくみ、およびさまざまなプロパティの詳細については、[この cookie](http://www.quirksmode.org/js/cookies.html)に関するチュートリアルを参照してください。

### <a name="specifying-the-tickets-timeout-value"></a>チケットのタイムアウト値の指定

フォーム認証チケットは、id を表すトークンです。 Cookie ベースの認証チケットでは、このトークンは cookie の形式で保持され、要求のたびに web サーバーに送信されます。 トークンを所有することは、基本的には、ユーザー*名*を宣言し、ログインしているので、ユーザーの id をページアクセス全体で記憶できるようにするために使用されます。

フォーム認証チケットには、ユーザーの id だけでなく、トークンの整合性とセキュリティを確保するための情報も含まれています。 結局のところ、不正ユーザーが偽造トークンを作成したり、legit トークンを何らかの方法で変更したりできないようにしたいと考えています。

チケットに含まれるこのような情報の1つに、チケットが有効ではなくなった日付と時刻を示す*有効期限*があります。 FormsAuthenticationModule が認証チケットを検査するたびに、チケットの有効期限がまだ渡されていないことを確認します。 含まれている場合、チケットは無視され、ユーザーは匿名であると識別されます。 このセーフガードによって、リプレイ攻撃を防ぐことができます。 有効期限がない場合、ハッカーが自分のコンピューターに物理的にアクセスして cookie を使用してルートを取得することで、ユーザーの有効な認証チケットを手に入れなければならない場合は、この盗難された認証チケットを使用してサーバーに要求を送信することができます。エントリを取得します。 有効期限によってこのシナリオが妨げられることはありませんが、このような攻撃が成功するまでの期間は制限されます。

> [!NOTE]
> 手順 3. 認証チケットを保護するためにフォーム認証システムによって使用されるその他の手法について説明します。

認証チケットを作成するときに、フォーム認証システムはタイムアウト設定をコンサルティングして有効期限を決定します。 表1に示されているように、タイムアウト設定は既定で30分に設定されています。これは、フォーム認証チケットが作成されると、その有効期限が将来の30分の日時に設定されることを意味します。

有効期限は、フォーム認証チケットの有効期限が切れるまでの絶対時間を定義します。 しかし、通常、開発者は、ユーザーがサイトを見直しするたびにリセットされるスライド式有効期限を実装する必要があります。 この動作は、slidingExpiration の設定によって決まります。 True (既定値) に設定すると、FormsAuthenticationModule がユーザーを認証するたびに、チケットの有効期限が更新されます。 False に設定すると、各要求で有効期限が更新されないため、チケットが最初に作成されたときのタイムアウト時間 (分) がチケットの有効期限切れになります。

> [!NOTE]
> 認証チケットに格納されている有効期限は、11:34 2008 年8月2日のような絶対日付と時刻の値です。 さらに、日付と時刻は web サーバーのローカル時刻を基準としています。 この設計上の決定には、夏時間 (DST) に関する興味深い副作用がある場合があります。これは、米国のクロックが1時間進んでいる (web サーバーが夏時間が監視されているロケールでホストされていることを前提としていることを前提としています)。 ASP.NET の web サイトでは、DST の開始時刻 (午前2:00 時) に対して30分の有効期限があるとします。 2008年3月11日の午前1:55 に、訪問者がサイトにサインオンしたとします。 これにより、2008年3月11日に期限切れになるフォーム認証チケットが 2:25 AM (30 分後に30分) で生成されます。 ただし、2:00 がロールオーバーされると、DST が原因で、時計は 3:00 AM に移動します。 ユーザーがサインインしてから6分後に新しいページを読み込むと (午前3:01 時)、FormsAuthenticationModule はチケットの有効期限が切れたことを示し、ユーザーをログインページにリダイレクトします。 この認証チケットとその他の認証チケットタイムアウト特異と、回避策の詳細については、Stefan ・ *ackackASP.NET Professional 2.0 のセキュリティ、メンバーシップ、ロール管理*(ISBN: 978-0-7645-9698-8) のコピーを取得してください。

図1は、slidingExpiration が false に設定され、timeout が30に設定されている場合のワークフローを示しています。 ログイン時に生成される認証チケットには有効期限が含まれており、その後の要求ではこの値は更新されないことに注意してください。 チケットの有効期限が切れたことが FormsAuthenticationModule によって検出されると、そのチケットは破棄され、要求は匿名として扱われます。

[slidingExpiration が false の場合にフォーム認証チケットの有効期限をグラフィカルに表示 ![する](forms-authentication-configuration-and-advanced-topics-vb/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image1.png)

**図 01**: slidingExpiration が False の場合のフォーム認証チケットの有効期限のグラフィック表示 ([クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image3.png)されます)

図2は、slidingExpiration が true に設定され、timeout が30に設定されている場合のワークフローを示しています。 認証された要求を受信したとき (有効期限が切れていないチケットを含む)、その有効期限は、今後のタイムアウト時間 (分) に更新されます。

[slidingExpiration が true の場合にフォーム認証チケットのグラフィック表示を ![する](forms-authentication-configuration-and-advanced-topics-vb/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image4.png)

**図 02**: フォーム認証チケットのグラフィカル表現 (slidingExpiration が True の場合) ([クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image6.png)されます)

Cookie ベースの認証チケット (既定) を使用している場合、cookie には独自の expiries を指定することもできるため、この説明は少し複雑になります。 Cookie の有効期限 (またはその不足) は、cookie を破棄する必要があることをブラウザーに指示します。 Cookie の有効期限が不足している場合は、ブラウザーがシャットダウンすると破棄されます。 ただし、有効期限が存在する場合、有効期限に指定された日付と時刻が経過するまで、cookie はユーザーのコンピューターに保存されたままになります。 Cookie がブラウザーによって破棄されると、web サーバーには送信されなくなります。 したがって、cookie の破棄は、サイトからのユーザーのログアウトに似ています。

> [!NOTE]
> もちろん、ユーザーはコンピューターに保存されている cookie を事前に削除することができます。 Internet Explorer 7 で、[ツール]、[オプション] の順に移動し、[閲覧の履歴] セクションの [削除] ボタンをクリックします。 そこから、[cookie の削除] ボタンをクリックします。

フォーム認証システムは、 *persistcookie*パラメーターに渡された値に応じて、セッションベースまたは有効期限に基づく cookie を作成します。 FormsAuthentication クラスの GetAuthCookie、SetAuthCookie、および RedirectFromLoginPage の各メソッドが、 *username*と*persistcookie*の2つの入力パラメーターを受け取ることを思い出してください。 前のチュートリアルで作成したログインページには、永続的な cookie が作成されたかどうかを確認する [覚えておく] チェックボックスが含まれていました。 永続的な cookie は有効期限ベースです。非永続的な cookie はセッションベースです。

既に説明したタイムアウトと slidingExpiration の概念は、セッションと有効期限に基づく cookie の両方に同じように適用されます。 実行には軽微な違いが1つだけあります。 slidingTimeout を true に設定して有効期限に基づく cookie を使用すると、指定した時間の半分以上が経過した場合にのみ、cookie の有効期限が更新されます。

Web サイトの認証チケットタイムアウトポリシーを更新して、チケットが1時間 (60 分) 後にタイムアウトになり、スライド式有効期限を使用するようにしてみましょう。 この変更を反映するには、web.config ファイルを更新し、次のマークアップを使用して、&lt;authentication&gt; 要素に &lt;forms&gt; 要素を追加します。

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>Login.aspx 以外のログインページ URL を使用する

FormsAuthenticationModule は、承認されていないユーザーをログインページに自動的にリダイレクトするため、ログインページの URL を知る必要があります。 この URL は &lt;forms&gt; 要素の loginUrl 属性によって指定され、既定で login.aspx に設定されます。 既存の web サイトを介して移植する場合は、別の URL を持つログインページが既に存在している可能性があります。これには既にブックマークがあり、検索エンジンによってインデックスが作成されています。 既存のログインページの名前を login.aspx に変更したり、リンクやユーザーのブックマークを破損させたりする代わりに、loginUrl 属性を変更してログインページを指すようにすることができます。

たとえば、ログインページの名前が loginUrl で、ユーザーディレクトリにある場合は、次のように、構成設定の値を ~/Users/SignIn.aspx にすることができます。

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample3.xml)]

現在のアプリケーションには、login.aspx という名前のログインページが既に存在するため、&lt;forms&gt; 要素でカスタム値を指定する必要はありません。

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>手順 2: Cookie なしのフォーム認証チケットの使用

既定では、フォーム認証システムは、認証チケットを cookies コレクションに格納するか、サイトにアクセスするユーザーエージェントに基づいて URL に埋め込むかを決定します。 Internet Explorer、Firefox、Opera、Safari などのすべてのメインストリームデスクトップブラウザーは cookie をサポートしていますが、すべてのモバイルデバイスではサポートされていません。

フォーム認証システムで使用される cookie ポリシーは、&lt;forms&gt; 要素の cookie なしの設定に依存します。これには、次の4つの値のいずれかを割り当てることができます。

- UseCookies-cookie ベースの認証チケットが常に使用されることを指定します。
- UseUri-cookie ベースの認証チケットが使用されないことを示します。
- 自動検出-デバイスプロファイルで cookie がサポートされていない場合、cookie ベースの認証チケットは使用されません。デバイスプロファイルで cookie がサポートされている場合は、プローブメカニズムを使用して cookie が有効かどうかを判断します。
- UseDeviceProfile-既定値。では、デバイスプロファイルで cookie がサポートされている場合にのみ、cookie ベースの認証チケットが使用されます。 プローブメカニズムは使用されません。

自動検出と UseDeviceProfile の設定は、cookie ベースの認証チケットを使用するか、クッキーレス認証チケットを使用するかにかかわらず、突き止めるの*デバイスプロファイル*に依存します。 ASP.NET は、さまざまなデバイスのデータベースとその機能を保持しています。たとえば、cookie をサポートしているかどうか、サポートされている JavaScript のバージョンなどです。 デバイスが web サーバーから web ページを要求するたびに、デバイスの種類を識別する*ユーザーエージェント*HTTP ヘッダーを介して送信されます。 ASP.NET は、指定されたユーザーエージェント文字列と、そのデータベースで指定されている対応するプロファイルを自動的に照合します。

> [!NOTE]
> このデバイス機能のデータベースは、[ブラウザー定義ファイルスキーマ](https://msdn.microsoft.com/library/ms228122.aspx)に準拠した多数の XML ファイルに格納されています。 既定のデバイスプロファイルファイルは%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers. にあります。 アプリケーションのアプリ\_ブラウザーフォルダーにカスタムファイルを追加することもできます。 詳細については、「[方法: ASP.NET Web ページでブラウザーの種類を検出する](https://msdn.microsoft.com/library/3yekbd5b.aspx)」を参照してください。

既定の設定は UseDeviceProfile であるため、cookie がサポートされていないことをプロファイルが報告するデバイスからサイトにアクセスするときに、cookie なしのフォーム認証チケットが使用されます。

### <a name="encoding-the-authentication-ticket-in-the-url"></a>URL に認証チケットをエンコードする

Cookie は、ブラウザーから特定の web サイトへの要求ごとに情報を含めるための自然なメディアです。そのため、訪問デバイスが cookie をサポートしている場合は、既定のフォーム認証設定で cookie が使用されます。 Cookie がサポートされていない場合は、クライアントからサーバーに認証チケットを渡すための代替手段を採用する必要があります。 Cookie なしの環境でよく使用される回避策は、URL の cookie データをエンコードすることです。

URL 内にそのような情報を埋め込む方法を確認する最善の方法は、cookie なしの認証チケットをサイトに強制的に使用させることです。 これを実現するには、cookie なしの構成設定を UseUri に設定します。

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample4.xml)]

この変更を行ったら、ブラウザーを使用してサイトにアクセスします。 匿名ユーザーとしてアクセスすると、Url は以前と同じように表示されます。 たとえば、default.aspx ページにアクセスすると、ブラウザーのアドレスバーに次の URL が表示されます。

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

ただし、ログイン時には、フォーム認証チケットが URL に埋め込まれます。 たとえば、ログインページにアクセスし、Sam としてログインした後、default.aspx ページに戻りますが、今回の URL は次のようになります。

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

フォーム認証チケットが URL 内に埋め込まれています。 文字列 (F (jaIOIDTJxIr12xYS-\_VVgkqKCVAuIoW30Bu0diWi6flQC) は、16進数でエンコードされた認証チケット情報を表し、通常は cookie 内に格納されているのと同じデータです。

クッキーレス認証チケットを機能させるには、システムがページ上のすべての Url をエンコードして認証チケットデータを含める必要があります。そうしないと、ユーザーがリンクをクリックすると認証チケットが失われます。 さいわいにも、この埋め込みロジックは自動的に実行されます。 この機能をデモンストレーションするには、default.aspx ページを開き、HyperLink コントロールを追加して、Text プロパティと NavigateUrl プロパティをそれぞれ Test Link に設定します。 実際には、プロジェクトには .aspx という名前のページが存在しないという問題はありません。

変更内容を default.aspx に保存し、ブラウザーからアクセスします。 フォーム認証チケットが URL に埋め込まれるように、サイトにログオンします。 次に、default.aspx から、[リンクのテスト] リンクをクリックします。 なぜでしょうか? ".Aspx" という名前のページが存在しない場合、404エラーが発生しますが、ここでは重要なことではありません。 代わりに、ブラウザーのアドレスバーにフォーカスを移動します。 URL にはフォーム認証チケットが含まれていることに注意してください。

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

リンクの .aspx ページ .aspx は、認証チケットが含まれている URL に自動的に変換されました。コードを作成する必要はありませんでした。 フォーム認証チケットは、 http://または/で始まらないハイパーリンクの URL に自動的に埋め込まれます。 ハイパーリンクが応答の呼び出しで表示されているかどうかは問題ではありません。リダイレクト、ハイパーリンクコントロール、またはアンカー HTML 要素 (つまり &lt;href = "..."&gt;...&lt;/a&gt;)。 URL が http://www.someserver.com/SomePage.aspx や/SomePage.aspx のようなものではない限り、フォーム認証チケットが埋め込まれます。

> [!NOTE]
> Cookie なしのフォーム認証チケットは、cookie ベースの認証チケットと同じタイムアウトポリシーに従います。 ただし、認証チケットは URL に直接埋め込まれるので、cookie なしの認証チケットはリプレイ攻撃を受けやすくなります。 たとえば、web サイトにアクセスしてログインし、電子メールの URL を同僚に貼り付けるユーザーがいるとします。 期限が切れる前に同僚がそのリンクをクリックすると、電子メールを送信したユーザーとしてログインします。

## <a name="step-3-securing-the-authentication-ticket"></a>手順 3: 認証チケットをセキュリティで保護する

フォーム認証チケットは、cookie で送信されるか、URL 内に直接埋め込まれます。 認証チケットには、id 情報だけでなく、ユーザーデータを含めることもできます (手順 4. を参照)。 そのため、チケットのデータは、暗号化されていないこと、および (さらに重要な) フォーム認証システムによってチケットが改ざんされていないことを保証できることが重要です。

チケットのデータのプライバシーを確保するために、フォーム認証システムはチケットデータを暗号化できます。 チケットデータの暗号化に失敗すると、機密情報がネットワーク経由でプレーンテキストで送信されます。

チケットの信頼性を保証するために、フォーム認証システムはチケットを*検証*する必要があります。 検証とは、特定のデータの一部が変更されていないことを確認し、 *[メッセージ認証コード (MAC)](http://en.wikipedia.org/wiki/Message_authentication_code)* を使用して実行することを意味します。 簡単に言うと、MAC は、検証する必要があるデータ (この場合はチケット) を識別する小さな情報です。 MAC によって表されるデータが変更された場合、MAC とデータは一致しません。 さらに、ハッカーがデータを変更し、変更されたデータに対応する独自の MAC を生成することが困難になります。

チケットを作成 (または変更) する場合、フォーム認証システムは MAC を作成し、チケットのデータに接続します。 後続の要求が到着すると、フォーム認証システムは、MAC とチケットデータを比較してチケットデータの信頼性を検証します。 図3は、このワークフローをグラフィカルに示しています。

[MAC でチケットの信頼性を保証 ![](forms-authentication-configuration-and-advanced-topics-vb/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image7.png)

**図 03**: チケットの信頼性は MAC で保証されます ([クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image9.png)されます)

認証チケットに適用されるセキュリティ対策は、&lt;forms&gt; 要素の保護設定によって異なります。 保護設定は、次の3つの値のいずれかに割り当てることができます。

- [すべて]-チケットは、暗号化され、デジタル署名されています (既定)。
- 暗号化のみの暗号化が適用されます。 MAC は生成されません。
- なし-チケットは暗号化もデジタル署名もされません。
- 検証-MAC が生成されますが、チケットデータはプレーンテキストでネットワーク経由で送信されます。

Microsoft では、[すべて] 設定を使用することを強くお勧めします。

### <a name="setting-the-validation-and-decryption-keys"></a>検証キーと復号化キーの設定

認証チケットの暗号化と検証のためにフォーム認証システムによって使用される暗号化アルゴリズムとハッシュアルゴリズムは、web.config の[&lt;machineKey&gt; 要素](https://msdn.microsoft.com/library/w8h3skw9.aspx)を使用してカスタマイズできます。表2に、&lt;machineKey&gt; 要素の属性とその使用可能な値の概要を示します。

| **属性** | **説明** |
| --- | --- |
| decryption | 暗号化に使用されるアルゴリズムを示します。 この属性には、次の4つの値のいずれかを指定できます。-Auto-既定値。decryptionKey 属性の長さに基づいてアルゴリズムを決定します。 -AES- [Advanced Encryption Standard (aes)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)アルゴリズムを使用します。 -DES-[データ暗号化標準 (DES)](http://en.wikipedia.org/wiki/Data_Encryption_Standard)を使用します。このアルゴリズムは計算上脆弱であると見なされるため、使用しないでください。 -3DES- [TRIPLE des](http://en.wikipedia.org/wiki/Triple_DES)アルゴリズムを使用します。これは、des アルゴリズムを3回適用することで機能します。 |
| decryptionKey | 暗号化アルゴリズムによって使用される秘密キー。 この値は、(暗号化解除の値に基づいて) 適切な長さの16進数文字列であるか、自動生成であるか、または IsolateApps で値が追加されたかのいずれかである必要があります。 IsolateApps を追加すると、ASP.NET は、アプリケーションごとに一意の値を使用するように指示します。 既定値は自動生成、IsolateApps です。 |
| validation | 検証に使用されるアルゴリズムを示します。 この属性には、次の4つの値のいずれかを指定できます。-AES-Advanced Encryption Standard (AES) アルゴリズムを使用します。 -MD5-では、[メッセージダイジェスト 5 (MD5)](http://en.wikipedia.org/wiki/MD5)アルゴリズムが使用されます。 -SHA1- [sha1](http://en.wikipedia.org/wiki/Sha1)アルゴリズム (既定値) を使用します。 -3DES-Triple DES アルゴリズムを使用します。 |
| validationKey | 検証アルゴリズムによって使用される秘密キー。 この値は、適切な長さの16進数文字列 (検証の値に基づく)、自動生成、または IsolateApps を使用して追加された値のいずれかである必要があります。 IsolateApps を追加すると、ASP.NET は、アプリケーションごとに一意の値を使用するように指示します。 既定値は自動生成、IsolateApps です。 |

**表 2**: &lt;MachineKey&gt; 要素の属性

これらの暗号化と検証のオプション、およびさまざまなアルゴリズムの長所と短所については、このチュートリアルでは説明しません。 これらの問題の詳細については、使用する暗号化と検証アルゴリズム、使用するキーの長さ、およびこれらのキーを生成する方法についてのガイダンスを参照してください。 *Professional ASP.NET 2.0 のセキュリティ、メンバーシップ、およびロール管理*に関する記事をご覧ください。

既定では、暗号化と検証に使用されるキーはアプリケーションごとに自動的に生成され、これらのキーはローカルセキュリティ機関 (LSA) に格納されます。 つまり、既定の設定では、web サーバーによって web サーバーとアプリケーションごとに一意のキーが保証されます。 そのため、この既定の動作は、次の2つのシナリオでは機能しません。

- **Web**ファーム- [web ファーム](http://en.wikipedia.org/wiki/Web_farm)のシナリオでは、スケーラビリティと冗長性を確保するために、1つの web アプリケーションが複数の web サーバーでホストされます。 各受信要求は、ファーム内のサーバーにディスパッチされます。つまり、ユーザーのセッションの有効期間にわたって、さまざまな要求を処理するためにさまざまなサーバーを使用できます。 そのため、1つのサーバーで作成、暗号化、および検証されるフォーム認証チケットをファーム内の別のサーバーで復号化および検証できるように、各サーバーは同じ暗号化および検証キーを使用する必要があります。
- **クロスアプリケーションチケット共有**-1 台の web サーバーで複数の ASP.NET アプリケーションをホストできます。 これらの異なるアプリケーションで1つのフォーム認証チケットを共有する必要がある場合は、暗号化キーと検証キーを確実に一致させることが不可欠です。

Web ファームで作業するときに、同じサーバー上の複数のアプリケーション間で認証チケットを共有する場合は、decryptionKey 値と validationKey 値が一致するように、影響を受けるアプリケーションの &lt;machineKey&gt; 要素を構成する必要があります。

上記のいずれのシナリオもサンプルアプリケーションには適用されませんが、明示的な decryptionKey と validationKey の値を指定して、使用するアルゴリズムを定義することはできます。 &lt;machineKey&gt; 設定を Web.config ファイルに追加します。

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample5.xml)]

詳細については、 [「方法: ASP.NET 2.0 で MachineKey を構成する」](https://msdn.microsoft.com/library/ms998288.aspx)を参照してください。

> [!NOTE]
> DecryptionKey と validationKey の値は、[上田 Gibson](http://www.grc.com/stevegibson.htm)の[完全なパスワードの web ページ](https://www.grc.com/passwords.htm)から取得されました。この web ページでは、ページにアクセスするたびに64のランダムな16進数文字が生成されます。 これらのキーが実稼働アプリケーションにもたらす可能性を低減するには、上記のキーをランダムに生成されたキーに置き換えることをお勧めします。

## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>手順 4: チケットに追加のユーザーデータを格納する

多くの web アプリケーションは、現在ログオンしているユーザーに関する情報を表示したり、ページの表示を基にしたりします。 たとえば、web ページには、ユーザーの名前と、その最後にログオンした日付が表示されます。 フォーム認証チケットには、現在ログオンしているユーザーのユーザー名が格納されますが、その他の情報が必要な場合は、ページはユーザーストア (通常はデータベース) にアクセスして、認証チケットに格納されていない情報を参照する必要があります。

少しのコードでは、フォーム認証チケットに追加のユーザー情報を格納できます。 このようなデータは、[フォーム Authenticationticket クラス](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)の[UserData プロパティ](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)を使用して表すことができます。 これは、一般的に必要なユーザーについての少量の情報を格納するのに便利な場所です。 UserData プロパティに指定された値は認証チケット cookie の一部として含まれ、他のチケットフィールドと同様に、フォーム認証システムの構成に基づいて暗号化および検証されます。 既定では、UserData は空の文字列です。

認証チケットにユーザーデータを格納するには、ログインページにコードを記述し、ユーザー固有の情報を取得してチケットに保存する必要があります。 UserData は String 型のプロパティであるため、格納されるデータは文字列として適切にシリアル化される必要があります。 たとえば、ユーザーストアに各ユーザーの誕生日と雇用者の名前が含まれており、これらの2つのプロパティ値を認証チケットに格納したいとします。 これらの値を文字列にシリアル化するには、ユーザーの生年月日の文字列にパイプ (|) を付け、その後に雇用者名を連結します。 1974年8月15日に公開され、Northwind Traders で動作するユーザーについては、UserData プロパティを string: 1974-08-15 |Northwind Traders。

チケットに格納されているデータにアクセスする必要がある場合は常に、現在の要求のフォーム認証チケットを取得し、UserData プロパティを逆シリアル化します。 誕生日と雇用者名の例の場合は、区切り記号 (|) に基づいて、UserData 文字列を2つの部分文字列に分割します。

[![追加のユーザー情報を認証チケットに格納することができます。](forms-authentication-configuration-and-advanced-topics-vb/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image10.png)

**図 04**: 追加のユーザー情報を認証チケットに格納できる ([クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image12.png)されます)

### <a name="writing-information-to-userdata"></a>UserData への情報の書き込み

残念ながら、フォーム認証チケットにユーザー固有の情報を追加することは、予想されるほど簡単ではありません。 フォーム Authenticationticket クラスの UserData プロパティは読み取り専用で、フォーム Authenticationticket クラスコンストラクターを使用してのみ指定できます。 コンストラクターで UserData プロパティを指定する場合は、チケットのその他の値 (ユーザー名、発行日、有効期限など) も指定する必要があります。 前のチュートリアルでログインページを作成したときに、FormsAuthentication クラスによってすべての処理が行われました。 フォーム Authenticationticket に UserData を追加するときは、FormsAuthentication クラスによって既に提供されている機能の多くをレプリケートするコードを記述する必要があります。

ユーザーに関する追加情報を認証チケットに記録するように login.aspx ページを更新することで、UserData を操作するために必要なコードについて説明します。 このユーザーストアには、ユーザーが作業している会社とそのタイトルに関する情報が含まれており、この情報を認証チケットに取り込む必要があるとします。 次のようなコードになるように、login.aspx ページの LoginButton Click イベントハンドラーを更新します。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample6.vb)]

このコードを1行ずつステップ実行してみましょう。 このメソッドは、まず、users、パスワード、companyName、およびタイトル Atcompany という4つの文字列配列を定義します。 これらの配列には、システム内のユーザーアカウントのユーザー名、パスワード、会社名、およびタイトルが格納されています。これには、Scott、Jisun、および Sam の3つがあります。 実際のアプリケーションでは、これらの値は、ページのソースコード内でハードコーディングされていないユーザーストアから照会されます。

前のチュートリアルでは、指定された資格情報が有効であった場合は、単に FormsAuthentication ページ (UserName, RememberMe) を呼び出しました。これにより、次の手順が実行されます。

1. フォーム認証チケットが作成されました
2. チケットを適切なストアに書き込みました。 Cookie ベースの認証チケットでは、ブラウザーの cookies コレクションが使用されます。cookie を使用しない認証チケットの場合、チケットデータは URL にシリアル化されます。
3. 適切なページにユーザーをリダイレクトします。

これらの手順は、上記のコードでレプリケートされています。 最初に、UserData プロパティに格納する文字列は、会社名とタイトルを組み合わせて、2つの値をパイプ文字 (|) で区切ることで形成されます。

Dim userDataString As String = String. Concat (companyName (i), "|", タイトル Atcompany (i))

次に、FormsAuthentication メソッドが呼び出されます。このメソッドは認証チケットを作成し、構成設定に従って暗号化して検証し、HttpCookie オブジェクトに配置します。

HttpCookie = FormsAuthentication (ユーザー名、RememberMe) として Dim authCookie を作成します。

Cookie 内に埋め込まれている FormAuthenticationTicket を操作するには、cookie 値を渡す Formauthentauthentication クラスの[復号化メソッド](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)を呼び出す必要があります。

Dim ticket As フォーム Authenticationticket = FormsAuthentication (authCookie. 値)

次に、既存のフォーム Authenticationticket の値に基づいて、*新しい*フォーム authenticationticket インスタンスを作成します。 ただし、この新しいチケットには、ユーザー固有の情報 (userDataString) が含まれています。

Dim newTicket As フォーム Authenticationticket = New フォーム Authenticationticket (チケット)バージョン、チケット。名前、チケット。IssueDate、ticket。有効期限、チケット。IsPersistent、userDataString)

次に、 [encrypt メソッド](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)を呼び出して新しいフォーム authenticationticket インスタンスを暗号化 (および検証) し、この暗号化 (および検証済み) データを authcookie に戻します。

authCookie.Value = FormsAuthentication.Encrypt(newTicket)

最後に、authCookie が応答に追加されます。 Cookies コレクションと GetRedirectUrl メソッドは、ユーザーを送信するための適切なページを決定するために呼び出されます。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample7.vb)]

UserData プロパティは読み取り専用であり、FormsAuthentication クラスには、GetAuthCookie、SetAuthCookie、または RedirectFromLoginPage の各メソッドで UserData 情報を指定するメソッドが用意されていないため、すべてのコードが必要です。

> [!NOTE]
> 上記のコードでは、cookie ベースの認証チケットにユーザー固有の情報が格納されています。 URL へのフォーム認証チケットのシリアル化を行うクラスは、.NET Framework 内部にあります。 長い話ですが、ユーザーデータを cookie なしのフォーム認証チケットに格納することはできません。

### <a name="accessing-the-userdata-information"></a>UserData 情報へのアクセス

この時点で、各ユーザーの会社名とタイトルは、ログイン時にフォーム認証チケットの UserData プロパティに格納されます。 この情報には、任意のページの認証チケットからアクセスできます。ユーザーストアへの出張は必要ありません。 UserData プロパティからこの情報を取得する方法を説明するために、default.aspx を更新して、ようこそメッセージにユーザーの名前だけでなく、勤務先の会社とそのタイトルも含まれるようにしてみましょう。

現在、default.aspx には、WelcomeBackMessage という名前のラベルコントロールを持つ認証 Atedmessagepanel パネルが含まれています。 このパネルは、認証されたユーザーにのみ表示されます。 次のように、default.aspx のページのコード\_読み込みイベントハンドラーを更新します。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample8.vb)]

要求の IsAuthenticated が True の場合、WelcomeBackMessage の Text プロパティは最初に "Welcome back, *Username*" に設定されます。 次に、FormsIdentity オブジェクトにキャストして、基になるフォーム Authenticationticket にアクセスできるようにします。 フォーム Authenticationticket を作成したら、UserData プロパティを会社名とタイトルに逆シリアル化します。 これは、文字列をパイプ文字に分割することで実現されます。 次に、会社名とタイトルが WelcomeBackMessage ラベルに表示されます。

図5に、この表示の動作のスクリーンショットを示します。 Scott としてログインすると、Scott の会社と肩書きを含むウェルカムメッセージが表示されます。

[現在ログオンしているユーザーの会社とタイトルが ![表示されます。](forms-authentication-configuration-and-advanced-topics-vb/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image13.png)

**図 05**: 現在ログオンしているユーザーの会社とタイトルが表示される ([クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image15.png)されます)

> [!NOTE]
> 認証チケットの UserData プロパティは、ユーザーストアのキャッシュとして機能します。 キャッシュと同様に、基になるデータが変更されたときに更新する必要があります。 たとえば、ユーザーが自分のプロファイルを更新できる web ページがある場合、UserData プロパティにキャッシュされたフィールドを更新して、ユーザーが行った変更を反映する必要があります。

## <a name="step-5-using-a-custom-principal"></a>手順 5: カスタムプリンシパルの使用

各受信要求で、FormsAuthenticationModule はユーザーの認証を試みます。 有効期限が切れていない認証チケットが存在する場合、FormsAuthenticationModule は新しい GenericPrincipal オブジェクトに Httpcontext.current プロパティを割り当てます。 この GenericPrincipal オブジェクトは、フォーム認証チケットへの参照を含む FormsIdentity 型の Id を持ちます。 GenericPrincipal クラスには、IPrincipal を実装するクラスに必要な最小限の機能が含まれています。これには、Identity プロパティと IsInRole メソッドが含まれているだけです。

プリンシパルオブジェクトには、ユーザーが属するロールを指定し、id 情報を提供するための2つの役割があります。 これは、IPrincipal インターフェイスの IsInRole (*roleName*) メソッドと Identity プロパティによってそれぞれ実現されます。 GenericPrincipal クラスを使用すると、ロール名の文字列配列をコンストラクターを使用して指定できます。IsInRole (*rolename*) メソッドは、渡された*roleName*が文字列配列内に存在するかどうかを確認するだけです。 FormsAuthenticationModule で GenericPrincipal が作成されると、GenericPrincipal のコンストラクターに空の文字列配列が渡されます。 その結果、IsInRole を呼び出すと、常に False が返されます。

GenericPrincipal クラスは、ロールが使用されないほとんどのフォームベース認証シナリオのニーズを満たしています。 既定のロール処理が不十分な場合、またはカスタム IIdentity オブジェクトをユーザーに関連付ける必要がある場合は、認証ワークフロー中にカスタムの IPrincipal オブジェクトを作成し、それを HttpContext. User プロパティに割り当てることができます。

> [!NOTE]
> 今後のチュートリアルでは、ASP の場合について説明します。NET の Roles framework は、 [roleprincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)型のカスタムプリンシパルオブジェクトを作成し、フォーム認証で作成された genericprincipal オブジェクトを上書きします。 これは、ロールフレームワークの API とのインターフェイスとして、プリンシパルの IsInRole メソッドをカスタマイズするために使用されます。

まだロールを使用しているわけではないため、この時点でカスタムプリンシパルを作成する唯一の理由は、カスタム IIdentity オブジェクトをプリンシパルに関連付けることです。 手順 4. では、認証チケットの UserData プロパティに追加のユーザー情報を保存することを検討しました。特に、ユーザーの会社名と役職です。 ただし、UserData 情報にアクセスできるのは認証チケットだけです。その後、シリアル化された文字列としてのみアクセスできます。つまり、チケットに格納されているユーザー情報を表示する必要があるときに、UserData プロパティを解析する必要があります。

IIdentity を実装するクラスを作成し、CompanyName および Title プロパティを含めることで、開発者のエクスペリエンスを向上させることができます。 このようにすることで、開発者は、現在ログオンしているユーザーの会社名とタイトルに CompanyName プロパティと Title プロパティを直接アクセスできます。このとき、UserData プロパティを解析する方法を知る必要はありません。

### <a name="creating-the-custom-identity-and-principal-classes"></a>カスタム Id およびプリンシパルクラスの作成

このチュートリアルでは、アプリ\_コードフォルダーにカスタムプリンシパルオブジェクトと id オブジェクトを作成します。 まず、アプリ\_コードフォルダーをプロジェクトに追加します。ソリューションエクスプローラーでプロジェクト名を右クリックし、[ASP.NET フォルダーの追加] オプションを選択し、[アプリ\_コード] を選択します。 アプリ\_コードフォルダーは、web サイトに固有のクラスファイルを保持する特別な ASP.NET フォルダーです。

> [!NOTE]
> アプリ\_コードフォルダーは、Web サイトプロジェクトモデルを使用してプロジェクトを管理する場合にのみ使用してください。 [Web アプリケーションプロジェクトモデル](https://msdn.microsoft.com/asp.net/Aa336618.aspx)を使用している場合は、標準のフォルダーを作成し、そのにクラスを追加します。 たとえば、クラスという名前の新しいフォルダーを追加し、そこにコードを配置することができます。

次に、2つの新しいクラスファイルをアプリ\_コードフォルダーに追加します。1つは CustomIdentity .vb、もう1つは Customidentity という名前です。

[CustomIdentity クラスおよび Customidentity クラスをプロジェクトに追加 ![には](forms-authentication-configuration-and-advanced-topics-vb/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image16.png)

**図 06**: Customidentity クラスと Customidentity クラスをプロジェクトに追加[する (クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image18.png)されます)

CustomIdentity クラスは、AuthenticationType、IsAuthenticated、および Name の各プロパティを定義する IIdentity インターフェイスを実装する役割を担います。 これらの必須プロパティに加えて、基になるフォーム認証チケットと、ユーザーの会社名とタイトルのプロパティを公開することに関心があります。 CustomIdentity クラスに次のコードを入力します。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample9.vb)]

クラスにはフォーム Authenticationticket メンバー変数 (\_ticket) が含まれており、このチケット情報はコンストラクターを通じて提供される必要があることに注意してください。 このチケットデータは、id の名前を返すために使用されます。UserData プロパティは、CompanyName プロパティと Title プロパティの値を返すために解析されます。

次に、CustomPrincipal クラスを作成します。 この時点でのロールは考慮されないため、CustomPrincipal クラスのコンストラクターは Customprincipal オブジェクトのみを受け入れます。その IsInRole メソッドは常に False を返します。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample10.vb)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>入力方向の要求のセキュリティコンテキストに CustomPrincipal オブジェクトを割り当てる

これで、既定の IIdentity 仕様を拡張するクラスが追加されました。このクラスには、CompanyName プロパティと Title プロパティに加えて、カスタム id を使用するカスタムプリンシパルクラスが含まれています。 ASP.NET パイプラインにステップインし、カスタムプリンシパルオブジェクトを受信要求のセキュリティコンテキストに割り当てる準備ができました。

ASP.NET パイプラインは、受信要求を受け取り、いくつかの手順で処理します。 各ステップでは、特定のイベントが発生します。これにより、開発者は ASP.NET パイプラインをタップし、ライフサイクルの特定の時点で要求を変更できます。 たとえば、FormsAuthenticationModule は、ASP.NET が[AuthenticateRequest イベント](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)を発生させるまで待機し、その時点で認証チケットの受信要求を検査します。 認証チケットが見つかると、GenericPrincipal オブジェクトが作成され、HttpContext. User プロパティに割り当てられます。

AuthenticateRequest イベントが発生すると、ASP.NET パイプラインによって[PostAuthenticateRequest イベント](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)が発生します。ここで、FormsAuthenticationModule によって作成された genericprincipal オブジェクトを customprincipal オブジェクトのインスタンスに置き換えることができます。 図7は、このワークフローを示しています。

[![GenericPrincipal は、PostAuthenticationRequest イベントの CustomPrincipal に置き換えられます。](forms-authentication-configuration-and-advanced-topics-vb/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image19.png)

**図 07**: Genericprincipal は PostAuthenticationRequest イベントの Customprincipal に置き換えられます ([クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image21.png)されます)

ASP.NET pipeline イベントに応答してコードを実行するために、global.asax で適切なイベントハンドラーを作成するか、独自の HTTP モジュールを作成することができます。 このチュートリアルでは、global.asax でイベントハンドラーを作成します。 まず、global.asax を web サイトに追加します。 ソリューションエクスプローラーでプロジェクト名を右クリックし、「global.asax」という名前のグローバルアプリケーションクラスの項目を追加します。

[global.asax ファイルを Web サイトに追加 ![には](forms-authentication-configuration-and-advanced-topics-vb/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image22.png)

**図 08**: グローバルな global.asax ファイルを web サイトに追加[する (クリックすると、フルサイズの画像が表示](forms-authentication-configuration-and-advanced-topics-vb/_static/image24.png)されます)

既定の global.asax テンプレートには、開始、終了、および[エラーイベント](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)など、多数の ASP.NET パイプラインイベントのイベントハンドラーが含まれています。 これらのイベントハンドラーは、このアプリケーションでは不要であるため、削除してもかまいません。 興味のあるイベントは PostAuthenticateRequest です。 Global.asax ファイルを更新して、マークアップが次のように見えるようにします。

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample11.aspx)]

アプリケーション\_OnPostAuthenticateRequest メソッドは、ASP.NET ランタイムが PostAuthenticateRequest イベントを発生させるたびに実行されます。このイベントは、受信ページの要求ごとに1回発生します。 イベントハンドラーは、ユーザーが認証されているかどうか、およびフォーム認証によって認証されたかどうかを確認することによって開始されます。 その場合は、新しい CustomIdentity オブジェクトが作成され、現在の要求の認証チケットがコンストラクターに渡されます。 その後、CustomPrincipal オブジェクトが作成され、作成された Customprincipal オブジェクトがコンストラクターに渡されます。 最後に、現在の要求のセキュリティコンテキストが、新しく作成された CustomPrincipal オブジェクトに割り当てられます。

最後の手順として、CustomPrincipal オブジェクトと要求のセキュリティコンテキストの関連付け-は、Thread.currentprincipal という2つのプロパティにプリンシパルを割り当てます。 これらの2つの割り当ては、ASP.NET でのセキュリティコンテキストの処理方法によって必要になります。 .NET Framework は、実行中の各スレッドにセキュリティコンテキストを関連付けます。この情報は、 [Thread オブジェクト](https://msdn.microsoft.com/library/system.threading.thread.aspx)の[thread.currentprincipal プロパティ](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)を使用して、IPrincipal オブジェクトとして取得できます。 紛らわしいのは、ASP.NET には独自のセキュリティコンテキスト情報 (HttpContext. User) があることです。

特定のシナリオでは、セキュリティコンテキストを決定するときに Thread.currentprincipal プロパティが検査されます。その他のシナリオでは、HttpContext. User が使用されます。 たとえば、.NET のセキュリティ機能を使用すると、クラスをインスタンス化したり特定のメソッドを呼び出したりできるユーザーまたはロールを宣言的に指定できます (「 [PrincipalPermissionAttributes を使用してビジネスおよびデータレイヤーに承認規則を追加](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)する」を参照してください)。 これらの宣言型技法は、内部の下で Thread.currentprincipal プロパティを使用してセキュリティコンテキストを決定します。

その他のシナリオでは、HttpContext. User プロパティが使用されます。 たとえば、前のチュートリアルでは、このプロパティを使用して、現在ログオンしているユーザーのユーザー名を表示しました。 明確に言うと、Thread.currentprincipal プロパティと HttpContext プロパティのセキュリティコンテキスト情報が一致している必要があります。

ASP.NET ランタイムは、これらのプロパティ値を自動的に同期します。 ただし、この同期は、AuthenticateRequest イベントの後、PostAuthenticateRequest イベントの*前に*発生します。 そのため、PostAuthenticateRequest イベントにカスタムプリンシパルを追加する場合は、Thread.currentprincipal または Thread.currentprincipal と HttpContext を手動で割り当てる必要があります。ユーザーは同期しません。この問題の詳細については、「 [thread.currentprincipal と.](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) .」を参照してください。

### <a name="accessing-the-companyname-and-title-properties"></a>CompanyName および Title プロパティへのアクセス

要求が到着し、ASP.NET エンジンにディスパッチされるたびに、global.asax の Application\_OnPostAuthenticateRequest イベントハンドラーが起動されます。 要求が FormsAuthenticationModule によって正常に認証された場合、イベントハンドラーは、フォーム認証チケットに基づく Customprincipal オブジェクトを含む新しい CustomPrincipal オブジェクトを作成します。 このロジックを使用すると、現在ログオンしているユーザーの会社名とタイトルに関する情報に簡単にアクセスできます。

ページに戻り、default.aspx のイベントハンドラーを読み込み\_ます。手順4では、フォーム認証チケットを取得し、UserData プロパティを解析してユーザーの会社名とタイトルを表示するコードを記述しました。 現在使用されている CustomPrincipal オブジェクトと Customprincipal オブジェクトを使用して、チケットの UserData プロパティから値を解析する必要はありません。 代わりに、単に CustomIdentity オブジェクトへの参照を取得し、CompanyName プロパティと Title プロパティを使用します。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample12.vb)]

## <a name="summary"></a>まとめ

このチュートリアルでは、web.config を使用してフォーム認証システムの設定をカスタマイズする方法について説明します。認証チケットの有効期限がどのように処理されるか、および暗号化と検証のセーフガードを使用して、検査と変更からチケットを保護する方法について説明しました。 最後に、認証チケットの UserData プロパティを使用して、チケット自体に追加のユーザー情報を格納します。また、カスタムプリンシパルオブジェクトと id オブジェクトを使用して、開発者にとってわかりやすい方法でこの情報を公開する方法についても説明しました。

このチュートリアルでは、ASP.NET フォーム認証、調査を終了します。 次のチュートリアルでは、メンバーシップフレームワークへの取り組みを開始します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [解説フォーム認証](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [ASP.NET 2.0 でのフォーム認証について説明しました。](https://msdn.microsoft.com/library/aa480476.aspx)
- [方法: ASP.NET 2.0 でフォーム認証を保護する](https://msdn.microsoft.com/library/ms998310.aspx)
- [Professional ASP.NET 2.0 のセキュリティ、メンバーシップ、およびロール管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)(ISBN: 978-0-7645-9698-8)
- [ログインコントロールのセキュリティ保護](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;authentication&gt; 要素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;認証用の &lt;フォーム&gt; 要素&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;machineKey&gt; 要素](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [フォーム認証チケットと Cookie について](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>このチュートリアルに含まれるトピックのビデオトレーニング

- [フォーム認証プロパティを変更する方法](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [ASP.NET アプリケーションで Cookie レス認証を設定して使用する方法](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP フォーム ログイン再配置](../../../videos/authentication/asp-forms-login-relocation.md)
- [フォーム ログイン カスタム キー構成](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [認証方法にカスタム データを追加する](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [カスタム プリンシパル オブジェクトを使用する](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Alicja Maziarz でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)の行を削除します。

> [!div class="step-by-step"]
> [[戻る]](an-overview-of-forms-authentication-vb.md)
