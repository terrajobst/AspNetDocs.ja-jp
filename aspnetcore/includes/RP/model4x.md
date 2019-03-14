---
ms.openlocfilehash: d875717d480fe234ac5a328493fcec6a268e37a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039519"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>ムービー モデルのスキャフォールディング

* コマンド ライン (*Program.cs*、*Startup.cs*、および *.csproj* ファイルを含むプロジェクト ディレクトリ) で次を実行します。

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

エラーが発生した場合は、次のようにします。
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

プロジェクト ディレクトリ (*Program.cs*、*Startup.cs*、および *.csproj* ファイルを含むディレクトリ) のコマンド シェルを開きます。
