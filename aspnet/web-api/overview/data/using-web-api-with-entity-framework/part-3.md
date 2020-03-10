---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Code First Migrations を使用してデータベースをシードする |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449116"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>Code First Migrations を使用してデータベースをシード処理する

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

このセクションでは、EF の[Code First Migrations](https://msdn.microsoft.com/data/jj591621)を使用して、データベースにテストデータをシードします。

**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](part-3/samples/sample1.cmd)]

このコマンドは、移行という名前のフォルダーをプロジェクトに追加し、Configuration.cs という名前のコードファイルを [移行] フォルダーに追加します。

![](part-3/_static/image1.png)

Configuration.cs ファイルを開きます。 次の**using ステートメントを**追加します。

[!code-csharp[Main](part-3/samples/sample2.cs)]

次に、次のコードを**構成の Seed**メソッドに追加します。

[!code-csharp[Main](part-3/samples/sample3.cs)]

[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](part-3/samples/sample4.cmd)]

最初のコマンドは、データベースを作成するコードを生成し、2番目のコマンドはそのコードを実行します。 データベースは、 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)を使用してローカルに作成されます。

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>API を探索する (省略可能)

F5 キーを押してデバッグ モードでアプリケーションを実行します。 Visual Studio が起動し IIS Express、web アプリが実行されます。 その後、Visual Studio によってブラウザーが起動され、アプリのホームページが開きます。

Visual Studio で web プロジェクトを実行すると、ポート番号が割り当てられます。 次の図では、ポート番号は50524です。 アプリケーションを実行すると、別のポート番号が表示されます。

![](part-3/_static/image3.png)

ホームページは、ASP.NET MVC を使用して実装されます。 ページの上部には、"API" というリンクがあります。 このリンクを使用すると、web API の自動生成されたヘルプページが表示されます。 (このヘルプページの生成方法と、独自のドキュメントをページに追加する方法については、「 [ASP.NET Web API のヘルプページの作成](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)」を参照してください)。[ヘルプ] ページのリンクをクリックすると、要求と応答の形式など、API の詳細を確認できます。

![](part-3/_static/image4.png)

この API により、データベースに対する CRUD 操作が有効になります。 API の概要を次に示します。

| Authors |  |
| --- | -- |
| GET api/authors | すべての作成者を取得します。 |
| GET api/authors/{id} | ID で作成者を取得します。 |
| POST /api/authors | 新しい作成者を作成します。 |
| PUT /api/authors/{id} | 既存の作成者を更新します。 |
| DELETE /api/authors/{id} | 作成者を削除します。 |

| 書籍 |  |
| --- | -- |
| GET /api/books | すべてのブックを取得します。 |
| GET /api/books/{id} | ID でブックを取得します。 |
| POST /api/books | 新しい本を作成します。 |
| PUT /api/books/{id} | 既存のブックを更新します。 |
| DELETE /api/books/{id} | ブックを削除します。 |

## <a name="view-the-database-optional"></a>データベースを表示する (省略可能)

データベースの更新コマンドを実行すると、EF によってデータベースが作成され、`Seed` メソッドが呼び出されます。 アプリケーションをローカルで実行すると、EF によって[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)が使用されます。 データベースは Visual Studio で表示できます。 **[表示]** メニューの **[SQL Server オブジェクト エクスプローラー]** を選択します。

![](part-3/_static/image5.png)

**[サーバーへの接続]** ダイアログの **[サーバー名]** ボックスに「(localdb) \ v11.0」と入力します。 **認証** オプションは Windows 認証 のままにします。 **[接続]** をクリックします。

![](part-3/_static/image6.png)

Visual Studio は LocalDB に接続し、[SQL Server オブジェクトエクスプローラー] ウィンドウに既存のデータベースを表示します。 ノードを展開して、EF によって作成されたテーブルを表示できます。

![](part-3/_static/image7.png)

データを表示するには、テーブルを右クリックし、 **[データの表示]** を選択します。

![](part-3/_static/image8.png)

次のスクリーンショットは、Books テーブルの結果を示しています。 EF によってシードデータがデータベースに設定され、テーブルに Authors テーブルへの外部キーが格納されていることに注意してください。

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [前へ](part-2.md)
> [次へ](part-4.md)
