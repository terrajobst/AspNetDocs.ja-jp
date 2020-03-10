---
uid: web-api/overview/security/individual-accounts-in-web-api
title: ASP.NET Web API 2.2 | で個別のアカウントとローカルログインを使用して Web API をセキュリティで保護するMicrosoft Docs
author: MikeWasson
description: このトピックでは、OAuth2 を使用して web API をセキュリティで保護し、メンバーシップデータベースに対して認証する方法について説明します。 このチュートリアルで使用されているソフトウェアのバージョンは、Visual Studio 201...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447178"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a><span data-ttu-id="15ea6-104">ASP.NET Web API 2.2 で個別のアカウントとローカルログインを使用して Web API をセキュリティで保護する</span><span class="sxs-lookup"><span data-stu-id="15ea6-104">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>

<span data-ttu-id="15ea6-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="15ea6-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="15ea6-106">サンプルアプリのダウンロード</span><span class="sxs-lookup"><span data-stu-id="15ea6-106">Download Sample App</span></span>](https://github.com/MikeWasson/LocalAccountsApp)

> <span data-ttu-id="15ea6-107">このトピックでは、OAuth2 を使用して web API をセキュリティで保護し、メンバーシップデータベースに対して認証する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-107">This topic shows how to secure a web API using OAuth2 to authenticate against a membership database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="15ea6-108">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="15ea6-108">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="15ea6-109">Visual Studio 2013 Update 3</span><span class="sxs-lookup"><span data-stu-id="15ea6-109">Visual Studio 2013 Update 3</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="15ea6-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="15ea6-110">Web API 2.2</span></span>](../releases/whats-new-in-aspnet-web-api-22.md)
> - [<span data-ttu-id="15ea6-111">ASP.NET Identity 2.1</span><span class="sxs-lookup"><span data-stu-id="15ea6-111">ASP.NET Identity 2.1</span></span>](../../../identity/index.md)

<span data-ttu-id="15ea6-112">Visual Studio 2013 の Web API プロジェクトテンプレートでは、次の3つの認証オプションが提供されています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-112">In Visual Studio 2013, the Web API project template gives you three options for authentication:</span></span>

- <span data-ttu-id="15ea6-113">**個々のアカウント。**</span><span class="sxs-lookup"><span data-stu-id="15ea6-113">**Individual accounts.**</span></span> <span data-ttu-id="15ea6-114">アプリはメンバーシップデータベースを使用します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-114">The app uses a membership database.</span></span>
- <span data-ttu-id="15ea6-115">**組織アカウント。**</span><span class="sxs-lookup"><span data-stu-id="15ea6-115">**Organizational accounts.**</span></span> <span data-ttu-id="15ea6-116">ユーザーは、Azure Active Directory、Office 365、またはオンプレミス Active Directory の資格情報でサインインします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-116">Users sign in with their Azure Active Directory, Office 365, or on-premise Active Directory credentials.</span></span>
- <span data-ttu-id="15ea6-117">**Windows 認証。**</span><span class="sxs-lookup"><span data-stu-id="15ea6-117">**Windows authentication.**</span></span> <span data-ttu-id="15ea6-118">このオプションは、イントラネットアプリケーションを対象としており、Windows 認証 IIS モジュールを使用します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-118">This option is intended for Intranet applications, and uses the Windows Authentication IIS module.</span></span>

<span data-ttu-id="15ea6-119">これらのオプションの詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="15ea6-119">For more details about these options, see [Creating ASP.NET Web Projects in Visual Studio 2013](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).</span></span>

<span data-ttu-id="15ea6-120">個々のアカウントは、ユーザーがログインするための2つの方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-120">Individual accounts provide two ways for a user to log in:</span></span>

- <span data-ttu-id="15ea6-121">**ローカルログイン**。</span><span class="sxs-lookup"><span data-stu-id="15ea6-121">**Local login**.</span></span> <span data-ttu-id="15ea6-122">ユーザーは、サイトにユーザー名とパスワードを入力して登録します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-122">The user registers at the site, entering a username and password.</span></span> <span data-ttu-id="15ea6-123">アプリは、メンバーシップデータベースにパスワードハッシュを格納します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-123">The app stores the password hash in the membership database.</span></span> <span data-ttu-id="15ea6-124">ユーザーがログインすると、ASP.NET Identity システムによってパスワードが検証されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-124">When the user logs in, the ASP.NET Identity system verifies the password.</span></span>
- <span data-ttu-id="15ea6-125">**ソーシャルログイン**。</span><span class="sxs-lookup"><span data-stu-id="15ea6-125">**Social login**.</span></span> <span data-ttu-id="15ea6-126">ユーザーは、Facebook、Microsoft、Google などの外部サービスを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-126">The user signs in with an external service, such as Facebook, Microsoft, or Google.</span></span> <span data-ttu-id="15ea6-127">アプリでは、メンバーシップデータベースにユーザーのエントリが作成されますが、資格情報は保存されません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-127">The app still creates an entry for the user in the membership database, but does not store any credentials.</span></span> <span data-ttu-id="15ea6-128">ユーザーは、外部サービスにサインインすることによって認証されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-128">The user authenticates by signing into the external service.</span></span>

