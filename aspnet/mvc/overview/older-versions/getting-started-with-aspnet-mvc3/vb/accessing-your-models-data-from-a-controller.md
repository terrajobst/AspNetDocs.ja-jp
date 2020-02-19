---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457981"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a>コントローラーからモデルのデータにアクセスする (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 必要に応じC#て[ C# ](../cs/accessing-your-models-data-from-a-controller.md) 、このチュートリアルのバージョンに切り替えます。

このセクションでは、新しい `MoviesController` クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。 続行する前に、アプリケーションをビルドしてください。

*Controllers*フォルダーを右クリックし、新しい `MoviesController` コントローラーを作成します。 次のオプションを選択します。

- コントローラー名: **moviescontroller.cs**。 (これが既定値です)。
- テンプレート: **Entity Framework を使用した、読み取り/書き込みアクションとビューを備えたコントローラー**。
- モデルクラス: **Movie (MvcMovie. model)** 。
- データコンテキストクラス: **moの Dbcontext (MvcMovie. model)** 。
- Views: **Razor (CSHTML)** 。 (既定値)。

[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)

**[追加]** をクリックします。 Visual Web Developer では、次のファイルとフォルダーが作成されます。

- プロジェクトの*Controllers*フォルダー内の*moviescontroller.cs*ファイル。
- プロジェクトの*Views*フォルダー内の*ムービー*フォルダー。
- 新しい*Views\Movies*フォルダーで、Vbhtml を作成し、 *vbhtml、Details*、Vbhtml、および*を削除します*。

[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 スキャフォールディング機構により、CRUD (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されます。 これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。

アプリケーションを実行し、ブラウザーのアドレスバーの URL に */ムービー*を追加して、`Movies` コントローラーを参照します。 アプリケーションは既定のルーティング ( *global.asax*ファイルで定義されている) に依存しているため、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、`Movies` コントローラーの既定の `Index` アクションメソッドにルーティングされます。 つまり、ブラウザーの要求 `http://localhost:xxxxx/Movies` は、ブラウザーの要求 `http://localhost:xxxxx/Movies/Index`と実質的に同じです。 まだ追加していないため、結果はムービーの空の一覧になります。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a>ムービーの作成

**[Create New]\(新規作成\)** リンクを選択します。 ムービーに関する詳細を入力し、 **[作成]** ボタンをクリックします。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

**[作成]** ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。 次に *、ムービーの URL に*リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)

いくつかのムービー エントリを作成します。 **[編集]** 、 **[詳細]** 、および **[削除]** リンクを試してください。すべて機能します。

## <a name="examining-the-generated-code"></a>生成されたコードの調査

*Controllers\MoviesController.vb*ファイルを開き、生成された `Index` メソッドを確認します。 `Index` メソッドを使用したムービーコントローラーの一部を次に示します。

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

前に説明したように、`MoviesController` クラスの次の行は、ムービーデータベースコンテキストをインスタンス化します。 ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

`Movies` コントローラーに対する要求では、ムービーデータベースの `Movies` テーブル内のすべてのエントリが返され、その結果が `Index` ビューに渡されます。

## <a name="strongly-typed-models-and-the-model-keyword"></a>厳密に型指定されたモデルと @model キーワード

このチュートリアルの前半では、`ViewBag` オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました。 `ViewBag` は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。

また、ASP.NET MVC では、厳密に型指定されたデータまたはオブジェクトをビューテンプレートに渡すこともできます。 この厳密に型指定されたアプローチによって、Visual Web Developer エディターでのコードのコンパイル時チェックと IntelliSense の強化が可能になります。 ここでは、`MoviesController` クラスと*インデックスの vbhtml*ビューテンプレートでこの方法を使用しています。

`Index` アクションメソッドで `View` ヘルパーメソッドを呼び出すときに、コードによって[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)オブジェクトが作成されることに注意してください。 次に、コードはこの `Movies` リストをコントローラーからビューに渡します。

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

ビューテンプレートファイルの先頭に `@ModelType` ステートメントを含めることにより、ビューが想定するオブジェクトの型を指定できます。 ムービーコントローラーを作成したときに、Visual Web Developer によって、次の `@model` ステートメントが*インデックスの vbhtml*ファイルの先頭に自動的に追加されました。

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

この `@ModelType` ディレクティブを使用すると、厳密に型指定された `Model` オブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。 たとえば、*インデックスの vbhtml*テンプレートでは、コードは、厳密に型指定された `Model` オブジェクトに対して `foreach` ステートメントを実行して、ムービーをループします。

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

`Model` オブジェクトは厳密に型指定されているため (`IEnumerable<Movie>` オブジェクトとして)、ループ内の各 `item` オブジェクトは `Movie`として型指定されます。 その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。

[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>SQL Server Compact の操作

Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していない `Movies` データベースを指していることを検出した Code First ため、データベースは自動的に作成されます。 これが作成されたことを確認するには、 *App\_Data*フォルダーを調べます。 *ムービーの .sdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの **[すべてのファイルを表示]** ボタンをクリックし、 **[更新]** ボタンをクリックして、[ *App\_Data* ] フォルダーを展開します。

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)

[*ムービー. .sdf* ] をダブルクリックして、**サーバーエクスプローラー**を開きます。 次に、 **[テーブル]** フォルダーを展開して、データベースに作成されたテーブルを表示します。

> [!NOTE]
> [ *.Sdf*] をダブルクリックしたときにエラーが表示された場合は、 **SQL Server Compact 4.0 用の VISUAL Studio 2010 SP1 ツール**がインストールされていることを確認してください。 (本ソフトウェアのリンクについては、このチュートリアルシリーズのパート1の前提条件の一覧を参照してください)。今すぐリリースをインストールする場合は、Visual Web Developer を閉じてから再度開く必要があります。

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)

2つのテーブルがあります。1つは `Movie` エンティティセット用、もう1つは `EdmMetadata` テーブルです。 `EdmMetadata` テーブルは、モデルとデータベースが同期されていないことを判断するために Entity Framework によって使用されます。

`Movies` テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成したデータを表示します。

[![Moの安定](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)

`Movies` テーブルを右クリックし、 **[テーブルスキーマの編集]** を選択します。

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

`Movies` テーブルのスキーマが、前に作成した `Movie` クラスにどのようにマップされるかに注目してください。 このスキーマは、`Movie` クラスに基づいて自動的に作成され Code First Entity Framework ます。

終了したら、接続を閉じます。 (接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)

これで、データベースと、そのコンテンツを表示する単純なリストページが作成されました。 次のチュートリアルでは、スキャフォールディングコードの残りの部分を調べ、`SearchIndex` メソッドと、このデータベースで映画を検索できる `SearchIndex` ビューを追加します。

> [!div class="step-by-step"]
> [前へ](adding-a-model.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)
