---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: SMS と電子メールを使用した2要素認証 (ASP.NET Identity-ASP.NET 4.x)
author: HaoK
description: このチュートリアルでは、SMS と電子メールを使用して2要素認証 (2FA) を設定する方法について説明します。 この記事は、Rick Anderson (@RickAndMSFT), Pr...
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499870"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>SMS と電子メールを使用した2要素認証 (ASP.NET Identity)

[Hao Kung](https://github.com/HaoK)、 [Pranav rastogi](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [suhas Joshi](https://github.com/suhasj)

> このチュートリアルでは、SMS と電子メールを使用して2要素認証 (2FA) を設定する方法について説明します。
> 
> この記事は、Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT))、Pranav Rastogi ([@rustd](https://twitter.com/rustd))、Hao Kung、suhas Joshi によって作成されました。 NuGet サンプルは、主に Hao Kung によって作成されました。

このトピックでは、以下の内容を説明します。

- [Id サンプルのビルド](#build)
- [2要素認証用に SMS を設定する](#SMS)
- [2要素認証を有効にする](#enable2)
- [2要素認証プロバイダーを登録する方法](#reg)
- [ソーシャルおよびローカルログインアカウントの結合](#combine)
- [ブルートフォース攻撃からのアカウントロックアウト](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>Id サンプルのビルド

このセクションでは、NuGet を使用して、使用するサンプルをダウンロードします。 まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールします。

> [!NOTE]
> 警告: このチュートリアルを完了するには、Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)をインストールする必要があります。

1. 新しい***空***の ASP.NET Web プロジェクトを作成します。
2. パッケージマネージャーコンソールで、次のコマンドを入力します。  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して、sms テキストに電子メール、 [Twilio](https://www.twilio.com/) 、または[aspsms](https://www.aspsms.com/asp.net/identity/testcredits/)を送信します。 `Identity.Samples` パッケージによって、使用するコードがインストールされます。
3. [SSL を使用するようにプロジェクトを](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。
4. *省略可能*: sendgrid をフックしてアプリを実行し、電子メールアカウントを登録するには、[電子メールの確認チュートリアル](account-confirmation-and-password-recovery-with-aspnet-identity.md)に記載されている手順に従ってください。
5. *省略可能:* サンプルからデモ用電子メールリンクの確認コードを削除します (アカウントコントローラーの `ViewBag.Link` コード)。 `DisplayEmail` と `ForgotPasswordConfirmation` のアクションメソッドと razor ビュー) を参照してください。
6. *省略可能:* `ViewBag.Status` コードを管理およびアカウントコントローラーから削除し、 *Views\Account\VerifyCode.cshtml*および*Views\Manage\VerifyPhoneNumber.cshtml* razor ビューから削除します。 または、`ViewBag.Status` の表示を保持して、電子メールや SMS メッセージをフックして送信することなく、このアプリがローカルで動作する方法をテストすることもできます。

> [!NOTE]
> 警告: このサンプルのセキュリティ設定を変更した場合、生産アプリは、行われた変更を明示的に呼び出すセキュリティ監査を受ける必要があります。

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
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   Address:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   名前空間:  
    `ASPSMSX2`
3. **SMS プロバイダーのユーザー資格情報の確認**  
  
   Twilio  
   Twilio アカウントの **[ダッシュボード]** タブで、**アカウント SID**と**認証トークン**をコピーします。  
  
   ASPSMS:  
   アカウント設定から、**ユーザーキー**に移動し、自己定義**パスワード**と共にコピーします。  
  
   これらの値は、後で `SMSAccountIdentification` および `SMSAccountPassword` 変数に格納します。
4. **SenderID/オリジネータの指定**  
  
   Twilio  
   **[数値]** タブで、Twilio 電話番号をコピーします。  
  
   ASPSMS:  
   [発信元の**ロック解除**] メニュー内で、1つ以上の発信者をロック解除するか、英数字の発信者を選択します (すべてのネットワークでサポートされていません)。  
  
   この値は、後で変数 `SMSAccountFrom` に格納します。
5. **SMS プロバイダーの資格情報をアプリに転送する**  
  
   資格情報と送信者の電話番号をアプリで使用できるようにします。

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > セキュリティ-機密データをソースコードに格納しません。 このサンプルを単純にするために、アカウントと資格情報が上記のコードに追加されています。 「Jon の[ASP.NET MVC: ソース管理からプライベート設定を保持](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)する」を参照してください。
6. **SMS プロバイダーへのデータ転送の実装**  
  
   *アプリ\_Start\IdentityConfig.cs*ファイルで `SmsService` クラスを構成します。  
  
   使用する SMS プロバイダーに応じて、 **Twilio**または**aspsms**セクションのいずれかをアクティブにします。 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. アプリを実行し、前に登録したアカウントでログインします。
8. ユーザー ID をクリックすると、`Manage` コントローラーで `Index` アクションメソッドがアクティブになります。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. [追加] をクリックします。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. 数秒で、確認コードを含むテキストメッセージが表示されます。 それを入力し、 **[Submit]** を押します。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. [管理] ビューには、電話番号が追加されたことが表示されます。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>コードを確認する

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

`Manage` controller の `Index` アクションメソッドは、前のアクションに基づいてステータスメッセージを設定し、ローカルパスワードを変更するか、ローカルアカウントを追加するためのリンクを提供します。 また、`Index` 方法では、状態または2FA 電話番号、外部ログイン、2FA が有効になっていること、およびこのブラウザーの [2FA] (後で説明します) を記憶していることを示します。 タイトルバーのユーザー ID (電子メール) をクリックしても、メッセージは渡されません。 **[電話番号: 削除]** リンクをクリックすると、クエリ文字列として `Message=RemovePhoneSuccess` が渡されます。  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber` アクションメソッドには、SMS メッセージを受信できる電話番号を入力するためのダイアログボックスが表示されます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

**[確認コードの送信]** ボタンをクリックすると、HTTP POST `AddPhoneNumber` アクションメソッドに電話番号が投稿されます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync` メソッドは、SMS メッセージで設定されるセキュリティトークンを生成します。 SMS サービスが構成されている場合、トークンは文字列として送信され &quot;セキュリティコードはトークン&gt;&quot;&lt;ます。 `SmsService.SendAsync` メソッドを非同期的に呼び出すと、アプリが `VerifyPhoneNumber` アクションメソッド (次のダイアログを表示) にリダイレクトされます。ここで、確認コードを入力できます。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

コードを入力して [送信] をクリックすると、コードが HTTP POST `VerifyPhoneNumber` アクションメソッドにポストされます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync` メソッドは、ポストされたセキュリティコードを確認します。 コードが正しい場合は、電話番号が `AspNetUsers` テーブルの [`PhoneNumber`] フィールドに追加されます。 この呼び出しが成功すると、`SignInAsync` メソッドが呼び出されます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent` パラメーターは、認証セッションを複数の要求にわたって永続化するかどうかを設定します。

セキュリティプロファイルを変更すると、新しいセキュリティスタンプが生成され、 *AspNetUsers*テーブルの `SecurityStamp` フィールドに格納されます。 `SecurityStamp` フィールドは、セキュリティ cookie とは異なります。 セキュリティクッキーは `AspNetUsers` テーブル (または Id DB 内の他の場所) に格納されません。 セキュリティ cookie トークンは、 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)を使用して自己署名され、`UserId, SecurityStamp` と有効期限情報を使用して作成されます。

Cookie ミドルウェアは、各要求の cookie を確認します。 `Startup` クラスの `SecurityStampValidator` メソッドは、データベースにヒットし、`validateInterval`で指定されているように、セキュリティスタンプを定期的にチェックします。 これは、セキュリティプロファイルを変更しない限り、30分 (このサンプルでは) ごとに実行されます。 データベースへのトリップを最小限に抑えるために、30分間隔が選択されました。

セキュリティプロファイルに何らかの変更が加えられた場合は、`SignInAsync` メソッドを呼び出す必要があります。 セキュリティプロファイルが変更されると、データベースは `SecurityStamp` フィールドを更新し、`SignInAsync` メソッドを呼び出さずに、次回の OWIN パイプラインがデータベース (`validateInterval` *) に到達するまでログイン*したままになります。 これをテストするには、`SignInAsync` メソッドを変更してすぐに制御を戻し、cookie の `validateInterval` プロパティを30分から5秒に設定します。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

上記のコード変更により、セキュリティプロファイルを変更することができます (たとえば、 **2 要素が有効になっている**状態を変更することによって)。 `SecurityStampValidator.OnValidateIdentity` 方法が失敗すると、5秒後にログアウトされます。 `SignInAsync` メソッドの改行を削除し、別のセキュリティプロファイルを変更して、ログアウトしないようにします。`SignInAsync` メソッドは、新しいセキュリティクッキーを生成します。

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>2 要素認証を有効にします。

サンプルアプリでは、UI を使用して2要素認証 (2FA) を有効にする必要があります。 2FA を有効にするには、ナビゲーションバーでユーザー ID (電子メールエイリアス) をクリックします。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
[2FA を有効にする] をクリックします。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) ログアウトしてから再度ログインします。 電子メールを有効にした場合 ([前のチュートリアル](account-confirmation-and-password-recovery-with-aspnet-identity.md)を参照)、2FA の SMS または電子メールを選択できます。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) [コードの確認] ページが表示され、(SMS または電子メールから) コードを入力できます。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) [**このブラウザーを記憶**する] チェックボックスをオンにすると、2fa を使用してそのコンピューターとブラウザーでログオンする必要がなくなります。 2FA を有効にし、[**このブラウザーを記憶**する] をクリックすると、悪意のあるユーザーが自分のアカウントにアクセスしようとしても、コンピューターへのアクセス権がない限り、強力な2fa による保護が提供されます。 この操作は、定期的に使用する任意のプライベートコンピューターで行うことができます。 [**このブラウザーを記憶**する] を設定すると、日常的に使用していないコンピューターから2fa のセキュリティが強化され、自分のコンピューターで2fa を使用する必要がなくなります。 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>2要素認証プロバイダーを登録する方法

新しい MVC プロジェクトを作成すると、 *IdentityConfig.cs*ファイルには、2要素認証プロバイダーを登録するための次のコードが含まれます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>2FA の電話番号を追加する

`Manage` コントローラーの `AddPhoneNumber` アクションメソッドは、セキュリティトークンを生成し、指定した電話番号に送信します。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

トークンを送信した後、`VerifyPhoneNumber` アクションメソッドにリダイレクトされます。このメソッドでは、2FA に SMS を登録するためのコードを入力できます。 SMS 2FA は、電話番号を確認するまで使用されません。

## <a name="enabling-2fa"></a>2FA を有効にする

`EnableTFA` アクションメソッドを使用すると、2FA が有効になります。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

[2FA を有効にする] がセキュリティプロファイルに変更されているため、`SignInAsync` を呼び出す必要があることに注意してください。 2FA が有効になっている場合、ユーザーは、登録されている2FA アプローチ (サンプルでは SMS と電子メール) を使用して、ログインに2FA を使用する必要があります。

QR コードジェネレーターなど、さらに2FA プロバイダーを追加することも、独自に作成することもできます (「 [ASP.NET Identity で Google Authenticator を使用](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)する」を参照してください)。

> [!NOTE]
> 2FA コードは、[時間ベースのワンタイムパスワードアルゴリズム](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)を使用して生成され、コードは6分間有効です。 コードを入力するのに6分以上かかる場合は、無効なコードエラーメッセージが表示されます。

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>ソーシャルおよびローカルログインアカウントの結合

電子メールリンクをクリックして、ローカルアカウントとソーシャルアカウントを組み合わせることができます。 次の順序で &quot;RickAndMSFT@gmail.com&quot; は最初にローカルログインとして作成されますが、最初にアカウントをソーシャルログとして作成してから、ローカルログインを追加することができます。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

**[管理]** リンクをクリックします。 このアカウントに関連付けられている0外部 (ソーシャルログイン) に注意してください。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

別のログインサービスへのリンクをクリックし、アプリの要求を受け入れます。 2つのアカウントが結合されているので、いずれかのアカウントでログオンすることができます。 認証サービスのソーシャルログがダウンした場合、またはソーシャルアカウントへのアクセスが失われる可能性がある場合に備えて、ユーザーにローカルアカウントを追加することをお勧めします。

次の図では、Tom はソーシャルログ (ページに表示されている**外部ログイン: 1**から参照できます) です。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

**[パスワードの選択]** をクリックすると、同じアカウントに関連付けられているローカルログオンを追加できます。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>ブルートフォース攻撃からのアカウントロックアウト

ユーザーロックアウトを有効にすることによって、アプリケーションのアカウントを辞書攻撃から保護することができます。 `ApplicationUserManager Create` メソッドの次のコードは、ロックアウトを構成します。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

上記のコードでは、2要素認証のロックアウトのみが有効になっています。 アカウントコントローラーの `Login` 方法で `shouldLockout` を true に変更することで、ログインのロックアウトを有効にすることができますが、ログインのロックアウトを有効にしないことをお勧めします。これは、アカウントが[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)ログイン攻撃の影響を受けやすくなるためです。 このサンプルコードでは、`ApplicationDbInitializer Seed` メソッドで作成された管理者アカウントのロックアウトが無効になっています。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>検証済みの電子メールアカウントをユーザーに要求する

次のコードでは、ユーザーがログインする前に、検証済みの電子メールアカウントを持っている必要があります。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>SignInManager が2FA 要件を確認する方法

ローカルログインとソーシャルログの両方で、2FA が有効になっているかどうかを確認します。 2FA が有効になっている場合、`SignInManager` ログオンメソッドは `SignInStatus.RequiresVerification`を返し、ユーザーは `SendCode` アクションメソッドにリダイレクトされます。このメソッドでは、ログインシーケンスを完了するためにコードを入力する必要があります。 ユーザーがユーザーのローカルクッキーに対して RememberMe が設定されている場合、`SignInManager` は `SignInStatus.Success` を返し、2FA を通過する必要はありません。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

次のコードは、`SendCode` アクションメソッドを示しています。 [Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)は、ユーザーに対して有効になっているすべての2fa メソッドを使用して作成されます。 [Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)は[DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper に渡されます。これにより、ユーザーは2fa アプローチ (通常は電子メールと SMS) を選択できます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

ユーザーが2FA アプローチを投稿すると、`HTTP POST SendCode` アクションメソッドが呼び出され、`SignInManager` は2FA コードを送信します。ユーザーは `VerifyCode` アクションメソッドにリダイレクトされ、ユーザーはログインを完了するコードを入力できます。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA ロックアウト

ログインパスワードの試行に失敗したときにアカウントのロックアウトを設定することはできますが、この方法を使用すると、ログインが[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)ロックアウトの影響を受けやすくなります。 アカウントロックアウトは、2FA でのみ使用することをお勧めします。 `ApplicationUserManager` が作成されると、サンプルコードは2FA のロックアウトと `MaxFailedAccessAttemptsBeforeLockout` を5に設定します。 ユーザーがローカルアカウントまたはソーシャルアカウントを使用してログインすると、2FA に失敗した各試行が保存されます。最大試行回数に達すると、ユーザーは5分間ロックアウトされます (ロックアウト時間は `DefaultAccountLockoutTimeSpan`で設定できます)。

<a id="addRes"></a>

## <a name="additional-resources"></a>その他のリソース

- [推奨されるリソースの ASP.NET Identity](../getting-started/aspnet-identity-recommended-resources.md)Id ブログ、ビデオ、チュートリアル、および優れたリンクの一覧が完成しました。
- [Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリで](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)は、ユーザーテーブルにプロファイル情報を追加する方法についても説明しています。
- [ASP.NET MVC And Identity 2.0: John の基本を理解](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)しています。
- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Identity 入門](../getting-started/introduction-to-aspnet-identity.md)
- Pranav Rastogi による[ASP.NET Identity 2.0.0 の RTM を発表](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)します。
- [ASP.NET Identity 2.0: 加藤さんがアカウントの検証と2要素認証を設定](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)しています。
