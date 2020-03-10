---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API での認証と承認 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API での認証と承認の概要について説明します。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484420"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="ace4a-103">ASP.NET Web API での認証と承認</span><span class="sxs-lookup"><span data-stu-id="ace4a-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="ace4a-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ace4a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ace4a-105">Web API を作成しましたが、それへのアクセスを制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="ace4a-106">この一連の記事では、承認されていないユーザーから web API をセキュリティで保護するためのオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="ace4a-107">このシリーズでは、認証と承認の両方について説明します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="ace4a-108">*認証*は、ユーザーの id を認識しています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="ace4a-109">たとえば、Alice はユーザー名とパスワードを使用してログインし、サーバーはパスワードを使用して Alice を認証します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="ace4a-110">*承認*は、ユーザーがアクションの実行を許可されているかどうかを判断するためのものです。</span><span class="sxs-lookup"><span data-stu-id="ace4a-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="ace4a-111">たとえば、Alice はリソースを取得するためのアクセス許可を持っていますが、リソースを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="ace4a-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="ace4a-112">このシリーズの最初の記事では、ASP.NET Web API での認証と承認の概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="ace4a-113">その他のトピックでは、Web API の一般的な認証シナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="ace4a-114">このシリーズをレビューし、Rick Anderson、Levi Broderick、Dorrans、Tom Dykstra、Hongmei Ge、David Matson、Daniel Roth、Tim Teebken のお客様のご意見をお寄せいただき、ありがとうございます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="ace4a-115">認証</span><span class="sxs-lookup"><span data-stu-id="ace4a-115">Authentication</span></span>

