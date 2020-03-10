---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用して MVC 5 アプリC#を作成する () |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ユーザーが外部事前の資格情報を使用して OAuth 2.0 を使用してログインできるようにする ASP.NET MVC 5 web アプリケーションを構築する方法について説明します。
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456508"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Facebook、Twitter、LinkedIn、Google の OAuth2 サインオンを使用して ASP.NET MVC 5 アプリを作成する (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、ユーザーが Facebook、Twitter、LinkedIn、Microsoft、Google などの外部認証プロバイダーからの資格情報を使用して[OAuth 2.0](http://oauth.net/2/)を使用してログインできるようにする、ASP.NET MVC 5 web アプリケーションを構築する方法について説明します。 わかりやすくするために、このチュートリアルでは Facebook と Google の資格情報を使用する方法について説明します。
> 
> Web サイトでこれらの資格情報を有効にすると、これらの外部プロバイダーのアカウントが何百万ものユーザーに既に存在するため、大きな利点があります。 このようなユーザーは、新しい資格情報のセットを作成して記憶する必要がない場合に、サイトにサインアップすることができます。
> 
> 「 [ASP.NET MVC 5 app WITH SMS」と「Email 2 Factor authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)」も参照してください。
> 
> このチュートリアルでは、ユーザーのプロファイルデータを追加する方法と、メンバーシップ API を使用してロールを追加する方法についても説明します。 このチュートリアルは[Rick Anderson](https://blogs.msdn.com/rickAndy)によって作成されました (Twitter の[@RickAndMSFT](https://twitter.com/RickAndMSFT) )。

<a id="start"></a>
## <a name="getting-started"></a>作業の開始

まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールします。 Dropbox、GitHub、Linkedin、Instagram、Buffer、Salesforce、蒸気、Stack Exchange、Tripit、Twitch、Twitter、Yahoo! などのヘルプについては、この[サンプルプロジェクト](https://github.com/matthewdunsdon/oauthforaspnet)を参照してください。

> [!NOTE]
> Google OAuth 2 を使用し、SSL 警告なしでローカルにデバッグするには、Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールする必要があります。

**スタート**ページで **[新しいプロジェクト]** をクリックするか、メニューを使用して **[ファイル]** 、 **[新しいプロジェクト]** の順に選択します。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>最初のアプリケーションの作成

**[新しいプロジェクト]** をクリックし、左側の **[ビジュアルC# ]** 、 **[web]** の順に選択し、 **[ASP.NET web Application]** を選択します。 プロジェクトに "MvcAuth" という名前を指定し、 **[OK]** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

**[New ASP.NET Project]** ダイアログボックスで、 **[MVC]** をクリックします。 認証が**個々のユーザーアカウント**ではない場合は、 **[認証の変更]** ボタンをクリックして、**個々のユーザーアカウント**を選択します。 **クラウドでホスト**を確認することで、アプリは Azure で非常に簡単にホストできます。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

**クラウドで [ホスト**] を選択した場合は、[構成] ダイアログボックスが表示されます。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>NuGet を使用して最新の OWIN ミドルウェアに更新する

NuGet パッケージマネージャーを使用して、 [OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)を更新します。 左側のメニューで **[更新プログラム]** を選択します。 **[すべて更新]** ボタンをクリックするか、OWIN パッケージのみを検索することができます (次の図を参照)。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

次の図では、OWIN パッケージのみが表示されています。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

パッケージマネージャーコンソール (PMC) から `Update-Package` コマンドを入力すると、すべてのパッケージが更新されます。

**F5**キーを押すか、Ctrl キーを押し**ながら f5**キーを押してアプリケーションを実行します。 次の図では、ポート番号は1234です。 アプリケーションを実行すると、別のポート番号が表示されます。

ブラウザーウィンドウのサイズによっては、ナビゲーションアイコンをクリックして、 **[ホーム]** 、 **[バージョン情報]** 、 **[連絡先]** 、 **[登録]** 、 **[ログイン]** リンクを表示することが必要になる場合があります。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>プロジェクトでの SSL の設定

Google や Facebook などの認証プロバイダーに接続するには、SSL を使用するように IIS Express を設定する必要があります。 ログイン後に SSL を使用して、HTTP に戻るのではなく、ログイン cookie をユーザー名とパスワードと同じように秘密にし、SSL を使用せずにネットワーク経由でクリアテキストで送信することが重要です。 また、MVC パイプラインを実行する前に、ハンドシェイクを実行し、チャネルをセキュリティで保護する (HTTP よりも HTTPS の速度が非常に遅い) こともあります。そのため、ログインした後に HTTP にリダイレクトすると、現在の要求は行われません。要求の速度が大幅に向上します。

1. **ソリューションエクスプローラー**で、 **MvcAuth**プロジェクトをクリックします。
2. F4 キーを押すと、プロジェクトのプロパティが表示されます。 または、 **[表示]** メニューの **[プロパティウィンドウ]** をクリックすることもできます。
3. **SSL Enabled**を True に変更します。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. SSL URL をコピーします (他の SSL プロジェクトを作成していない場合は `https://localhost:44300/` になります)。
5. **ソリューションエクスプローラー**で、 **MvcAuth**プロジェクトを右クリックし、 **[プロパティ]** を選択します。
6. **[Web]** タブを選択し、 **[プロジェクト url]** ボックスに SSL url を貼り付けます。 ファイルを保存します (Ctl + S)。 Facebook と Google の認証アプリを構成するには、この URL が必要になります。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性を `Home` コントローラーに追加して、すべての要求で HTTPS を使用する必要があることを要求します。 より安全な方法は、 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)フィルターをアプリケーションに追加することです。 「SSL を使用してアプリケーションを保護する」および「&quot;の承認」のセクション「 [auth と SQL DB を使用した ASP.NET MVC アプリの作成」と「Azure App Service へのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」の&quot; を参照してください。 Home コントローラーの一部を次に示します。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 以前に証明書をインストールしたことがある場合は、このセクションの残りの部分をスキップし、 [OAuth 2 用の Google アプリの作成に進み、アプリをプロジェクトに接続](#goog)します。それ以外の場合は、指示に従って、IIS Express が生成した自己署名証明書を信頼します。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. **[セキュリティの警告]** ダイアログを読み、localhost を表す証明書をインストールする場合は [**はい]** をクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE は *ホーム* ページを表示し、SSL の警告はありません。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome は証明書も受け入れ、警告なしで HTTPS コンテンツを表示します。 Firefox は独自の証明書ストアを使用するため、警告が表示されます。 このアプリケーションでは **、[リスクを理解して**います] をクリックしても安全です。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>OAuth 2 用の Google アプリを作成し、そのアプリをプロジェクトに接続する

> [!WARNING]
> Google OAuth の現在の手順については、「 [ASP.NET Core での google 認証の構成](/aspnet/core/security/authentication/social/google-logins)」を参照してください。

1. [Google Developers Console](https://console.developers.google.com/)にアクセスします。
2. 前にプロジェクトを作成していない場合は、左のタブで **[資格情報]** を選択し、 **[作成]** を選択します。
3. 左側のタブで、 **[資格情報]** をクリックします。
4. **[資格情報の作成]** 、 **[OAuth クライアント ID]** の順にクリックします。 

    1. **[クライアント ID の作成]** ダイアログボックスで、アプリケーションの種類の既定の**Web アプリケーション**をそのまま使用します。
    2. 承認された**JavaScript**オリジンを、上で使用した ssl URL (他の ssl プロジェクトを作成していない場合は`https://localhost:44300/`) に設定します。
    3. 承認された**リダイレクト URI**を次のように設定します。  
         `https://localhost:44300/signin-google`
5. [OAuth 同意画面] メニュー項目をクリックし、電子メールアドレスと製品名を設定します。 フォームが完了したら、 **[保存]** をクリックします。
6. [ライブラリ] メニュー項目をクリックし、 **Google + API**を検索して、[有効にする] をクリックします。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   次の画像は、有効になっている Api を示しています。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Google Api の API マネージャーで、 **[資格情報]** タブを開いて**クライアント ID**を取得します。 アプリケーションシークレットを使用して JSON ファイルを保存するには、をダウンロードします。 **ClientId**と**clientsecret**をコピーし、 *App_Start*フォルダーの*Startup.Auth.cs*ファイルにある `UseGoogleAuthentication` メソッドに貼り付けます。 次に示す**ClientId**と**clientsecret**の値はサンプルであり、動作しません。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > セキュリティ-機密データをソースコードに格納しません。 このサンプルを単純にするために、アカウントと資格情報が上記のコードに追加されています。 [ASP.NET と Azure App Service にパスワードやその他の機密データをデプロイするためのベストプラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)を参照してください。
8. **Ctrl キーを押しながら F5 キーを押して** アプリケーションをビルドし、実行します。 **[Log in]** リンクをクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. **[別のサービスを使用してログインする]** で、 **[Google]** をクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 上記のいずれかの手順を実行しないと、HTTP 401 エラーが発生します。 上記の手順を再確認してください。 必要な設定 (**製品名**など) を忘れた場合は、不足している項目を追加して保存します。認証が機能するまでに数分かかることがあります。
10. 資格情報を入力する Google サイトにリダイレクトされます。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 資格情報を入力すると、先ほど作成した web アプリケーションにアクセス許可を付与するように求められます。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. **[Accept]\(受け入れる\)** をクリックします。 これで、MvcAuth アプリケーションの**登録**ページにリダイレクトされ、Google アカウントを登録できるようになります。 Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。 **[登録]** をクリックします。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Facebook でアプリを作成し、アプリをプロジェクトに接続する

> [!WARNING]
> Facebook OAuth2 の現在の認証手順については、「 [facebook 認証の構成](/aspnet/core/security/authentication/social/facebook-logins)」を参照してください。

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>メンバーシップデータを確認する

**[表示]** メニューの **[サーバーエクスプローラー]** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

**Defaultconnection (MvcAuth)** を展開し、 **[テーブル]** を展開して、 **[AspNetUsers]** を右クリックし、 **[テーブルデータの表示]** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers テーブルデータ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>ユーザークラスへのプロファイルデータの追加

このセクションでは、次の図に示すように、登録時にユーザーデータに生年月日と自宅の町を追加します。

![自宅の町と Bday を使用した reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

*Models\IdentityModels.cs*ファイルを開き、生年月日と自宅のプロパティを追加します。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

*Models\AccountViewModels.cs*ファイルを開き、`ExternalLoginConfirmationViewModel`で [誕生日と自宅の住所] プロパティを設定します。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

次に示すように、*コントローラー*ファイルを開き、`ExternalLoginConfirmation` アクションメソッドに生年月日と自宅の郵便番号を追加します。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

*Views\Account\ExternalLoginConfirmation.cshtml*ファイルに生年月日と自宅の町を追加します。

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

もう一度 Facebook アカウントをアプリケーションに登録できるように、メンバーシップデータベースを削除し、新しい生年月日と自宅のプロファイル情報を追加できることを確認します。

**ソリューションエクスプローラー**で、**すべてのファイルを表示** アイコンをクリックし、*追加\_Data\aspnet-MvcAuth-&lt;datestamp&gt;* を右クリックして、**削除** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

**[ツール]** メニューの **[NuGet パッケージ]** マネージャー をクリックし、 **[パッケージマネージャーコンソール]** (PMC) をクリックします。 PMC に次のコマンドを入力します。

1. 移行を有効にする
2. 追加-移行の初期化
3. Update-Database

アプリケーションを実行し、FaceBook と Google を使用してログインし、一部のユーザーを登録します。

## <a name="examine-the-membership-data"></a>メンバーシップデータを確認する

**[表示]** メニューの **[サーバーエクスプローラー]** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

**AspNetUsers**を右クリックし、 **[テーブルデータの表示]** をクリックします。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

`HomeTown` フィールドと `BirthDate` フィールドを次に示します。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>アプリをログオフし、別のアカウントでログインする

Facebook のを使用してアプリにログオンしてからログアウトし、別の Facebook アカウント (同じブラウザーを使用) でもう一度ログインすると、使用した前の Facebook アカウントにすぐにログインします。 別のアカウントを使用するには、facebook に移動し、Facebook でログアウトする必要があります。 他のサードパーティの認証プロバイダーにも同じ規則が適用されます。 または、別のブラウザーを使用して別のアカウントでログインすることもできます。

## <a name="next-steps"></a>次の手順

Yahoo と LinkedIn の手順については、「OWIN by Jerrie Pelser [for The yahoo And Linkedin OAuth security providers for](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) 」を参照してください。 ソーシャルログインボタンを有効にする方法については、Jerrie の「ASP.NET MVC 5 の非常にソーシャルログインボタン」を参照してください。

チュートリアル「 [auth と SQL DB を使用して ASP.NET MVC アプリを作成し、Azure App Service にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)する」に従って、このチュートリアルを続行し、次の内容を示します。

1. アプリを Azure にデプロイする方法。
2. ロールを使用してアプリをセキュリティで保護する方法。
3. [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)および[承認](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)フィルターを使用してアプリをセキュリティで保護する方法。
4. メンバーシップ API を使用してユーザーとロールを追加する方法。

このチュートリアルの気に入った点と改善点についてのフィードバックをお寄せください。 「[コードの使用方法を表示](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)する」で新しいトピックを要求することもできます。 ASP.NET に追加する新機能について質問したり、投票したりすることもできます。 たとえば、[ユーザーとロールを作成して管理](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)するためのツールに投票することができます。

ASP.NET 外部認証サービスのしくみの詳細については、「Robert McMurray の[外部認証サービス](https://asp.net/web-api/overview/security/external-authentication-services)」を参照してください。 また、Robert の記事では、Microsoft と Twitter の認証を有効にする方法についても詳しく説明します。 Tom Dykstra の優れた[EF/MVC チュートリアル](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、Entity Framework の操作方法について説明します。
