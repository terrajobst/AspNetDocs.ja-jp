---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API の HTTP Cookie-ASP.NET 4.x
author: MikeWasson
description: Web API for ASP.NET 4.x で HTTP クッキーを送受信する方法について説明します。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449314"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="caa9e-103">ASP.NET Web API の HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="caa9e-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="caa9e-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="caa9e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="caa9e-105">このトピックでは、Web API で HTTP cookie を送受信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="caa9e-106">HTTP クッキーの背景</span><span class="sxs-lookup"><span data-stu-id="caa9e-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="caa9e-107">ここでは、HTTP レベルでの cookie の実装方法について簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="caa9e-108">詳細については、 [RFC 6265](http://tools.ietf.org/html/rfc6265)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="caa9e-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="caa9e-109">Cookie は、サーバーが HTTP 応答で送信するデータの一部です。</span><span class="sxs-lookup"><span data-stu-id="caa9e-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="caa9e-110">クライアントは (必要に応じて) cookie を保存し、後続の要求でそれを返します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="caa9e-111">これにより、クライアントとサーバーが状態を共有できるようになります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-111">This allows the client and server to share state.</span></span> <span data-ttu-id="caa9e-112">Cookie を設定するために、サーバーには、応答に設定 Cookie ヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="caa9e-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="caa9e-113">Cookie の形式は、名前と値のペアであり、省略可能な属性があります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="caa9e-114">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="caa9e-115">属性を使用した例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="caa9e-116">クッキーをサーバーに返すために、クライアントには、後で要求する Cookie ヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="caa9e-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="caa9e-117">HTTP 応答には、複数の設定 Cookie ヘッダーを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="caa9e-118">クライアントは、単一の Cookie ヘッダーを使用して複数の cookie を返します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="caa9e-119">Cookie のスコープと存続期間は、次の属性によって、Set Cookie ヘッダーに含まれる属性によって制御されます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="caa9e-120">**Domain**: クッキーを受信する必要があるドメインをクライアントに指示します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="caa9e-121">たとえば、ドメインが "example.com" の場合、クライアントは example.com のすべてのサブドメインに cookie を返します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="caa9e-122">指定しない場合、ドメインは配信元サーバーになります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="caa9e-123">**パス**: ドメイン内の指定されたパスに cookie を制限します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="caa9e-124">指定しない場合は、要求 URI のパスが使用されます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="caa9e-125">**有効期限**: クッキーの有効期限を設定します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="caa9e-126">クライアントは、有効期限が切れたときに cookie を削除します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="caa9e-127">**最長有効期間**: cookie の最大有効期間を設定します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="caa9e-128">クライアントは、最大有効期間に達したときにクッキーを削除します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="caa9e-129">`Expires` と `Max-Age` の両方が設定されている場合は、`Max-Age` が優先されます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="caa9e-130">どちらも設定されていない場合、クライアントは、現在のセッションが終了したときにクッキーを削除します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="caa9e-131">("セッション" の正確な意味は、ユーザーエージェントによって決まります)。</span><span class="sxs-lookup"><span data-stu-id="caa9e-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="caa9e-132">ただし、クライアントでは cookie が無視される可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="caa9e-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="caa9e-133">たとえば、プライバシー上の理由から、ユーザーが cookie を無効にする場合があります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="caa9e-134">クライアントは、有効期限が切れる前に cookie を削除することも、保存される cookie の数を制限することもできます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="caa9e-135">プライバシー上の理由から、クライアントは、ドメインが配信元サーバーと一致しない "サードパーティ" の cookie を拒否することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="caa9e-136">つまり、サーバーは、設定された cookie の取得に依存しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="caa9e-137">Web API の cookie</span><span class="sxs-lookup"><span data-stu-id="caa9e-137">Cookies in Web API</span></span>