<span data-ttu-id="ace4a-116">Web API は、ホストで認証が行われることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="ace4a-117">Web ホストの場合、ホストは IIS で、認証に HTTP モジュールを使用します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="ace4a-118">IIS または ASP.NET に組み込まれている認証モジュールのいずれかを使用するようにプロジェクトを構成するか、独自の HTTP モジュールを記述してカスタム認証を実行することができます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="ace4a-119">ホストがユーザーを認証すると、*プリンシパル*が作成されます。これは、コードが実行されているセキュリティコンテキストを表す[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ace4a-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="ace4a-120">ホストは、 **thread.currentprincipal**を設定することによって、プリンシパルを現在のスレッドにアタッチします。</span><span class="sxs-lookup"><span data-stu-id="ace4a-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="ace4a-121">プリンシパルには、ユーザーに関する情報を含む、関連付けられた**id**オブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="ace4a-122">ユーザーが認証されると、 **IsAuthenticated**プロパティは**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="ace4a-123">匿名要求の場合、 **Isauthenticated**は**false**を返します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="ace4a-124">プリンシパルの詳細については、「[ロールベースのセキュリティ](https://msdn.microsoft.com/library/shz8h065.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ace4a-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="ace4a-125">認証用の HTTP メッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="ace4a-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="ace4a-126">認証にはホストを使用するのではなく、 [HTTP メッセージハンドラー](../advanced/http-message-handlers.md)に認証ロジックを配置することができます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="ace4a-127">この場合、メッセージハンドラーは HTTP 要求を調べ、プリンシパルを設定します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="ace4a-128">認証にメッセージハンドラーを使用する必要があるのはいつですか。</span><span class="sxs-lookup"><span data-stu-id="ace4a-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="ace4a-129">いくつかのトレードオフを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="ace4a-130">HTTP モジュールは、ASP.NET パイプラインを経由するすべての要求を認識します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="ace4a-131">メッセージハンドラーには、Web API にルーティングされる要求のみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="ace4a-132">ルートごとのメッセージハンドラーを設定できます。これにより、特定のルートに認証スキームを適用できます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="ace4a-133">HTTP モジュールは IIS に固有のものです。</span><span class="sxs-lookup"><span data-stu-id="ace4a-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="ace4a-134">メッセージハンドラーは、ホストに依存しないため、web ホストと自己ホストの両方で使用できます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="ace4a-135">HTTP モジュールは、IIS のログ記録や監査などに関与します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="ace4a-136">HTTP モジュールは、パイプラインで以前に実行されています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="ace4a-137">メッセージハンドラーで認証を処理する場合、プリンシパルはハンドラーが実行されるまで設定されません。</span><span class="sxs-lookup"><span data-stu-id="ace4a-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="ace4a-138">さらに、応答がメッセージハンドラーから外れると、プリンシパルは前のプリンシパルに戻ります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="ace4a-139">一般に、自己ホストをサポートする必要がない場合は、HTTP モジュールを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ace4a-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="ace4a-140">自己ホストをサポートする必要がある場合は、メッセージハンドラーを検討してください。</span><span class="sxs-lookup"><span data-stu-id="ace4a-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="ace4a-141">プリンシパルの設定</span><span class="sxs-lookup"><span data-stu-id="ace4a-141">Setting the Principal</span></span>

<span data-ttu-id="ace4a-142">アプリケーションでカスタム認証ロジックを実行する場合は、次の2つの場所でプリンシパルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="ace4a-143">**Thread.currentprincipal**。</span><span class="sxs-lookup"><span data-stu-id="ace4a-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="ace4a-144">このプロパティは、.NET でスレッドのプリンシパルを設定するための標準的な方法です。</span><span class="sxs-lookup"><span data-stu-id="ace4a-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="ace4a-145">**HttpContext. Current. User**.</span><span class="sxs-lookup"><span data-stu-id="ace4a-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="ace4a-146">このプロパティは、ASP.NET に固有です。</span><span class="sxs-lookup"><span data-stu-id="ace4a-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="ace4a-147">次のコードは、プリンシパルを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="ace4a-148">Web ホストの場合、両方の場所でプリンシパルを設定する必要があります。そうしないと、セキュリティコンテキストが不整合になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="ace4a-149">ただし、自己ホストの場合、 **HttpContext**は null になります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="ace4a-150">コードがホストに依存しないようにするには、以下に示すように、null を確認してから**HttpContext**に割り当てます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="ace4a-151">承認</span><span class="sxs-lookup"><span data-stu-id="ace4a-151">Authorization</span></span>

<span data-ttu-id="ace4a-152">承認は、後で、コントローラーに近いパイプラインで行われます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="ace4a-153">これにより、リソースへのアクセスを許可するときにより詳細な選択を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="ace4a-154">*承認フィルター*は、コントローラーアクションの前に実行されます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="ace4a-155">要求が承認されていない場合、フィルターはエラー応答を返し、アクションは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="ace4a-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="ace4a-156">コントローラーアクション内では、 **ApiController**プロパティから現在のプリンシパルを取得できます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="ace4a-157">たとえば、ユーザー名に基づいてリソースの一覧をフィルター処理し、そのユーザーに属するリソースのみを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="ace4a-158">[承認] 属性の使用</span><span class="sxs-lookup"><span data-stu-id="ace4a-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="ace4a-159">Web API には、組み込みの承認フィルターである[Authorizeattribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)が用意されています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="ace4a-160">このフィルターは、ユーザーが認証されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="ace4a-161">そうでない場合は、アクションを呼び出さずに HTTP 状態コード 401 (未承認) が返されます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="ace4a-162">フィルターは、グローバルに、コントローラーレベルで、または個々のアクションのレベルで適用できます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="ace4a-163">**グローバル**: すべての Web API コントローラーのアクセスを制限するには、 **authorizeattribute**フィルターをグローバルフィルター一覧に追加します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="ace4a-164">**コントローラー**: 特定のコントローラーへのアクセスを制限するには、フィルターを属性としてコントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="ace4a-165">**アクション**: 特定のアクションに対するアクセスを制限するには、属性をアクションメソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="ace4a-166">または、`[AllowAnonymous]` 属性を使用して、コントローラーを制限し、特定のアクションへの匿名アクセスを許可することもできます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="ace4a-167">次の例では、`Post` メソッドが制限されていますが、`Get` メソッドは匿名アクセスを許可しています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="ace4a-168">前の例では、フィルターを使用して、認証されたユーザーが制限されたメソッドにアクセスすることを許可しています。匿名ユーザーのみが保持されます。特定のユーザーまたは特定のロールのユーザーへのアクセスを制限することもできます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="ace4a-169">Web API コントローラーの**Authorizeattribute**フィルター**は、system.web 名前空間**にあります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="ace4a-170">**System.web 名前空間**には、web API コントローラーと互換性のない mvc コントローラーに似たフィルターがあります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="ace4a-171">カスタム承認フィルター</span><span class="sxs-lookup"><span data-stu-id="ace4a-171">Custom Authorization Filters</span></span>

<span data-ttu-id="ace4a-172">カスタム承認フィルターを作成するには、次のいずれかの型から派生します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="ace4a-173">**Authorizeattribute**。</span><span class="sxs-lookup"><span data-stu-id="ace4a-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="ace4a-174">現在のユーザーとユーザーのロールに基づいて承認ロジックを実行するように、このクラスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="ace4a-175">**Authorizationfilterattribute**。</span><span class="sxs-lookup"><span data-stu-id="ace4a-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="ace4a-176">このクラスを拡張して、現在のユーザーまたはロールに基づいているとは限らない同期承認ロジックを実行します。</span><span class="sxs-lookup"><span data-stu-id="ace4a-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="ace4a-177">**IAuthorizationFilter**。</span><span class="sxs-lookup"><span data-stu-id="ace4a-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="ace4a-178">非同期承認ロジックを実行するには、このインターフェイスを実装します。たとえば、承認ロジックが非同期 i/o またはネットワーク呼び出しを行う場合です。</span><span class="sxs-lookup"><span data-stu-id="ace4a-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="ace4a-179">(認証ロジックが CPU にバインドされている場合は、 **Authorizationfilterattribute**から派生する方が簡単です。これは、非同期メソッドを記述する必要がないためです)。</span><span class="sxs-lookup"><span data-stu-id="ace4a-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="ace4a-180">次の図は、 **Authorizeattribute**クラスのクラス階層を示しています。</span><span class="sxs-lookup"><span data-stu-id="ace4a-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="ace4a-181">コントローラーアクション内の承認</span><span class="sxs-lookup"><span data-stu-id="ace4a-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="ace4a-182">場合によっては、要求の続行を許可しても、プリンシパルに基づいて動作を変更することがあります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="ace4a-183">たとえば、返される情報は、ユーザーのロールによって変わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ace4a-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="ace4a-184">コントローラーメソッド内では、 **ApiController**プロパティから現在のプリンシパルを取得できます。</span><span class="sxs-lookup"><span data-stu-id="ace4a-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
