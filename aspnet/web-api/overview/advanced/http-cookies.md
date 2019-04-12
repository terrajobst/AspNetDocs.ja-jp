---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API - ASP.NET の HTTP Cookie 4.x
author: MikeWasson
description: ASP.NET 用の Web API の HTTP クッキーを送受信する方法について説明します 4.x です。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: cd6391582f05ab80c4bd45a455a2ce488d1186c1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418327"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="7493a-103">ASP.NET Web API の HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="7493a-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="7493a-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7493a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7493a-105">このトピックでは、Web API で HTTP クッキーを送受信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7493a-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="7493a-106">HTTP クッキーの背景</span><span class="sxs-lookup"><span data-stu-id="7493a-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="7493a-107">ここでは、HTTP レベルで cookie を実装する方法について概説します。</span><span class="sxs-lookup"><span data-stu-id="7493a-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="7493a-108">詳細についてを参照してください[RFC 6265](http://tools.ietf.org/html/rfc6265)します。</span><span class="sxs-lookup"><span data-stu-id="7493a-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="7493a-109">Cookie とは、サーバーが HTTP 応答で送信するデータの一部です。</span><span class="sxs-lookup"><span data-stu-id="7493a-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="7493a-110">(省略可能)、クライアントはクッキーを格納し、後続の要求で返します。</span><span class="sxs-lookup"><span data-stu-id="7493a-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="7493a-111">これにより、クライアントとサーバー状態を共有できます。</span><span class="sxs-lookup"><span data-stu-id="7493a-111">This allows the client and server to share state.</span></span> <span data-ttu-id="7493a-112">サーバーには cookie を設定するには、応答 Set-cookie ヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7493a-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="7493a-113">Cookie の形式は、省略可能な属性を持つ、名前と値のペアです。</span><span class="sxs-lookup"><span data-stu-id="7493a-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="7493a-114">例:</span><span class="sxs-lookup"><span data-stu-id="7493a-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="7493a-115">属性を持つ例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="7493a-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="7493a-116">クライアントにはサーバーに返す cookie は、以降の要求で Cookie ヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7493a-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="7493a-117">HTTP 応答には、複数 Set-cookie ヘッダーを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="7493a-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="7493a-118">クッキー ヘッダーを 1 つを使用して複数の cookie をクライアントに返します。</span><span class="sxs-lookup"><span data-stu-id="7493a-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="7493a-119">Set-cookie ヘッダーで次の属性では、スコープと cookie の期間が制御されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="7493a-120">**ドメイン**:ドメインがクッキーを受信する必要があります、クライアントに指示します。</span><span class="sxs-lookup"><span data-stu-id="7493a-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="7493a-121">たとえば、ドメインが"example.com"の場合は、クライアントは、example.com のすべてのサブドメインに cookie を返します。</span><span class="sxs-lookup"><span data-stu-id="7493a-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="7493a-122">指定しない場合、ドメイン、配信元サーバーです。</span><span class="sxs-lookup"><span data-stu-id="7493a-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="7493a-123">**パス**:ドメイン内で指定したパスに cookie を制限します。</span><span class="sxs-lookup"><span data-stu-id="7493a-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="7493a-124">指定されていない場合は、要求 URI のパスが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="7493a-125">**有効期限が切れる**:Cookie の有効期限を設定します。</span><span class="sxs-lookup"><span data-stu-id="7493a-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="7493a-126">クライアントは、有効期限が切れた cookie を削除します。</span><span class="sxs-lookup"><span data-stu-id="7493a-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="7493a-127">**Max Age**:クッキーの最大有効期間を設定します。</span><span class="sxs-lookup"><span data-stu-id="7493a-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="7493a-128">クライアントは、最大有効期間に達すると、クッキーを削除します。</span><span class="sxs-lookup"><span data-stu-id="7493a-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="7493a-129">両方`Expires`と`Max-Age`が設定されている`Max-Age`が優先されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="7493a-130">どちらも設定されている場合、クライアントは、現在のセッションの終了時に cookie を削除します。</span><span class="sxs-lookup"><span data-stu-id="7493a-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="7493a-131">(「セッション」の厳密な意味は、ユーザー エージェントによって決まります。)</span><span class="sxs-lookup"><span data-stu-id="7493a-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="7493a-132">ただし、クライアントがクッキーを無視することこともあります。</span><span class="sxs-lookup"><span data-stu-id="7493a-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="7493a-133">たとえば、ユーザーには、プライバシー保護のための cookie が無効にする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7493a-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="7493a-134">クライアントは、有効期限、または格納されているクッキーの数を制限する前に、cookie を削除できます。</span><span class="sxs-lookup"><span data-stu-id="7493a-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="7493a-135">プライバシー上の理由から、クライアントは多くの場合、ドメインが配信元サーバーと一致しません、「サードパーティ」の cookie を拒否します。</span><span class="sxs-lookup"><span data-stu-id="7493a-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="7493a-136">簡単に言えば、これを設定する cookie を取得するのには、サーバーが依存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7493a-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="7493a-137">Web API の cookie</span><span class="sxs-lookup"><span data-stu-id="7493a-137">Cookies in Web API</span></span>

<span data-ttu-id="7493a-138">クッキーを HTTP 応答に追加するには、作成、 **CookieHeaderValue**クッキーを表すインスタンス。</span><span class="sxs-lookup"><span data-stu-id="7493a-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="7493a-139">呼び出して、 **AddCookies**で定義されている拡張メソッド、 **System.Net.Http します。HttpResponseHeadersExtensions**クラスに、cookie を追加します。</span><span class="sxs-lookup"><span data-stu-id="7493a-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="7493a-140">たとえば、次のコードでは、コント ローラー アクション内のクッキーが追加されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="7493a-141">注意**AddCookies**の配列を受け取る**CookieHeaderValue**インスタンス。</span><span class="sxs-lookup"><span data-stu-id="7493a-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="7493a-142">クライアント要求から cookie を抽出する呼び出し、 **GetCookies**メソッド。</span><span class="sxs-lookup"><span data-stu-id="7493a-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="7493a-143">A **CookieHeaderValue**のコレクションを含む**CookieState**インスタンス。</span><span class="sxs-lookup"><span data-stu-id="7493a-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="7493a-144">各**CookieState** cookie の 1 つを表します。</span><span class="sxs-lookup"><span data-stu-id="7493a-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="7493a-145">取得するインデクサー メソッドを使用して、 **CookieState**名前で示すようにします。</span><span class="sxs-lookup"><span data-stu-id="7493a-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="7493a-146">構造化された Cookie のデータ</span><span class="sxs-lookup"><span data-stu-id="7493a-146">Structured Cookie Data</span></span>

<span data-ttu-id="7493a-147">多くのブラウザーの制限数の cookie が格納されます&#8212;合計の数と、ドメインごとの数。</span><span class="sxs-lookup"><span data-stu-id="7493a-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="7493a-148">したがって、複数の cookie を設定する代わりに、1 つの cookie に構造化データを格納するのに便利ですができます。</span><span class="sxs-lookup"><span data-stu-id="7493a-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="7493a-149">RFC 6265 は、cookie のデータの構造を定義しません。</span><span class="sxs-lookup"><span data-stu-id="7493a-149">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="7493a-150">使用して、 **CookieHeaderValue**クラス、cookie のデータの名前と値のペアの一覧を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="7493a-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="7493a-151">これらの名前と値のペアは、Set-cookie ヘッダーの URL でエンコードされたフォーム データとしてエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="7493a-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="7493a-152">前のコードでは、次の Set-cookie ヘッダーが生成されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="7493a-153">**CookieState**クラス インデクサー要求メッセージ内の cookie からサブの値を読み取るメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="7493a-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="7493a-154">例:設定およびメッセージ ハンドラーで Cookie を取得します。</span><span class="sxs-lookup"><span data-stu-id="7493a-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="7493a-155">前の例では、Web API コント ローラー内から cookie を使用する方法を示しました。</span><span class="sxs-lookup"><span data-stu-id="7493a-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="7493a-156">別のオプションは、使用する[メッセージ ハンドラー](http-message-handlers.md)します。</span><span class="sxs-lookup"><span data-stu-id="7493a-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="7493a-157">コント ローラーとパイプラインの初期には、メッセージのハンドラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="7493a-158">メッセージ ハンドラーは、コント ローラーに到達する前に、cookie を要求から読み取りまたはコント ローラーが応答を生成した後、応答に cookie を追加できます。</span><span class="sxs-lookup"><span data-stu-id="7493a-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="7493a-159">次のコードでは、セッション Id を作成するためのメッセージ ハンドラーを示します。</span><span class="sxs-lookup"><span data-stu-id="7493a-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="7493a-160">セッション ID は、cookie に格納されます。</span><span class="sxs-lookup"><span data-stu-id="7493a-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="7493a-161">ハンドラーは、セッション cookie の要求を確認します。</span><span class="sxs-lookup"><span data-stu-id="7493a-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="7493a-162">ハンドラーが新しいセッション ID を生成する要求にクッキーが含まれていない場合</span><span class="sxs-lookup"><span data-stu-id="7493a-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="7493a-163">どちらの場合、ハンドラーが内のセッション ID を格納、 **HttpRequestMessage.Properties**プロパティ バッグ。</span><span class="sxs-lookup"><span data-stu-id="7493a-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="7493a-164">また、セッション クッキーを HTTP 応答に追加します。</span><span class="sxs-lookup"><span data-stu-id="7493a-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="7493a-165">この実装では、クライアントからのセッション ID がサーバーによって実際に発行されたことを検証しません。</span><span class="sxs-lookup"><span data-stu-id="7493a-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="7493a-166">認証の形式として使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="7493a-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="7493a-167">この例のポイントでは、HTTP クッキー管理を説明します。</span><span class="sxs-lookup"><span data-stu-id="7493a-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="7493a-168">コント ローラーからのセッション ID を取得できます、 **HttpRequestMessage.Properties**プロパティ バッグ。</span><span class="sxs-lookup"><span data-stu-id="7493a-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
