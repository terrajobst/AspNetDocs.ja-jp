---
uid: webhooks/receiving/handlers
title: ASP.NET Webhook ハンドラー |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook で要求を処理する方法。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518032"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="25bfd-103">ASP.NET Webhook ハンドラー</span><span class="sxs-lookup"><span data-stu-id="25bfd-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="25bfd-104">WebHook 受信者によって WebHook 要求が検証されると、ユーザーコードによって処理する準備が整います。</span><span class="sxs-lookup"><span data-stu-id="25bfd-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="25bfd-105">ここで*ハンドラー*が登場します。</span><span class="sxs-lookup"><span data-stu-id="25bfd-105">This is where *handlers* come in.</span></span> <span data-ttu-id="25bfd-106">ハンドラーは[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)インターフェイスから派生しますが、通常はインターフェイスから直接派生するのではなく、 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="25bfd-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="25bfd-107">WebHook 要求は、1つまたは複数のハンドラーによって処理できます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="25bfd-108">ハンドラーは、それぞれの*順序*プロパティに基づいて順に呼び出されます。順序は単純な整数です (1 ~ 100 の範囲で指定することをお勧めします)。</span><span class="sxs-lookup"><span data-stu-id="25bfd-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook ハンドラーの順序プロパティの図](_static/Handlers.png)

<span data-ttu-id="25bfd-110">ハンドラーでは、必要に応じて WebHookHandlerContext の*response*プロパティを設定できます。これにより、処理が停止し、応答が WebHook への HTTP 応答として返されます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="25bfd-111">上記の場合、ハンドラー C は呼び出されません。これは、B よりも上位の順序になっており、B が応答を設定しているためです。</span><span class="sxs-lookup"><span data-stu-id="25bfd-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="25bfd-112">応答の設定は、通常、応答が元の API に情報を伝達できる Webhook にのみ関連します。</span><span class="sxs-lookup"><span data-stu-id="25bfd-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="25bfd-113">これは、たとえば、WebHook が発生したチャネルに応答がポストバックされる、余裕のある webhook があるケースです。</span><span class="sxs-lookup"><span data-stu-id="25bfd-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="25bfd-114">特定の受信側から Webhook を受信するだけの場合、ハンドラーは受信側のプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="25bfd-115">受信者が設定されていない場合は、すべてのユーザーに対して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="25bfd-116">応答のその他の一般的な用途の1つは、 *410*の応答を使用して、WebHook がアクティブでなくなったこと、およびそれ以降の要求を送信しないことを示すことです。</span><span class="sxs-lookup"><span data-stu-id="25bfd-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="25bfd-117">既定では、すべての WebHook 受信側によってハンドラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="25bfd-118">ただし、*受信側*のプロパティがハンドラーの名前に設定されている場合、そのハンドラーは受信側からの WebHook 要求のみを受信します。</span><span class="sxs-lookup"><span data-stu-id="25bfd-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="25bfd-119">WebHook の処理</span><span class="sxs-lookup"><span data-stu-id="25bfd-119">Processing a WebHook</span></span>

<span data-ttu-id="25bfd-120">ハンドラーが呼び出されると、WebHook 要求に関する情報を含む[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)が取得されます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="25bfd-121">データ (通常は HTTP 要求本文) は、*データ*プロパティから取得できます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="25bfd-122">データの型は、通常、JSON または HTML 形式のデータですが、必要に応じて、より具体的な型にキャストすることもできます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="25bfd-123">たとえば、ASP.NET Webhook によって生成されるカスタム Webhook は、次のように[customnotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)型にキャストできます。</span><span class="sxs-lookup"><span data-stu-id="25bfd-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="25bfd-124">キューに置かれた処理</span><span class="sxs-lookup"><span data-stu-id="25bfd-124">Queued Processing</span></span>

<span data-ttu-id="25bfd-125">ほとんどの WebHook センダーは、数秒以内に応答が生成されない場合、WebHook を再送信します。</span><span class="sxs-lookup"><span data-stu-id="25bfd-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="25bfd-126">これは、ハンドラーが再度呼び出されないように、その時間枠内の処理を完了する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="25bfd-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="25bfd-127">処理に時間がかかる場合、または個別に処理する方がよい場合は、 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)を使用してキューに WebHook 要求を送信することができます ( [Azure Storage queue](https://msdn.microsoft.com/library/azure/dd179353.aspx)など)。</span><span class="sxs-lookup"><span data-stu-id="25bfd-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="25bfd-128">[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)実装の概要については、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25bfd-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
