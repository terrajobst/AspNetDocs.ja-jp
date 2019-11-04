---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリで EF を使用して関連データを読み取る'
description: このチュートリアルでは、関連データ (Entity Framework がナビゲーションプロパティに読み込むデータ) の読み取りと表示を行います。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445660"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリで EF を使用して関連データを読み取る

前のチュートリアルでは、School データモデルを完成しました。 このチュートリアルでは、関連データ (Entity Framework がナビゲーションプロパティに読み込むデータ) の読み取りと表示を行います。

以下の図は、使用するページを示しています。

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 6 Code First と Visual Studio を使用して ASP.NET MVC 5 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * 関連データを読み込む方法を学習する
> * Courses ページを作成する
> * Instructors ページを作成する

## <a name="prerequisites"></a>必要条件

* [より複雑なデータモデルを作成する](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>関連データを読み込む方法を学習する

Entity Framework がエンティティのナビゲーションプロパティに関連データを読み込むには、いくつかの方法があります。

- *遅延読み込み*。 エンティティが最初に読み込まれるときに、関連データは取得されません。 ただし、ナビゲーション プロパティに初めてアクセスしようとすると、そのナビゲーション プロパティに必要なデータが自動的に取得されます。 この結果、複数のクエリがデータベースに送信されます。1つはエンティティ自体に対して、もう1つはエンティティの関連データを取得する必要があるときです。 `DbContext` クラスを使用すると、既定で遅延読み込みが有効になります。

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *一括読み込み*。 エンティティが読み取られるときに、関連データがエンティティと共に取得されます。 これは通常、必要なすべてのデータを取得する 1 つの結合クエリになります。 一括読み込みは、`Include` メソッドを使用して指定します。

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *明示的読み込み*。 これは、コード内の関連データを明示的に取得する点を除いて、遅延読み込みに似ています。ナビゲーションプロパティにアクセスしても、自動的には発生しません。 関連データを手動で読み込むには、エンティティのオブジェクト状態マネージャーエントリを取得し、[コレクションの load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)メソッドを呼び出すか、単一のエンティティを保持するプロパティのコレクションまたは参照メソッドを読み込み[ます](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)。 (次の例では、管理者ナビゲーションプロパティを読み込む場合は、`Collection(x => x.Courses)` を `Reference(x => x.Administrator)`に置き換えます)。通常、明示的な読み込みは、遅延読み込みを無効にした場合にのみ使用します。

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

遅延読み込みと明示的な読み込みは、すぐにプロパティ値を取得しないため、*遅延読み込み*とも呼ばれます。

### <a name="performance-considerations"></a>パフォーマンスに関する考慮事項

取得したすべてのエンティティの関連データが必要な場合は、通常、データベースに送信された 1 つのクエリの方が、取得した各エンティティに対する分離したクエリよりも効率的なため、一括読み込みを使用すると、より最適なパフォーマンスが得られます。 たとえば、上記の例では、各部門に関連コースが10個あるとします。 一括読み込みの例では、単一の (結合) クエリと、データベースへの1回のラウンドトリップだけが発生します。 遅延読み込みと明示的な読み込みの例では、両方とも11個のクエリと、データベースへの11回のラウンドトリップが発生します。 データベースとの余分なラウンド トリップは、特に待ち時間が長いときのパフォーマンスに悪影響をもたらします。

一方、シナリオによっては、遅延読み込みの方が効率的です。 一括読み込みでは、非常に複雑な結合が生成される可能性がありますが、SQL Server は効率的に処理できません。 また、処理しているエンティティのセットのサブセットに対してのみエンティティのナビゲーションプロパティにアクセスする必要がある場合は、一括読み込みで必要以上のデータを取得するため、遅延読み込みの方がパフォーマンスが向上する可能性があります。 パフォーマンスが重要な場合、最適な選択を行うために、両方の方法でパフォーマンスをテストすることをお勧めします。

遅延読み込みでは、パフォーマンスの問題を引き起こすコードをマスクできます。 たとえば、一括または明示的な読み込みを指定せずに大量のエンティティを処理し、各イテレーションで複数のナビゲーションプロパティを使用するコードは、データベースへのラウンドトリップが多くなるため、非常に非効率になる可能性があります。 オンプレミスの SQL server を使用して開発を正常に実行するアプリケーションでは、待機時間の増加と遅延読み込みのために Azure SQL Database に移動したときにパフォーマンスの問題が発生する可能性があります。 現実的なテスト負荷を使用してデータベースクエリをプロファイルすると、遅延読み込みが適切かどうかを判断するのに役立ちます。 詳細については、「 [Demystifying Entity Framework 方法: 関連データの読み込み](https://msdn.microsoft.com/magazine/hh205756.aspx)」と「 [Entity Framework を使用したネットワーク待機 SQL Azure 時間の短縮](https://msdn.microsoft.com/magazine/gg309181.aspx)」を参照してください。

### <a name="disable-lazy-loading-before-serialization"></a>シリアル化の前に遅延読み込みを無効にする

シリアル化中に遅延読み込みを有効にしたままにすると、最終的には意図したよりもはるかに多くのデータを照会できます。 通常、シリアル化は、型のインスタンスの各プロパティにアクセスすることによって機能します。 プロパティアクセスは遅延読み込みをトリガーし、それらの遅延読み込みされたエンティティをシリアル化します。 次に、シリアル化プロセスは、遅延読み込みされたエンティティの各プロパティにアクセスします。これにより、さらに遅延読み込みとシリアル化が発生する可能性があります。 この実行後のチェーンの反応を回避するには、エンティティをシリアル化する前に遅延読み込みをオフにします。

また、[高度なシナリオのチュートリアル](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)で説明されているように、Entity Framework が使用するプロキシクラスによっても、シリアル化が複雑になることがあります。

シリアル化の問題を回避する1つの方法は、「 [Using WEB API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)チュートリアル」に示されているように、エンティティオブジェクトではなくデータ転送オブジェクト (dto) をシリアル化することです。

Dto を使用しない場合は、遅延読み込みを無効にして、プロキシの[作成を無効](https://msdn.microsoft.com/data/jj592886.aspx)にすることでプロキシの問題を回避できます。

[遅延読み込みを無効にする](https://msdn.microsoft.com/data/jj574232)その他の方法を次に示します。

- 特定のナビゲーションプロパティについては、プロパティを宣言するときに `virtual` キーワードを省略します。
- すべてのナビゲーションプロパティで、`LazyLoadingEnabled` を `false`に設定し、コンテキストクラスのコンストラクターに次のコードを追加します。

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>Courses ページを作成する

`Course` エンティティには、コースが割り当てられている部署の `Department` エンティティを含むナビゲーションプロパティが含まれています。 割り当てられた部門の名前をコースの一覧に表示するには、`Course.Department` ナビゲーションプロパティにある `Department` エンティティから `Name` プロパティを取得する必要があります。

`Course` エンティティ型に対して `CourseController` (not CoursesController) という名前のコントローラーを作成します。これには、ビューと同じオプションを使用します。これには、以前に `Student` コントローラーで行った**Entity Framework scaffolder を使用**します。

| 設定 | [値] |
| ------- | ----- |
| モデルクラス | **[コース (ContosoUniversity)]** を選択します。 |
| データコンテキストクラス | **[Schoolcontext.cs (ContosoUniversity)]** を選択します。 |
| コントローラー名 | 「 *CourseController*」と入力します。 ここでも、には*CoursesController* *がありません。* **[Course (ContosoUniversity)]** を選択すると、**コントローラー名**の値が自動的に設定されます。 値を変更する必要があります。 |

他の既定値はそのままにして、コントローラーを追加します。

*Controllers\CourseController.cs*を開き、`Index` メソッドを確認します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

自動スキャフォールディングでは、`Include` メソッドを使って、`Department` ナビゲーション プロパティに一括読み込みを指定しています。

*Views\Course\Index.cshtml*を開き、テンプレートコードを次のコードに置き換えます。 変更が強調表示されています。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

スキャフォールディング コードに、次の変更を行いました。

- 見出しを **[インデックス]** から **[コース]** に変更しました。
- `CourseID` プロパティ値を示す **Number** 列が追加されました。 既定では、主キーはスキャフォールディングされません。これは通常、エンドユーザーにとって意味がないためです。 ただし、このケースでは、主キーは意味があり、表示する必要があります。
- **Department**列を右側に移動し、見出しを変更しました。 Scaffolder は、`Department` エンティティから `Name` プロパティを表示するように正しく選択しましたが、コースページでは、列見出しが**Name**ではなく**Department**である必要があります。

Department 列の場合、スキャフォールディングコードは `Department` ナビゲーションプロパティに読み込まれる `Department` エンティティの `Name` プロパティを表示します。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

ページを実行します (Contoso 大学のホームページの **[コース]** タブを選択します)。部署名の一覧が表示されます。

## <a name="create-an-instructors-page"></a>Instructors ページを作成する

このセクションでは、`Instructor` エンティティのコントローラーとビューを作成して、インストラクターのページを表示します。 このページは、次の方法で関連データを読み取って表示します。

- インストラクターの一覧には、`OfficeAssignment` エンティティの関連データが表示されます。 `Instructor` エンティティと `OfficeAssignment` エンティティは、一対ゼロまたは一対一のリレーションシップです。 `OfficeAssignment` エンティティに一括読み込みを使用します。 前述のように、通常、一括読み込みは、主テーブルで取得したすべての行の関連データが必要なときにより効率的です。 このケースでは、割り当てられたすべてのインストラクターのオフィスの割り当てを表示する必要があります。
- ユーザーがインストラクターを選択すると、関連する `Course` エンティティが表示されます。 `Instructor` エンティティと `Course` エンティティは多対多リレーションシップです。 `Course` エンティティとそれに関連する `Department` エンティティに一括読み込みを使用します。 この場合、選択したインストラクターのコースのみが必要になるため、遅延読み込みの方が効率的な場合があります。 ただし、この例では、ナビゲーション プロパティにあるエンティティ内のナビゲーション プロパティに一括読み込みを使用する方法を示します。
- ユーザーがコースを選択すると、`Enrollments` エンティティセットの関連データが表示されます。 `Course` エンティティと `Enrollment` エンティティは一対多リレーションシップです。 `Enrollment` エンティティとそれに関連する `Student` エンティティに対して明示的な読み込みを追加します。 (遅延読み込みが有効になっているため、明示的な読み込みは必要ありませんが、これは明示的な読み込みを行う方法を示しています)。

### <a name="create-a-view-model-for-the-instructor-index-view"></a>インストラクターのインデックスビューのビューモデルを作成する

[インストラクター] ページには、3つの異なるテーブルが表示されます。 そのため、テーブルの 1 つにデータを保持するごとに、3 つのプロパティを含むビュー モデルを作成します。

*Viewmodel*フォルダーで、 *InstructorIndexData.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>インストラクターのコントローラーとビューを作成する

EF の読み取り/書き込みアクションを使用して `InstructorController` (not InstructorsController) コントローラーを作成します。

| 設定 | [値] |
| ------- | ----- |
| モデルクラス | **[インストラクター (ContosoUniversity)]** を選択します。 |
| データコンテキストクラス | **[Schoolcontext.cs (ContosoUniversity)]** を選択します。 |
| コントローラー名 | 「 *InstructorController*」と入力します。 ここでも、には*InstructorsController* *がありません。* **[Course (ContosoUniversity)]** を選択すると、**コントローラー名**の値が自動的に設定されます。 値を変更する必要があります。 |

他の既定値はそのままにして、コントローラーを追加します。

*Controllers\InstructorController.cs*を開き、`ViewModels` 名前空間の `using` ステートメントを追加します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` メソッドのスキャフォールディングコードは、`OfficeAssignment` ナビゲーションプロパティに対してのみ一括読み込みを指定します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

`Index` メソッドを次のコードに置き換えて、追加の関連データを読み込み、ビューモデルに配置します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

メソッドは、オプションのルートデータ (`id`) と、選択したインストラクターと選択したコースの ID 値を提供するクエリ文字列パラメーター (`courseID`) を受け取り、必要なすべてのデータをビューに渡します。 パラメーターは、ページの **Select** ハイパーリンクによって指定されます。

このコードは、ビュー モデルのインスタンスを作成し、インストラクターのリストに配置することから始めます。 このコードでは、`Instructor.OfficeAssignment` と `Instructor.Courses` ナビゲーションプロパティの一括読み込みを指定します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

2番目の `Include` メソッドは、コースを読み込み、読み込まれた各コースで `Course.Department` ナビゲーションプロパティの一括読み込みを行います。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

前述のように、一括読み込みは必要ありませんが、パフォーマンスを向上させるために行われます。 ビューには常に `OfficeAssignment` エンティティが必要であるため、同じクエリでフェッチする方が効率的です。 `Course` エンティティは、web ページでインストラクターが選択されている場合に必要になります。したがって、[なし] を選択した場合に比べて、ページがより頻繁に表示される場合のみ、一括読み込みの方が遅延読み込みより優れています。

[インストラクター ID] が選択されている場合は、選択したインストラクターがビューモデルのインストラクターの一覧から取得されます。 次に、ビューモデルの `Courses` プロパティが、そのインストラクターの `Courses` ナビゲーションプロパティからの `Course` エンティティと共に読み込まれます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Where` メソッドはコレクションを返しますが、この場合は、そのメソッドに渡された条件によって返されるのは、1つの `Instructor` エンティティだけになります。 `Single` メソッドは、コレクションを1つの `Instructor` エンティティに変換します。これにより、そのエンティティの `Courses` プロパティにアクセスできるようになります。

コレクションに項目が1つしかないことがわかっている場合は、コレクションに対して[1 つ](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)のメソッドを使用します。 `Single` メソッドは、渡されたコレクションが空である場合、または複数の項目がある場合に、例外をスローします。 別の方法としては[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)があります。これは、コレクションが空の場合に既定値 (この場合は`null`) を返します。 ただし、この場合も例外が発生します (`null` 参照の `Courses` プロパティを見つけようとする)。例外メッセージは、問題の原因を明確に示すものではありません。 `Single` メソッドを呼び出すと、`Where` メソッドを個別に呼び出す代わりに、`Where` 条件を渡すこともできます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

これは次のコードの代わりに使用します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

次に、コースが選択された場合、選択したコースはビュー モデルのコースのリストから取得されます。 次に、ビューモデルの `Enrollments` プロパティが、そのコースの `Enrollments` ナビゲーションプロパティからの `Enrollment` エンティティと共に読み込まれます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>インストラクターのインデックスビューを変更する

*Views\Instructor\Index.cshtml*で、テンプレートコードを次のコードに置き換えます。 変更が強調表示されています。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

既存のコードに次の変更を行いました。

- モデル クラスが `InstructorIndexData` に変更されました。
- **Index** のページ タイトルが **Instructors** に変更されました。
- `item.OfficeAssignment` が null でない場合にのみ `item.OfficeAssignment.Location` を表示する**Office**列を追加しました。 (これは一対ゼロまたは一対一のリレーションシップであるため、関連する `OfficeAssignment` エンティティが存在しない可能性があります)。

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- 選択したインストラクターの `tr` 要素に `class="success"` を動的に追加するコードを追加しました。 これにより、[ブートストラップ](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)クラスを使用して、選択した行の背景色が設定されます。

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- 各行の [その他のリンクの直前に**選択する]** というラベルの新しい `ActionLink` が追加されました。選択したインストラクター ID が `Index` メソッドに送信されます。

アプリケーションを実行し、 **[インストラクター]** タブを選択します。このページには、関連する `OfficeAssignment` エンティティの [`Location`] プロパティと、関連する `OfficeAssignment` エンティティが存在しない場合の空のテーブルセルが表示されます。

*Views\Instructor\Index.cshtml*ファイルで、終了 `table` 要素 (ファイルの末尾) の後に、次のコードを追加します。 このコードでは、インストラクターが選択されたときに、インストラクターに関連するコースのリストを表示します。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

このコードでは、ビュー モデルの `Courses` プロパティを読み取り、コースのリストを表示します。 また、選択したコースの ID を `Index` アクションメソッドに送信する `Select` ハイパーリンクも用意されています。

ページを実行し、インストラクターを選択します。 選択したインストラクターに割り当てられたコースを表示するグリッドを表示し、各コースに割り当てられた部門の名前を表示します。

追加したコード ブロックの後に、次のコードを追加します。 このコードは、コースを選択したときに、コースに登録されている受講者のリストを表示します。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

このコードは、コースに登録されている学生の一覧を表示するために、ビューモデルの `Enrollments` プロパティを読み取ります。

ページを実行し、インストラクターを選択します。 次に、コースを選択して、登録済みの受講者とその成績のリストを表示します。

### <a name="adding-explicit-loading"></a>明示的な読み込みの追加

*InstructorController.cs*を開き、選択したコースの登録の一覧を `Index` メソッドがどのように取得するかを確認します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

インストラクターのリストを取得したときに、`Courses` ナビゲーションプロパティの一括読み込みを指定し、各コースの `Department` プロパティを指定しました。 次に、ビューモデルに `Courses` コレクションを配置します。これで、そのコレクション内の1つのエンティティから `Enrollments` ナビゲーションプロパティにアクセスしています。 `Course.Enrollments` ナビゲーションプロパティに一括読み込みを指定しなかったため、遅延読み込みの結果として、そのプロパティのデータがページに表示されます。

他の方法でコードを変更せずに遅延読み込みを無効にした場合、実際に存在していた登録数に関係なく、`Enrollments` プロパティは null になります。 この場合、`Enrollments` プロパティを読み込むには、一括読み込みまたは明示的な読み込みのいずれかを指定する必要があります。 一括読み込みを実行する方法については既に説明しました。 明示的な読み込みの例を表示するには、`Index` メソッドを次のコードに置き換えます。このコードは、`Enrollments` プロパティを明示的に読み込みます。 変更されたコードが強調表示されます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

選択した `Course` エンティティを取得すると、新しいコードによってそのコースの `Enrollments` ナビゲーションプロパティが明示的に読み込まれます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

次に、`Enrollment` エンティティに関連する各 `Student` エンティティを明示的に読み込みます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

`Collection` メソッドを使用してコレクションプロパティを読み込むことに注意してくださいが、1つのエンティティのみを保持するプロパティの場合は、`Reference` メソッドを使用します。

[インストラクターのインデックス] ページを実行すると、データの取得方法が変更されましたが、ページに表示される内容に違いはありません。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトのダウンロード](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他の技術情報

その他の Entity Framework リソースへのリンクについては、 [ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)を参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * 関連データを読み込む方法を学習した
> * Courses ページを作成した
> * Instructors ページを作成した

関連データを更新する方法について学習するには、次の記事に進んでください。

> [!div class="nextstepaction"]
> [関連データの更新](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
