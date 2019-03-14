---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062599"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>ムービー モデルのスキャフォールディング

* コマンド ライン (*Program.cs*、*Startup.cs*、および *.csproj* ファイルを含むプロジェクト ディレクトリ) で次を実行します。

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

エラーが発生した場合は、次のようにします。
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

前のエラーは、間違ったディレクトリにいる場合に発生します。 プロジェクト ディレクトリ (*Program.cs*、*Startup.cs*、および *.csproj* ファイルを含むディレクトリ) のコマンド シェルを開いて、前のコマンドを実行します。

エラーが発生した場合は、次のようにします。
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

Visual Studio を終了し、コマンドを再度実行します。
