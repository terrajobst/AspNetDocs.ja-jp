---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: ログイン、電子メール確認、パスワードリセット (C#) を使用して、SECURE ASP.NET MVC 5 web アプリを作成します。Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET Identity メンバーシップシステムを使用して、電子メールの確認とパスワードのリセットを使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。 ...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 07f5b290b73f75000e6f29fe09e4dc25e144452f
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74899695"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="872b4-104">ログイン、電子メール確認、パスワード リセットを使用して安全な ASP.NET MVC 5 Web アプリを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="872b4-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="872b4-105">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="872b4-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="872b4-106">このチュートリアルでは、ASP.NET Identity メンバーシップシステムを使用して、電子メールの確認とパスワードのリセットを使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="872b4-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="872b4-107">.NET Core を使用するこのチュートリアルの更新バージョンについては、[ASP.NET Core でのアカウントの確認とパスワードの回復] [/aspnet/core/security/authentication/accconfirm] を参照してください。</span><span class="sxs-lookup"><span data-stu-id="872b4-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core[/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="872b4-108">ASP.NET MVC アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="872b4-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="872b4-109">まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。</span><span class="sxs-lookup"><span data-stu-id="872b4-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="872b4-110">[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="872b4-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="872b4-111">警告: このチュートリアルを完了するには、 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="872b4-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="872b4-112">新しい ASP.NET Web プロジェクトを作成し、MVC テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="872b4-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="872b4-113">Web フォームでも ASP.NET Identity がサポートされているため、web フォームアプリで同様の手順に従うことができます。</span><span class="sxs-lookup"><span data-stu-id="872b4-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="872b4-114">既定の認証は、**個々のユーザーアカウント**として残しておきます。</span><span class="sxs-lookup"><span data-stu-id="872b4-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="872b4-115">Azure でアプリをホストする場合は、チェックボックスをオンのままにします。</span><span class="sxs-lookup"><span data-stu-id="872b4-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="872b4-116">このチュートリアルの後半では、Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="872b4-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="872b4-117">[Azure アカウントは無料で開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)ことができます。</span><span class="sxs-lookup"><span data-stu-id="872b4-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="872b4-118">[SSL を使用するようにプロジェクトを](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。</span><span class="sxs-lookup"><span data-stu-id="872b4-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="872b4-119">アプリを実行し、 **[登録]** リンクをクリックして、ユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="872b4-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="872b4-120">この時点で、電子メールの検証は、 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性でのみ行うことができます。</span><span class="sxs-lookup"><span data-stu-id="872b4-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="872b4-121">サーバーエクスプローラーで、 **[Data Connections\DefaultConnection\Tables\AspNetUsers]** に移動して右クリックし、 **[テーブル定義を開く]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="872b4-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="872b4-122">次の図は、`AspNetUsers` スキーマを示しています。</span><span class="sxs-lookup"><span data-stu-id="872b4-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="872b4-123">**AspNetUsers**テーブルを右クリックし、 **[テーブルデータの表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="872b4-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="872b4-124">この時点で、電子メールは確認されていません。</span><span class="sxs-lookup"><span data-stu-id="872b4-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="872b4-125">行をクリックし、[削除] を選択します。</span><span class="sxs-lookup"><span data-stu-id="872b4-125">Click on the row and select delete.</span></span> <span data-ttu-id="872b4-126">次の手順でもう一度このメールを追加し、確認の電子メールを送信します。</span><span class="sxs-lookup"><span data-stu-id="872b4-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="872b4-127">電子メールの確認</span><span class="sxs-lookup"><span data-stu-id="872b4-127">Email confirmation</span></span>

<span data-ttu-id="872b4-128">新しいユーザー登録の電子メールを確認して、他のユーザーが偽装していないこと (つまり、他のユーザーの電子メールに登録されていないこと) を確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="872b4-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="872b4-129">ディスカッションフォーラムがあるとしたら、`"bob@example.com"` が `"joe@contoso.com"`として登録されないようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="872b4-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="872b4-130">電子メールを確認しないと、`"joe@contoso.com"` アプリから不要な電子メールを受け取る可能性があります。</span><span class="sxs-lookup"><span data-stu-id="872b4-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="872b4-131">Bob が誤って `"bib@example.com"` として登録されていて気付かないとしても、アプリには正しい電子メールがないため、パスワードの回復を使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="872b4-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="872b4-132">電子メールの確認では、bot から制限された保護のみを提供し、特定のスパム送信者からの保護を提供しません。登録に使用できる多くの勤務先の電子メールエイリアスがあります。</span><span class="sxs-lookup"><span data-stu-id="872b4-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="872b4-133">通常は、電子メール、SMS テキストメッセージ、または別のメカニズムによって確認される前に、新しいユーザーが web サイトにデータを投稿できないようにします。</span><span class="sxs-lookup"><span data-stu-id="872b4-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="872b4-134">以下のセクションでは、電子メールの確認を有効にし、コードを変更して、新しく登録されたユーザーが電子メールを確認するまでログインできないようにします。</span><span class="sxs-lookup"><span data-stu-id="872b4-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="872b4-135">SendGrid をフックする</span><span class="sxs-lookup"><span data-stu-id="872b4-135">Hook up SendGrid</span></span>

<span data-ttu-id="872b4-136">このセクションの手順は最新ではありません。</span><span class="sxs-lookup"><span data-stu-id="872b4-136">The instructions in this section are not current.</span></span> <span data-ttu-id="872b4-137">詳細な手順については、「 [SendGrid 電子メールプロバイダーの構成](/aspnet/core/security/authentication/accconfirm#configure-email-provider)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="872b4-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="872b4-138">このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して電子メール通知を追加する方法のみを説明していますが、SMTP などのメカニズムを使用[して電子](#addRes)メールを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="872b4-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="872b4-139">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="872b4-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="872b4-140">[Azure SendGrid のサインアップページ](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)にアクセスし、無料の sendgrid アカウントを登録します。</span><span class="sxs-lookup"><span data-stu-id="872b4-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="872b4-141">*App_Start/identityconfig.cs*で次のようなコードを追加して、sendgrid を構成します。</span><span class="sxs-lookup"><span data-stu-id="872b4-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="872b4-142">次のインクルードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="872b4-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="872b4-143">このサンプルを簡単に保つために、アプリケーションの設定を web.config*ファイルに保存します*。</span><span class="sxs-lookup"><span data-stu-id="872b4-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="872b4-144">セキュリティ-機密データをソースコードに格納しません。</span><span class="sxs-lookup"><span data-stu-id="872b4-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="872b4-145">アカウントと資格情報は appSetting に格納されます。</span><span class="sxs-lookup"><span data-stu-id="872b4-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="872b4-146">Azure では、これらの値を Azure portal の [ **[構成](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] タブに安全に格納できます。</span><span class="sxs-lookup"><span data-stu-id="872b4-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="872b4-147">[ASP.NET と Azure にパスワードやその他の機密データをデプロイするためのベストプラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="872b4-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="872b4-148">アカウントコントローラーで電子メールの確認を有効にする</span><span class="sxs-lookup"><span data-stu-id="872b4-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="872b4-149">*Views\Account\ConfirmEmail.cshtml*ファイルに正しい razor 構文があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="872b4-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="872b4-150">(最初の行の @ 文字が欠落している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="872b4-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="872b4-151">)</span><span class="sxs-lookup"><span data-stu-id="872b4-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="872b4-152">アプリを実行し、[登録] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="872b4-152">Run the app and click the Register link.</span></span> <span data-ttu-id="872b4-153">登録フォームを送信すると、ログインしたことになります。</span><span class="sxs-lookup"><span data-stu-id="872b4-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="872b4-154">電子メールアカウントを確認し、リンクをクリックして電子メールを確認します。</span><span class="sxs-lookup"><span data-stu-id="872b4-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="872b4-155">ログインする前に電子メールの確認を要求する</span><span class="sxs-lookup"><span data-stu-id="872b4-155">Require email confirmation before log in</span></span>

<span data-ttu-id="872b4-156">現在、ユーザーが登録フォームを完了すると、ログインします。</span><span class="sxs-lookup"><span data-stu-id="872b4-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="872b4-157">通常は、ログを記録する前に電子メールを確認します。</span><span class="sxs-lookup"><span data-stu-id="872b4-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="872b4-158">以下のセクションでは、新しいユーザーがログイン (認証) される前に確認済みの電子メールを要求するようにコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="872b4-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="872b4-159">次の強調表示された変更を使用して、`HttpPost Register` メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="872b4-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="872b4-160">`SignInAsync` メソッドをコメントアウトすることで、ユーザーは登録によってサインインされません。</span><span class="sxs-lookup"><span data-stu-id="872b4-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="872b4-161">`TempData["ViewBagLink"] = callbackUrl;` 行を使用して、電子メールを送信することなく、[アプリをデバッグ](#dbg)し、登録をテストできます。</span><span class="sxs-lookup"><span data-stu-id="872b4-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="872b4-162">`ViewBag.Message` は、確認の指示を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="872b4-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="872b4-163">[ダウンロードサンプル](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)には、電子メールを設定せずに電子メールの確認をテストするコードが含まれており、アプリケーションのデバッグにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="872b4-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="872b4-164">`Views\Shared\Info.cshtml` ファイルを作成し、次の razor マークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="872b4-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="872b4-165">[承認属性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)を Home コントローラーの `Contact` アクションメソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="872b4-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="872b4-166">**[Contact]** リンクをクリックすると、匿名ユーザーがアクセス権を持っていないこと、および認証されたユーザーがアクセス権を持っていないことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="872b4-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="872b4-167">また、`HttpPost Login` アクションメソッドも更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="872b4-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="872b4-168">*Views\Shared\Error.cshtml*ビューを更新して、エラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="872b4-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="872b4-169">テストする電子メールエイリアスが含まれている**AspNetUsers**テーブル内のすべてのアカウントを削除します。</span><span class="sxs-lookup"><span data-stu-id="872b4-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="872b4-170">アプリを実行し、電子メールアドレスが確認されるまでログインできないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="872b4-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="872b4-171">電子メールアドレスを確認したら、 **[Contact]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="872b4-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="872b4-172">パスワードの回復/リセット</span><span class="sxs-lookup"><span data-stu-id="872b4-172">Password recovery/reset</span></span>

<span data-ttu-id="872b4-173">アカウントコントローラーの `HttpPost ForgotPassword` アクションメソッドからコメント文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="872b4-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="872b4-174">*Views\Account\Login.cshtml* razor ビューファイルの `ForgotPassword` [html.actionlink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx)からコメント文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="872b4-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="872b4-175">ログインページに、パスワードをリセットするためのリンクが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="872b4-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="872b4-176">電子メールの再送信の確認リンク</span><span class="sxs-lookup"><span data-stu-id="872b4-176">Resend email confirmation link</span></span>

<span data-ttu-id="872b4-177">ユーザーは、新しいローカルアカウントを作成すると、ログオンする前に使用する必要がある確認のリンクを電子メールで送信します。</span><span class="sxs-lookup"><span data-stu-id="872b4-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="872b4-178">ユーザーが誤って確認メールを削除した場合、または電子メールが届いていない場合は、確認リンクを再度送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="872b4-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="872b4-179">次のコード変更は、これを有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="872b4-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="872b4-180">次のヘルパーメソッドを、*コントローラー*ファイルの一番下に追加します。</span><span class="sxs-lookup"><span data-stu-id="872b4-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="872b4-181">新しいヘルパーを使用するように Register メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="872b4-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="872b4-182">ユーザーアカウントが確認されていない場合は、ログイン方法を更新してパスワードを再送信します。</span><span class="sxs-lookup"><span data-stu-id="872b4-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="872b4-183">ソーシャルおよびローカルログインアカウントの結合</span><span class="sxs-lookup"><span data-stu-id="872b4-183">Combine social and local login accounts</span></span>

<span data-ttu-id="872b4-184">電子メールリンクをクリックして、ローカルアカウントとソーシャルアカウントを組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="872b4-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="872b4-185">次のシーケンスでは、最初にローカルログインとして **RickAndMSFT@gmail.com** が作成されますが、最初にアカウントをソーシャルログとして作成してから、ローカルログインを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="872b4-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="872b4-186">**[管理]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="872b4-186">Click on the **Manage** link.</span></span> <span data-ttu-id="872b4-187">このアカウントに関連付けられている**外部ログイン: 0**に注意してください。</span><span class="sxs-lookup"><span data-stu-id="872b4-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="872b4-188">別のログインサービスへのリンクをクリックし、アプリの要求を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="872b4-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="872b4-189">2つのアカウントが結合されているので、いずれかのアカウントでログオンすることができます。</span><span class="sxs-lookup"><span data-stu-id="872b4-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="872b4-190">認証サービスのソーシャルログがダウンした場合、またはソーシャルアカウントへのアクセスが失われる可能性がある場合に備えて、ユーザーにローカルアカウントを追加することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="872b4-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="872b4-191">次の図では、Tom はソーシャルログ (ページに表示されている**外部ログイン: 1**から参照できます) です。</span><span class="sxs-lookup"><span data-stu-id="872b4-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="872b4-192">**[パスワードの選択]** をクリックすると、同じアカウントに関連付けられているローカルログオンを追加できます。</span><span class="sxs-lookup"><span data-stu-id="872b4-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="872b4-193">より詳細な電子メールの確認</span><span class="sxs-lookup"><span data-stu-id="872b4-193">Email confirmation in more depth</span></span>

<span data-ttu-id="872b4-194">このトピックでは[、ASP.NET Identity を使用したチュートリアルアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="872b4-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="872b4-195">アプリのデバッグ</span><span class="sxs-lookup"><span data-stu-id="872b4-195">Debugging the app</span></span>

<span data-ttu-id="872b4-196">リンクを含む電子メールが表示されない場合は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="872b4-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="872b4-197">迷惑メールまたは迷惑メールフォルダーを確認します。</span><span class="sxs-lookup"><span data-stu-id="872b4-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="872b4-198">SendGrid アカウントにログインし、[ [Email Activity] リンク](https://sendgrid.com/logs/index)をクリックします。</span><span class="sxs-lookup"><span data-stu-id="872b4-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="872b4-199">電子メールを使用せずに検証リンクをテストするには、[完成したサンプル](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="872b4-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="872b4-200">ページに確認のリンクと確認コードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="872b4-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="872b4-201">その他の資料</span><span class="sxs-lookup"><span data-stu-id="872b4-201">Additional Resources</span></span>

- [<span data-ttu-id="872b4-202">推奨されるリソースへのリンク ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="872b4-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="872b4-203">[ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)パスワードの回復とアカウントの確認についてさらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="872b4-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="872b4-204">[Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)このチュートリアルでは、Facebook と Google OAuth 2 認証を使用して ASP.NET MVC 5 アプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="872b4-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="872b4-205">また、Id データベースにデータを追加する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="872b4-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="872b4-206">[メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC アプリを Azure にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。</span><span class="sxs-lookup"><span data-stu-id="872b4-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="872b4-207">このチュートリアルでは、Azure のデプロイ、ロールを使用してアプリをセキュリティで保護する方法、メンバーシップ API を使用してユーザーとロールを追加する方法、および追加のセキュリティ機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="872b4-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="872b4-208">OAuth 2 用の Google アプリを作成し、そのアプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="872b4-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="872b4-209">Facebook でアプリを作成し、アプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="872b4-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="872b4-210">プロジェクトでの SSL の設定</span><span class="sxs-lookup"><span data-stu-id="872b4-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
