---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 5d882d765133d32d3acdba9ffb5d43b69119a273
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499228"
---
# <a name="accessing-your-models-data-from-a-controller"></a>コントローラーからモデルのデータにアクセスする

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

このセクションでは、新しい `MoviesController` クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。

次の手順に進む前に **、アプリケーションをビルドし**ます。 アプリケーションをビルドしないと、コントローラーを追加するときにエラーが表示されます。

ソリューションエクスプローラーで、 *Controllers*フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** の順にクリックします。

![](accessing-your-models-data-from-a-controller/_static/image1.png)

**[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 Controller with views]** をクリックし、Entity Framework をクリックして、 **[追加]** をクリックします。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- モデルクラスの **[ムービー (MvcMovie)]** を選択します。
- データコンテキストクラスの**Mo? Dbcontext (MvcMovie. model)** を選択します。
- コントローラー名として「 **moviescontroller.cs**」と入力します。

  次の図は、完成したダイアログを示しています。  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

**[追加]** をクリックします。 (エラーが発生した場合は、コントローラーの追加を開始する前にアプリケーションをビルドしていないことがあります)。Visual Studio では、次のファイルとフォルダーが作成されます。

- *Controllers*フォルダー内の*MoviesController.cs*ファイル。
- *Views\Movies*フォルダー。
- 新しい*Views\Movies*フォルダーに、cshtml、Cshtml、 *Details、Edit.* cshtml、および*Index*を作成します。

Visual Studio では、 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されます (crud アクションメソッドとビューの自動作成はスキャフォールディングと呼ばれます)。 これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。

アプリケーションを実行し、 **[MVC ムービー]** リンクをクリックします (または、ブラウザーのアドレスバーの URL に */ムービー*を追加して、`Movies` コントローラーを参照します)。 アプリケーションは既定のルーティング (*アプリ\_Start\RouteConfig.cs*ファイルで定義されている) に依存しているため、ブラウザーの要求 `http://localhost:xxxxx/Movies` は `Movies` コントローラーの既定の `Index` アクションメソッドにルーティングされます。 つまり、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、ブラウザーの要求 `http://localhost:xxxxx/Movies/Index`と実質的に同じです。 まだ追加していないため、結果はムービーの空の一覧になります。

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>ムービーの作成

**[Create New]\(新規作成\)** リンクを選択します。 ムービーに関する詳細を入力し、 **[作成]** ボタンをクリックします。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> 価格フィールドに小数点またはコンマを入力することはできません。 小数点に対してコンマ (&quot;、&quot;) を使用する英語以外のロケール、および米国英語以外の日付形式に対して jQuery 検証をサポートするには、`Globalize.parseFloat`を使用するように、*グローバライズ*および特定の*カルチャ/グローバライズ*ファイル ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize)から)、および JavaScript を含める必要があります。 これを行う方法については、次のチュートリアルで説明します。 ここでは、単に 10 のような整数を入力します。

**[作成]** ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。 次に *、ムービーの URL に*リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

いくつかのムービー エントリを作成します。 **[編集]** 、 **[詳細]** 、および **[削除]** リンクを試してください。すべて機能します。

## <a name="examining-the-generated-code"></a>生成されたコードの調査

*Controllers\MoviesController.cs*ファイルを開き、生成された `Index` メソッドを確認します。 `Index` メソッドを使用したムービーコントローラーの一部を次に示します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

`Movies` コントローラーに対する要求では、`Movies` テーブル内のすべてのエントリが返され、その結果が `Index` ビューに渡されます。 前に説明したように、`MoviesController` クラスの次の行は、ムービーデータベースコンテキストをインスタンス化します。 ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>厳密に型指定されたモデルと @model キーワード

このチュートリアルの前半では、`ViewBag` オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました。 `ViewBag` は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。

MVC では、*厳密*に型指定されたオブジェクトをビューテンプレートに渡すこともできます。 この厳密に型指定されたアプローチによって、Visual Studio エディターでのコードのコンパイル時のチェックと、より高度な[IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx)が有効になります。 Visual Studio のスキャフォールディング機構では、メソッドとビューを作成するときに、この方法 (*厳密*に型指定されたモデルを渡す) を `MoviesController` クラスおよびビューテンプレートと共に使用しました。

