---
uid: webhooks/diagnostics/logging
title: ASP.NET Webhook logging |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook でログを記録する方法。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457584"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="d2ed8-103">ASP.NET Webhook のログ記録</span><span class="sxs-lookup"><span data-stu-id="d2ed8-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="d2ed8-104">Microsoft ASP.NET Webhook では、問題と問題を報告する方法としてログ記録を使用します。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="d2ed8-105">既定では、ログは managed を使用して書き込まれます。この[トレース](https://msdn.microsoft.com/library/system.diagnostics.trace)は、他のログストリームと同様に[トレースリスナー](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)を使用して実行できます。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="d2ed8-106">Web アプリケーションを Azure Web アプリとしてデプロイすると、ログは自動的に選択され、他のすべての[システム診断](https://msdn.microsoft.com/library/system.diagnostics.trace)ログと一緒に管理できます。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="d2ed8-107">詳細については、「 [Azure App Service での web アプリの診断ログの有効化](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="d2ed8-108">さらに、「 [Visual studio を使用した Azure App Service での web アプリのトラブルシューティング](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)」の説明に従って、visual studio 内から直接ログを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="d2ed8-109">ログのリダイレクト</span><span class="sxs-lookup"><span data-stu-id="d2ed8-109">Redirecting Logs</span></span>

<span data-ttu-id="d2ed8-110">ログを[Log4Net](http://logging.apache.org/log4net/) [に書き込む](https://msdn.microsoft.com/library/system.diagnostics.trace)のではなく、ログマネージャーに直接ログ記録することができます。これは、ログマネージャーに直接記録することができ[ます。](http://nlog-project.org/)</span><span class="sxs-lookup"><span data-stu-id="d2ed8-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="d2ed8-111">[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)の実装を提供し、任意の依存関係挿入エンジンに登録するだけで、webhook Microsoft ASP.NET によって取得されます。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="d2ed8-112">詳細については、 [ASP.NET Web API 2 での依存関係の挿入に](https://www.asp.net/web-api/overview/advanced/dependency-injection)関する説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2ed8-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
