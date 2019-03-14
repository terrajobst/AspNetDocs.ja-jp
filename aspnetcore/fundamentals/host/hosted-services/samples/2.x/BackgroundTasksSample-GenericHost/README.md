---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056489"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="314be-101">ASP.NET Core のバックグラウンド タスクのサンプル (汎用ホスト)</span><span class="sxs-lookup"><span data-stu-id="314be-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="314be-102">このサンプルでは、[IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice) の使用方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="314be-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="314be-103">このサンプルでは、「[ASP.NET Core でホステッド サービスを使用するバックグラウンド タスク](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services)」トピックで説明されている機能を示します。</span><span class="sxs-lookup"><span data-stu-id="314be-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="314be-104">[Visual Studio Code](https://code.visualstudio.com/) でサンプルを実行する場合は、*.vscode/launch.json* 内のコンソールの構成の **console** の値を、`externalTerminal` か `integratedTerminal` のいずれかに設定します。</span><span class="sxs-lookup"><span data-stu-id="314be-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="314be-105">`internalConsole` の使用は、バックグラウンド作業項目をエンキューするためにアプリが使用するコンソールのキー操作入力と互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="314be-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
