---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API の HTTP メッセージハンドラー-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API での HTTP メッセージハンドラーの概要
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504928"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="0b071-103">ASP.NET Web API の HTTP メッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="0b071-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="0b071-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0b071-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0b071-105">*メッセージハンドラー*は、http 要求を受け取り、http 応答を返すクラスです。</span><span class="sxs-lookup"><span data-stu-id="0b071-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="0b071-106">メッセージハンドラーは、抽象**Httpmessagehandler**クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="0b071-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="0b071-107">通常、一連のメッセージハンドラーが連結されます。</span><span class="sxs-lookup"><span data-stu-id="0b071-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="0b071-108">最初のハンドラーは HTTP 要求を受け取り、何らかの処理を行い、次のハンドラーに要求を渡します。</span><span class="sxs-lookup"><span data-stu-id="0b071-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="0b071-109">ある時点で、応答が作成され、チェーンがバックアップされます。</span><span class="sxs-lookup"><span data-stu-id="0b071-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="0b071-110">このパターンは、*デリゲート*ハンドラーと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="0b071-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="0b071-111">サーバー側のメッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="0b071-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="0b071-112">サーバー側では、Web API パイプラインはいくつかの組み込みメッセージハンドラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="0b071-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="0b071-113">**HttpServer**は、ホストから要求を取得します。</span><span class="sxs-lookup"><span data-stu-id="0b071-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="0b071-114">**HttpRoutingDispatcher**は、ルートに基づいて要求をディスパッチします。</span><span class="sxs-lookup"><span data-stu-id="0b071-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="0b071-115">**Httpcontroller ディスパッチャー**は、要求を Web API コントローラーに送信します。</span><span class="sxs-lookup"><span data-stu-id="0b071-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="0b071-116">パイプラインにカスタムハンドラーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="0b071-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="0b071-117">メッセージハンドラーは、(コントローラーアクションではなく) HTTP メッセージレベルで動作する横断的な懸念に適しています。</span><span class="sxs-lookup"><span data-stu-id="0b071-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="0b071-118">たとえば、次のようなメッセージハンドラーがあるとします。</span><span class="sxs-lookup"><span data-stu-id="0b071-118">For example, a message handler might:</span></span>

- <span data-ttu-id="0b071-119">要求ヘッダーを読み取りまたは変更します。</span><span class="sxs-lookup"><span data-stu-id="0b071-119">Read or modify request headers.</span></span>
- <span data-ttu-id="0b071-120">応答ヘッダーを応答に追加します。</span><span class="sxs-lookup"><span data-stu-id="0b071-120">Add a response header to responses.</span></span>
- <span data-ttu-id="0b071-121">コントローラーに到着する前に、要求を検証します。</span><span class="sxs-lookup"><span data-stu-id="0b071-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="0b071-122">次の図は、パイプラインに挿入された2つのカスタムハンドラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="0b071-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="0b071-123">クライアント側では、HttpClient はメッセージハンドラーも使用します。</span><span class="sxs-lookup"><span data-stu-id="0b071-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="0b071-124">詳細については、「 [Httpclient メッセージハンドラー](httpclient-message-handlers.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b071-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="0b071-125">カスタムメッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="0b071-125">Custom Message Handlers</span></span>

