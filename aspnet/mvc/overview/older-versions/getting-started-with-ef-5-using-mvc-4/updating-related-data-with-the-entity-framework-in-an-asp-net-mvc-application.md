---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの更新 (6/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468286"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの更新 (6/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、関連データを表示していました。このチュートリアルでは、関連データを更新します。 ほとんどのリレーションシップでは、適切な外部キーフィールドを更新することによってこれを行うことができます。 多対多リレーションシップの場合、Entity Framework は結合テーブルを直接公開しないため、適切なナビゲーションプロパティとの間でエンティティを明示的に追加および削除する必要があります。

以下の図は、使用するページを示しています。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>Courses の Create ページと Edit ページをカスタマイズする

新しいコース エンティティが作成されると、既存の部門とのリレーションシップが必要になります。 これを容易にするため、スキャフォールディング コードには、コントローラーのメソッドと、部門を選択するためのドロップダウン リストを含む Create ビューと Edit ビューが含まれます。 ドロップダウンリストでは、`Course.DepartmentID` の外部キープロパティが設定されます。これは、適切な `Department` エンティティを使用して `Department` ナビゲーションプロパティを読み込むために必要な Entity Framework です。 このスキャフォールディング コードを使用しますが、エラー処理を追加し、ドロップダウン リストを並べ替えるために少し変更します。

*CourseController.cs*で、4つの `Edit` と `Create` メソッドを削除し、次のコードに置き換えます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList` メソッドは、名前で並べ替えられたすべての部門の一覧を取得し、ドロップダウンリストの `SelectList` コレクションを作成して、`ViewBag` プロパティのビューにコレクションを渡します。 このメソッドは、ドロップダウン リストがレンダリングされるときに選択される項目を指定するためのコード呼び出しを許可する、省略可能な `selectedDepartment` パラメーターを受け取ります。 ビューは `DepartmentID` 名前を[`DropDownList` ヘルパー](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)に渡し、ヘルパーは `DepartmentID`という名前の `SelectList` の `ViewBag` オブジェクトを検索することを認識します。

`HttpGet` `Create` メソッドは、選択された項目を設定せずに `PopulateDepartmentsDropDownList` メソッドを呼び出します。これは、新しいコースでは、部門がまだ確立されていないためです。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` メソッドは、選択した項目を、編集するコースに既に割り当てられている部署の ID に基づいて設定します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`Create` と `Edit` の両方の `HttpPost` メソッドには、エラー発生後にページを再表示するときに選択した項目を設定するコードも含まれています。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

このコードにより、ページを再表示してエラーメッセージが表示されるようになり、選択した部門が選択されたままになります。

*Views\Course\Create.cshtml*で、強調表示されたコードを追加して、 **[タイトル]** フィールドの前に新しい "Course number" フィールドを作成します。 前のチュートリアルで説明したように、主キーフィールドは既定ではスキャフォールディングませんが、この主キーは意味があるため、ユーザーがキー値を入力できるようにする必要があります。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

*Views\Course\Edit.cshtml*、 *Views\Course\Delete.cshtml*、および*Views\Course\Details.cshtml*で、 **Title**フィールドの前に "Course number" フィールドを追加します。 これは主キーであるため、表示されますが、変更することはできません。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

**[作成]** ページを実行し (コースのインデックス ページを表示し、 **[新規作成]** をクリックして)、新しいコースのデータを入力します。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

**Create** をクリックしてください。 新しいコースが一覧に追加された状態で、Course Index ページが表示されます。 Index ページのリストの部門名は、ナビゲーション プロパティから取得され、リレーションシップが正常に確立されていることを示しています。

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

**編集**ページを実行します (コースのインデックスページを表示し、コースで **[編集]** をクリックします)。

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

ページ上のデータを変更し、 **[Save]\(保存\)** をクリックします。 コースデータが更新された状態で、コースのインデックスページが表示されます。

## <a name="adding-an-edit-page-for-instructors"></a>インストラクターの編集ページを追加する

インストラクター レコードを編集するときに、インストラクターのオフィスの割り当ての更新が必要な場合があります。 `Instructor` エンティティには、`OfficeAssignment` エンティティとの一対ゼロまたは一対一のリレーションシップがあります。つまり、次のような状況を処理する必要があります。

- ユーザーがオフィスの割り当てをクリアし、最初に値を持っていた場合は、`OfficeAssignment` エンティティを削除して削除する必要があります。
- ユーザーがオフィスの割り当て値を入力し、最初は空だった場合は、新しい `OfficeAssignment` エンティティを作成する必要があります。
- ユーザーがオフィスの割り当ての値を変更した場合は、既存の `OfficeAssignment` エンティティの値を変更する必要があります。

*InstructorController.cs*を開き、`HttpGet` `Edit` 方法を確認します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

スキャフォールディングのコードは、必要なものではありません。 ドロップダウンリストのデータは設定されていますが、必要なのはテキストボックスです。 このメソッドを次のコードに置き換えます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

このコードは、`ViewBag` ステートメントを削除し、関連付けられた `OfficeAssignment` エンティティの一括読み込みを追加します。 `Find` メソッドを使用して一括読み込みを実行することはできません。そのため、`Where` と `Single` のメソッドを使用してインストラクターを選択します。

`HttpPost` `Edit` メソッドを次のコードに置き換えます。 office 割り当ての更新を処理します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

このコードは、次の処理を実行します。

- `Instructor` ナビゲーション プロパティの一括読み込みを使用して、現在の `OfficeAssignment` エンティティをデータベースから取得します。 これは、`HttpGet` `Edit` メソッドで行ったものと同じです。
- モデル バインダーからの値を使用して、取得した `Instructor` エンティティを更新します。 使用する[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)オーバーロードを使用すると、含めるプロパティを*ホワイトリスト*に追加できます。 これにより、 [2 番目のチュートリアル](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)で説明されているように、過剰なポストを防ぐことができます。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- オフィスの場所が空白の場合は、`Instructor.OfficeAssignment` プロパティを null に設定して、`OfficeAssignment` テーブル内の関連する行が削除されるようにします。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- データベースへの変更を保存します。

*Views\Instructor\Edit.cshtml*で、 **[入社日]** フィールドの `div` 要素の後に、オフィスの場所を編集するための新しいフィールドを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

ページを実行します ([インストラクター **] タブを選択し、インストラクター**の **[編集]** をクリックします)。 **[Office Location]\(オフィスの場所\)** を変更し、 **[Save]\(保存\)** をクリックします。

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>インストラクターの編集ページにコースの割り当てを追加する

インストラクターは、任意の数のコースを担当する場合があります。 次のスクリーン ショットに示すように、チェック ボックスのグループを使用して、コースの割り当てを変更する機能を追加して、Instructor/Edit ページを拡張します。

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

`Course` エンティティと `Instructor` エンティティ間のリレーションシップは多対多であるため、結合テーブルに直接アクセスすることはできません。 代わりに、`Instructor.Courses` ナビゲーションプロパティからエンティティを追加および削除します。

インストラクターに割り当てられるコースを変更できるようにする UI は、チェック ボックスのグループです。 データベース内のすべてのコースのチェック ボックスが表示され、インストラクターに現在割り当てられているコースが選択されます。 ユーザーは、チェック ボックスをオンまたはオフにしてコースの割り当てを変更できます。 コースの数がはるかに多い場合は、ビューにデータを表示する別の方法を使用することをお勧めしますが、リレーションシップを作成または削除するには、ナビゲーションプロパティを操作するのと同じ方法を使用します。

チェック ボックスのリストのためにデータをビューに提供するには、ビュー モデル クラスを使用します。 *Viewmodel*フォルダーに*AssignedCourseData.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

*InstructorController.cs*で、`HttpGet` `Edit` メソッドを次のコードに置き換えます。 変更が強調表示されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

このコードは、`Courses` ナビゲーション プロパティに一括読み込みを追加し、新しい `PopulateAssignedCourseData` メソッドを呼び出して、`AssignedCourseData` ビュー モデル クラスを使用してチェック ボックス配列に情報を提供します。

`PopulateAssignedCourseData` メソッドのコードは、ビューモデルクラスを使用してコースのリストを読み込むために、すべての `Course` エンティティを読み取ります。 各コースに対し、コードはそのコースがインストラクターの `Courses` ナビゲーション プロパティ内に存在しているかどうかをチェックします。 コースがインストラクターに割り当てられているかどうかを確認するときに効率的な検索を作成するには、インストラクターに割り当てられたコースを[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)コレクションに含めます。 `Assigned` プロパティは、インストラクターが割り当てられているコースの `true` に設定されます。 ビューは、このプロパティを使用して、どのチェック ボックスを選択済みとして表示する必要があるかを判断します。 最後に、リストは `ViewBag` プロパティのビューに渡されます。

次に、ユーザーが **[Save]\(保存\)** をクリックしたときに実行されるコードを追加します。 `HttpPost` `Edit` メソッドを次のコードに置き換えます。このコードは、`Instructor` エンティティの `Courses` ナビゲーションプロパティを更新する新しいメソッドを呼び出します。 変更が強調表示されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

ビューには `Course` エンティティのコレクションがないため、モデルバインダーは、`Courses` ナビゲーションプロパティを自動的に更新することはできません。 モデルバインダーを使用して course ナビゲーションプロパティを更新するのではなく、新しい `UpdateInstructorCourses` メソッドで作成します。 そのため、モデル バインドから `Courses` プロパティを除外する必要があります。 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)を呼び出すコードを変更する必要はありません。これは、ホワイトリスト*のオーバーロードを*使用していて、`Courses` が含まれていないためです。

