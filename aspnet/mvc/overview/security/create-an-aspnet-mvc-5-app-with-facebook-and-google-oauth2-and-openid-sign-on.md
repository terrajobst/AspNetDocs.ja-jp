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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="ea7c1-103">Facebook、Twitter、LinkedIn、Google の OAuth2 サインオンを使用して ASP.NET MVC 5 アプリを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="ea7c1-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="ea7c1-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ea7c1-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="ea7c1-105">このチュートリアルでは、ユーザーが Facebook、Twitter、LinkedIn、Microsoft、Google などの外部認証プロバイダーからの資格情報を使用して[OAuth 2.0](http://oauth.net/2/)を使用してログインできるようにする、ASP.NET MVC 5 web アプリケーションを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="ea7c1-106">わかりやすくするために、このチュートリアルでは Facebook と Google の資格情報を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="ea7c1-107">Web サイトでこれらの資格情報を有効にすると、これらの外部プロバイダーのアカウントが何百万ものユーザーに既に存在するため、大きな利点があります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="ea7c1-108">このようなユーザーは、新しい資格情報のセットを作成して記憶する必要がない場合に、サイトにサインアップすることができます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="ea7c1-109">「 [ASP.NET MVC 5 app WITH SMS」と「Email 2 Factor authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="ea7c1-110">このチュートリアルでは、ユーザーのプロファイルデータを追加する方法と、メンバーシップ API を使用してロールを追加する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="ea7c1-111">このチュートリアルは[Rick Anderson](https://blogs.msdn.com/rickAndy)によって作成されました (Twitter の[@RickAndMSFT](https://twitter.com/RickAndMSFT) )。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="ea7c1-112">作業の開始</span><span class="sxs-lookup"><span data-stu-id="ea7c1-112">Getting Started</span></span>

<span data-ttu-id="ea7c1-113">まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="ea7c1-114">Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="ea7c1-115">Dropbox、GitHub、Linkedin、Instagram、Buffer、Salesforce、蒸気、Stack Exchange、Tripit、Twitch、Twitter、Yahoo! などのヘルプについては、この[サンプルプロジェクト](https://github.com/matthewdunsdon/oauthforaspnet)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="ea7c1-116">Google OAuth 2 を使用し、SSL 警告なしでローカルにデバッグするには、Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="ea7c1-117">**スタート**ページで **[新しいプロジェクト]** をクリックするか、メニューを使用して **[ファイル]** 、 **[新しいプロジェクト]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="ea7c1-118">最初のアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="ea7c1-118">Creating Your First Application</span></span>

<span data-ttu-id="ea7c1-119">**[新しいプロジェクト]** をクリックし、左側の **[ビジュアルC# ]** 、 **[web]** の順に選択し、 **[ASP.NET web Application]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="ea7c1-120">プロジェクトに "MvcAuth" という名前を指定し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="ea7c1-121">**[New ASP.NET Project]** ダイアログボックスで、 **[MVC]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="ea7c1-122">認証が**個々のユーザーアカウント**ではない場合は、 **[認証の変更]** ボタンをクリックして、**個々のユーザーアカウント**を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="ea7c1-123">**クラウドでホスト**を確認することで、アプリは Azure で非常に簡単にホストできます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="ea7c1-124">**クラウドで [ホスト**] を選択した場合は、[構成] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="ea7c1-125">NuGet を使用して最新の OWIN ミドルウェアに更新する</span><span class="sxs-lookup"><span data-stu-id="ea7c1-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="ea7c1-126">NuGet パッケージマネージャーを使用して、 [OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)を更新します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="ea7c1-127">左側のメニューで **[更新プログラム]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="ea7c1-128">**[すべて更新]** ボタンをクリックするか、OWIN パッケージのみを検索することができます (次の図を参照)。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="ea7c1-129">次の図では、OWIN パッケージのみが表示されています。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="ea7c1-130">パッケージマネージャーコンソール (PMC) から `Update-Package` コマンドを入力すると、すべてのパッケージが更新されます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="ea7c1-131">**F5**キーを押すか、Ctrl キーを押し**ながら f5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="ea7c1-132">次の図では、ポート番号は1234です。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="ea7c1-133">アプリケーションを実行すると、別のポート番号が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="ea7c1-134">ブラウザーウィンドウのサイズによっては、ナビゲーションアイコンをクリックして、 **[ホーム]** 、 **[バージョン情報]** 、 **[連絡先]** 、 **[登録]** 、 **[ログイン]** リンクを表示することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="ea7c1-135">プロジェクトでの SSL の設定</span><span class="sxs-lookup"><span data-stu-id="ea7c1-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="ea7c1-136">Google や Facebook などの認証プロバイダーに接続するには、SSL を使用するように IIS Express を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="ea7c1-137">ログイン後に SSL を使用して、HTTP に戻るのではなく、ログイン cookie をユーザー名とパスワードと同じように秘密にし、SSL を使用せずにネットワーク経由でクリアテキストで送信することが重要です。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="ea7c1-138">また、MVC パイプラインを実行する前に、ハンドシェイクを実行し、チャネルをセキュリティで保護する (HTTP よりも HTTPS の速度が非常に遅い) こともあります。そのため、ログインした後に HTTP にリダイレクトすると、現在の要求は行われません。要求の速度が大幅に向上します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="ea7c1-139">**ソリューションエクスプローラー**で、 **MvcAuth**プロジェクトをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="ea7c1-140">F4 キーを押すと、プロジェクトのプロパティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="ea7c1-141">または、 **[表示]** メニューの **[プロパティウィンドウ]** をクリックすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="ea7c1-142">**SSL Enabled**を True に変更します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="ea7c1-143">SSL URL をコピーします (他の SSL プロジェクトを作成していない場合は `https://localhost:44300/` になります)。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="ea7c1-144">**ソリューションエクスプローラー**で、 **MvcAuth**プロジェクトを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="ea7c1-145">**[Web]** タブを選択し、 **[プロジェクト url]** ボックスに SSL url を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="ea7c1-146">ファイルを保存します (Ctl + S)。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="ea7c1-147">Facebook と Google の認証アプリを構成するには、この URL が必要になります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="ea7c1-148">[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性を `Home` コントローラーに追加して、すべての要求で HTTPS を使用する必要があることを要求します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="ea7c1-149">より安全な方法は、 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)フィルターをアプリケーションに追加することです。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="ea7c1-150">「SSL を使用してアプリケーションを保護する」および「&quot;の承認」のセクション「 [auth と SQL DB を使用した ASP.NET MVC アプリの作成」と「Azure App Service へのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」の&quot; を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="ea7c1-151">Home コントローラーの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="ea7c1-152">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="ea7c1-153">以前に証明書をインストールしたことがある場合は、このセクションの残りの部分をスキップし、 [OAuth 2 用の Google アプリの作成に進み、アプリをプロジェクトに接続](#goog)します。それ以外の場合は、指示に従って、IIS Express が生成した自己署名証明書を信頼します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="ea7c1-154">**[セキュリティの警告]** ダイアログを読み、localhost を表す証明書をインストールする場合は [**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="ea7c1-155">IE は *ホーム* ページを表示し、SSL の警告はありません。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="ea7c1-156">Google Chrome は証明書も受け入れ、警告なしで HTTPS コンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="ea7c1-157">Firefox は独自の証明書ストアを使用するため、警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="ea7c1-158">このアプリケーションでは **、[リスクを理解して**います] をクリックしても安全です。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ea7c1-159">OAuth 2 用の Google アプリを作成し、そのアプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="ea7c1-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ea7c1-160">Google OAuth の現在の手順については、「 [ASP.NET Core での google 認証の構成](/aspnet/core/security/authentication/social/google-logins)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="ea7c1-161">[Google Developers Console](https://console.developers.google.com/)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="ea7c1-162">前にプロジェクトを作成していない場合は、左のタブで **[資格情報]** を選択し、 **[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="ea7c1-163">左側のタブで、 **[資格情報]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="ea7c1-164">**[資格情報の作成]** 、 **[OAuth クライアント ID]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="ea7c1-165">**[クライアント ID の作成]** ダイアログボックスで、アプリケーションの種類の既定の**Web アプリケーション**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="ea7c1-166">承認された**JavaScript**オリジンを、上で使用した ssl URL (他の ssl プロジェクトを作成していない場合は`https://localhost:44300/`) に設定します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="ea7c1-167">承認された**リダイレクト URI**を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="ea7c1-168">[OAuth 同意画面] メニュー項目をクリックし、電子メールアドレスと製品名を設定します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="ea7c1-169">フォームが完了したら、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="ea7c1-170">[ライブラリ] メニュー項目をクリックし、 **Google + API**を検索して、[有効にする] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="ea7c1-171">次の画像は、有効になっている Api を示しています。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="ea7c1-172">Google Api の API マネージャーで、 **[資格情報]** タブを開いて**クライアント ID**を取得します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="ea7c1-173">アプリケーションシークレットを使用して JSON ファイルを保存するには、をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="ea7c1-174">**ClientId**と**clientsecret**をコピーし、 *App_Start*フォルダーの*Startup.Auth.cs*ファイルにある `UseGoogleAuthentication` メソッドに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="ea7c1-175">次に示す**ClientId**と**clientsecret**の値はサンプルであり、動作しません。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="ea7c1-176">セキュリティ-機密データをソースコードに格納しません。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="ea7c1-177">このサンプルを単純にするために、アカウントと資格情報が上記のコードに追加されています。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="ea7c1-178">[ASP.NET と Azure App Service にパスワードやその他の機密データをデプロイするためのベストプラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="ea7c1-179">**Ctrl キーを押しながら F5 キーを押して** アプリケーションをビルドし、実行します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="ea7c1-180">**[Log in]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="ea7c1-181">**[別のサービスを使用してログインする]** で、 **[Google]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="ea7c1-182">上記のいずれかの手順を実行しないと、HTTP 401 エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="ea7c1-183">上記の手順を再確認してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-183">Recheck your steps above.</span></span> <span data-ttu-id="ea7c1-184">必要な設定 (**製品名**など) を忘れた場合は、不足している項目を追加して保存します。認証が機能するまでに数分かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="ea7c1-185">資格情報を入力する Google サイトにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="ea7c1-186">資格情報を入力すると、先ほど作成した web アプリケーションにアクセス許可を付与するように求められます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="ea7c1-187">**[Accept]\(受け入れる\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-187">Click **Accept**.</span></span> <span data-ttu-id="ea7c1-188">これで、MvcAuth アプリケーションの**登録**ページにリダイレクトされ、Google アカウントを登録できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="ea7c1-189">Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="ea7c1-190">**[登録]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ea7c1-191">Facebook でアプリを作成し、アプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="ea7c1-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ea7c1-192">Facebook OAuth2 の現在の認証手順については、「 [facebook 認証の構成](/aspnet/core/security/authentication/social/facebook-logins)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="ea7c1-193">メンバーシップデータを確認する</span><span class="sxs-lookup"><span data-stu-id="ea7c1-193">Examine the Membership Data</span></span>

<span data-ttu-id="ea7c1-194">**[表示]** メニューの **[サーバーエクスプローラー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="ea7c1-195">**Defaultconnection (MvcAuth)** を展開し、 **[テーブル]** を展開して、 **[AspNetUsers]** を右クリックし、 **[テーブルデータの表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers テーブルデータ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="ea7c1-197">ユーザークラスへのプロファイルデータの追加</span><span class="sxs-lookup"><span data-stu-id="ea7c1-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="ea7c1-198">このセクションでは、次の図に示すように、登録時にユーザーデータに生年月日と自宅の町を追加します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![自宅の町と Bday を使用した reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="ea7c1-200">*Models\IdentityModels.cs*ファイルを開き、生年月日と自宅のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="ea7c1-201">*Models\AccountViewModels.cs*ファイルを開き、`ExternalLoginConfirmationViewModel`で [誕生日と自宅の住所] プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="ea7c1-202">次に示すように、*コントローラー*ファイルを開き、`ExternalLoginConfirmation` アクションメソッドに生年月日と自宅の郵便番号を追加します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="ea7c1-203">*Views\Account\ExternalLoginConfirmation.cshtml*ファイルに生年月日と自宅の町を追加します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="ea7c1-204">もう一度 Facebook アカウントをアプリケーションに登録できるように、メンバーシップデータベースを削除し、新しい生年月日と自宅のプロファイル情報を追加できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="ea7c1-205">**ソリューションエクスプローラー**で、**すべてのファイルを表示** アイコンをクリックし、*追加\_Data\aspnet-MvcAuth-&lt;datestamp&gt;* を右クリックして、**削除** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="ea7c1-206">**[ツール]** メニューの **[NuGet パッケージ]** マネージャー をクリックし、 **[パッケージマネージャーコンソール]** (PMC) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="ea7c1-207">PMC に次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="ea7c1-208">移行を有効にする</span><span class="sxs-lookup"><span data-stu-id="ea7c1-208">Enable-Migrations</span></span>
2. <span data-ttu-id="ea7c1-209">追加-移行の初期化</span><span class="sxs-lookup"><span data-stu-id="ea7c1-209">Add-Migration Init</span></span>
3. <span data-ttu-id="ea7c1-210">Update-Database</span><span class="sxs-lookup"><span data-stu-id="ea7c1-210">Update-Database</span></span>

<span data-ttu-id="ea7c1-211">アプリケーションを実行し、FaceBook と Google を使用してログインし、一部のユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="ea7c1-212">メンバーシップデータを確認する</span><span class="sxs-lookup"><span data-stu-id="ea7c1-212">Examine the Membership Data</span></span>

<span data-ttu-id="ea7c1-213">**[表示]** メニューの **[サーバーエクスプローラー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="ea7c1-214">**AspNetUsers**を右クリックし、 **[テーブルデータの表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="ea7c1-215">`HomeTown` フィールドと `BirthDate` フィールドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="ea7c1-216">アプリをログオフし、別のアカウントでログインする</span><span class="sxs-lookup"><span data-stu-id="ea7c1-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="ea7c1-217">Facebook のを使用してアプリにログオンしてからログアウトし、別の Facebook アカウント (同じブラウザーを使用) でもう一度ログインすると、使用した前の Facebook アカウントにすぐにログインします。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="ea7c1-218">別のアカウントを使用するには、facebook に移動し、Facebook でログアウトする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="ea7c1-219">他のサードパーティの認証プロバイダーにも同じ規則が適用されます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="ea7c1-220">または、別のブラウザーを使用して別のアカウントでログインすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea7c1-221">次の手順</span><span class="sxs-lookup"><span data-stu-id="ea7c1-221">Next Steps</span></span>

<span data-ttu-id="ea7c1-222">Yahoo と LinkedIn の手順については、「OWIN by Jerrie Pelser [for The yahoo And Linkedin OAuth security providers for](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="ea7c1-223">ソーシャルログインボタンを有効にする方法については、Jerrie の「ASP.NET MVC 5 の非常にソーシャルログインボタン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="ea7c1-224">チュートリアル「 [auth と SQL DB を使用して ASP.NET MVC アプリを作成し、Azure App Service にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)する」に従って、このチュートリアルを続行し、次の内容を示します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="ea7c1-225">アプリを Azure にデプロイする方法。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="ea7c1-226">ロールを使用してアプリをセキュリティで保護する方法。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="ea7c1-227">[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)および[承認](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)フィルターを使用してアプリをセキュリティで保護する方法。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="ea7c1-228">メンバーシップ API を使用してユーザーとロールを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="ea7c1-229">このチュートリアルの気に入った点と改善点についてのフィードバックをお寄せください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="ea7c1-230">「[コードの使用方法を表示](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)する」で新しいトピックを要求することもできます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="ea7c1-231">ASP.NET に追加する新機能について質問したり、投票したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="ea7c1-232">たとえば、[ユーザーとロールを作成して管理](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)するためのツールに投票することができます。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="ea7c1-233">ASP.NET 外部認証サービスのしくみの詳細については、「Robert McMurray の[外部認証サービス](https://asp.net/web-api/overview/security/external-authentication-services)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="ea7c1-234">また、Robert の記事では、Microsoft と Twitter の認証を有効にする方法についても詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="ea7c1-235">Tom Dykstra の優れた[EF/MVC チュートリアル](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、Entity Framework の操作方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea7c1-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
