---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook の受信者の依存関係 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook での受信側の依存関係と依存関係の挿入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564872"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="3e52b-103">ASP.NET Webhook の受信者の依存関係</span><span class="sxs-lookup"><span data-stu-id="3e52b-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="3e52b-104">Microsoft ASP.NET Webhook は、依存関係の挿入を念頭に置いて設計されています。</span><span class="sxs-lookup"><span data-stu-id="3e52b-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="3e52b-105">システムのほとんどの依存関係は、依存関係挿入エンジンを使用して代替の実装に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="3e52b-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="3e52b-106">受信側の依存関係の一覧については、「dependencies [Encyscopeextensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3e52b-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="3e52b-107">依存関係が登録されていない場合は、既定の実装が使用されます。</span><span class="sxs-lookup"><span data-stu-id="3e52b-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="3e52b-108">既定の実装の一覧については、「 [Receiverservices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3e52b-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