チェックボックスが選択されていない場合、`UpdateInstructorCourses` のコードは、空のコレクションで `Courses` ナビゲーションプロパティを初期化します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

その後コードは、データベース内のすべてのコースをループ処理し、各コースを現在インストラクターに割り当てられているコースとビューで選択されているコースを比較してチェックします。 検索を効率化するため、最後の 2 つのコレクションが `HashSet` オブジェクトに格納されます。

コースのチェック ボックスが選択されたが、そのコースが `Instructor.Courses`ナビゲーション プロパティにない場合、そのコースがナビゲーション プロパティ内のコレクションに追加されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

コースのチェック ボックスが選択さていないが、そのコースが `Instructor.Courses`ナビゲーション プロパティにある場合、そのコースがナビゲーション プロパティから削除されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

*Views\Instructor\Edit.cshtml*で、次の強調表示されたコードを `OfficeAssignment` フィールドの `div` 要素の直後に追加して、チェックボックスの配列を含む**course フィールドを**追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

このコードは、3 つの列を含む HTML テーブルを作成します。 各列には、チェック ボックスとその後に続くキャプションがあります。キャプションは、コース番号とタイトルから構成されます。 すべてのチェックボックスに同じ名前 ("selectedCourses") があります。これは、グループとして扱われることをモデルバインダーに通知します。 各チェックボックスの `value` 属性は、ページがポストされるときに `CourseID.` の値に設定されます。モデルバインダーは、選択されているチェックボックスのみの `CourseID` 値で構成される配列をコントローラーに渡します。

