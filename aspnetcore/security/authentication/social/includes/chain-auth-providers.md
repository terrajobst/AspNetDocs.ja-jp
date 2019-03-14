---
ms.openlocfilehash: dc6c86c48cfb4dd7e27c03ae29519417e60eac5b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57168666"
---
## <a name="multiple-authentication-providers"></a><span data-ttu-id="4a7b3-101">複数の認証プロバイダー</span><span class="sxs-lookup"><span data-stu-id="4a7b3-101">Multiple authentication providers</span></span>

<span data-ttu-id="4a7b3-102">アプリが複数のプロバイダーを必要とする場合、[AddAuthentication](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication) の背後にあるプロバイダーの拡張メソッドをチェインします。</span><span class="sxs-lookup"><span data-stu-id="4a7b3-102">When the app requires multiple providers, chain the provider extension methods behind [AddAuthentication](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication):</span></span>

```csharp
services.AddAuthentication()
    .AddMicrosoftAccount(microsoftOptions => { ... })
    .AddGoogle(googleOptions => { ... })
    .AddTwitter(twitterOptions => { ... })
    .AddFacebook(facebookOptions => { ... });
```
