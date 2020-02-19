---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS と電子メール2要素認証を使用した ASP.NET MVC 5 アプリ |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、2要素認証を使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。 「Secure ASP.NET MVC 5 web アプリの作成」を完了する必要があります。
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457597"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>SMS や電子メールで 2 要素認証する ASP.NET MVC 5 アプリ

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、2要素認証を使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。 続行する前に[、「ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する」](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)を完了しておく必要があります。 完成したアプリケーションは[こちら](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)からダウンロードできます。 ダウンロードには、電子メールまたは SMS プロバイダーを設定せずに電子メールの確認と SMS をテストできるデバッグヘルパーが含まれています。
> 
> このチュートリアルは、 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ) によって作成されました。

- [ASP.NET MVC アプリを作成する](#createMvc)
- [2要素認証用に SMS を設定する](#SMS)
- [2要素認証を有効にする](#enable2)
- [その他のリソース](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC アプリを作成する

まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールします。

> [!NOTE]
> 警告: 続行する前に[、「ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する」](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)を完了しておく必要があります。 このチュートリアルを完了するには、 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールする必要があります。

1. 新しい ASP.NET Web プロジェクトを作成し、MVC テンプレートを選択します。 Web フォームでも ASP.NET Identity がサポートされているため、web フォームアプリで同様の手順に従うことができます。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 既定の認証は、**個々のユーザーアカウント**として残しておきます。 Azure でアプリをホストする場合は、チェックボックスをオンのままにします。 このチュートリアルの後半では、Azure にデプロイします。 [Azure アカウントは無料で開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)ことができます。
3. [SSL を使用するようにプロジェクトを](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a>2要素認証用に SMS を設定する

このチュートリアルでは、Twilio または ASPSMS を使用する手順について説明しますが、他の SMS プロバイダーを使用することもできます。

1. **SMS プロバイダーを使用したユーザーアカウントの作成**  
  
   [Twilio](https://www.twilio.com/try-twilio)または[aspsms](https://www.aspsms.com/asp.net/identity/testcredits/)アカウントを作成します。
2. **追加のパッケージのインストール、またはサービス参照の追加**  
  
   Twilio  
   パッケージ マネージャー コンソールで、次のコマンドを入力します。  
    `Install-Package Twilio`  
  
   ASPSMS:  
   次のサービス参照を追加する必要があります。  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   住所 :  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   名前空間:  
    `ASPSMSX2`
3. **SMS プロバイダーのユーザー資格情報の確認**  
  
   Twilio  
   Twilio アカウントの **[ダッシュボード]** タブで、**アカウント SID**と**認証トークン**をコピーします。  
  
   ASPSMS:  
   アカウント設定から、**ユーザーキー**に移動し、自己定義**パスワード**と共にコピーします。  
  
   これらの値は、後で `"SMSAccountIdentification"` および `"SMSAccountPassword"` キー*内の web.config ファイルに*格納されます。
4. **SenderID/オリジネータの指定**  
  
   Twilio  
   **[数値]** タブで、Twilio 電話番号をコピーします。  
  
   ASPSMS:  
   [発信元の**ロック解除**] メニュー内で、1つ以上の発信者をロック解除するか、英数字の発信者を選択します (すべてのネットワークでサポートされていません)。  
  
   この値は、後でキー `"SMSAccountFrom"`*内の web.config ファイルに*格納されます。
5. **SMS プロバイダーの資格情報をアプリに転送する**  
  
   資格情報と送信者の電話番号をアプリで使用できるようにします。 単純にするために、これらの値を web.config*ファイルに*格納します。 Azure にデプロイするときに、web サイトの構成 タブの **アプリの設定** セクションに値を安全に格納できます。 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > セキュリティ-機密データをソースコードに格納しません。 このサンプルを単純にするために、アカウントと資格情報が上記のコードに追加されています。 [ASP.NET と Azure にパスワードやその他の機密データをデプロイするためのベストプラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)をご覧ください。
6. **SMS プロバイダーへのデータ転送の実装**  
  
   *アプリ\_Start\IdentityConfig.cs*ファイルで `SmsService` クラスを構成します。  
  
   使用する SMS プロバイダーに応じて、 **Twilio**または**aspsms**セクションのいずれかをアクティブにします。 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. *Views\Manage\Index.cshtml* Razor ビューを更新します。 (注: 終了しているコードのコメントを削除するだけではなく、次のコードを使用してください)。  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. `ManageController` 内の `EnableTwoFactorAuthentication` および `DisableTwoFactorAuthentication` アクションメソッドに[[Validateアンチ Forgerytoken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)属性があることを確認します。  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. アプリを実行し、前に登録したアカウントでログインします。
10. ユーザー ID をクリックすると、`Manage` コントローラーで `Index` アクションメソッドがアクティブになります。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. [追加] をクリックします。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` アクションメソッドには、SMS メッセージを受信できる電話番号を入力するためのダイアログボックスが表示されます。

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 数秒で、確認コードを含むテキストメッセージが表示されます。 それを入力し、 **[Submit]** を押します。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. [管理] ビューには、電話番号が追加されたことが表示されます。

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>2 要素認証を有効にします。

テンプレートで生成されたアプリでは、UI を使用して2要素認証 (2FA) を有効にする必要があります。 2FA を有効にするには、ナビゲーションバーでユーザー ID (電子メールエイリアス) をクリックします。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

[2FA を有効にする] をクリックします。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

ログアウトしてから再度ログインします。 電子メールを有効にした場合 ([前のチュートリアル](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)を参照)、2FA の SMS または電子メールを選択できます。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

[コードの確認] ページが表示され、(SMS または電子メールから) コードを入力できます。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

[**このブラウザーを記憶**する] チェックボックスをオンにすると、チェックボックスをオンにしたブラウザーとデバイスを使用するときに、2fa を使用してログインする必要がありません。 悪意のあるユーザーがデバイスにアクセスできない限り、2FA を有効にし、[**このブラウザーを記憶**する] をオンにすると、信頼されていないデバイスからのすべてのアクセスに対して強力な2fa 保護を維持しながら、便利なワンステップパスワードアクセスが提供されます。 これは、定期的に使用するプライベートあらゆるデバイスで行うことができます。

このチュートリアルでは、新しい ASP.NET MVC アプリで2FA を有効にする方法について簡単に説明します。 このチュートリアルでは、 [SMS と電子メールを使用した2要素認証](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)について、サンプルの背後にあるコードについて詳しく説明します。 ASP.NET Identity。

<a id="addRes"></a>
## <a name="additional-resources"></a>その他のリソース

- [SMS と電子メールを使用した2要素認証 (ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) )2要素認証の詳細について説明します。
- [推奨されるリソースへのリンク ASP.NET Identity](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)パスワードの回復とアカウントの確認についてさらに詳しく説明します。
- [Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)このチュートリアルでは、Facebook と Google OAuth 2 認証を使用して ASP.NET MVC 5 アプリを作成する方法について説明します。 また、Id データベースにデータを追加する方法についても説明します。
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC アプリを Azure Web にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。 このチュートリアルでは、Azure のデプロイ、ロールを使用してアプリをセキュリティで保護する方法、メンバーシップ API を使用してユーザーとロールを追加する方法、および追加のセキュリティ機能を追加します。
- [OAuth 2 用の Google アプリを作成し、そのアプリをプロジェクトに接続する](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook でアプリを作成し、アプリをプロジェクトに接続する](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [プロジェクトでの SSL の設定](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [C#と ASP.NET MVC 開発環境を設定する方法](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
