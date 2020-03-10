---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: ASP.NET Web ページ (Razor) サイトのサイト全体の動作をカスタマイズする |Microsoft Docs
author: Rick-Anderson
description: この章では、ページだけではなく、web サイト全体またはフォルダー全体に対して設定を行う方法について説明します。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515248"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a><span data-ttu-id="5bd46-103">ASP.NET Web ページ (Razor) サイトのサイト全体の動作のカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="5bd46-103">Customizing Site-Wide Behavior for ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="5bd46-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5bd46-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5bd46-105">この記事では、ASP.NET Web ページ (Razor) web サイトのページに対してサイト側の設定を行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-105">This article explains how to make site-side settings for pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="5bd46-106">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="5bd46-107">サイト内のすべてのページに対して値 (グローバル値またはヘルパー設定) を設定できるコードを実行する方法。</span><span class="sxs-lookup"><span data-stu-id="5bd46-107">How to run code that lets you set values (global values or helper settings) for all pages in a site.</span></span>
> - <span data-ttu-id="5bd46-108">フォルダー内のすべてのページの値を設定できるコードを実行する方法。</span><span class="sxs-lookup"><span data-stu-id="5bd46-108">How to run code that lets you set values for all pages in a folder.</span></span>
> - <span data-ttu-id="5bd46-109">ページが読み込まれる前と後にコードを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-109">How to run code before and after a page loads.</span></span>
> - <span data-ttu-id="5bd46-110">中央のエラーページにエラーを送信する方法。</span><span class="sxs-lookup"><span data-stu-id="5bd46-110">How to send errors to a central error page.</span></span>
> - <span data-ttu-id="5bd46-111">フォルダー内のすべてのページに認証を追加する方法</span><span class="sxs-lookup"><span data-stu-id="5bd46-111">How to add authentication to all pages in a folder.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5bd46-112">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="5bd46-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5bd46-113">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="5bd46-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="5bd46-114">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="5bd46-114">WebMatrix 3</span></span>
> - <span data-ttu-id="5bd46-115">ASP.NET Web ヘルパーライブラリ (NuGet パッケージ)</span><span class="sxs-lookup"><span data-stu-id="5bd46-115">ASP.NET Web Helpers Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="5bd46-116">このチュートリアルでは、ASP.NET Web ヘルパーライブラリを使用できない点を除いて、ASP.NET Web ページ3と Visual Studio 2013 (または Web 用の Visual Studio Express 2013) でも動作します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-116">This tutorial also works with ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web), except you cannot use the ASP.NET Web Helpers Library.</span></span>

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a><span data-ttu-id="5bd46-117">ASP.NET Web ページの Web サイトのスタートアップコードを追加する</span><span class="sxs-lookup"><span data-stu-id="5bd46-117">Adding Website Startup Code for ASP.NET Web Pages</span></span>

<span data-ttu-id="5bd46-118">ASP.NET Web ページに記述するコードの大部分では、そのページに必要なすべてのコードを個別のページに含めることができます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-118">For much of the code that you write in ASP.NET Web Pages, an individual page can contain all the code that's required for that page.</span></span> <span data-ttu-id="5bd46-119">たとえば、ページが電子メールメッセージを送信する場合、その操作のすべてのコードを1ページにまとめることができます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-119">For example, if a page sends an email message, it's possible to put all the code for that operation in a single page.</span></span> <span data-ttu-id="5bd46-120">これには、電子メールの送信 (SMTP サーバーの場合) および電子メールメッセージの送信の設定を初期化するコードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-120">This can include the code to initialize the settings for sending email (that is, for the SMTP server) and for sending the email message.</span></span>

<span data-ttu-id="5bd46-121">ただし、状況によっては、サイトのページが実行される前にコードを実行することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-121">However, in some situations, you might want to run some code before any page on the site runs.</span></span> <span data-ttu-id="5bd46-122">これは、サイト内の任意の場所 (*グローバル値*と呼ばれます) で使用できる値を設定する場合に便利です。たとえば、一部のヘルパーでは、電子メールの設定やアカウントキーなどの値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-122">This is useful for setting values that can be used anywhere in the site (referred to as *global values*.) For example, some helpers require you to provide values like email settings or account keys.</span></span> <span data-ttu-id="5bd46-123">これらの設定をグローバル値に保持すると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-123">It can be handy to keep these settings in global values.</span></span>

