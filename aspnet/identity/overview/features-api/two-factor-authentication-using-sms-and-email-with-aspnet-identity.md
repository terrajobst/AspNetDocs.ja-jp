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
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456739"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="a04b8-104">SMS と電子メールを使用した2要素認証 (ASP.NET Identity)</span><span class="sxs-lookup"><span data-stu-id="a04b8-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="a04b8-105">[Hao Kung](https://github.com/HaoK)、 [Pranav rastogi](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="a04b8-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="a04b8-106">このチュートリアルでは、SMS と電子メールを使用して2要素認証 (2FA) を設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="a04b8-107">この記事は、Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT))、Pranav Rastogi ([@rustd](https://twitter.com/rustd))、Hao Kung、suhas Joshi によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="a04b8-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="a04b8-108">NuGet サンプルは、主に Hao Kung によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="a04b8-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="a04b8-109">このトピックでは、以下の内容を説明します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-109">This topic covers the following:</span></span>

- [<span data-ttu-id="a04b8-110">Id サンプルのビルド</span><span class="sxs-lookup"><span data-stu-id="a04b8-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="a04b8-111">2要素認証用に SMS を設定する</span><span class="sxs-lookup"><span data-stu-id="a04b8-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="a04b8-112">2要素認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="a04b8-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="a04b8-113">2要素認証プロバイダーを登録する方法</span><span class="sxs-lookup"><span data-stu-id="a04b8-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="a04b8-114">ソーシャルおよびローカルログインアカウントの結合</span><span class="sxs-lookup"><span data-stu-id="a04b8-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="a04b8-115">ブルートフォース攻撃からのアカウントロックアウト</span><span class="sxs-lookup"><span data-stu-id="a04b8-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="a04b8-116">Id サンプルのビルド</span><span class="sxs-lookup"><span data-stu-id="a04b8-116">Building the Identity sample</span></span>

<span data-ttu-id="a04b8-117">このセクションでは、NuGet を使用して、使用するサンプルをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="a04b8-118">まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="a04b8-119">Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="a04b8-120">警告: このチュートリアルを完了するには、Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="a04b8-121">新しい***空***の ASP.NET Web プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="a04b8-122">パッケージマネージャーコンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="a04b8-123">このチュートリアルでは、 [Sendgrid](http://sendgrid.com/)を使用して、sms テキストに電子メール、 [Twilio](https://www.twilio.com/) 、または[aspsms](https://www.aspsms.com/asp.net/identity/testcredits/)を送信します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="a04b8-124">`Identity.Samples` パッケージによって、使用するコードがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="a04b8-125">[SSL を使用するようにプロジェクトを](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="a04b8-126">*省略可能*: sendgrid をフックしてアプリを実行し、電子メールアカウントを登録するには、[電子メールの確認チュートリアル](account-confirmation-and-password-recovery-with-aspnet-identity.md)に記載されている手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="a04b8-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="a04b8-127">*省略可能:* サンプルからデモ用電子メールリンクの確認コードを削除します (アカウントコントローラーの `ViewBag.Link` コード)。</span><span class="sxs-lookup"><span data-stu-id="a04b8-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="a04b8-128">`DisplayEmail` と `ForgotPasswordConfirmation` のアクションメソッドと razor ビュー) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a04b8-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="a04b8-129">*省略可能:* `ViewBag.Status` コードを管理およびアカウントコントローラーから削除し、 *Views\Account\VerifyCode.cshtml*および*Views\Manage\VerifyPhoneNumber.cshtml* razor ビューから削除します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="a04b8-130">または、`ViewBag.Status` の表示を保持して、電子メールや SMS メッセージをフックして送信することなく、このアプリがローカルで動作する方法をテストすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="a04b8-131">警告: このサンプルのセキュリティ設定を変更した場合、生産アプリは、行われた変更を明示的に呼び出すセキュリティ監査を受ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="a04b8-132">2要素認証用に SMS を設定する</span><span class="sxs-lookup"><span data-stu-id="a04b8-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="a04b8-133">このチュートリアルでは、Twilio または ASPSMS を使用する手順について説明しますが、他の SMS プロバイダーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="a04b8-134">**SMS プロバイダーを使用したユーザーアカウントの作成**</span><span class="sxs-lookup"><span data-stu-id="a04b8-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="a04b8-135">[Twilio](https://www.twilio.com/try-twilio)または[aspsms](https://www.aspsms.com/asp.net/identity/testcredits/)アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="a04b8-136">**追加のパッケージのインストール、またはサービス参照の追加**</span><span class="sxs-lookup"><span data-stu-id="a04b8-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="a04b8-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="a04b8-137">Twilio:</span></span>  
   <span data-ttu-id="a04b8-138">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="a04b8-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="a04b8-139">ASPSMS:</span></span>  
   <span data-ttu-id="a04b8-140">次のサービス参照を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="a04b8-141">住所 :</span><span class="sxs-lookup"><span data-stu-id="a04b8-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="a04b8-142">名前空間:</span><span class="sxs-lookup"><span data-stu-id="a04b8-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="a04b8-143">**SMS プロバイダーのユーザー資格情報の確認**</span><span class="sxs-lookup"><span data-stu-id="a04b8-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="a04b8-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="a04b8-144">Twilio:</span></span>  
   <span data-ttu-id="a04b8-145">Twilio アカウントの **[ダッシュボード]** タブで、**アカウント SID**と**認証トークン**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="a04b8-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="a04b8-146">ASPSMS:</span></span>  
   <span data-ttu-id="a04b8-147">アカウント設定から、**ユーザーキー**に移動し、自己定義**パスワード**と共にコピーします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="a04b8-148">これらの値は、後で `SMSAccountIdentification` および `SMSAccountPassword` 変数に格納します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="a04b8-149">**SenderID/オリジネータの指定**</span><span class="sxs-lookup"><span data-stu-id="a04b8-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="a04b8-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="a04b8-150">Twilio:</span></span>  
   <span data-ttu-id="a04b8-151">**[数値]** タブで、Twilio 電話番号をコピーします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="a04b8-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="a04b8-152">ASPSMS:</span></span>  
   <span data-ttu-id="a04b8-153">[発信元の**ロック解除**] メニュー内で、1つ以上の発信者をロック解除するか、英数字の発信者を選択します (すべてのネットワークでサポートされていません)。</span><span class="sxs-lookup"><span data-stu-id="a04b8-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="a04b8-154">この値は、後で変数 `SMSAccountFrom` に格納します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="a04b8-155">**SMS プロバイダーの資格情報をアプリに転送する**</span><span class="sxs-lookup"><span data-stu-id="a04b8-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="a04b8-156">資格情報と送信者の電話番号をアプリで使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="a04b8-157">セキュリティ-機密データをソースコードに格納しません。</span><span class="sxs-lookup"><span data-stu-id="a04b8-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="a04b8-158">このサンプルを単純にするために、アカウントと資格情報が上記のコードに追加されています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="a04b8-159">「Jon の[ASP.NET MVC: ソース管理からプライベート設定を保持](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a04b8-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="a04b8-160">**SMS プロバイダーへのデータ転送の実装**</span><span class="sxs-lookup"><span data-stu-id="a04b8-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="a04b8-161">*アプリ\_Start\IdentityConfig.cs*ファイルで `SmsService` クラスを構成します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="a04b8-162">使用する SMS プロバイダーに応じて、 **Twilio**または**aspsms**セクションのいずれかをアクティブにします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="a04b8-163">アプリを実行し、前に登録したアカウントでログインします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="a04b8-164">ユーザー ID をクリックすると、`Manage` コントローラーで `Index` アクションメソッドがアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="a04b8-165">[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="a04b8-166">数秒で、確認コードを含むテキストメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="a04b8-167">それを入力し、 **[Submit]** を押します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="a04b8-168">[管理] ビューには、電話番号が追加されたことが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="a04b8-169">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="a04b8-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="a04b8-170">`Manage` controller の `Index` アクションメソッドは、前のアクションに基づいてステータスメッセージを設定し、ローカルパスワードを変更するか、ローカルアカウントを追加するためのリンクを提供します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="a04b8-171">また、`Index` 方法では、状態または2FA 電話番号、外部ログイン、2FA が有効になっていること、およびこのブラウザーの [2FA] (後で説明します) を記憶していることを示します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="a04b8-172">タイトルバーのユーザー ID (電子メール) をクリックしても、メッセージは渡されません。</span><span class="sxs-lookup"><span data-stu-id="a04b8-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="a04b8-173">**[電話番号: 削除]** リンクをクリックすると、クエリ文字列として `Message=RemovePhoneSuccess` が渡されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="a04b8-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="a04b8-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="a04b8-175">`AddPhoneNumber` アクションメソッドには、SMS メッセージを受信できる電話番号を入力するためのダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="a04b8-176">**[確認コードの送信]** ボタンをクリックすると、HTTP POST `AddPhoneNumber` アクションメソッドに電話番号が投稿されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="a04b8-177">`GenerateChangePhoneNumberTokenAsync` メソッドは、SMS メッセージで設定されるセキュリティトークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="a04b8-178">SMS サービスが構成されている場合、トークンは文字列として送信され &quot;セキュリティコードはトークン&gt;&quot;&lt;ます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="a04b8-179">`SmsService.SendAsync` メソッドを非同期的に呼び出すと、アプリが `VerifyPhoneNumber` アクションメソッド (次のダイアログを表示) にリダイレクトされます。ここで、確認コードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="a04b8-180">コードを入力して [送信] をクリックすると、コードが HTTP POST `VerifyPhoneNumber` アクションメソッドにポストされます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="a04b8-181">`ChangePhoneNumberAsync` メソッドは、ポストされたセキュリティコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="a04b8-182">コードが正しい場合は、電話番号が `AspNetUsers` テーブルの [`PhoneNumber`] フィールドに追加されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="a04b8-183">この呼び出しが成功すると、`SignInAsync` メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="a04b8-184">`isPersistent` パラメーターは、認証セッションを複数の要求にわたって永続化するかどうかを設定します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="a04b8-185">セキュリティプロファイルを変更すると、新しいセキュリティスタンプが生成され、 *AspNetUsers*テーブルの `SecurityStamp` フィールドに格納されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="a04b8-186">`SecurityStamp` フィールドは、セキュリティ cookie とは異なります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="a04b8-187">セキュリティクッキーは `AspNetUsers` テーブル (または Id DB 内の他の場所) に格納されません。</span><span class="sxs-lookup"><span data-stu-id="a04b8-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="a04b8-188">セキュリティ cookie トークンは、 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)を使用して自己署名され、`UserId, SecurityStamp` と有効期限情報を使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="a04b8-189">Cookie ミドルウェアは、各要求の cookie を確認します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="a04b8-190">`Startup` クラスの `SecurityStampValidator` メソッドは、データベースにヒットし、`validateInterval`で指定されているように、セキュリティスタンプを定期的にチェックします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="a04b8-191">これは、セキュリティプロファイルを変更しない限り、30分 (このサンプルでは) ごとに実行されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="a04b8-192">データベースへのトリップを最小限に抑えるために、30分間隔が選択されました。</span><span class="sxs-lookup"><span data-stu-id="a04b8-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="a04b8-193">セキュリティプロファイルに何らかの変更が加えられた場合は、`SignInAsync` メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="a04b8-194">セキュリティプロファイルが変更されると、データベースは `SecurityStamp` フィールドを更新し、`SignInAsync` メソッドを呼び出さずに、次回の OWIN パイプラインがデータベース (`validateInterval` *) に到達するまでログイン*したままになります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="a04b8-195">これをテストするには、`SignInAsync` メソッドを変更してすぐに制御を戻し、cookie の `validateInterval` プロパティを30分から5秒に設定します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="a04b8-196">上記のコード変更により、セキュリティプロファイルを変更することができます (たとえば、 **2 要素が有効になっている**状態を変更することによって)。 `SecurityStampValidator.OnValidateIdentity` 方法が失敗すると、5秒後にログアウトされます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="a04b8-197">`SignInAsync` メソッドの改行を削除し、別のセキュリティプロファイルを変更して、ログアウトしないようにします。`SignInAsync` メソッドは、新しいセキュリティクッキーを生成します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="a04b8-198">2 要素認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-198">Enable two-factor authentication</span></span>

<span data-ttu-id="a04b8-199">サンプルアプリでは、UI を使用して2要素認証 (2FA) を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="a04b8-200">2FA を有効にするには、ナビゲーションバーでユーザー ID (電子メールエイリアス) をクリックします。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a04b8-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="a04b8-201">[2FA を有効にする] をクリックします。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="a04b8-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="a04b8-202">ログアウトしてから再度ログインします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-202">Log out, then log back in.</span></span> <span data-ttu-id="a04b8-203">電子メールを有効にした場合 ([前のチュートリアル](account-confirmation-and-password-recovery-with-aspnet-identity.md)を参照)、2FA の SMS または電子メールを選択できます。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="a04b8-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="a04b8-204">[コードの確認] ページが表示され、(SMS または電子メールから) コードを入力できます。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="a04b8-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="a04b8-205">[**このブラウザーを記憶**する] チェックボックスをオンにすると、2fa を使用してそのコンピューターとブラウザーでログオンする必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="a04b8-206">2FA を有効にし、[**このブラウザーを記憶**する] をクリックすると、悪意のあるユーザーが自分のアカウントにアクセスしようとしても、コンピューターへのアクセス権がない限り、強力な2fa による保護が提供されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="a04b8-207">この操作は、定期的に使用する任意のプライベートコンピューターで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="a04b8-208">[**このブラウザーを記憶**する] を設定すると、日常的に使用していないコンピューターから2fa のセキュリティが強化され、自分のコンピューターで2fa を使用する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="a04b8-209">2要素認証プロバイダーを登録する方法</span><span class="sxs-lookup"><span data-stu-id="a04b8-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="a04b8-210">新しい MVC プロジェクトを作成すると、 *IdentityConfig.cs*ファイルには、2要素認証プロバイダーを登録するための次のコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="a04b8-211">2FA の電話番号を追加する</span><span class="sxs-lookup"><span data-stu-id="a04b8-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="a04b8-212">`Manage` コントローラーの `AddPhoneNumber` アクションメソッドは、セキュリティトークンを生成し、指定した電話番号に送信します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="a04b8-213">トークンを送信した後、`VerifyPhoneNumber` アクションメソッドにリダイレクトされます。このメソッドでは、2FA に SMS を登録するためのコードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="a04b8-214">SMS 2FA は、電話番号を確認するまで使用されません。</span><span class="sxs-lookup"><span data-stu-id="a04b8-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="a04b8-215">2FA を有効にする</span><span class="sxs-lookup"><span data-stu-id="a04b8-215">Enabling 2FA</span></span>

<span data-ttu-id="a04b8-216">`EnableTFA` アクションメソッドを使用すると、2FA が有効になります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="a04b8-217">[2FA を有効にする] がセキュリティプロファイルに変更されているため、`SignInAsync` を呼び出す必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a04b8-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="a04b8-218">2FA が有効になっている場合、ユーザーは、登録されている2FA アプローチ (サンプルでは SMS と電子メール) を使用して、ログインに2FA を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="a04b8-219">QR コードジェネレーターなど、さらに2FA プロバイダーを追加することも、独自に作成することもできます (「 [ASP.NET Identity で Google Authenticator を使用](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)する」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="a04b8-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="a04b8-220">2FA コードは、[時間ベースのワンタイムパスワードアルゴリズム](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)を使用して生成され、コードは6分間有効です。</span><span class="sxs-lookup"><span data-stu-id="a04b8-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="a04b8-221">コードを入力するのに6分以上かかる場合は、無効なコードエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="a04b8-222">ソーシャルおよびローカルログインアカウントの結合</span><span class="sxs-lookup"><span data-stu-id="a04b8-222">Combine social and local login accounts</span></span>

<span data-ttu-id="a04b8-223">電子メールリンクをクリックして、ローカルアカウントとソーシャルアカウントを組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="a04b8-224">次の順序で &quot;RickAndMSFT@gmail.com&quot; は最初にローカルログインとして作成されますが、最初にアカウントをソーシャルログとして作成してから、ローカルログインを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="a04b8-225">**[管理]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-225">Click on the **Manage** link.</span></span> <span data-ttu-id="a04b8-226">このアカウントに関連付けられている0外部 (ソーシャルログイン) に注意してください。</span><span class="sxs-lookup"><span data-stu-id="a04b8-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="a04b8-227">別のログインサービスへのリンクをクリックし、アプリの要求を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="a04b8-228">2つのアカウントが結合されているので、いずれかのアカウントでログオンすることができます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="a04b8-229">認証サービスのソーシャルログがダウンした場合、またはソーシャルアカウントへのアクセスが失われる可能性がある場合に備えて、ユーザーにローカルアカウントを追加することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="a04b8-230">次の図では、Tom はソーシャルログ (ページに表示されている**外部ログイン: 1**から参照できます) です。</span><span class="sxs-lookup"><span data-stu-id="a04b8-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="a04b8-231">**[パスワードの選択]** をクリックすると、同じアカウントに関連付けられているローカルログオンを追加できます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="a04b8-232">ブルートフォース攻撃からのアカウントロックアウト</span><span class="sxs-lookup"><span data-stu-id="a04b8-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="a04b8-233">ユーザーロックアウトを有効にすることによって、アプリケーションのアカウントを辞書攻撃から保護することができます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="a04b8-234">`ApplicationUserManager Create` メソッドの次のコードは、ロックアウトを構成します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="a04b8-235">上記のコードでは、2要素認証のロックアウトのみが有効になっています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="a04b8-236">アカウントコントローラーの `Login` 方法で `shouldLockout` を true に変更することで、ログインのロックアウトを有効にすることができますが、ログインのロックアウトを有効にしないことをお勧めします。これは、アカウントが[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)ログイン攻撃の影響を受けやすくなるためです。</span><span class="sxs-lookup"><span data-stu-id="a04b8-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="a04b8-237">このサンプルコードでは、`ApplicationDbInitializer Seed` メソッドで作成された管理者アカウントのロックアウトが無効になっています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="a04b8-238">検証済みの電子メールアカウントをユーザーに要求する</span><span class="sxs-lookup"><span data-stu-id="a04b8-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="a04b8-239">次のコードでは、ユーザーがログインする前に、検証済みの電子メールアカウントを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="a04b8-240">SignInManager が2FA 要件を確認する方法</span><span class="sxs-lookup"><span data-stu-id="a04b8-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="a04b8-241">ローカルログインとソーシャルログの両方で、2FA が有効になっているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="a04b8-242">2FA が有効になっている場合、`SignInManager` ログオンメソッドは `SignInStatus.RequiresVerification`を返し、ユーザーは `SendCode` アクションメソッドにリダイレクトされます。このメソッドでは、ログインシーケンスを完了するためにコードを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="a04b8-243">ユーザーがユーザーのローカルクッキーに対して RememberMe が設定されている場合、`SignInManager` は `SignInStatus.Success` を返し、2FA を通過する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a04b8-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="a04b8-244">次のコードは、`SendCode` アクションメソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="a04b8-245">[Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)は、ユーザーに対して有効になっているすべての2fa メソッドを使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="a04b8-246">[Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)は[DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper に渡されます。これにより、ユーザーは2fa アプローチ (通常は電子メールと SMS) を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="a04b8-247">ユーザーが2FA アプローチを投稿すると、`HTTP POST SendCode` アクションメソッドが呼び出され、`SignInManager` は2FA コードを送信します。ユーザーは `VerifyCode` アクションメソッドにリダイレクトされ、ユーザーはログインを完了するコードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="a04b8-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="a04b8-248">2FA ロックアウト</span><span class="sxs-lookup"><span data-stu-id="a04b8-248">2FA Lockout</span></span>

<span data-ttu-id="a04b8-249">ログインパスワードの試行に失敗したときにアカウントのロックアウトを設定することはできますが、この方法を使用すると、ログインが[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)ロックアウトの影響を受けやすくなります。</span><span class="sxs-lookup"><span data-stu-id="a04b8-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="a04b8-250">アカウントロックアウトは、2FA でのみ使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a04b8-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="a04b8-251">`ApplicationUserManager` が作成されると、サンプルコードは2FA のロックアウトと `MaxFailedAccessAttemptsBeforeLockout` を5に設定します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="a04b8-252">ユーザーがローカルアカウントまたはソーシャルアカウントを使用してログインすると、2FA に失敗した各試行が保存されます。最大試行回数に達すると、ユーザーは5分間ロックアウトされます (ロックアウト時間は `DefaultAccountLockoutTimeSpan`で設定できます)。</span><span class="sxs-lookup"><span data-stu-id="a04b8-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="a04b8-253">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="a04b8-253">Additional Resources</span></span>

- <span data-ttu-id="a04b8-254">[推奨されるリソースの ASP.NET Identity](../getting-started/aspnet-identity-recommended-resources.md)Id ブログ、ビデオ、チュートリアル、および優れたリンクの一覧が完成しました。</span><span class="sxs-lookup"><span data-stu-id="a04b8-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="a04b8-255">[Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリで](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)は、ユーザーテーブルにプロファイル情報を追加する方法についても説明しています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="a04b8-256">[ASP.NET MVC And Identity 2.0: John の基本を理解](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)しています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="a04b8-257">ASP.NET Identity を使用したアカウントの確認とパスワードの回復</span><span class="sxs-lookup"><span data-stu-id="a04b8-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="a04b8-258">ASP.NET Identity 入門</span><span class="sxs-lookup"><span data-stu-id="a04b8-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="a04b8-259">Pranav Rastogi による[ASP.NET Identity 2.0.0 の RTM を発表](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="a04b8-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="a04b8-260">[ASP.NET Identity 2.0: 加藤さんがアカウントの検証と2要素認証を設定](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)しています。</span><span class="sxs-lookup"><span data-stu-id="a04b8-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
