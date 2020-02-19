---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 接続文字列を作成し SQL Server LocalDB | を操作するMicrosoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456518"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>接続文字列の作成と SQL Server LocalDB の使用

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>接続文字列の作成と SQL Server LocalDB の使用

作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。 ただし、接続先のデータベースを指定する方法について質問することもできます。 実際には、使用するデータベースを指定する必要はありません。 Entity Framework 既定で[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)が使用されます。 このセクションで*は、アプリケーションの web.config ファイルに*接続文字列を明示的に追加します。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)は、オンデマンドで開始され、ユーザーモードで実行される SQL Server Express データベースエンジンの軽量バージョンです。 LocalDB は、 *.mdf*ファイルとしてデータベースを操作できるようにする SQL Server Express の特別な実行モードで実行されます。 通常、LocalDB データベースファイルは、web プロジェクトの*App\_Data*フォルダーに保持されます。

SQL Server Express は、運用 web アプリケーションでは使用しないことをお勧めします。 特に LocalDB は、IIS で動作するように設計されていないため、web アプリケーションを使用した運用環境では使用しないでください。 ただし、LocalDB データベースは、SQL Server または SQL Azure に簡単に移行できます。

Visual Studio 2017 では、LocalDB は既定で Visual Studio と共にインストールされます。

既定では、Entity Framework は、オブジェクトコンテキストクラス (このプロジェクトの`MovieDBContext`) と同じ名前の接続文字列を検索します。 詳細については、「 [SQL Server ASP.NET Web Applications の接続文字列」を](https://msdn.microsoft.com/library/jj653752.aspx)参照してください。

次に示すように、*アプリケーションルートの web.config ファイル*を開きます。 ( *Views*フォルダー*内の web.config ファイルで*はありません)。

![](creating-a-connection-string/_static/image1.png)

`<connectionStrings>` 要素を検索します。

![](creating-a-connection-string/_static/image2.png)

次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

2つの接続文字列はよく似ています。 最初の接続文字列には `DefaultConnection` という名前が付けられ、メンバーシップデータベースでアプリケーションにアクセスできるユーザーを制御するために使用されます。 追加した接続文字列によって、 *App\_Data*フォルダーにある、 *Movie*という名前の LocalDB データベースが指定されます。 このチュートリアルではメンバーシップデータベースを使用しません。メンバーシップ、認証、およびセキュリティの詳細については、「 [ASP.NET MVC アプリを認証および SQL DB で作成する」と「Azure App Service に配置する](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」を参照してください。

接続文字列の名前は、 [Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)クラスの名前と一致している必要があります。

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

実際には、`MovieDBContext` 接続文字列を追加する必要はありません。 接続文字列を指定しない場合、Entity Framework によって、 [Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)クラス (この場合 `MvcMovie.Models.MovieDBContext`) の完全修飾名を持つ LocalDB データベースが users ディレクトリに作成されます。 データベースには、が含まれている限り、任意の名前を指定でき*ます。MDF*サフィックス。 たとえば、データベースに*Myfilms .mdf*という名前を指定できます。

次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。

> [!div class="step-by-step"]
> [前へ](adding-a-model.md)
> [次へ](accessing-your-models-data-from-a-controller.md)
