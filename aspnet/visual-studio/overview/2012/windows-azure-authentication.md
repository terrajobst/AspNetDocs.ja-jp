---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure 認証 |Microsoft Docs
author: Rick-Anderson
description: Windows Azure Active Directory 用の Microsoft ASP.NET ツールを使用すると、Windows Azure Web サイトでホストされている web アプリケーションの認証を簡単に有効にできます...
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: 41c4e6d02c965c10aa35b882964f4f04d9b8c44b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075152"
---
# <a name="windows-azure-authentication"></a>Windows Azure 認証

[Rick Anderson]((https://twitter.com/RickAndMSFT))

> Windows Azure Active Directory 用の Microsoft ASP.NET ツールを使用すると、 [Windows Azure Web サイト](https://www.windowsazure.com/home/features/web-sites/)でホストされている web アプリケーションの認証を簡単に有効にすることができます。 Windows Azure 認証を使用すると、社内 Active Directory、または独自のカスタム Windows Azure Active Directory ドメインで作成されたユーザーとの間で企業アカウントを使用して、Office 365 ユーザーを認証できます。 Windows Azure 認証を有効にすると、1つの[windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)テナントを使用してユーザーを認証するようにアプリケーションが構成されます。
>
> ASP.NET Windows Azure 認証ツールは、クラウドサービスの web ロールではサポートされていませんが、今後のリリースではこれを予定しています。 Windows [Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) は、windows Azure の web ロールでサポートされています。
>
> オンプレミスの Active Directory と Windows Azure Active Directory テナントの間の同期をセットアップする方法の詳細については、「 [AD FS 2.0 を使用してシングルサインオンを実装および管理する」を](https://technet.microsoft.com/library/jj205462.aspx)参照してください。
>
> 現在、Windows Azure Active Directory は無料の[プレビューサービス](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)として提供されています。

## <a name="requirements"></a>要件:

- Visual Studio 2012 または[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- [Visual Studio 2012 用 Web ツール拡張](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)機能または[Visual Studio Express 2012 用 web ツール拡張](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)機能
- [Windows Azure Active Directory 用 Microsoft ASP.NET ツール-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)または[Microsoft ASP.NET tools for windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>Visual Studio 2012 で ASP.NET Web アプリケーションを作成する

このチュートリアルでは、Visual Studio 2012 を使用して任意の Web アプリケーションを作成できます。このチュートリアルでは、ASP.NET MVC イントラネットテンプレートを使用します。

1. 新しい ASP.NET MVC 4 イントラネットアプリケーションを作成し、すべての既定値をそのまま使用します。 (これは、 **ter** Net プロジェクトではなく、 **Tra** net のである必要があります)。
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>Windows Azure 認証を有効にする (原則のグローバル管理者である場合)

既存の Windows Azure Active Directory テナント (たとえば、既存の Office 365 アカウントを使用) がない場合は、[新しい windows Azure Active Directory アカウント](https://g.microsoftonline.com/0AX00en/5)にサインアップすることで新しいテナントを作成できます。

1. プロジェクト メニューの  **Windows Azure 認証を有効にする** を選択します。

   ![](windows-azure-authentication/_static/image2.png)

2. Windows Azure Active Directory テナントのドメイン (たとえば、contoso.onmicrosoft.com) を入力し、 **[有効にする]** をクリックします。

![](windows-azure-authentication/_static/image3.png)

3. [Web 認証] ダイアログで、Windows Azure Active Directory テナントの管理者としてサインインします。

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>管理者以外の方法で Windows Azure を有効にする

Windows Azure Active Directory テナントのグローバル管理者特権を持っていない場合は、アプリケーションをプロビジョニングするためのチェックボックスをオフにすることができます。

![](windows-azure-authentication/_static/image6.png)

このダイアログには、Azure Active Directory の理念でアプリケーションをプロビジョニングするために必要な**ドメイン**、**アプリケーションプリンシパル Id** 、および**応答 URL**が表示されます。 この情報は、アプリケーションをプロビジョニングするための十分な特権を持つユーザーに提供する必要があります。 コマンドレットを使用してサービスプリンシパルを手動で作成する方法の詳細については、「[Windows Azure Active Directory ASP.NET アプリケーションでシングルサインオンを実装する方法](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)」を参照してください。
アプリケーションが正常にプロビジョニングされたら、[続行] をクリックして **、選択した設定で web.config を更新**できます。 プロビジョニングが行われるのを待機している間にアプリケーションの開発を続行する場合は、[閉じる] をクリックし**て、プロジェクトファイルの設定を記憶**することができます。 次に Windows Azure 認証を有効にする をクリックし、プロビジョニング チェックボックスをオフにすると、同じ設定が表示されます。 **続行** をクリックし、次へ をクリックして、**これらの設定を web.config に適用**します。

1. アプリケーションが Windows Azure 認証用に構成されていて、Windows Azure Active Directory でプロビジョニングされている間、しばらくお待ちください。
2. アプリケーションに対して Windows Azure 認証が有効になったら、[閉じる] をクリックし**ます。**

    ![](windows-azure-authentication/_static/image7.png)
3. F5 キーを押してアプリケーションを実行します。 ログインページに自動的にリダイレクトされます。 アプリケーションにログインするには、ディレクトリの理念ユーザー資格情報を使用します。

    ![](windows-azure-authentication/_static/image1.jpg)
4. アプリケーションが現在自己署名テスト証明書を使用しているため、信頼された証明機関によって証明書が発行されていないという警告がブラウザーに表示されます。

    この警告は、ローカル開発時に **[このサイトの続行]** をクリックすると、無視してかまいません。

    ![](windows-azure-authentication/_static/image8.png)
5. これで、Windows Azure 認証を使用してアプリケーションに正常にログインできました。

    ![](windows-azure-authentication/_static/image2.jpg)

Windows Azure 認証を有効にすると、アプリケーションに次の変更が加えられます。

- クロスサイト要求偽造 ([Csrf](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) クラス ( *App\_Start\AntiXsrfConfig.cs* ) がプロジェクトに追加されます。
- `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` NuGet パッケージがプロジェクトに追加されます。
- アプリケーションの windows Identity Foundation の設定は、Windows Azure Active Directory テナントからのセキュリティトークンを受け入れるように構成されます。 次の画像をクリックする*と、web.config ファイルに*加えられた変更の展開されたビューが表示されます。

     ![](windows-azure-authentication/_static/image9.png)
- Windows Azure Active Directory テナント内のアプリケーションのサービスプリンシパルがプロビジョニングされます。
- HTTPS が有効になっています。

## <a name="deploy-the-application-to-windows-azure"></a>Windows Azure にアプリケーションをデプロイする

詳細な手順については、「 [Windows Azure Web サイトへの ASP.NET Web アプリケーションのデプロイ](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」を参照してください。

Windows Azure 認証を使用してアプリケーションを Azure の Web サイトに発行するには、次のようにします。

1. アプリケーションを右クリックし、[発行] を選択し**ます。**

    ![](windows-azure-authentication/_static/image3.jpg)
2. [Web の発行] ダイアログで、Azure の Web サイトの発行プロファイルをダウンロードしてインポートします。

    ![](windows-azure-authentication/_static/image4.jpg)
3. **[接続]** タブには、**送信先 url** (アプリケーションの公開 url) が表示されます。 **[接続の検証]** をクリックして接続をテストします。

    ![](windows-azure-authentication/_static/image5.jpg)
4. この Azure Web サイトに発行したことがある場合は、アプリケーションが正常に公開されるように、[**ターゲットで追加ファイルを削除**する] 設定をオンにすることを検討してください。 **[Windows Azure 認証を有効にする]** チェックボックスがオンになっていることに注意してください。

    ![](windows-azure-authentication/_static/image10.png)
5. 省略可能: **[プレビュー]** タブで、 **[プレビューの開始]** をクリックして、展開されたファイルを確認します。

    ![](windows-azure-authentication/_static/image6.jpg)
6. [**発行] をクリックします。**

    ターゲットホストに対して Windows Azure 認証を有効にするように求められます。 **[有効]** をクリックして続行します。

    ![](windows-azure-authentication/_static/image11.png)
7. Windows Azure Active Directory テナントの管理者の資格情報を入力してください:

    ![](windows-azure-authentication/_static/image7.jpg)
8. アプリケーションが正常に発行されると、公開された web サイトでブラウザーが開きます。

    > [!NOTE]
    > ターゲットホストに対して Windows Azure 認証を有効にした後、アプリケーションが Windows Azure Active Directory で完全にプロビジョニングされるまでに、最大5分かかる場合があります。 エラー ACS50001 を受信したときに初めてアプリケーションを実行したとき: ' [realm] ' という名前の証明書利用者が見つかりませんでした。数分待ってから、アプリケーションをもう一度実行してください。
9. プロンプトが表示されたら、ディレクトリにユーザーとしてログインします。

    ![](windows-azure-authentication/_static/image8.jpg)
10. これで、Windows Azure 認証を使用して Azure ホステッドアプリケーションに正常にログインできました。

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>既知の問題

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>Windows Azure 認証を使用すると、ロールベースの承認に失敗する

現在、Windows Azure 認証では、ロールベースの承認を実行するために必要なロール要求が提供されていません。 認証されたユーザーのロールは、Windows Azure Active Directory から手動で取得する必要があります。

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>Windows Azure 認証を使用してアプリケーションを参照すると、"ログインしているユーザーのドメイン (live.com) は、この STS の許可されているドメインと一致しません" というエラーが表示されます。

Microsoft アカウント (hotmail.com、live.com、outlook.com など) に既にログインしていて、Windows Azure 認証が有効になっているアプリケーションにアクセスしようとすると、Microsoft アカウントのドメインが原因で400エラー応答が表示されることがあります。Windows Azure Active Directory では認識されません。 アプリケーションにログインするには、最初に Microsoft アカウントからログアウトします。

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>Windows Azure 認証が有効になっているアプリケーションにログインし、[なし] 以外の X509certificatevalidationmode.custom を使用すると、accounts.accesscontrol.windows.net 証明書の証明書検証エラーが発生します。

証明書の検証は必須ではないため、無効のままにしておく必要があります。 発行者証明書の拇印は、WSFederationAuthenticationModule によって検証されます。

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>Windows Azure 認証を有効にしようとすると、[Web 認証] ダイアログに "ACS20016: ログインしているユーザーのドメイン (contoso.onmicrosoft.com) は、この STS で許可されているドメインと一致しません。" というエラーが表示されます。

同じ Visual Studio プロセス内から別の Windows Azure Active Directory アカウントを使用して正常にログインした場合に、このエラーが表示されることがあります。 指定されたアカウントからログアウトするか、Visual Studio を再起動します。 以前にログインして [サインインしたままにする] オプションを選択した場合は、ブラウザーの cookie をクリアする必要がある場合があります。

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012: 要求が有効な WS-FEDERATION プロトコルメッセージではありません

これは、Azure サービスのいずれかに既に他の Microsoft ID でログインしている場合に発生する可能性があります。 IE の InPrivate や Chrome の Incognito などのプライベートブラウザーウィンドウを使用するか、すべての cookie をクリアします。

## <a name="additional-resources"></a>その他のリソース

- [Windows Azure Active Directory 用の Microsoft ASP.NET ツール-Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio/cci
- [Windows Azure の機能: Id](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory: 組織向けのアプリを開発する](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory: 複数の組織向けのアプリを開発する](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [Windows Azure Active Directory でシングルサインオンを実装する方法](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Windows Azure Active Directory でのシングルサインオン: 詳細については、](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) Vittorio/cci
- [AD FS 2.0 を使用してシングルサインオンを実装および管理する](https://technet.microsoft.com/library/jj205462.aspx)
