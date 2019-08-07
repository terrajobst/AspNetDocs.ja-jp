---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリケーションで、並べ替え、フィルター処理、およびページングを Entity Framework に追加する |Microsoft Docs'
author: tdykstra
description: このチュートリアルでは、並べ替え、フィルター処理、およびページング機能を**Students**インデックスページに追加します。 また、単純なグループ化ページも作成します。
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810759"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>チュートリアル: ASP.NET MVC アプリケーションでの Entity Framework による並べ替え、フィルター処理、およびページングの追加

前の[チュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、エンティティに対する`Student`基本的な CRUD 操作用の一連の web ページを実装しています。 このチュートリアルでは、並べ替え、フィルター処理、およびページング機能を**Students**インデックスページに追加します。 また、単純なグループ化ページも作成します。

次の図は、完了したときのページの外観を示しています。 列見出しとは、ユーザーがクリックしてその列で並べ替えを行うことができるリンクです。 列見出しを繰り返しクリックすると、昇順と降順の並べ替え順序が切り替えられます。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * 列の並べ替えリンクを追加する
> * [検索] ボックスを追加する
> * ページングの追加
> * About ページを作成する

## <a name="prerequisites"></a>必須コンポーネント

* [基本 CRUD 機能を実装する](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>列の並べ替えリンクを追加する

学生用インデックスページに並べ替えを追加するには、 `Index` `Student`コントローラーのメソッドを変更`Student`し、インデックスビューにコードを追加します。

### <a name="add-sorting-functionality-to-the-index-method"></a>Index メソッドに並べ替え機能を追加する

- *Controllers\StudentController.cs*で、 `Index`メソッドを次のコードに置き換えます。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

このコードは、URL 内の文字列から `sortOrder` パラメーターを受け取ります。 クエリ文字列値は、ASP.NET MVC によってアクションメソッドのパラメーターとして提供されます。 パラメーターは、"Name" または "Date" の文字列であり、必要に応じてアンダースコアと文字列 "desc" を降順で指定します。 既定の並べ替え順序は昇順です。

インデックス ページが初めて要求されたときには、クエリ文字列はありません。 学生は昇順`LastName`で表示されます。これは、 `switch`ステートメントのフォールスルーケースによって確立される既定の設定です。 ユーザーが列見出しハイパーリンクをクリックすると、適切な `sortOrder` 値がクエリ文字列で提供されます。

次の`ViewBag` 2 つの変数を使用して、ビューが列見出しのハイパーリンクと適切なクエリ文字列値を構成できるようにします。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

これらは、三項ステートメントです。 最初の`sortOrder`パラメーターは、パラメーターが null または空の場合`ViewBag.NameSortParm` 、を "name\_desc" に設定する必要があることを指定します。それ以外の場合は、空の文字列に設定する必要があります。 これらの 2 つのステートメントを使用して、次のようにビューで列見出しのハイパーリンクの設定することができます。

| 既定の並べ替え順 | 姓のハイパーリンク | 日付のハイパーリンク |
| --- | --- | --- |
| 姓の昇順 | descending | ascending |
| 姓の降順 | ascending | ascending |
| 日付の昇順 | ascending | descending |
| 日付の降順 | ascending | ascending |

このメソッドは[LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)を使用して、並べ替えの基準となる列を指定します。 このコードは、 <xref:System.Linq.IQueryable%601>ステートメントの`switch`前に変数`switch`を作成し、ステートメントで変更し、 `ToList`ステートメントの`switch`後にメソッドを呼び出します。 `IQueryable` 変数を作成および変更するときに、データベースに送信されるクエリはありません。 クエリは、など`IQueryable` `ToList`のメソッドを呼び出すことによって、オブジェクトをコレクションに変換するまで実行されません。 このため、このコードでは、 `return View`ステートメントまで実行されない1つのクエリが生成されます。

各並べ替え順序に対して異なる LINQ ステートメントを記述する代わりに、LINQ ステートメントを動的に作成することもできます。 動的 LINQ の詳細については、「 [DYNAMIC linq](https://go.microsoft.com/fwlink/?LinkID=323957)」を参照してください。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>列見出しのハイパーリンクを Student インデックスビューに追加する

1. *Views\Student\Index.cshtml*で、見出し行`<tr>`の`<th>`要素と要素を、強調表示されたコードに置き換えます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   このコードでは、プロパティの`ViewBag`情報を使用して、適切なクエリ文字列値を持つハイパーリンクを設定します。

2. ページを実行し、 **[Last Name]** と **[Enrollment Date]** 列見出しをクリックして、並べ替えが機能することを確認します。

   **最後の名前**の見出しをクリックすると、学生が姓の降順で表示されます。

## <a name="add-a-search-box"></a>[検索] ボックスを追加する

Students インデックスページにフィルターを追加するには、テキストボックスと [送信] ボタンをビューに追加し、 `Index`メソッドに対応する変更を行います。 テキストボックスを使用すると、[名] および [姓] フィールドで検索する文字列を入力できます。

### <a name="add-filtering-functionality-to-the-index-method"></a>Index メソッドにフィルター機能を追加する

- *Controllers\StudentController.cs*で、 `Index`メソッドを次のコードに置き換えます (変更は強調表示されています)。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

このコードは、 `searchString` `Index`メソッドにパラメーターを追加します。 インデックス ビューに追加するテキスト ボックスから検索する文字列値を受け取ります。 また、最初の`where`名前または姓に検索文字列が含まれている学生だけを選択するように、LINQ ステートメントに句を追加します。 <xref:System.Linq.Queryable.Where%2A>句を追加するステートメントは、検索する値がある場合にのみ実行されます。

> [!NOTE]
> 多くの場合、Entity Framework のエンティティセットまたはメモリ内のコレクションの拡張メソッドとして、同じメソッドを呼び出すことができます。 通常、結果は同じですが、場合によっては異なる場合があります。
>
> たとえば、 `Contains`メソッドの .NET Framework 実装では、空の文字列を渡すとすべての行が返されますが、SQL Server Compact 4.0 の Entity Framework プロバイダーは空の文字列に対して0行を返します。 したがって、この例のコード (ステートメント`Where` `if`内にステートメントを記述する) を使用すると、SQL Server のすべてのバージョンで同じ結果が得られるようになります。 また、 `Contains`メソッドの .NET Framework 実装では、既定で大文字と小文字を区別した比較が実行されますが、Entity Framework SQL Server プロバイダーは既定で大文字と小文字を区別しない比較を実行します。 したがって、 `ToUpper`メソッドを呼び出してテストを明示的に大文字小文字を区別しないようにすると、後でリポジトリを使用するようにコードを変更しても`IQueryable` 、オブジェクトではなくコレクションが`IEnumerable`返されるようになります。 (`IEnumerable` コレクションに対して `Contains` メソッドを呼び出したときには、.NET Framework の実装を取得します。`IQueryable` オブジェクトに対して呼び出したときには、データベース プロバイダーの実装を取得します)。
>
> また、Null 処理は、データベースプロバイダーによって異なる場合や、 `IQueryable` `IEnumerable`コレクションを使用する場合と比較してオブジェクトを使用する場合には異なる場合があります。 たとえば、一部のシナリオ`Where`では、などの条件`table.Column != 0`で値`null`としての列が返されないことがあります。 既定では、EF は、メモリ内で動作するように、null 値間の等価性をデータベースで機能させるために、追加の SQL 演算子を生成します。ただし、EF6 で[Usedatabasenullsemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics)フラグを設定するか、または EF Core で[UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls)メソッドを呼び出すことができます。この動作を構成します。

### <a name="add-a-search-box-to-the-student-index-view"></a>学生用インデックスビューに検索ボックスを追加する

1. *Views\Student\Index.cshtml*で、キャプション、テキストボックス、および**検索**ボタン`table`を作成するために、開始タグの直前に強調表示されているコードを追加します。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. ページを実行し、検索文字列を入力して **[検索]** をクリックし、フィルター処理が機能していることを確認します。

   URL に "an" という検索文字列が含まれていないことに注意してください。つまり、このページにブックマークを指定すると、ブックマークを使用するとフィルター処理された一覧が表示されません。 これは、一覧全体を並べ替えるため、列の並べ替えリンクにも適用されます。 このチュートリアルの後の方で、フィルター条件にクエリ文字列を使用するように **[検索]** ボタンを変更します。

## <a name="add-paging"></a>ページングの追加

Students インデックスページにページングを追加するには、まず**PagedList** NuGet パッケージをインストールします。 次に、 `Index`メソッドに追加の変更を加え、ページングリンク`Index`をビューに追加します。 **PagedList**は、ASP.NET Mvc 用の多くの優れたページングおよび並べ替えパッケージの1つです。この使用方法は、他のオプションよりも推奨されるものではなく、例としてのみ使用することを目的としています。

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList NuGet パッケージをインストールする

NuGet **PagedList**パッケージは、 **PagedList**パッケージを依存関係として自動的にインストールします。 **PagedList**パッケージは、コレクション`PagedList`と`IEnumerable`コレクションの`IQueryable`コレクション型および拡張メソッドをインストールします。 `PagedList`拡張メソッドは、 `IQueryable`または`IEnumerable`からコレクション内の1ページのデータを作成し`PagedList`ます。コレクションには、ページングを容易にするいくつかのプロパティとメソッドが用意されています。 **PagedList**パッケージは、ページングボタンを表示するページングヘルパーをインストールします。

1. **[ツール]** メニューの **[NuGet パッケージマネージャー]** をポイントし、 **[パッケージマネージャーコンソール]** をクリックします。

2. **パッケージマネージャーコンソール**ウィンドウで、**パッケージソース**が**nuget.org**で、**既定のプロジェクト**が**ContosoUniversity**であることを確認し、次のコマンドを入力します。

   ```text
   Install-Package PagedList.Mvc
   ```

3. プロジェクトをビルドします。

### <a name="add-paging-functionality-to-the-index-method"></a>Index メソッドにページング機能を追加する

1. *Controllers\StudentController.cs*で、 `using` `PagedList`名前空間のステートメントを追加します。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. `Index` メソッドを次のコードで置き換えます。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   このコードは、 `page`パラメーター、現在の並べ替え順序パラメーター、および現在のフィルターパラメーターをメソッドシグネチャに追加します。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   ページが初めて表示されたとき、またはユーザーがページングまたは並べ替えリンクをクリックしていない場合は、すべてのパラメーターが null になります。 ページングリンクをクリックすると、表示`page`するページ番号が変数に格納されます。

   プロパティ`ViewBag`は、ページング中に並べ替え順序を同じにするためにページングリンクに含める必要があるため、現在の並べ替え順序でビューを提供します。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   もう1つ`ViewBag.CurrentFilter`のプロパティは、現在のフィルター文字列を使用してビューを提供します。 ページング中にフィルターの設定を維持するために、ページングのリンクにこの値を含める必要があり、ページが再表示されるときに、この値をテキスト ボックスに復元する必要があります。 ページングの中に検索文字列を変更した場合は、新しいフィルターのために別のデータが表示されるため、ページを 1 にリセットする必要があります。 テキストボックスに値を入力し、[送信] ボタンを押すと、検索文字列が変更されます。 この場合、 `searchString`パラメーターは null ではありません。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   メソッドの最後で、students `ToPagedList` `IQueryable`オブジェクトの拡張メソッドは、ページングをサポートするコレクション型の1ページに学生クエリを変換します。 これにより、学生の1つのページがビューに渡されます。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   `ToPagedList` メソッドは、ページ番号を受け取ります。 2つの疑問符は、 [null 合体演算子](/dotnet/csharp/language-reference/operators/null-coalescing-operator)を表します。 null 合体演算子は null 許容型の既定値を定義します。式 `(page ?? 1)` は、値がある場合は `page` の値を返し、`page` が null の場合は 1 を返すことを意味します。

### <a name="add-paging-links-to-the-student-index-view"></a>Student インデックスビューにページングリンクを追加する

1. *Views\Student\Index.cshtml*で、既存のコードを次のコードに置き換えます。 変更が強調表示されます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   ページの上部にある `@model` ステートメントは、ビューが `List` オブジェクトの代わりに `PagedList` オブジェクトを取得するようになったことを指定します。

   `using` の`PagedList.Mvc`ステートメントは、ページングボタンの MVC ヘルパーへのアクセスを提供します。

   このコードでは、 [Beginform](/previous-versions/aspnet/dd492719(v=vs.108))のオーバーロードを使用して、 [Formmethod. Get](/previous-versions/aspnet/dd460179(v=vs.100))を指定できます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   既定の[Beginform](/previous-versions/aspnet/dd492719(v=vs.108))は POST を使用してフォームデータを送信します。つまり、パラメーターは URL ではなく、クエリ文字列として渡されます。 HTTP GET を指定すると、フォーム データがクエリ文字列として URL で渡され、ユーザーが URL をブックマークできるようになります。 [HTTP get を使用する場合の W3C ガイドライン](http://www.w3.org/2001/tag/doc/whenToUseGet.html)では、アクションによって更新されない場合に get を使用することをお勧めします。

   テキストボックスは現在の検索文字列で初期化されるため、新しいページをクリックすると、現在の検索文字列を確認できます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   列ヘッダーへのリンクは、フィルターの結果内でユーザーが並べ替えられるように、クエリ文字列を使用してコントローラーに現在の検索文字列を渡します。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   現在のページとページの合計数が表示されます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   表示するページがない場合は、"Page 0 of 0" が表示されます。 (その場合、が 1 `Model.PageNumber` `Model.PageCount`で、が0であるため、ページ番号がページ数を超えています)。

   ページングボタンは、 `PagedListPager`ヘルパーによって次のように表示されます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   ヘルパー `PagedListPager`には、url やスタイルなど、カスタマイズできる多くのオプションが用意されています。 詳細については、GitHub サイトの「 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 」を参照してください。

2. ページを実行します。

   異なる並べ替え順でページングのリンクをクリックし、ページングが機能することを確認します。 その後で、検索文字列を入力して、ページングをもう一度試し、並べ替えとフィルター処理を使用してもページングが正しく機能することを確認します。

## <a name="create-an-about-page"></a>About ページを作成する

Contoso 大学の web サイトの [About] ページには、登録日ごとに登録された学生の数が表示されます。 これには、グループ化とグループに関する簡単な計算が必要です。 これを実行するためには、次の手順を実行します。

- ビューに渡す必要があるデータのビュー モデル クラスを作成します。
- `Home`コントローラーの`About`メソッドを変更します。
- ビューを`About`変更します。

### <a name="create-the-view-model"></a>ビューモデルを作成する

プロジェクトフォルダーに*viewmodel*フォルダーを作成します。 そのフォルダーで、クラスファイル*EnrollmentDateGroup.cs*を追加し、テンプレートコードを次のコードに置き換えます。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Home コントローラーを変更する

1. *HomeController.cs*で、ファイルの先頭`using`に次のステートメントを追加します。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. クラスの左中かっこの直後に、データベースコンテキストのクラス変数を追加します。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. `About` メソッドを次のコードで置き換えます。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   LINQ ステートメントは、登録日で受講者エンティティをグループ化し、各グループ内のエンティティの数を計算して、結果を `EnrollmentDateGroup` ビュー モデル オブジェクトのコレクションに格納します。

4. メソッドを`Dispose`追加します。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>About ビューを変更する

1. *Views\Home\About.cshtml*ファイルのコードを次のコードに置き換えます。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. アプリを実行し、 **[バージョン情報]** リンクをクリックします。

   登録日ごとの生徒の数がテーブルに表示されます。

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトをダウンロードする](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他の技術情報

その他の Entity Framework リソースへのリンクについては[、「ASP.NET Data Access-推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * 列の並べ替えリンクを追加する
> * [検索] ボックスを追加する
> * ページングの追加
> * About ページを作成する

次の記事に進み、接続の回復性とコマンドインターセプトの使用方法を学習してください。
> [!div class="nextstepaction"]
> [接続の回復性とコマンドのインターセプト](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
