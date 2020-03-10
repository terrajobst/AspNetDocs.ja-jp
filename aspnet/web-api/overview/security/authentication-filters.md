---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 | の認証フィルターMicrosoft Docs
author: MikeWasson
description: 認証フィルターは、HTTP 要求を認証するコンポーネントです。 Web API 2 と MVC 5 はどちらも認証フィルターをサポートしていますが、若干異なります。
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447772"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="b7952-104">ASP.NET Web API 2 の認証フィルター</span><span class="sxs-lookup"><span data-stu-id="b7952-104">Authentication Filters in ASP.NET Web API 2</span></span>

<span data-ttu-id="b7952-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b7952-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b7952-106">認証フィルターは、HTTP 要求を認証するコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="b7952-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="b7952-107">Web API 2 と MVC 5 はどちらも認証フィルターをサポートしていますが、ほとんどの場合、フィルターインターフェイスの名前付け規則によって若干異なります。</span><span class="sxs-lookup"><span data-stu-id="b7952-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="b7952-108">このトピックでは、Web API 認証フィルターについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b7952-108">This topic describes Web API authentication filters.</span></span>

<span data-ttu-id="b7952-109">認証フィルターを使用すると、個々のコントローラーまたはアクションに対して認証スキームを設定できます。</span><span class="sxs-lookup"><span data-stu-id="b7952-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="b7952-110">こうすることで、アプリはさまざまな HTTP リソースに対してさまざまな認証メカニズムをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="b7952-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="b7952-111">この記事では、 [https://github.com/aspnet/samples](https://github.com/aspnet/samples)の[基本的な認証](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)サンプルからのコードを紹介します。</span><span class="sxs-lookup"><span data-stu-id="b7952-111">In this article, I'll show code from the [Basic Authentication](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample on [https://github.com/aspnet/samples](https://github.com/aspnet/samples).</span></span> <span data-ttu-id="b7952-112">このサンプルは、HTTP 基本アクセス認証スキーム (RFC 2617) を実装する認証フィルターを示しています。</span><span class="sxs-lookup"><span data-stu-id="b7952-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="b7952-113">このフィルターは `IdentityBasicAuthenticationAttribute`という名前のクラスに実装されています。</span><span class="sxs-lookup"><span data-stu-id="b7952-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="b7952-114">サンプルのコードをすべて表示するのではなく、認証フィルターを記述する方法を示す部分だけを示します。</span><span class="sxs-lookup"><span data-stu-id="b7952-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="b7952-115">認証フィルターを設定する</span><span class="sxs-lookup"><span data-stu-id="b7952-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="b7952-116">他のフィルターと同様に、認証フィルターはコントローラーごと、アクション単位、またはすべての Web API コントローラーにグローバルに適用できます。</span><span class="sxs-lookup"><span data-stu-id="b7952-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="b7952-117">コントローラーに認証フィルターを適用するには、コントローラークラスを filter 属性で装飾します。</span><span class="sxs-lookup"><span data-stu-id="b7952-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="b7952-118">次のコードは、コントローラークラスの `[IdentityBasicAuthentication]` フィルターを設定します。これにより、コントローラーのすべてのアクションに対して基本認証が有効になります。</span><span class="sxs-lookup"><span data-stu-id="b7952-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="b7952-119">1つのアクションにフィルターを適用するには、フィルターを使用してアクションを装飾します。</span><span class="sxs-lookup"><span data-stu-id="b7952-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="b7952-120">次のコードは、コントローラーの `Post` メソッドの `[IdentityBasicAuthentication]` フィルターを設定します。</span><span class="sxs-lookup"><span data-stu-id="b7952-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="b7952-121">フィルターをすべての Web API コントローラーに適用するには、 **Globalconfiguration. Filters**に追加します。</span><span class="sxs-lookup"><span data-stu-id="b7952-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="b7952-122">Web API 認証フィルターを実装する</span><span class="sxs-lookup"><span data-stu-id="b7952-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="b7952-123">Web API では、認証フィルターによって、 [system.web. Http. フィルター](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)インターフェイスが実装されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="b7952-124">また、属性として適用するために、これら**の属性を system.string から継承**する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="b7952-125">**Iauthenticationfilter**インターフェイスには、次の2つのメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="b7952-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="b7952-126">**AuthenticateAsync**は、要求で資格情報を検証することによって要求を認証します (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="b7952-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="b7952-127">**ChallengeAsync**は、必要に応じて、HTTP 応答に認証チャレンジを追加します。</span><span class="sxs-lookup"><span data-stu-id="b7952-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="b7952-128">これらのメソッドは、 [rfc 2612](http://tools.ietf.org/html/rfc2616)および[rfc 2617](http://tools.ietf.org/html/rfc2617)で定義されている認証フローに対応します。</span><span class="sxs-lookup"><span data-stu-id="b7952-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="b7952-129">クライアントは、Authorization ヘッダーで資格情報を送信します。</span><span class="sxs-lookup"><span data-stu-id="b7952-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="b7952-130">これは通常、クライアントがサーバーから 401 (未承認) の応答を受信した後に発生します。</span><span class="sxs-lookup"><span data-stu-id="b7952-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="b7952-131">ただし、クライアントは、401を取得した直後ではなく、任意の要求で資格情報を送信できます。</span><span class="sxs-lookup"><span data-stu-id="b7952-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="b7952-132">サーバーが資格情報を受け入れない場合は、401 (未承認) の応答を返します。</span><span class="sxs-lookup"><span data-stu-id="b7952-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="b7952-133">応答には、1つまたは複数のチャレンジを含む Www 認証ヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7952-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="b7952-134">各チャレンジは、サーバーで認識される認証スキームを指定します。</span><span class="sxs-lookup"><span data-stu-id="b7952-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="b7952-135">サーバーは、匿名要求から401を返すこともできます。</span><span class="sxs-lookup"><span data-stu-id="b7952-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="b7952-136">実際、これは通常、認証プロセスが開始される方法です。</span><span class="sxs-lookup"><span data-stu-id="b7952-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="b7952-137">クライアントが匿名要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="b7952-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="b7952-138">サーバーは401を返します。</span><span class="sxs-lookup"><span data-stu-id="b7952-138">The server returns 401.</span></span>
3. <span data-ttu-id="b7952-139">クライアントは、資格情報を使用して要求を再送信します。</span><span class="sxs-lookup"><span data-stu-id="b7952-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="b7952-140">このフローには、*認証*と*承認*の両方の手順が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7952-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="b7952-141">認証は、クライアントの id を証明します。</span><span class="sxs-lookup"><span data-stu-id="b7952-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="b7952-142">承認によって、クライアントが特定のリソースにアクセスできるかどうかが決まります。</span><span class="sxs-lookup"><span data-stu-id="b7952-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="b7952-143">Web API では、認証フィルターは認証を処理しますが、承認は処理しません。</span><span class="sxs-lookup"><span data-stu-id="b7952-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="b7952-144">承認は、承認フィルターまたはコントローラーアクション内で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="b7952-145">Web API 2 パイプラインのフローを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b7952-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="b7952-146">アクションを呼び出す前に、Web API によってそのアクションの認証フィルターの一覧が作成されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="b7952-147">これには、アクションスコープ、コントローラースコープ、およびグローバルスコープを含むフィルターが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b7952-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="b7952-148">Web API は、リスト内のすべてのフィルターに対して**AuthenticateAsync**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b7952-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="b7952-149">各フィルターでは、要求で資格情報を検証できます。</span><span class="sxs-lookup"><span data-stu-id="b7952-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="b7952-150">フィルターによって資格情報が正常に検証された場合、フィルターは**IPrincipal**を作成し、要求にアタッチします。</span><span class="sxs-lookup"><span data-stu-id="b7952-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="b7952-151">フィルターでは、この時点でエラーをトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b7952-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="b7952-152">その場合、パイプラインの残りの部分は実行されません。</span><span class="sxs-lookup"><span data-stu-id="b7952-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="b7952-153">エラーがないと仮定すると、要求はパイプラインの残りの部分を通過します。</span><span class="sxs-lookup"><span data-stu-id="b7952-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="b7952-154">最後に、Web API は、すべての認証フィルターの**ChallengeAsync**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b7952-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="b7952-155">フィルターは、必要に応じて、このメソッドを使用して応答にチャレンジを追加します。</span><span class="sxs-lookup"><span data-stu-id="b7952-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="b7952-156">通常は (常にではありませんが)、401エラーに応答して発生します。</span><span class="sxs-lookup"><span data-stu-id="b7952-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="b7952-157">次の図は、考えられる2つのケースを示しています。</span><span class="sxs-lookup"><span data-stu-id="b7952-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="b7952-158">最初の方法では、認証フィルターによって要求が正常に認証され、承認フィルターによって要求が承認され、コントローラーのアクションによって 200 (OK) が返されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="b7952-159">2番目の例では、認証フィルターは要求を認証しますが、承認フィルターは 401 (許可されていません) を返します。</span><span class="sxs-lookup"><span data-stu-id="b7952-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="b7952-160">この場合、コントローラーアクションは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="b7952-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="b7952-161">認証フィルターによって、Www 認証ヘッダーが応答に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="b7952-162">その他の組み合わせも&mdash;可能です。たとえば、コントローラーアクションによって匿名要求が許可されている場合は、認証フィルターを使用できますが、承認はありません。</span><span class="sxs-lookup"><span data-stu-id="b7952-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="b7952-163">AuthenticateAsync メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="b7952-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="b7952-164">**AuthenticateAsync**メソッドは、要求の認証を試みます。</span><span class="sxs-lookup"><span data-stu-id="b7952-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="b7952-165">このメソッド シグネチャを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b7952-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="b7952-166">**AuthenticateAsync**メソッドは、次のいずれかを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="b7952-167">Nothing (no op)。</span><span class="sxs-lookup"><span data-stu-id="b7952-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="b7952-168">**IPrincipal**を作成し、要求に対して設定します。</span><span class="sxs-lookup"><span data-stu-id="b7952-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="b7952-169">エラーの結果を設定します。</span><span class="sxs-lookup"><span data-stu-id="b7952-169">Set an error result.</span></span>

<span data-ttu-id="b7952-170">オプション (1) は、要求に、フィルターによって認識される資格情報がないことを示します。</span><span class="sxs-lookup"><span data-stu-id="b7952-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="b7952-171">オプション (2) は、フィルターが要求を正常に認証したことを意味します。</span><span class="sxs-lookup"><span data-stu-id="b7952-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="b7952-172">オプション (3) は、要求に無効な資格情報 (間違ったパスワードなど) が含まれていることを示します。これにより、エラー応答がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="b7952-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="b7952-173">ここでは、 **AuthenticateAsync**を実装するための一般的な概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="b7952-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="b7952-174">要求で資格情報を探します。</span><span class="sxs-lookup"><span data-stu-id="b7952-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="b7952-175">資格情報がない場合は、何もしないで (no op) が返されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="b7952-176">資格情報があるものの、フィルターで認証スキームが認識されない場合は、何も行わずに (no op) を返します。</span><span class="sxs-lookup"><span data-stu-id="b7952-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="b7952-177">パイプライン内の別のフィルターによって、スキームが認識される場合があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="b7952-178">フィルターによって認識される資格情報がある場合は、認証を試みます。</span><span class="sxs-lookup"><span data-stu-id="b7952-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="b7952-179">資格情報が正しくない場合は、`context.ErrorResult`を設定して401を返します。</span><span class="sxs-lookup"><span data-stu-id="b7952-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="b7952-180">資格情報が有効な場合は、 **IPrincipal**を作成し `context.Principal`を設定します。</span><span class="sxs-lookup"><span data-stu-id="b7952-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="b7952-181">次のコードは、[基本認証](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)サンプルの**AuthenticateAsync**メソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="b7952-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample.</span></span> <span data-ttu-id="b7952-182">コメントは各ステップを示します。</span><span class="sxs-lookup"><span data-stu-id="b7952-182">The comments indicate each step.</span></span> <span data-ttu-id="b7952-183">このコードは、資格情報のない Authorization ヘッダー、不適切な資格情報、および無効なユーザー名/パスワードを使用して、いくつかの種類のエラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="b7952-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="b7952-184">エラー結果の設定</span><span class="sxs-lookup"><span data-stu-id="b7952-184">Setting an Error Result</span></span>

<span data-ttu-id="b7952-185">資格情報が無効である場合、フィルターでは、エラー応答を作成する**Ihttpactionresult**に `context.ErrorResult` を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="b7952-186">**Ihttpactionresult**の詳細については、「 [Web API 2 でのアクションの結果](../getting-started-with-aspnet-web-api/action-results.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b7952-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="b7952-187">基本認証のサンプルには、この目的に適した `AuthenticationFailureResult` クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7952-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="b7952-188">ChallengeAsync の実装</span><span class="sxs-lookup"><span data-stu-id="b7952-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="b7952-189">**ChallengeAsync**メソッドの目的は、必要に応じて、応答に認証チャレンジを追加することです。</span><span class="sxs-lookup"><span data-stu-id="b7952-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="b7952-190">このメソッド シグネチャを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b7952-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="b7952-191">メソッドは、要求パイプラインのすべての認証フィルターで呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="b7952-192">**ChallengeAsync**は、HTTP 応答が作成される*前*と、場合によってはコントローラーアクションが実行される前に呼び出されることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="b7952-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="b7952-193">**ChallengeAsync**が呼び出されると、`context.Result` には**Ihttpactionresult**が含まれます。これは、後で HTTP 応答を作成するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="b7952-194">そのため、 **ChallengeAsync**を呼び出すと、HTTP 応答に関する情報はまだわかりません。</span><span class="sxs-lookup"><span data-stu-id="b7952-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="b7952-195">**ChallengeAsync**メソッドは、`context.Result` の元の値を新しい**Ihttpactionresult**に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="b7952-196">この**Ihttpactionresult**は元の `context.Result`をラップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="b7952-197">元の**Ihttpactionresult**を呼び出すと*内部結果*が生成され、新しい**ihttpactionresult**によって*外部結果*が生成されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="b7952-198">外部結果は、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7952-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="b7952-199">内部結果を呼び出して、HTTP 応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="b7952-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="b7952-200">応答を確認します。</span><span class="sxs-lookup"><span data-stu-id="b7952-200">Examine the response.</span></span>
3. <span data-ttu-id="b7952-201">必要に応じて、認証チャレンジを応答に追加します。</span><span class="sxs-lookup"><span data-stu-id="b7952-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="b7952-202">次の例は、「基本認証のサンプル」から抜粋したものです。</span><span class="sxs-lookup"><span data-stu-id="b7952-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="b7952-203">外部結果の**Ihttpactionresult**を定義します。</span><span class="sxs-lookup"><span data-stu-id="b7952-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="b7952-204">`InnerResult` プロパティは、内部の**Ihttpactionresult**を保持します。</span><span class="sxs-lookup"><span data-stu-id="b7952-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="b7952-205">`Challenge` プロパティは、Www 認証ヘッダーを表します。</span><span class="sxs-lookup"><span data-stu-id="b7952-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="b7952-206">**Executeasync**は、最初に `InnerResult.ExecuteAsync` を呼び出して HTTP 応答を作成し、必要に応じてチャレンジを追加することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b7952-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="b7952-207">チャレンジを追加する前に、応答コードを確認してください。</span><span class="sxs-lookup"><span data-stu-id="b7952-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="b7952-208">次に示すように、ほとんどの認証方式では、応答が401の場合にのみチャレンジが追加されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="b7952-209">ただし、一部の認証方式では、成功応答にチャレンジが追加されます。</span><span class="sxs-lookup"><span data-stu-id="b7952-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="b7952-210">例については、「 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b7952-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="b7952-211">`AddChallengeOnUnauthorizedResult` クラスを指定すると、 **ChallengeAsync**の実際のコードは単純になります。</span><span class="sxs-lookup"><span data-stu-id="b7952-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="b7952-212">結果を作成し `context.Result`にアタッチするだけです。</span><span class="sxs-lookup"><span data-stu-id="b7952-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="b7952-213">注: 基本認証のサンプルでは、このロジックを拡張メソッドに配置することによって、このロジックを抽象化します。</span><span class="sxs-lookup"><span data-stu-id="b7952-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="b7952-214">認証フィルターとホストレベル認証の組み合わせ</span><span class="sxs-lookup"><span data-stu-id="b7952-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="b7952-215">"ホストレベルの認証" は、要求が Web API フレームワークに到達する前に、ホスト (IIS など) によって実行される認証です。</span><span class="sxs-lookup"><span data-stu-id="b7952-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="b7952-216">多くの場合、アプリケーションの残りの部分に対してホストレベルの認証を有効にする必要がありますが、Web API コントローラーに対しては無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="b7952-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="b7952-217">たとえば、一般的なシナリオでは、ホストレベルでフォーム認証を有効にしますが、Web API にはトークンベースの認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="b7952-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="b7952-218">Web API パイプライン内でホストレベルの認証を無効にするには、構成で `config.SuppressHostPrincipal()` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b7952-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="b7952-219">これにより、web api は Web API パイプラインに入る要求から**IPrincipal**を削除します。</span><span class="sxs-lookup"><span data-stu-id="b7952-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="b7952-220">実質的には、要求&quot; の認証を解除 &quot;ます。</span><span class="sxs-lookup"><span data-stu-id="b7952-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="b7952-221">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="b7952-221">Additional Resources</span></span>

<span data-ttu-id="b7952-222">[ASP.NET Web API セキュリティフィルター](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN マガジン)</span><span class="sxs-lookup"><span data-stu-id="b7952-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
