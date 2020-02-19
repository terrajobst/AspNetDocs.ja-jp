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
ms.openlocfilehash: ce98effe18dd739504fb0d5453bae8a46c3ba102
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457480"
---
# <a name="windows-azure-authentication"></a><span data-ttu-id="21def-103">Windows Azure 認証</span><span class="sxs-lookup"><span data-stu-id="21def-103">Windows Azure Authentication</span></span>

<span data-ttu-id="21def-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="21def-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="21def-105">Windows Azure Active Directory 用の Microsoft ASP.NET ツールを使用すると、 [Windows Azure Web サイト](https://www.windowsazure.com/home/features/web-sites/)でホストされている web アプリケーションの認証を簡単に有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="21def-105">Microsoft ASP.NET tools for Windows Azure Active Directory makes it simple to enable authentication for web applications hosted on [Windows Azure Web Sites](https://www.windowsazure.com/home/features/web-sites/).</span></span> <span data-ttu-id="21def-106">Windows Azure 認証を使用すると、社内 Active Directory、または独自のカスタム Windows Azure Active Directory ドメインで作成されたユーザーとの間で企業アカウントを使用して、Office 365 ユーザーを認証できます。</span><span class="sxs-lookup"><span data-stu-id="21def-106">You can use Windows Azure Authentication to authenticate Office 365 users from your organization, corporate accounts synced from your on-premise Active Directory or users created in your own custom Windows Azure Active Directory domain.</span></span> <span data-ttu-id="21def-107">Windows Azure 認証を有効にすると、1つの[windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)テナントを使用してユーザーを認証するようにアプリケーションが構成されます。</span><span class="sxs-lookup"><span data-stu-id="21def-107">Enabling Windows Azure Authentication configures your application to authenticate users using a single [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) tenant.</span></span>
>
> <span data-ttu-id="21def-108">ASP.NET Windows Azure 認証ツールは、クラウドサービスの web ロールではサポートされていませんが、今後のリリースではこれを予定しています。</span><span class="sxs-lookup"><span data-stu-id="21def-108">The ASP.NET Windows Azure Authentication tool is not supported for web roles in a cloud service but we plan to do so in a future release.</span></span> <span data-ttu-id="21def-109">Windows [Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) は、windows Azure の web ロールでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="21def-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) is supported in Windows Azure web roles.</span></span>
>
> <span data-ttu-id="21def-110">オンプレミスの Active Directory と Windows Azure Active Directory テナントの間の同期をセットアップする方法の詳細については、「 [AD FS 2.0 を使用してシングルサインオンを実装および管理する」を](https://technet.microsoft.com/library/jj205462.aspx)参照してください。</span><span class="sxs-lookup"><span data-stu-id="21def-110">For details on how to setup synchronization between your on-premise Active Directory and your Windows Azure Active Directory tenant please see [Use AD FS 2.0 to implement and manage single sign-on](https://technet.microsoft.com/library/jj205462.aspx).</span></span>
>
> <span data-ttu-id="21def-111">現在、Windows Azure Active Directory は無料の[プレビューサービス](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)として提供されています。</span><span class="sxs-lookup"><span data-stu-id="21def-111">Windows Azure Active Directory is currently available as a [free preview service](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

## <a name="requirements"></a><span data-ttu-id="21def-112">要件:</span><span class="sxs-lookup"><span data-stu-id="21def-112">Requirements:</span></span>

- <span data-ttu-id="21def-113">Visual Studio 2012 または[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span><span class="sxs-lookup"><span data-stu-id="21def-113">Visual Studio 2012 or [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span></span>
- <span data-ttu-id="21def-114">[Visual Studio 2012 用 Web ツール拡張](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)機能または[Visual Studio Express 2012 用 web ツール拡張](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)機能</span><span class="sxs-lookup"><span data-stu-id="21def-114">[Web Tools Extensions for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) or [Web Tools Extensions for Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span></span>
- <span data-ttu-id="21def-115">[Windows Azure Active Directory 用 Microsoft ASP.NET ツール-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)または[Microsoft ASP.NET tools for windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span><span class="sxs-lookup"><span data-stu-id="21def-115">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) or [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span></span>

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a><span data-ttu-id="21def-116">Visual Studio 2012 で ASP.NET Web アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="21def-116">Create an ASP.NET Web Application with Visual Studio 2012</span></span>

<span data-ttu-id="21def-117">このチュートリアルでは、Visual Studio 2012 を使用して任意の Web アプリケーションを作成できます。このチュートリアルでは、ASP.NET MVC イントラネットテンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="21def-117">You can create any Web Application with Visual Studio 2012, this tutorial uses the ASP.NET MVC intranet template.</span></span>

1. <span data-ttu-id="21def-118">新しい ASP.NET MVC 4 イントラネットアプリケーションを作成し、すべての既定値をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="21def-118">Create a new ASP.NET MVC 4 Intranet Application and accept all the defaults.</span></span> <span data-ttu-id="21def-119">(これは、 **ter** Net プロジェクトではなく、 **Tra** net のである必要があります)。</span><span class="sxs-lookup"><span data-stu-id="21def-119">(It must be an In **tra** net and not In **ter** net project).</span></span>
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a><span data-ttu-id="21def-120">Windows Azure 認証を有効にする (原則のグローバル管理者である場合)</span><span class="sxs-lookup"><span data-stu-id="21def-120">Enable Window Azure Authentication (When you are a Global Administrator of the Tenet)</span></span>

<span data-ttu-id="21def-121">既存の Windows Azure Active Directory テナント (たとえば、既存の Office 365 アカウントを使用) がない場合は、[新しい windows Azure Active Directory アカウント](https://g.microsoftonline.com/0AX00en/5)にサインアップすることで新しいテナントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="21def-121">If you do not have an existing Windows Azure Active Directory tenant (For example, through an existing Office 365 account) you can create a new tenant by signing up for a [new Windows Azure Active Directory account](https://g.microsoftonline.com/0AX00en/5).</span></span>

1. <span data-ttu-id="21def-122">プロジェクト メニューの  **Windows Azure 認証を有効にする** を選択します。</span><span class="sxs-lookup"><span data-stu-id="21def-122">From the Project menu select **Enable Windows Azure Authentication**:</span></span>

   ![](windows-azure-authentication/_static/image2.png)

2. <span data-ttu-id="21def-123">Windows Azure Active Directory テナントのドメイン (たとえば、contoso.onmicrosoft.com) を入力し、 **[有効にする]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="21def-123">Enter the domain for your Windows Azure Active Directory tenant (for example, contoso.onmicrosoft.com) and click **Enable**:</span></span>

![](windows-azure-authentication/_static/image3.png)

3. <span data-ttu-id="21def-124">[Web 認証] ダイアログで、Windows Azure Active Directory テナントの管理者としてサインインします。</span><span class="sxs-lookup"><span data-stu-id="21def-124">In the Web Authentication dialog sign in as an administrator for your Windows Azure Active Directory tenant:</span></span>

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a><span data-ttu-id="21def-125">管理者以外の方法で Windows Azure を有効にする</span><span class="sxs-lookup"><span data-stu-id="21def-125">Enable Window Azure by a non-administrator of the Tenet</span></span>

<span data-ttu-id="21def-126">Windows Azure Active Directory テナントのグローバル管理者特権を持っていない場合は、アプリケーションをプロビジョニングするためのチェックボックスをオフにすることができます。</span><span class="sxs-lookup"><span data-stu-id="21def-126">If you do not have Global Administrator privilege for your Windows Azure Active Directory tenant, you can uncheck the checkbox for provisioning the application.</span></span>

![](windows-azure-authentication/_static/image6.png)

<span data-ttu-id="21def-127">このダイアログには、Azure Active Directory の理念でアプリケーションをプロビジョニングするために必要な**ドメイン**、**アプリケーションプリンシパル Id** 、および**応答 URL**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="21def-127">The dialog will display the **Domain**, **Application Principal Id** and **Reply URL** which are required for provisioning the application with an Azure Active Directory tenet.</span></span> <span data-ttu-id="21def-128">この情報は、アプリケーションをプロビジョニングするための十分な特権を持つユーザーに提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="21def-128">You need to give this information to someone who has sufficient privilege to provision the application.</span></span> <span data-ttu-id="21def-129">コマンドレットを使用してサービスプリンシパルを手動で作成する方法の詳細については、「[Windows Azure Active Directory ASP.NET アプリケーションでシングルサインオンを実装する方法](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="21def-129">See[How to implement single sign-on with Windows Azure Active Directory - ASP.NET Application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) for details on how to use cmdlet to create the service principal manually.</span></span>
<span data-ttu-id="21def-130">アプリケーションが正常にプロビジョニングされたら、[続行] をクリックして **、選択した設定で web.config を更新**できます。</span><span class="sxs-lookup"><span data-stu-id="21def-130">Once the application has been successfully provisioned, you can click on **Continue to update web.config with the selected settings**.</span></span> <span data-ttu-id="21def-131">プロビジョニングが行われるのを待機している間にアプリケーションの開発を続行する場合は、[閉じる] をクリックし**て、プロジェクトファイルの設定を記憶**することができます。</span><span class="sxs-lookup"><span data-stu-id="21def-131">If you want to continue developing the application while waiting for provisioning to happen, you can click **Close to remember the settings in project file**.</span></span> <span data-ttu-id="21def-132">次に Windows Azure 認証を有効にする をクリックし、プロビジョニング チェックボックスをオフにすると、同じ設定が表示されます。 **続行** をクリックし、次へ をクリックして、**これらの設定を web.config に適用**します。</span><span class="sxs-lookup"><span data-stu-id="21def-132">The next time you invoke Enable Windows Azure Authentication and uncheck the provisioning checkbox, you will see the same settings and you can click **Continue**, then click, **Apply these settings in web.config**.</span></span>

1. <span data-ttu-id="21def-133">アプリケーションが Windows Azure 認証用に構成されていて、Windows Azure Active Directory でプロビジョニングされている間、しばらくお待ちください。</span><span class="sxs-lookup"><span data-stu-id="21def-133">Wait while your application is configured for Windows Azure Authentication and provisioned with Windows Azure Active Directory.</span></span>
2. <span data-ttu-id="21def-134">アプリケーションに対して Windows Azure 認証が有効になったら、[閉じる] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="21def-134">Once Windows Azure Authentication has been enabled for your application, click **Close:**</span></span>

    ![](windows-azure-authentication/_static/image7.png)
3. <span data-ttu-id="21def-135">F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="21def-135">Hit F5 to run your application.</span></span> <span data-ttu-id="21def-136">ログインページに自動的にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="21def-136">You should automatically get redirected to login page.</span></span> <span data-ttu-id="21def-137">アプリケーションにログインするには、ディレクトリの理念ユーザー資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="21def-137">Use the directory tenet user credentials to login to the application..</span></span>

    ![](windows-azure-authentication/_static/image1.jpg)
4. <span data-ttu-id="21def-138">アプリケーションが現在自己署名テスト証明書を使用しているため、信頼された証明機関によって証明書が発行されていないという警告がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="21def-138">Because your application is currently using a self-signed test certificate you will receive a warning from the browser that the certificate was not issued by a trusted certificate authority.</span></span>

    <span data-ttu-id="21def-139">この警告は、ローカル開発時に **[このサイトの続行]** をクリックすると、無視してかまいません。</span><span class="sxs-lookup"><span data-stu-id="21def-139">This warning can be safely ignored during local development by clicking **Continue to this website:**</span></span>

    ![](windows-azure-authentication/_static/image8.png)
5. <span data-ttu-id="21def-140">これで、Windows Azure 認証を使用してアプリケーションに正常にログインできました。</span><span class="sxs-lookup"><span data-stu-id="21def-140">You have now successfully logged in to your application using Windows Azure Authentication!</span></span>

    ![](windows-azure-authentication/_static/image2.jpg)

<span data-ttu-id="21def-141">Windows Azure 認証を有効にすると、アプリケーションに次の変更が加えられます。</span><span class="sxs-lookup"><span data-stu-id="21def-141">Enabling Windows Azure authentication makes the following changes to your application:</span></span>

- <span data-ttu-id="21def-142">クロスサイト要求偽造 ([Csrf](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) クラス ( *App\_Start\AntiXsrfConfig.cs* ) がプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="21def-142">An Anti-Cross-Site Request Forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) class ( *App\_Start\AntiXsrfConfig.cs* ) is added to your project.</span></span>
- <span data-ttu-id="21def-143">`System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` NuGet パッケージがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="21def-143">The NuGet packages `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` is added to your project.</span></span>
- <span data-ttu-id="21def-144">アプリケーションの windows Identity Foundation の設定は、Windows Azure Active Directory テナントからのセキュリティトークンを受け入れるように構成されます。</span><span class="sxs-lookup"><span data-stu-id="21def-144">Windows Identity Foundation settings in your application will be configured to accept security tokens from your Windows Azure Active Directory tenant.</span></span> <span data-ttu-id="21def-145">次の画像をクリックする*と、web.config ファイルに*加えられた変更の展開されたビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="21def-145">Click on the image below to see an expanded view of the changes made to the *Web.config* file.</span></span>

     ![](windows-azure-authentication/_static/image9.png)
- <span data-ttu-id="21def-146">Windows Azure Active Directory テナント内のアプリケーションのサービスプリンシパルがプロビジョニングされます。</span><span class="sxs-lookup"><span data-stu-id="21def-146">A service principal for your application in your Windows Azure Active Directory tenant will be provisioned.</span></span>
- <span data-ttu-id="21def-147">HTTPS が有効になっています。</span><span class="sxs-lookup"><span data-stu-id="21def-147">HTTPS is enabled.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="21def-148">Windows Azure にアプリケーションをデプロイする</span><span class="sxs-lookup"><span data-stu-id="21def-148">Deploy the application to Windows Azure</span></span>

<span data-ttu-id="21def-149">詳細な手順については、「 [Windows Azure Web サイトへの ASP.NET Web アプリケーションのデプロイ](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="21def-149">For complete instructions, see [Deploying an ASP.NET Web Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

<span data-ttu-id="21def-150">Windows Azure 認証を使用してアプリケーションを Azure の Web サイトに発行するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="21def-150">To publish an application using Windows Azure Authentication to an Azure Web Site:</span></span>

1. <span data-ttu-id="21def-151">アプリケーションを右クリックし、[発行] を選択し**ます。**</span><span class="sxs-lookup"><span data-stu-id="21def-151">Right click on your application and select **Publish:**</span></span>

    ![](windows-azure-authentication/_static/image3.jpg)
2. <span data-ttu-id="21def-152">[Web の発行] ダイアログで、Azure の Web サイトの発行プロファイルをダウンロードしてインポートします。</span><span class="sxs-lookup"><span data-stu-id="21def-152">From the Publish Web dialog download and import a publishing profile for your Azure Web Site.</span></span>

    ![](windows-azure-authentication/_static/image4.jpg)
3. <span data-ttu-id="21def-153">**[接続]** タブには、**送信先 url** (アプリケーションの公開 url) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="21def-153">The **Connection** tab shows the **Destination URL** (the public facing URL for your application).</span></span> <span data-ttu-id="21def-154">**[接続の検証]** をクリックして接続をテストします。</span><span class="sxs-lookup"><span data-stu-id="21def-154">Click **Validate Connection** to test your connection:</span></span>

    ![](windows-azure-authentication/_static/image5.jpg)
4. <span data-ttu-id="21def-155">この Azure Web サイトに発行したことがある場合は、アプリケーションが正常に公開されるように、[**ターゲットで追加ファイルを削除**する] 設定をオンにすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="21def-155">If you have published to this Azure Web Site previously consider checking the **Remove additional files at destination** setting to ensure your application publishes cleanly.</span></span> <span data-ttu-id="21def-156">**[Windows Azure 認証を有効にする]** チェックボックスがオンになっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="21def-156">Notice the **Enable Windows Azure Authentication** check box is selected.</span></span>

    ![](windows-azure-authentication/_static/image10.png)
5. <span data-ttu-id="21def-157">省略可能: **[プレビュー]** タブで、 **[プレビューの開始]** をクリックして、展開されたファイルを確認します。</span><span class="sxs-lookup"><span data-stu-id="21def-157">Optional: On the **Preview** tab click **Start Preview** to see the files deployed.</span></span>

    ![](windows-azure-authentication/_static/image6.jpg)
6. <span data-ttu-id="21def-158">[**発行] をクリックします。**</span><span class="sxs-lookup"><span data-stu-id="21def-158">Click **Publish.**</span></span>

    <span data-ttu-id="21def-159">ターゲットホストに対して Windows Azure 認証を有効にするように求められます。</span><span class="sxs-lookup"><span data-stu-id="21def-159">You will be prompted to enable Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="21def-160">**[有効]** をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="21def-160">Click **Enable** to continue:</span></span>

    ![](windows-azure-authentication/_static/image11.png)
7. <span data-ttu-id="21def-161">Windows Azure Active Directory テナントの管理者の資格情報を入力してください:</span><span class="sxs-lookup"><span data-stu-id="21def-161">Enter your administrator credentials for your Windows Azure Active Directory tenant:</span></span>

    ![](windows-azure-authentication/_static/image7.jpg)
8. <span data-ttu-id="21def-162">アプリケーションが正常に発行されると、公開された web サイトでブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="21def-162">Once your application has been successfully published, a browser will open to the published web site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="21def-163">ターゲットホストに対して Windows Azure 認証を有効にした後、アプリケーションが Windows Azure Active Directory で完全にプロビジョニングされるまでに、最大5分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="21def-163">It may take up to five minutes (typically must less) for your application to be fully provisioned with Windows Azure Active Directory after enabling Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="21def-164">エラー ACS50001 を受信したときに初めてアプリケーションを実行したとき: ' [realm] ' という名前の証明書利用者が見つかりませんでした。数分待ってから、アプリケーションをもう一度実行してください。</span><span class="sxs-lookup"><span data-stu-id="21def-164">When you first run your application if you receive error ACS50001: Relying party with name ‘[realm]' was not found, then wait a few minutes and try running the application again.</span></span>
9. <span data-ttu-id="21def-165">プロンプトが表示されたら、ディレクトリにユーザーとしてログインします。</span><span class="sxs-lookup"><span data-stu-id="21def-165">When prompted, log in as a user in your directory:</span></span>

    ![](windows-azure-authentication/_static/image8.jpg)
10. <span data-ttu-id="21def-166">これで、Windows Azure 認証を使用して Azure ホステッドアプリケーションに正常にログインできました。</span><span class="sxs-lookup"><span data-stu-id="21def-166">You have now successfully logged into your Azure hosted application using Windows Azure Authentication.</span></span>

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a><span data-ttu-id="21def-167">既知の問題</span><span class="sxs-lookup"><span data-stu-id="21def-167">Known Issues</span></span>

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a><span data-ttu-id="21def-168">Windows Azure 認証を使用すると、ロールベースの承認に失敗する</span><span class="sxs-lookup"><span data-stu-id="21def-168">Role-based authorization fails when using Windows Azure Authentication</span></span>

<span data-ttu-id="21def-169">現在、Windows Azure 認証では、ロールベースの承認を実行するために必要なロール要求が提供されていません。</span><span class="sxs-lookup"><span data-stu-id="21def-169">Windows Azure Authentication does not currently provide the necessary role claim so that role-based authorization can be performed.</span></span> <span data-ttu-id="21def-170">認証されたユーザーのロールは、Windows Azure Active Directory から手動で取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="21def-170">The role of the authenticated user must be manually retrieved from Windows Azure Active Directory.</span></span>

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="21def-171">Windows Azure 認証を使用してアプリケーションを参照すると、"ログインしているユーザーのドメイン (live.com) は、この STS の許可されているドメインと一致しません" というエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="21def-171">Browsing to an application with Windows Azure Authentication results in the error "ACS20016 The domain of the logged in user (live.com) does not match any allowed domain of this STS"</span></span>

<span data-ttu-id="21def-172">Microsoft アカウント (hotmail.com、live.com、outlook.com など) に既にログインしていて、Windows Azure 認証が有効になっているアプリケーションにアクセスしようとすると、Microsoft アカウントのドメインが原因で400エラー応答が表示されることがあります。Windows Azure Active Directory では認識されません。</span><span class="sxs-lookup"><span data-stu-id="21def-172">If you are already logged in to a Microsoft Account (for example hotmail.com, live.com, outlook.com) and you attempt to access an application that has enabled Windows Azure Authentication you may get a 400 error response because the domain of your Microsoft Account is not recognized by Windows Azure Active Directory.</span></span> <span data-ttu-id="21def-173">アプリケーションにログインするには、最初に Microsoft アカウントからログアウトします。</span><span class="sxs-lookup"><span data-stu-id="21def-173">To log into the application, log out from your Microsoft Account first.</span></span>

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a><span data-ttu-id="21def-174">Windows Azure 認証が有効になっているアプリケーションにログインし、[なし] 以外の X509certificatevalidationmode.custom を使用すると、accounts.accesscontrol.windows.net 証明書の証明書検証エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="21def-174">Logging into an application with Windows Azure Authentication enabled and a X509CertificateValidationMode other than None results in certificate validation errors for the accounts.accesscontrol.windows.net certificate</span></span>

<span data-ttu-id="21def-175">証明書の検証は必須ではないため、無効のままにしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="21def-175">Certificate validation is not required and should be left disabled.</span></span> <span data-ttu-id="21def-176">発行者証明書の拇印は、WSFederationAuthenticationModule によって検証されます。</span><span class="sxs-lookup"><span data-stu-id="21def-176">The thumbprint of the issuer certificate is validated by the WSFederationAuthenticationModule.</span></span>

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="21def-177">Windows Azure 認証を有効にしようとすると、[Web 認証] ダイアログに "ACS20016: ログインしているユーザーのドメイン (contoso.onmicrosoft.com) は、この STS で許可されているドメインと一致しません。" というエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="21def-177">When attempting to enable Windows Azure Authentication the Web Authentication dialog shows the error "ACS20016: The domain of the logged in user (contoso.onmicrosoft.com) does not match any allowed domain of this STS."</span></span>

<span data-ttu-id="21def-178">同じ Visual Studio プロセス内から別の Windows Azure Active Directory アカウントを使用して正常にログインした場合に、このエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="21def-178">You may see this error when you have previously successfully logged in using a different Windows Azure Active Directory account from within the same Visual Studio process.</span></span> <span data-ttu-id="21def-179">指定されたアカウントからログアウトするか、Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="21def-179">Log out from the specified account or restart Visual Studio.</span></span> <span data-ttu-id="21def-180">以前にログインして [サインインしたままにする] オプションを選択した場合は、ブラウザーの cookie をクリアする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="21def-180">If you previously logged in and selected the option to "Keep me signed in" then you may need to clear your browser cookies.</span></span>

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a><span data-ttu-id="21def-181">ACS20012: 要求が有効な WS-FEDERATION プロトコルメッセージではありません</span><span class="sxs-lookup"><span data-stu-id="21def-181">ACS20012: The request is not a valid WS-Federation protocol message</span></span>

<span data-ttu-id="21def-182">これは、Azure サービスのいずれかに既に他の Microsoft ID でログインしている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="21def-182">This can happen if you are already logged in with some other Microsoft ID to one of the Azure services.</span></span> <span data-ttu-id="21def-183">IE の InPrivate や Chrome の Incognito などのプライベートブラウザーウィンドウを使用するか、すべての cookie をクリアします。</span><span class="sxs-lookup"><span data-stu-id="21def-183">Use Private browser window like InPrivate in IE or Incognito in Chrome or clear all the cookies.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21def-184">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="21def-184">Additional Resources</span></span>

- <span data-ttu-id="21def-185">[Windows Azure Active Directory 用の Microsoft ASP.NET ツール-Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio/cci</span><span class="sxs-lookup"><span data-stu-id="21def-185">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="21def-186">Windows Azure の機能: Id</span><span class="sxs-lookup"><span data-stu-id="21def-186">Windows Azure Features: Identity</span></span>](https://docs.microsoft.com/azure/active-directory/)
- [<span data-ttu-id="21def-187">TechNet: Windows Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21def-187">TechNet: Windows Azure Active Directory</span></span>](https://technet.microsoft.com/library/hh967619.aspx)
- [<span data-ttu-id="21def-188">Windows Azure Active Directory: 組織向けのアプリを開発する</span><span class="sxs-lookup"><span data-stu-id="21def-188">Windows Azure Active Directory: Develop Apps for your organization</span></span>](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [<span data-ttu-id="21def-189">Windows Azure Active Directory: 複数の組織向けのアプリを開発する</span><span class="sxs-lookup"><span data-stu-id="21def-189">Windows Azure Active Directory: Develop Apps for multiple organizations</span></span>](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [<span data-ttu-id="21def-190">Windows Azure Active Directory でシングルサインオンを実装する方法</span><span class="sxs-lookup"><span data-stu-id="21def-190">How to implement single sign-on with Windows Azure Active Directory</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- <span data-ttu-id="21def-191">[Windows Azure Active Directory でのシングルサインオン: 詳細については、](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) Vittorio/cci</span><span class="sxs-lookup"><span data-stu-id="21def-191">[Single Sign-On with Windows Azure Active Directory: a Deep Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="21def-192">AD FS 2.0 を使用してシングルサインオンを実装および管理する</span><span class="sxs-lookup"><span data-stu-id="21def-192">Use AD FS 2.0 to implement and manage single sign-on</span></span>](https://technet.microsoft.com/library/jj205462.aspx)
