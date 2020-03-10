---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API の基本認証 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API での基本認証の使用について説明します。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447634"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="1bea3-103">ASP.NET Web API での基本認証</span><span class="sxs-lookup"><span data-stu-id="1bea3-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="1bea3-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1bea3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1bea3-105">基本認証は[、RFC 2617、HTTP 認証 (基本およびダイジェストアクセス認証)](http://www.ietf.org/rfc/rfc2617.txt)で定義されています。</span><span class="sxs-lookup"><span data-stu-id="1bea3-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="1bea3-106">短所</span><span class="sxs-lookup"><span data-stu-id="1bea3-106">Disadvantages</span></span>

- <span data-ttu-id="1bea3-107">ユーザーの資格情報は、要求で送信されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="1bea3-108">資格情報はプレーンテキストとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="1bea3-109">資格情報は、すべての要求と共に送信されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="1bea3-110">ブラウザーセッションを終了する場合を除き、ログアウトすることはできません。</span><span class="sxs-lookup"><span data-stu-id="1bea3-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="1bea3-111">クロスサイト要求偽造 (CSRF) に対して脆弱CSRF 対策が必要です。</span><span class="sxs-lookup"><span data-stu-id="1bea3-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="1bea3-112">長所</span><span class="sxs-lookup"><span data-stu-id="1bea3-112">Advantages</span></span>

- <span data-ttu-id="1bea3-113">インターネット標準。</span><span class="sxs-lookup"><span data-stu-id="1bea3-113">Internet standard.</span></span>
- <span data-ttu-id="1bea3-114">すべての主要なブラウザーでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bea3-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="1bea3-115">比較的単純なプロトコル。</span><span class="sxs-lookup"><span data-stu-id="1bea3-115">Relatively simple protocol.</span></span>

<span data-ttu-id="1bea3-116">基本認証は次のように機能します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="1bea3-117">要求に認証が必要な場合、サーバーは 401 (権限のない) を返します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="1bea3-118">応答には、サーバーが基本認証をサポートしていることを示す、WWW 認証ヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1bea3-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="1bea3-119">クライアントは、承認ヘッダーにクライアント資格情報を使用して別の要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="1bea3-120">資格情報は、base64 でエンコードされた文字列 "name: password" として書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="1bea3-121">資格情報は暗号化されません。</span><span class="sxs-lookup"><span data-stu-id="1bea3-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="1bea3-122">基本認証は、"領域" のコンテキスト内で実行されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="1bea3-123">サーバーには、WWW-認証ヘッダーに領域の名前が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1bea3-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="1bea3-124">ユーザーの資格情報は、その領域内で有効です。</span><span class="sxs-lookup"><span data-stu-id="1bea3-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="1bea3-125">領域の正確なスコープは、サーバーによって定義されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="1bea3-126">たとえば、リソースをパーティション分割するために複数の領域を定義することができます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="1bea3-127">資格情報は暗号化されずに送信されるため、基本認証は HTTPS 経由でのみセキュリティで保護されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="1bea3-128">「 [WEB API での SSL の](working-with-ssl-in-web-api.md)使用」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bea3-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="1bea3-129">基本認証は CSRF 攻撃にも脆弱です。</span><span class="sxs-lookup"><span data-stu-id="1bea3-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="1bea3-130">ユーザーが資格情報を入力すると、ブラウザーは、セッションの間、同じドメインへの後続の要求でそれらを自動的に送信します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="1bea3-131">これには、AJAX 要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-131">This includes AJAX requests.</span></span> <span data-ttu-id="1bea3-132">「[クロスサイト要求偽造 (CSRF) 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bea3-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="1bea3-133">IIS を使用した基本認証</span><span class="sxs-lookup"><span data-stu-id="1bea3-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="1bea3-134">IIS は基本認証をサポートしていますが、注意が必要です。ユーザーは、Windows 資格情報に対して認証されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="1bea3-135">つまり、ユーザーは、サーバーのドメインのアカウントを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bea3-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="1bea3-136">公開された web サイトの場合は、通常、ASP.NET メンバーシッププロバイダーに対して認証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bea3-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="1bea3-137">IIS を使用して基本認証を有効にするには、ASP.NET プロジェクトの web.config で認証モードを "Windows" に設定します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="1bea3-138">このモードでは、IIS は Windows 資格情報を使用して認証を行います。</span><span class="sxs-lookup"><span data-stu-id="1bea3-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="1bea3-139">さらに、IIS で基本認証を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bea3-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="1bea3-140">IIS マネージャーで、[機能ビュー] にアクセスし、[認証] を選択して、基本認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1bea3-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="1bea3-141">Web API プロジェクトで、認証を必要とするコントローラーアクションの `[Authorize]` 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="1bea3-142">クライアントは、要求で Authorization ヘッダーを設定することによって自身を認証します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="1bea3-143">ブラウザークライアントは、この手順を自動的に実行します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="1bea3-144">ブラウザー以外のクライアントは、ヘッダーを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bea3-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="1bea3-145">カスタムメンバーシップを使用した基本認証</span><span class="sxs-lookup"><span data-stu-id="1bea3-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="1bea3-146">前述のように、IIS に組み込まれている基本認証では Windows 資格情報が使用されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="1bea3-147">つまり、ホスティングサーバーでユーザーのアカウントを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bea3-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="1bea3-148">ただし、インターネットアプリケーションの場合、ユーザーアカウントは通常、外部データベースに格納されます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="1bea3-149">次のコードは、基本認証を実行する HTTP モジュールを示しています。</span><span class="sxs-lookup"><span data-stu-id="1bea3-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="1bea3-150">この例のダミーメソッドである `CheckPassword` メソッドを置き換えることで、ASP.NET メンバーシッププロバイダーを簡単にプラグインできます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="1bea3-151">Web API 2 では、HTTP モジュールの代わりに、[認証フィルター](authentication-filters.md)または[OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/index.md)を記述することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1bea3-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="1bea3-152">HTTP モジュールを有効にするには、次の内容を**system.webserver**セクションの web.config ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="1bea3-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="1bea3-153">"自分の Assemblyname" は、アセンブリの名前 ("dll" 拡張を含まない) に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1bea3-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="1bea3-154">フォームや Windows 認証など、他の認証方式を無効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1bea3-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
