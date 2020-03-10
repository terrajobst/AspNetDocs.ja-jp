---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: CAPTCHA を使用して、ボットが ASP.NET Web Razor を使用しないようにします。Microsoft Docs
author: microsoft
description: この記事では、ReCaptcha (セキュリティ対策) を使用して、自動プログラム (ボット) が ASP.NET Web ページ (Razor) のタスクを実行できないようにする方法について説明します。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440194"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="e0716-103">CAPTCHA を使用して、ボットが ASP.NET Web Razor) サイトを使用しないようにする</span><span class="sxs-lookup"><span data-stu-id="e0716-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="e0716-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e0716-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e0716-105">この記事では、ReCaptcha (セキュリティ対策) を使用して、自動プログラム (ボット) が ASP.NET Web ページ (Razor) web サイトでタスクを実行できないようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e0716-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="e0716-106">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="e0716-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="e0716-107">CAPTCHA テストをサイトに追加する方法。</span><span class="sxs-lookup"><span data-stu-id="e0716-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="e0716-108">この記事で導入された ASP.NET 機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="e0716-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="e0716-109">`ReCaptcha` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="e0716-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="e0716-110">この記事の情報は、ASP.NET Web ページ1.0 と Web ページ2に適用されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="e0716-111">CAPTCHAs について</span><span class="sxs-lookup"><span data-stu-id="e0716-111">About CAPTCHAs</span></span>

<span data-ttu-id="e0716-112">ユーザーがサイトに登録するとき、または名前と URL を入力するだけで (ブログコメントなど)、フェイク名があふれてしまうことがあります。</span><span class="sxs-lookup"><span data-stu-id="e0716-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="e0716-113">これらは、多くの場合、検索可能なすべての web サイトに Url を残しようとする自動プログラム (ボット) によって残されています。</span><span class="sxs-lookup"><span data-stu-id="e0716-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="e0716-114">(一般的な動機は、販売する製品の Url を投稿することです)。</span><span class="sxs-lookup"><span data-stu-id="e0716-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="e0716-115">ユーザーが*CAPTCHA*を使用してユーザーを登録したとき、またはその他の方法で名前とサイトを入力したときにユーザーを検証することで、ユーザーがコンピュータープログラムではないことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="e0716-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="e0716-116">CAPTCHA は、コンピューターや人間を区別するために、完全に自動化されたパブリックチューリングテストを意味します。</span><span class="sxs-lookup"><span data-stu-id="e0716-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="e0716-117">CAPTCHA は*チャレンジ/レスポンス*テストであり、ユーザーは簡単に実行できますが、自動化されたプログラムを実行するのは難しいものです。</span><span class="sxs-lookup"><span data-stu-id="e0716-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="e0716-118">最も一般的な種類の CAPTCHA は、歪んだ文字が表示され、入力を求められるものです。</span><span class="sxs-lookup"><span data-stu-id="e0716-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="e0716-119">(ゆがみは、ボットが文字を解読するのを困難にすることが想定されています)。</span><span class="sxs-lookup"><span data-stu-id="e0716-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="e0716-120">ReCaptcha テストの追加</span><span class="sxs-lookup"><span data-stu-id="e0716-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="e0716-121">ASP.NET ページでは、`ReCaptcha` ヘルパーを使用して、ReCaptcha サービス ([http://recaptcha.net](http://recaptcha.net)) に基づく CAPTCHA テストを表示できます。</span><span class="sxs-lookup"><span data-stu-id="e0716-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="e0716-122">`ReCaptcha` ヘルパーは、ページが検証される前にユーザーが正しく入力する必要がある、2つの歪んだ単語の画像を表示します。</span><span class="sxs-lookup"><span data-stu-id="e0716-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="e0716-123">ユーザーの応答は、ReCaptcha.Net サービスによって検証されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="e0716-124">Web サイトを ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)) に登録します。</span><span class="sxs-lookup"><span data-stu-id="e0716-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="e0716-125">登録が完了すると、公開キーと秘密キーが取得されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="e0716-126">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。</span><span class="sxs-lookup"><span data-stu-id="e0716-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="e0716-127">*\_該当*ファイルをまだ持っていない場合は、web サイトのルートフォルダーに *\_該当*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="e0716-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="e0716-128">*\_該当*ファイルに次の `Recaptcha` helper 設定を追加します。</span><span class="sxs-lookup"><span data-stu-id="e0716-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="e0716-129">独自の公開キーと秘密キーを使用して、`PublicKey` と `PrivateKey` のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="e0716-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="e0716-130">*\_該当*ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="e0716-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="e0716-131">Web サイトのルートフォルダーに、 *Recaptcha*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="e0716-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="e0716-132">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e0716-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="e0716-133">ブラウザーで*Recaptcha*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="e0716-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="e0716-134">`PrivateKey` の値が有効な場合、ページには ReCaptcha コントロールとボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="e0716-135">*\_該当*でグローバルにキーを設定しなかった場合は、ページにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="e0716-136">テスト用の単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="e0716-136">Enter the words for the test.</span></span> <span data-ttu-id="e0716-137">ReCaptcha テストに合格すると、その効果に関するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="e0716-138">それ以外の場合は、エラーメッセージが表示され、ReCaptcha コントロールが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="e0716-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="e0716-139">コンピューターがプロキシサーバーを使用するドメインにある場合*は、web.config ファイルの*`defaultproxy` 要素の構成が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="e0716-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="e0716-140">次の例は、ReCaptcha サービスが機能するように構成された `defaultproxy` 要素を含む*web.config ファイルを*示しています。</span><span class="sxs-lookup"><span data-stu-id="e0716-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="e0716-141">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="e0716-141">Additional Resources</span></span>

- [<span data-ttu-id="e0716-142">ASP.NET Web ページサイトのサイト全体の動作のカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="e0716-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="e0716-143">ReCaptcha サイト</span><span class="sxs-lookup"><span data-stu-id="e0716-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
