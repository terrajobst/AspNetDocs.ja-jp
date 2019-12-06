---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: ログイン、電子メール確認、パスワードリセット (C#) を使用して、SECURE ASP.NET MVC 5 web アプリを作成します。Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET Identity メンバーシップシステムを使用して、電子メールの確認とパスワードのリセットを使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。 ...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 07f5b290b73f75000e6f29fe09e4dc25e144452f
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74899695"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>ログイン、電子メール確認、パスワード リセットを使用して安全な ASP.NET MVC 5 Web アプリを作成する (C#)

[Rick Anderson]((https://twitter.com/RickAndMSFT))

このチュートリアルでは、ASP.NET Identity メンバーシップシステムを使用して、電子メールの確認とパスワードのリセットを使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。

.NET Core を使用するこのチュートリアルの更新バージョンについては、[ASP.NET Core でのアカウントの確認とパスワードの回復] [/aspnet/core/security/authentication/accconfirm] を参照してください。

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC アプリを作成する

まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールします。

> [!NOTE]
> 警告: このチュートリアルを完了するには、 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールする必要があります。

1. 新しい ASP.NET Web プロジェクトを作成し、MVC テンプレートを選択します。 Web フォームでも ASP.NET Identity がサポートされているため、web フォームアプリで同様の手順に従うことができます。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 既定の認証は、**個々のユーザーアカウント**として残しておきます。 Azure でアプリをホストする場合は、チェックボックスをオンのままにします。 このチュートリアルの後半では、Azure にデプロイします。 [Azure アカウントは無料で開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)ことができます。
3. [SSL を使用するようにプロジェクトを](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。
4. アプリを実行し、 **[登録]** リンクをクリックして、ユーザーを登録します。 この時点で、電子メールの検証は、 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性でのみ行うことができます。
5. サーバーエクスプローラーで、 **[Data Connections\DefaultConnection\Tables\AspNetUsers]** に移動して右クリックし、 **[テーブル定義を開く]** を選択します。

    次の図は、`AspNetUsers` スキーマを示しています。

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. **AspNetUsers**テーブルを右クリックし、 **[テーブルデータの表示]** を選択します。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 この時点で、電子メールは確認されていません。
7. 行をクリックし、[削除] を選択します。 次の手順でもう一度このメールを追加し、確認の電子メールを送信します。

## <a name="email-confirmation"></a>電子メールの確認

新しいユーザー登録の電子メールを確認して、他のユーザーが偽装していないこと (つまり、他のユーザーの電子メールに登録されていないこと) を確認することをお勧めします。 ディスカッションフォーラムがあるとしたら、`"bob@example.com"` が `"joe@contoso.com"`として登録されないようにしたいと考えています。 電子メールを確認しないと、`"joe@contoso.com"` アプリから不要な電子メールを受け取る可能性があります。 Bob が誤って `"bib@example.com"` として登録されていて気付かないとしても、アプリには正しい電子メールがないため、パスワードの回復を使用することはできません。 電子メールの確認では、bot から制限された保護のみを提供し、特定のスパム送信者からの保護を提供しません。登録に使用できる多くの勤務先の電子メールエイリアスがあります。

通常は、電子メール、SMS テキストメッセージ、または別のメカニズムによって確認される前に、新しいユーザーが web サイトにデータを投稿できないようにします。 <a id="build"></a>以下のセクションでは、電子メールの確認を有効にし、コードを変更して、新しく登録されたユーザーが電子メールを確認するまでログインできないようにします。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid をフックする

このセクションの手順は最新ではありません。 詳細な手順については、「 [SendGrid 電子メールプロバイダーの構成](/aspnet/core/security/authentication/accconfirm#configure-email-provider)」を参照してください。

このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して電子メール通知を追加する方法のみを説明していますが、SMTP などのメカニズムを使用[して電子](#addRes)メールを送信することもできます。

1. パッケージ マネージャー コンソールで、次のコマンドを入力します。 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. [Azure SendGrid のサインアップページ](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)にアクセスし、無料の sendgrid アカウントを登録します。 *App_Start/identityconfig.cs*で次のようなコードを追加して、sendgrid を構成します。

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

次のインクルードを追加する必要があります。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

このサンプルを簡単に保つために、アプリケーションの設定を web.config*ファイルに保存します*。

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> セキュリティ-機密データをソースコードに格納しません。 アカウントと資格情報は appSetting に格納されます。 Azure では、これらの値を Azure portal の [ **[構成](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] タブに安全に格納できます。 [ASP.NET と Azure にパスワードやその他の機密データをデプロイするためのベストプラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)をご覧ください。

### <a name="enable-email-confirmation-in-the-account-controller"></a>アカウントコントローラーで電子メールの確認を有効にする

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

*Views\Account\ConfirmEmail.cshtml*ファイルに正しい razor 構文があることを確認します。 (最初の行の @ 文字が欠落している可能性があります。 )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

アプリを実行し、[登録] リンクをクリックします。 登録フォームを送信すると、ログインしたことになります。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

電子メールアカウントを確認し、リンクをクリックして電子メールを確認します。

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>ログインする前に電子メールの確認を要求する

現在、ユーザーが登録フォームを完了すると、ログインします。 通常は、ログを記録する前に電子メールを確認します。 以下のセクションでは、新しいユーザーがログイン (認証) される前に確認済みの電子メールを要求するようにコードを変更します。 次の強調表示された変更を使用して、`HttpPost Register` メソッドを更新します。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

`SignInAsync` メソッドをコメントアウトすることで、ユーザーは登録によってサインインされません。 `TempData["ViewBagLink"] = callbackUrl;` 行を使用して、電子メールを送信することなく、[アプリをデバッグ](#dbg)し、登録をテストできます。 `ViewBag.Message` は、確認の指示を表示するために使用されます。 [ダウンロードサンプル](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)には、電子メールを設定せずに電子メールの確認をテストするコードが含まれており、アプリケーションのデバッグにも使用できます。

`Views\Shared\Info.cshtml` ファイルを作成し、次の razor マークアップを追加します。

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

[承認属性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)を Home コントローラーの `Contact` アクションメソッドに追加します。 **[Contact]** リンクをクリックすると、匿名ユーザーがアクセス権を持っていないこと、および認証されたユーザーがアクセス権を持っていないことを確認できます。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

また、`HttpPost Login` アクションメソッドも更新する必要があります。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

*Views\Shared\Error.cshtml*ビューを更新して、エラーメッセージを表示します。

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

テストする電子メールエイリアスが含まれている**AspNetUsers**テーブル内のすべてのアカウントを削除します。 アプリを実行し、電子メールアドレスが確認されるまでログインできないことを確認します。 電子メールアドレスを確認したら、 **[Contact]** リンクをクリックします。

<a id="reset"></a>
## <a name="password-recoveryreset"></a>パスワードの回復/リセット

アカウントコントローラーの `HttpPost ForgotPassword` アクションメソッドからコメント文字を削除します。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

*Views\Account\Login.cshtml* razor ビューファイルの `ForgotPassword` [html.actionlink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx)からコメント文字を削除します。

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

ログインページに、パスワードをリセットするためのリンクが表示されるようになります。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>電子メールの再送信の確認リンク

ユーザーは、新しいローカルアカウントを作成すると、ログオンする前に使用する必要がある確認のリンクを電子メールで送信します。 ユーザーが誤って確認メールを削除した場合、または電子メールが届いていない場合は、確認リンクを再度送信する必要があります。 次のコード変更は、これを有効にする方法を示しています。

次のヘルパーメソッドを、*コントローラー*ファイルの一番下に追加します。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

新しいヘルパーを使用するように Register メソッドを更新します。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

ユーザーアカウントが確認されていない場合は、ログイン方法を更新してパスワードを再送信します。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>ソーシャルおよびローカルログインアカウントの結合

電子メールリンクをクリックして、ローカルアカウントとソーシャルアカウントを組み合わせることができます。 次のシーケンスでは、最初にローカルログインとして **RickAndMSFT@gmail.com** が作成されますが、最初にアカウントをソーシャルログとして作成してから、ローカルログインを追加することができます。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

**[管理]** リンクをクリックします。 このアカウントに関連付けられている**外部ログイン: 0**に注意してください。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

別のログインサービスへのリンクをクリックし、アプリの要求を受け入れます。 2つのアカウントが結合されているので、いずれかのアカウントでログオンすることができます。 認証サービスのソーシャルログがダウンした場合、またはソーシャルアカウントへのアクセスが失われる可能性がある場合に備えて、ユーザーにローカルアカウントを追加することをお勧めします。

次の図では、Tom はソーシャルログ (ページに表示されている**外部ログイン: 1**から参照できます) です。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

**[パスワードの選択]** をクリックすると、同じアカウントに関連付けられているローカルログオンを追加できます。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>より詳細な電子メールの確認

このトピックでは[、ASP.NET Identity を使用したチュートリアルアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)について詳しく説明します。

<a id="dbg"></a>
## <a name="debugging-the-app"></a>アプリのデバッグ

リンクを含む電子メールが表示されない場合は、次のようになります。

- 迷惑メールまたは迷惑メールフォルダーを確認します。
- SendGrid アカウントにログインし、[ [Email Activity] リンク](https://sendgrid.com/logs/index)をクリックします。

電子メールを使用せずに検証リンクをテストするには、[完成したサンプル](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)をダウンロードします。 ページに確認のリンクと確認コードが表示されます。

<a id="addRes"></a>
## <a name="additional-resources"></a>その他の資料

- [推奨されるリソースへのリンク ASP.NET Identity](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)パスワードの回復とアカウントの確認についてさらに詳しく説明します。
- [Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)このチュートリアルでは、Facebook と Google OAuth 2 認証を使用して ASP.NET MVC 5 アプリを作成する方法について説明します。 また、Id データベースにデータを追加する方法についても説明します。
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC アプリを Azure にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。 このチュートリアルでは、Azure のデプロイ、ロールを使用してアプリをセキュリティで保護する方法、メンバーシップ API を使用してユーザーとロールを追加する方法、および追加のセキュリティ機能を追加します。
- [OAuth 2 用の Google アプリを作成し、そのアプリをプロジェクトに接続する](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook でアプリを作成し、アプリをプロジェクトに接続する](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [プロジェクトでの SSL の設定](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