*Controllers\MoviesController.cs*ファイルで、生成された `Details` メソッドを確認します。 `Details` メソッドを次に示します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id` パラメーターは通常、ルートデータとして渡されます。たとえば、`http://localhost:1234/movies/details/1` によってコントローラーがムービーコントローラーに設定され、アクションが `details`、`id` が1に設定されます。 次のように、クエリ文字列を使用して id を渡すこともできます。

`http://localhost:1234/movies/details?id=1`

`Movie` が見つかった場合、`Movie` モデルのインスタンスが `Details` ビューに渡されます。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

*Views\Movies\Details.cshtml*ファイルの内容を確認します。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

ビューテンプレートファイルの先頭に `@model` ステートメントを含めることにより、ビューが想定するオブジェクトの型を指定できます。 ムービー コントローラーを作成したとき、Visual Studio によって `@model`Details.cshtml*ファイルの先頭に* ステートメントが自動的に追加されています。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

この `@model` ディレクティブにより、厳密に型指定された `Model` オブジェクトを使って、コントローラーがビューに渡したムービーにアクセスできます。 たとえば、 *Details. cshtml*テンプレートでは、コードは各ムービーフィールドを `DisplayNameFor` に渡し、厳密に型指定された `Model` オブジェクトを使用して HTML ヘルパー[を](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx)表示します。 `Create` メソッドと `Edit` メソッドとビューテンプレートも、ムービーモデルオブジェクトを渡します。

*MoviesController.cs*ファイルで、*インデックスの cshtml*ビューテンプレートと `Index` メソッドを確認します。 `Index` アクションメソッドで `View` ヘルパーメソッドを呼び出すときに、コードによって[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)オブジェクトが作成されることに注意してください。 次に、コードはこの `Movies` リストを `Index` アクションメソッドからビューに渡します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

ムービーコントローラーを作成すると、Visual Studio によって、次の `@model` ステートメントが*Index. cshtml*ファイルの先頭に自動的に含まれます。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

この `@model` ディレクティブを使用すると、厳密に型指定された `Model` オブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。 たとえば、 *Index. cshtml*テンプレートでは、厳密に型指定された `Model` オブジェクトに対して `foreach` ステートメントを実行して、ムービーをループします。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

`Model` オブジェクトは厳密に型指定されているため (`IEnumerable<Movie>` オブジェクトとして)、ループ内の各 `item` オブジェクトは `Movie`として型指定されます。 その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB の使用

Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していない `Movies` データベースを指していることを検出した Code First ため、データベースは自動的に作成されます。 これが作成されたことを確認するには、 *App\_Data*フォルダーを調べます。 *ムービーの .mdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの **[すべてのファイルを表示]** ボタンをクリックし、最新の情報に **[更新]** ボタンをクリックして、[ *App\_Data* ] フォルダーを展開します。

![](accessing-your-models-data-from-a-controller/_static/image9.png)

[ *.Mdf* ] をダブルクリックして**サーバーエクスプローラー**を開き、 **[テーブル]** フォルダーを展開して、ムービーテーブルを表示します。 [ID] の横にあるキーアイコンに注意してください。 既定では、EF は、ID という名前のプロパティを主キーとして作成します。 EF と MVC の詳細については、「Tom Dykstra's [mvc と ef](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)の優れたチュートリアル」を参照してください。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

`Movies` テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成したデータを表示します。

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

`Movies` テーブルを右クリックし、 **[テーブル定義を開く]** を選択して、Entity Framework 作成 Code First テーブルの構造を確認します。

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

`Movies` テーブルのスキーマが、前に作成した `Movie` クラスにどのようにマップされるかに注目してください。 このスキーマは、`Movie` クラスに基づいて自動的に作成され Code First Entity Framework ます。

操作が完了したら、 *Mo? Dbcontext*を右クリックし、 **[接続を閉じる]** を選択して接続を閉じます。 (接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

これで、データを表示、編集、更新および削除できるデータベースができました。 次のチュートリアルでは、スキャフォールディングコードの残りの部分を調べ、`SearchIndex` メソッドと、このデータベースで映画を検索できる `SearchIndex` ビューを追加します。 MVC での Entity Framework の使用の詳細については、「 [ASP.NET MVC アプリケーションの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](creating-a-connection-string.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)
