---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: ASP.NET Web ページ (Razor) サイトで外部サイトを使用してログインする |Microsoft Docs
author: Rick-Anderson
description: この記事では、Facebook、Google、Twitter、Yahoo、およびその他のサイト (サポートする方法) を使用して、ASP.NET Web ページ (Razor) サイトにログインする方法について説明します。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518788"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="ac671-103">ASP.NET Web ページ (Razor) サイトで外部サイトを使用してログインする</span><span class="sxs-lookup"><span data-stu-id="ac671-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="ac671-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ac671-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ac671-105">この記事では、Facebook、Google、Twitter、Yahoo などのサイトを使用して ASP.NET Web ページ (Razor) サイトにログインする方法について説明します。つまり、サイトで OAuth と OpenID をサポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ac671-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="ac671-106">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="ac671-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="ac671-107">WebMatrix スターターサイトテンプレートを使用するときに、他のサイトからのログインを有効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ac671-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="ac671-108">この記事で導入された ASP.NET 機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ac671-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="ac671-109">`OAuthWebSecurity` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="ac671-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ac671-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="ac671-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ac671-111">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="ac671-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="ac671-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="ac671-112">WebMatrix 3</span></span>

<span data-ttu-id="ac671-113">ASP.NET Web ページには、 [OAuth](http://oauth.net/)および[OpenID](http://openid.net/)プロバイダーのサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ac671-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="ac671-114">これらのプロバイダーを使用すると、Facebook、Twitter、Microsoft、Google の既存の資格情報を使用して、ユーザーがサイトにログインできるようになります。</span><span class="sxs-lookup"><span data-stu-id="ac671-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="ac671-115">たとえば、Facebook アカウントを使用してログインする場合、ユーザーは Facebook アイコンを選択するだけで、facebook のログインページにリダイレクトされ、ユーザー情報が入力されます。</span><span class="sxs-lookup"><span data-stu-id="ac671-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="ac671-116">その後、Facebook ログインをサイトのアカウントに関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="ac671-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="ac671-117">Web ページのメンバーシップ機能に関連する機能強化として、ユーザーは複数のログイン (ソーシャルネットワークサイトからのログインを含む) を web サイトの1つのアカウントに関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="ac671-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="ac671-118">このイメージは、**スターターサイト**テンプレートのログインページを示しています。ユーザーは、Facebook、Twitter、Google、Microsoft アイコンを選択して、外部アカウントでログインできるようになります。</span><span class="sxs-lookup"><span data-stu-id="ac671-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![外部プロバイダー](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="ac671-120">コメント解除を使用して、いくつかのコード行を**スターターサイト**テンプレートに記述することにより、OAuth および OpenID メンバーシップを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="ac671-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="ac671-121">OAuth プロバイダーおよび OpenID プロバイダーの操作に使用するメソッドとプロパティは、`WebMatrix.Security.OAuthWebSecurity` クラスに含まれています。</span><span class="sxs-lookup"><span data-stu-id="ac671-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="ac671-122">**スターターサイト**テンプレートには、完全なメンバーシップインフラストラクチャが含まれており、ログインページ、メンバーシップデータベース、およびユーザーがローカルの資格情報または別のサイトのサイトにログインするために必要なすべてのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ac671-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="ac671-123">このセクションでは、ユーザーが外部サイトから**スターターサイト**テンプレートに基づくサイトにログインできるようにする方法の例を示します。</span><span class="sxs-lookup"><span data-stu-id="ac671-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="ac671-124">スターターサイトを作成した後、次の手順を実行します (詳細については、こちらを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="ac671-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="ac671-125">OAuth プロバイダー (Facebook、Twitter、Microsoft) を使用するサイトでは、外部サイトでアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="ac671-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="ac671-126">これにより、これらのサイトのログイン機能を呼び出すために必要なアプリケーションキーが得られます。</span><span class="sxs-lookup"><span data-stu-id="ac671-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="ac671-127">OpenID プロバイダー (Google) を使用するサイトでは、アプリケーションを作成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="ac671-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="ac671-128">これらのサイトのすべてについて、ログインし、開発者アプリケーションを作成するためのアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="ac671-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac671-129">Microsoft アプリケーションは、実際の web サイトのライブ URL のみを受け入れるため、ログインのテストにローカル web サイトの URL を使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="ac671-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="ac671-130">適切な認証プロバイダーを指定し、使用するサイトにログインを送信するために、web サイト内のいくつかのファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="ac671-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="ac671-131">この記事では、次のタスクについて個別に説明します。</span><span class="sxs-lookup"><span data-stu-id="ac671-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="ac671-132">Google ログインを有効にする</span><span class="sxs-lookup"><span data-stu-id="ac671-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="ac671-133">Facebook ログインの有効化</span><span class="sxs-lookup"><span data-stu-id="ac671-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="ac671-134">Twitter ログインの有効化</span><span class="sxs-lookup"><span data-stu-id="ac671-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="ac671-135">Google ログインを有効にする</span><span class="sxs-lookup"><span data-stu-id="ac671-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="ac671-136">WebMatrix スターターサイトテンプレートに基づく ASP.NET Web ページサイトを作成または開きます。</span><span class="sxs-lookup"><span data-stu-id="ac671-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="ac671-137">*\_該当*ページを開き、次のコード行をコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="ac671-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="ac671-138">Google ログインをテストしています</span><span class="sxs-lookup"><span data-stu-id="ac671-138">Testing Google login</span></span>

1. <span data-ttu-id="ac671-139">サイトの*既定の cshtml*ページを実行し、 **[ログイン]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="ac671-140">[*ログイン*] ページの **[別のサービスを使用してログインする]** セクションで、 **[Google]** または **[Yahoo]** submit ボタンのいずれかを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="ac671-141">この例では、Google ログインを使用します。</span><span class="sxs-lookup"><span data-stu-id="ac671-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="ac671-142">Web ページは、要求を Google ログインページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="ac671-142">The web page redirects the request to the Google login page.</span></span>

    ![Google サインイン](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="ac671-144">既存の Google アカウントの資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac671-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="ac671-145">アカウントの情報を*Localhost*で使用できるようにするかどうかを確認するメッセージが表示されたら、 **[許可]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="ac671-146">このコードでは、Google トークンを使用してユーザーを認証した後、web サイトのこのページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="ac671-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="ac671-147">このページでは、ユーザーは Google ログインを web サイトの既存のアカウントに関連付けることができます。また、サイトに新しいアカウントを登録して、外部ログインをに関連付けることもできます。</span><span class="sxs-lookup"><span data-stu-id="ac671-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="ac671-149">**[関連付け]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-149">Choose the **Associate** button.</span></span> <span data-ttu-id="ac671-150">ブラウザーがアプリケーションのホームページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="ac671-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="ac671-151">Facebook ログインの有効化</span><span class="sxs-lookup"><span data-stu-id="ac671-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="ac671-152">[Facebook 開発者サイト](https://developers.facebook.com/apps)にアクセスします (まだログインしていない場合はログインしてください)。</span><span class="sxs-lookup"><span data-stu-id="ac671-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="ac671-153">**[新しいアプリの作成]** ボタンを選択し、画面の指示に従って新しいアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="ac671-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="ac671-154">**[アプリを Facebook と統合する方法を選択**します] セクションで、 **[web サイト]** セクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="ac671-155">[サイトの**url** ] フィールドに、サイトの url (`http://www.example.com`など) を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac671-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="ac671-156">**ドメイン**フィールドは省略可能です。これを使用して、ドメイン全体 ( *example.com*など) の認証を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ac671-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ac671-157">`http://localhost:12345` のような URL (番号はローカルポート番号) を使用してローカルコンピューター上でサイトを実行している場合は、サイトをテストするための **[サイトの URL]** フィールドにこの値を追加できます。</span><span class="sxs-lookup"><span data-stu-id="ac671-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="ac671-158">ただし、ローカルサイトのポート番号が変更された場合は常に、アプリケーションの **[サイトの URL]** フィールドを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac671-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="ac671-159">**[変更の保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="ac671-160">もう一度 **[アプリ]** タブをクリックし、アプリケーションのスタートページを表示します。</span><span class="sxs-lookup"><span data-stu-id="ac671-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="ac671-161">アプリケーションの**アプリ ID**と**アプリシークレット**の値をコピーし、一時テキストファイルに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ac671-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="ac671-162">これらの値は、web サイトコードの Facebook プロバイダーに渡されます。</span><span class="sxs-lookup"><span data-stu-id="ac671-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="ac671-163">Facebook 開発者サイトを終了します。</span><span class="sxs-lookup"><span data-stu-id="ac671-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="ac671-164">ここで、ユーザーが Facebook アカウントを使用してサイトにログインできるように、web サイトの2つのページに変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="ac671-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="ac671-165">WebMatrix スターターサイトテンプレートに基づく ASP.NET Web ページサイトを作成または開きます。</span><span class="sxs-lookup"><span data-stu-id="ac671-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="ac671-166">*\_該当*ページを開き、Facebook OAuth プロバイダーのコードをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="ac671-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="ac671-167">コメント解除されたコードブロックは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ac671-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="ac671-168">Facebook アプリケーションの **[アプリ ID]** の値を `appId` パラメーター (引用符内) の値としてコピーします。</span><span class="sxs-lookup"><span data-stu-id="ac671-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="ac671-169">`appSecret` パラメーター値として Facebook アプリケーションから**アプリシークレット**値をコピーします。</span><span class="sxs-lookup"><span data-stu-id="ac671-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="ac671-170">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="ac671-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="ac671-171">Facebook ログインのテスト</span><span class="sxs-lookup"><span data-stu-id="ac671-171">Testing Facebook login</span></span>

1. <span data-ttu-id="ac671-172">サイトの既定の*cshtml*ページを実行し、 **[ログイン]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="ac671-173">[*ログイン*] ページの **[別のサービスを使用してログインする]** セクションで、 **[Facebook]** アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="ac671-174">Web ページは、Facebook ログインページに要求をリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="ac671-174">The web page redirects the request to the Facebook login page.</span></span>

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="ac671-176">Facebook アカウントにログインします。</span><span class="sxs-lookup"><span data-stu-id="ac671-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="ac671-177">このコードでは、Facebook トークンを使用して認証を行い、Facebook ログインをサイトのログインに関連付けることができるページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="ac671-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="ac671-178">ユーザー名または電子メールアドレスは、フォームの **[電子メール]** フィールドに入力されます。</span><span class="sxs-lookup"><span data-stu-id="ac671-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="ac671-180">**[関連付け]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="ac671-181">ブラウザーがホームページに戻り、ログインします。</span><span class="sxs-lookup"><span data-stu-id="ac671-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="ac671-182">Twitter ログインの有効化</span><span class="sxs-lookup"><span data-stu-id="ac671-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="ac671-183">[Twitter 開発者サイト](https://dev.twitter.com/)に移動します。</span><span class="sxs-lookup"><span data-stu-id="ac671-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="ac671-184">**[アプリの作成]** リンクを選択し、サイトにログインします。</span><span class="sxs-lookup"><span data-stu-id="ac671-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="ac671-185">**[アプリケーションの作成]** フォームで、 **[名前]** フィールドと **[説明]** フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="ac671-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="ac671-186">**[Web サイト]** フィールドに、サイトの URL (`http://www.example.com`など) を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac671-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ac671-187">(`http://localhost:12345`のような URL を使用して) サイトをローカルでテストしている場合、Twitter は URL を受け入れない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ac671-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="ac671-188">ただし、ローカルループバック IP アドレス (`http://127.0.0.1:12345`など) を使用できる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ac671-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="ac671-189">これにより、アプリケーションをローカルでテストするプロセスが簡単になります。</span><span class="sxs-lookup"><span data-stu-id="ac671-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="ac671-190">ただし、ローカルサイトのポート番号が変更されるたびに、アプリケーションの**Web サイト**フィールドを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac671-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="ac671-191">**[コールバック URL]** フィールドに、Twitter にログインした後にユーザーが返す web サイトのページの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac671-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="ac671-192">たとえば、スタートサイトのホームページ (ログイン状態を認識する) にユーザーを送信するには、 **[Web サイト]** フィールドに入力したものと同じ URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac671-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="ac671-193">使用条件に同意し、 **[Twitter アプリケーションの作成]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="ac671-194">**[マイアプリケーション**] ランディングページで、作成したアプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="ac671-195">**[詳細]** タブで一番下までスクロールし、 **[アクセストークンの作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="ac671-196">**[詳細]** タブで、アプリケーションの**コンシューマーキー**と**コンシューマーシークレット**の値をコピーし、一時テキストファイルに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ac671-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="ac671-197">これらの値は、web サイトコードの Twitter プロバイダーに渡されます。</span><span class="sxs-lookup"><span data-stu-id="ac671-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="ac671-198">Twitter サイトを終了します。</span><span class="sxs-lookup"><span data-stu-id="ac671-198">Exit the Twitter site.</span></span>

<span data-ttu-id="ac671-199">これで、ユーザーが Twitter アカウントを使用してサイトにログインできるように、web サイトの2つのページに変更が加えられました。</span><span class="sxs-lookup"><span data-stu-id="ac671-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="ac671-200">WebMatrix スターターサイトテンプレートに基づく ASP.NET Web ページサイトを作成または開きます。</span><span class="sxs-lookup"><span data-stu-id="ac671-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="ac671-201">*\_該当*ページを開き、Twitter OAuth プロバイダーのコードをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="ac671-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="ac671-202">コメント解除されたコードブロックは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ac671-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="ac671-203">Twitter アプリケーションの**コンシューマーキー**の値を `consumerKey` パラメーター (引用符内) の値としてコピーします。</span><span class="sxs-lookup"><span data-stu-id="ac671-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="ac671-204">`consumerSecret` パラメーターの値として、Twitter アプリケーションから**コンシューマーシークレット**の値をコピーします。</span><span class="sxs-lookup"><span data-stu-id="ac671-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="ac671-205">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="ac671-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="ac671-206">Twitter ログインのテスト</span><span class="sxs-lookup"><span data-stu-id="ac671-206">Testing Twitter login</span></span>

1. <span data-ttu-id="ac671-207">サイトの*既定の cshtml*ページを実行し、 **[ログイン]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="ac671-208">[*ログイン*] ページの **[別のサービスを使用してログインする]** セクションで、 **Twitter**アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac671-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="ac671-209">Web ページによって、作成したアプリケーションの Twitter ログインページに要求がリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="ac671-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="ac671-211">Twitter アカウントにログインします。</span><span class="sxs-lookup"><span data-stu-id="ac671-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="ac671-212">このコードでは、Twitter トークンを使用してユーザーを認証した後、ログインを web サイトアカウントに関連付けることができるページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="ac671-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="ac671-213">名前または電子メールアドレスは、フォームの **[電子メール]** フィールドに入力されます。</span><span class="sxs-lookup"><span data-stu-id="ac671-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="ac671-215">**[関連付け]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ac671-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="ac671-216">ブラウザーがホームページに戻り、ログインします。</span><span class="sxs-lookup"><span data-stu-id="ac671-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ac671-217">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="ac671-217">Additional Resources</span></span>

- [<span data-ttu-id="ac671-218">サイト全体の動作をカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="ac671-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="ac671-219">ASP.NET Web ページサイトにセキュリティとメンバーシップを追加する</span><span class="sxs-lookup"><span data-stu-id="ac671-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
