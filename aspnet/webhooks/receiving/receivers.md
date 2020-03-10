---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook のレシーバー |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook レシーバー
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463462"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="3c35d-103">ASP.NET Webhook レシーバー</span><span class="sxs-lookup"><span data-stu-id="3c35d-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="3c35d-104">Webhook の受信は、送信者が誰であるかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="3c35d-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="3c35d-105">場合によっては、サブスクライバーが実際にリッスンしていることを確認するために、WebHook の登録に関する追加の手順があります。</span><span class="sxs-lookup"><span data-stu-id="3c35d-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="3c35d-106">一部の Webhook にはプッシュツープルモデルが用意されています。このモデルでは、HTTP POST 要求には、イベント情報への参照のみが含まれ、その後、個別に取得されます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="3c35d-107">多くの場合、セキュリティモデルは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="3c35d-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="3c35d-108">Webhook の Microsoft ASP.NET の目的は、特定のバリエーションの Webhook を処理する方法を理解することなく、API を簡単かつ一貫性のある方法で作成できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="3c35d-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="3c35d-109">WebHook 受信側は、特定の送信元からの webhook を受け入れて検証する役割を担います。</span><span class="sxs-lookup"><span data-stu-id="3c35d-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="3c35d-110">WebHook 受信者は任意の数の webhook をサポートでき、それぞれに独自の構成があります。</span><span class="sxs-lookup"><span data-stu-id="3c35d-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="3c35d-111">たとえば、GitHub WebHook 受信者は、任意の数の GitHub リポジトリからの webhook を受け入れることができます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="3c35d-112">WebHook 受信者の Uri</span><span class="sxs-lookup"><span data-stu-id="3c35d-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="3c35d-113">Microsoft ASP.NET webhook をインストールすることにより、一般に終了したサービス数から WebHook 要求を受け入れる汎用 WebHook コントローラーを取得できます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="3c35d-114">要求が到着すると、特定の WebHook センダーを処理するためにインストールした適切な受信者が選択されます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="3c35d-115">このコントローラーの URI は、サービスに登録する WebHook URI であり、次の形式です。</span><span class="sxs-lookup"><span data-stu-id="3c35d-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="3c35d-116">セキュリティ上の理由から、多くの WebHook レシーバーでは URI が*https* uri である必要があり、場合によっては、意図したパーティのみが上記の uri に webhook を送信できるようにするために使用される追加のクエリパラメーターも含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="3c35d-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="3c35d-117">`<receiver>` コンポーネントは、`github` や `slack`など、受信者の名前です。</span><span class="sxs-lookup"><span data-stu-id="3c35d-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="3c35d-118">*{Id}* は、特定の WebHook 受信者の構成を識別するために使用できる、省略可能な識別子です。</span><span class="sxs-lookup"><span data-stu-id="3c35d-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="3c35d-119">これは、特定の受信者に N Webhook を登録するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="3c35d-120">たとえば、次の3つの Uri を使用して、3つの独立した Webhook を登録できます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="3c35d-121">WebHook 受信側のインストール</span><span class="sxs-lookup"><span data-stu-id="3c35d-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="3c35d-122">Microsoft ASP.NET WebHook を使用して webhook を受信するには、まず WebHook プロバイダーの Nuget パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="3c35d-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="3c35d-123">Nuget パッケージには、" [Microsoft.](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) .............." という名前が付けられます。最後の部分は、サポートされるサービスを示します。</span><span class="sxs-lookup"><span data-stu-id="3c35d-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="3c35d-124">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3c35d-124">For example</span></span>

<span data-ttu-id="3c35d-125">ASP.NET webhook によって生成された webhook を受信するためのサポート[を提供します。](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)カスタムは、webhook によって生成される webhook の受信をサポート[し](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)ています。</span><span class="sxs-lookup"><span data-stu-id="3c35d-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="3c35d-126">既定では、Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、余裕、ストライプ、Trello、および WordPress がサポートされていますが、他の任意の数のプロバイダーをサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="3c35d-127">WebHook 受信側の構成</span><span class="sxs-lookup"><span data-stu-id="3c35d-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="3c35d-128">WebHook レシーバーは[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)インターフェイスによって構成され、そのインターフェイスの特定の実装は、任意の依存関係挿入モデルを使用して登録できます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="3c35d-129">既定の実装では、web.config ファイルで設定できるアプリケーション設定が使用されます。または、Azure Web Apps を使用する場合は、 [Azure Portal](https://portal.azure.com/)で設定できます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure App Settings](_static/AzureAppSettings.png)

<span data-ttu-id="3c35d-131">アプリケーション設定キーの形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3c35d-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="3c35d-132">値は、Webhook が登録されている *{id}* 値に一致する値のコンマ区切りのリストです。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="3c35d-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="3c35d-133">WebHook 受信側の初期化</span><span class="sxs-lookup"><span data-stu-id="3c35d-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="3c35d-134">WebHook レシーバーは、次の例のように、 *webapiconfig.cs*静的クラスに登録することによって初期化されます。</span><span class="sxs-lookup"><span data-stu-id="3c35d-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