<span data-ttu-id="5bd46-124">これを行うには、サイトのルートに *\_該当*という名前のページを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-124">You can do this by creating a page named *\_AppStart.cshtml* in the root of the site.</span></span> <span data-ttu-id="5bd46-125">このページが存在する場合は、サイトのページが最初に要求されたときに実行されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-125">If this page exists, it runs the first time any page in the site is requested.</span></span> <span data-ttu-id="5bd46-126">そのため、グローバル値を設定するコードを実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5bd46-126">Therefore, it's a good place to run code to set global values.</span></span> <span data-ttu-id="5bd46-127">( *\_該当*にはアンダースコアプレフィックスが付いているため、ユーザーが直接要求した場合でも、ASP.NET はページをブラウザーに送信しません。)</span><span class="sxs-lookup"><span data-stu-id="5bd46-127">(Because *\_AppStart.cshtml* has an underscore prefix, ASP.NET won't send the page to a browser even if users request it directly.)</span></span>

<span data-ttu-id="5bd46-128">次の図は、 *\_該当*ページの動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="5bd46-128">The following diagram shows how the *\_AppStart.cshtml* page works.</span></span> <span data-ttu-id="5bd46-129">ページに対して要求が送信され、それがサイト内のいずれかのページの最初の要求である場合、ASP.NET は最初に、 *\_該当*ページが存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-129">When a request comes in for a page, and if this is the first request for any page in the site, ASP.NET first checks whether a *\_AppStart.cshtml* page exists.</span></span> <span data-ttu-id="5bd46-130">その場合は、 *\_該当*ページ内のすべてのコードが実行され、要求されたページが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-130">If so, any code in the *\_AppStart.cshtml* page runs, and then the requested page runs.</span></span>

