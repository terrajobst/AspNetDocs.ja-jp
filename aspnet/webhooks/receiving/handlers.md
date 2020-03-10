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
# <a name="aspnet-webhooks-handlers"></a>ASP.NET Webhook ハンドラー

WebHook 受信者によって WebHook 要求が検証されると、ユーザーコードによって処理する準備が整います。 ここで*ハンドラー*が登場します。 ハンドラーは[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)インターフェイスから派生しますが、通常はインターフェイスから直接派生するのではなく、 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)クラスを使用します。

WebHook 要求は、1つまたは複数のハンドラーによって処理できます。 ハンドラーは、それぞれの*順序*プロパティに基づいて順に呼び出されます。順序は単純な整数です (1 ~ 100 の範囲で指定することをお勧めします)。

![WebHook ハンドラーの順序プロパティの図](_static/Handlers.png)

ハンドラーでは、必要に応じて WebHookHandlerContext の*response*プロパティを設定できます。これにより、処理が停止し、応答が WebHook への HTTP 応答として返されます。 上記の場合、ハンドラー C は呼び出されません。これは、B よりも上位の順序になっており、B が応答を設定しているためです。

応答の設定は、通常、応答が元の API に情報を伝達できる Webhook にのみ関連します。 これは、たとえば、WebHook が発生したチャネルに応答がポストバックされる、余裕のある webhook があるケースです。 特定の受信側から Webhook を受信するだけの場合、ハンドラーは受信側のプロパティを設定できます。 受信者が設定されていない場合は、すべてのユーザーに対して呼び出されます。

応答のその他の一般的な用途の1つは、 *410*の応答を使用して、WebHook がアクティブでなくなったこと、およびそれ以降の要求を送信しないことを示すことです。

既定では、すべての WebHook 受信側によってハンドラーが呼び出されます。 ただし、*受信側*のプロパティがハンドラーの名前に設定されている場合、そのハンドラーは受信側からの WebHook 要求のみを受信します。

## <a name="processing-a-webhook"></a>WebHook の処理

ハンドラーが呼び出されると、WebHook 要求に関する情報を含む[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)が取得されます。 データ (通常は HTTP 要求本文) は、*データ*プロパティから取得できます。

データの型は、通常、JSON または HTML 形式のデータですが、必要に応じて、より具体的な型にキャストすることもできます。 たとえば、ASP.NET Webhook によって生成されるカスタム Webhook は、次のように[customnotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)型にキャストできます。

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

  ## <a name="queued-processing"></a>キューに置かれた処理

ほとんどの WebHook センダーは、数秒以内に応答が生成されない場合、WebHook を再送信します。 これは、ハンドラーが再度呼び出されないように、その時間枠内の処理を完了する必要があることを意味します。

処理に時間がかかる場合、または個別に処理する方がよい場合は、 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)を使用してキューに WebHook 要求を送信することができます ( [Azure Storage queue](https://msdn.microsoft.com/library/azure/dd179353.aspx)など)。

[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)実装の概要については、次を参照してください。

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
