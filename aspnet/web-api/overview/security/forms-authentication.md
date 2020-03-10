---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API | のフォーム認証Microsoft Docs
author: MikeWasson
description: ASP.NET Web API でのフォーム認証の使用について説明します。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484378"
---
# <a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="dabde-103">ASP.NET Web API でのフォーム認証</span><span class="sxs-lookup"><span data-stu-id="dabde-103">Forms Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="dabde-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dabde-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="dabde-105">フォーム認証では、HTML フォームを使用してユーザーの資格情報をサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="dabde-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="dabde-106">インターネット標準ではありません。</span><span class="sxs-lookup"><span data-stu-id="dabde-106">It is not an Internet standard.</span></span> <span data-ttu-id="dabde-107">ユーザーが HTML フォームを操作できるように、フォーム認証は web、web アプリケーションから呼び出される API の適切なのみ。</span><span class="sxs-lookup"><span data-stu-id="dabde-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="dabde-108">長所</span><span class="sxs-lookup"><span data-stu-id="dabde-108">Advantages</span></span> | <span data-ttu-id="dabde-109">短所</span><span class="sxs-lookup"><span data-stu-id="dabde-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="dabde-110">-実装が簡単: ASP.NET に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="dabde-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="dabde-111">-ASP.NET メンバーシッププロバイダーを使用します。これにより、ユーザーアカウントの管理が容易になります。</span><span class="sxs-lookup"><span data-stu-id="dabde-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="dabde-112">-標準の HTTP 認証機構ではありません。では、標準の Authorization ヘッダーではなく HTTP クッキーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="dabde-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="dabde-113">-ブラウザークライアントが必要です。</span><span class="sxs-lookup"><span data-stu-id="dabde-113">- Requires a browser client.</span></span> <span data-ttu-id="dabde-114">-資格情報はプレーンテキストとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="dabde-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="dabde-115">-クロスサイト要求偽造 (CSRF) に対して脆弱です。CSRF 対策が必要です。</span><span class="sxs-lookup"><span data-stu-id="dabde-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="dabde-116">-ブラウザー以外のクライアントから使用するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="dabde-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="dabde-117">ログインにはブラウザーが必要です。</span><span class="sxs-lookup"><span data-stu-id="dabde-117">Login requires a browser.</span></span> <span data-ttu-id="dabde-118">-ユーザー資格情報は、要求で送信されます。</span><span class="sxs-lookup"><span data-stu-id="dabde-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="dabde-119">-Cookie を無効にするユーザーもいます。</span><span class="sxs-lookup"><span data-stu-id="dabde-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="dabde-120">について簡単に、ASP.NET フォーム認証は、次のように動作します。</span><span class="sxs-lookup"><span data-stu-id="dabde-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="dabde-121">クライアントは、認証を必要とするリソースを要求します。</span><span class="sxs-lookup"><span data-stu-id="dabde-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="dabde-122">ユーザーが認証されていない場合は、サーバーから HTTP 302 (検出) が返され、ログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="dabde-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="dabde-123">ユーザーは資格情報を入力し、フォームを送信します。</span><span class="sxs-lookup"><span data-stu-id="dabde-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="dabde-124">サーバーは、元の URI にリダイレクトする別の HTTP 302 を返します。</span><span class="sxs-lookup"><span data-stu-id="dabde-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="dabde-125">この応答には、認証クッキーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dabde-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="dabde-126">クライアントはリソースを再度要求します。</span><span class="sxs-lookup"><span data-stu-id="dabde-126">The client requests the resource again.</span></span> <span data-ttu-id="dabde-127">要求に認証クッキーが含まれているため、サーバーは要求を許可します。</span><span class="sxs-lookup"><span data-stu-id="dabde-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="dabde-128">詳細については、「[フォーム認証の概要](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dabde-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="dabde-129">Web API でフォーム認証を使用する</span><span class="sxs-lookup"><span data-stu-id="dabde-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="dabde-130">フォーム認証を使用するアプリケーションを作成するには、MVC 4 プロジェクトウィザードで [インターネットアプリケーション] テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="dabde-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="dabde-131">このテンプレートは、アカウント管理用の MVC コントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="dabde-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="dabde-132">ASP.NET フォール2012更新プログラムで利用可能な "シングルページアプリケーション" テンプレートを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="dabde-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="dabde-133">Web API コントローラーでは、「 [[承認] 属性の使用](authentication-and-authorization-in-aspnet-web-api.md#auth3)」で説明されているように、`[Authorize]` 属性を使用してアクセスを制限できます。</span><span class="sxs-lookup"><span data-stu-id="dabde-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="dabde-134">フォーム認証では、セッション cookie を使用して要求を認証します。</span><span class="sxs-lookup"><span data-stu-id="dabde-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="dabde-135">ブラウザーは、関連するすべての cookie を送信先の web サイトに自動的に送信します。</span><span class="sxs-lookup"><span data-stu-id="dabde-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="dabde-136">この機能により、クロスサイト要求偽造 (CSRF) 攻撃に対してフォーム認証が脆弱になる可能性があります。「[クロスサイト要求偽造 (csrf) 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dabde-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="dabde-137">フォーム認証では、ユーザーの資格情報は暗号化されません。</span><span class="sxs-lookup"><span data-stu-id="dabde-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="dabde-138">そのため、SSL で使用しない限り、フォーム認証は安全ではありません。</span><span class="sxs-lookup"><span data-stu-id="dabde-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="dabde-139">「 [WEB API での SSL の](working-with-ssl-in-web-api.md)使用」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dabde-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
