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
# <a name="aspnet-webhooks-logging"></a>ASP.NET Webhook のログ記録

Microsoft ASP.NET Webhook では、問題と問題を報告する方法としてログ記録を使用します。 既定では、ログは managed を使用して書き込まれます。この[トレース](https://msdn.microsoft.com/library/system.diagnostics.trace)は、他のログストリームと同様に[トレースリスナー](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)を使用して実行できます。

Web アプリケーションを Azure Web アプリとしてデプロイすると、ログは自動的に選択され、他のすべての[システム診断](https://msdn.microsoft.com/library/system.diagnostics.trace)ログと一緒に管理できます。 詳細については、「 [Azure App Service での web アプリの診断ログの有効化](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)」を参照してください。

さらに、「 [Visual studio を使用した Azure App Service での web アプリのトラブルシューティング](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)」の説明に従って、visual studio 内から直接ログを取得することもできます。

## <a name="redirecting-logs"></a>ログのリダイレクト

ログを[Log4Net](http://logging.apache.org/log4net/) [に書き込む](https://msdn.microsoft.com/library/system.diagnostics.trace)のではなく、ログマネージャーに直接ログ記録することができます。これは、ログマネージャーに直接記録することができ[ます。](http://nlog-project.org/) [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)の実装を提供し、任意の依存関係挿入エンジンに登録するだけで、webhook Microsoft ASP.NET によって取得されます。 詳細については、 [ASP.NET Web API 2 での依存関係の挿入に](https://www.asp.net/web-api/overview/advanced/dependency-injection)関する説明を参照してください。
