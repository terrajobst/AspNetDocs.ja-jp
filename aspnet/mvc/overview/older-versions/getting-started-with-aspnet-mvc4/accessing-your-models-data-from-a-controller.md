---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456167"
---
# <a name="accessing-your-models-data-from-a-controller"></a>コントローラーからモデルのデータにアクセスする

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

このセクションでは、新しい `MoviesController` クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。

次の手順に進む前に **、アプリケーションをビルドし**ます。

*Controllers*フォルダーを右クリックし、新しい `MoviesController` コントローラーを作成します。 以下のオプションは、アプリケーションをビルドするまで表示されません。 次のオプションを選択します。

- コントローラー名: **moviescontroller.cs**。 (これが既定値です。 )
- テンプレート: **Entity Framework を使用した、読み取り/書き込みアクションとビューがある MVC コントローラー**。
- モデルクラス: **Movie (MvcMovie. model)** 。
- データコンテキストクラス: **moの Dbcontext (MvcMovie. model)** 。
- Views: **Razor (CSHTML)** 。 (既定値)。

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

**[追加]** をクリックします。 Visual Studio Express によって、次のファイルとフォルダーが作成されます。

- プロジェクトの*Controllers*フォルダー内の*MoviesController.cs*ファイル。
- プロジェクトの*Views*フォルダー内の*ムービー*フォルダー。
- 新しい*Views\Movies*フォルダーに、cshtml、Cshtml、 *Details、Edit.* cshtml、および*Index*を作成します。

