---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した並べ替え、フィルター処理、およびページング (3/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b1ddb70805dcb07fb60eea895ff572c054bde5c6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595233"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>ASP.NET MVC アプリケーションでの Entity Framework を使用した並べ替え、フィルター処理、およびページング (3/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、`Student` エンティティに対する基本的な CRUD 操作用の一連の web ページを実装しています。 このチュートリアルでは、並べ替え、フィルター処理、およびページング機能を**Students**インデックスページに追加します。 単純なグループ化を実行するページも作成します。

次の図は、作業が終了したときにページがどのように表示されるかを示しています。 列見出しとは、ユーザーがクリックしてその列で並べ替えを行うことができるリンクです。 列見出しを繰り返しクリックすると、昇順と降順の並べ替え順序が切り替えられます。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>Students インデックス ページに列の並べ替えリンクを追加する

学生用インデックスページに並べ替えを追加するには、`Student` コントローラーの `Index` メソッドを変更し、`Student` インデックスビューにコードを追加します。

### <a name="add-sorting-functionality-to-the-index-method"></a>Index メソッドに並べ替え機能を追加する

*Controllers\StudentController.cs*で、`Index` メソッドを次のコードに置き換えます。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

このコードは、URL 内の文字列から `sortOrder` パラメーターを受け取ります。 クエリ文字列値は、ASP.NET MVC によってアクションメソッドのパラメーターとして提供されます。 パラメータは、"Name" または "Date" という文字列で、その後に必要に応じてアンダースコアと降順を指定する文字列 "desc" が続きます。 既定の並べ替え順序は昇順です。

インデックス ページが初めて要求されたときには、クエリ文字列はありません。 学生は、`LastName`によって昇順に表示されます。これは、`switch` ステートメントのフォールスルーケースによって確立される既定の設定です。 ユーザーが列見出しハイパーリンクをクリックすると、適切な `sortOrder` 値がクエリ文字列で提供されます。

次の2つの `ViewBag` 変数を使用して、ビューが列見出しのハイパーリンクと適切なクエリ文字列値を構成できるようにします。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

これらは、三項ステートメントです。 最初のパラメーターでは、`sortOrder` パラメーターが null または空の場合、`ViewBag.NameSortParm` を "name\_desc" に設定する必要があることを指定します。それ以外の場合は、空の文字列に設定する必要があります。 これらの 2 つのステートメントを使用して、次のようにビューで列見出しのハイパーリンクの設定することができます。

| 既定の並べ替え順 | 姓のハイパーリンク | 日付のハイパーリンク |
| --- | --- | --- |
| 姓の昇順 | descending | ascending |
| 姓の降順 | ascending | ascending |
| 日付の昇順 | ascending | descending |
| 日付の降順 | ascending | ascending |

このメソッドは[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)を使用して、並べ替えの基準となる列を指定します。 このコードは、`switch` ステートメントの前に[IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)変数を作成し、`switch` ステートメントで変更し、`switch` ステートメントの後に `ToList` メソッドを呼び出します。 `IQueryable` 変数を作成および変更するときに、データベースに送信されるクエリはありません。 `ToList`などのメソッドを呼び出すことによって `IQueryable` オブジェクトをコレクションに変換するまで、クエリは実行されません。 このため、このコードでは、`return View` ステートメントまで実行されない1つのクエリが生成されます。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>列見出しのハイパーリンクを Student インデックスビューに追加する

*Views\Student\Index.cshtml*で、見出し行の `<tr>` と `<th>` の要素を、強調表示されたコードに置き換えます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

このコードでは、`ViewBag` プロパティの情報を使用して、適切なクエリ文字列値を持つハイパーリンクを設定します。

ページを実行し、 **[Last Name]** と **[Enrollment Date]** 列見出しをクリックして、並べ替えが機能することを確認します。

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

**最後の名前**の見出しをクリックすると、学生が姓の降順で表示されます。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>Students インデックスページに検索ボックスを追加する

Students インデックス ページにフィルターを追加するには、テキスト ボックスと送信ボタンをビューに追加し、`Index` メソッドで対応する変更を行います。 テキスト ボックスを使用して、姓と名のフィールドに検索する文字列を入力できます。

### <a name="add-filtering-functionality-to-the-index-method"></a>Index メソッドにフィルター機能を追加する

*Controllers\StudentController.cs*で、`Index` メソッドを次のコードに置き換えます (変更は強調表示されています)。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

`searchString` パラメーターを `Index` メソッドに追加しました。 また、LINQ ステートメント `where` 句を追加しました。この句は、名または姓に検索文字列が含まれている学生だけを選択します。 検索文字列の値は、インデックスビューに追加するテキストボックスから受け取ります。[Where](https://msdn.microsoft.com/library/bb535040.aspx)句を追加するステートメントは、検索する値がある場合にのみ実行されます。

> [!NOTE]
> 多くの場合、Entity Framework のエンティティセットまたはメモリ内のコレクションの拡張メソッドとして、同じメソッドを呼び出すことができます。 通常、結果は同じですが、場合によっては異なる場合があります。 たとえば、`Contains` メソッドの .NET Framework 実装では、空の文字列を渡すとすべての行が返されますが、SQL Server Compact 4.0 の Entity Framework プロバイダーは空の文字列に対して0行を返します。 したがって、この例のコード (`if` ステートメント内に `Where` ステートメントを記述する) を使用すると、すべてのバージョンの SQL Server に対して同じ結果が得られるようになります。 また、`Contains` メソッドの .NET Framework 実装では、既定で大文字と小文字を区別した比較が実行されますが、Entity Framework SQL Server プロバイダーは既定で大文字と小文字を区別しない比較を実行します。 したがって、`ToUpper` メソッドを呼び出してテストを明示的に大文字と小文字を区別しないようにすると、後でリポジトリを使用するようにコードを変更したときに結果が変更されないようにすることができます。これにより、`IQueryable` オブジェクトではなく `IEnumerable` コレクションが返されます。 (`IEnumerable` コレクションに対して `Contains` メソッドを呼び出したときには、.NET Framework の実装を取得します。`IQueryable` オブジェクトに対して呼び出したときには、データベース プロバイダーの実装を取得します)。

### <a name="add-a-search-box-to-the-student-index-view"></a>Students インデックス ビューに [検索] ボックスを追加する

*Views\Student\Index.cshtml*で、キャプション、テキストボックス、および**検索**ボタンを作成するために、開始 `table` タグの直前に強調表示されているコードを追加します。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

ページを実行し、検索文字列を入力して **[検索]** をクリックし、フィルター処理が機能していることを確認します。

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

URL に "an" という検索文字列が含まれていないことに注意してください。つまり、このページにブックマークを指定すると、ブックマークを使用するとフィルター処理された一覧が表示されません。 このチュートリアルの後の方で、フィルター条件にクエリ文字列を使用するように **[検索]** ボタンを変更します。

## <a name="add-paging-to-the-students-index-page"></a>Students インデックスページにページングを追加する

Students インデックスページにページングを追加するには、まず**PagedList** NuGet パッケージをインストールします。 次に、`Index` メソッドに追加の変更を加え、ページングリンクを `Index` ビューに追加します。 **PagedList**は、ASP.NET Mvc 用の多くの優れたページングおよび並べ替えパッケージの1つです。この使用方法は、他のオプションよりも推奨されるものではなく、例としてのみ使用することを目的としています。 次の図は、ページングリンクを示しています。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList NuGet パッケージをインストールする

NuGet **PagedList**パッケージは、 **PagedList**パッケージを依存関係として自動的にインストールします。 **PagedList**パッケージは `IQueryable` コレクションと `IEnumerable` コレクションの `PagedList` コレクション型および拡張メソッドをインストールします。 拡張メソッドは、`IQueryable` または `IEnumerable`から `PagedList` コレクション内の1ページのデータを作成します。 `PagedList` コレクションには、ページングを容易にするいくつかのプロパティとメソッドが用意されています。 **PagedList**パッケージは、ページングボタンを表示するページングヘルパーをインストールします。

**[ツール]** メニューの **[nuget パッケージマネージャー]** を選択し、 **[ソリューションの nuget パッケージの管理]** をクリックします。

**[NuGet パッケージの管理]** ダイアログボックスで、左側の **[オンライン]** タブをクリックし、検索ボックスに「ページ」と入力します。 **PagedList**パッケージが表示されたら、 **[インストール]** をクリックします。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

**[プロジェクトの選択]** ボックスで、[ **OK]** をクリックします。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>Index メソッドにページング機能を追加する

*Controllers\StudentController.cs*で、`PagedList` 名前空間の `using` ステートメントを追加します。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` メソッドを次のコードで置き換えます。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

次に示すように、このコードでは、`page` パラメーター、現在の並べ替え順序パラメーター、および現在のフィルターパラメーターをメソッドシグネチャに追加します。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

最初にページが表示されるとき、またはユーザーがページングや並べ替えのリンクをクリックしていない場合、すべてのパラメーターは null になります。 ページングリンクがクリックされると、`page` 変数に表示するページ番号が含まれます。

ページング中に並べ替え順序を維持するためにページングリンクに含める必要があるため、`A ViewBag` プロパティは現在の並べ替え順序でビューを提供します。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

もう1つのプロパティである `ViewBag.CurrentFilter`は、現在のフィルター文字列を使用してビューを提供します。 ページング中にフィルターの設定を維持するために、ページングのリンクにこの値を含める必要があり、ページが再表示されるときに、この値をテキスト ボックスに復元する必要があります。 ページングの中に検索文字列を変更した場合は、新しいフィルターのために別のデータが表示されるため、ページを 1 にリセットする必要があります。 テキストボックスに値を入力し、[送信] ボタンを押すと、検索文字列が変更されます。 この場合、`searchString` パラメーターは null ではありません。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

メソッドの末尾で、students `IQueryable` オブジェクトの `ToPagedList` 拡張メソッドは、ページングをサポートするコレクション型の生徒の1ページに学生クエリを変換します。 これにより、学生の1つのページがビューに渡されます。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` メソッドは、ページ番号を受け取ります。 2つの疑問符は、 [null 合体演算子](https://msdn.microsoft.com/library/ms173224.aspx)を表します。 null 合体演算子は null 許容型の既定値を定義します。式 `(page ?? 1)` は、値がある場合は `page` の値を返し、`page` が null の場合は 1 を返すことを意味します。

### <a name="add-paging-links-to-the-student-index-view"></a>Student インデックスビューにページングリンクを追加する

*Views\Student\Index.cshtml*で、既存のコードを次のコードに置き換えます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

ページの上部にある `@model` ステートメントは、ビューが `List` オブジェクトの代わりに `PagedList` オブジェクトを取得するようになったことを指定します。

`PagedList.Mvc` の `using` ステートメントを使用すると、[ページング] ボタンの MVC ヘルパーにアクセスできます。

このコードでは、 [Beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)のオーバーロードを使用して、 [Formmethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)を指定できます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

既定の[Beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)は POST を使用してフォームデータを送信します。つまり、パラメーターは URL ではなく、クエリ文字列として渡されます。 HTTP GET を指定すると、フォーム データがクエリ文字列として URL で渡され、ユーザーが URL をブックマークできるようになります。 [HTTP get を使用する場合の W3C ガイドライン](http://www.w3.org/2001/tag/doc/whenToUseGet.html)では、アクションによって更新が行われない場合に GET を使用する必要があることを指定しています。

テキストボックスは現在の検索文字列で初期化されるため、新しいページをクリックすると、現在の検索文字列を確認できます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

列ヘッダーへのリンクは、フィルターの結果内でユーザーが並べ替えられるように、クエリ文字列を使用してコントローラーに現在の検索文字列を渡します。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

現在のページとページの合計数が表示されます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

表示するページがない場合は、"Page 0 of 0" が表示されます。 (この場合、ページ番号はページ数よりも大きくなります。 `Model.PageNumber` が1で、`Model.PageCount` が0であるためです)。

ページングボタンは `PagedListPager` ヘルパーによって表示されます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager` helper には、Url やスタイルなど、カスタマイズできるさまざまなオプションが用意されています。 詳細については、GitHub サイトの「 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 」を参照してください。

ページを実行します。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

異なる並べ替え順でページングのリンクをクリックし、ページングが機能することを確認します。 その後で、検索文字列を入力して、ページングをもう一度試し、並べ替えとフィルター処理を使用してもページングが正しく機能することを確認します。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>学生の統計情報を表示する About ページを作成する

Contoso 大学の web サイトの [About] ページには、登録日ごとに登録された学生の数が表示されます。 これには、グループ化とグループに関する簡単な計算が必要です。 これを実行するためには、次の手順を実行します。

- ビューに渡す必要があるデータのビュー モデル クラスを作成します。
- `Home` コントローラーの `About` メソッドを変更します。
- `About` ビューを変更します。

### <a name="create-the-view-model"></a>ビューモデルを作成する

*Viewmodel*フォルダーを作成します。 そのフォルダーで、クラスファイル*EnrollmentDateGroup.cs*を追加し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Home コントローラーを変更する

*HomeController.cs*で、ファイルの先頭に次の `using` ステートメントを追加します。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

クラスの左中かっこの直後に、データベースコンテキストのクラス変数を追加します。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

`About` メソッドを次のコードで置き換えます。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ ステートメントは、登録日で受講者エンティティをグループ化し、各グループ内のエンティティの数を計算して、結果を `EnrollmentDateGroup` ビュー モデル オブジェクトのコレクションに格納します。

`Dispose` メソッドを追加します。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>About ビューを変更する

*Views\Home\About.cshtml*ファイルのコードを次のコードに置き換えます。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

アプリを実行し、 **[バージョン情報]** リンクをクリックします。 登録の日付ごとの学生の数が、テーブルに表示されます。

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>省略可能: Windows Azure にアプリを展開する

これまでは、アプリケーションは開発用コンピューターの IIS Express でローカルに実行されていました。 他のユーザーがインターネット経由で使用できるようにするには、それを web ホスティングプロバイダーに展開する必要があります。 このチュートリアルの省略可能なセクションでは、Windows Azure の Web サイトに展開します。

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Code First Migrations を使用したデータベースの配置

データベースを配置するには、Code First Migrations を使用します。 Visual Studio からデプロイするための設定を構成するために使用する発行プロファイルを作成する場合は、 **[Execute Code First Migrations (アプリケーションの起動時に実行)]** というラベルのチェックボックスをオンにします。 この設定により、配置プロセスでは、Code First が `MigrateDatabaseToLatestVersion` 初期化子クラスを使用するように、移行先サーバー上のアプリケーションの*web.config*ファイルが自動的に構成されます。

Visual Studio は、配置プロセス中にデータベースに対して何も実行しません。 配置後に配置されたアプリケーションがデータベースに初めてアクセスすると、Code First によってデータベースが自動的に作成されるか、データベーススキーマが最新バージョンに更新されます。 アプリケーションが移行 `Seed` 方法を実装している場合、メソッドは、データベースが作成された後、またはスキーマが更新された後に実行されます。

移行 `Seed` 方法によって、テストデータが挿入されます。 運用環境に配置する場合は、実稼働データベースに挿入するデータのみが挿入されるように `Seed` 方法を変更する必要があります。 たとえば、現在のデータモデルでは、開発用データベースに架空のコースを作成することができます。 `Seed` メソッドを作成して、両方の開発で読み込み、架空の学生をコメントアウトしてから、運用環境にデプロイすることができます。 または、`Seed` メソッドを記述してコースのみを読み込み、アプリケーションの UI を使用して、テストデータベースに架空の学生を手動で入力することもできます。

### <a name="get-a-windows-azure-account"></a>Windows Azure アカウントを取得する

Windows Azure アカウントが必要です。 まだお持ちでない場合は、無料試用版アカウントを数分で作成できます。 詳細については、「 [Windows Azure 無料評価版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)」を参照してください。

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>Windows Azure で web サイトと SQL データベースを作成する

Windows Azure の Web サイトは、共有ホスティング環境で実行されます。これは、他の Windows Azure クライアントと共有されている仮想マシン (Vm) 上で実行されることを意味します。 共有ホスティング環境は、クラウドでの使い始めるための低コストな方法です。 その後、web トラフィックが増加した場合は、専用の Vm でを実行することで、ニーズに合わせてアプリケーションを拡張できます。 より複雑なアーキテクチャが必要な場合は、Windows Azure クラウドサービスに移行できます。 クラウドサービスは、必要に応じて構成できる専用 Vm 上で実行されます。

Windows Azure SQL Database は、SQL Server のテクノロジに基づいて構築されたクラウドベースのリレーショナルデータベースサービスです。 SQL Server と連携するツールとアプリケーションも SQL Database で動作します。

1. [Windows Azure 管理ポータル](https://manage.windowsazure.com/)の左側のタブで **[Web サイト]** をクリックし、 **[新規]** をクリックします。

    ![管理ポータルの [新規] ボタン](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. **[カスタム作成]** をクリックします。

    ![管理ポータルでデータベースリンクを使用して作成する](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **新しい Web サイト-カスタム作成**ウィザードが開きます。
3. ウィザードの **[新しい Web サイト]** ステップで、アプリケーションの一意の url として使用する文字列を **[URL]** ボックスに入力します。 完全な URL は、ここで入力した内容に、テキストボックスの横に表示されるサフィックスを加えたものになります。 この図には "ConU" が示されていますが、その URL は別のものを選択する必要がある場合があります。

    ![管理ポータルでデータベースリンクを使用して作成する](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. **[リージョン]** ドロップダウンリストで、近くのリージョンを選択します。 この設定では、web サイトが実行されるデータセンターを指定します。
5. **[データベース]** ボックスの一覧で、 **[無料の 20 MB の SQL データベースを作成する]** を選択します。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. **[DB 接続文字列名]** に「 *schoolcontext.cs*」と入力します。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. ボックスの下部にある右矢印をクリックします。 ウィザードの [データベースの**設定**] 手順に進みます。
8. **[名前]** ボックスに、「コンテキストを指定する」と*入力します*。
9. **[サーバー]** ボックスで、 **[新しい SQL Database サーバー]** を選択します。 または、サーバーを既に作成してある場合は、ドロップダウンリストからそのサーバーを選択できます。
10. 管理者の**ログイン名**と**パスワード**を入力します。 **[新しい SQL Database サーバー]** を選択した場合は、ここで既存の名前とパスワードを入力していないので、後でデータベースにアクセスするときに使用する新しい名前とパスワードを入力します。 以前に作成したサーバーを選択した場合は、そのサーバーの資格情報を入力します。 このチュートリアルでは、[***詳細設定***] チェックボックスはオンにしません。 ***[詳細***設定] オプションを使用すると、データベースの[照合順序](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)を設定できます。
11. Web サイト用に選択したものと同じ**リージョン**を選択します。
12. 終了したことを示すには、ボックスの右下にあるチェックマークをクリックします。   
  
    ![新しい Web サイト-データベースを使用した作成ウィザードの [データベースの設定] 手順](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    次の図は、既存の SQL Server とログインの使用方法を示しています。   
  
    ![新しい Web サイト-データベースを使用した作成ウィザードの [データベースの設定] 手順](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    管理ポータルが Web サイト ページに戻り、**状態** 列にサイトが作成されていることが示されます。 しばらくすると (通常は1分未満)、サイトが正常に作成されたことが **[状態]** 列に表示されます。 左側のナビゲーションバーで、アカウント内のサイトの数**が [websites] アイコン**の横に表示され、 **[SQL データベース]** アイコンの横にデータベースの数が表示されます。

## <a name="deploy-the-application-to-windows-azure"></a>Windows Azure にアプリケーションをデプロイする

1. Visual Studio で**ソリューションエクスプローラー**でプロジェクトを右クリックし、コンテキストメニューから **[発行]** を選択します。  
  
    ![プロジェクトのコンテキストメニューの [発行]](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. **Web の発行**ウィザードの **[プロファイル]** タブで、 **[インポート]** をクリックします。  
  
    ![発行設定のインポート](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. Visual Studio で Windows Azure サブスクリプションをまだ追加していない場合は、次の手順を実行します。 この手順では、サブスクリプションを追加して、 **[Windows Azure web サイトからのインポート]** の下にあるドロップダウンリストに web サイトが含まれるようにします。

    キーを押します。 **[発行プロファイルのインポート]** ダイアログボックスで、 **[windows azure web サイトからのインポート]** をクリックし、 **[windows azure サブスクリプションの追加]** をクリックします。

    ![Windows Azure サブスクリプションの追加](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. **[Windows Azure サブスクリプションのインポート]** ダイアログボックスで、 **[サブスクリプションファイルのダウンロード]** をクリックします。

    ![サブスクリプションファイルのダウンロード](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. ブラウザーウィンドウで、 *.publishsettings*ファイルを保存します。

    ![.publishsettings ファイルをダウンロードします。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > セキュリティ- *.publishsettings*ファイルには、Windows Azure のサブスクリプションとサービスの管理に使用される資格情報 (エンコードされていません) が含まれています。 このファイルのセキュリティのベストプラクティスは、ソースディレクトリの外部 (たとえば、[*ライブラリ*] フォルダー内) に一時的に保存し、インポートが完了した後に削除することです。 悪意のあるユーザーが `.publishsettings` ファイルにアクセスすると、Windows Azure サービスを編集、作成、および削除できます。

    d. **[Windows Azure サブスクリプションのインポート]** ダイアログボックスで **[参照]** をクリックし、 *.publishsettings*ファイルに移動します。

    ![サブのダウンロード](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. **[インポート]** をクリックします。

    ![取り込み](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. **[発行プロファイルのインポート]** ダイアログボックスで、 **[Windows Azure Web サイトからインポートする]** を選択し、ドロップダウンリストから web サイトを選択して、[ **OK]** をクリックします。  
  
    ![発行プロファイルのインポート](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. **[接続]** タブで、 **[接続の検証]** をクリックして、設定が正しいことを確認します。  
  
    ![接続の検証](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 接続が検証されると、 **[接続の検証]** ボタンの横に緑色のチェックマークが表示されます。 [次へ] をクリックします。  
  
    ![接続が正常に検証されました](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. **[Schoolcontext.cs]** の下の **[リモート接続文字列]** ドロップダウンリストを開き、作成したデータベースの接続文字列を選択します。
8. **[Code First Migrations の実行 (アプリケーションの起動時に実行)]** を選択します。
9. このアプリケーションではメンバーシップデータベースが使用されていないため、[UserContext の**実行時にこの接続文字列を使用する** **(defaultconnection)** ] チェックボックスをオフにします。   
  
    ![[設定] タブ](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. [次へ] をクリックします。
11. **[プレビュー]** タブで、 **[プレビューの開始]** をクリックします。  
  
    ![[プレビュー] タブの [StartPreview] ボタン](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    このタブには、サーバーにコピーされるファイルの一覧が表示されます。 アプリケーションの発行にはプレビューの表示は必要ありませんが、注意すべき便利な機能です。 この場合、表示されるファイルの一覧を使用して何もする必要はありません。 次回このアプリケーションを展開するときに、変更されたファイルだけがこの一覧に表示されます。  
  
    ![StartPreview ファイルの出力](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. **[発行]** をクリックします。  
    Visual Studio によって、ファイルを Windows Azure サーバーにコピーする処理が開始されます。
13. **[出力]** ウィンドウには、実行された配置アクションが表示され、デプロイが正常に完了したことがレポートされます。  
  
    ![成功した配置を報告する出力ウィンドウ](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. デプロイが成功すると、既定のブラウザーが自動的に開き、デプロイされた web サイトの URL が表示されます。  
    これで、作成したアプリケーションがクラウドで実行されます。 [Students] タブをクリックします。  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

この時点で、 **[Code First Migrations の実行 (アプリの起動時に実行)]** を選択したため、 *Schoolcontext.cs*データベースが Windows Azure SQL Database に作成されました。 デプロイされた web サイトの*web.config ファイルが*変更され、コードでデータベース内のデータの読み取りまたは書き込みが初めて実行されるようになりました ( **[Students]** タブを選択したときに[発生しまし](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)た)。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

また、配置プロセスでは、データベーススキーマの更新とデータベースのシード処理に使用する Code First Migrations 用の新しい接続文字列 *(schoolcontext.cs\_DatabasePublish*) も作成されています。

![Database_Publish 接続文字列](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*Defaultconnection*接続文字列はメンバーシップデータベース用です (このチュートリアルでは使用しません)。 *Schoolcontext.cs*接続文字列は ContosoUniversity データベース用です。

配置された web.config ファイルのバージョンは、自分のコンピューターのユーザーのコンピューターに配置されていることがわかります。詳細については、 *「」を*参照してください。配置された*web.config*ファイル自体には、FTP を使用してアクセスできます。 手順については、「 [ASP.NET Web Deployment Using Visual Studio: Code Update のデプロイ](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)」を参照してください。 「FTP ツールを使用するには」で始まる指示に従って、FTP URL、ユーザー名、およびパスワードの3つが必要になります。

> [!NOTE]
> Web アプリはセキュリティを実装していないので、URL を見つけたすべてのユーザーがデータを変更できます。 Web サイトをセキュリティで保護する方法については、「 [Windows Azure の Web サイトにメンバーシップ、OAuth、および SQL Database を使用する secure ASP.NET MVC アプリをデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)する」を参照してください。 Windows Azure 管理ポータルを使用するか、Visual Studio で**サーバーエクスプローラー**してサイトを停止することで、他のユーザーがサイトを使用できないようにすることができます。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Code First 初期化子

[デプロイ] セクションでは、Migrateに使用されている、 [Migrateasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初期化子があることを確認しました。 Code First には、 [Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (既定)、 [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) 、 [dropcreatedatabasealways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)など、使用できるその他の初期化子も用意されています。 `DropCreateAlways` 初期化子は、単体テストの条件を設定する場合に役立ちます。 独自の初期化子を記述することもできます。また、アプリケーションがデータベースに対して読み取りまたは書き込みを行うまで待機しない場合は、初期化子を明示的に呼び出すことができます。 初期化子の包括的な説明については、「 [Entity Framework:](http://shop.oreilly.com/product/0636920022220.do)ジュリー Lerman と Rowan 明美による Code First」の「本プログラミングの第6章」を参照してください。

## <a name="summary"></a>要約

このチュートリアルでは、データモデルを作成し、基本的な CRUD、並べ替え、フィルター処理、ページング、およびグループ化の機能を実装する方法について説明しました。 次のチュートリアルでは、データモデルを拡張することで、さらに高度なトピックを見ていきます。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [次へ](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
