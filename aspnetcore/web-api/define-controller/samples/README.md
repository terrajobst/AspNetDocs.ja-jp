---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024869"
---
# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="7ebaf-101">ASP.NET Core Web API コントローラーのサンプル</span><span class="sxs-lookup"><span data-stu-id="7ebaf-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="7ebaf-102">このサンプル アプリは、次のプロジェクトで構成されています。</span><span class="sxs-lookup"><span data-stu-id="7ebaf-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="7ebaf-103">\**WebApiSample.Api.22*:.NET Core 2.2 を対象とする ASP.NET Core 2.2 プロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="7ebaf-103">\**WebApiSample.Api.22*: An ASP.NET Core 2.2 project targeting .NET Core 2.2.</span></span>
- <span data-ttu-id="7ebaf-104">**WebApiSample.Api.21**:.NET Core 2.1 を対象とする ASP.NET Core 2.1 のプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="7ebaf-104">**WebApiSample.Api.21**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="7ebaf-105">**WebApiSample.Api.Pre21**:.NET Core 2.0 を対象とする ASP.NET Core 2.0 プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="7ebaf-105">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="7ebaf-106">**WebApiSample.DataAccess**:2 つの Web API プロジェクトのデータ アクセス層として機能する .NET Standard 2.0 クラス ライブラリです。</span><span class="sxs-lookup"><span data-stu-id="7ebaf-106">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="7ebaf-107">このサンプルでは、Web API コントローラー作成のバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="7ebaf-107">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="7ebaf-108">ControllerBase からクラスを派生する</span><span class="sxs-lookup"><span data-stu-id="7ebaf-108">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [<span data-ttu-id="7ebaf-109">ApiControllerAttribute でクラスに注釈を付ける</span><span class="sxs-lookup"><span data-stu-id="7ebaf-109">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
