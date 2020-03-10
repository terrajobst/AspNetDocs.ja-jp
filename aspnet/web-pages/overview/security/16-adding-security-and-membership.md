---
uid: web-pages/overview/security/16-adding-security-and-membership
title: ASP.NET Web ページ (Razor) サイトへのセキュリティとメンバーシップの追加 |Microsoft Docs
author: Rick-Anderson
description: この章では、ログインしているユーザーのみが使用できるように web サイトをセキュリティで保護する方法について説明します。 (ページ tha を作成する方法についても説明します。
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 0be3e767a42939a3c343f6d4a730eb1d9a6b367c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509902"
---
# <a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトへのセキュリティとメンバーシップの追加

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトをセキュリティで保護する方法について説明します。これにより、一部のページは、ログインしているユーザーのみが使用できるようになります。 (誰でもアクセスできるページの作成方法についても説明します)。
> 
> **学習内容:** 
> 
> - 登録ページとログインページを持つ web サイトを作成する方法。一部のページでは、アクセスをメンバーのみに制限できるようにします。
> - パブリックページとメンバー専用ページを作成する方法。
> - 役割を定義する方法 (サイトに対して異なるセキュリティアクセス許可を持つグループ)、およびユーザーをロールに割り当てる方法について説明します。
> - CAPTCHA を使用して、自動プログラム (ボット) がメンバーアカウントを作成できないようにする方法。
>   
> 
> この記事で導入された ASP.NET 機能を次に示します。
> 
> - WebMatrix**スターターサイト**テンプレート。
> - `WebSecurity` helper および `Roles` クラス。
> - `ReCaptcha` ヘルパー。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - WebMatrix 3
> - ASP.NET Web ヘルパーライブラリ

サイトが&#8212; *メンバーシップ*をサポートするように、web サイトをセットアップすることができます。 これは、さまざまな理由で役に立ちます。 たとえば、メンバーだけが使用できるページがサイトに存在する場合があります。 場合によっては、フィードバックを送信したりコメントを残したりするためにユーザーにログインすることが必要になる場合があります。

Web サイトでメンバーシップがサポートされている場合でも、ユーザーはサイトの一部のページを使用する前に、必ずしもログインする必要はありません。 ログインしていないユーザーは、*匿名ユーザー*と呼ばれます。

ユーザーは、web サイトに登録して、サイトにログインできます。 Web サイトには、ユーザー名 (電子メールアドレス) とパスワードを入力して、ユーザーが要求していることを確認する必要があります。 このようにログインし、ユーザーの id を確認するプロセスは、*認証*と呼ばれます。

セキュリティとメンバーシップは、さまざまな方法で設定できます。

- WebMatrix を使用している場合、簡単な方法は、**スタートサイト**テンプレートに基づいて新しいサイトを作成することです。 このテンプレートは既にセキュリティとメンバーシップ用に構成されており、登録ページ、ログインページなどが既に存在します。

    テンプレートによって作成されたサイトには、ユーザーが Facebook、Google、Twitter などの外部サイトを使用してログインできるようにするオプションもあります。
- 既存のサイトにセキュリティを追加する場合、または**スターターサイト**テンプレートを使用しない場合は、独自の登録ページやログインページなどを作成できます。

この記事では、**スターターサイト**テンプレートを使用してセキュリティを追加する方法 &mdash; 最初のオプションについて説明します。 また、独自のセキュリティを実装する方法についての基本的な情報を提供し、その方法に関する詳細情報へのリンクを示します。 外部ログインを有効にする方法についての情報もあります。詳細については、別の記事で説明します。

## <a name="creating-website-security-using-the-starter-site-template"></a>スターターサイトテンプレートを使用して Web サイトのセキュリティを作成する

WebMatrix では、**スターターサイト**テンプレートを使用して、次のものを含む web サイトを作成できます。

- メンバーのユーザー名とパスワードを格納するために使用されるデータベース。
- 匿名 (新規) ユーザーが登録できる登録ページ。
- ログインとログアウトのページ。
- パスワードの回復とリセットのページ。

次の手順では、サイトを作成して構成する方法について説明します。

1. WebMatrix を起動し、 **[クイックスタート]** ページで、 **[テンプレートからサイト]** を選択します。
2. **スターターサイト**テンプレートを選択し、[ **OK]** をクリックします。 WebMatrix によって新しいサイトが作成されます。
3. 左側のウィンドウで、 **[ファイル]** ワークスペースセレクターをクリックします。
4. Web サイトのルートフォルダーで、 *\_該当*ファイルを開きます。このファイルは、グローバル設定を格納するために使用される特殊なファイルです。 ここには、`//` 文字を使用してコメントアウトされたステートメントがいくつか含まれています。

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    これらのステートメントは、電子メールの送信に使用できる `WebMail` ヘルパーを構成します。 メンバーシップシステムは、ユーザーが登録するとき、またはパスワードを変更するときに、電子メールを使用して確認メッセージを送信できます。 (たとえば、ユーザーが登録した後、登録プロセスを完了するためにクリックできるリンクを含む電子メールが届きます)。

    電子メールを送信するには、「 [ASP.NET Web ページサイトに電子メールを追加](https://go.microsoft.com/fwlink/?LinkId=202899)する」の説明に従って、SMTP サーバーにアクセスする必要があります。 電子メールの設定を*該当ファイル\_* に保存し、電子メールを送信できる各ページに繰り返しコードを記述する必要がないようにします。 (SMTP 設定を構成して登録データベースを設定する必要はありません。電子メールエイリアスからユーザーを検証し、ユーザーが忘れたパスワードをリセットできるようにする場合にのみ、SMTP 設定が必要です)。
5. ステートメントをコメント解除するには、各ステートメントの先頭から `//` を削除します。

    電子メールの確認を設定しない場合は、この手順と次の手順を省略できます。 SMTP の値が設定されていない場合は、確認の電子メールを送信せずに、新しいアカウントをすぐに使用できます。
6. コード内の次の電子メール関連の設定を変更します。

   - `WebMail.SmtpServer` に、アクセス権のある SMTP サーバーの名前を設定します。
   - `WebMail.EnableSsl` を `true`に設定したままにします。 この設定により、SMTP サーバーに送信される資格情報が暗号化されて保護されます。
   - `WebMail.UserName` を、SMTP サーバーアカウントのユーザー名に設定します。
   - `WebMail.Password` を SMTP サーバーアカウントのパスワードに設定します。
   - `WebMail.From` を独自の電子メールアドレスに設定します。 これは、メッセージの送信元の電子メールアドレスです。

     > [!NOTE] 
     > 
     > **ヒント**これらのプロパティの値の詳細については、「 [ASP.NET Web ページのサイト全体の動作をカスタマイズ](https://go.microsoft.com/fwlink/?LinkID=202906)する」の「[電子メール設定の構成](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings)」を参照してください。
7. 該当を保存して *\_* 閉じます。
8. ブラウザーで*既定の cshtml*ページを実行します。

    ![セキュリティ-メンバーシップ-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > プロパティが `ExtendedMembershipProvider`のインスタンスである必要があることを示すエラーが表示された場合は、ASP.NET Web ページメンバーシップシステム (SimpleMembership) を使用するようにサイトが構成されていない可能性があります。 これは、ホスティングプロバイダーのサーバーがローカルサーバーとは異なる方法で構成されている場合に発生することがあります。 この問題を解決するには、次の要素をサイトの*web.config*ファイルに追加します。
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > この要素を `<configuration>` 要素の子として、`<system.web>` 要素のピアとして追加します。
9. ページの右上隅にある **[登録]** リンクをクリックします。 [の*登録*] ページが表示されます。
10. ユーザー名とパスワードを入力し、 **[登録]** をクリックします。

    ![セキュリティ-メンバーシップ-3](16-adding-security-and-membership/_static/image2.png)

    **スターターサイト**テンプレートから web サイトを作成した場合、サイトの*App\_Data*フォルダーに、 *startersite. .sdf*という名前のデータベースが作成されます。 登録時に、ユーザー情報がデータベースに追加されます。 SMTP の値を設定すると、登録を完了するために使用した電子メールアドレスにメッセージが送信されます。

    ![セキュリティ-メンバーシップ-4](16-adding-security-and-membership/_static/image3.png)
11. 電子メールプログラムにアクセスし、メッセージを検索します。このメッセージには、確認コードとサイトへのハイパーリンクが含まれています。
12. ハイパーリンクをクリックして、アカウントをアクティブ化します。 確認のハイパーリンクを開くと、[登録の確認] ページが開きます。

    ![セキュリティ-メンバーシップ-5](16-adding-security-and-membership/_static/image4.png)
13. **[ログイン]** リンクをクリックし、登録したアカウントを使用してログインします。

      ログインすると、**ログイン**リンクと**登録**リンクが**ログアウト**リンクに置き換えられます。 ログイン名がリンクとして表示されます。 (このリンクを使用すると、パスワードを変更できるページに移動できます)。

      ![セキュリティ-メンバーシップ-6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 既定では、ASP.NET web ページは、資格情報をクリアテキストでサーバーに送信します (人間が判読できるテキスト)。 運用サイトでは、サーバーと交換される機密情報を暗号化するために、セキュリティで保護された HTTP (https://、 *secure sockets layer*または SSL とも呼ばれます) を使用する必要があります。 前の例のように `WebMail.EnableSsl=true` を設定することにより、SSL を使用して電子メールメッセージを送信する必要があります。 SSL の詳細については、「 [Web 通信をセキュリティで保護する: 証明書、SSL、および https://](https://go.microsoft.com/fwlink/?LinkId=208660)」を参照してください。

## <a name="additional-membership-functionality-in-the-site"></a>サイトの追加のメンバーシップ機能

サイトには、ユーザーが自分のアカウントを管理できるようにするその他の機能が含まれています。 ユーザーは次の操作を実行できます。

- パスワードを変更します。 ログインした後、ユーザー名 (リンク) をクリックできます。 これにより、新しいパスワード (*Account/ChangePassword. cshtml*) を作成できるページに移動します。
- 忘れたパスワードを回復します。 [ログイン] ページに、ユーザーが電子メールアドレスを入力できるページ (*Account/ForgotPassword*) に移動するリンク (**パスワードを忘れた場合**) が表示されます。 サイトは、新しいパスワードを設定するためにクリックできるリンクを含む電子メールメッセージを送信します (*アカウント/PasswordReset. cshtml*)。

また、後で説明するように、ユーザーが外部サイトを使用してログインすることもできます。

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>メンバー専用ページを作成する

期間中は、だれでも web サイト内の任意のページを参照できます。 ただし、ログインしているユーザー (つまり、メンバー) だけが使用できるページが必要になる場合もあります。 ASP.NET を使用すると、ログインしているメンバーだけがアクセスできるページを作成できます。 通常、匿名ユーザーがメンバーのみのページにアクセスしようとすると、ログインページにリダイレクトされます。

この手順では、ログインしているユーザーのみが使用できるページを含むフォルダーを作成します。

1. サイトのルートで、新しいフォルダーを作成します。 (リボンで、 **[新規]** の下の矢印をクリックし、 **[新しいフォルダー]** を選択します)。
2. 新しいフォルダーの*メンバー*に名前を指定します。
3. *Members*フォルダー内に新しいページを作成し、そのページに「 *membersinformation. cshtml*」という名前を付けます。
4. 既存の内容を次のコードとマークアップに置き換えます。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    このコードは、`WebSecurity` オブジェクトの `IsAuthenticated` プロパティをテストします。これにより、ユーザーがログインした場合は `true` が返されます。 ユーザーがログインしていない場合、コードは `Response.Redirect` を呼び出して、*アカウント*フォルダーの*Login. cshtml*ページにユーザーを送信します。

    リダイレクトの URL には、現在のページのパスを設定するために `Request.Url.LocalPath` を使用する `returnUrl` クエリ文字列値が含まれます。 次のようなクエリ文字列で `returnUrl` 値を設定した場合 (および返される URL がローカルパスの場合)、ログインページはログイン後にこのページにユーザーを返します。

    また、このコードでは *\_SiteLayout*ページをレイアウトページとして設定します。 (レイアウトページの詳細については、「 [ASP.NET Web ページサイトでの一貫したレイアウトの作成](https://go.microsoft.com/fwlink/?LinkId=202891)」を参照してください)。
5. サイトを実行します。 まだログインしている場合は、ページの上部にある **[ログアウト]** ボタンをクリックします。
6. ブラウザーで、ページ */メンバーの情報*を要求します。 たとえば、URL は次のようになります。

    `http://localhost:38366/Members/MembersInformation`

    (ポート番号 (38366) は URL によって異なる可能性があります)。

    ログインしていないので、[ *cshtml* ] ページにリダイレクトされます。
7. 前の手順で作成したアカウントを使用してログインします。 [ *Membersinformation* ] ページにリダイレクトされます。 この時点でログインしているため、ページの内容が表示されます。

複数のページへのアクセスをセキュリティで保護するには、次の操作を行います。

- 各ページにセキュリティチェックを追加します。
- 保護されたページを保持するフォルダーに *\_PageStart. cshtml*ページを作成し、そこにセキュリティチェックを追加します。 *\_PageStart. cshtml*ページは、フォルダー内のすべてのページのグローバルページの一種として機能します。 この手法の詳細については、「 [ASP.NET Web ページのサイト全体の動作をカスタマイズする](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)」を参照してください。

## <a name="creating-security-for-groups-of-users-roles"></a>ユーザーグループ (ロール) のセキュリティを作成する

サイトに多数のメンバーが含まれている場合は、ページを表示する前に、各ユーザーのアクセス許可を個別に確認するのは効率的ではありません。 代わりに、個々のメンバーが属するグループ (*ロール*) を作成することができます。 その後、ロールに基づいてアクセス許可を確認できます。 このセクションでは、&quot;管理者&quot; ロールを作成し、そのロールに属している (だれが属している) ユーザーがアクセスできるページを作成します。

ASP.NET メンバーシップシステムは、ロールをサポートするように設定されています。 ただし、メンバーシップの登録とログインとは異なり、**スターターサイト**テンプレートには、役割の管理に役立つページは含まれていません。 (ロールの管理は、ユーザータスクではなく、管理タスクです)。ただし、WebMatrix のメンバーシップデータベースにグループを直接追加することはできます。

1. WebMatrix で、 **[データベース]** ワークスペースセレクターをクリックします。
2. 左側のウィンドウで、 *Startersite. .sdf*ノードを開き、 **[テーブル]** ノードを開いて、[ *web ページ\_ロール*] テーブルをダブルクリックします。

    ![セキュリティ-メンバーシップ-7](16-adding-security-and-membership/_static/image6.png)
3. &quot;admin&quot;という名前のロールを追加します。 *RoleId*フィールドは自動的に入力されます。 (これは主キーであり、「 [ASP.NET Web ページサイトでのデータベースの操作の概要](https://go.microsoft.com/fwlink/?LinkId=202893)」で説明されているように、識別フィールドとして設定されています)。
4. *RoleId*フィールドの値をメモしておきます。 (定義している最初のロールである場合は1になります)。

    ![セキュリティ-メンバーシップ-8](16-adding-security-and-membership/_static/image7.png)
5. *Web ページの\_Roles*  テーブルを閉じます。
6. *UserProfile*テーブルを開きます。
7. テーブル内の1人以上のユーザーの*UserId*値をメモしておき、テーブルを閉じます。
8. *Web ページ\_UserInRoles*テーブルを開き、 *UserID*と*RoleID*値をテーブルに入力します。 たとえば、ユーザー2を &quot;admin&quot; ロールに配置するには、次の値を入力します。

    ![セキュリティ-メンバーシップ-9](16-adding-security-and-membership/_static/image8.png)
9. *Web ページ\_UsersInRoles*テーブルを閉じます。

    ロールが定義されたので、そのロールに属しているユーザーがアクセスできるページを構成できます。
10. Web サイトのルートフォルダーで、 *Adminerror. cshtml*という名前の新しいページを作成し、既存の内容を次のコードに置き換えます。 これは、ページへのアクセスが許可されていない場合にユーザーがリダイレクトされるページです。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. Web サイトのルートフォルダーで、 *Adminonly. cshtml*という名前の新しいページを作成し、既存のコードを次のコードに置き換えます。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    `Roles.IsUserInRole` メソッドは、現在のユーザーが指定されたロール (この場合は "admin" ロール) のメンバーである場合に `true` を返します。
12. *既定の cshtml*をブラウザーで実行しますが、ログインしません。 (既にログインしている場合は、ログアウトしてください)。
13. ブラウザーのアドレスバーで、URL に*Adminonly*を追加します。 (つまり、 *Adminonly. cshtml*ファイルを要求します)。&quot;admin&quot; ロールのユーザーとして現在ログインしていないため、 *Adminerror. cshtml*ページにリダイレクトされます。
14. 既定の*cshtml*に戻り、&quot;admin&quot; ロールに追加したユーザーとしてログインします。
15. *Adminonly. cshtml*ページを参照します。 今度は、このページが表示されます。

## <a name="preventing-automated-programs-from-joining-your-website"></a>自動プログラムが Web サイトに参加できないようにする

ログインページでは、自動プログラム ( *web ロボット*または*ボット*と呼ばれることもあります) が web サイトへの登録を停止することはありません。 この手順では、登録ページの ReCaptcha テストを有効にする方法について説明します。

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. Web サイトを ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)) に登録します。 登録が完了すると、公開キーと秘密キーが取得されます。
2. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。
3. *Account*フォルダーで、 *Register. cshtml*という名前のファイルを開きます。
4. ページの上部にあるコードで、次の行を見つけて、`//` コメント文字を削除してコメント解除します。

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. `PRIVATE_KEY` を独自の ReCaptcha 秘密キーに置き換えます。
6. ページのマークアップで、ページマークアップの次の行の周囲にある `@*` と `*@` コメント化文字を削除します。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. `PUBLIC_KEY` をキーに置き換えます。
8. まだ削除していない場合は、"CAPTCHA 検証を有効にするには、" で始まるテキストを含む `<div>` 要素を削除します。 (`<div>` 要素全体とその内容を削除します)。

9. ブラウザーで*既定の cshtml*を実行します。 サイトにログインしている場合は、 **[ログアウト]** リンクをクリックします。
10. [Register] \ (**登録**\) リンクをクリックし、CAPTCHA テストを使用して登録をテストします。

     ![セキュリティ-メンバーシップ-10](16-adding-security-and-membership/_static/image9.png)

`ReCaptcha` helper の詳細については、「 [CATPCHA を使用して自動プログラム (ボット) が ASP.NET Web サイトを使用できないようにする](https://go.microsoft.com/fwlink/?LinkId=251967)」を参照してください。

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>ユーザーが外部サイトを使用してログインできるようにする

**スターターサイト**テンプレートには、ユーザーが Facebook、Windows Live、Twitter、Google、または Yahoo を使用してログインできるようにするコードとマークアップが含まれています。 既定では、この機能は有効になっていません。 これらの外部プロバイダーを使用したログインをユーザーに使用するための一般的な手順は次のとおりです。

- サポートする外部サイトを決定します。
- 必要に応じて、そのサイトにアクセスし、ログインアプリを設定します。 (たとえば、Facebook ログインを許可するには、これを行う必要があります)。
- サイトで、プロバイダーを構成します。 ほとんどの場合、 *\_該当*ファイルの一部のコードをコメント解除するだけで済みます。
- 登録ページにマークアップを追加して、ユーザーがログインのために外部サイトにリンクできるようにします。 通常は、必要なマークアップをコピーし、テキストを少し変更します。

詳細な手順については、「 [ASP.NET Web ページサイトの外部サイトからのログインを有効](https://go.microsoft.com/fwlink/?LinkId=251969)にする」を参照してください。

ユーザーが別のサイトからログインすると、ユーザーはサイトに戻り、そのログインをサイトに*関連付け*ます。 実際には、ユーザーの外部ログイン用のメンバーシップエントリがサイトに作成されます。 これにより、外部ログインでメンバーシップの通常の機能 (ロールなど) を使用できるようになります。

## <a name="adding-security-to-an-existing-website"></a>既存の Web サイトへのセキュリティの追加

この記事の前半で説明した手順は、web サイトのセキュリティの基礎として**スターターサイト**テンプレートを使用することに依存しています。 **スターターサイト**テンプレートから開始したり、そのテンプレートに基づいてサイトから関連ページをコピーしたりするのが実用的でない場合は、自分でコーディングすることで、独自のサイトに同じ種類のセキュリティを実装できます。 同じ種類のページ (登録、ログインなど) を作成し、ヘルパーとクラスを使用してメンバーシップを設定します。

基本的なプロセスについては、ブログ記事「 [ASP.NET Razor セキュリティを実装する最も基本的な方法](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)」で説明されています。 ほとんどの作業は、`WebSecurity` ヘルパーの次のメソッドとプロパティを使用して行われます。

- [WebCreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx)、 [websecurity.](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx)のようになります。 これらのメソッドを使用すると、他のユーザーが既に登録されているかどうかを判断し、登録できます。
- [Webauthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx)。 このプロパティを使用すると、現在のユーザーがログインしているかどうかを判断できます。 これは、ログインページにユーザーがまだログインしていない場合にユーザーをリダイレクトするのに便利です。
- [Websecurity. Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx), [Websecurity. Logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx). これらのメソッドは、ユーザーを記録します。
- [Websecurity. CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx)。 このプロパティは、現在のユーザーのログイン名 (ユーザーがログインしている場合) を表示する場合に便利です。
- [Websecurity. ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx)。 この方法は、登録の電子メール確認を設定する場合に便利です。 (詳細につい[ては、ASP.NET Web ページセキュリティの確認機能を使用し](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)たブログ投稿を参照してください)。

ロールを管理するには、ブログの記事で説明されているように、[ロール](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx)と[メンバーシップ](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx)クラスを使用できます。

## <a name="additional-resources"></a>その他のリソース

- [サイト全体の動作をカスタマイズする](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Web 通信のセキュリティ保護: 証明書、SSL、 https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- ASP.NET Razor セキュリティを実装し、 [ASP.NET Web ページセキュリティの確認機能を使用](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)[する最も基本的な方法](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)です。 これらは、**スターターサイト**テンプレートを使用せずに ASP.NET メンバーシップ機能を実装する方法を説明するブログの投稿です。
- [ASP.NET Web ページ サイトで外部サイトからのログインを有効にする](https://go.microsoft.com/fwlink/?LinkId=251969)
- [Websecurity CLASS API リファレンス](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99))(MSDN)
- [Simpleroleprovider クラス API リファレンス](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99))(MSDN)
- [SimpleMembershipProvider CLASS API リファレンス](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99))(MSDN)