![[画像]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a><span data-ttu-id="5bd46-132">Web サイトのグローバル値を設定する</span><span class="sxs-lookup"><span data-stu-id="5bd46-132">Setting Global Values for Your Website</span></span>

1. <span data-ttu-id="5bd46-133">WebMatrix web サイトのルートフォルダーに、 *\_該当*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-133">In the root folder of a WebMatrix website, create a file named *\_AppStart.cshtml*.</span></span> <span data-ttu-id="5bd46-134">ファイルは、サイトのルートにある必要があります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-134">The file must be in the root of the site.</span></span>
2. <span data-ttu-id="5bd46-135">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-135">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    <span data-ttu-id="5bd46-136">このコードは `AppState` ディクショナリに値を格納します。このディクショナリは、サイト内のすべてのページで自動的に使用できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-136">This code stores a value in the `AppState` dictionary, which is automatically available to all pages in the site.</span></span> <span data-ttu-id="5bd46-137">*\_該当*ファイルにマークアップがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5bd46-137">Notice that the *\_AppStart.cshtml* file does not have any markup in it.</span></span> <span data-ttu-id="5bd46-138">このページでコードが実行され、最初に要求されたページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-138">The page will run the code and then redirect to the page that was originally requested.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5bd46-139">*\_該当*ファイルにコードを配置する場合は注意してください。</span><span class="sxs-lookup"><span data-stu-id="5bd46-139">Be careful when you put code in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="5bd46-140">*\_該当*ファイルのコードでエラーが発生した場合、web サイトは開始されません。</span><span class="sxs-lookup"><span data-stu-id="5bd46-140">If any errors occur in code in the *\_AppStart.cshtml* file, the website won't start.</span></span>
3. <span data-ttu-id="5bd46-141">ルートフォルダーに、 *AppName. cshtml*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-141">In the root folder, create a new page named *AppName.cshtml*.</span></span>
4. <span data-ttu-id="5bd46-142">既定のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-142">Replace the default markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    <span data-ttu-id="5bd46-143">このコードは、 *\_該当*ページで設定した `AppState` オブジェクトから値を抽出します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-143">This code extracts the value from the `AppState` object that you set in the *\_AppStart.cshtml* page.</span></span>
5. <span data-ttu-id="5bd46-144">ブラウザーで*AppName*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-144">Run the *AppName.cshtml* page in a browser.</span></span> <span data-ttu-id="5bd46-145">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。ページにグローバル値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-145">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays the global value.</span></span> 

    ![[画像]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a><span data-ttu-id="5bd46-147">ヘルパーの値の設定</span><span class="sxs-lookup"><span data-stu-id="5bd46-147">Setting Values for Helpers</span></span>

<span data-ttu-id="5bd46-148">*\_該当*ファイルは、サイトで使用するヘルパーの値を設定し、初期化することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5bd46-148">A good use for the *\_AppStart.cshtml* file is to set values for helpers that you use in your site and that have to be initialized.</span></span> <span data-ttu-id="5bd46-149">一般的な例としては、`WebMail` ヘルパーの電子メール設定と、`ReCaptcha` ヘルパーの秘密キーと公開キーがあります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-149">Typical examples are email settings for the `WebMail` helper and the private and public keys for the `ReCaptcha` helper.</span></span> <span data-ttu-id="5bd46-150">このような場合は、 *\_該当*で値を1回設定すると、サイト内のすべてのページに対して既に設定されています。</span><span class="sxs-lookup"><span data-stu-id="5bd46-150">In cases like these, you can set the values once in the *\_AppStart.cshtml* and then they're already set for all the pages in your site.</span></span>

<span data-ttu-id="5bd46-151">この手順では、`WebMail` 設定をグローバルに設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-151">This procedure shows you how to set `WebMail` settings globally.</span></span> <span data-ttu-id="5bd46-152">(`WebMail` ヘルパーの使用方法の詳細については、「 [ASP.NET Web ページサイトへの電子メールの追加](../getting-started/11-adding-email-to-your-web-site.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="5bd46-152">(For more information about using the `WebMail` helper, see [Adding Email to an ASP.NET Web Pages Site](../getting-started/11-adding-email-to-your-web-site.md).)</span></span>

1. <span data-ttu-id="5bd46-153">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。</span><span class="sxs-lookup"><span data-stu-id="5bd46-153">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="5bd46-154">*\_該当*ファイルをまだ持っていない場合は、web サイトのルートフォルダーに *\_該当*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-154">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
3. <span data-ttu-id="5bd46-155">次の `WebMail` 設定を *\_該当*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-155">Add the following `WebMail` settings to the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    <span data-ttu-id="5bd46-156">コード内の次の電子メール関連の設定を変更します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-156">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="5bd46-157">`your-SMTP-host` に、アクセス権のある SMTP サーバーの名前を設定します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-157">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="5bd46-158">`your-user-name-here` を、SMTP サーバーアカウントのユーザー名に設定します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-158">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="5bd46-159">`your-account-password` を SMTP サーバーアカウントのパスワードに設定します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-159">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="5bd46-160">`your-email-address-here` を独自の電子メールアドレスに設定します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-160">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="5bd46-161">これは、メッセージの送信元の電子メールアドレスです。</span><span class="sxs-lookup"><span data-stu-id="5bd46-161">This is the email address that the message is sent from.</span></span> <span data-ttu-id="5bd46-162">(一部の電子メールプロバイダーでは、別の `From` アドレスを指定することはできず、`From` アドレスとしてユーザー名が使用されます)。</span><span class="sxs-lookup"><span data-stu-id="5bd46-162">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     <span data-ttu-id="5bd46-163">SMTP 設定の詳細については、「 [ASP.NET Web ページ (razor) トラブルシューティングガイド](https://go.microsoft.com/fwlink/?LinkId=253001)」の「 [ASP.NET Web ページ (razor) サイトから](https://go.microsoft.com/fwlink/?LinkID=202899)電子メールを送信する」と「電子[メールの送信に関する問題](https://go.microsoft.com/fwlink/?LinkId=253001#email)」の「電子メール[設定の構成](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5bd46-163">For more information about SMTP settings, see [Configuring Email Settings](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) in the article [Sending Email from an ASP.NET Web Pages (Razor) Site](https://go.microsoft.com/fwlink/?LinkID=202899) and [Issues with Sending Email](https://go.microsoft.com/fwlink/?LinkId=253001#email) in the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>
4. <span data-ttu-id="5bd46-164">*\_該当*ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-164">Save the *\_AppStart.cshtml* file and close it.</span></span>
5. <span data-ttu-id="5bd46-165">Web サイトのルートフォルダーに、 *Testemail. cshtml*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-165">In the root folder of a website, create new page named *TestEmail.cshtml*.</span></span>
6. <span data-ttu-id="5bd46-166">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-166">Replace the existing content with the following:</span></span> 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. <span data-ttu-id="5bd46-167">ブラウザーで*Testemail. cshtml*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-167">Run the *TestEmail.cshtml* page in a browser.</span></span>
8. <span data-ttu-id="5bd46-168">フィールドに電子メールメッセージを送信するように入力し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5bd46-168">Fill in the fields to send yourself an email message and then click **Send**.</span></span>
9. <span data-ttu-id="5bd46-169">メールを確認して、メッセージが表示されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="5bd46-169">Check your email to make sure you've gotten the message.</span></span>

<span data-ttu-id="5bd46-170">この例の重要な部分は、通常は変更しない設定 (SMTP サーバーの名前や電子メールの資格情報など) が *\_該当*ファイルに設定されていることです。</span><span class="sxs-lookup"><span data-stu-id="5bd46-170">The important part of this example is that the settings that you don't usually change — like the name of your SMTP server and your email credentials — are set in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="5bd46-171">このようにして、電子メールを送信する各ページで再度設定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5bd46-171">That way you don't need to set them again in each page where you send email.</span></span> <span data-ttu-id="5bd46-172">(何らかの理由で、これらの設定を変更する必要がある場合は、ページで個別に設定できます)。このページでは、通常、電子メールメッセージの受信者や本文など、毎回変更される値のみを設定します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-172">(Although if for some reason you need to change those settings, you can set them individually in a page.) In the page, you only set the values that typically change each time, like the recipient and the body of the email message.</span></span>

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a><span data-ttu-id="5bd46-173">フォルダー内のファイルの前後にコードを実行する</span><span class="sxs-lookup"><span data-stu-id="5bd46-173">Running Code Before and After Files in a Folder</span></span>

<span data-ttu-id="5bd46-174">*\_該当*を使用して、サイト内のページの前にコードを記述するのと同様に、特定のフォルダー内の任意のページが実行される前 (および後) に実行されるコードを記述することができます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-174">Just like you can use *\_AppStart.cshtml* to write code before pages in the site run, you can write code that runs before (and after) any page in a particular folder run.</span></span> <span data-ttu-id="5bd46-175">これは、フォルダー内のすべてのページに対して同じレイアウトページを設定する場合や、フォルダー内のページを実行する前にユーザーがログインしていることを確認する場合などに便利です。</span><span class="sxs-lookup"><span data-stu-id="5bd46-175">This is useful for things like setting the same layout page for all the pages in a folder, or for checking that a user is logged in before running a page in the folder.</span></span>

<span data-ttu-id="5bd46-176">特定のフォルダーのページでは、 *\_PageStart. cshtml*という名前のファイルにコードを作成できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-176">For pages in particular folders, you can create code in a file named *\_PageStart.cshtml*.</span></span> <span data-ttu-id="5bd46-177">次の図は、 *\_PageStart. cshtml*ページがどのように動作するかを示しています。</span><span class="sxs-lookup"><span data-stu-id="5bd46-177">The following diagram shows how the *\_PageStart.cshtml* page works.</span></span> <span data-ttu-id="5bd46-178">ページに対して要求が送信されると、ASP.NET は最初に、 *\_該当*ページを確認し、それを実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-178">When a request comes in for a page, ASP.NET first checks for a *\_AppStart.cshtml* page and runs that.</span></span> <span data-ttu-id="5bd46-179">次に、ASP.NET ページがあるか *\_* どうかを確認し、存在する場合はそれを実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-179">Then ASP.NET checks whether there's a *\_PageStart.cshtml* page, and if so, runs that.</span></span> <span data-ttu-id="5bd46-180">次に、要求されたページを実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-180">It then runs the requested page.</span></span>

<span data-ttu-id="5bd46-181">*\_PageStart. cshtml*ページ内で、`RunPage` メソッドを含めることで、要求されたページの実行を処理する場所を指定できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-181">Inside the *\_PageStart.cshtml* page, you can specify where during processing you want the requested page to run by including a `RunPage` method.</span></span> <span data-ttu-id="5bd46-182">これにより、要求されたページが実行される前にコードを実行してから、後で再度実行できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-182">This lets you run code before the requested page runs and then again after it.</span></span> <span data-ttu-id="5bd46-183">`RunPage`を指定しない場合は、 *\_pagestart*すべてのコードが実行され、要求されたページが自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-183">If you don't include `RunPage`, all the code in *\_PageStart.cshtml* runs, and then the requested page runs automatically.</span></span>

![[画像]](18-customizing-site-wide-behavior/_static/image3.jpg)

<span data-ttu-id="5bd46-185">ASP.NET を使用すると *\_PageStart. cshtml*ファイルの階層を作成できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-185">ASP.NET lets you create a hierarchy of *\_PageStart.cshtml* files.</span></span> <span data-ttu-id="5bd46-186">サイトのルートと任意のサブフォルダーに、 *\_PageStart. cshtml*ファイルを配置できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-186">You can put a *\_PageStart.cshtml* file in the root of the site and in any subfolder.</span></span> <span data-ttu-id="5bd46-187">ページが要求されると、最上位レベル (サイトルートに最も近い) の *\_PageStart. cshtml*ファイルが実行され、その後、次のサブフォルダーにある *\_pagestart. cshtml*ファイルが実行されます。その後、要求されたページを含むフォルダーに要求が到達するまで、サブフォルダーの構造が下になります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-187">When a page is requested, the *\_PageStart.cshtml* file at the top-most level (nearest to the site root) runs, followed by the *\_PageStart.cshtml* file in the next subfolder, and so on down the subfolder structure until the request reaches the folder that contains the requested page.</span></span> <span data-ttu-id="5bd46-188">適用可能なすべての *\_PageStart. cshtml*ファイルが実行されると、要求されたページが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-188">After all the applicable *\_PageStart.cshtml* files have run, the requested page runs.</span></span>

<span data-ttu-id="5bd46-189">たとえば、次のような *\_PageStart. cshtml*ファイルと*既定の cshtml*ファイルの組み合わせがあるとします。</span><span class="sxs-lookup"><span data-stu-id="5bd46-189">For example, you might have the following combination of *\_PageStart.cshtml* files and *Default.cshtml* file:</span></span>

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

<span data-ttu-id="5bd46-190">*/Myfolderを*実行すると、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-190">When you run */myfolder/default.cshtml*, you'll see the following:</span></span>

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a><span data-ttu-id="5bd46-191">フォルダー内のすべてのページに対して初期化コードを実行する</span><span class="sxs-lookup"><span data-stu-id="5bd46-191">Running Initialization Code for All Pages in a Folder</span></span>

<span data-ttu-id="5bd46-192">*PageStart. cshtml*ファイルを\_には、1つのフォルダー内のすべてのファイルに対して同じレイアウトページを初期化することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5bd46-192">A good use for *\_PageStart.cshtml* files is to initialize the same layout page for all files in a single folder.</span></span>

1. <span data-ttu-id="5bd46-193">ルートフォルダーに、 *Initpages*という名前の新しいフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-193">In the root folder, create a new folder named *InitPages*.</span></span>
2. <span data-ttu-id="5bd46-194">Web サイトの*Initpages*フォルダーで、 *\_pagestart. cshtml*という名前のファイルを作成し、既定のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-194">In the *InitPages* folder of your website, create a file named *\_PageStart.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. <span data-ttu-id="5bd46-195">Web サイトのルートで、 *Shared*という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-195">In the root of the website, create a folder named *Shared*.</span></span>
4. <span data-ttu-id="5bd46-196">*共有*フォルダーで *\_Layout1*という名前のファイルを作成し、既定のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-196">In the *Shared* folder, create a file named *\_Layout1.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. <span data-ttu-id="5bd46-197">*Initpages*フォルダーで、 *Content1*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-197">In the *InitPages* folder, create a file named *Content1.cshtml* and replace the existing content with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. <span data-ttu-id="5bd46-198">*Initpages*フォルダーで、 *Content2*という名前の別のファイルを作成し、既定のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-198">In the *InitPages* folder, create another file named *Content2.cshtml* and replace the default markup with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. <span data-ttu-id="5bd46-199">ブラウザーで*Content1*を実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-199">Run *Content1.cshtml* in a browser.</span></span> 

    ![[画像]](18-customizing-site-wide-behavior/_static/image4.jpg)

    <span data-ttu-id="5bd46-201">*Content1*ページを実行すると、 *\_pagestart. cshtml*ファイルが `Layout` 設定され、`PageData["MyBackground"]` も色に設定されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-201">When the *Content1.cshtml* page runs, the *\_PageStart.cshtml* file sets `Layout` and also sets `PageData["MyBackground"]` to a color.</span></span> <span data-ttu-id="5bd46-202">*Content1*では、レイアウトと色が適用されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-202">In *Content1.cshtml*, the layout and color are applied.</span></span>
8. <span data-ttu-id="5bd46-203">ブラウザーで*Content2*を表示します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-203">Display *Content2.cshtml* in a browser.</span></span> 

    <span data-ttu-id="5bd46-204">レイアウトは同じです。どちらのページも、 *\_PageStart. cshtml*で初期化されたのと同じレイアウトページと色を使用するためです。</span><span class="sxs-lookup"><span data-stu-id="5bd46-204">The layout is the same, because both pages use the same layout page and color as initialized in *\_PageStart.cshtml*.</span></span>

## <a name="using-_pagestartcshtml-to-handle-errors"></a><span data-ttu-id="5bd46-205">\_PageStart. cshtml を使用してエラーを処理する</span><span class="sxs-lookup"><span data-stu-id="5bd46-205">Using \_PageStart.cshtml to Handle Errors</span></span>

<span data-ttu-id="5bd46-206">*\_PageStart. cshtml*ファイルのもう1つの使用方法は、フォルダー内の任意の*cshtml*ページで発生する可能性があるプログラミングエラー (例外) を処理する方法を作成することです。</span><span class="sxs-lookup"><span data-stu-id="5bd46-206">Another good use for the *\_PageStart.cshtml* file is to create a way to handle programming errors (exceptions) that might occur in any *.cshtml* page in a folder.</span></span> <span data-ttu-id="5bd46-207">この例では、これを行う1つの方法を示します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-207">This example shows you one way to do this.</span></span>

1. <span data-ttu-id="5bd46-208">ルートフォルダーに、 *Initcatch*という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-208">In the root folder, create a folder named *InitCatch*.</span></span>
2. <span data-ttu-id="5bd46-209">Web サイトの*Initcatch*フォルダーで、 *\_pagestart. cshtml*という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-209">In the *InitCatch* folder of your website, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    <span data-ttu-id="5bd46-210">このコードでは、`try` ブロック内で `RunPage` メソッドを呼び出すことによって、要求されたページを明示的に実行しようとしています。</span><span class="sxs-lookup"><span data-stu-id="5bd46-210">In this code, you try running the requested page explicitly by calling the `RunPage` method inside a `try` block.</span></span> <span data-ttu-id="5bd46-211">要求されたページで何らかのプログラミングエラーが発生した場合は、`catch` ブロック内のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-211">If any programming errors occur in the requested page, the code inside the `catch` block runs.</span></span> <span data-ttu-id="5bd46-212">この場合、コードはページ (*エラー cshtml*) にリダイレクトし、URL の一部としてエラーが発生したファイルの名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-212">In this case, the code redirects to a page (*Error.cshtml*) and passes the name of the file that experienced the error as part of the URL.</span></span> <span data-ttu-id="5bd46-213">(ページはすぐに作成します)。</span><span class="sxs-lookup"><span data-stu-id="5bd46-213">(You'll create the page shortly.)</span></span>
3. <span data-ttu-id="5bd46-214">Web サイトの*Initcatch*フォルダーで、 *Exception. cshtml*という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-214">In the *InitCatch* folder of your website, create a file named *Exception.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    <span data-ttu-id="5bd46-215">この例では、このページで行っていることは、存在しないデータベースファイルを開こうとすると意図的にエラーになります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-215">For purposes of this example, what you're doing in this page is deliberately creating an error by trying to open a database file that doesn't exist.</span></span>
4. <span data-ttu-id="5bd46-216">ルートフォルダーで、「 *Error. cshtml* 」という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-216">In the root folder, create a file named *Error.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    <span data-ttu-id="5bd46-217">このページでは、式 `@Request["source"]` が URL から値を取得して表示します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-217">In this page, the expression `@Request["source"]` gets the value out of the URL and displays it.</span></span>
5. <span data-ttu-id="5bd46-218">ツールバーの **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5bd46-218">In the toolbar, click **Save**.</span></span>
6. <span data-ttu-id="5bd46-219">ブラウザーで*例外を*実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-219">Run *Exception.cshtml* in a browser.</span></span> 

    ![[画像]](18-customizing-site-wide-behavior/_static/image5.jpg)

    <span data-ttu-id="5bd46-221">*例外*が発生したため、 *\_pagestart. Cshtml*ページが*エラーの cshtml*ファイルにリダイレクトされ、メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-221">Because an error occurs in *Exception.cshtml*, the *\_PageStart.cshtml* page redirects to the *Error.cshtml* file, which displays the message.</span></span>

    <span data-ttu-id="5bd46-222">例外の詳細については、「 [Razor 構文を使用した ASP.NET Web ページプログラミングの概要](https://go.microsoft.com/fwlink/?LinkID=251587)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5bd46-222">For more information about exceptions, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587).</span></span>

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a><span data-ttu-id="5bd46-223">\_PageStart. cshtml を使用してフォルダーアクセスを制限する</span><span class="sxs-lookup"><span data-stu-id="5bd46-223">Using \_PageStart.cshtml to Restrict Folder Access</span></span>

<span data-ttu-id="5bd46-224">また、 *\_PageStart. cshtml*ファイルを使用して、フォルダー内のすべてのファイルへのアクセスを制限することもできます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-224">You can also use the *\_PageStart.cshtml* file to restrict access to all the files in a folder.</span></span>

1. <span data-ttu-id="5bd46-225">WebMatrix で、 **[テンプレートからのサイト]** オプションを使用して新しい web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-225">In WebMatrix, create a new website using the **Site From Template** option.</span></span>
2. <span data-ttu-id="5bd46-226">使用可能なテンプレートから、 **[スターターサイト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-226">From the available templates, select **Starter Site**.</span></span>
3. <span data-ttu-id="5bd46-227">ルートフォルダーに、認証*Atedcontent*という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-227">In the root folder, create a folder named *AuthenticatedContent*.</span></span>
4. <span data-ttu-id="5bd46-228">[認証*Atedcontent* ] フォルダーで、 *\_pagestart. cshtml*という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-228">In the *AuthenticatedContent* folder, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    <span data-ttu-id="5bd46-229">このコードは、フォルダー内のすべてのファイルがキャッシュされるのを防ぐことから始まります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-229">The code starts by preventing all files in the folder from being cached.</span></span> <span data-ttu-id="5bd46-230">(これは、パブリックコンピューターのようなシナリオで、1人のユーザーのキャッシュされたページを次のユーザーが使用できないようにする場合に必要です)。次に、ユーザーがフォルダー内のページを表示する前に、サイトにサインインしているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-230">(This is required for scenarios like public computers, where you don't want one user's cached pages to be available to the next user.) Next, the code determines whether the user has signed in to the site before they can view any of the pages in the folder.</span></span> <span data-ttu-id="5bd46-231">ユーザーがサインインしていない場合、コードはログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-231">If the user is not signed in, the code redirects to the login page.</span></span> <span data-ttu-id="5bd46-232">ログインページでは、`ReturnUrl`という名前のクエリ文字列値を指定した場合に、最初に要求されたページにユーザーを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-232">The login page can return the user to the page that was originally requested if you include a query string value named `ReturnUrl`.</span></span>
5. <span data-ttu-id="5bd46-233">"/" という名前の認証の*コンテンツ*フォルダーに新しいページを作成*します。*</span><span class="sxs-lookup"><span data-stu-id="5bd46-233">Create a new page in the *AuthenticatedContent* folder named *Page.cshtml*.</span></span>
6. <span data-ttu-id="5bd46-234">既定のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-234">Replace the default markup with the following:</span></span>  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. <span data-ttu-id="5bd46-235">ブラウザーで、[ *Cshtml]* を実行します。</span><span class="sxs-lookup"><span data-stu-id="5bd46-235">Run *Page.cshtml* in a browser.</span></span> <span data-ttu-id="5bd46-236">このコードにより、ログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-236">The code redirects you to a login page.</span></span> <span data-ttu-id="5bd46-237">ログインする前に登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5bd46-237">You must register before logging in.</span></span> <span data-ttu-id="5bd46-238">登録してログインすると、ページに移動してその内容を表示できます。</span><span class="sxs-lookup"><span data-stu-id="5bd46-238">After you've registered and logged in, you can navigate to the page and view its contents.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="5bd46-239">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="5bd46-239">Additional Resources</span></span>

[<span data-ttu-id="5bd46-240">Razor 構文を使用した ASP.NET Web ページプログラミングの概要</span><span class="sxs-lookup"><span data-stu-id="5bd46-240">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
