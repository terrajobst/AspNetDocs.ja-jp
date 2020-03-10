---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 4 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518284"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート4

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="working-with-related-data"></a>関連データの操作

前のチュートリアルでは、`EntityDataSource` コントロールを使用して、データのフィルター処理、並べ替え、およびグループ化を行っていました。 このチュートリアルでは、関連データを表示および更新します。

インストラクターの一覧を表示する講師ページを作成します。 インストラクターを選択すると、そのインストラクターがトレーニングしたコースの一覧が表示されます。 コースを選択すると、コースの詳細と、コースに登録されている学生の一覧が表示されます。 講師の名前、採用日、およびオフィスの割り当てを編集できます。 オフィスの割り当ては、ナビゲーションプロパティを使用してアクセスする個別のエンティティセットです。

マークアップまたはコードで、マスターデータを詳細データにリンクすることができます。 チュートリアルのこの部分では、両方の方法を使用します。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>GridView コントロールの関連エンティティの表示と更新

*.Master* *という名前の*新しい web ページを作成し、次のマークアップを `Content2`という名前の `Content` コントロールに追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

このマークアップは、インストラクターを選択して更新を有効にする `EntityDataSource` コントロールを作成します。 `div` 要素は、後で列を追加できるように、左に表示するマークアップを構成します。

`EntityDataSource` マークアップと終了 `</div>` タグの間に、`GridView` コントロールを作成する次のマークアップと、エラーメッセージに使用する `Label` コントロールを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

この `GridView` コントロールを使用すると、行の選択が可能になり、選択した行が明るい灰色の背景色で強調表示されます。また、`SelectedIndexChanged` イベントと `Updating` イベントに対して、後で作成するハンドラーを指定します。 また、`DataKeyNames` プロパティの `PersonID` を指定して、選択した行のキー値を後で追加する別のコントロールに渡すことができるようにします。

最後の列には、インストラクターのオフィスの割り当てが含まれています。これは、関連付けられているエンティティからのものであるため、`Person` エンティティのナビゲーションプロパティに格納されています。 `EditItemTemplate` 要素は `Bind`ではなく `Eval` を指定していることに注意してください。これは、`GridView` コントロールがナビゲーションプロパティに直接バインドして更新することができないためです。 コードでオフィスの割り当てを更新します。 これを行うには、`TextBox` コントロールへの参照が必要です。これを取得して、`TextBox` コントロールの `Init` イベントに保存します。

`GridView` コントロールに従うことは、エラーメッセージに使用される `Label` コントロールです。 コントロールの `Visible` プロパティは `false`、ビューステートはオフになっています。これにより、エラーに応じてコードが表示される場合にのみ、ラベルが表示されるようになります。

*Instructors.aspx.cs*ファイルを開き、次の `using` ステートメントを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

[Office の割り当て] テキストボックスへの参照を保持するために、部分クラス名の宣言の直後にプライベートクラスフィールドを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

後でコードを追加する `SelectedIndexChanged` イベントハンドラーのスタブを追加します。 また、office 割り当て `TextBox` コントロールの `Init` イベントのハンドラーを追加して、`TextBox` コントロールへの参照を格納できるようにします。 この参照を使用して、ナビゲーションプロパティに関連付けられているエンティティを更新するためにユーザーが入力した値を取得します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

`GridView` コントロールの `Updating` イベントを使用して、関連付けられている `OfficeAssignment` エンティティの `Location` プロパティを更新します。 `Updating` イベントに対して次のハンドラーを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

このコードは、ユーザーが `GridView` 行で  **Update (更新**) をクリックしたときに実行されます。 このコードでは、イベント引数から選択された行の `PersonID` を使用して、現在の `Person` エンティティに関連付けられている `OfficeAssignment` エンティティを取得するために LINQ to Entities を使用します。

このコードは、`InstructorOfficeTextBox` コントロールの値に応じて、次のいずれかのアクションを実行します。

- テキストボックスに値があり、更新する `OfficeAssignment` エンティティがない場合は、それが作成されます。
- テキストボックスに値があり、`OfficeAssignment` エンティティがある場合は、`Location` プロパティ値が更新されます。
- テキストボックスが空で `OfficeAssignment` エンティティが存在する場合は、エンティティが削除されます。

その後、変更内容がデータベースに保存されます。 例外が発生した場合は、エラーメッセージが表示されます。

ページを実行します。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

**[編集]** をクリックすると、すべてのフィールドがテキストボックスに変わります。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

**Office の割り当て**など、これらの値のいずれかを変更します。 **[更新]** をクリックすると、一覧に反映された変更が表示されます。

## <a name="displaying-related-entities-in-a-separate-control"></a>別のコントロールでの関連エンティティの表示

