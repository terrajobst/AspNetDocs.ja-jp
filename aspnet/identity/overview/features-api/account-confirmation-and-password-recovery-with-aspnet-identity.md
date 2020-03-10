---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: アカウントの確認 & パスワードの回復-C#ASP.NET Identity ()-ASP.NET 4.x
author: HaoK
description: このチュートリアルを実行する前に、「ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する」を完了しておく必要があります。 このチュートリアル...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4b2c88280df39aa81d60f9508910e8fe5d6db6b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499984"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>ASP.NET Identity (C#) を使用したアカウントの確認とパスワードの回復

> このチュートリアルを実行する前に[、「ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する」](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)を完了しておく必要があります。 このチュートリアルでは詳細について説明します。また、ローカルアカウントの確認のために電子メールを設定し、ユーザーが ASP.NET Identity で忘れたパスワードをリセットできるようにする方法についても説明します。

ローカルユーザーアカウントでは、ユーザーはアカウントのパスワードを作成する必要があり、そのパスワードは web アプリで (安全に) 格納されます。 ASP.NET Identity は、ユーザーがアプリのパスワードを作成する必要がないソーシャルアカウントもサポートしています。 [ソーシャルアカウント](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)は、サードパーティ (Google、Twitter、Facebook、Microsoft など) を使用してユーザーを認証します。 このトピックでは、以下の内容を説明します。

