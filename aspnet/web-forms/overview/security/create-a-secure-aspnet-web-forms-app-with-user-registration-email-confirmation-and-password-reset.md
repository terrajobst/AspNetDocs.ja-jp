---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: ユーザー登録、電子メール確認、パスワードリセット (C#) を使用して、Secure ASP.NET Web フォームアプリを作成します。Microsoft Docs
author: Erikre
description: このチュートリアルでは、ASP.NET Identity メンバーを使用して、ユーザー登録、電子メール確認、パスワードリセットを使用して ASP.NET Web フォームアプリを構築する方法について説明します。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: af3653bc164810126bc3bf8f1b1794d75642d807
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507130"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>ユーザー登録、電子メール確認、パスワード リセットを利用し、安全な ASP.NET Web フォームを作成する (C#)

[Erik Reitan](https://github.com/Erikre)

> このチュートリアルでは、ASP.NET Identity メンバーシップシステムを使用して、ユーザー登録、電子メール確認、パスワードリセットを使用して ASP.NET Web フォームアプリを構築する方法について説明します。 このチュートリアルは、Rick Anderson の[MVC チュートリアル](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)に基づいています。

## <a name="introduction"></a>はじめに

このチュートリアルでは、Visual Studio と ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを作成し、ユーザー登録、電子メール確認、パスワードリセットを使用してセキュリティで保護された Web フォームアプリを作成するために必要な手順について説明します。

### <a name="tutorial-tasks-and-information"></a>チュートリアルのタスクと情報:

- [ASP.NET Web フォームアプリを作成する](#createWebForms)
- [SendGrid をフックする](#SG)
- [ログインする前に電子メールの確認を要求する](#require)
- [パスワードの回復とリセット](#reset)
- [電子メールの再送信の確認リンク](#rsend)
- [アプリのトラブルシューティング](#dbg)
- [その他のリソース](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web フォームアプリを作成する

まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降もインストールします。

> [!NOTE]
> 警告: このチュートリアルを完了するには、 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールする必要があります。

1. 新しいプロジェクト (**ファイル** -&gt;**新しいプロジェクト**) を作成し、 **[新しいプロジェクト]** ダイアログボックスで**ASP.NET Web アプリケーション**テンプレートと最新の .NET Framework バージョンを選択します。
2. **[New ASP.NET プロジェクト]** ダイアログボックスで、 **[Web フォーム]** テンプレートを選択します。 既定の認証は、**個々のユーザーアカウント**として残しておきます。 Azure でアプリをホストする場合は、[**クラウドにホスト**する] チェックボックスをオンのままにします。   
 次に、[ **OK]** をクリックして、新しいプロジェクトを作成します。  
    ![[新しい ASP.NET プロジェクト] ダイアログ ボックス](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. プロジェクトの Secure Sockets Layer (SSL) を有効にします。 「 [Web フォームチュートリアルシリーズを使用したはじめに](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)」の「**プロジェクトに対して SSL を有効にする**」セクションで説明されている手順に従います。
4. アプリを実行し、 **[登録]** リンクをクリックして、新しいユーザーを登録します。 この時点で、電子メールの検証は、電子メールアドレスが整形式であることを確認するために、 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性に基づいています。 電子メールの確認を追加するようにコードを変更します。 ブラウザー ウィンドウを閉じます。
5. Visual Studio の**サーバーエクスプローラー** ( -&gt;**サーバーエクスプローラー**の**表示**) で、 **Data Connections\DefaultConnection\Tables\AspNetUsers**に移動し、右クリックして、 **[テーブル定義を開く]** を選択します。 

    次の図は、`AspNetUsers` テーブルスキーマを示しています。

    ![AspNetUsers テーブルスキーマ](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. **サーバーエクスプローラー**で、 **AspNetUsers**テーブルを右クリックし、 **[テーブルデータの表示]** を選択します。  
  
    ![AspNetUsers テーブルデータ](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 この時点で、登録済みユーザーの電子メールは確認されていません。
7. 行をクリックし、[削除] を選択してユーザーを削除します。 次の手順でもう一度このメールを追加し、電子メールアドレスに確認メッセージを送信します。

## <a name="email-confirmation"></a>電子メールの確認

新しいユーザーの登録時に電子メールを確認して、他のユーザーが偽装していないこと (つまり、他のユーザーの電子メールに登録されていないこと) を確認することをお勧めします。 ディスカッションフォーラムがあるとしたら、`"bob@cpandl.com"` が `"joe@contoso.com"`として登録されないようにしたいと考えています。 電子メールを確認しないと、`"joe@contoso.com"` アプリから不要な電子メールを受け取る可能性があります。 Bob が誤って `"bib@cpandl.com"` として登録されていて気付かないとしても、アプリには正しい電子メールがないため、パスワードの回復を使用することはできません。 電子メールの確認では、bot からの保護のみが制限されており、特定のスパム送信者からの保護は提供されません。

通常は、電子メール、SMS テキストメッセージ、または別のメカニズムによって確認される前に、新しいユーザーが web サイトにデータを投稿できないようにします。 以下のセクションでは、電子メールの確認を有効にし、コードを変更して、新しく登録されたユーザーが電子メールを確認するまでログインできないようにします。 このチュートリアルでは、電子メールサービス SendGrid を使用します。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid をフックする

このチュートリアルが記述されているため、SendGrid によって API が変更されました。 現在の SendGrid の手順については、「 [sendgrid](http://sendgrid.com/) 」または「[アカウント確認とパスワードの回復を有効にする](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)」を参照してください。

このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して電子メール通知を追加する方法のみを説明していますが、SMTP などのメカニズムを使用[して電子](#addRes)メールを送信することもできます。

1. Visual Studio で、**パッケージマネージャーコンソール**([**ツール** -&gt; **NuGet パッケージ**マネージャー] -&gt;**パッケージマネージャーコンソール**) を開き、次のコマンドを入力します。  
    `Install-Package SendGrid`
2. [Azure SendGrid のサインアップページ](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)にアクセスし、無料の sendgrid アカウントを登録します。 [Sendgrid のサイト](http://www.sendgrid.com)で、無料の sendgrid アカウントに直接サインアップすることもできます。
3. **ソリューションエクスプローラー**で、*アプリ\_スタート*フォルダーの*IdentityConfig.cs*ファイルを開き、黄色で強調表示されている次のコードを `EmailService` クラスに追加して、 **sendgrid**を構成します。

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. また、 *IdentityConfig.cs*ファイルの先頭に次の `using` ステートメントを追加します。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. このサンプルを簡単に保つために、電子メールサービスアカウントの値を web.config ファイルの `appSettings` セクションに保存*します。* 次の XML を、黄色で強調表示されているプロジェクトのルートにある*web.config ファイルに*追加します。

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > セキュリティ-機密データをソースコードに格納しません。 この例では、アカウントと資格情報は、 *web.config ファイルの* **appSetting**セクションに格納されています。 Azure では、これらの値を Azure portal の [ **[構成](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] タブに安全に格納できます。 関連情報については、Rick Anderson のトピック「[パスワードやその他の機密データを ASP.NET と Azure にデプロイするためのベストプラクティス](https://go.microsoft.com/fwlink/?LinkId=513141)」を参照してください。
6. アプリから電子メールを正常に送信できるように、SendGrid 認証値 (ユーザー名とパスワード) を反映するために、電子メールサービスの値を追加します。 Sendgrid を指定した電子メールアドレスではなく、SendGrid アカウント名を使用してください。

### <a name="enable-email-confirmation"></a>電子メールの確認を有効にする

 電子メールの確認を有効にするには、次の手順に従って登録コードを変更します。  

1. *Account*フォルダーで*Register.aspx.cs*分離コードを開き、次の強調表示された変更を有効にするために `CreateUser_Click` メソッドを更新します。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. **ソリューションエクスプローラー**で、 *default.aspx*を右クリックし、 **[スタートページとして設定]** を選択します。
3. F5 キーを押してアプリを実行し**ます。** ページが表示されたら、 **[登録]** リンクをクリックして登録ページを表示します。
4. 電子メールとパスワードを入力し、 **[登録]** ボタンをクリックして、sendgrid 経由で電子メールメッセージを送信します。  
   プロジェクトとコードの現在の状態により、ユーザーは、アカウントが確認されていなくても、登録フォームの完了後にログインできるようになります。
5. 電子メールアカウントを確認し、リンクをクリックして電子メールを確認します。  
   登録フォームを送信すると、ログインされます。  
    ![サンプル Web サイト-サインイン済み](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>ログインする前に電子メールの確認を要求する

電子メールアカウントを確認しましたが、この時点で、完全にサインインするには、確認の電子メールに含まれているリンクをクリックする必要はありません。 次のセクションでは、新しいユーザーがログイン (認証) される前に確認済みの電子メールを持っている必要のあるコードを変更します。

1. Visual Studio の**ソリューションエクスプローラー**で、次の強調表示された変更を使用して、 *Accounts*フォルダーに含まれている*Register.aspx.cs*分離コードの `CreateUser_Click` イベントを更新します。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. 次の強調表示された変更を使用して、 *Login.aspx.cs*の分離コードの `LogIn` メソッドを更新します。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>アプリケーションの実行

 これで、ユーザーの電子メールアドレスが確認されているかどうかを確認するコードを実装できました。次は、**登録**ページと**ログイン**ページの両方で機能を確認します。 

1. テストする電子メールエイリアスが含まれている**AspNetUsers**テーブル内のすべてのアカウントを削除します。
2. **F5 キー**を押してアプリを実行し、電子メールアドレスが確認されるまでユーザーとして登録できないことを確認します。
3. 送信した電子メールで新しいアカウントを確認する前に、新しいアカウントでログインします。  
 ログインできないことと、確認済みの電子メールアカウントが必要であることがわかります。
4. 電子メールアドレスを確認したら、アプリにログインします。

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>パスワードの回復とリセット

1. Visual Studio で、 *Account*フォルダーに格納されている*Forgot.aspx.cs*の分離コードの `Forgot` メソッドからコメント文字を削除して、メソッドが次のように表示されるようにします。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. *Login.aspx*ページを開きます。 次に強調表示されているように、 **Loginform**セクションの末尾付近にあるマークアップを置き換えます。 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. *Login.aspx.cs*の分離コードを開き、`Page_Load` イベントハンドラーから黄色で強調表示されている次のコード行をコメント解除します。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. F5 キーを押してアプリを実行し**ます。** ページが表示されたら、 **[ログイン]** リンクをクリックします。
5. [**パスワードを忘れ**た場合] リンクをクリックして、[パスワードを**忘れ**た場合] ページを表示します。
6. メールアドレスを入力し、 **[Submit]** \ (送信 \) ボタンをクリックして、自分のアドレスに電子メールを送信します。これにより、パスワードをリセットできます。   
   電子メールアカウントを確認し、リンクをクリックして **[パスワードのリセット]** ページを表示します。
7. **[パスワードのリセット]** ページで、電子メール、パスワード、確認用のパスワードを入力します。 次に、 **[リセット]** ボタンを押します。  
   パスワードが正常にリセットされると、 **[パスワードの変更]** ページが表示されます。 これで、新しいパスワードでログインできるようになりました。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>電子メールの再送信の確認リンク

ユーザーは、新しいローカルアカウントを作成すると、ログオンする前に使用する必要がある確認のリンクを電子メールで送信します。 ユーザーが誤って確認メールを削除した場合、または電子メールが届いていない場合は、確認リンクを再度送信する必要があります。 次のコード変更は、これを有効にする方法を示しています。

1. Visual Studio で、 **Login.aspx.cs**分離コードを開き、`LogIn` イベントハンドラーの後に次のイベントハンドラーを追加します。   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. 次のように、黄色で強調表示されているコードを変更して、 *Login.aspx.cs*の分離コードで `LogIn` イベントハンドラーを変更します。 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. 次のように、黄色で強調表示されているコードを追加して、 *login.aspx*ページを更新します。 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. テストする電子メールエイリアスが含まれている**AspNetUsers**テーブル内のすべてのアカウントを削除します。
5. **F5 キー**を押してアプリを実行し、電子メールアドレスを登録します。
6. 送信した電子メールで新しいアカウントを確認する前に、新しいアカウントでログインします。  
   ログインできないことと、確認済みの電子メールアカウントが必要であることがわかります。 さらに、確認メッセージを電子メールアカウントに再送信できるようになりました。
7. 電子メールアドレスとパスワードを入力し、[**再送信] 確認**ボタンを押します。
8. 新しく送信された電子メールメッセージに基づいて電子メールアドレスを確認したら、アプリにログインします。

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>アプリのトラブルシューティング

資格情報を確認するためのリンクが記載された電子メールが届かない場合は、次のようにします。

- 迷惑メールまたは迷惑メールフォルダーを確認します。
- SendGrid アカウントにログインし、[ [Email Activity] リンク](https://sendgrid.com/logs/index)をクリックします。
- Sendgrid のユーザーアカウント名は、SendGrid アカウントの電子メールアドレスでは*なく、web.config 値と*して使用していることを確認してください。

<a id="addRes"></a>
## <a name="additional-resources"></a>その他のリソース

- [推奨されるリソースへのリンク ASP.NET Identity](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Web Forms チュートリアルシリーズ-OAuth 2.0 プロバイダーの追加](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure App Service にデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web フォームチュートリアルシリーズ-プロジェクトの SSL を有効にする](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
