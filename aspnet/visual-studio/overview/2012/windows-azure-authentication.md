---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure Authentication |Microsoft Docs
author: Rick-Anderson
description: Windows Azure Active Directory 用の Microsoft ASP.NET ツールをシンプルな Windows Azure Web サイトでホストされている web アプリケーションの認証を有効にしています.
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: cd3eed8c14103d29a66acd475fafe5ff3122a960
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421584"
---
# <a name="windows-azure-authentication"></a><span data-ttu-id="1bd3e-103">Windows Azure 認証</span><span class="sxs-lookup"><span data-stu-id="1bd3e-103">Windows Azure Authentication</span></span>

<span data-ttu-id="1bd3e-104">によって[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="1bd3e-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="1bd3e-105">Windows Azure Active Directory でホストされている web アプリケーションの認証を有効にする単純な用のツールは Microsoft ASP.NET [Windows Azure Websites](https://www.windowsazure.com/home/features/web-sites/)します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-105">Microsoft ASP.NET tools for Windows Azure Active Directory makes it simple to enable authentication for web applications hosted on [Windows Azure Web Sites](https://www.windowsazure.com/home/features/web-sites/).</span></span> <span data-ttu-id="1bd3e-106">Windows Azure の認証を使用して、組織、オンプレミスの Active Directory から同期された会社のアカウントまたはカスタムの Windows Azure Active Directory ドメインで作成されたユーザーから Office 365 ユーザーを認証することができます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-106">You can use Windows Azure Authentication to authenticate Office 365 users from your organization, corporate accounts synced from your on-premise Active Directory or users created in your own custom Windows Azure Active Directory domain.</span></span> <span data-ttu-id="1bd3e-107">Windows Azure Authentication を有効にすると、1 つを使用してユーザーを認証するアプリケーションを構成します[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)テナント。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-107">Enabling Windows Azure Authentication configures your application to authenticate users using a single [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) tenant.</span></span>
>
> <span data-ttu-id="1bd3e-108">クラウド サービスの web ロール ASP.NET Windows Azure Authentication ツールがサポートされていませんが、将来のリリースで予定します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-108">The ASP.NET Windows Azure Authentication tool is not supported for web roles in a cloud service but we plan to do so in a future release.</span></span> <span data-ttu-id="1bd3e-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) が Windows Azure の web ロールでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) is supported in Windows Azure web roles.</span></span>
>
> <span data-ttu-id="1bd3e-110">組織のオンプレミスの Active Directory と Windows Azure Active Directory テナント間の同期をセットアップする方法の詳細については、「[実装および管理を使用して AD FS 2.0 シングル サインオン](https://technet.microsoft.com/library/jj205462.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-110">For details on how to setup synchronization between your on-premise Active Directory and your Windows Azure Active Directory tenant please see [Use AD FS 2.0 to implement and manage single sign-on](https://technet.microsoft.com/library/jj205462.aspx).</span></span>
>
> <span data-ttu-id="1bd3e-111">Windows Azure Active Directory が現在として使用できますが、[無料のプレビュー サービス](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-111">Windows Azure Active Directory is currently available as a [free preview service](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>


## <a name="requirements"></a><span data-ttu-id="1bd3e-112">要件:</span><span class="sxs-lookup"><span data-stu-id="1bd3e-112">Requirements:</span></span>

- <span data-ttu-id="1bd3e-113">Visual Studio 2012 または[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span><span class="sxs-lookup"><span data-stu-id="1bd3e-113">Visual Studio 2012 or [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span></span>
- <span data-ttu-id="1bd3e-114">[Web ツールの Visual Studio 2012 用拡張機能](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)または[Web ツールの拡張機能の Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="1bd3e-114">[Web Tools Extensions for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) or [Web Tools Extensions for Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span></span>
- <span data-ttu-id="1bd3e-115">[Microsoft ASP.NET ツールの Windows の Visual Studio 2012 – Azure Active Directory](https://go.microsoft.com/fwlink/?LinkID=282306)または[Microsoft ASP.NET ツールの Windows 用 Azure Active Directory-Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span><span class="sxs-lookup"><span data-stu-id="1bd3e-115">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) or [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span></span>

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a><span data-ttu-id="1bd3e-116">Visual Studio 2012 での ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-116">Create an ASP.NET Web Application with Visual Studio 2012</span></span>

<span data-ttu-id="1bd3e-117">任意の Web アプリケーションを作成するには Visual Studio 2012 で、このチュートリアルは、ASP.NET MVC イントラネット テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-117">You can create any Web Application with Visual Studio 2012, this tutorial uses the ASP.NET MVC intranet template.</span></span>

1. <span data-ttu-id="1bd3e-118">新しい ASP.NET MVC 4 イントラネット アプリケーションを作成し、すべての既定値をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-118">Create a new ASP.NET MVC 4 Intranet Application and accept all the defaults.</span></span> <span data-ttu-id="1bd3e-119">(In する必要があります**tra** net ではなく**を入力してください**net プロジェクト)。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-119">(It must be an In **tra** net and not In **ter** net project).</span></span>
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a><span data-ttu-id="1bd3e-120">(この場合、テナントのグローバル管理者である場合)、Window Azure の認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-120">Enable Window Azure Authentication (When you are a Global Administrator of the Tenet)</span></span>

<span data-ttu-id="1bd3e-121">サインアップして、新しいテナントを作成するには (既存の Office 365 アカウント) を使用して既存の Windows Azure Active Directory テナントがあるない場合、[新しい Windows Azure Active Directory アカウント](http://g.microsoftonline.com/0AX00en/5)します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-121">If you do not have an existing Windows Azure Active Directory tenant (For example, through an existing Office 365 account) you can create a new tenant by signing up for a [new Windows Azure Active Directory account](http://g.microsoftonline.com/0AX00en/5).</span></span>

1. <span data-ttu-id="1bd3e-122">[プロジェクト] メニューから選択**を有効にする Windows Azure Authentication**:</span><span class="sxs-lookup"><span data-stu-id="1bd3e-122">From the Project menu select **Enable Windows Azure Authentication**:</span></span>

   ![](windows-azure-authentication/_static/image2.png)

2. <span data-ttu-id="1bd3e-123">Windows Azure Active Directory テナント (contoso.onmicrosoft.com など) のドメインを入力し、クリックして**を有効にする**:</span><span class="sxs-lookup"><span data-stu-id="1bd3e-123">Enter the domain for your Windows Azure Active Directory tenant (for example, contoso.onmicrosoft.com) and click **Enable**:</span></span>

![](windows-azure-authentication/_static/image3.png)

3. <span data-ttu-id="1bd3e-124">管理者は、Windows Azure Active Directory テナントで Web 認証ダイアログ サインイン。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-124">In the Web Authentication dialog sign in as an administrator for your Windows Azure Active Directory tenant:</span></span>

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a><span data-ttu-id="1bd3e-125">理念でも、非管理者によって Window Azure を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-125">Enable Window Azure by a non-administrator of the Tenet</span></span>

<span data-ttu-id="1bd3e-126">Windows Azure Active Directory テナントのグローバル管理者特権がない、アプリケーションをプロビジョニングするためのチェック ボックスをオフにできます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-126">If you do not have Global Administrator privilege for your Windows Azure Active Directory tenant, you can uncheck the checkbox for provisioning the application.</span></span>

![](windows-azure-authentication/_static/image6.png)

<span data-ttu-id="1bd3e-127">ダイアログ ボックスが表示されます、**ドメイン**、**アプリケーション プリンシパル Id**と**応答 URL** Azure Active Directory とアプリケーションのプロビジョニングに必要な理念でもあります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-127">The dialog will display the **Domain**, **Application Principal Id** and **Reply URL** which are required for provisioning the application with an Azure Active Directory tenet.</span></span> <span data-ttu-id="1bd3e-128">情報は、アプリケーションをプロビジョニングするための十分な特権を持っている人に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-128">You need to give this information to someone who has sufficient privilege to provision the application.</span></span> <span data-ttu-id="1bd3e-129">参照してください[Windows Azure Active Directory - ASP.NET アプリケーションでシングル サインオンを実装する方法](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)コマンドレットを使用して手動でサービス プリンシパルを作成する方法の詳細について。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-129">See[How to implement single sign-on with Windows Azure Active Directory - ASP.NET Application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) for details on how to use cmdlet to create the service principal manually.</span></span>
<span data-ttu-id="1bd3e-130">クリックすることができます、アプリケーションが正常にプロビジョニングされたら、 **、選択した設定を web.config の更新を続行**します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-130">Once the application has been successfully provisioned, you can click on **Continue to update web.config with the selected settings**.</span></span> <span data-ttu-id="1bd3e-131">クリックすることができますが発生します。 へのプロビジョニングを待っている間に、アプリケーションの開発を続ける場合**に近いプロジェクト ファイル内の設定を保存**します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-131">If you want to continue developing the application while waiting for provisioning to happen, you can click **Close to remember the settings in project file**.</span></span> <span data-ttu-id="1bd3e-132">次回の Windows Azure の認証の有効化を呼び出すし、プロビジョニングのチェック ボックスをオフにする、同じ設定が表示されますおよびクリックすることができます**続行**、クリックして、そして**web.configでこれらの設定を適用**.</span><span class="sxs-lookup"><span data-stu-id="1bd3e-132">The next time you invoke Enable Windows Azure Authentication and uncheck the provisioning checkbox, you will see the same settings and you can click **Continue**, then click, **Apply these settings in web.config**.</span></span>

1. <span data-ttu-id="1bd3e-133">アプリケーションが Windows Azure の認証用に構成して Windows Azure Active Directory でプロビジョニングされています。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-133">Wait while your application is configured for Windows Azure Authentication and provisioned with Windows Azure Active Directory.</span></span>
2. <span data-ttu-id="1bd3e-134">アプリケーションの Windows Azure Authentication を有効にすると、クリックして**閉じる。**</span><span class="sxs-lookup"><span data-stu-id="1bd3e-134">Once Windows Azure Authentication has been enabled for your application, click **Close:**</span></span>

    ![](windows-azure-authentication/_static/image7.png)
3. <span data-ttu-id="1bd3e-135">アプリケーションを実行するには、f5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-135">Hit F5 to run your application.</span></span> <span data-ttu-id="1bd3e-136">ログイン ページにする自動的にリダイレクトする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-136">You should automatically get redirected to login page.</span></span> <span data-ttu-id="1bd3e-137">ディレクトリのテナント ユーザーの資格情報を使用して、アプリケーションにログインする.</span><span class="sxs-lookup"><span data-stu-id="1bd3e-137">Use the directory tenet user credentials to login to the application..</span></span>

    ![](windows-azure-authentication/_static/image1.jpg)
4. <span data-ttu-id="1bd3e-138">アプリケーションには、テスト用の自己署名証明書が現在使用しているため、証明書が信頼された証明機関から発行されていませんが、ブラウザーから、警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-138">Because your application is currently using a self-signed test certificate you will receive a warning from the browser that the certificate was not issued by a trusted certificate authority.</span></span>

    <span data-ttu-id="1bd3e-139">この警告は無視してかまいませんローカルの開発中をクリックして**このサイトの閲覧を続行します。**</span><span class="sxs-lookup"><span data-stu-id="1bd3e-139">This warning can be safely ignored during local development by clicking **Continue to this website:**</span></span>

    ![](windows-azure-authentication/_static/image8.png)
5. <span data-ttu-id="1bd3e-140">今すぐが正常にログインする Windows Azure の認証を使用して、アプリケーションに!</span><span class="sxs-lookup"><span data-stu-id="1bd3e-140">You have now successfully logged in to your application using Windows Azure Authentication!</span></span>

    ![](windows-azure-authentication/_static/image2.jpg)

<span data-ttu-id="1bd3e-141">Windows Azure を有効にする認証は、アプリケーションに、次の変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-141">Enabling Windows Azure authentication makes the following changes to your application:</span></span>

- <span data-ttu-id="1bd3e-142">対策、クロスサイト リクエスト フォージェリ ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) クラス (*アプリ\_Start\AntiXsrfConfig.cs* ) をプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-142">An Anti-Cross-Site Request Forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) class ( *App\_Start\AntiXsrfConfig.cs* ) is added to your project.</span></span>
- <span data-ttu-id="1bd3e-143">NuGet パッケージ`System.IdentityModel.Tokens.ValidatingIssuerNameRegistry`をプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-143">The NuGet packages `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` is added to your project.</span></span>
- <span data-ttu-id="1bd3e-144">Windows Identity Foundation の設定、アプリケーションでは、Windows Azure Active Directory テナントからのセキュリティ トークンを受け入れるように構成されます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-144">Windows Identity Foundation settings in your application will be configured to accept security tokens from your Windows Azure Active Directory tenant.</span></span> <span data-ttu-id="1bd3e-145">加えられた変更の展開ビューを表示する次の画像をクリックして、 *Web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-145">Click on the image below to see an expanded view of the changes made to the *Web.config* file.</span></span>

     ![](windows-azure-authentication/_static/image9.png)
- <span data-ttu-id="1bd3e-146">Windows Azure Active Directory テナントでアプリケーションのサービス プリンシパルがプロビジョニングされます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-146">A service principal for your application in your Windows Azure Active Directory tenant will be provisioned.</span></span>
- <span data-ttu-id="1bd3e-147">HTTPS が有効になっているとします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-147">HTTPS is enabled.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="1bd3e-148">Windows Azure へのアプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-148">Deploy the application to Windows Azure</span></span>

<span data-ttu-id="1bd3e-149">完全な手順については、次を参照してください。 [ASP.NET Web アプリケーションを Windows Azure Web サイトを展開する](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-149">For complete instructions, see [Deploying an ASP.NET Web Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

<span data-ttu-id="1bd3e-150">Windows Azure Authentication を Azure Web サイトを使用してアプリケーションを発行するには。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-150">To publish an application using Windows Azure Authentication to an Azure Web Site:</span></span>

1. <span data-ttu-id="1bd3e-151">アプリケーションを右クリックし、選択**発行。**</span><span class="sxs-lookup"><span data-stu-id="1bd3e-151">Right click on your application and select **Publish:**</span></span>

    ![](windows-azure-authentication/_static/image3.jpg)
2. <span data-ttu-id="1bd3e-152">Web の発行 ダイアログ ボックスからダウンロードし、Azure Web サイトの発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-152">From the Publish Web dialog download and import a publishing profile for your Azure Web Site.</span></span>

    ![](windows-azure-authentication/_static/image4.jpg)
3. <span data-ttu-id="1bd3e-153">**接続** タブの表示、**送信先 URL** (アプリケーションのパブリックに公開された URL)。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-153">The **Connection** tab shows the **Destination URL** (the public facing URL for your application).</span></span> <span data-ttu-id="1bd3e-154">クリックして**接続の検証**接続をテストします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-154">Click **Validate Connection** to test your connection:</span></span>

    ![](windows-azure-authentication/_static/image5.jpg)
4. <span data-ttu-id="1bd3e-155">チェック検討以前この Azure Web サイトにパブリッシュした場合、**転送先に追加のファイルを削除**アプリケーションのことを確認するには設定が正常に発行します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-155">If you have published to this Azure Web Site previously consider checking the **Remove additional files at destination** setting to ensure your application publishes cleanly.</span></span> <span data-ttu-id="1bd3e-156">通知、**を有効にする Windows Azure Authentication**  チェック ボックスをオンします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-156">Notice the **Enable Windows Azure Authentication** check box is selected.</span></span>

    ![](windows-azure-authentication/_static/image10.png)
5. <span data-ttu-id="1bd3e-157">省略可能:**プレビュー**タブをクリックして**プレビューの開始**に展開されたファイルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-157">Optional: On the **Preview** tab click **Start Preview** to see the files deployed.</span></span>

    ![](windows-azure-authentication/_static/image6.jpg)
6. <span data-ttu-id="1bd3e-158">クリックして**を発行します。**</span><span class="sxs-lookup"><span data-stu-id="1bd3e-158">Click **Publish.**</span></span>

    <span data-ttu-id="1bd3e-159">ターゲット ホスト用の Windows Azure Authentication を有効にするように促されます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-159">You will be prompted to enable Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="1bd3e-160">をクリックして**を有効にする**を続行します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-160">Click **Enable** to continue:</span></span>

    ![](windows-azure-authentication/_static/image11.png)
7. <span data-ttu-id="1bd3e-161">Windows Azure Active Directory テナントの管理者の資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-161">Enter your administrator credentials for your Windows Azure Active Directory tenant:</span></span>

    ![](windows-azure-authentication/_static/image7.jpg)
8. <span data-ttu-id="1bd3e-162">アプリケーションが正常に公開されると、ブラウザーが発行した web サイトを開きます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-162">Once your application has been successfully published, a browser will open to the published web site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1bd3e-163">5 分 (通常必要が少なく) アプリケーションのターゲット ホスト用の Windows Azure Authentication を有効にした後、Windows Azure Active Directory と完全にプロビジョニングするに時間がかかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-163">It may take up to five minutes (typically must less) for your application to be fully provisioned with Windows Azure Active Directory after enabling Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="1bd3e-164">初めて実行する場合、アプリケーション エラー ACS50001 が発生する場合。名前 '[realm]' の証明書利用者が見つかりませんに数分待ってをもう一度アプリケーションを実行してみてください。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-164">When you first run your application if you receive error ACS50001: Relying party with name ‘[realm]' was not found, then wait a few minutes and try running the application again.</span></span>
9. <span data-ttu-id="1bd3e-165">求められたら、ディレクトリ内のユーザーとしてログインします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-165">When prompted, log in as a user in your directory:</span></span>

    ![](windows-azure-authentication/_static/image8.jpg)
10. <span data-ttu-id="1bd3e-166">正常に、Azure にログインして今すぐ Windows Azure の認証を使用してアプリケーションをホストします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-166">You have now successfully logged into your Azure hosted application using Windows Azure Authentication.</span></span>

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a><span data-ttu-id="1bd3e-167">既知の問題</span><span class="sxs-lookup"><span data-stu-id="1bd3e-167">Known Issues</span></span>

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a><span data-ttu-id="1bd3e-168">Windows Azure の認証を使用する場合、ロール ベースの承認が失敗します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-168">Role-based authorization fails when using Windows Azure Authentication</span></span>

<span data-ttu-id="1bd3e-169">Windows Azure の認証は必要なロール クレームが役割ベースの承認を実行できるように現在提供していません。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-169">Windows Azure Authentication does not currently provide the necessary role claim so that role-based authorization can be performed.</span></span> <span data-ttu-id="1bd3e-170">認証されたユーザーのロールは、Windows Azure Active Directory から手動で取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-170">The role of the authenticated user must be manually retrieved from Windows Azure Active Directory.</span></span>

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="1bd3e-171">Windows のアプリケーションに参照し、Azure の認証結果がエラーで「ACS20016 (live.com) ログインしたユーザーのドメインと一致しません、許可されているこのドメイン STS」</span><span class="sxs-lookup"><span data-stu-id="1bd3e-171">Browsing to an application with Windows Azure Authentication results in the error "ACS20016 The domain of the logged in user (live.com) does not match any allowed domain of this STS"</span></span>

<span data-ttu-id="1bd3e-172">400 エラー応答が取得が Windows Azure Authentication を有効になっているアプリケーションにアクセスしようとした場合、Microsoft アカウント (hotmail.com、live.com、outlook.com など) にログインして既に Microsoft アカウントのドメインWindows Azure Active Directory では認識されません。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-172">If you are already logged in to a Microsoft Account (for example hotmail.com, live.com, outlook.com) and you attempt to access an application that has enabled Windows Azure Authentication you may get a 400 error response because the domain of your Microsoft Account is not recognized by Windows Azure Active Directory.</span></span> <span data-ttu-id="1bd3e-173">アプリケーションにログイン、ログアウト、Microsoft アカウントから最初にします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-173">To log into the application, log out from your Microsoft Account first.</span></span>

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a><span data-ttu-id="1bd3e-174">Windows Azure の認証が有効になっていると、X509CertificateValidationMode 以外のアプリケーションにログイン accounts.accesscontrol.windows.net 証明書の証明書の検証エラーの結果なし</span><span class="sxs-lookup"><span data-stu-id="1bd3e-174">Logging into an application with Windows Azure Authentication enabled and a X509CertificateValidationMode other than None results in certificate validation errors for the accounts.accesscontrol.windows.net certificate</span></span>

<span data-ttu-id="1bd3e-175">証明書の検証は必要でないし、無効のままにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-175">Certificate validation is not required and should be left disabled.</span></span> <span data-ttu-id="1bd3e-176">発行者の証明書の拇印が、WSFederationAuthenticationModule によって検証されます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-176">The thumbprint of the issuer certificate is validated by the WSFederationAuthenticationModule.</span></span>

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="1bd3e-177">Web 認証ダイアログがエラーを示します Windows Azure Authentication を有効にしようとしています"ACS20016:。ログインしているユーザー (contoso.onmicrosoft.com) のドメインと一致しませんこの STS の許可されたどのドメインです。"</span><span class="sxs-lookup"><span data-stu-id="1bd3e-177">When attempting to enable Windows Azure Authentication the Web Authentication dialog shows the error "ACS20016: The domain of the logged in user (contoso.onmicrosoft.com) does not match any allowed domain of this STS."</span></span>

<span data-ttu-id="1bd3e-178">このエラーは、Visual Studio の同じプロセス内からさまざまな Windows Azure Active Directory アカウントを使用して正常にログインしたときに表示があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-178">You may see this error when you have previously successfully logged in using a different Windows Azure Active Directory account from within the same Visual Studio process.</span></span> <span data-ttu-id="1bd3e-179">指定されたアカウントからログアウトするか、Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-179">Log out from the specified account or restart Visual Studio.</span></span> <span data-ttu-id="1bd3e-180">以前ログインし、「サインインしたまま」するオプションを選択する場合は、ブラウザーのクッキーをクリアする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-180">If you previously logged in and selected the option to "Keep me signed in" then you may need to clear your browser cookies.</span></span>

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a><span data-ttu-id="1bd3e-181">ACS20012:要求が有効な Ws-federation プロトコル メッセージではありません。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-181">ACS20012: The request is not a valid WS-Federation protocol message</span></span>

<span data-ttu-id="1bd3e-182">これは、既に Azure サービスのいずれかにその他の Microsoft ID を使用してログインしている場合に発生することができます。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-182">This can happen if you are already logged in with some other Microsoft ID to one of the Azure services.</span></span> <span data-ttu-id="1bd3e-183">使用してプライベート ブラウザー ウィンドウなどの IE で InPrivate または chrome Incognito またはすべての cookie をクリアします。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-183">Use Private browser window like InPrivate in IE or Incognito in Chrome or clear all the cookies.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1bd3e-184">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="1bd3e-184">Additional Resources</span></span>

- <span data-ttu-id="1bd3e-185">[Microsoft ASP.NET ツールの Windows 用 Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="1bd3e-185">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="1bd3e-186">Windows Azure の機能。Id</span><span class="sxs-lookup"><span data-stu-id="1bd3e-186">Windows Azure Features: Identity</span></span>](https://docs.microsoft.com/azure/active-directory/)
- [<span data-ttu-id="1bd3e-187">TechNet:Windows Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bd3e-187">TechNet: Windows Azure Active Directory</span></span>](https://technet.microsoft.com/library/hh967619.aspx)
- [<span data-ttu-id="1bd3e-188">Windows Azure Active Directory:組織のアプリを開発します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-188">Windows Azure Active Directory: Develop Apps for your organization</span></span>](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [<span data-ttu-id="1bd3e-189">Windows Azure Active Directory:複数の組織向けアプリを開発します。</span><span class="sxs-lookup"><span data-stu-id="1bd3e-189">Windows Azure Active Directory: Develop Apps for multiple organizations</span></span>](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [<span data-ttu-id="1bd3e-190">Windows Azure Active Directory でのシングル サインオンを実装する方法</span><span class="sxs-lookup"><span data-stu-id="1bd3e-190">How to implement single sign-on with Windows Azure Active Directory</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- <span data-ttu-id="1bd3e-191">[シングル サインオンが windows Azure Active Directory: Deep Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="1bd3e-191">[Single Sign-On with Windows Azure Active Directory: a Deep Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="1bd3e-192">実装および管理を使用して AD FS 2.0 シングル サインオン</span><span class="sxs-lookup"><span data-stu-id="1bd3e-192">Use AD FS 2.0 to implement and manage single sign-on</span></span>](https://technet.microsoft.com/library/jj205462.aspx)
