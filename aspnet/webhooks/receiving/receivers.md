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
# <a name="aspnet-webhooks-receivers"></a>ASP.NET Webhook レシーバー

Webhook の受信は、送信者が誰であるかによって異なります。 場合によっては、サブスクライバーが実際にリッスンしていることを確認するために、WebHook の登録に関する追加の手順があります。 一部の Webhook にはプッシュツープルモデルが用意されています。このモデルでは、HTTP POST 要求には、イベント情報への参照のみが含まれ、その後、個別に取得されます。 多くの場合、セキュリティモデルは少し異なります。

Webhook の Microsoft ASP.NET の目的は、特定のバリエーションの Webhook を処理する方法を理解することなく、API を簡単かつ一貫性のある方法で作成できるようにすることです。

WebHook 受信側は、特定の送信元からの webhook を受け入れて検証する役割を担います。 WebHook 受信者は任意の数の webhook をサポートでき、それぞれに独自の構成があります。 たとえば、GitHub WebHook 受信者は、任意の数の GitHub リポジトリからの webhook を受け入れることができます。

## <a name="webhook-receiver-uris"></a>WebHook 受信者の Uri

Microsoft ASP.NET webhook をインストールすることにより、一般に終了したサービス数から WebHook 要求を受け入れる汎用 WebHook コントローラーを取得できます。 要求が到着すると、特定の WebHook センダーを処理するためにインストールした適切な受信者が選択されます。

このコントローラーの URI は、サービスに登録する WebHook URI であり、次の形式です。

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

セキュリティ上の理由から、多くの WebHook レシーバーでは URI が*https* uri である必要があり、場合によっては、意図したパーティのみが上記の uri に webhook を送信できるようにするために使用される追加のクエリパラメーターも含める必要があります。

`<receiver>` コンポーネントは、`github` や `slack`など、受信者の名前です。

*{Id}* は、特定の WebHook 受信者の構成を識別するために使用できる、省略可能な識別子です。 これは、特定の受信者に N Webhook を登録するために使用できます。 たとえば、次の3つの Uri を使用して、3つの独立した Webhook を登録できます。

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>WebHook 受信側のインストール

Microsoft ASP.NET WebHook を使用して webhook を受信するには、まず WebHook プロバイダーの Nuget パッケージをインストールします。 Nuget パッケージには、" [Microsoft.](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) .............." という名前が付けられます。最後の部分は、サポートされるサービスを示します。 次に例を示します。

ASP.NET webhook によって生成された webhook を受信するためのサポート[を提供します。](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)カスタムは、webhook によって生成される webhook の受信をサポート[し](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)ています。

既定では、Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、余裕、ストライプ、Trello、および WordPress がサポートされていますが、他の任意の数のプロバイダーをサポートすることもできます。

## <a name="configuring-a-webhook-receiver"></a>WebHook 受信側の構成

WebHook レシーバーは[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)インターフェイスによって構成され、そのインターフェイスの特定の実装は、任意の依存関係挿入モデルを使用して登録できます。 既定の実装では、web.config ファイルで設定できるアプリケーション設定が使用されます。または、Azure Web Apps を使用する場合は、 [Azure Portal](https://portal.azure.com/)で設定できます。

![Azure App Settings](_static/AzureAppSettings.png)

アプリケーション設定キーの形式は次のとおりです。

```
MS_WebHookReceiverSecret_<receiver>
```

値は、Webhook が登録されている *{id}* 値に一致する値のコンマ区切りのリストです。次に例を示します。

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>WebHook 受信側の初期化

WebHook レシーバーは、次の例のように、 *webapiconfig.cs*静的クラスに登録することによって初期化されます。

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
