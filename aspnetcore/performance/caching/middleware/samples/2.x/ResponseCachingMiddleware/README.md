---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062719"
---
# <a name="aspnet-core-response-caching-sample"></a>ASP.NET Core の応答キャッシュのサンプル

このサンプルは、ASP.NET Core の使用方法を示します[応答キャッシュ ミドルウェア](https://docs.microsoft.com/aspnet/core/performance/caching/middleware)します。

そのインデックス ページのアプリの応答を含む、`Cache-Control`ヘッダー キャッシュの動作を構成します。 また、アプリ、設定、`Vary`場合にのみ応答を処理するためにキャッシュを構成するヘッダー、`Accept-Encoding`を指定する元の要求からの後続の要求のヘッダーと一致します。

サンプルを実行するときに、インデックス ページは保存され、最大で 10 秒間キャッシュにキャッシュから提供されます。
