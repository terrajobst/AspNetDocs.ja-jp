---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: LINQ to SQL (C#) を使用したモデルクラスの作成Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、ASP.NET MVC アプリケーションのモデルクラスを作成する方法の1つについて説明することです。 このチュートリアルでは、モデル c を構築する方法について説明します。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: c27d1ffac3846fe4bc13b32c2ae91a63b2493126
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437188"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>LINQ to SQL でモデル クラスを作成する (C#)

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> このチュートリアルの目的は、ASP.NET MVC アプリケーションのモデルクラスを作成する方法の1つについて説明することです。 このチュートリアルでは、Microsoft LINQ to SQL を利用して、モデルクラスを作成し、データベースへのアクセスを実行する方法について説明します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションのモデルクラスを作成する方法の1つについて説明することです。 このチュートリアルでは、Microsoft LINQ to SQL を利用して、モデルクラスを作成し、データベースへのアクセスを実行する方法について説明します。

このチュートリアルでは、基本的なムービーデータベースアプリケーションを作成します。 まず、できるだけ最速かつ最も簡単な方法でムービーデータベースアプリケーションを作成します。 私たちは、お客様のコントローラーアクションから直接、すべてのデータアクセスを実行しています。

次に、リポジトリパターンの使用方法について説明します。 リポジトリパターンを使用するには、もう少し作業が必要です。 ただし、このパターンを採用する利点は、変更に適合し、簡単にテストできるアプリケーションを構築できることです。

## <a name="what-is-a-model-class"></a>モデルクラスとは

Mvc モデルには、MVC ビューまたは MVC コントローラーに含まれていないアプリケーションロジックがすべて含まれています。 特に、MVC モデルには、アプリケーションのビジネスとデータアクセスのロジックがすべて含まれています。

さまざまなテクノロジを使用して、データアクセスロジックを実装できます。 たとえば、Microsoft Entity Framework、NHibernate、Subsonic、または ADO.NET クラスを使用して、データアクセスクラスを構築できます。

このチュートリアルでは、LINQ to SQL を使用してデータベースのクエリと更新を行います。 LINQ to SQL には、Microsoft SQL Server データベースとの対話方法が非常に簡単に用意されています。 ただし、ASP.NET MVC フレームワークは、何らかの方法で LINQ to SQL に関連付けられていないことを理解しておくことが重要です。 ASP.NET MVC は、あらゆるデータアクセステクノロジと互換性があります。

## <a name="create-a-movie-database"></a>ムービーデータベースを作成する

このチュートリアルでは、モデルクラスを作成する方法を説明するために、単純なムービーデータベースアプリケーションを作成します。 最初の手順では、新しいデータベースを作成します。 ソリューションエクスプローラーウィンドウで App\_Data フォルダーを右クリックし、メニューオプション 追加、**新しい項目** の順に選択します。 **SQL Server データベース**テンプレートを選択して、MoviesDB という名前を付け、 **[追加]** ボタンをクリックします (図1を参照)。

[新しい SQL Server データベースを追加 ![には](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**図 01**: 新しい SQL Server データベースを追加する ([クリックすると、フルサイズの画像が表示](creating-model-classes-with-linq-to-sql-cs/_static/image3.png)される)

新しいデータベースを作成したら、[App\_Data] フォルダー内の MoviesDB ファイルをダブルクリックして、データベースを開くことができます。 MoviesDB ファイルをダブルクリックすると、[サーバーエクスプローラー] ウィンドウが開きます (図2を参照)。

[サーバーエクスプローラー] ウィンドウは、Visual Web Developer を使用するときに [データベースエクスプローラー] ウィンドウと呼ばれます。

[[サーバーエクスプローラー] ウィンドウを使用した ![](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**図 02**: サーバーエクスプローラーウィンドウの使用 ([クリックしてフルサイズの画像を表示する](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))

ここでは、映画を表すテーブルをデータベースに1つ追加する必要があります。 テーブル フォルダーを右クリックし、**新しいテーブルの追加** メニューオプションを選択します。 このメニューオプションを選択すると、テーブルデザイナーが開きます (図3を参照)。

[[サーバーエクスプローラー] ウィンドウを使用した ![](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**図 03**: テーブルデザイナー ([クリックすると、フルサイズの画像が表示](creating-model-classes-with-linq-to-sql-cs/_static/image9.png)されます)

次の列をデータベーステーブルに追加する必要があります。

| **列名** | **[データ型]** | **[NULL を許容]** |
| --- | --- | --- |
| Id | int | False |
| タイトル | Nvarchar(200) | False |
| ディレクター | Nvarchar (50) | False |

Id 列には、2つの特殊な操作を行う必要があります。 まず、テーブルデザイナーで列を選択し、キーのアイコンをクリックして、Id 列を主キー列としてマークする必要があります。 LINQ to SQL では、データベースに対して挿入または更新を実行するときに主キー列を指定する必要があります。

次に、[Id] 列を id 列としてマークする必要があります。これを行うに**は**、"id" プロパティに "Yes" という値を割り当てます (図3を参照)。 Id 列は、テーブルに新しいデータ行を追加するたびに新しい数値が自動的に割り当てられる列です。

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL クラスの作成

MVC モデルには、tblMovie データベーステーブルを表す LINQ to SQL クラスが含まれています。 これらの LINQ to SQL クラスを作成する最も簡単な方法は、モデル フォルダーを右クリックして **追加、新しい項目** の順に選択し、LINQ to SQL クラス テンプレートを選択し、**追加** ボタンをクリックします (図4を参照)。

[LINQ to SQL クラスの作成 ![](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**図 04**: LINQ to SQL クラスの作成 ([クリックすると、フルサイズの画像が表示](creating-model-classes-with-linq-to-sql-cs/_static/image12.png)される)

Movie LINQ to SQL クラスを作成するとすぐに、オブジェクトリレーショナルデザイナーが表示されます。 データベーステーブルを [サーバーエクスプローラー] ウィンドウからオブジェクトリレーショナルデザイナーにドラッグして、特定のデータベーステーブルを表す LINQ to SQL クラスを作成できます。 TblMovie database テーブルをオブジェクトリレーショナルデザイナーに追加する必要があります (図5を参照)。

[オブジェクトリレーショナルデザイナーを使用した ![](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**図 05**: オブジェクトリレーショナルデザイナーの使用 ([クリックすると、フルサイズの画像が表示](creating-model-classes-with-linq-to-sql-cs/_static/image15.png)されます)

既定では、オブジェクトリレーショナルデザイナーによって、デザイナーにドラッグしたデータベーステーブルとまったく同じ名前のクラスが作成されます。 ただし、クラス `tblMovie`を呼び出す必要はありません。 そのため、デザイナーでクラスの名前をクリックし、クラスの名前を「Movie」に変更します。

最後に、 **[保存]** ボタン (フロッピーの画像) をクリックして LINQ to SQL クラスを保存してください。 それ以外の場合、LINQ to SQL クラスはオブジェクトリレーショナルデザイナーによって生成されません。

## <a name="using-linq-to-sql-in-a-controller-action"></a>コントローラーアクションでの LINQ to SQL の使用

LINQ to SQL クラスを用意したので、次のクラスを使用してデータベースからデータを取得できます。 このセクションでは、コントローラーアクション内で LINQ to SQL クラスを直接使用する方法について説明します。 MVC ビューの tblMovies database テーブルからムービーの一覧を表示します。

まず、HomeController クラスを変更する必要があります。 このクラスは、アプリケーションの Controllers フォルダーにあります。 リスト1のクラスのようにクラスを変更します。

**リスト1– `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

リスト1の `Index()` アクションでは、LINQ to SQL DataContext クラス (`MovieDataContext`) を使用して、`MoviesDB` データベースを表します。 `MoveDataContext` クラスは、Visual Studio オブジェクトリレーショナルデザイナーによって生成されました。

`tblMovies` データベーステーブルからすべてのムービーを取得するために、DataContext に対して LINQ クエリが実行されます。 ムービーの一覧は、`movies`という名前のローカル変数に割り当てられます。 最後に、ムービーの一覧がビューデータを通じてビューに渡されます。

ムービーを表示するために、次にインデックスビューを変更する必要があります。 インデックスビューは、[`Views\Home\`] フォルダーにあります。 リスト2のビューのようにインデックスビューを更新します。

**リスト2– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

変更したインデックスビューには、ビューの上部に `<%@ import namespace %>` ディレクティブが含まれていることに注意してください。 このディレクティブは、`MvcApplication1.Models namespace`をインポートします。 ビューで `model` クラス (特に、`Movie` クラス) を使用するには、この名前空間が必要です。

リスト2のビューには、`ViewData.Model` プロパティによって表されるすべての項目を反復処理する `foreach` ループが含まれています。 `movie`ごとに `Title` プロパティの値が表示されます。

`ViewData.Model` プロパティの値が `IEnumerable`にキャストされていることに注意してください。 これは、`ViewData.Model`の内容をループするために必要です。 ここでのもう1つのオプションは、厳密に型指定された `view`を作成することです。 厳密に型指定された `view`を作成する場合は、`ViewData.Model` プロパティをビューの分離コードクラスの特定の型にキャストします。

`HomeController` クラスとインデックスビューを変更した後にアプリケーションを実行すると、空白のページが表示されます。 `tblMovies` データベーステーブルにムービーレコードがないため、空白のページが表示されます。

レコードを `tblMovies` データベーステーブルに追加するには、サーバーエクスプローラーウィンドウ (Visual Web Developer のデータベースエクスプローラーウィンドウ) で `tblMovies` データベーステーブルを右クリックし、[テーブルデータの表示] メニューオプションを選択します。 表示されるグリッドを使用して `movie` レコードを挿入できます (図6を参照)。

[ムービーの挿入 ![](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**図 06**: ムービーの挿入 ([クリックすると、フルサイズの画像が表示](creating-model-classes-with-linq-to-sql-cs/_static/image18.png)される)

`tblMovies` テーブルにいくつかのデータベースレコードを追加し、アプリケーションを実行すると、図7にそのページが表示されます。 すべてのムービーデータベースレコードが箇条書きの一覧に表示されます。

[インデックスビューで映画を表示 ![には](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**図 07**: インデックスビューを使用した映画の表示 ([クリックすると、フルサイズの画像が表示](creating-model-classes-with-linq-to-sql-cs/_static/image21.png)されます)

## <a name="using-the-repository-pattern"></a>リポジトリパターンの使用

前のセクションでは、コントローラーアクション内で LINQ to SQL クラスを直接使用しています。 `Index()` controller アクションから、`MovieDataContext` クラスを直接使用しています。 単純なアプリケーションの場合は、この操作に問題はありません。 ただし、コントローラークラスの LINQ to SQL を直接操作すると、より複雑なアプリケーションを構築する必要がある場合に問題が発生します。

コントローラークラス内で LINQ to SQL を使用すると、将来、データアクセステクノロジを切り替えることが困難になります。 たとえば、Microsoft LINQ to SQL の使用から、データアクセステクノロジとして Microsoft Entity Framework の使用に切り替えることができます。 その場合は、アプリケーション内のデータベースにアクセスするすべてのコントローラーを書き直す必要があります。

コントローラークラス内で LINQ to SQL を使用すると、アプリケーションの単体テストを作成することが難しくなります。 通常、単体テストを実行するときにデータベースと対話する必要はありません。 単体テストを使用して、データベースサーバーではなくアプリケーションロジックをテストします。

将来の変更に適応性があり、より簡単にテストできる MVC アプリケーションを構築するには、リポジトリパターンの使用を検討する必要があります。 リポジトリパターンを使用する場合は、すべてのデータベースアクセスロジックを含む個別のリポジトリクラスを作成します。

リポジトリクラスを作成するときに、リポジトリクラスによって使用されるすべてのメソッドを表すインターフェイスを作成します。 コントローラー内では、リポジトリではなく、インターフェイスに対してコードを記述します。 これにより、将来、さまざまなデータアクセステクノロジを使用してリポジトリを実装できます。

リスト3のインターフェイスには `IMovieRepository` という名前が付けられ、`ListAll()`という名前の1つのメソッドを表します。

**リスト3– `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

リスト4のリポジトリクラスは、`IMovieRepository` インターフェイスを実装します。 これには、`IMovieRepository` インターフェイスで必要なメソッドに対応する `ListAll()` という名前のメソッドが含まれていることに注意してください。

**リスト4– `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

最後に、リスト5の `MoviesController` クラスは、リポジトリパターンを使用します。 LINQ to SQL クラスを直接使用しなくなりました。

**リスト5– `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

リスト5の `MoviesController` クラスに2つのコンストラクターがあることに注意してください。 最初のコンストラクター (パラメーターなしのコンストラクター) は、アプリケーションの実行時に呼び出されます。 このコンストラクターは `MovieRepository` クラスのインスタンスを作成し、2番目のコンストラクターに渡します。

2番目のコンストラクターには、パラメーターとして `IMovieRepository` パラメーターが1つあります。 このコンストラクターは、パラメーターの値を `_repository`という名前のクラスレベルのフィールドに単純に代入します。

`MoviesController` クラスは、依存関係挿入パターンと呼ばれるソフトウェア設計パターンを利用しています。 特に、コンストラクター依存関係の挿入と呼ばれるものを使用しています。 このパターンの詳細については、Martin Fowler で次の記事を参照してください。

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

`MoviesController` クラスのすべてのコード (最初のコンストラクターを除く) は、実際の `MovieRepository` クラスではなく、`IMovieRepository` インターフェイスと対話します。 このコードは、インターフェイスの具象実装ではなく、抽象インターフェイスと対話します。

アプリケーションで使用されるデータアクセステクノロジを変更する場合は、別のデータベースアクセステクノロジを使用するクラスを使用して `IMovieRepository` インターフェイスを実装するだけで済みます。 たとえば、`EntityFrameworkMovieRepository` クラスまたは `SubSonicMovieRepository` クラスを作成できます。 コントローラークラスはインターフェイスに対してプログラミングされているため、`IMovieRepository` の新しい実装をコントローラークラスに渡すことができ、クラスは引き続き機能します。

さらに、`MoviesController` クラスをテストする場合は、偽のムービーリポジトリクラスを `HomeController`に渡すことができます。 `IMovieRepository` クラスは、実際にはデータベースにアクセスしないが、`IMovieRepository` インターフェイスに必要なすべてのメソッドを含むクラスを使用して実装できます。 そうすることで、実際のデータベースに実際にアクセスすることなく、`MoviesController` クラスの単体テストを行うことができます。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、Microsoft LINQ to SQL を利用して、MVC モデルクラスを作成する方法を説明することでした。 ASP.NET MVC アプリケーションでデータベースデータを表示するための2つの方法を検討しています。 まず、LINQ to SQL クラスを作成し、コントローラーアクション内でクラスを直接使用しました。 コントローラー内で LINQ to SQL クラスを使用すると、MVC アプリケーションでデータベースデータをすばやく簡単に表示できます。

次に、データベースデータを表示するための好循環のパスを少し複雑にしました。 リポジトリパターンを利用し、すべてのデータベースアクセスロジックを別のリポジトリクラスに配置しました。 このコントローラーでは、具象クラスではなく、すべてのコードをインターフェイスに対して記述しました。 リポジトリパターンの利点は、将来的にデータベースアクセステクノロジを簡単に変更できることと、コントローラークラスを簡単にテストできることです。

> [!div class="step-by-step"]
> [前へ](creating-model-classes-with-the-entity-framework-cs.md)
> [次へ](displaying-a-table-of-database-data-cs.md)
