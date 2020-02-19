---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS と電子メール2要素認証を使用した ASP.NET MVC 5 アプリ |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、2要素認証を使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。 「Secure ASP.NET MVC 5 web アプリの作成」を完了する必要があります。
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457597"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="2a028-104">SMS や電子メールで 2 要素認証する ASP.NET MVC 5 アプリ</span><span class="sxs-lookup"><span data-stu-id="2a028-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>

<span data-ttu-id="2a028-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2a028-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="2a028-106">このチュートリアルでは、2要素認証を使用して ASP.NET MVC 5 web アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2a028-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="2a028-107">続行する前に[、「ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する」](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)を完了しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a028-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="2a028-108">完成したアプリケーションは[こちら](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="2a028-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="2a028-109">ダウンロードには、電子メールまたは SMS プロバイダーを設定せずに電子メールの確認と SMS をテストできるデバッグヘルパーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2a028-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="2a028-110">このチュートリアルは、 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ) によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="2a028-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

- [<span data-ttu-id="2a028-111">ASP.NET MVC アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2a028-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="2a028-112">2要素認証用に SMS を設定する</span><span class="sxs-lookup"><span data-stu-id="2a028-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="2a028-113">2要素認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="2a028-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="2a028-114">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="2a028-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="2a028-115">ASP.NET MVC アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2a028-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="2a028-116">まず、Web または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013 を](https://go.microsoft.com/fwlink/?LinkId=299058)インストールして実行します。</span><span class="sxs-lookup"><span data-stu-id="2a028-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="2a028-117">[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="2a028-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="2a028-118">警告: 続行する前に[、「ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する」](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)を完了しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a028-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="2a028-119">このチュートリアルを完了するには、 [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)以降をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a028-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="2a028-120">新しい ASP.NET Web プロジェクトを作成し、MVC テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="2a028-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="2a028-121">Web フォームでも ASP.NET Identity がサポートされているため、web フォームアプリで同様の手順に従うことができます。</span><span class="sxs-lookup"><span data-stu-id="2a028-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="2a028-122">既定の認証は、**個々のユーザーアカウント**として残しておきます。</span><span class="sxs-lookup"><span data-stu-id="2a028-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="2a028-123">Azure でアプリをホストする場合は、チェックボックスをオンのままにします。</span><span class="sxs-lookup"><span data-stu-id="2a028-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="2a028-124">このチュートリアルの後半では、Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="2a028-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="2a028-125">[Azure アカウントは無料で開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)ことができます。</span><span class="sxs-lookup"><span data-stu-id="2a028-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="2a028-126">[SSL を使用するようにプロジェクトを](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)設定します。</span><span class="sxs-lookup"><span data-stu-id="2a028-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="2a028-127">2要素認証用に SMS を設定する</span><span class="sxs-lookup"><span data-stu-id="2a028-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="2a028-128">このチュートリアルでは、Twilio または ASPSMS を使用する手順について説明しますが、他の SMS プロバイダーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2a028-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="2a028-129">**SMS プロバイダーを使用したユーザーアカウントの作成**</span><span class="sxs-lookup"><span data-stu-id="2a028-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="2a028-130">[Twilio](https://www.twilio.com/try-twilio)または[aspsms](https://www.aspsms.com/asp.net/identity/testcredits/)アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="2a028-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="2a028-131">**追加のパッケージのインストール、またはサービス参照の追加**</span><span class="sxs-lookup"><span data-stu-id="2a028-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="2a028-132">Twilio</span><span class="sxs-lookup"><span data-stu-id="2a028-132">Twilio:</span></span>  
   <span data-ttu-id="2a028-133">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="2a028-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="2a028-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="2a028-134">ASPSMS:</span></span>  
   <span data-ttu-id="2a028-135">次のサービス参照を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a028-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="2a028-136">住所 :</span><span class="sxs-lookup"><span data-stu-id="2a028-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="2a028-137">名前空間:</span><span class="sxs-lookup"><span data-stu-id="2a028-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="2a028-138">**SMS プロバイダーのユーザー資格情報の確認**</span><span class="sxs-lookup"><span data-stu-id="2a028-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="2a028-139">Twilio</span><span class="sxs-lookup"><span data-stu-id="2a028-139">Twilio:</span></span>  
   <span data-ttu-id="2a028-140">Twilio アカウントの **[ダッシュボード]** タブで、**アカウント SID**と**認証トークン**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="2a028-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="2a028-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="2a028-141">ASPSMS:</span></span>  
   <span data-ttu-id="2a028-142">アカウント設定から、**ユーザーキー**に移動し、自己定義**パスワード**と共にコピーします。</span><span class="sxs-lookup"><span data-stu-id="2a028-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="2a028-143">これらの値は、後で `"SMSAccountIdentification"` および `"SMSAccountPassword"` キー*内の web.config ファイルに*格納されます。</span><span class="sxs-lookup"><span data-stu-id="2a028-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="2a028-144">**SenderID/オリジネータの指定**</span><span class="sxs-lookup"><span data-stu-id="2a028-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="2a028-145">Twilio</span><span class="sxs-lookup"><span data-stu-id="2a028-145">Twilio:</span></span>  
   <span data-ttu-id="2a028-146">**[数値]** タブで、Twilio 電話番号をコピーします。</span><span class="sxs-lookup"><span data-stu-id="2a028-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="2a028-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="2a028-147">ASPSMS:</span></span>  
   <span data-ttu-id="2a028-148">[発信元の**ロック解除**] メニュー内で、1つ以上の発信者をロック解除するか、英数字の発信者を選択します (すべてのネットワークでサポートされていません)。</span><span class="sxs-lookup"><span data-stu-id="2a028-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="2a028-149">この値は、後でキー `"SMSAccountFrom"`*内の web.config ファイルに*格納されます。</span><span class="sxs-lookup"><span data-stu-id="2a028-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="2a028-150">**SMS プロバイダーの資格情報をアプリに転送する**</span><span class="sxs-lookup"><span data-stu-id="2a028-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="2a028-151">資格情報と送信者の電話番号をアプリで使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2a028-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="2a028-152">単純にするために、これらの値を web.config*ファイルに*格納します。</span><span class="sxs-lookup"><span data-stu-id="2a028-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="2a028-153">Azure にデプロイするときに、web サイトの構成 タブの **アプリの設定** セクションに値を安全に格納できます。</span><span class="sxs-lookup"><span data-stu-id="2a028-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="2a028-154">セキュリティ-機密データをソースコードに格納しません。</span><span class="sxs-lookup"><span data-stu-id="2a028-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="2a028-155">このサンプルを単純にするために、アカウントと資格情報が上記のコードに追加されています。</span><span class="sxs-lookup"><span data-stu-id="2a028-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="2a028-156">[ASP.NET と Azure にパスワードやその他の機密データをデプロイするためのベストプラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2a028-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="2a028-157">**SMS プロバイダーへのデータ転送の実装**</span><span class="sxs-lookup"><span data-stu-id="2a028-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="2a028-158">*アプリ\_Start\IdentityConfig.cs*ファイルで `SmsService` クラスを構成します。</span><span class="sxs-lookup"><span data-stu-id="2a028-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="2a028-159">使用する SMS プロバイダーに応じて、 **Twilio**または**aspsms**セクションのいずれかをアクティブにします。</span><span class="sxs-lookup"><span data-stu-id="2a028-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="2a028-160">*Views\Manage\Index.cshtml* Razor ビューを更新します。 (注: 終了しているコードのコメントを削除するだけではなく、次のコードを使用してください)。</span><span class="sxs-lookup"><span data-stu-id="2a028-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="2a028-161">`ManageController` 内の `EnableTwoFactorAuthentication` および `DisableTwoFactorAuthentication` アクションメソッドに[[Validateアンチ Forgerytoken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)属性があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2a028-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="2a028-162">アプリを実行し、前に登録したアカウントでログインします。</span><span class="sxs-lookup"><span data-stu-id="2a028-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="2a028-163">ユーザー ID をクリックすると、`Manage` コントローラーで `Index` アクションメソッドがアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="2a028-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="2a028-164">[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2a028-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="2a028-165">`AddPhoneNumber` アクションメソッドには、SMS メッセージを受信できる電話番号を入力するためのダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a028-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="2a028-166">数秒で、確認コードを含むテキストメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a028-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="2a028-167">それを入力し、 **[Submit]** を押します。</span><span class="sxs-lookup"><span data-stu-id="2a028-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="2a028-168">[管理] ビューには、電話番号が追加されたことが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a028-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="2a028-169">2 要素認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2a028-169">Enable two-factor authentication</span></span>

<span data-ttu-id="2a028-170">テンプレートで生成されたアプリでは、UI を使用して2要素認証 (2FA) を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a028-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="2a028-171">2FA を有効にするには、ナビゲーションバーでユーザー ID (電子メールエイリアス) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2a028-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="2a028-172">[2FA を有効にする] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2a028-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="2a028-173">ログアウトしてから再度ログインします。</span><span class="sxs-lookup"><span data-stu-id="2a028-173">Logout, then log back in.</span></span> <span data-ttu-id="2a028-174">電子メールを有効にした場合 ([前のチュートリアル](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)を参照)、2FA の SMS または電子メールを選択できます。</span><span class="sxs-lookup"><span data-stu-id="2a028-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="2a028-175">[コードの確認] ページが表示され、(SMS または電子メールから) コードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="2a028-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="2a028-176">[**このブラウザーを記憶**する] チェックボックスをオンにすると、チェックボックスをオンにしたブラウザーとデバイスを使用するときに、2fa を使用してログインする必要がありません。</span><span class="sxs-lookup"><span data-stu-id="2a028-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="2a028-177">悪意のあるユーザーがデバイスにアクセスできない限り、2FA を有効にし、[**このブラウザーを記憶**する] をオンにすると、信頼されていないデバイスからのすべてのアクセスに対して強力な2fa 保護を維持しながら、便利なワンステップパスワードアクセスが提供されます。</span><span class="sxs-lookup"><span data-stu-id="2a028-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="2a028-178">これは、定期的に使用するプライベートあらゆるデバイスで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2a028-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="2a028-179">このチュートリアルでは、新しい ASP.NET MVC アプリで2FA を有効にする方法について簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="2a028-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="2a028-180">このチュートリアルでは、 [SMS と電子メールを使用した2要素認証](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)について、サンプルの背後にあるコードについて詳しく説明します。 ASP.NET Identity。</span><span class="sxs-lookup"><span data-stu-id="2a028-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="2a028-181">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="2a028-181">Additional Resources</span></span>

- <span data-ttu-id="2a028-182">[SMS と電子メールを使用した2要素認証 (ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) )2要素認証の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="2a028-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="2a028-183">推奨されるリソースへのリンク ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="2a028-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="2a028-184">[ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)パスワードの回復とアカウントの確認についてさらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="2a028-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="2a028-185">[Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)このチュートリアルでは、Facebook と Google OAuth 2 認証を使用して ASP.NET MVC 5 アプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2a028-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="2a028-186">また、Id データベースにデータを追加する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="2a028-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="2a028-187">[メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC アプリを Azure Web にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。</span><span class="sxs-lookup"><span data-stu-id="2a028-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="2a028-188">このチュートリアルでは、Azure のデプロイ、ロールを使用してアプリをセキュリティで保護する方法、メンバーシップ API を使用してユーザーとロールを追加する方法、および追加のセキュリティ機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="2a028-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="2a028-189">OAuth 2 用の Google アプリを作成し、そのアプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="2a028-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="2a028-190">Facebook でアプリを作成し、アプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="2a028-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="2a028-191">プロジェクトでの SSL の設定</span><span class="sxs-lookup"><span data-stu-id="2a028-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [<span data-ttu-id="2a028-192">C#と ASP.NET MVC 開発環境を設定する方法</span><span class="sxs-lookup"><span data-stu-id="2a028-192">How to set up your C# and ASP.NET MVC development environment</span></span>](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
