---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024869"
---
# <a name="aspnet-core-web-api-controller-sample"></a>ASP.NET Core Web API コントローラーのサンプル

このサンプル アプリは、次のプロジェクトで構成されています。

- **WebApiSample.Api.22*:.NET Core 2.2 を対象とする ASP.NET Core 2.2 プロジェクトです。
- **WebApiSample.Api.21**:.NET Core 2.1 を対象とする ASP.NET Core 2.1 のプロジェクトです。
- **WebApiSample.Api.Pre21**:.NET Core 2.0 を対象とする ASP.NET Core 2.0 プロジェクト。
- **WebApiSample.DataAccess**:2 つの Web API プロジェクトのデータ アクセス層として機能する .NET Standard 2.0 クラス ライブラリです。

このサンプルでは、Web API コントローラー作成のバリエーションを示します。

- [ControllerBase からクラスを派生する](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [ApiControllerAttribute でクラスに注釈を付ける](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