ASP.NET MVC 4 では、CRUD (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されました (CRUD アクションメソッドとビューの自動作成はスキャフォールディングと呼ばれています)。 これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。

アプリケーションを実行し、ブラウザーのアドレスバーの URL に */ムービー*を追加して、`Movies` コントローラーを参照します。 アプリケーションは既定のルーティング ( *global.asax*ファイルで定義されている) に依存しているため、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、`Movies` コントローラーの既定の `Index` アクションメソッドにルーティングされます。 つまり、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、ブラウザーの要求 `http://localhost:xxxxx/Movies/Index`と実質的に同じです。 まだ追加していないため、結果はムービーの空の一覧になります。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>ムービーの作成

**[Create New]\(新規作成\)** リンクを選択します。 ムービーに関する詳細を入力し、 **[作成]** ボタンをクリックします。

![](accessing-your-models-data-from-a-controller/_static/image3.png)

**[作成]** ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。 次に *、ムービーの URL に*リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。

![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")

いくつかのムービー エントリを作成します。 **[編集]** 、 **[詳細]** 、および **[削除]** リンクを試してください。すべて機能します。

## <a name="examining-the-generated-code"></a>生成されたコードの調査

*Controllers\MoviesController.cs*ファイルを開き、生成された `Index` メソッドを確認します。 `Index` メソッドを使用したムービーコントローラーの一部を次に示します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

前に説明したように、`MoviesController` クラスの次の行は、ムービーデータベースコンテキストをインスタンス化します。 ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

`Movies` コントローラーに対する要求では、ムービーデータベースの `Movies` テーブル内のすべてのエントリが返され、その結果が `Index` ビューに渡されます。

## <a name="strongly-typed-models-and-the-model-keyword"></a>厳密に型指定されたモデルと @model キーワード

このチュートリアルの前半では、`ViewBag` オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました。 `ViewBag` は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。

また、ASP.NET MVC では、厳密に型指定されたデータまたはオブジェクトをビューテンプレートに渡すこともできます。 この厳密に型指定されたアプローチによって、Visual Studio エディターでのコードのコンパイル時のチェックと、より高度な IntelliSense が有効になります。 Visual Studio のスキャフォールディングメカニズムでは、メソッドとビューを作成するときに、`MoviesController` クラスとビューテンプレートでこの方法を使用しました。

*Controllers\MoviesController.cs*ファイルで、生成された `Details` メソッドを確認します。 `Details` メソッドを使用したムービーコントローラーの一部を次に示します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

`Movie` が見つかった場合は、`Movie` モデルのインスタンスが詳細ビューに渡されます。 *Views\Movies\Details.cshtml*ファイルの内容を確認します。

ビューテンプレートファイルの先頭に `@model` ステートメントを含めることにより、ビューが想定するオブジェクトの型を指定できます。 ムービー コントローラーを作成したとき、Visual Studio によって `@model`Details.cshtml*ファイルの先頭に* ステートメントが自動的に追加されています。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

この `@model` ディレクティブにより、厳密に型指定された `Model` オブジェクトを使って、コントローラーがビューに渡したムービーにアクセスできます。 たとえば、 *Details. cshtml*テンプレートでは、コードは各ムービーフィールドを `DisplayNameFor` に渡し、厳密に型指定された `Model` オブジェクトを使用して HTML ヘルパー[を](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx)表示します。 Create メソッドと Edit メソッドとビューテンプレートも、ムービーモデルオブジェクトを渡します。

*MoviesController.cs*ファイルで、*インデックスの cshtml*ビューテンプレートと `Index` メソッドを確認します。 `Index` アクションメソッドで `View` ヘルパーメソッドを呼び出すときに、コードによって[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)オブジェクトが作成されることに注意してください。 次に、コードはこの `Movies` リストをコントローラーからビューに渡します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

ムービーコントローラーを作成すると、Visual Studio Express によって、次の `@model` ステートメントが*Index. cshtml*ファイルの先頭に自動的に含まれます。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

この `@model` ディレクティブを使用すると、厳密に型指定された `Model` オブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。 たとえば、 *Index. cshtml*テンプレートでは、厳密に型指定された `Model` オブジェクトに対して `foreach` ステートメントを実行して、ムービーをループします。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

`Model` オブジェクトは厳密に型指定されているため (`IEnumerable<Movie>` オブジェクトとして)、ループ内の各 `item` オブジェクトは `Movie`として型指定されます。 その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB の使用

Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していない `Movies` データベースを指していることを検出した Code First ため、データベースは自動的に作成されます。 これが作成されたことを確認するには、 *App\_Data*フォルダーを調べます。 *ムービーの .mdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの **[すべてのファイルを表示]** ボタンをクリックし、最新の情報に **[更新]** ボタンをクリックして、[ *App\_Data* ] フォルダーを展開します。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

[ *.Mdf* ] をダブルクリックして**データベースエクスプローラー**を開き、 **[テーブル]** フォルダーを展開して、ムービーテーブルを表示します。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> データベースエクスプローラーが表示されない場合は、 **[ツール]** メニューの **[データベースへの接続]** をクリックし、 **[データソースの選択]** ダイアログをキャンセルします。 これにより、データベースエクスプローラーが強制的に開きます。

> [!NOTE]
> VWD または Visual Studio 2010 を使用していて、次のようなエラーが表示される場合:
> 
> - データベース ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF ' はバージョン706であるため、開くことができません。 このサーバーでは、バージョン655以前がサポートされています。 このダウングレード パスはサポートされません。
> - 指定された SqlConnection が初期カタログを指定していない&quot;、&quot;InvalidOperation Exception がユーザーコードによって処理されませんでした。
> 
> [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)と[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)をインストールする必要があります。 前のページで指定した `MovieDBContext` 接続文字列を確認します。

`Movies` テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成したデータを表示します。

![](accessing-your-models-data-from-a-controller/_static/image8.png)

`Movies` テーブルを右クリックし、 **[テーブル定義を開く]** を選択して、Entity Framework 作成 Code First テーブルの構造を確認します。

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

`Movies` テーブルのスキーマが、前に作成した `Movie` クラスにどのようにマップされるかに注目してください。 このスキーマは、`Movie` クラスに基づいて自動的に作成され Code First Entity Framework ます。

操作が完了したら、 *Mo? Dbcontext*を右クリックし、 **[接続を閉じる]** を選択して接続を閉じます。 (接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

これで、データベースと、そのコンテンツを表示する単純なリストページが作成されました。 次のチュートリアルでは、スキャフォールディングコードの残りの部分を調べ、`SearchIndex` メソッドと、このデータベースで映画を検索できる `SearchIndex` ビューを追加します。

> [!div class="step-by-step"]
> [前へ](adding-a-model.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)
