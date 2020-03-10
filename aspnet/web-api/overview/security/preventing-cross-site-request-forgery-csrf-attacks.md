---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET MVC でのクロスサイト要求偽造 (CSRF) 攻撃の防止
author: MikeWasson
description: クロスサイト要求偽造 (CSRF) 攻撃と、ASP.NET Web MVC で CSRF メジャーを実装する方法について説明します。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447112"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a><span data-ttu-id="dbce6-103">ASP.NET MVC アプリケーションでのクロスサイト要求偽造 (CSRF) 攻撃の防止</span><span class="sxs-lookup"><span data-stu-id="dbce6-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET MVC Application</span></span>

<span data-ttu-id="dbce6-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dbce6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="dbce6-105">クロスサイト要求偽造 (CSRF) は、悪意のあるサイトが、ユーザーが現在ログインしている脆弱なサイトに要求を送信する攻撃です。</span><span class="sxs-lookup"><span data-stu-id="dbce6-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="dbce6-106">CSRF 攻撃の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="dbce6-107">ユーザーは、フォーム認証を使用して `www.example.com` にログインします。</span><span class="sxs-lookup"><span data-stu-id="dbce6-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="dbce6-108">サーバーは、ユーザーを認証します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-108">The server authenticates the user.</span></span> <span data-ttu-id="dbce6-109">サーバーからの応答には、認証クッキーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dbce6-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="dbce6-110">ログオフしないと、ユーザーは悪意のある web サイトにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="dbce6-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="dbce6-111">この悪意のあるサイトには、次の HTML フォームが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dbce6-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="dbce6-112">フォームアクションは、悪意のあるサイトではなく、脆弱なサイトに投稿されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dbce6-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="dbce6-113">これは、CSRF の "cross-site" の一部です。</span><span class="sxs-lookup"><span data-stu-id="dbce6-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="dbce6-114">ユーザーが [送信] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbce6-114">The user clicks the submit button.</span></span> <span data-ttu-id="dbce6-115">ブラウザーには、要求と共に認証クッキーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="dbce6-116">要求は、ユーザーの認証コンテキストを使用してサーバー上で実行され、認証されたユーザーが実行できるすべての操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="dbce6-117">この例では、ユーザーがフォームボタンをクリックする必要がありますが、悪意のあるページでは、フォームを自動的に送信するスクリプトを簡単に実行できます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="dbce6-118">また、悪意のあるサイトが "https://" 要求を送信できるため、SSL を使用しても CSRF 攻撃を防ぐことはできません。</span><span class="sxs-lookup"><span data-stu-id="dbce6-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="dbce6-119">通常、ブラウザーでは、関連するすべての cookie が送信先の web サイトに送信されるため、認証に cookie を使用する web サイトに対しては CSRF 攻撃を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="dbce6-120">ただし、CSRF 攻撃は cookie を利用することに限定されません。</span><span class="sxs-lookup"><span data-stu-id="dbce6-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="dbce6-121">例えば、ベーシック認証やダイジェスト認証も脆弱です。</span><span class="sxs-lookup"><span data-stu-id="dbce6-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="dbce6-122">ユーザーが基本認証またはダイジェスト認証を使用してログインした後。</span><span class="sxs-lookup"><span data-stu-id="dbce6-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="dbce6-123">ブラウザーは、セッションが終了するまで資格情報を自動的に送信します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="dbce6-124">偽造防止トークン</span><span class="sxs-lookup"><span data-stu-id="dbce6-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="dbce6-125">CSRF 攻撃を防ぐために、ASP.NET MVC では偽造防止トークンを使用します。これは、*要求検証トークン*とも呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="dbce6-126">クライアントは、フォームを含む HTML ページを要求します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="dbce6-127">サーバーには、応答に2つのトークンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dbce6-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="dbce6-128">1つのトークンが cookie として送信されます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-128">One token is sent as a cookie.</span></span> <span data-ttu-id="dbce6-129">もう一方は、非表示のフォームフィールドに配置されます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="dbce6-130">トークンはランダムに生成されるため、敵対者は値を推測できません。</span><span class="sxs-lookup"><span data-stu-id="dbce6-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="dbce6-131">クライアントは、フォームを送信するときに、両方のトークンをサーバーに送り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbce6-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="dbce6-132">クライアントは cookie トークンをクッキーとして送信し、フォームデータ内にフォームトークンを送信します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="dbce6-133">(ブラウザークライアントは、ユーザーがフォームを送信したときに自動的にこれを行います)。</span><span class="sxs-lookup"><span data-stu-id="dbce6-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="dbce6-134">要求に両方のトークンが含まれていない場合、サーバーは要求を拒否します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="dbce6-135">次に、非表示のフォームトークンを持つ HTML フォームの例を示します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="dbce6-136">悪意のあるページでは、同じオリジンのポリシーによってユーザーのトークンを読み取ることができないため、偽造防止トークンが機能します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="dbce6-137">([同じオリジンポリシー](http://www.w3.org/Security/wiki/Same_Origin_Policy)を利用すると、2つの異なるサイトでホストされているドキュメントから互いのコンテンツにアクセスできなくなります。</span><span class="sxs-lookup"><span data-stu-id="dbce6-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="dbce6-138">このため、前の例では、悪意のあるページは example.com に要求を送信できますが、応答を読み取ることはできません)。</span><span class="sxs-lookup"><span data-stu-id="dbce6-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="dbce6-139">CSRF 攻撃を防ぐには、ユーザーがログインした後にブラウザーがサイレントモードで資格情報を送信する認証プロトコルで偽造防止トークンを使用します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="dbce6-140">これには、フォーム認証などの cookie ベースの認証プロトコルや、基本認証やダイジェスト認証などのプロトコルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="dbce6-141">安全でないメソッド (POST、PUT、DELETE) では、偽造防止トークンが必要です。</span><span class="sxs-lookup"><span data-stu-id="dbce6-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="dbce6-142">また、安全なメソッド (GET、HEAD) に副作用がないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="dbce6-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="dbce6-143">さらに、CORS や JSONP などのドメイン間のサポートを有効にすると、GET などの安全なメソッドも CSRF 攻撃に対して脆弱になる可能性があるため、攻撃者は機密データを読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="dbce6-144">ASP.NET MVC の偽造防止トークン</span><span class="sxs-lookup"><span data-stu-id="dbce6-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="dbce6-145">偽造防止トークンを Razor ページに追加するには、 **htmlhelper..........................** :</span><span class="sxs-lookup"><span data-stu-id="dbce6-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="dbce6-146">このメソッドは、隠しフォームフィールドを追加し、cookie トークンも設定します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="dbce6-147">CSRF と AJAX の防止</span><span class="sxs-lookup"><span data-stu-id="dbce6-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="dbce6-148">AJAX 要求は HTML フォーム データではなく JSON データを送信する場合があるため、フォーム トークンは AJAX 要求に対して問題である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="dbce6-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="dbce6-149">1 つの解決策は、カスタム HTTP ヘッダーでトークンを送信することです。</span><span class="sxs-lookup"><span data-stu-id="dbce6-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="dbce6-150">次のコードでは、Razor 構文を使ってトークンを生成した後、AJAX 要求にトークンを追加しています。</span><span class="sxs-lookup"><span data-stu-id="dbce6-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="dbce6-151">トークンは、**偽造防止. GetTokens**を呼び出すことによって、サーバーで生成されます。</span><span class="sxs-lookup"><span data-stu-id="dbce6-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="dbce6-152">要求を処理するときは、要求ヘッダーからトークンを抽出します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="dbce6-153">次に、**偽造**防止の validate メソッドを呼び出してトークンを検証します。</span><span class="sxs-lookup"><span data-stu-id="dbce6-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="dbce6-154">トークンが有効でない場合、 **Validate**メソッドは例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="dbce6-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