各インストラクターは1つまたは複数のコースを教えることができるので、`EntityDataSource` コントロールと `GridView` コントロールを追加して、インストラクター `GridView` コントロールで選択されているインストラクターに関連するコースの一覧を表示します。 Course エンティティの見出しと `EntityDataSource` コントロールを作成するには、エラーメッセージ `Label` コントロールと終了 `</div>` タグの間に次のマークアップを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` パラメーターには、`InstructorsGridView` コントロールで行が選択されているインストラクターの `PersonID` の値が含まれています。 `Where` プロパティには、`Course` エンティティの `People` ナビゲーションプロパティから関連付けられているすべての `Person` エンティティを取得し、関連付けられているいずれかの `Course` エンティティに選択した `Person` 値が含まれている場合にのみ、`PersonID` エンティティを選択するサブセレクトコマンドが含まれています。

`GridView` コントロールを作成するには、`CoursesEntityDataSource` コントロールの直後 (終了 `</div>` タグの前) に次のマークアップを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

インストラクターが選択されていない場合はコースが表示されないため、`EmptyDataTemplate` 要素が含まれます。

ページを実行します。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

1つ以上のコースが割り当てられているインストラクターを選択すると、コースやコースが一覧に表示されます。 (注: データベーススキーマでは複数のコースが許可されていますが、データベースに用意されているテストデータでは、インストラクターには複数のコースがありません。 **サーバーエクスプローラー**ウィンドウまたは*CoursesAdd*ページを使用して、データベースにコースを追加できます。このページは、後のチュートリアルで追加します)。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` コントロールには、いくつかのコースフィールドのみが表示されます。 コースの詳細をすべて表示するには、ユーザーが選択したコースに対して `DetailsView` コントロールを使用します。 *講師*の `</div>` タグの後に、次のマークアップを追加します (このマークアップは、終了 div タグの**後**に配置してください)。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

このマークアップは、`Courses` エンティティセットにバインドされている `EntityDataSource` コントロールを作成します。 `Where` プロパティは、コース `GridView` コントロールで選択された行の `CourseID` 値を使用してコースを選択します。 マークアップは `Selected` イベントのハンドラーを指定します。これは、階層内の別のレベルである学生の成績を表示するために後で使用します。

*Instructors.aspx.cs*で、`CourseDetailsEntityDataSource_Selected` メソッドに対して次のスタブを作成します。 (このスタブは、このチュートリアルで後ほど説明します。ここでは、ページをコンパイルして実行するために必要になります)。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

ページを実行します。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

コースが選択されていないため、最初はコースの詳細はありません。 コースが割り当てられているインストラクターを選択し、コースを選択して詳細を表示します。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>EntityDataSource "Selected" イベントを使用して関連データを表示する

最後に、選択したコースのすべての登録済み学生とその成績を表示します。 これを行うには、コース `DetailsView`にバインドされている `EntityDataSource` コントロールの `Selected` イベントを使用します。

*講師*の `DetailsView` コントロールの後に、次のマークアップを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

このマークアップは、選択したコースの学生とその成績のリストを表示する `ListView` コントロールを作成します。 コントロールをコードにバインドするため、データソースは指定されません。 `EmptyDataTemplate` 要素は、コースが選択されていないときに表示するメッセージを提供します。この場合、表示する学生は存在しません。 `LayoutTemplate` 要素は、リストを表示するための HTML テーブルを作成し、`ItemTemplate` は表示する列を指定します。 学生 ID と学生の成績は `StudentGrade` エンティティからのもので、学生名は、Entity Framework が `StudentGrade` エンティティの `Person` ナビゲーションプロパティで使用できる `Person` エンティティからのものです。

*Instructors.aspx.cs*で、スタブアウト `CourseDetailsEntityDataSource_Selected` メソッドを次のコードに置き換えます。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

このイベントのイベント引数は、選択されたデータをコレクションの形式で提供します。これは、何も選択されていない場合、または `Course` エンティティが選択されている場合に1つの項目がある場合に、項目が0になります。 `Course` エンティティが選択されている場合、コードは、`First` メソッドを使用してコレクションを単一のオブジェクトに変換します。 次に、ナビゲーションプロパティから `StudentGrade` エンティティを取得し、コレクションに変換して、`GradesListView` コントロールをコレクションにバインドします。

これで成績を表示できますが、最初にページが表示されたときと、コースが選択されていないときに、空のデータテンプレート内のメッセージが表示されるようにする必要があります。 これを行うには、次の2つの場所から呼び出すメソッドを作成します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

ページを初めて表示するときに空のデータテンプレートを表示するには、`Page_Load` メソッドからこの新しいメソッドを呼び出します。 また、インストラクターが選択されたときにそのイベントが発生するので、`InstructorsGridView_SelectedIndexChanged` メソッドから呼び出します。これは、新しいコースがコース `GridView` コントロールに読み込まれ、何も選択されていないことを意味します。 2つの呼び出しを次に示します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

ページを実行します。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

コースが割り当てられているインストラクターを選択し、コースを選択します。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

これで、関連データを操作するいくつかの方法が見られました。 次のチュートリアルでは、既存のエンティティ間のリレーションシップを追加する方法、リレーションシップを削除する方法、既存のエンティティとのリレーションシップを持つ新しいエンティティを追加する方法について説明します。

> [!div class="step-by-step"]
> [前へ](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-5.md)