<span data-ttu-id="caa9e-138">クッキーを HTTP 応答に追加するには、クッキーを表す**Cookieheadervalue**インスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="caa9e-139">次に、システムの .Net. Http で定義されている**Addcookies**拡張メソッドを呼び出し**ます。** クッキーを追加する HttpResponseHeadersExtensions クラス。</span><span class="sxs-lookup"><span data-stu-id="caa9e-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="caa9e-140">たとえば、次のコードでは、コントローラーアクション内に cookie を追加します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="caa9e-141">**Addcookies**は、 **cookieheadervalue**インスタンスの配列を受け取ることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="caa9e-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="caa9e-142">クライアント要求からクッキーを抽出するには、 **Getcookies**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="caa9e-143">**Cookieheadervalue**には、 **cookiestate**インスタンスのコレクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="caa9e-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="caa9e-144">各**Cookiestate**は、1つの cookie を表します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="caa9e-145">以下に示すように、インデクサーメソッドを使用して、名前で**Cookiestate**を取得します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="caa9e-146">構造化された Cookie データ</span><span class="sxs-lookup"><span data-stu-id="caa9e-146">Structured Cookie Data</span></span>

<span data-ttu-id="caa9e-147">多くのブラウザーでは、合計数と&#8212;ドメインあたりの数の両方を格納する cookie の数が制限されています。</span><span class="sxs-lookup"><span data-stu-id="caa9e-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="caa9e-148">そのため、複数の cookie を設定するのではなく、構造化されたデータを1つの cookie に格納すると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="caa9e-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="caa9e-149">RFC 6265 では、cookie データの構造は定義されていません。</span><span class="sxs-lookup"><span data-stu-id="caa9e-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="caa9e-150">**Cookieheadervalue**クラスを使用して、cookie データの名前と値のペアのリストを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="caa9e-151">これらの名前と値のペアは、URL エンコードされたフォームデータとして、Set Cookie ヘッダーにエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="caa9e-152">前のコードでは、次の Set Cookie ヘッダーが生成されます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="caa9e-153">**Cookiestate**クラスには、要求メッセージの cookie からサブ値を読み取るためのインデクサーメソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="caa9e-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="caa9e-154">例: メッセージハンドラーで Cookie を設定および取得する</span><span class="sxs-lookup"><span data-stu-id="caa9e-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="caa9e-155">前の例では、Web API コントローラー内から cookie を使用する方法を示しました。</span><span class="sxs-lookup"><span data-stu-id="caa9e-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="caa9e-156">別の方法として、[メッセージハンドラー](http-message-handlers.md)を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="caa9e-157">メッセージハンドラーは、パイプラインの前にコントローラーよりも先に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="caa9e-158">メッセージハンドラーは、要求がコントローラーに到達する前に要求から cookie を読み取るか、コントローラーが応答を生成した後に cookie を応答に追加します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="caa9e-159">次のコードは、セッション Id を作成するためのメッセージハンドラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="caa9e-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="caa9e-160">セッション ID はクッキーに格納されます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="caa9e-161">ハンドラーは、セッション cookie の要求を確認します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="caa9e-162">要求にクッキーが含まれていない場合、ハンドラーは新しいセッション ID を生成します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="caa9e-163">どちらの場合も、ハンドラーは**HttpRequestMessage**プロパティバッグにセッション ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="caa9e-164">また、セッション cookie を HTTP 応答に追加します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="caa9e-165">この実装では、クライアントからのセッション ID がサーバーによって実際に発行されたかどうかは検証されません。</span><span class="sxs-lookup"><span data-stu-id="caa9e-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="caa9e-166">認証形式として使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="caa9e-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="caa9e-167">この例では、HTTP クッキー管理を示します。</span><span class="sxs-lookup"><span data-stu-id="caa9e-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="caa9e-168">コントローラーは、 **HttpRequestMessage**プロパティバッグからセッション ID を取得できます。</span><span class="sxs-lookup"><span data-stu-id="caa9e-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