チェックボックスが最初に表示されたときに、インストラクターに割り当てられているコースの属性には `checked` の属性があります (チェックボックスがオンになっています)。

コースの割り当てを変更した後、サイトが `Index` ページに戻ったときに変更を確認できるようにする必要があります。 そのため、そのページのテーブルに列を追加する必要があります。 この場合、`ViewBag` オブジェクトを使用する必要はありません。表示する情報は、モデルとしてページに渡す `Instructor` エンティティの `Courses` ナビゲーションプロパティに既に存在しているためです。

*Views\Instructor\Index.cshtml*で、次の例に示すように、 **Office**見出しの直後に**コース**見出しを追加します。

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

次に、[office location detail] セルの直後に新しい詳細セルを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

インストラクターの**インデックス**ページを実行して、各インストラクターに割り当てられているコースを確認します。

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

インストラクターの **[編集]** をクリックして、編集ページを表示します。

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

いくつかのコースの割り当てを変更し、 **[保存]** をクリックします。 行った変更が Index ページに反映されます。

 注: インストラクターコースデータを編集する方法は、コースの数が限られている場合に適しています。 非常に大きいコレクションの場合、別の UI と別の更新方法が必要になる場合があります。  

## <a name="update-the-delete-method"></a>Delete メソッドを更新する

次のように、HttpPost Delete メソッドのコードを変更して、講師が削除されたときに office 割り当てレコード (存在する場合) が削除されるようにします。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

管理者として部門に割り当てられているインストラクターを削除しようとすると、参照整合性エラーが発生します。 インストラクターが管理者として割り当てられている任意の部門からインストラクターを自動的に削除するその他のコードについては[、このチュートリアルの現在のバージョン](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)を参照してください。

## <a name="summary"></a>まとめ

これで、関連データの操作の概要が完了しました。 ここまでのチュートリアルでは、さまざまな CRUD 操作を行ってきましたが、同時実行の問題については扱いませんでした。 次のチュートリアルでは、同時実行のトピックを紹介し、それを処理するためのオプションについて説明し、1つのエンティティ型に対して既に記述した CRUD コードに同時実行処理を追加します。

その他の Entity Framework リソースへのリンクについては、[このシリーズの最後のチュートリアル](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)の最後に記載されています。

> [!div class="step-by-step"]
> [前へ](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