<span data-ttu-id="0b071-126">カスタムメッセージハンドラーを作成するには、 **DelegatingHandler**から派生させ、 **sendasync**メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="0b071-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="0b071-127">このメソッドのシグネチャは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0b071-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="0b071-128">このメソッドは、 **HttpRequestMessage**を入力として受け取り、非同期的に**HttpResponseMessage**を返します。</span><span class="sxs-lookup"><span data-stu-id="0b071-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="0b071-129">一般的な実装では、次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="0b071-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="0b071-130">要求メッセージを処理します。</span><span class="sxs-lookup"><span data-stu-id="0b071-130">Process the request message.</span></span>
2. <span data-ttu-id="0b071-131">`base.SendAsync` を呼び出して、要求を内部ハンドラーに送信します。</span><span class="sxs-lookup"><span data-stu-id="0b071-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="0b071-132">内部ハンドラーは、応答メッセージを返します。</span><span class="sxs-lookup"><span data-stu-id="0b071-132">The inner handler returns a response message.</span></span> <span data-ttu-id="0b071-133">(この手順は非同期です)。</span><span class="sxs-lookup"><span data-stu-id="0b071-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="0b071-134">応答を処理し、呼び出し元に返します。</span><span class="sxs-lookup"><span data-stu-id="0b071-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="0b071-135">単純な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="0b071-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="0b071-136">`base.SendAsync` の呼び出しは非同期です。</span><span class="sxs-lookup"><span data-stu-id="0b071-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="0b071-137">この呼び出しの後でハンドラーが何らかの処理を実行する場合は、次に示すように**await**キーワードを使用します。</span><span class="sxs-lookup"><span data-stu-id="0b071-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="0b071-138">デリゲートハンドラーは、内部ハンドラーをスキップし、直接応答を作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="0b071-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="0b071-139">デリゲートハンドラーが `base.SendAsync`を呼び出さずに応答を作成した場合、要求はパイプラインの残りの部分をスキップします。</span><span class="sxs-lookup"><span data-stu-id="0b071-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="0b071-140">これは、要求を検証するハンドラー (エラー応答の作成) に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0b071-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="0b071-141">パイプラインへのハンドラーの追加</span><span class="sxs-lookup"><span data-stu-id="0b071-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="0b071-142">サーバー側にメッセージハンドラーを追加するには、ハンドラーを**Httpconfiguration. messagehandlers**コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="0b071-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="0b071-143">"ASP.NET MVC 4 Web アプリケーション" テンプレートを使用してプロジェクトを作成した場合は、 **webapiconfig.cs**クラス内でこれを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0b071-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="0b071-144">メッセージハンドラーは、 **messagehandlers**コレクションに表示される順序と同じ順序で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="0b071-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="0b071-145">入れ子になっているため、応答メッセージは別の方向に移動します。</span><span class="sxs-lookup"><span data-stu-id="0b071-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="0b071-146">つまり、最後のハンドラーは、応答メッセージを取得するための最初のハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="0b071-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="0b071-147">内部ハンドラーを設定する必要がないことに注意してください。Web API フレームワークは、メッセージハンドラーを自動的に接続します。</span><span class="sxs-lookup"><span data-stu-id="0b071-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="0b071-148">[自己ホスト](../older-versions/self-host-a-web-api.md)している場合は、 **Httpselfhostconfiguration**クラスのインスタンスを作成し、そのハンドラーを**messagehandlers**コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="0b071-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="0b071-149">次に、カスタムメッセージハンドラーの例をいくつか見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="0b071-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="0b071-150">例: X-y-Override</span><span class="sxs-lookup"><span data-stu-id="0b071-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="0b071-151">-HTTP メソッドオーバーライドは、非標準の HTTP ヘッダーです。</span><span class="sxs-lookup"><span data-stu-id="0b071-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="0b071-152">これは、PUT や DELETE など、特定の種類の HTTP 要求を送信できないクライアント向けに設計されています。</span><span class="sxs-lookup"><span data-stu-id="0b071-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="0b071-153">代わりに、クライアントは POST 要求を送信し、X-y-Override ヘッダーを目的のメソッドに設定します。</span><span class="sxs-lookup"><span data-stu-id="0b071-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="0b071-154">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0b071-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="0b071-155">次に示すのは、X-HTTP メソッドオーバーライドのサポートを追加するメッセージハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="0b071-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="0b071-156">**Sendasync**メソッドでは、ハンドラーは、要求メッセージが POST 要求であるかどうか、およびそのメッセージに HTTP メソッドオーバーライドヘッダーが含まれているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="0b071-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="0b071-157">その場合は、ヘッダー値を検証してから、要求メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="0b071-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="0b071-158">最後に、ハンドラーは `base.SendAsync` を呼び出して、メッセージを次のハンドラーに渡します。</span><span class="sxs-lookup"><span data-stu-id="0b071-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="0b071-159">要求が**Httpコントローラーディスパッチャー**クラスに到達すると、 **httpコントローラーディスパッチャー**は、更新された要求メソッドに基づいて要求をルーティングします。</span><span class="sxs-lookup"><span data-stu-id="0b071-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="0b071-160">例: カスタム応答ヘッダーの追加</span><span class="sxs-lookup"><span data-stu-id="0b071-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="0b071-161">次に示すのは、すべての応答メッセージにカスタムヘッダーを追加するメッセージハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="0b071-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="0b071-162">まず、ハンドラーは `base.SendAsync` を呼び出して、要求を内部メッセージハンドラーに渡します。</span><span class="sxs-lookup"><span data-stu-id="0b071-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="0b071-163">内部ハンドラーは応答メッセージを返しますが、**タスク&lt;t&gt;** オブジェクトを使用して非同期的に処理します。</span><span class="sxs-lookup"><span data-stu-id="0b071-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="0b071-164">応答メッセージは、`base.SendAsync` が非同期に完了するまで使用できません。</span><span class="sxs-lookup"><span data-stu-id="0b071-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="0b071-165">この例では、 **await**キーワードを使用して `SendAsync` の完了後に非同期に作業を実行します。</span><span class="sxs-lookup"><span data-stu-id="0b071-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="0b071-166">.NET Framework 4.0 を対象としている場合は、&lt;T&gt;**タスク**を使用し**ます。System.threading.tasks.task.continuewith**メソッド:</span><span class="sxs-lookup"><span data-stu-id="0b071-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="0b071-167">例: API キーの確認</span><span class="sxs-lookup"><span data-stu-id="0b071-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="0b071-168">一部の web サービスでは、クライアントが要求に API キーを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b071-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="0b071-169">次の例は、メッセージハンドラーが有効な API キーの要求を確認する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="0b071-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="0b071-170">このハンドラーは、URI クエリ文字列内の API キーを検索します。</span><span class="sxs-lookup"><span data-stu-id="0b071-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="0b071-171">(この例では、キーが静的な文字列であると想定しています。</span><span class="sxs-lookup"><span data-stu-id="0b071-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="0b071-172">実際の実装では、より複雑な検証を使用する可能性があります)。クエリ文字列にキーが含まれている場合、ハンドラーは内部ハンドラーに要求を渡します。</span><span class="sxs-lookup"><span data-stu-id="0b071-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="0b071-173">要求に有効なキーがない場合、ハンドラーは状態が403である応答メッセージを作成します。</span><span class="sxs-lookup"><span data-stu-id="0b071-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="0b071-174">この場合、ハンドラーは `base.SendAsync`を呼び出さないため、内部ハンドラーは要求を受信せず、コントローラーも受け入れません。</span><span class="sxs-lookup"><span data-stu-id="0b071-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="0b071-175">したがって、コントローラーは、すべての受信要求に有効な API キーがあると見なすことができます。</span><span class="sxs-lookup"><span data-stu-id="0b071-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="0b071-176">API キーが特定のコントローラーアクションにのみ適用される場合は、メッセージハンドラーの代わりにアクションフィルターを使用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="0b071-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="0b071-177">アクションフィルターは、URI ルーティングが実行された後に実行されます。</span><span class="sxs-lookup"><span data-stu-id="0b071-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="0b071-178">ルートごとのメッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="0b071-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="0b071-179">**Httpconfiguration. MessageHandlers**コレクション内のハンドラーはグローバルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="0b071-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="0b071-180">または、ルートを定義するときに、特定のルートにメッセージハンドラーを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="0b071-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="0b071-181">この例では、要求 URI が "Route2" に一致する場合、要求は `MessageHandler2`にディスパッチされます。</span><span class="sxs-lookup"><span data-stu-id="0b071-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="0b071-182">次の図は、これらの2つのルートのパイプラインを示しています。</span><span class="sxs-lookup"><span data-stu-id="0b071-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="0b071-183">既定の**Httpコントローラーディスパッチャー**が `MessageHandler2` に置き換わることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0b071-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="0b071-184">この例では、`MessageHandler2` によって応答が作成され、"Route2" に一致する要求はコントローラーに送られません。</span><span class="sxs-lookup"><span data-stu-id="0b071-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="0b071-185">これにより、Web API コントローラーのメカニズム全体を独自のカスタムエンドポイントに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="0b071-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="0b071-186">もう1つの方法として、ルートごとのメッセージハンドラーは**httpcontroller ディスパッチャー**に委任できます。これにより、コントローラーにディスパッチされます。</span><span class="sxs-lookup"><span data-stu-id="0b071-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="0b071-187">次のコードは、このルートを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="0b071-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
