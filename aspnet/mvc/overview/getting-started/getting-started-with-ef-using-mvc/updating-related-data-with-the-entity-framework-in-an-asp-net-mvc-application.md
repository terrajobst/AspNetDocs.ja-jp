---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリで EF を使用して関連データを更新する'
description: このチュートリアルでは、関連データを更新します。 ほとんどのリレーションシップでは、外部キーフィールドまたはナビゲーションプロパティを更新することによってこれを行うことができます。
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499300"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリで EF を使用して関連データを更新する

前のチュートリアルでは、関連データを表示しています。 このチュートリアルでは、関連データを更新します。 ほとんどのリレーションシップでは、外部キーフィールドまたはナビゲーションプロパティを更新することによってこれを行うことができます。 多対多リレーションシップの場合、Entity Framework は結合テーブルを直接公開しないため、適切なナビゲーションプロパティとの間でエンティティを追加したり削除したりできます。

以下の図は、使用するページの一部を示しています。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![コースでのインストラクターによる編集](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * コースページのカスタマイズ
> * [講師にオフィスを追加する] ページ
> * コースを講師ページに追加する
> * DeleteConfirmed の更新
> * オフィスの場所とコースを Create ページに追加する

## <a name="prerequisites"></a>前提条件

* [関連データの読み取り](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a>コースページのカスタマイズ

新しいコース エンティティが作成されると、既存の部門とのリレーションシップが必要になります。 これを容易にするため、スキャフォールディング コードには、コントローラーのメソッドと、部門を選択するためのドロップダウン リストを含む Create ビューと Edit ビューが含まれます。 ドロップダウンリストでは、`Course.DepartmentID` の外部キープロパティが設定されます。これは、適切な `Department` エンティティを使用して `Department` ナビゲーションプロパティを読み込むために必要な Entity Framework です。 このスキャフォールディング コードを使用しますが、エラー処理を追加し、ドロップダウン リストを並べ替えるために少し変更します。

*CourseController.cs*で、4つの `Create` と `Edit` メソッドを削除し、次のコードに置き換えます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

ファイルの先頭に次の `using` ステートメントを追加します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` メソッドは、名前で並べ替えられたすべての部門の一覧を取得し、ドロップダウンリストの `SelectList` コレクションを作成して、`ViewBag` プロパティのビューにコレクションを渡します。 このメソッドは、ドロップダウン リストがレンダリングされるときに選択される項目を指定するためのコード呼び出しを許可する、省略可能な `selectedDepartment` パラメーターを受け取ります。 ビューでは `DepartmentID` 名前が[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)ヘルパーに渡され、ヘルパーは `DepartmentID`という名前の `SelectList` の `ViewBag` オブジェクトを検索することを認識します。

`HttpGet` `Create` メソッドは、選択された項目を設定せずに `PopulateDepartmentsDropDownList` メソッドを呼び出します。これは、新しいコースでは、部門がまだ確立されていないためです。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` メソッドは、選択した項目を、編集するコースに既に割り当てられている部署の ID に基づいて設定します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

`Create` と `Edit` の両方の `HttpPost` メソッドには、エラー発生後にページを再表示するときに選択した項目を設定するコードも含まれています。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

このコードにより、ページを再表示してエラーメッセージが表示されるようになり、選択した部門が選択されたままになります。

コースビューは既に department フィールドのドロップダウンリストにスキャフォールディングていますが、このフィールドには DepartmentID キャプションは必要ないので、 *Views\Course\Create.cshtml*ファイルに対して次の強調表示された変更を行い、キャプションを変更します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

*Views\Course\Edit.cshtml*で同じ変更を行います。

通常、scaffolder は、キー値がデータベースによって生成され、変更することはできず、ユーザーに表示される意味のある値ではないため、主キーをスキャフォールディングしません。 Course エンティティの場合、scaffolder には `CourseID` フィールドのテキストボックスが含まれています。これは、ユーザーが主キーの値を入力できる必要があることを `DatabaseGeneratedOption.None` 属性で認識しているためです。 しかし、数値は意味があるため、他のビューで表示することをお勧めします。そのため、手動で追加する必要があります。

*Views\Course\Edit.cshtml*で、 **[タイトル]** フィールドの前に "Course number" フィールドを追加します。 これは主キーであるため、表示されますが、変更することはできません。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

編集ビューでは、コース番号の隠しフィールド (`Html.HiddenFor` ヘルパー) が既に存在しています。 ヘルパー*の .html*を追加しても、ユーザーが 編集 ページの **保存** をクリックしたときに、ポストされたデータにコース番号が含まれないため、隠しフィールドは不要になります。

*Views\Course\Delete.cshtml*と*Views\Course\Details.cshtml*で、学科名のキャプションを "Name" から "department" に変更し、 **[タイトル]** フィールドの前に "Course number" フィールドを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

**[作成]** ページを実行し (コースのインデックス ページを表示し、 **[新規作成]** をクリックして)、新しいコースのデータを入力します。

| 値 | 設定 |
| ----- | ------- |
| Number | 「 *1000*」と入力します。 |
| タイトル | *代数*を入力します。 |
| 謝辞 | 「 *4*」と入力します。 |
|部署 | **[数学]** を選択します。 |

**Create** をクリックしてください。 新しいコースが一覧に追加された状態で、Course Index ページが表示されます。 Index ページのリストの部門名は、ナビゲーション プロパティから取得され、リレーションシップが正常に確立されていることを示しています。

**編集**ページを実行します (コースのインデックスページを表示し、コースで **[編集]** をクリックします)。

ページ上のデータを変更し、 **[Save]\(保存\)** をクリックします。 コースデータが更新された状態で、コースのインデックスページが表示されます。

## <a name="add-office-to-instructors-page"></a>[講師にオフィスを追加する] ページ

インストラクター レコードを編集するときに、インストラクターのオフィスの割り当ての更新が必要な場合があります。 `Instructor` エンティティには、`OfficeAssignment` エンティティとの一対ゼロまたは一対一のリレーションシップがあります。つまり、次のような状況を処理する必要があります。

- ユーザーがオフィスの割り当てをクリアし、最初に値を持っていた場合は、`OfficeAssignment` エンティティを削除して削除する必要があります。
- ユーザーがオフィスの割り当て値を入力し、最初は空だった場合は、新しい `OfficeAssignment` エンティティを作成する必要があります。
- ユーザーがオフィスの割り当ての値を変更した場合は、既存の `OfficeAssignment` エンティティの値を変更する必要があります。

*InstructorController.cs*を開き、`HttpGet` `Edit` 方法を確認します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

スキャフォールディングのコードは、必要なものではありません。 ドロップダウンリストのデータは設定されていますが、必要なのはテキストボックスです。 このメソッドを次のコードに置き換えます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

このコードは、`ViewBag` ステートメントを削除し、関連付けられた `OfficeAssignment` エンティティの一括読み込みを追加します。 `Find` メソッドを使用して一括読み込みを実行することはできません。そのため、`Where` と `Single` のメソッドを使用してインストラクターを選択します。

`HttpPost` `Edit` メソッドを次のコードに置き換えます。 office 割り当ての更新を処理します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`RetryLimitExceededException` への参照には、`using` ステートメントが必要です。これを追加するには、`RetryLimitExceededException`上にマウスポインターを置きます。 次のメッセージが表示されます: ![ 再試行の例外メッセージ](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

**潜在的な修正プログラムの表示** を選択し、次へ を**使用**します。

![再試行の例外を解決する](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

このコードは、次の処理を実行します。

- シグネチャが `HttpGet` メソッドと同じであるため、メソッド名を `EditPost` に変更します (`ActionName` 属性では、/Edit/URL が引き続き使用されていることを指定します)。
- `Instructor` ナビゲーション プロパティの一括読み込みを使用して、現在の `OfficeAssignment` エンティティをデータベースから取得します。 これは、`HttpGet` `Edit` メソッドで行ったものと同じです。
- モデル バインダーからの値を使用して、取得した `Instructor` エンティティを更新します。 使用する[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)オーバーロードを使用すると、含めるプロパティを*ホワイトリスト*に追加できます。 これにより、 [2 番目のチュートリアル](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)で説明されているように、過剰なポストを防ぐことができます。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- オフィスの場所が空白の場合は、`Instructor.OfficeAssignment` プロパティを null に設定して、`OfficeAssignment` テーブル内の関連する行が削除されるようにします。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- データベースへの変更を保存します。

*Views\Instructor\Edit.cshtml*で、 **[入社日]** フィールドの `div` 要素の後に、オフィスの場所を編集するための新しいフィールドを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

ページを実行します ([インストラクター **] タブを選択し、インストラクター**の **[編集]** をクリックします)。 **[Office Location]\(オフィスの場所\)** を変更し、 **[Save]\(保存\)** をクリックします。

## <a name="add-courses-to-instructors-page"></a>コースを講師ページに追加する

インストラクターは、任意の数のコースを担当する場合があります。 次に、チェックボックスのグループを使用してコースの割り当てを変更する機能を追加して、インストラクターの編集ページを拡張します。

`Course` エンティティと `Instructor` エンティティ間のリレーションシップは多対多であるため、結合テーブル内の外部キープロパティに直接アクセスすることはできません。 代わりに、`Instructor.Courses` ナビゲーションプロパティからエンティティを追加および削除します。

インストラクターに割り当てられるコースを変更できるようにする UI は、チェック ボックスのグループです。 データベース内のすべてのコースのチェック ボックスが表示され、インストラクターに現在割り当てられているコースが選択されます。 ユーザーは、チェック ボックスをオンまたはオフにしてコースの割り当てを変更できます。 コースの数がはるかに多い場合は、ビューにデータを表示する別の方法を使用することをお勧めしますが、リレーションシップを作成または削除するには、ナビゲーションプロパティを操作するのと同じ方法を使用します。

チェック ボックスのリストのためにデータをビューに提供するには、ビュー モデル クラスを使用します。 *Viewmodel*フォルダーに*AssignedCourseData.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

*InstructorController.cs*で、`HttpGet` `Edit` メソッドを次のコードに置き換えます。 変更が強調表示されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

このコードは、`Courses` ナビゲーション プロパティに一括読み込みを追加し、新しい `PopulateAssignedCourseData` メソッドを呼び出して、`AssignedCourseData` ビュー モデル クラスを使用してチェック ボックス配列に情報を提供します。

`PopulateAssignedCourseData` メソッドのコードは、ビューモデルクラスを使用してコースのリストを読み込むために、すべての `Course` エンティティを読み取ります。 各コースに対し、コードはそのコースがインストラクターの `Courses` ナビゲーション プロパティ内に存在しているかどうかをチェックします。 コースがインストラクターに割り当てられているかどうかを確認するときに効率的な検索を作成するには、インストラクターに割り当てられたコースを[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)コレクションに含めます。 `Assigned` プロパティは、インストラクターが割り当てられているコースの `true` に設定されます。 ビューは、このプロパティを使用して、どのチェック ボックスを選択済みとして表示する必要があるかを判断します。 最後に、リストは `ViewBag` プロパティのビューに渡されます。

次に、ユーザーが **[Save]\(保存\)** をクリックしたときに実行されるコードを追加します。 `EditPost` メソッドを次のコードに置き換えます。このコードは、`Instructor` エンティティの `Courses` ナビゲーションプロパティを更新する新しいメソッドを呼び出します。 変更が強調表示されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

メソッドシグネチャが `HttpGet` `Edit` メソッドとは異なるようになったため、メソッド名は `EditPost` から `Edit`に変更されます。

ビューには `Course` エンティティのコレクションがないため、モデルバインダーは、`Courses` ナビゲーションプロパティを自動的に更新することはできません。 モデルバインダーを使用して `Courses` ナビゲーションプロパティを更新する代わりに、新しい `UpdateInstructorCourses` メソッドでこれを行います。 そのため、モデル バインドから `Courses` プロパティを除外する必要があります。 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)を呼び出すコードを変更する必要はありません。これは、ホワイトリスト*のオーバーロードを*使用していて、`Courses` が含まれていないためです。

チェックボックスが選択されていない場合、`UpdateInstructorCourses` のコードは、空のコレクションで `Courses` ナビゲーションプロパティを初期化します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

その後コードは、データベース内のすべてのコースをループ処理し、各コースを現在インストラクターに割り当てられているコースとビューで選択されているコースを比較してチェックします。 検索を効率化するため、最後の 2 つのコレクションが `HashSet` オブジェクトに格納されます。

コースのチェック ボックスが選択されたが、そのコースが `Instructor.Courses`ナビゲーション プロパティにない場合、そのコースがナビゲーション プロパティ内のコレクションに追加されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

コースのチェック ボックスが選択さていないが、そのコースが `Instructor.Courses`ナビゲーション プロパティにある場合、そのコースがナビゲーション プロパティから削除されます。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

*Views\Instructor\Edit.cshtml*で、次のコードを `OfficeAssignment` フィールドの `div` 要素の直後、および **[保存]** ボタンの `div` 要素の前に追加して、チェックボックスの配列を含む**course フィールドを**追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

コードを貼り付けた後、改行やインデントがここに表示されない場合は、すべてを手動で修正して、ここに表示されているようにします。 インデントは完璧である必要はありませんが、`@</tr><tr>`、`@:<td>`、`@:</td>`、および `@</tr>` の行は、示されているようにそれぞれ 1 行にする必要があります。そうしないと、ランタイム エラーが発生します。

このコードは、3 つの列を含む HTML テーブルを作成します。 各列には、チェック ボックスとその後に続くキャプションがあります。キャプションは、コース番号とタイトルから構成されます。 すべてのチェックボックスに同じ名前 ("selectedCourses") があります。これは、グループとして扱われることをモデルバインダーに通知します。 各チェックボックスの `value` 属性は、ページがポストされるときに `CourseID.` の値に設定されます。モデルバインダーは、選択されているチェックボックスのみの `CourseID` 値で構成される配列をコントローラーに渡します。

チェックボックスが最初に表示されたときに、インストラクターに割り当てられているコースの属性には `checked` の属性があります (チェックボックスがオンになっています)。

コースの割り当てを変更した後、サイトが `Index` ページに戻ったときに変更を確認できるようにする必要があります。 そのため、そのページのテーブルに列を追加する必要があります。 この場合、`ViewBag` オブジェクトを使用する必要はありません。表示する情報は、モデルとしてページに渡す `Instructor` エンティティの `Courses` ナビゲーションプロパティに既に存在しているためです。

*Views\Instructor\Index.cshtml*で、次の例に示すように、 **Office**見出しの直後に**コース**見出しを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

次に、[office location detail] セルの直後に新しい詳細セルを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

インストラクターの**インデックス**ページを実行して、各インストラクターに割り当てられているコースを確認します。

インストラクターの **[編集]** をクリックして、編集ページを表示します。

いくつかのコースの割り当てを変更し、 **[保存]** をクリックします。 行った変更が Index ページに反映されます。

 注: インストラクターコースデータを編集するために使用する方法は、コースの数が限られている場合に適しています。 非常に大きいコレクションの場合、別の UI と別の更新方法が必要になる場合があります。

## <a name="update-deleteconfirmed"></a>DeleteConfirmed の更新

*InstructorController.cs*で、`DeleteConfirmed` メソッドを削除し、その場所に次のコードを挿入します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

このコードにより、次のように変更されます。

- インストラクターが任意の部門の管理者として割り当てられている場合、はその部門からインストラクターの割り当てを削除します。 このコードがないと、部門の管理者として割り当てられたインストラクターを削除しようとすると、参照整合性エラーが発生します。

このコードでは、複数の部門の管理者として割り当てられた1人のインストラクターのシナリオを処理しません。 最後のチュートリアルでは、このシナリオが発生しないようにするコードを追加します。

## <a name="add-office-location-and-courses-to-the-create-page"></a>オフィスの場所とコースを Create ページに追加する

*InstructorController.cs*で、`HttpGet` と `HttpPost` `Create` メソッドを削除し、その場所に次のコードを追加します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

このコードは、最初はコースが選択されていない点を除いて、Edit メソッドで見たものと似ています。 `HttpGet` `Create` メソッドは、コースが選択されている可能性がありますが、ビューの `foreach` ループに空のコレクションを提供するために、`PopulateAssignedCourseData` メソッドを呼び出します (それ以外の場合、ビューコードは null 参照例外をスローします)。

HttpPost の Create メソッドは、検証エラーをチェックし、新しいインストラクターをデータベースに追加するテンプレートコードの前に、選択した各コースを course ナビゲーションプロパティに追加します。 モデルエラーが発生した場合でもコースが追加されるので (たとえば、ユーザーが無効な日付でキーを指定した場合)、ページがエラーメッセージと共に再表示されると、実行されたすべてのコース選択が自動的に復元されます。

コースを `Courses` ナビゲーション プロパティに追加できるようにするには、プロパティを空のコレクションとして初期化する必要があることに注意してください。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

コントローラー コードでこれを行うための別の方法として、Instructor モデルでこれを行うことができます。このためには、プロパティ ゲッターを変更して、コレクションが存在しない場合に自動的に作成するようにします。次の例に示します。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Courses` プロパティをこの方法で変更する場合、コントローラー内の明示的なプロパティの初期化コードを削除することができます。

*Views\Instructor\Create.cshtml*で、入社日] フィールドの後、 **[送信]** ボタンの前に、[オフィスの場所 テキストボックスとコースのチェックボックスを追加します。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

コードを貼り付けた後、前に編集ページで行ったように、改行とインデントを修正します。

[作成] ページを実行し、インストラクターを追加します。

<a id="transactions"></a>

## <a name="handling-transactions"></a>トランザクションの処理

[基本的な CRUD 機能のチュートリアル](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)で説明したように、既定では Entity Framework はトランザクションを暗黙的に実装します。 より詳細な制御が必要なシナリオ (たとえば、トランザクションで Entity Framework 以外で行われた操作を含める場合) については、「MSDN での[トランザクション](https://msdn.microsoft.com/data/dn456843)の使用」を参照してください。

## <a name="get-the-code"></a>コードの入手

[完成したプロジェクトをダウンロードする](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他のリソース

その他の Entity Framework リソースへのリンクについては[、「ASP.NET Data Access-推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

## <a name="next-step"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * カスタマイズしたコースページ
> * インストラクターのページに office を追加しました
> * コースを講師ページに追加しました
> * 更新された DeleteConfirmed 確定
> * 作成ページにオフィスの場所とコースを追加しました

次の記事に進み、非同期プログラミングモデルを実装する方法を学習してください。
> [!div class="nextstepaction"]
> [非同期プログラミングモデル](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
