---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047129"
---
次の表で、ASP.NET Core コード ジェネレーターのパラメーターについて詳しく説明します。

| パラメーター               | 説明|
| ----------------- | ------------ |
| -m  | モデルの名前。 |
| -dc  | データ コンテキスト。 |
| -udl | 既定のレイアウトを使用します。 |
| --relativeFolderPath | ビューを作成するための相対出力フォルダー パス。 |
| --useDefaultLayout | ビューには既定のレイアウトを使用してください。 |
| --referenceScriptLibraries | [編集] および [作成] ページに `_ValidationScriptsPartial` を追加します。 |

次のように、`h` スイッチを使用して、`aspnet-codegenerator controller` コマンドに関するヘルプを取得します。

```console
dotnet aspnet-codegenerator controller -h
```