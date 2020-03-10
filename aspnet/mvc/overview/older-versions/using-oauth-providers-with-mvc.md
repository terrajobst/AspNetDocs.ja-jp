---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4 での OAuth プロバイダーの使用 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ユーザーが外部プロバイダーから資格情報 (Facebo... など) を使用してログインできるようにする ASP.NET MVC 4 web アプリケーションを構築する方法について説明します。
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433366"
---
# <a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="5c710-103">MVC 4 で OAuth プロバイダーを使用する</span><span class="sxs-lookup"><span data-stu-id="5c710-103">Using OAuth Providers with MVC 4</span></span>

<span data-ttu-id="5c710-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5c710-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5c710-105">このチュートリアルでは、ユーザーが Facebook、Twitter、Microsoft、Google などの外部プロバイダーから資格情報を使用してログインできるようにする ASP.NET MVC 4 web アプリケーションを作成する方法について説明します。また、これらのプロバイダーの機能の一部をに統合します。web アプリケーション。</span><span class="sxs-lookup"><span data-stu-id="5c710-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="5c710-106">わかりやすくするために、このチュートリアルでは Facebook の資格情報を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5c710-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="5c710-107">ASP.NET MVC 5 web アプリケーションで外部資格情報を使用するには、 [Facebook と Google OAuth2 を使用した ASP.NET MVC 5 アプリの作成と OpenID サインオン](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)に関する web サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="5c710-108">Web サイトでこれらの資格情報を有効にすると、これらの外部プロバイダーのアカウントが何百万ものユーザーに既に存在するため、大きな利点があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="5c710-109">このようなユーザーは、新しい資格情報のセットを作成して記憶する必要がない場合に、サイトにサインアップすることができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="5c710-110">また、ユーザーがこれらのプロバイダーのいずれかを使用してログインした後、プロバイダーからソーシャル操作を組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="5c710-111">ビルドする内容</span><span class="sxs-lookup"><span data-stu-id="5c710-111">What you'll build</span></span>

<span data-ttu-id="5c710-112">このチュートリアルには主に次の2つの目標があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="5c710-113">ユーザーが OAuth プロバイダーからの資格情報でログインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="5c710-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="5c710-114">プロバイダーからアカウント情報を取得し、その情報をサイトのアカウント登録と統合します。</span><span class="sxs-lookup"><span data-stu-id="5c710-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="5c710-115">このチュートリアルの例では、Facebook を認証プロバイダーとして使用する方法に焦点を当てていますが、プロバイダーのいずれかを使用するようにコードを変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="5c710-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="5c710-116">プロバイダーを実装する手順は、このチュートリアルで説明されている手順とよく似ています。</span><span class="sxs-lookup"><span data-stu-id="5c710-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="5c710-117">プロバイダーの API セットを直接呼び出す場合は、大きな違いに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c710-118">前提条件</span><span class="sxs-lookup"><span data-stu-id="5c710-118">Prerequisites</span></span>

- <span data-ttu-id="5c710-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)または[Web 用 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="5c710-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="5c710-120">または</span><span class="sxs-lookup"><span data-stu-id="5c710-120">Or</span></span>

