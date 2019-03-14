---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044079"
---
## <a name="add-initial-migration-and-update-the-database"></a>最初の移行を追加して、データベースの更新

* コマンド プロンプトを開き、プロジェクト ディレクトリに移動します。 (ディレクトリを含む、 *Startup.cs*ファイル)。

* コマンド プロンプトで次のコマンドを実行します。

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  [.NET core](/dotnet/core/tools/index) .NET のクロスプラット フォーム対応の実装です。 これらのコマンドの実行内容を次に示します。

  * [dotnet restore](/dotnet/core/tools/dotnet-restore):指定された NuGet パッケージをダウンロード、 *.csproj*ファイル。
  * `dotnet ef migrations add Initial` Entity Framework の .NET Core CLI の移行コマンドを実行し、最初の移行を作成します。 パラメーターの"add"後では、移行に割り当てる名前です。 ここで名前を付ける移行「初期」初期データベースの移行があるためです。 この操作を作成、 */データの移行/\<日付と時刻 > _Initial.cs*ファイルを追加する、移行コマンドを含む、*ムービー*テーブルがデータベースにします。
  * `dotnet ef database update`  先ほど作成した移行では、データベースを更新します。

データベースと接続文字列について次のチュートリアルでします。 データ モデルの変更について説明します、[フィールドを追加する](xref:tutorials/first-mvc-app/new-field)チュートリアル。