- [ASP.NET MVC アプリを作成](#createMvc)し、ASP.NET Identity の機能を調べます。
- [Id サンプルをビルドする](#build)
- [電子メールの確認を設定する](#email)

新しいユーザーが自分の電子メールエイリアスを登録すると、ローカルアカウントが作成されます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

[登録] ボタンを選択すると、検証トークンを含む確認メールが電子メールアドレスに送信されます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

ユーザーには、アカウントの確認トークンを含む電子メールが送信されます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

リンクを選択すると、アカウントが確認されます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>パスワードの回復/リセット

ローカルユーザーのパスワードを忘れた場合、セキュリティトークンを電子メールアカウントに送信して、パスワードをリセットできるようにすることができます。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
ユーザーはすぐに、パスワードをリセットするためのリンクを含む電子メールを受け取ります。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
リンクを選択すると、[リセット] ページに移動します。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
**[リセット]** ボタンを選択すると、パスワードがリセットされたことが確認されます。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>ASP.NET Web アプリを作成する

まず、 [Visual Studio 2017](https://visualstudio.microsoft.com/)をインストールして実行します。

1. 新しい ASP.NET Web プロジェクトを作成し、MVC テンプレートを選択します。 Web フォームでも ASP.NET Identity がサポートされているため、web フォームアプリで同様の手順に従うことができます。
2. 認証を個々の**ユーザーアカウント**に変更します。
3. アプリを実行し、 **[登録]** リンクを選択してユーザーを登録します。 この時点で、電子メールの検証は、 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性でのみ行うことができます。
4. サーバーエクスプローラーで、 **[Data Connections\DefaultConnection\Tables\AspNetUsers]** に移動し、右クリックして、 **[テーブル定義を開く]** を選択します。

    次の図は、`AspNetUsers` スキーマを示しています。

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. **AspNetUsers**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   この時点で、電子メールは確認されていません。

ASP.NET Identity の既定のデータストアは Entity Framework ですが、他のデータストアを使用したり、フィールドを追加したりするように構成することができます。 このチュートリアルの最後にある「[その他のリソース](#addRes)」セクションを参照してください。

[OWIN startup クラス](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md)( *Startup.cs* ) は、アプリの起動時に呼び出され、 *app\_Start\Startup.Auth.cs*の `ConfigureAuth` メソッドを呼び出します。これにより、OWIN パイプラインが構成され、ASP.NET Identity が初期化されます。 `ConfigureAuth` メソッドを調べます。 各 `CreatePerOwinContext` 呼び出しは、指定された型のインスタンスを作成するために要求ごとに1回呼び出されるコールバック (`OwinContext`に保存されます) を登録します。 コンストラクターにブレークポイントを設定し、各型 (`ApplicationDbContext, ApplicationUserManager`) の `Create` メソッドを設定して、各要求で呼び出されることを確認できます。 `ApplicationDbContext` と `ApplicationUserManager` のインスタンスは OWIN コンテキストに格納され、アプリケーション全体でアクセスできます。 クッキーミドルウェアを使用して OWIN パイプラインにフックする ASP.NET Identity ます。 詳細については、 [ASP.NET Identity の UserManager クラスの要求ごとの有効期間管理に](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)関する説明を参照してください。

セキュリティプロファイルを変更すると、新しいセキュリティスタンプが生成され、 *AspNetUsers*テーブルの `SecurityStamp` フィールドに格納されます。 `SecurityStamp` フィールドは、セキュリティ cookie とは異なります。 セキュリティクッキーは `AspNetUsers` テーブル (または Id DB 内の他の場所) に格納されません。 セキュリティ cookie トークンは、 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)を使用して自己署名され、`UserId, SecurityStamp` と有効期限情報を使用して作成されます。

Cookie ミドルウェアは、各要求の cookie を確認します。 `Startup` クラスの `SecurityStampValidator` メソッドは、データベースにヒットし、`validateInterval`で指定されているように、セキュリティスタンプを定期的にチェックします。 これは、セキュリティプロファイルを変更しない限り、30分 (このサンプルでは) ごとに実行されます。 データベースへのトリップを最小限に抑えるために、30分間隔が選択されました。 詳細については[、「2要素認証チュートリアル](index.md)」を参照してください。

`UseCookieAuthentication` メソッドは、コード内のコメントに従って cookie 認証をサポートします。 `SecurityStamp` のフィールドと関連付けられたコードによって、アプリに追加のセキュリティ層が提供されます。パスワードを変更すると、ログインに使用したブラウザーからログアウトされます。 `SecurityStampValidator.OnValidateIdentity` メソッドを使用すると、ユーザーがログインするときに、アプリはセキュリティトークンを検証できます。パスワードを変更したり、外部ログインを使用したりするときに使用されます。 これは、古いパスワードを使用して生成されたトークン (cookie) がすべて無効になるようにするために必要です。 サンプルプロジェクトでは、ユーザーのパスワードを変更すると、ユーザーの新しいトークンが生成され、以前のトークンは無効になり `SecurityStamp` フィールドが更新されます。

Id システムを使用すると、ユーザーのセキュリティプロファイルが変更されたとき (たとえば、ユーザーがパスワードを変更したり、関連付けられているログイン (Facebook、Google、Microsoft アカウントなど) を変更したりしたときに、ユーザーがログオフしてからログアウトするようにアプリを構成することができます。ブラウザーインスタンス。 たとえば、次の図は、1つのボタンを選択することによって、ユーザーがすべてのブラウザーインスタンス (この場合は IE、Firefox、Chrome) からサインアウトできる[サインアウトサンプル](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample)アプリを示しています。 または、サンプルを使用すると、特定のブラウザーインスタンスからのみログアウトできます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[シングルサインアウトサンプル](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample)アプリでは、ASP.NET Identity でセキュリティトークンを再生成する方法を示しています。 これは、古いパスワードを使用して生成されたトークン (cookie) がすべて無効になるようにするために必要です。 この機能により、アプリケーションのセキュリティが強化されます。パスワードを変更すると、このアプリケーションにログインした場所でログアウトされます。

*アプリ\_Start\IdentityConfig.cs*ファイルには、`ApplicationUserManager`、`EmailService`、および `SmsService` の各クラスが含まれています。 `EmailService` クラスと `SmsService` クラスはそれぞれ `IIdentityMessageService` インターフェイスを実装します。そのため、各クラスには、電子メールと SMS を構成するための一般的なメソッドが用意されています。 このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して電子メール通知を追加する方法のみを示していますが、SMTP などのメカニズムを使用して電子メールを送信することもできます。

`Startup` クラスには、ソーシャルログイン (Facebook、Twitter など) を追加するためのボイラープレートも含まれています。詳細については、 [facebook、twitter、LinkedIn、Google OAuth2 サインオンを使用した my チュートリアル MVC 5 アプリ](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)を参照してください。

`ApplicationUserManager` クラスを調べます。このクラスには、ユーザーの id 情報が含まれており、次の機能が構成されています。

- パスワードの強度の要件。
- ユーザーのロックアウト (試行回数と時間)。
- 2要素認証 (2FA)。 もう1つのチュートリアルでは、2FA と SMS について説明します。
- 電子メールと SMS サービスをフックする。 (別のチュートリアルで SMS について説明します)。

`ApplicationUserManager` クラスは、ジェネリック `UserManager<ApplicationUser>` クラスから派生します。 `ApplicationUser` は、[ユーザー](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)から派生します。 `IdentityUser` は、ジェネリック `IdentityUser` クラスから派生します。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

上のプロパティは、上に示した `AspNetUsers` テーブルのプロパティと一致します。

`IUser` の汎用引数を使用すると、主キーに対して異なる型を使用してクラスを派生させることができます。 主キーを文字列から int または GUID に変更する方法を示す[Changepk](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)サンプルを参照してください。

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`) は、 *Models\IdentityModels.cs*で次のように定義されています。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

上の強調表示されたコードは、 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)を生成します。 ASP.NET Identity と OWIN Cookie 認証はクレームベースであるため、フレームワークでは、ユーザーの `ClaimsIdentity` を生成するようにアプリに要求します。 `ClaimsIdentity` には、ユーザーの名前、年齢、ユーザーが属するロールなど、ユーザーのすべての要求に関する情報が含まれています。 この段階で、ユーザーに対する要求をさらに追加することもできます。

OWIN `AuthenticationManager.SignIn` メソッドは、`ClaimsIdentity` を渡し、ユーザーにサインインします。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリ](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)は、`ApplicationUser` クラスにプロパティを追加する方法を示しています。

## <a name="email-confirmation"></a>電子メールの確認

新しいユーザーが登録した電子メールを確認して、他のユーザーが偽装していないこと (つまり、他のユーザーの電子メールに登録されていないこと) を確認することをお勧めします。 ディスカッションフォーラムがあるとしたら、`"bob@example.com"` が `"joe@contoso.com"`として登録されないようにしたいと考えています。 電子メールを確認しないと、`"joe@contoso.com"` アプリから不要な電子メールを受け取る可能性があります。 Bob が誤って `"bib@example.com"` として登録されていて気付かないとしても、アプリには正しい電子メールがないため、パスワードの回復を使用することはできません。 電子メールの確認では、bot から制限された保護のみを提供し、特定のスパム送信者からの保護を提供しません。登録に使用できる多くの勤務先の電子メールエイリアスがあります。次のサンプルでは、アカウントが確認されるまで、ユーザーはパスワードを変更できません (登録した電子メールアカウントで受信した確認リンクを選択します)。この作業フローを他のシナリオに適用できます。たとえば、管理者が作成した新しいアカウントのパスワードを確認およびリセットするためのリンクを送信したり、ユーザーがプロファイルを変更したときに電子メールを送信したりすることができます。 通常は、電子メール、SMS テキストメッセージ、または別のメカニズムによって確認される前に、新しいユーザーが web サイトにデータを投稿できないようにします。 <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>より完全なサンプルをビルドする

このセクションでは、NuGet を使用して、使用するより完全なサンプルをダウンロードします。

1. 新しい***空***の ASP.NET Web プロジェクトを作成します。
2. パッケージマネージャーコンソールで、次のコマンドを入力します。 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して電子メールを送信します。 `Identity.Samples` パッケージによって、使用するコードがインストールされます。
3. [SSL を使用するようにプロジェクトを](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。
4. アプリを実行し、 **[登録]** リンクを選択して、登録フォームを投稿することで、ローカルアカウントの作成をテストします。
5. 電子メールの確認をシミュレートするデモ用電子メールのリンクを選択します。
6. サンプルからデモ用電子メールリンクの確認コードを削除します (アカウントコントローラーの `ViewBag.Link` コード)。 `DisplayEmail` と `ForgotPasswordConfirmation` のアクションメソッドと razor ビュー) を参照してください。

> [!WARNING]
> このサンプルのセキュリティ設定を変更した場合、生産アプリは、行われた変更を明示的に呼び出すセキュリティ監査を受ける必要があります。

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>App\_Start\IdentityConfig.cs のコードを確認する

このサンプルでは、アカウントを作成し、*管理者*ロールに追加する方法を示します。 サンプルの電子メールは、管理者アカウントに使用する電子メールに置き換える必要があります。 管理者アカウントを作成するための最も簡単な方法は、プログラムで `Seed` 方法です。 ユーザーとロールを作成および管理するためのツールを今後用意する予定です。 サンプルコードを使用すると、ユーザーとロールを作成および管理できますが、ロールとユーザー管理ページを実行するには、まず管理者アカウントが必要です。 このサンプルでは、DB がシード処理されるときに管理者アカウントが作成されます。

パスワードを変更し、電子メール通知を受信できるアカウントに名前を変更します。

> [!WARNING]
> セキュリティ-機密データをソースコードに格納しません。

前に説明したように、startup クラスの `app.CreatePerOwinContext` 呼び出しは、アプリケーション DB コンテンツ、ユーザーマネージャー、およびロールマネージャークラスの `Create` メソッドにコールバックを追加します。 OWIN パイプラインは、各要求に対してこれらのクラスの `Create` メソッドを呼び出し、各クラスのコンテキストを格納します。 アカウントコントローラーは、HTTP コンテキスト (OWIN コンテキストを含む) からユーザーマネージャーを公開します。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

ユーザーがローカルアカウントを登録すると、`HTTP Post Register` メソッドが呼び出されます。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

上記のコードでは、モデルデータを使用して、入力された電子メールとパスワードを使用して新しいユーザーアカウントを作成します。 データストアに電子メールエイリアスが含まれている場合、アカウントの作成は失敗し、フォームが再び表示されます。 `GenerateEmailConfirmationTokenAsync` メソッドは、セキュリティで保護された確認トークンを作成し、ASP.NET Identity データストアに格納します。 [Url. Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx)メソッドは、`UserId` と確認トークンを含むリンクを作成します。 その後、このリンクはユーザーに電子メールで送信され、ユーザーは電子メールアプリ内のリンクを選択してアカウントを確認することができます。

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>電子メールの確認を設定する

[Azure SendGrid のサインアップページ](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)にアクセスし、無料アカウントに登録します。 SendGrid を構成するには、次のようなコードを追加します。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 電子メールクライアントは、テキストメッセージのみを頻繁に受け入れます (HTML は使用しません)。 メッセージはテキストと HTML で提供する必要があります。 上記の SendGrid サンプルでは、上記の `myMessage.Text` と `myMessage.Html` コードを使用してこれを行います。

次のコードは、 [send-mailmessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx)クラスを使用して電子メールを送信する方法を示しています。ここで `message.Body` はリンクのみを返します。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> セキュリティ-機密データをソースコードに格納しません。 アカウントと資格情報は appSetting に格納されます。 Azure では、これらの値を Azure portal の [ **[構成](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] タブに安全に格納できます。 [ASP.NET と Azure にパスワードやその他の機密データをデプロイするためのベストプラクティス](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)をご覧ください。

SendGrid の資格情報を入力し、アプリを実行して、電子メールのエイリアスで登録します。電子メールの [確認] リンクを選択できます。 [Outlook.com](http://outlook.com)の電子メールアカウントでこれを行う方法については、 [ C# Outlook.Com smtp Host の John の smtp 構成に関する](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx)記事 ASP.NET Identity と「[2.0: アカウントの検証と2要素認証](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)の投稿の設定」を参照してください。

ユーザーが**登録**ボタンを選択すると、検証トークンを含む確認メールが電子メールアドレスに送信されます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

ユーザーには、アカウントの確認トークンを含む電子メールが送信されます。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>コードを確認する

次のコードは `POST ForgotPassword` メソッドを示します。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

ユーザーの電子メールが確認されていない場合、メソッドはサイレントモードで失敗します。 無効な電子メールアドレスに対してエラーがポストされた場合、悪意のあるユーザーがその情報を使用して、攻撃対象の有効なユーザー Id (電子メールエイリアス) を見つけることができます。

次のコードは、ユーザーが送信された電子メールで確認リンクを選択したときに呼び出される account controller の `ConfirmEmail` メソッドを示しています。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

忘れたパスワードトークンが使用されると、無効になります。 `Create` メソッド ( *App\_Start\IdentityConfig.cs*ファイル内) の次のコード変更により、トークンの有効期限が3時間に設定されます。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

上記のコードでは、忘れたパスワードと電子メール確認トークンの有効期限が3時間で切れます。 既定の `TokenLifespan` は1日です。

次のコードは、電子メールの確認方法を示しています。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 アプリのセキュリティを強化するために、ASP.NET Identity では2要素認証 (2FA) がサポートされています。 「 [ASP.NET Identity 2.0: アカウントの検証の設定」と「John の規則による2要素認証の設定](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)」を参照してください。 ログインパスワードの試行に失敗したときにアカウントのロックアウトを設定することはできますが、この方法を使用すると、ログインが[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)ロックアウトの影響を受けやすくなります。 アカウントロックアウトは、2FA でのみ使用することをお勧めします。  
<a id="addRes"></a>

## <a name="additional-resources"></a>その他のリソース

- [ASP.NET Identity のカスタム ストレージ プロバイダーの概要](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリで](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)は、ユーザーテーブルにプロファイル情報を追加する方法についても説明しています。
- [ASP.NET MVC And Identity 2.0: John の基本を理解](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)しています。
- [ASP.NET Identity 入門](../getting-started/introduction-to-aspnet-identity.md)
- Pranav Rastogi による[ASP.NET Identity 2.0.0 の RTM を発表](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)します。