<span data-ttu-id="15ea6-129">この記事では、ローカルログインのシナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-129">This article looks at the local login scenario.</span></span> <span data-ttu-id="15ea6-130">ローカルログインとソーシャルログインの両方で、Web API は OAuth2 を使用して要求を認証します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-130">For both local and social login, Web API uses OAuth2 to authenticate requests.</span></span> <span data-ttu-id="15ea6-131">ただし、ローカルとソーシャルのログインでは、資格情報のフローは異なります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-131">However, the credential flows are different for local and social login.</span></span>

<span data-ttu-id="15ea6-132">この記事では、ユーザーがログインし、認証された AJAX 呼び出しを web API に送信できるようにする簡単なアプリについて説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-132">In this article, I'll demonstrate a simple app that lets the user log in and send authenticated AJAX calls to a web API.</span></span> <span data-ttu-id="15ea6-133">サンプルコードは[こちら](https://github.com/MikeWasson/LocalAccountsApp)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-133">You can download the sample code [here](https://github.com/MikeWasson/LocalAccountsApp).</span></span> <span data-ttu-id="15ea6-134">この readme では、Visual Studio でサンプルをゼロから作成する方法について説明しています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-134">The readme describes how to create the sample from scratch in Visual Studio.</span></span>

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

<span data-ttu-id="15ea6-135">サンプルアプリでは、データバインディングにはノックアウトを使用し、AJAX 要求を送信するには jQuery を使用します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-135">The sample app uses Knockout.js for data-binding and jQuery for sending AJAX requests.</span></span> <span data-ttu-id="15ea6-136">ここでは AJAX 呼び出しについて説明します。そのため、この記事では、ノックアウトを知る必要はありません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-136">I'll be focusing on the AJAX calls, so you don't need to know Knockout.js for this article.</span></span>

<span data-ttu-id="15ea6-137">その過程で、次のことについて説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-137">Along the way, I'll describe:</span></span>

- <span data-ttu-id="15ea6-138">クライアント側でアプリが何をしているか。</span><span class="sxs-lookup"><span data-stu-id="15ea6-138">What the app is doing on the client side.</span></span>
- <span data-ttu-id="15ea6-139">サーバーで何が起こっているか。</span><span class="sxs-lookup"><span data-stu-id="15ea6-139">What's happening on the server.</span></span>
- <span data-ttu-id="15ea6-140">中間の HTTP トラフィック。</span><span class="sxs-lookup"><span data-stu-id="15ea6-140">The HTTP traffic in the middle.</span></span>

<span data-ttu-id="15ea6-141">まず、いくつかの OAuth2 用語を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-141">First, we need to define some OAuth2 terminology.</span></span>

- <span data-ttu-id="15ea6-142">*リソース*。</span><span class="sxs-lookup"><span data-stu-id="15ea6-142">*Resource*.</span></span> <span data-ttu-id="15ea6-143">保護できるデータの一部。</span><span class="sxs-lookup"><span data-stu-id="15ea6-143">Some piece of data that can be protected.</span></span>
- <span data-ttu-id="15ea6-144">*リソースサーバー*。</span><span class="sxs-lookup"><span data-stu-id="15ea6-144">*Resource server*.</span></span> <span data-ttu-id="15ea6-145">リソースをホストするサーバー。</span><span class="sxs-lookup"><span data-stu-id="15ea6-145">The server that hosts the resource.</span></span>
- <span data-ttu-id="15ea6-146">*リソース所有者*。</span><span class="sxs-lookup"><span data-stu-id="15ea6-146">*Resource owner*.</span></span> <span data-ttu-id="15ea6-147">リソースへのアクセス許可を付与できるエンティティ。</span><span class="sxs-lookup"><span data-stu-id="15ea6-147">The entity that can grant permission to access a resource.</span></span> <span data-ttu-id="15ea6-148">(通常はユーザーです)。</span><span class="sxs-lookup"><span data-stu-id="15ea6-148">(Typically the user.)</span></span>
- <span data-ttu-id="15ea6-149">*Client*: リソースへのアクセスを必要とするアプリ。</span><span class="sxs-lookup"><span data-stu-id="15ea6-149">*Client*: The app that wants access to the resource.</span></span> <span data-ttu-id="15ea6-150">この記事では、クライアントは web ブラウザーです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-150">In this article, the client is a web browser.</span></span>
- <span data-ttu-id="15ea6-151">*アクセストークン*。</span><span class="sxs-lookup"><span data-stu-id="15ea6-151">*Access token*.</span></span> <span data-ttu-id="15ea6-152">リソースへのアクセスを許可するトークン。</span><span class="sxs-lookup"><span data-stu-id="15ea6-152">A token that grants access to a resource.</span></span>
- <span data-ttu-id="15ea6-153">*ベアラートークン*。</span><span class="sxs-lookup"><span data-stu-id="15ea6-153">*Bearer token*.</span></span> <span data-ttu-id="15ea6-154">任意のユーザーがトークンを使用できるプロパティを持つ、特定の種類のアクセストークン。</span><span class="sxs-lookup"><span data-stu-id="15ea6-154">A particular type of access token, with the property that anyone can use the token.</span></span> <span data-ttu-id="15ea6-155">つまり、クライアントは、ベアラートークンを使用するために暗号化キーまたはその他のシークレットを必要としません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-155">In other words, a client doesn't need a cryptographic key or other secret to use a bearer token.</span></span> <span data-ttu-id="15ea6-156">そのため、ベアラートークンは HTTPS 経由でのみ使用する必要があり、有効期限が比較的短くなっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-156">For that reason, bearer tokens should only be used over a HTTPS, and should have relatively short expiration times.</span></span>
- <span data-ttu-id="15ea6-157">*承認サーバー*。</span><span class="sxs-lookup"><span data-stu-id="15ea6-157">*Authorization server*.</span></span> <span data-ttu-id="15ea6-158">アクセストークンを提供するサーバー。</span><span class="sxs-lookup"><span data-stu-id="15ea6-158">A server that gives out access tokens.</span></span>

<span data-ttu-id="15ea6-159">アプリケーションは、承認サーバーとリソースサーバーの両方として機能することができます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-159">An application can act as both authorization server and resource server.</span></span> <span data-ttu-id="15ea6-160">Web API プロジェクトテンプレートは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="15ea6-160">The Web API project template follows this pattern.</span></span>

## <a name="local-login-credential-flow"></a><span data-ttu-id="15ea6-161">ローカルログイン資格情報のフロー</span><span class="sxs-lookup"><span data-stu-id="15ea6-161">Local Login Credential Flow</span></span>

<span data-ttu-id="15ea6-162">ローカルログインの場合、Web API は OAuth2 で定義されている[リソース所有者のパスワードフロー](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)を使用します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-162">For local login, Web API uses the [resource owner password flow](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) defined in OAuth2.</span></span>

1. <span data-ttu-id="15ea6-163">ユーザーは、クライアントに名前とパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-163">The user enters a name and password into the client.</span></span>
2. <span data-ttu-id="15ea6-164">クライアントは、これらの資格情報を承認サーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-164">The client sends these credentials to the authorization server.</span></span>
3. <span data-ttu-id="15ea6-165">承認サーバーは、資格情報を認証し、アクセストークンを返します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-165">The authorization server authenticates the credentials and returns an access token.</span></span>
4. <span data-ttu-id="15ea6-166">保護されたリソースにアクセスするために、クライアントは、HTTP 要求の Authorization ヘッダーにアクセストークンを含めます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-166">To access a protected resource, the client includes the access token in the Authorization header of the HTTP request.</span></span>

![](individual-accounts-in-web-api/_static/image3.png)

<span data-ttu-id="15ea6-167">Web API プロジェクトテンプレートで**個別のアカウント**を選択すると、プロジェクトには、ユーザーの資格情報を検証してトークンを発行する承認サーバーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-167">When you select **Individual accounts** in the Web API project template, the project includes an authorization server that validates user credentials and issues tokens.</span></span> <span data-ttu-id="15ea6-168">次の図は、Web API コンポーネントと同じ資格情報フローを示しています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-168">The following diagram shows the same credential flow in terms of Web API components.</span></span>

![](individual-accounts-in-web-api/_static/image4.png)

<span data-ttu-id="15ea6-169">このシナリオでは、Web API コントローラーはリソースサーバーとして機能します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-169">In this scenario, Web API controllers act as resource servers.</span></span> <span data-ttu-id="15ea6-170">認証フィルターはアクセストークンを検証し、 **[承認]** 属性はリソースを保護するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-170">An authentication filter validates access tokens, and the **[Authorize]** attribute is used to protect a resource.</span></span> <span data-ttu-id="15ea6-171">コントローラーまたはアクションに **[承認]** 属性がある場合、そのコントローラーまたはアクションに対するすべての要求を認証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-171">When a controller or action has the **[Authorize]** attribute, all requests to that controller or action must be authenticated.</span></span> <span data-ttu-id="15ea6-172">それ以外の場合は、承認が拒否され、Web API は 401 (未承認) エラーを返します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-172">Otherwise, authorization is denied, and Web API returns a 401 (Unauthorized) error.</span></span>

<span data-ttu-id="15ea6-173">承認サーバーと認証フィルターは両方とも、OAuth2 の詳細を処理する[OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)コンポーネントを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-173">The authorization server and the authentication filter both call into an [OWIN middleware](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) component that handles the details of OAuth2.</span></span> <span data-ttu-id="15ea6-174">設計については、このチュートリアルの後半で詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-174">I'll describe the design in more detail later in this tutorial.</span></span>

## <a name="sending-an-unauthorized-request"></a><span data-ttu-id="15ea6-175">承認されていない要求の送信</span><span class="sxs-lookup"><span data-stu-id="15ea6-175">Sending an Unauthorized Request</span></span>

<span data-ttu-id="15ea6-176">まず、アプリを実行し、[API の**呼び出し**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-176">To get started, run the app and click the **Call API** button.</span></span> <span data-ttu-id="15ea6-177">要求が完了すると、 **[結果]** ボックスにエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-177">When the request completes, you should see an error message in the **Result** box.</span></span> <span data-ttu-id="15ea6-178">これは、要求にアクセストークンが含まれていないため、要求が承認されていないためです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-178">That's because the request does not contain an access token, so the request is unauthorized.</span></span>

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

<span data-ttu-id="15ea6-179">**[Api の呼び出し]** ボタンは、Web API コントローラーアクションを呼び出す AJAX 要求を ~/の値に送信します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-179">The **Call API** button sends an AJAX request to ~/api/values, which invokes a Web API controller action.</span></span> <span data-ttu-id="15ea6-180">ここでは、AJAX 要求を送信する JavaScript コードのセクションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-180">Here is the section of JavaScript code that sends the AJAX request.</span></span> <span data-ttu-id="15ea6-181">サンプルアプリでは、すべての JavaScript アプリコードは、スクリプトファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-181">In the sample app, all of the JavaScript app code is located in the Scripts\app.js file.</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

<span data-ttu-id="15ea6-182">ユーザーがログインするまで、ベアラートークンは存在しないため、要求に Authorization ヘッダーはありません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-182">Until the user logs in, there is no bearer token, and therefore no Authorization header in the request.</span></span> <span data-ttu-id="15ea6-183">これにより、要求で401エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-183">This causes the request to return a 401 error.</span></span>

<span data-ttu-id="15ea6-184">HTTP 要求を次に示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-184">Here is the HTTP request.</span></span> <span data-ttu-id="15ea6-185">(私は[Fiddler](http://www.telerik.com/fiddler)を使用して HTTP トラフィックをキャプチャしました)。</span><span class="sxs-lookup"><span data-stu-id="15ea6-185">(I used [Fiddler](http://www.telerik.com/fiddler) to capture the HTTP traffic.)</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

<span data-ttu-id="15ea6-186">HTTP 応答:</span><span class="sxs-lookup"><span data-stu-id="15ea6-186">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

<span data-ttu-id="15ea6-187">応答には、チャレンジがベアラーに設定された Www 認証ヘッダーが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="15ea6-187">Notice that the response includes a Www-Authenticate header with the challenge set to Bearer.</span></span> <span data-ttu-id="15ea6-188">これは、サーバーがベアラートークンを必要とすることを示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-188">That indicates the server expects a bearer token.</span></span>

## <a name="register-a-user"></a><span data-ttu-id="15ea6-189">ユーザーを登録する</span><span class="sxs-lookup"><span data-stu-id="15ea6-189">Register a User</span></span>

<span data-ttu-id="15ea6-190">アプリの **[登録]** セクションで、電子メールとパスワードを入力し、 **[登録]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-190">In the **Register** section of the app, enter an email and password, and click the **Register** button.</span></span>

<span data-ttu-id="15ea6-191">このサンプルでは有効な電子メールアドレスを使用する必要はありませんが、実際のアプリではアドレスが確認されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-191">You don't need to use a valid email address for this sample, but a real app would confirm the address.</span></span> <span data-ttu-id="15ea6-192">(「[ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)」を参照してください)。パスワードには、大文字、小文字、数字、英数字以外の文字を含む "Password1!" のようなものを使用します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-192">(See [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) For the password, use something like "Password1!", with an upper case letter, lower case letter, number, and non-alpha-numeric character.</span></span> <span data-ttu-id="15ea6-193">アプリを単純にするために、クライアント側の検証を省略しました。そのため、パスワード形式に問題がある場合は、400 (Bad Request) エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-193">To keep the app simple, I left out client-side validation, so if there is a problem with the password format, you'll get a 400 (Bad Request) error.</span></span>

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

<span data-ttu-id="15ea6-194">**[登録]** ボタンをクリックすると、POST 要求が ~/api/Account/Register/. に送信されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-194">The **Register** button sends a POST request to ~/api/Account/Register/.</span></span> <span data-ttu-id="15ea6-195">要求本文は、名前とパスワードを保持する JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-195">The request body is a JSON object that holds the name and password.</span></span> <span data-ttu-id="15ea6-196">要求を送信する JavaScript コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-196">Here is the JavaScript code that sends the request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

<span data-ttu-id="15ea6-197">HTTP 要求:</span><span class="sxs-lookup"><span data-stu-id="15ea6-197">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

<span data-ttu-id="15ea6-198">HTTP 応答:</span><span class="sxs-lookup"><span data-stu-id="15ea6-198">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

<span data-ttu-id="15ea6-199">この要求は `AccountController` クラスによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-199">This request is handled by the `AccountController` class.</span></span> <span data-ttu-id="15ea6-200">内部的には、`AccountController` は ASP.NET Identity を使用してメンバーシップデータベースを管理します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-200">Internally, `AccountController` uses ASP.NET Identity to manage the membership database.</span></span>

<span data-ttu-id="15ea6-201">アプリを Visual Studio からローカルで実行する場合、ユーザーアカウントは LocalDB の AspNetUsers テーブルに格納されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-201">If you run the app locally from Visual Studio, user accounts are stored in LocalDB, in the AspNetUsers table.</span></span> <span data-ttu-id="15ea6-202">Visual Studio でテーブルを表示するには、 **[表示]** メニューの **[サーバーエクスプローラー]** をクリックし、 **[データ接続]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-202">To view the tables in Visual Studio, click the **View** menu, select **Server Explorer**, then expand **Data Connections**.</span></span>

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a><span data-ttu-id="15ea6-203">アクセストークンを取得する</span><span class="sxs-lookup"><span data-stu-id="15ea6-203">Get an Access Token</span></span>

<span data-ttu-id="15ea6-204">これまでは OAuth は実行されていませんでしたが、アクセストークンを要求すると、OAuth 承認サーバーが動作していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-204">So far we have not done any OAuth, but now we'll see the OAuth authorization server in action, when we request an access token.</span></span> <span data-ttu-id="15ea6-205">サンプルアプリの **[ログイン]** 領域で、電子メールとパスワードを入力し、 **[ログイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-205">In the **Log In** area of the sample app, enter the email and password and click **Log In**.</span></span>

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

<span data-ttu-id="15ea6-206">**[ログイン]** ボタンをクリックすると、要求がトークンエンドポイントに送信されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-206">The **Log In** button sends a request to the token endpoint.</span></span> <span data-ttu-id="15ea6-207">要求の本文には、次の形式の url エンコードされたデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-207">The body of the request contains the following form-url-encoded data:</span></span>

- <span data-ttu-id="15ea6-208">grant\_type: "password"</span><span class="sxs-lookup"><span data-stu-id="15ea6-208">grant\_type: "password"</span></span>
- <span data-ttu-id="15ea6-209">ユーザー名: ユーザーの電子メール&gt; &lt;</span><span class="sxs-lookup"><span data-stu-id="15ea6-209">username: &lt;the user's email&gt;</span></span>
- <span data-ttu-id="15ea6-210">パスワード: &lt;パスワード&gt;</span><span class="sxs-lookup"><span data-stu-id="15ea6-210">password: &lt;password&gt;</span></span>

<span data-ttu-id="15ea6-211">AJAX 要求を送信する JavaScript コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-211">Here is the JavaScript code that sends the AJAX request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

<span data-ttu-id="15ea6-212">要求が成功した場合、承認サーバーは応答本文にアクセストークンを返します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-212">If the request succeeds, the authorization server returns an access token in the response body.</span></span> <span data-ttu-id="15ea6-213">API に要求を送信するときに、後で使用するために、トークンはセッションストレージに格納されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="15ea6-213">Notice that we store the token in session storage, to use later when sending requests to the API.</span></span> <span data-ttu-id="15ea6-214">一部の認証形式 (cookie ベースの認証など) とは異なり、ブラウザーでは後続の要求にアクセストークンが自動的に含まれません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-214">Unlike some forms of authentication (such as cookie-based authentication), the browser will not automatically include the access token in subsequent requests.</span></span> <span data-ttu-id="15ea6-215">アプリケーションは明示的に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-215">The application must do so explicitly.</span></span> <span data-ttu-id="15ea6-216">[Csrf の脆弱性](preventing-cross-site-request-forgery-csrf-attacks.md)が制限されるため、これは良いことです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-216">That's a good thing, because it limits [CSRF vulnerabilities](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="15ea6-217">HTTP 要求:</span><span class="sxs-lookup"><span data-stu-id="15ea6-217">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

<span data-ttu-id="15ea6-218">要求にユーザーの資格情報が含まれていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-218">You can see that the request contains the user's credentials.</span></span> <span data-ttu-id="15ea6-219">トランスポート層のセキュリティを提供するには、HTTPS を使用する*必要があり*ます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-219">You *must* use HTTPS to provide transport layer security.</span></span>

<span data-ttu-id="15ea6-220">HTTP 応答:</span><span class="sxs-lookup"><span data-stu-id="15ea6-220">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

<span data-ttu-id="15ea6-221">読みやすくするために、JSON をインデントし、アクセストークンを切り詰めました。これは非常に長いです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-221">For readability, I indented the JSON and truncated the access token, which is a quite long.</span></span>

<span data-ttu-id="15ea6-222">`access_token`、`token_type`、および `expires_in` の各プロパティは、OAuth2 仕様によって定義されます。その他のプロパティ (`userName`、`.issued`、および `.expires`) は単なる情報を提供するためのものです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-222">The `access_token`, `token_type`, and `expires_in` properties are defined by the OAuth2 spec. The other properties (`userName`, `.issued`, and `.expires`) are just for informational purposes.</span></span> <span data-ttu-id="15ea6-223">これらの追加のプロパティを追加するコードについては、/Providers/ApplicationOAuthProvider.cs ファイルの `TokenEndpoint` メソッドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="15ea6-223">You can find the code that adds those additional properties in the `TokenEndpoint` method, in the /Providers/ApplicationOAuthProvider.cs file.</span></span>

## <a name="send-an-authenticated-request"></a><span data-ttu-id="15ea6-224">認証済みの要求を送信する</span><span class="sxs-lookup"><span data-stu-id="15ea6-224">Send an Authenticated Request</span></span>

<span data-ttu-id="15ea6-225">ベアラートークンがあるので、API に対して認証された要求を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-225">Now that we have a bearer token, we can make an authenticated request to the API.</span></span> <span data-ttu-id="15ea6-226">これを行うには、要求で Authorization ヘッダーを設定します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-226">This is done by setting the Authorization header in the request.</span></span> <span data-ttu-id="15ea6-227">このことを確認するには、 **[API の呼び出し]** ボタンをもう一度クリックします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-227">Click the **Call API** button again to see this.</span></span>

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

<span data-ttu-id="15ea6-228">HTTP 要求:</span><span class="sxs-lookup"><span data-stu-id="15ea6-228">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

<span data-ttu-id="15ea6-229">HTTP 応答:</span><span class="sxs-lookup"><span data-stu-id="15ea6-229">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a><span data-ttu-id="15ea6-230">ログアウト</span><span class="sxs-lookup"><span data-stu-id="15ea6-230">Log Out</span></span>

<span data-ttu-id="15ea6-231">ブラウザーでは資格情報またはアクセストークンがキャッシュされないため、ログアウトは、セッションストレージからトークンを削除することによって、トークンを "忘れる" だけです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-231">Because the browser does not cache the credentials or the access token, logging out is simply a matter of "forgetting" the token, by removing it from session storage:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a><span data-ttu-id="15ea6-232">個々のアカウントプロジェクトテンプレートについて</span><span class="sxs-lookup"><span data-stu-id="15ea6-232">Understanding the Individual Accounts Project Template</span></span>

<span data-ttu-id="15ea6-233">ASP.NET Web アプリケーションプロジェクトテンプレートで**個別のアカウント**を選択すると、プロジェクトには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-233">When you select **Individual Accounts** in the ASP.NET Web Application project template, the project includes:</span></span>

- <span data-ttu-id="15ea6-234">OAuth2 承認サーバー。</span><span class="sxs-lookup"><span data-stu-id="15ea6-234">An OAuth2 authorization server.</span></span>
- <span data-ttu-id="15ea6-235">ユーザーアカウントを管理するための Web API エンドポイント</span><span class="sxs-lookup"><span data-stu-id="15ea6-235">A Web API endpoint for managing user accounts</span></span>
- <span data-ttu-id="15ea6-236">ユーザーアカウントを格納するための EF モデル。</span><span class="sxs-lookup"><span data-stu-id="15ea6-236">An EF model for storing user accounts.</span></span>

<span data-ttu-id="15ea6-237">これらの機能を実装する主なアプリケーションクラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-237">Here are the main application classes that implement these features:</span></span>

- <span data-ttu-id="15ea6-238">[https://login.microsoftonline.com/consumers/](`AccountController`)</span><span class="sxs-lookup"><span data-stu-id="15ea6-238">`AccountController`.</span></span> <span data-ttu-id="15ea6-239">には、ユーザーアカウントを管理するための Web API エンドポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-239">Provides a Web API endpoint for managing user accounts.</span></span> <span data-ttu-id="15ea6-240">このチュートリアルで使用したのは、`Register` アクションだけです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-240">The `Register` action is the only one that we used in this tutorial.</span></span> <span data-ttu-id="15ea6-241">クラスの他のメソッドは、パスワードのリセット、ソーシャルログイン、およびその他の機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-241">Other methods on the class support password reset, social logins, and other functionality.</span></span>
- <span data-ttu-id="15ea6-242">`ApplicationUser`、/Models/IdentityModels.cs. で定義されています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-242">`ApplicationUser`, defined in /Models/IdentityModels.cs.</span></span> <span data-ttu-id="15ea6-243">このクラスは、メンバーシップデータベース内のユーザーアカウントの EF モデルです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-243">This class is the EF model for user accounts in the membership database.</span></span>
- <span data-ttu-id="15ea6-244">`ApplicationUserManager`、/\_アプリで定義されています。このクラスは、 [Usermanager](https://msdn.microsoft.com/library/dn613290.aspx)から派生し、ユーザーアカウント (新しいユーザーの作成、パスワードの検証など) に対する操作を実行し、データベースへの変更を自動的に保持します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-244">`ApplicationUserManager`, defined in /App\_Start/IdentityConfig.cs This class derives from [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) and performs operations on user accounts, such as creating a new user, verifying passwords, and so forth, and automatically persists changes to the database.</span></span>
- <span data-ttu-id="15ea6-245">[https://login.microsoftonline.com/consumers/](`ApplicationOAuthProvider`)</span><span class="sxs-lookup"><span data-stu-id="15ea6-245">`ApplicationOAuthProvider`.</span></span> <span data-ttu-id="15ea6-246">このオブジェクトは、OWIN ミドルウェアに接続し、ミドルウェアによって発生したイベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-246">This object plugs into the OWIN middleware, and processes events raised by the middleware.</span></span> <span data-ttu-id="15ea6-247">[Oauthauthorizationserverprovider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)から派生します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-247">It derives from [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx).</span></span>

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a><span data-ttu-id="15ea6-248">承認サーバーを構成する</span><span class="sxs-lookup"><span data-stu-id="15ea6-248">Configuring the Authorization Server</span></span>

<span data-ttu-id="15ea6-249">StartupAuth.cs では、次のコードで OAuth2 authorization サーバーを構成します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-249">In StartupAuth.cs, the following code configures the OAuth2 authorization server.</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

<span data-ttu-id="15ea6-250">`TokenEndpointPath` プロパティは、承認サーバーエンドポイントへの URL パスです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-250">The `TokenEndpointPath` property is the URL path to the authorization server endpoint.</span></span> <span data-ttu-id="15ea6-251">これは、アプリがベアラートークンを取得するために使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="15ea6-251">That's the URL that app uses to get the bearer tokens.</span></span>

<span data-ttu-id="15ea6-252">`Provider` プロパティは、OWIN ミドルウェアに接続するプロバイダーを指定し、ミドルウェアによって発生するイベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-252">The `Provider` property specifies a provider that plugs into the OWIN middleware, and processes events raised by the middleware.</span></span>

<span data-ttu-id="15ea6-253">アプリでトークンを取得する場合の基本的なフローを次に示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-253">Here is the basic flow when the app wants to get a token:</span></span>

1. <span data-ttu-id="15ea6-254">アクセストークンを取得するために、アプリは ~/tokenに要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-254">To get an access token, the app sends a request to ~/Token.</span></span>
2. <span data-ttu-id="15ea6-255">OAuth ミドルウェアは、プロバイダーの `GrantResourceOwnerCredentials` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-255">The OAuth middleware calls `GrantResourceOwnerCredentials` on the provider.</span></span>
3. <span data-ttu-id="15ea6-256">プロバイダーは `ApplicationUserManager` を呼び出して資格情報を検証し、クレーム id を作成します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-256">The provider calls the `ApplicationUserManager` to validate the credentials and create a claims identity.</span></span>
4. <span data-ttu-id="15ea6-257">成功した場合は、トークンの生成に使用される認証チケットがプロバイダーによって作成されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-257">If that succeeds, the provider creates an authentication ticket, which is used to generate the token.</span></span>

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

<span data-ttu-id="15ea6-258">OAuth ミドルウェアでは、ユーザーアカウントについて何も知られていません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-258">The OAuth middleware doesn't know anything about the user accounts.</span></span> <span data-ttu-id="15ea6-259">プロバイダーはミドルウェアと ASP.NET Identity 間で通信します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-259">The provider communicates between the middleware and ASP.NET Identity.</span></span> <span data-ttu-id="15ea6-260">承認サーバーの実装の詳細については、「 [OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="15ea6-260">For more information about implementing the authorization server, see [OWIN OAuth 2.0 Authorization Server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).</span></span>

### <a name="configuring-web-api-to-use-bearer-tokens"></a><span data-ttu-id="15ea6-261">ベアラートークンを使用するように Web API を構成する</span><span class="sxs-lookup"><span data-stu-id="15ea6-261">Configuring Web API to use Bearer Tokens</span></span>

<span data-ttu-id="15ea6-262">`WebApiConfig.Register` メソッドでは、次のコードによって Web API パイプラインの認証が設定されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-262">In the `WebApiConfig.Register` method, the following code sets up authentication for the Web API pipeline:</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

<span data-ttu-id="15ea6-263">**Hostauthenticationfilter**クラスは、ベアラートークンを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="15ea6-263">The **HostAuthenticationFilter** class enables authentication using bearer tokens.</span></span>

<span data-ttu-id="15ea6-264">**Config.suppressdefaulthostauthentication**メソッドは、IIS または OWIN ミドルウェアによって、要求が web api パイプラインに到達する前に発生する認証を無視するように web api に指示します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-264">The **SuppressDefaultHostAuthentication** method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span></span> <span data-ttu-id="15ea6-265">そのため、ベアラー トークンを使用する場合にのみ認証するように Web API を制限することができます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-265">That way, we can restrict Web API to authenticate only using bearer tokens.</span></span>

> [!NOTE]
> <span data-ttu-id="15ea6-266">特に、アプリの MVC 部分では、資格情報を cookie に格納するフォーム認証を使用する場合があります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-266">In particular, the MVC portion of your app might use forms authentication, which stores credentials in a cookie.</span></span> <span data-ttu-id="15ea6-267">Cookie ベースの認証では、CSRF 攻撃を防ぐために、偽造防止トークンを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-267">Cookie-based authentication requires the use of anti-forgery tokens, to prevent CSRF attacks.</span></span> <span data-ttu-id="15ea6-268">これは web api の場合に問題になります。これは、web API が偽造防止トークンをクライアントに送信するための便利な方法がないためです。</span><span class="sxs-lookup"><span data-stu-id="15ea6-268">That's a problem for web APIs, because there is no convenient way for the web API to send the anti-forgery token to the client.</span></span> <span data-ttu-id="15ea6-269">(この問題の背景の詳細については、「 [WEB API での CSRF 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください)。**Config.suppressdefaulthostauthentication**を呼び出すと、cookie に格納されている資格情報から Web API が csrf 攻撃に対して脆弱ではないことが保証されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-269">(For more background on this issue, see [Preventing CSRF Attacks in Web API](preventing-cross-site-request-forgery-csrf-attacks.md).) Calling **SuppressDefaultHostAuthentication** ensures that Web API is not vulnerable to CSRF attacks from credentials stored in cookies.</span></span>

<span data-ttu-id="15ea6-270">クライアントが保護されたリソースを要求した場合、Web API パイプラインでは次の処理が行われます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-270">When the client requests a protected resource, here is what happens in the Web API pipeline:</span></span>

1. <span data-ttu-id="15ea6-271">**Hostauthentication**フィルターは、OAuth ミドルウェアを呼び出してトークンを検証します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-271">The **HostAuthentication** filter calls the OAuth middleware to validate the token.</span></span>
2. <span data-ttu-id="15ea6-272">ミドルウェアは、トークンを要求 id に変換します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-272">The middleware converts the token into a claims identity.</span></span>
3. <span data-ttu-id="15ea6-273">この時点で、要求は*認証*されていますが*承認*されていません。</span><span class="sxs-lookup"><span data-stu-id="15ea6-273">At this point, the request is *authenticated* but not *authorized*.</span></span>
4. <span data-ttu-id="15ea6-274">承認フィルターは、要求 id を調べます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-274">The authorization filter examines the claims identity.</span></span> <span data-ttu-id="15ea6-275">要求がそのリソースのユーザーを承認すると、要求は承認されます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-275">If the claims authorize the user for that resource, the request is authorized.</span></span> <span data-ttu-id="15ea6-276">既定では、 **[承認]** 属性は、認証されたすべての要求を承認します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-276">By default, the **[Authorize]** attribute will authorize any request that is authenticated.</span></span> <span data-ttu-id="15ea6-277">ただし、ロールまたは他の要求によって承認することができます。</span><span class="sxs-lookup"><span data-stu-id="15ea6-277">However, you can authorize by role or by other claims.</span></span> <span data-ttu-id="15ea6-278">詳細については、「 [WEB API での認証と承認](authentication-and-authorization-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="15ea6-278">For more information, see [Authentication and Authorization in Web API](authentication-and-authorization-in-aspnet-web-api.md).</span></span>
5. <span data-ttu-id="15ea6-279">前の手順が成功した場合、コントローラーは保護されたリソースを返します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-279">If the previous steps are successful, the controller returns the protected resource.</span></span> <span data-ttu-id="15ea6-280">それ以外の場合、クライアントは 401 (未承認) のエラーを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="15ea6-280">Otherwise, the client receives a 401 (Unauthorized) error.</span></span>

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a><span data-ttu-id="15ea6-281">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="15ea6-281">Additional Resources</span></span>

- [<span data-ttu-id="15ea6-282">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="15ea6-282">ASP.NET Identity</span></span>](../../../identity/index.md)
- <span data-ttu-id="15ea6-283">[VS2013 RC 用の SPA テンプレートのセキュリティ機能について](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)説明します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-283">[Understanding Security Features in the SPA Template for VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx).</span></span> <span data-ttu-id="15ea6-284">Hongye Sun による MSDN ブログ投稿。</span><span class="sxs-lookup"><span data-stu-id="15ea6-284">MSDN blog post by Hongye Sun.</span></span>
- <span data-ttu-id="15ea6-285">[WEB API の個々のアカウントテンプレートを解説する–パート 2: ローカルアカウント](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。</span><span class="sxs-lookup"><span data-stu-id="15ea6-285">[Dissecting the Web API Individual Accounts Template–Part 2: Local Accounts](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/).</span></span> <span data-ttu-id="15ea6-286">Dominick Baier によるブログ投稿。</span><span class="sxs-lookup"><span data-stu-id="15ea6-286">Blog post by Dominick Baier.</span></span>
- <span data-ttu-id="15ea6-287">[OWIN で認証と WEB API をホスト](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)します。</span><span class="sxs-lookup"><span data-stu-id="15ea6-287">[Host authentication and Web API with OWIN](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/).</span></span> <span data-ttu-id="15ea6-288">Brock Allen による `SuppressDefaultHostAuthentication` と `HostAuthenticationFilter` についてのよくある説明です。</span><span class="sxs-lookup"><span data-stu-id="15ea6-288">A good explanation of `SuppressDefaultHostAuthentication` and `HostAuthenticationFilter` by Brock Allen.</span></span>
- <span data-ttu-id="15ea6-289">[VS 2013 テンプレートでの ASP.NET Identity でのプロファイル情報のカスタマイズ](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15ea6-289">[Customizing profile information in ASP.NET Identity in VS 2013 templates](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx).</span></span> <span data-ttu-id="15ea6-290">Pranav Rastogi による MSDN のブログ投稿。</span><span class="sxs-lookup"><span data-stu-id="15ea6-290">MSDN blog post by Pranav Rastogi.</span></span>
- <span data-ttu-id="15ea6-291">[ASP.NET Identity の UserManager クラスの要求ごとの有効期間管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15ea6-291">[Per request lifetime management for UserManager class in ASP.NET Identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).</span></span> <span data-ttu-id="15ea6-292">Suhas Suhas の MSDN ブログ投稿には、`UserManager` クラスの詳細が掲載されています。</span><span class="sxs-lookup"><span data-stu-id="15ea6-292">MSDN blog post by Suhas Joshi, with a good explanation of the `UserManager` class.</span></span>
