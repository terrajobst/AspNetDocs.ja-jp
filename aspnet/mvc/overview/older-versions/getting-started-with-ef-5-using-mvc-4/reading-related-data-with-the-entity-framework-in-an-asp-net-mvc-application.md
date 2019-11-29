---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り (5/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e1752022b66952783039fbea0c2880e2f9be6ef8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595209"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り (5/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、School データモデルを完成しました。 このチュートリアルでは、関連データ (Entity Framework がナビゲーションプロパティに読み込むデータ) の読み取りと表示を行います。

以下の図は、使用するページを示しています。

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>関連データの遅延、一括、明示的な読み込み

Entity Framework がエンティティのナビゲーションプロパティに関連データを読み込むには、いくつかの方法があります。

- *遅延読み込み*。 エンティティが最初に読み込まれるときに、関連データは取得されません。 ただし、ナビゲーション プロパティに初めてアクセスしようとすると、そのナビゲーション プロパティに必要なデータが自動的に取得されます。 この結果、複数のクエリがデータベースに送信されます。1つはエンティティ自体に対して、もう1つはエンティティの関連データを取得する必要があるときです。 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *一括読み込み*。 エンティティが読み取られるときに、関連データがエンティティと共に取得されます。 これは通常、必要なすべてのデータを取得する 1 つの結合クエリになります。 一括読み込みは、`Include` メソッドを使用して指定します。

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *明示的読み込み*。 これは、コード内の関連データを明示的に取得する点を除いて、遅延読み込みに似ています。ナビゲーションプロパティにアクセスしても、自動的には発生しません。 関連データを手動で読み込むには、エンティティのオブジェクト状態マネージャーエントリを取得し、コレクションの `Collection.Load` メソッドを呼び出すか、1つのエンティティを保持するプロパティの `Reference.Load` メソッドを呼び出します。 (次の例では、管理者ナビゲーションプロパティを読み込む場合は、`Collection(x => x.Courses)` を `Reference(x => x.Administrator)`に置き換えます)。

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

遅延読み込みと明示的な読み込みは、すぐにプロパティ値を取得しないため、*遅延読み込み*とも呼ばれます。

一般に、取得したすべてのエンティティに関連データが必要であることがわかっている場合は、一括読み込みで最高のパフォーマンスが得られます。これは、データベースに送信される単一のクエリは、通常、取得されたエンティティごとに個別のクエリよりも効率的であるためです。 たとえば、上記の例では、各部門に関連コースが10個あるとします。 一括読み込みの例では、単一の (結合) クエリと、データベースへの1回のラウンドトリップだけが発生します。 遅延読み込みと明示的な読み込みの例では、両方とも11個のクエリと、データベースへの11回のラウンドトリップが発生します。 データベースとの余分なラウンド トリップは、特に待ち時間が長いときのパフォーマンスに悪影響をもたらします。

一方、シナリオによっては、遅延読み込みの方が効率的です。 一括読み込みでは、非常に複雑な結合が生成される可能性がありますが、SQL Server は効率的に処理できません。 また、処理している一連のエンティティのサブセットに対してのみエンティティのナビゲーションプロパティにアクセスする必要がある場合は、一括読み込みで必要以上のデータを取得するため、遅延読み込みの方がパフォーマンスが向上する可能性があります。 パフォーマンスが重要な場合、最適な選択を行うために、両方の方法でパフォーマンスをテストすることをお勧めします。

通常、明示的な読み込みは、遅延読み込みを無効にした場合にのみ使用します。 遅延読み込みをオフにする必要があるシナリオの1つは、シリアル化時です。 遅延読み込みとシリアル化は十分に混同されていません。注意を払っていない場合は、遅延読み込みが有効になっている場合よりもはるかに多くのデータを照会できます。 通常、シリアル化は、型のインスタンスの各プロパティにアクセスすることによって機能します。 プロパティアクセスは遅延読み込みをトリガーし、それらの遅延読み込みされたエンティティをシリアル化します。 次に、シリアル化プロセスは、遅延読み込みされたエンティティの各プロパティにアクセスします。これにより、さらに遅延読み込みとシリアル化が発生する可能性があります。 この実行後のチェーンの反応を回避するには、エンティティをシリアル化する前に遅延読み込みをオフにします。

既定では、データベースコンテキストクラスは遅延読み込みを実行します。 遅延読み込みを無効にするには、次の2つの方法があります。

- 特定のナビゲーションプロパティについては、プロパティを宣言するときに `virtual` キーワードを省略します。
- すべてのナビゲーションプロパティについて、`LazyLoadingEnabled` を `false`に設定します。 たとえば、コンテキストクラスのコンストラクターに次のコードを配置できます。 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

遅延読み込みでは、パフォーマンスの問題を引き起こすコードをマスクできます。 たとえば、一括または明示的な読み込みを指定せずに大量のエンティティを処理し、各イテレーションで複数のナビゲーションプロパティを使用するコードは、データベースへのラウンドトリップが多くなるため、非常に非効率になる可能性があります。 オンプレミスの SQL server を使用して開発を正常に実行するアプリケーションでは、待機時間の増加と遅延読み込みのために Azure SQL Database に移動したときにパフォーマンスの問題が発生する可能性があります。 現実的なテスト負荷を使用してデータベースクエリをプロファイルすると、遅延読み込みが適切かどうかを判断するのに役立ちます。 詳細については、「 [Demystifying Entity Framework 方法: 関連データの読み込み](https://msdn.microsoft.com/magazine/hh205756.aspx)」と「 [Entity Framework を使用したネットワーク待機 SQL Azure 時間の短縮](https://msdn.microsoft.com/magazine/gg309181.aspx)」を参照してください。

## <a name="create-a-courses-index-page-that-displays-department-name"></a>学科名を表示するコースのインデックスページを作成する

`Course` エンティティには、コースが割り当てられている部署の `Department` エンティティを含むナビゲーションプロパティが含まれています。 割り当てられた部門の名前をコースの一覧に表示するには、`Course.Department` ナビゲーションプロパティにある `Department` エンティティから `Name` プロパティを取得する必要があります。

次の図に示すように、前に `Student` コントローラーで行ったのと同じオプションを使用して、`Course` エンティティ型の `CourseController` という名前のコントローラーを作成します (イメージとは異なり、コンテキストクラスは、モデルの名前空間ではなく、DAL 名前空間にあります)。

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

*Controllers\CourseController.cs*を開き、`Index` メソッドを確認します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

自動スキャフォールディングでは、`Include` メソッドを使って、`Department` ナビゲーション プロパティに一括読み込みを指定しています。

*Views\Course\Index.cshtml*を開き、既存のコードを次のコードに置き換えます。 変更が強調表示されています。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

スキャフォールディング コードに、次の変更を行いました。

- 見出しを **[インデックス]** から **[コース]** に変更しました。
- 行のリンクを左に移動しました。
- `CourseID` プロパティ値を示す列が見出し**番号**の下に追加されました。 (既定では、主キーは、通常、エンドユーザーにとって意味がないため、スキャフォールディングされません。 ただし、この場合、主キーは意味があり、表示する必要があります)。
- 最後の列見出しを**DepartmentID** (外部 `Department` キーの名前) から**Department**に変更しました。

最後の列では、スキャフォールディングコードによって、`Department` ナビゲーションプロパティに読み込まれる `Department` エンティティの `Name` プロパティが表示されます。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

ページを実行します (Contoso 大学のホームページの **[コース]** タブを選択します)。部署名の一覧が表示されます。

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>コースと加入契約を示す講師用のインデックスページを作成する

このセクションでは、インストラクターのインデックスページを表示するために、`Instructor` エンティティのコントローラーとビューを作成します。

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

このページは、次の方法で関連データを読み取って表示します。

- インストラクターの一覧には、`OfficeAssignment` エンティティの関連データが表示されます。 `Instructor` エンティティと `OfficeAssignment` エンティティは、一対ゼロまたは一対一のリレーションシップです。 `OfficeAssignment` エンティティに一括読み込みを使用します。 前述のように、通常、一括読み込みは、主テーブルで取得したすべての行の関連データが必要なときにより効率的です。 このケースでは、割り当てられたすべてのインストラクターのオフィスの割り当てを表示する必要があります。
- ユーザーがインストラクターを選択すると、関連する `Course` エンティティが表示されます。 `Instructor` エンティティと `Course` エンティティは多対多リレーションシップです。 `Course` エンティティとそれに関連する `Department` エンティティに一括読み込みを使用します。 この場合、選択したインストラクターのコースのみが必要になるため、遅延読み込みの方が効率的な場合があります。 ただし、この例では、ナビゲーション プロパティにあるエンティティ内のナビゲーション プロパティに一括読み込みを使用する方法を示します。
- ユーザーがコースを選択すると、`Enrollments` エンティティセットの関連データが表示されます。 `Course` エンティティと `Enrollment` エンティティは一対多リレーションシップです。 `Enrollment` エンティティとそれに関連する `Student` エンティティに対して明示的な読み込みを追加します。 (遅延読み込みが有効になっているため、明示的な読み込みは必要ありませんが、これは明示的な読み込みを行う方法を示しています)。

### <a name="create-a-view-model-for-the-instructor-index-view"></a>インストラクターのインデックスビューのビューモデルを作成する

インストラクターのインデックスページには、3つの異なるテーブルが表示されます。 そのため、テーブルの 1 つにデータを保持するごとに、3 つのプロパティを含むビュー モデルを作成します。

*Viewmodel*フォルダーで、 *InstructorIndexData.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>選択した行のスタイルを追加する

選択した行をマークするには、別の背景色が必要です。 この UI のスタイルを指定するには、次に示すように、次の強調表示されているコードを*contentsiteの*`/* info and errors */` セクションに追加します。

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>インストラクターのコントローラーとビューの作成

次の図に示すように、`InstructorController` コントローラーを作成します。

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

*Controllers\InstructorController.cs*を開き、`ViewModels` 名前空間の `using` ステートメントを追加します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

`Index` メソッドのスキャフォールディングコードは、`OfficeAssignment` ナビゲーションプロパティに対してのみ一括読み込みを指定します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

`Index` メソッドを次のコードに置き換えて、追加の関連データを読み込み、ビューモデルに配置します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

メソッドは、オプションのルートデータ (`id`) と、選択したインストラクターと選択したコースの ID 値を提供するクエリ文字列パラメーター (`courseID`) を受け取り、必要なすべてのデータをビューに渡します。 パラメーターは、ページの **Select** ハイパーリンクによって指定されます。

> [!TIP]
> 
> **ルートデータ**
> 
> Route data は、モデルバインダーがルーティングテーブルで指定された URL セグメントで見つかったデータです。 たとえば、既定のルートでは、`controller`、`action`、および `id` セグメントが指定されています。
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> 次の URL では、既定のルートは、`Instructor` を `controller`としてマップし、`Index` `action` として、1を `id`としてマップします。これらはルートデータ値です。
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "? courseID = 2021" はクエリ文字列値です。 モデルバインダーは、`id` をクエリ文字列値として渡す場合にも機能します。
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> Url は、Razor ビューの `ActionLink` ステートメントによって作成されます。 次のコードでは、`id` パラメーターが既定のルートと一致するため、`id` がルートデータに追加されます。
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> 次のコードでは、`courseID` が既定のルートのパラメーターと一致しないため、クエリ文字列として追加されます。
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

このコードは、ビュー モデルのインスタンスを作成し、インストラクターのリストに配置することから始めます。 このコードでは、`Instructor.OfficeAssignment` と `Instructor.Courses` ナビゲーションプロパティの一括読み込みを指定します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

2番目の `Include` メソッドは、コースを読み込み、読み込まれた各コースで `Course.Department` ナビゲーションプロパティの一括読み込みを行います。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

前述のように、一括読み込みは必要ありませんが、パフォーマンスを向上させるために行われます。 ビューには常に `OfficeAssignment` エンティティが必要であるため、同じクエリでフェッチする方が効率的です。 `Course` エンティティは、web ページでインストラクターが選択されている場合に必要になります。したがって、[なし] を選択した場合に比べて、ページがより頻繁に表示される場合のみ、一括読み込みの方が遅延読み込みより優れています。

[インストラクター ID] が選択されている場合は、選択したインストラクターがビューモデルのインストラクターの一覧から取得されます。 次に、ビューモデルの `Courses` プロパティが、そのインストラクターの `Courses` ナビゲーションプロパティからの `Course` エンティティと共に読み込まれます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

`Where` メソッドはコレクションを返しますが、この場合は、そのメソッドに渡された条件によって返されるのは、1つの `Instructor` エンティティだけになります。 `Single` メソッドは、コレクションを1つの `Instructor` エンティティに変換します。これにより、そのエンティティの `Courses` プロパティにアクセスできるようになります。

コレクションに項目が1つしかないことがわかっている場合は、コレクションに対して[1 つ](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)のメソッドを使用します。 `Single` メソッドは、渡されたコレクションが空である場合、または複数の項目がある場合に、例外をスローします。 別の方法としては[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)があります。これは、コレクションが空の場合に既定値 (この場合は`null`) を返します。 ただし、この場合も例外が発生します (`null` 参照の `Courses` プロパティを見つけようとする)。例外メッセージは、問題の原因を明確に示すものではありません。 `Single` メソッドを呼び出すと、`Where` メソッドを個別に呼び出す代わりに、`Where` 条件を渡すこともできます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

次の代わりに、

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

次に、コースが選択された場合、選択したコースはビュー モデルのコースのリストから取得されます。 次に、ビューモデルの `Enrollments` プロパティが、そのコースの `Enrollments` ナビゲーションプロパティからの `Enrollment` エンティティと共に読み込まれます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>インストラクターのインデックスビューの変更

*Views\Instructor\Index.cshtml*で、既存のコードを次のコードに置き換えます。 変更が強調表示されています。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

既存のコードに次の変更を行いました。

- モデル クラスが `InstructorIndexData` に変更されました。
- **Index** のページ タイトルが **Instructors** に変更されました。
- 行リンク列を左に移動しました。
- **FullName**列が削除されました。
- `item.OfficeAssignment` が null でない場合にのみ `item.OfficeAssignment.Location` を表示する**Office**列を追加しました。 (これは一対ゼロまたは一対一のリレーションシップであるため、関連する `OfficeAssignment` エンティティが存在しない可能性があります)。 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- 選択したインストラクターの `tr` 要素に `class="selectedrow"` を動的に追加するコードを追加しました。 これにより、前に作成した CSS クラスを使用して、選択した行の背景色が設定されます。 (`valign` 属性は、テーブルに複数行の列を追加するときに、次のチュートリアルで役に立ちます)。 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- 各行の [その他のリンクの直前に**選択する]** というラベルの新しい `ActionLink` が追加されました。選択したインストラクター ID が `Index` メソッドに送信されます。

アプリケーションを実行し、 **[インストラクター]** タブを選択します。このページには、関連する `OfficeAssignment` エンティティの [`Location`] プロパティと、関連する `OfficeAssignment` エンティティが存在しない場合の空のテーブルセルが表示されます。

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

*Views\Instructor\Index.cshtml*ファイルで、終了 `table` 要素 (ファイルの末尾) の後に、次の強調表示されたコードを追加します。 インストラクターが選択されている場合に、インストラクターに関連するコースの一覧が表示されます。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

このコードでは、ビュー モデルの `Courses` プロパティを読み取り、コースのリストを表示します。 また、選択したコースの ID を `Index` アクションメソッドに送信する `Select` ハイパーリンクも用意されています。

> [!NOTE]
> *.Css*ファイルは、ブラウザーによってキャッシュされます。 アプリケーションの実行時に変更が表示されない場合は、(CTRL キーを押しながら **[更新]** ボタンをクリックするか、ctrl キーを押しながら F5 キーを押す)、ハード更新を行います。

ページを実行し、インストラクターを選択します。 選択したインストラクターに割り当てられたコースを表示するグリッドを表示し、各コースに割り当てられた部門の名前を表示します。

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

追加したコード ブロックの後に、次のコードを追加します。 このコードは、コースを選択したときに、コースに登録されている受講者のリストを表示します。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

このコードは、コースに登録されている学生の一覧を表示するために、ビューモデルの `Enrollments` プロパティを読み取ります。

ページを実行し、インストラクターを選択します。 次に、コースを選択して、登録済みの受講者とその成績のリストを表示します。

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>明示的な読み込みの追加

*InstructorController.cs*を開き、選択したコースの登録の一覧を `Index` メソッドがどのように取得するかを確認します。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

インストラクターのリストを取得したときに、`Courses` ナビゲーションプロパティの一括読み込みを指定し、各コースの `Department` プロパティを指定しました。 次に、ビューモデルに `Courses` コレクションを配置します。これで、そのコレクション内の1つのエンティティから `Enrollments` ナビゲーションプロパティにアクセスしています。 `Course.Enrollments` ナビゲーションプロパティに一括読み込みを指定しなかったため、遅延読み込みの結果として、そのプロパティのデータがページに表示されます。

他の方法でコードを変更せずに遅延読み込みを無効にした場合、実際に存在していた登録数に関係なく、`Enrollments` プロパティは null になります。 この場合、`Enrollments` プロパティを読み込むには、一括読み込みまたは明示的な読み込みのいずれかを指定する必要があります。 一括読み込みを実行する方法については既に説明しました。 明示的な読み込みの例を表示するには、`Index` メソッドを次のコードに置き換えます。このコードは、`Enrollments` プロパティを明示的に読み込みます。 変更されたコードが強調表示されます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

選択した `Course` エンティティを取得すると、新しいコードによってそのコースの `Enrollments` ナビゲーションプロパティが明示的に読み込まれます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

次に、`Enrollment` エンティティに関連する各 `Student` エンティティを明示的に読み込みます。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

`Collection` メソッドを使用してコレクションプロパティを読み込むことに注意してくださいが、1つのエンティティのみを保持するプロパティの場合は、`Reference` メソッドを使用します。 ここで [講師用のインデックス] ページを実行すると、データの取得方法を変更しても、ページに表示される内容に違いはありません。

## <a name="summary"></a>要約

これで、3つのすべての方法 (lazy、一括、および explicit) を使用して、関連するデータをナビゲーションプロパティに読み込むことができました。 次のチュートリアルでは、関連データの更新方法を学習します。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [次へ](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
