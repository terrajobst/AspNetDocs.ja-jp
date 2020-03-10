---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API の HttpClient メッセージハンドラー-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x で ASP.NET Web API 用のカスタムメッセージハンドラーを作成する
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449278"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="46292-103">ASP.NET Web API 内の HttpClient メッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="46292-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="46292-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="46292-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="46292-105">*メッセージハンドラー*は、http 要求を受け取り、http 応答を返すクラスです。</span><span class="sxs-lookup"><span data-stu-id="46292-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="46292-106">通常、一連のメッセージハンドラーが連結されます。</span><span class="sxs-lookup"><span data-stu-id="46292-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="46292-107">最初のハンドラーは HTTP 要求を受け取り、何らかの処理を行い、次のハンドラーに要求を渡します。</span><span class="sxs-lookup"><span data-stu-id="46292-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="46292-108">ある時点で、応答が作成され、チェーンがバックアップされます。</span><span class="sxs-lookup"><span data-stu-id="46292-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="46292-109">このパターンは、*デリゲート*ハンドラーと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="46292-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="46292-110">クライアント側では、 **Httpclient**クラスはメッセージハンドラーを使用して要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="46292-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="46292-111">既定のハンドラーは**Httpclienthandler**であり、ネットワーク経由で要求を送信し、サーバーからの応答を取得します。</span><span class="sxs-lookup"><span data-stu-id="46292-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="46292-112">クライアントパイプラインにカスタムメッセージハンドラーを挿入できます。</span><span class="sxs-lookup"><span data-stu-id="46292-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="46292-113">ASP.NET Web API は、サーバー側でもメッセージハンドラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="46292-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="46292-114">詳細については、「 [HTTP メッセージハンドラー](http-message-handlers.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="46292-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="46292-115">カスタムメッセージハンドラー</span><span class="sxs-lookup"><span data-stu-id="46292-115">Custom Message Handlers</span></span>

<span data-ttu-id="46292-116">カスタムメッセージハンドラーを作成するには、 **DelegatingHandler**から派生させ、 **sendasync**メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="46292-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="46292-117">このメソッド シグネチャを次に示します。</span><span class="sxs-lookup"><span data-stu-id="46292-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="46292-118">このメソッドは、 **HttpRequestMessage**を入力として受け取り、非同期的に**HttpResponseMessage**を返します。</span><span class="sxs-lookup"><span data-stu-id="46292-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="46292-119">一般的な実装では、次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="46292-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="46292-120">要求メッセージを処理します。</span><span class="sxs-lookup"><span data-stu-id="46292-120">Process the request message.</span></span>
2. <span data-ttu-id="46292-121">`base.SendAsync` を呼び出して、要求を内部ハンドラーに送信します。</span><span class="sxs-lookup"><span data-stu-id="46292-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="46292-122">内部ハンドラーは、応答メッセージを返します。</span><span class="sxs-lookup"><span data-stu-id="46292-122">The inner handler returns a response message.</span></span> <span data-ttu-id="46292-123">(この手順は非同期です)。</span><span class="sxs-lookup"><span data-stu-id="46292-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="46292-124">応答を処理し、呼び出し元に返します。</span><span class="sxs-lookup"><span data-stu-id="46292-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="46292-125">次の例は、送信要求にカスタムヘッダーを追加するメッセージハンドラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="46292-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="46292-126">`base.SendAsync` の呼び出しは非同期です。</span><span class="sxs-lookup"><span data-stu-id="46292-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="46292-127">この呼び出しの後でハンドラーが何らかの処理を実行する場合は、 **await**キーワードを使用して、メソッドの完了後に実行を再開します。</span><span class="sxs-lookup"><span data-stu-id="46292-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="46292-128">次の例は、エラーコードをログに記録するハンドラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="46292-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="46292-129">ログ自体はあまり興味深いものではありませんが、この例では、ハンドラー内の応答を取得する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="46292-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="46292-130">クライアントパイプラインへのメッセージハンドラーの追加</span><span class="sxs-lookup"><span data-stu-id="46292-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="46292-131">**Httpclient**にカスタムハンドラーを追加するには、 **HttpClientFactory**メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="46292-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="46292-132">メッセージハンドラーは、 **Create**メソッドに渡す順序で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="46292-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="46292-133">ハンドラーは入れ子になっているため、応答メッセージは別の方向に移動します。</span><span class="sxs-lookup"><span data-stu-id="46292-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="46292-134">つまり、最後のハンドラーは、応答メッセージを取得するための最初のハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="46292-134">That is, the last handler is the first to get the response message.</span></span>
