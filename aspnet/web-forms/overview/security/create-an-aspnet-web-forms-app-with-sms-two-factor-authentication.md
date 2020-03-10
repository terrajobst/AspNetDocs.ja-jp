---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: SMS 2 要素認証を使用して ASP.NET Web フォームアプリをC#作成する () |Microsoft Docs
author: Erikre
description: このチュートリアルでは、2要素認証を使用して ASP.NET Web フォームアプリを構築する方法について説明します。 このチュートリアルは、「Cr...」というタイトルのチュートリアルを補完するように設計されています。
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455980"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>SMS 2 要素認証を利用し、ASP.NET Web フォームを作成する (C#)

[Erik Reitan](https://github.com/Erikre)

[電子メールと SMS 2 要素認証を使用して ASP.NET Web フォームアプリをダウンロードする](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> このチュートリアルでは、2要素認証を使用して ASP.NET Web フォームアプリを構築する方法について説明します。 このチュートリアルは、 [「ユーザー登録、電子メール確認、パスワードリセットを使用して secure ASP.NET Web フォームアプリを作成する」](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)というタイトルのチュートリアルを補足することを目的としています。 また、このチュートリアルは Rick Anderson の[MVC チュートリアル](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)に基づいています。

## <a name="introduction"></a>はじめに

このチュートリアルでは、Visual Studio を使用して2要素認証をサポートする ASP.NET Web フォームアプリケーションを作成するために必要な手順について説明します。 2要素認証は、追加のユーザー認証手順です。 この追加の手順では、サインイン時に一意の暗証番号 (PIN) が生成されます。 PIN は、通常、電子メールまたは SMS メッセージとしてユーザーに送信されます。 その後、アプリのユーザーは、サインイン時に追加の認証手段として PIN を入力します。

### <a name="tutorial-tasks-and-information"></a>チュートリアルのタスクと情報:

- [ASP.NET Web フォームアプリを作成する](#createWebForms)
- [SMS と2要素認証のセットアップ](#SMS)
- [登録されたユーザーに対して2要素認証を有効にする](#use2FA)
- [その他のリソース](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web フォームアプリを作成する

まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降もインストールします。 また、以下で説明するように、 [Twilio](https://www.twilio.com/try-twilio)アカウントを作成する必要があります。

> [!NOTE]
> 重要: このチュートリアルを完了するには、 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールする必要があります。

1. 新しいプロジェクト (**ファイル** -&gt;**新しいプロジェクト**) を作成し、 **[新しいプロジェクト]** ダイアログボックスから、.NET Framework バージョンの4.5.2 と共に**ASP.NET Web アプリケーション**テンプレートを選択します。
2. **[New ASP.NET プロジェクト]** ダイアログボックスで、 **[Web フォーム]** テンプレートを選択します。 既定の認証は、**個々のユーザーアカウント**として残しておきます。 次に、[ **OK]** をクリックして、新しいプロジェクトを作成します。  
    ![[新しい ASP.NET プロジェクト] ダイアログ ボックス](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. プロジェクトの Secure Sockets Layer (SSL) を有効にします。 「 [Web フォームチュートリアルシリーズを使用したはじめに](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)」の「**プロジェクトに対して SSL を有効にする**」セクションで説明されている手順に従います。
4. Visual Studio で、**パッケージマネージャーコンソール**([**ツール** -&gt; **NuGet パッケージ**マネージャー] -&gt;**パッケージマネージャーコンソール**) を開き、次のコマンドを入力します。  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>SMS と2要素認証のセットアップ

このチュートリアルでは Twilio を使用しますが、どの SMS プロバイダーでも使用できます。

1. [Twilio](https://www.twilio.com/try-twilio)アカウントを作成します。
2. Twilio アカウントの **[ダッシュボード]** タブで、**アカウント SID**と認証トークンをコピーし**ます。** 後でアプリに追加します。
3. **[数値]** タブで、Twilio**電話番号**もコピーします。
4. Twilio**アカウント SID**、**認証トークン**、および**電話番号**をアプリで使用できるようにします。 単純にするために、これらの値は web.config*ファイルに*格納します。 Azure にデプロイするときに、[web サイトの構成] タブの**appSettings**セクションに値を安全に格納できます。また、電話番号を追加するときは、数字のみを使用します。   
   SendGrid の資格情報を追加することもできます。 SendGrid は、電子メール通知サービスです。 SendGrid を有効にする方法の詳細については、「[ユーザー登録、電子メール確認、パスワードリセットを使用した安全な ASP.NET Web フォームアプリの作成](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)」のチュートリアルの「Sendgrid をフックする」セクションを参照してください。

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > セキュリティ-機密データをソースコードに格納しません。 この例では、アカウントと資格情報*は、web.config ファイルの* **appSettings**セクションに格納されています。 Azure では、これらの値を Azure portal の [ **[構成](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] タブに安全に格納できます。 関連情報については、Rick Anderson のトピック「[パスワードやその他の機密データを ASP.NET と Azure にデプロイするためのベストプラクティス](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)」を参照してください。
5. 次の変更を黄色で強調表示して、*アプリ\_Start\IdentityConfig.cs*ファイルで `SmsService` クラスを構成します。 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. *IdentityConfig.cs*ファイルの先頭に、次の `using` ステートメントを追加します。 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. 黄色で強調表示されている行を削除して、 *Account/Manage .aspx*ファイルを更新します。  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. *Manage.aspx.cs*の `Page_Load` ハンドラーで、次のように黄色で強調表示されているコード行をコメント解除します。 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. *アカウント*/*TwoFactorAuthenticationSignIn.aspx.cs*の分離コードで、次のコードを黄色で強調表示して、`Page_Load` ハンドラーを更新します。 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   上記のコードを変更すると、認証オプションを含む "Providers" の DropDownList は、最初の値にリセットされません。 これにより、最初のオプションだけでなく、認証時に使用するすべてのオプションをユーザーが適切に選択できるようになります。
10. **ソリューションエクスプローラー**で、 *default.aspx*を右クリックし、 **[スタートページとして設定]** を選択します。
11. アプリをテストすることで、まずアプリをビルドし (**Ctrl**+**Shift**+**B**)、アプリを実行 (**F5**キー) し、 **[登録]** を選択して新しいユーザーアカウントを作成するか、ユーザーアカウントが既に登録されている場合は **[ログイン]** を選択します。
12. ユーザーがログインした後、ナビゲーションバーのユーザー ID (電子メールアドレス) をクリックして、 **[アカウントの管理]** ページ (.aspx) を表示します。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. **[アカウントの管理]** ページで、 **[電話番号]** の横にある **[追加]** をクリックします。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. ユーザーが SMS メッセージ (テキストメッセージ) を受信する電話番号を追加し、 **[送信]** ボタンをクリックします。   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    この時点で、アプリは web.config の資格情報を使用して*Twilio に接続*します。 SMS メッセージ (テキストメッセージ) は、ユーザーアカウントに関連付けられている電話に送信されます。 Twilio メッセージが送信されたことを確認するには、Twilio ダッシュボードを表示します。
15. 数秒後に、ユーザーアカウントに関連付けられている電話に、確認コードを含むテキストメッセージが表示されます。 確認コードを入力し、 **[送信]** を押します。  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>登録されたユーザーに対して2要素認証を有効にする

この時点で、アプリの2要素認証が有効になりました。 ユーザーが2要素認証を使用するには、UI を使用して設定を変更するだけです。 

1. アプリのユーザーは、ナビゲーションバーのユーザー ID (電子メールエイリアス) をクリックして **[アカウントの管理]** ページを表示することにより、特定のアカウントに対して2要素認証を有効にすることができます。次に、 **[有効]** にする リンクをクリックして、アカウントの2要素認証を有効にします。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. ログオフし、再度ログインします。 電子メールを有効にした場合は、2要素認証に SMS または電子メールのいずれかを選択できます。 電子メールを有効にしていない場合は、「[ユーザー登録、電子メール確認、パスワードリセットを使用して Secure ASP.NET Web フォームアプリを作成](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)する」というタイトルのチュートリアルを参照してください。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. [2 要素認証] ページが表示されます。このページでは、(SMS または電子メールから) コードを入力できます。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 [**このブラウザーを記憶**する] チェックボックスをオンにすると、チェックボックスをオンにしたブラウザーとデバイスを使用するときに、2要素認証を使用してログインする必要がなくなります。 悪意のあるユーザーがデバイスにアクセスできない限り、2要素認証を有効にし、[**このブラウザーを記憶**する] をオンにすると、信頼されていないデバイスからのすべてのアクセスに対して強力な2要素認証保護を維持しながら、便利なワンステップパスワードアクセスが提供されます。 これは、定期的に使用するプライベートあらゆるデバイスで行うことができます。

<a id="addRes"></a>
## <a name="additional-resources"></a>その他のリソース

- [ASP.NET Identity で SMS と電子メールを利用して 2 要素認証を行う](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [推奨されるリソースへのリンク ASP.NET Identity](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure Web サイトにデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms チュートリアルシリーズ-OAuth 2.0 プロバイダーの追加](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web フォームチュートリアルシリーズ-プロジェクトの SSL を有効にする](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Facebook でアプリを作成し、アプリをプロジェクトに接続する](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