- <span data-ttu-id="5c710-121">Microsoft Visual Studio 2010 SP1 または[Visual Web Developer Express 2010 sp1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="5c710-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="5c710-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="5c710-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="5c710-123">さらに、このトピックでは、ASP.NET MVC と Visual Studio に関する基本的な知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="5c710-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="5c710-124">ASP.NET MVC 4 の概要については、「 [ASP.NET mvc 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)の概要」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="5c710-125">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="5c710-125">Create the project</span></span>

<span data-ttu-id="5c710-126">Visual Studio で、新しい ASP.NET MVC 4 Web アプリケーションを作成し、&quot;OAuthMVC&quot;という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5c710-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="5c710-127">.NET Framework 4.5 または4のいずれかを対象にすることができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-127">You can target either .NET Framework 4.5 or 4.</span></span>

![プロジェクトの作成](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="5c710-129">新しい ASP.NET MVC 4 プロジェクトウィンドウで、 **[インターネットアプリケーション]** を選択し、 **Razor**をビューエンジンとして残します。</span><span class="sxs-lookup"><span data-stu-id="5c710-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![インターネットアプリケーションの選択](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="5c710-131">プロバイダーを有効にする</span><span class="sxs-lookup"><span data-stu-id="5c710-131">Enable a provider</span></span>

<span data-ttu-id="5c710-132">インターネットアプリケーションテンプレートを使用して MVC 4 web アプリケーションを作成すると、アプリ\_の [開始] フォルダーに AuthConfig.cs という名前のファイルがプロジェクトに作成されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig ファイル](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="5c710-134">AuthConfig ファイルには、外部認証プロバイダーのクライアントを登録するためのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c710-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="5c710-135">既定では、このコードはコメントアウトされているため、外部プロバイダーは有効になりません。</span><span class="sxs-lookup"><span data-stu-id="5c710-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="5c710-136">外部認証クライアントを使用するには、このコードのコメントを解除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="5c710-137">サイトに含めるプロバイダーのみをコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="5c710-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="5c710-138">このチュートリアルでは、Facebook の資格情報のみを有効にします。</span><span class="sxs-lookup"><span data-stu-id="5c710-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="5c710-139">上記の例では、メソッドに登録パラメーターに空の文字列が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="5c710-140">ここでアプリケーションを実行しようとすると、パラメーターに空の文字列が許可されていないため、アプリケーションは引数の例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="5c710-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="5c710-141">有効な値を指定するには、次のセクションで示すように、外部プロバイダーに web サイトを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="5c710-142">外部プロバイダーへの登録</span><span class="sxs-lookup"><span data-stu-id="5c710-142">Registering with an external provider</span></span>

<span data-ttu-id="5c710-143">外部プロバイダーからの資格情報を使用してユーザーを認証するには、web サイトをプロバイダーに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="5c710-144">サイトを登録すると、クライアントを登録するときに含めるパラメーター (キー、id、シークレットなど) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="5c710-145">使用するプロバイダーを持つアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="5c710-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="5c710-146">このチュートリアルでは、これらのプロバイダーに登録するために実行する必要があるすべての手順については説明しません。</span><span class="sxs-lookup"><span data-stu-id="5c710-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="5c710-147">通常、この手順は困難ではありません。</span><span class="sxs-lookup"><span data-stu-id="5c710-147">The steps are typically not difficult.</span></span> <span data-ttu-id="5c710-148">サイトを正常に登録するには、これらのサイトに記載されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="5c710-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="5c710-149">サイトの登録を開始するには、次の開発者向けサイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="5c710-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="5c710-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="5c710-151">Google</span><span class="sxs-lookup"><span data-stu-id="5c710-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="5c710-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="5c710-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="5c710-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="5c710-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="5c710-154">Facebook にサイトを登録するときに、次の図に示すように、サイトドメインに &quot;localhost&quot; を指定し、URL に `&quot; http://localhost/&quot;` します。</span><span class="sxs-lookup"><span data-stu-id="5c710-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="5c710-155">Localhost の使用はほとんどのプロバイダーで機能しますが、現在、Microsoft プロバイダーでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="5c710-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="5c710-156">Microsoft プロバイダーには、有効な web サイトの URL を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![サイトの登録](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="5c710-158">前の画像では、アプリ id、アプリのシークレット、連絡先の電子メールの値が削除されています。</span><span class="sxs-lookup"><span data-stu-id="5c710-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="5c710-159">実際にサイトを登録すると、その値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="5c710-160">アプリ id とアプリシークレットの値は、アプリケーションに追加するため、メモしておきます。</span><span class="sxs-lookup"><span data-stu-id="5c710-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="5c710-161">テストユーザーの作成</span><span class="sxs-lookup"><span data-stu-id="5c710-161">Creating test users</span></span>

<span data-ttu-id="5c710-162">既存の Facebook アカウントを使用してサイトをテストすることが気にならない場合は、このセクションを省略してもかまいません。</span><span class="sxs-lookup"><span data-stu-id="5c710-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="5c710-163">Facebook アプリの管理ページで、アプリケーションのテストユーザーを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c710-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="5c710-164">これらのテストアカウントを使用して、サイトにログインすることができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="5c710-165">テストユーザーを作成するには、左側のナビゲーションウィンドウで **[ロール]** リンクをクリックし、 **[作成]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="5c710-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![テストユーザーの作成](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="5c710-167">Facebook サイトでは、要求したテストアカウントの数が自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="5c710-168">プロバイダーからのアプリケーション id とシークレットの追加</span><span class="sxs-lookup"><span data-stu-id="5c710-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="5c710-169">Facebook から id とシークレットを受け取ったので、AuthConfig ファイルに戻り、パラメーター値として追加します。</span><span class="sxs-lookup"><span data-stu-id="5c710-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="5c710-170">次に示す値は実際の値ではありません。</span><span class="sxs-lookup"><span data-stu-id="5c710-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="5c710-171">外部資格情報を使用してログインする</span><span class="sxs-lookup"><span data-stu-id="5c710-171">Log in with external credentials</span></span>

<span data-ttu-id="5c710-172">これで、サイトで外部資格情報を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="5c710-173">アプリケーションを実行し、右上隅にある [ログイン] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="5c710-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="5c710-174">このテンプレートは、Facebook をプロバイダーとして登録し、プロバイダーのボタンを含むことを自動的に認識します。</span><span class="sxs-lookup"><span data-stu-id="5c710-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="5c710-175">複数のプロバイダーを登録すると、1つのボタンが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![外部ログイン](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="5c710-177">このチュートリアルでは、外部プロバイダーの [ログイン] ボタンをカスタマイズする方法については説明しません。</span><span class="sxs-lookup"><span data-stu-id="5c710-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="5c710-178">詳細については、「 [OAuth/OpenID を使用する場合のログイン UI のカスタマイズ](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="5c710-179">Facebook の資格情報でログインするには、[Facebook] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="5c710-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="5c710-180">外部プロバイダーの1つを選択すると、そのサイトにリダイレクトされ、そのサービスからログインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="5c710-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="5c710-181">次の図は、Facebook のログイン画面を示しています。</span><span class="sxs-lookup"><span data-stu-id="5c710-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="5c710-182">ここでは、oauthmvcexample という名前のサイトにログインするために Facebook アカウントを使用していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 認証](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="5c710-184">Facebook の資格情報を使用してログインすると、サイトが基本情報にアクセスできることをユーザーに通知するページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![アクセス許可の要求](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="5c710-186">**[アプリにアクセスする]** を選択した後、ユーザーはサイトに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="5c710-187">次の図は、ユーザーが Facebook の資格情報でログインした後の登録ページを示しています。</span><span class="sxs-lookup"><span data-stu-id="5c710-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="5c710-188">通常、ユーザー名はプロバイダーからの名前で事前に入力されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-188">The user name is typically pre-filled with a name from the provider.</span></span>

![registrations](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="5c710-190">**[登録]** をクリックして登録を完了します。</span><span class="sxs-lookup"><span data-stu-id="5c710-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="5c710-191">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="5c710-191">Close the browser.</span></span>

<span data-ttu-id="5c710-192">新しいアカウントがデータベースに追加されていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="5c710-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="5c710-193">サーバーエクスプローラーで、 **Defaultconnection**データベースを開き、 **Tables**フォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="5c710-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![データベース テーブル](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="5c710-195">**UserProfile**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5c710-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![データの表示](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="5c710-197">追加した新しいアカウントが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-197">You will see the new account you added.</span></span> <span data-ttu-id="5c710-198">**Web ページ\_OAuthMembership**テーブルのデータを確認します。</span><span class="sxs-lookup"><span data-stu-id="5c710-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="5c710-199">追加したアカウントの外部プロバイダーに関連するデータがさらに表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="5c710-200">外部認証のみを有効にする場合は、これで完了です。</span><span class="sxs-lookup"><span data-stu-id="5c710-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="5c710-201">ただし、次のセクションに示すように、プロバイダーからの情報を新しいユーザー登録プロセスにさらに統合することができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="5c710-202">追加のユーザー情報のモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="5c710-202">Create models for additional user information</span></span>

<span data-ttu-id="5c710-203">前のセクションでご存知のように、組み込みアカウントの登録に関する追加情報を取得する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5c710-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="5c710-204">ただし、ほとんどの外部プロバイダーは、ユーザーに関する追加情報を返します。</span><span class="sxs-lookup"><span data-stu-id="5c710-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="5c710-205">以下のセクションでは、その情報を保持し、データベースに保存する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5c710-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="5c710-206">具体的には、ユーザーのフルネーム、ユーザーの個人用 web ページの URI、および Facebook によってアカウントが検証されたかどうかを示す値を保持します。</span><span class="sxs-lookup"><span data-stu-id="5c710-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="5c710-207">追加のユーザー情報を格納するテーブルを追加するには、 [Code First Migrations](https://msdn.microsoft.com/data/jj591621)を使用します。</span><span class="sxs-lookup"><span data-stu-id="5c710-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="5c710-208">既存のデータベースにテーブルを追加しようとしているため、最初に現在のデータベースのスナップショットを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="5c710-209">現在のデータベースのスナップショットを作成することによって、後で新しいテーブルだけを含む移行を作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c710-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="5c710-210">現在のデータベースのスナップショットを作成するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="5c710-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="5c710-211">**パッケージマネージャーコンソール**を開く</span><span class="sxs-lookup"><span data-stu-id="5c710-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="5c710-212">**Enable-移行**コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="5c710-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="5c710-213">**[追加-移行の初期-ignorechanges 追加]** コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="5c710-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="5c710-214">コマンド「 **update-database** 」を実行します。</span><span class="sxs-lookup"><span data-stu-id="5c710-214">Run the command **update-database**</span></span>

<span data-ttu-id="5c710-215">ここでは、新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c710-215">Now, you will add the new properties.</span></span> <span data-ttu-id="5c710-216">[モデル] フォルダーで、AccountModels.cs ファイルを開き、RegisterExternalLoginModel クラスを見つけます。</span><span class="sxs-lookup"><span data-stu-id="5c710-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="5c710-217">RegisterExternalLoginModel クラスは、認証プロバイダーから返される値を保持します。</span><span class="sxs-lookup"><span data-stu-id="5c710-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="5c710-218">次に強調表示されているように、FullName と Link という名前のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c710-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="5c710-219">また、AccountModels.cs で、ExtraUserInformation という名前の新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c710-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="5c710-220">このクラスは、データベースに作成される新しいテーブルを表します。</span><span class="sxs-lookup"><span data-stu-id="5c710-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="5c710-221">[プロパティ] コンテキストクラスで、下に強調表示されているコードを追加して、新しいクラスの DbSet プロパティを作成します。</span><span class="sxs-lookup"><span data-stu-id="5c710-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="5c710-222">これで、新しいテーブルを作成する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="5c710-222">You are now ready to create the new table.</span></span> <span data-ttu-id="5c710-223">次のように、パッケージマネージャーコンソールをもう一度開きます。</span><span class="sxs-lookup"><span data-stu-id="5c710-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="5c710-224">**AddExtraUserInformation**コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="5c710-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="5c710-225">コマンド「 **update-database** 」を実行します。</span><span class="sxs-lookup"><span data-stu-id="5c710-225">Run the command **update-database**</span></span>

<span data-ttu-id="5c710-226">新しいテーブルがデータベースに存在するようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c710-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="5c710-227">追加データを取得する</span><span class="sxs-lookup"><span data-stu-id="5c710-227">Retrieve the additional data</span></span>

<span data-ttu-id="5c710-228">追加のユーザーデータを取得するには、2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="5c710-229">最初の方法は、認証要求時に既定で返されるユーザーデータを保持することです。</span><span class="sxs-lookup"><span data-stu-id="5c710-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="5c710-230">2つ目の方法は、プロバイダー API を呼び出し、詳細情報を要求することです。</span><span class="sxs-lookup"><span data-stu-id="5c710-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="5c710-231">FullName と Link の値は、Facebook によって自動的に返されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="5c710-232">Facebook API の呼び出しによってアカウントが取得されたことを Facebook が検証したかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="5c710-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="5c710-233">まず、FullName と Link の値を設定してから、後で検証済みの値を取得します。</span><span class="sxs-lookup"><span data-stu-id="5c710-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="5c710-234">追加のユーザーデータを取得するには、 **Controllers**フォルダー内の**AccountController.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5c710-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="5c710-235">このファイルには、アカウントのログ記録、登録、管理を行うためのロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c710-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="5c710-236">具体的には、 **Externallogincallback**および**externallogincallback**と呼ばれるメソッドに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="5c710-237">これらのメソッド内では、アプリケーションの外部ログイン操作をカスタマイズするコードを追加できます。</span><span class="sxs-lookup"><span data-stu-id="5c710-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="5c710-238">**Externallogincallback**メソッドの最初の行には、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5c710-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="5c710-239">追加のユーザーデータは、 **Verifyauthentication**メソッドから返される**Authenticationresult**オブジェクトの**ExtraData**プロパティに戻されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="5c710-240">Facebook クライアントには、 **ExtraData**プロパティに次の値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c710-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="5c710-241">id</span><span class="sxs-lookup"><span data-stu-id="5c710-241">id</span></span>
- <span data-ttu-id="5c710-242">name</span><span class="sxs-lookup"><span data-stu-id="5c710-242">name</span></span>
- <span data-ttu-id="5c710-243">link</span><span class="sxs-lookup"><span data-stu-id="5c710-243">link</span></span>
- <span data-ttu-id="5c710-244">gender</span><span class="sxs-lookup"><span data-stu-id="5c710-244">gender</span></span>
- <span data-ttu-id="5c710-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="5c710-245">accesstoken</span></span>

<span data-ttu-id="5c710-246">他のプロバイダーは、ExtraData プロパティに類似しているがわずかに異なるデータを持ちます。</span><span class="sxs-lookup"><span data-stu-id="5c710-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="5c710-247">ユーザーがサイトを初めて使用する場合は、追加データを取得し、そのデータを確認ビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="5c710-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="5c710-248">メソッドの最後のコードブロックは、ユーザーがサイトを初めて使用する場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="5c710-249">次の行を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5c710-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="5c710-250">次の行に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="5c710-251">この変更には、FullName プロパティと Link プロパティの値のみが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5c710-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="5c710-252">**Externalloginconfirmation**メソッドで、以下の強調表示されているコードを変更して、追加のユーザー情報を保存します。</span><span class="sxs-lookup"><span data-stu-id="5c710-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="5c710-253">ビューの調整</span><span class="sxs-lookup"><span data-stu-id="5c710-253">Adjusting the view</span></span>

<span data-ttu-id="5c710-254">プロバイダーから取得した追加のユーザーデータが登録ページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="5c710-255">**Views**/**Account**フォルダーで、 **externalloginconfirmation. cshtml**を開きます。</span><span class="sxs-lookup"><span data-stu-id="5c710-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="5c710-256">[ユーザー名] の既存のフィールドの下に、[FullName]、[Link]、および [ピクチャ] リンクのフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c710-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="5c710-257">これで、アプリケーションを実行し、追加情報が保存された新しいユーザーを登録する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="5c710-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="5c710-258">まだサイトに登録されていないアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="5c710-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="5c710-259">別のテストアカウントを使用するか、再利用するアカウントの**UserProfile**および**Web ページ\_oauthmembership**テーブル内の行を削除することができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="5c710-260">これらの行を削除すると、アカウントが再度登録されることになります。</span><span class="sxs-lookup"><span data-stu-id="5c710-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="5c710-261">アプリケーションを実行し、新しいユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="5c710-261">Run the application and register the new user.</span></span> <span data-ttu-id="5c710-262">今回は、確認ページに多くの値が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-262">Notice that this time the confirmation page contains more values.</span></span>

![registrations](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="5c710-264">登録が完了したら、ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="5c710-264">After completing registration, close the browser.</span></span> <span data-ttu-id="5c710-265">データベースを調べて、 **ExtraUserInformation**テーブルの新しい値を確認します。</span><span class="sxs-lookup"><span data-stu-id="5c710-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="5c710-266">Facebook API の NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="5c710-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="5c710-267">Facebook には、操作を実行するために呼び出すことができる[API](https://developers.facebook.com/docs/reference/apis/)が用意されています。</span><span class="sxs-lookup"><span data-stu-id="5c710-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="5c710-268">Facebook API は、HTTP 要求を送信するか、これらの要求の送信を容易にする NuGet パッケージのインストールを使用して呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="5c710-269">このチュートリアルでは、NuGet パッケージの使用方法について説明しますが、NuGet パッケージのインストールは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="5c710-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="5c710-270">このチュートリアルでは、Facebook C# SDK パッケージを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5c710-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="5c710-271">Facebook API の呼び出しに役立つ NuGet パッケージが他にもあります。</span><span class="sxs-lookup"><span data-stu-id="5c710-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="5c710-272">**[NuGet パッケージの管理]** ウィンドウで、Facebook C# SDK パッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="5c710-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![パッケージのインストール](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="5c710-274">Facebook C# SDK を使用して、ユーザーのアクセストークンを必要とする操作を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5c710-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="5c710-275">次のセクションでは、アクセストークンを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5c710-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="5c710-276">アクセストークンの取得</span><span class="sxs-lookup"><span data-stu-id="5c710-276">Retrieve access token</span></span>

<span data-ttu-id="5c710-277">ほとんどの外部プロバイダーは、ユーザーの資格情報が検証された後にアクセストークンを返します。</span><span class="sxs-lookup"><span data-stu-id="5c710-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="5c710-278">このアクセストークンは、認証されたユーザーのみが使用できる操作を呼び出すことができるため、非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="5c710-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="5c710-279">そのため、より多くの機能を提供する必要がある場合は、アクセストークンの取得と格納が不可欠です。</span><span class="sxs-lookup"><span data-stu-id="5c710-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="5c710-280">外部プロバイダーによっては、アクセストークンの有効期間が限られている場合があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="5c710-281">有効なアクセストークンがあることを確認するには、ユーザーがログインするたびにそれを取得し、それをデータベースに保存するのではなく、セッション値として格納します。</span><span class="sxs-lookup"><span data-stu-id="5c710-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="5c710-282">**Externallogincallback**メソッドでは、アクセストークンも**Authenticationresult**オブジェクトの**ExtraData**プロパティに戻されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="5c710-283">強調表示されているコードを**Externallogincallback**に追加して、**セッション**オブジェクトにアクセストークンを保存します。</span><span class="sxs-lookup"><span data-stu-id="5c710-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="5c710-284">このコードは、ユーザーが Facebook アカウントでログインするたびに実行されます。</span><span class="sxs-lookup"><span data-stu-id="5c710-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="5c710-285">この例では Facebook からアクセストークンを取得しますが、&quot;accesstoken&quot;という名前の同じキーを使用して外部プロバイダーからアクセストークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="5c710-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="5c710-286">ログオフ中</span><span class="sxs-lookup"><span data-stu-id="5c710-286">Logging off</span></span>

<span data-ttu-id="5c710-287">既定の**ログオフ**メソッドでは、アプリケーションからユーザーがログアウトされますが、外部プロバイダーからユーザーがログアウトされることはありません。</span><span class="sxs-lookup"><span data-stu-id="5c710-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="5c710-288">ユーザーを Facebook からログアウトし、ユーザーがログオフした後にトークンが保持されないようにするには、次の強調表示されたコードを AccountController の**LogOff**メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="5c710-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="5c710-289">`next` パラメーターで指定する値は、ユーザーが Facebook からログアウトした後に使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="5c710-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="5c710-290">ローカルコンピューターでテストする場合は、ローカルサイトの正しいポート番号を指定します。</span><span class="sxs-lookup"><span data-stu-id="5c710-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="5c710-291">実稼働環境では、contoso.com などの既定のページを指定します。</span><span class="sxs-lookup"><span data-stu-id="5c710-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="5c710-292">アクセストークンを必要とするユーザー情報を取得する</span><span class="sxs-lookup"><span data-stu-id="5c710-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="5c710-293">アクセストークンを格納し、Facebook C# SDK パッケージをインストールしたので、これらを一緒に使用して、facebook から追加のユーザー情報を要求することができます。</span><span class="sxs-lookup"><span data-stu-id="5c710-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="5c710-294">**Externalloginconfirmation**メソッドで、アクセストークンの値を渡して、 **FacebookClient**クラスのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="5c710-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="5c710-295">現在の認証済みユーザーの**検証済み**プロパティの値を要求します。</span><span class="sxs-lookup"><span data-stu-id="5c710-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="5c710-296">"**確認済み**" プロパティは、携帯電話にメッセージを送信するなど、他の方法で Facebook がアカウントを検証したかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="5c710-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="5c710-297">この値をデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="5c710-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="5c710-298">この場合も、ユーザーのデータベース内のレコードを削除するか、別の Facebook アカウントを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c710-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="5c710-299">アプリケーションを実行し、新しいユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="5c710-299">Run the application, and register the new user.</span></span> <span data-ttu-id="5c710-300">検証済みプロパティの値を確認するには、 **ExtraUserInformation**テーブルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c710-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5c710-301">まとめ</span><span class="sxs-lookup"><span data-stu-id="5c710-301">Conclusion</span></span>

<span data-ttu-id="5c710-302">このチュートリアルでは、ユーザー認証と登録データ用に Facebook と統合されたサイトを作成しました。</span><span class="sxs-lookup"><span data-stu-id="5c710-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="5c710-303">MVC 4 web アプリケーション用に設定されている既定の動作と、その既定の動作をカスタマイズする方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="5c710-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="5c710-304">関連トピック</span><span class="sxs-lookup"><span data-stu-id="5c710-304">Related topics</span></span>

- [<span data-ttu-id="5c710-305">認証および SQL DB を使用する ASP.NET MVC アプリの作成と、Azure App Service へのデプロイ</span><span class="sxs-lookup"><span data-stu-id="5c710-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
