---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 5 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423868"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート5

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="working-with-related-data-continued"></a>関連データの操作 (続き)

前のチュートリアルでは、`EntityDataSource` コントロールを使用して関連データを操作しました。 複数レベルの階層と、ナビゲーションプロパティで編集されたデータを表示しています。 このチュートリアルでは、リレーションシップを追加および削除し、既存のエンティティとのリレーションシップを持つ新しいエンティティを追加することによって、関連データの操作を続行します。

部門に割り当てられているコースを追加するページを作成します。 部門は既に存在しています。新しいコースを作成するときは、その部門と既存の部門との間にリレーションシップを確立します。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

また、インストラクターを講座に割り当て (選択した2つのエンティティ間にリレーションシップを追加する)、またはコースからインストラクターを削除する (2 つのエンティティ間のリレーションシップを削除する) ことによって、多対多リレーションシップで動作するページを作成します ([] を選択します)。 データベースでは、インストラクターとコースの間にリレーションシップを追加すると、`CourseInstructor` association テーブルに新しい行が追加されます。リレーションシップを削除するには、`CourseInstructor` アソシエーションテーブルから行を削除する必要があります。 ただし、Entity Framework では、`CourseInstructor` テーブルを明示的に参照せずにナビゲーションプロパティを設定することによって、この操作を行います。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>既存のエンティティへのリレーションシップを持つエンティティの追加

*CoursesAdd*という名前の新しい web ページを作成し、*そのマスターページ*を使用して、`Content2`という名前の `Content` コントロールに次のマークアップを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

このマークアップは、挿入を可能にし、`Inserting` イベントのハンドラーを指定する、コースを選択する `EntityDataSource` コントロールを作成します。 新しい `Course` エンティティが作成されたときに、`Department` ナビゲーションプロパティを更新するには、ハンドラーを使用します。

また、マークアップによって、新しい `Course` エンティティを追加するために使用する `DetailsView` コントロールも作成されます。 マークアップでは、`Course` エンティティのプロパティにバインドされたフィールドを使用します。 システムによって生成された ID フィールドではないため、`CourseID` 値を入力する必要があります。 もちろん、コースの作成時に手動で指定する必要があるコース番号です。

ナビゲーションプロパティは `BoundField` コントロールでは使用できないため、`Department` ナビゲーションプロパティのテンプレートフィールドを使用します。 [テンプレート] フィールドには、部門を選択するドロップダウンリストが表示されます。 ドロップダウンリストは `Bind`ではなく `Eval` を使用して `Departments` エンティティセットにバインドされます。これは、ナビゲーションプロパティを更新するために直接バインドすることができないためです。 `DepartmentID` 外部キーを更新するコードで使用するために、コントロールへの参照を格納できるように、`DropDownList` コントロールの `Init` イベントのハンドラーを指定します。

部分クラス宣言の直後に*CoursesAdd.aspx.cs*で、`DepartmentsDropDownList` コントロールへの参照を保持するクラスフィールドを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

コントロールへの参照を格納できるように、`DepartmentsDropDownList` コントロールの `Init` イベントのハンドラーを追加します。 これにより、ユーザーが入力した値を取得し、それを使用して `Course` エンティティの `DepartmentID` 値を更新できます。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

`DetailsView` コントロールの `Inserting` イベントのハンドラーを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

ユーザーが [`Insert`] をクリックすると、新しいレコードが挿入される前に `Inserting` イベントが発生します。 ハンドラー内のコードは、`DropDownList` コントロールから `DepartmentID` を取得し、それを使用して `Course` エンティティの `DepartmentID` プロパティに使用される値を設定します。

Entity Framework は、関連付けられている `Department` エンティティの `Courses` ナビゲーションプロパティにこのコースを追加する処理を行います。 また、`Course` エンティティの `Department` ナビゲーションプロパティに department を追加します。

ページを実行します。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

ID、タイトル、クレジットの数を入力し、部門を選択して、 **[挿入]** をクリックします。

[Course *] ページを*実行し、同じ部門を選択して新しいコースを表示します。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>多対多リレーションシップの操作

`Courses` エンティティセットと `People` エンティティセットのリレーションシップは、多対多リレーションシップです。 `Course` エンティティには、`People` という名前のナビゲーションプロパティがあります。このプロパティには、0個以上の関連 `Person` エンティティを含めることができます (そのコースに割り当てられたインストラクターを表す)。 また、`Person` エンティティには `Courses` という名前のナビゲーションプロパティがあります。これには、0個以上の関連 `Course` エンティティ (インストラクターが教えるために割り当てられたコースを表す) を含めることができます。 1人のインストラクターが複数のコースを教えることができ、1つのコースは複数の教師によって講習される可能性があります。 チュートリアルのこのセクションでは、関連エンティティのナビゲーションプロパティを更新して、`Person` エンティティと `Course` エンティティ間のリレーションシップを追加および削除します。

*InstructorsCourses*という名前の新しい web ページを作成し、*そのマスターページ*を使用して、`Content2`という名前の `Content` コントロールに次のマークアップを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

このマークアップは、インストラクターの `Person` エンティティの名前と `PersonID` を取得する `EntityDataSource` コントロールを作成します。 `DropDrownList` コントロールは、`EntityDataSource` コントロールにバインドされます。 `DropDownList` コントロールは、`DataBound` イベントのハンドラーを指定します。 このハンドラーを使用して、コースを表示する2つのドロップダウンリストをバインドします。

マークアップでは、選択したインストラクターにコースを割り当てるために使用する次のコントロールグループも作成されます。

- 割り当てるコースを選択するための `DropDownList` コントロールです。 このコントロールには、選択したインストラクターに現在割り当てられていないコースが設定されます。
- 割り当てを開始する `Button` コントロール。
- 割り当てが失敗した場合にエラーメッセージを表示する `Label` コントロール。

また、マークアップは、選択したインストラクターからコースを削除するために使用するコントロールのグループも作成します。

*InstructorsCourses.aspx.cs*で、using ステートメントを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

コースを表示する2つのドロップダウンリストを設定するためのメソッドを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

このコードでは、`Courses` エンティティセットからすべてのコースを取得し、選択したインストラクターの `Person` エンティティの `Courses` ナビゲーションプロパティからコースを取得します。 次に、そのインストラクターに割り当てられているコースを特定し、それに応じてドロップダウンリストを設定します。

`Assign` ボタンの `Click` イベントのハンドラーを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

このコードは、選択したインストラクターの `Person` エンティティを取得し、選択したコースの `Course` エンティティを取得し、選択したコースをインストラクターの `Person` エンティティの `Courses` ナビゲーションプロパティに追加します。 次に、変更内容をデータベースに保存し、ドロップダウンリストを再設定して、結果をすぐに表示できるようにします。

`Remove` ボタンの `Click` イベントのハンドラーを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

このコードは、選択したインストラクターの `Person` エンティティを取得し、選択したコースの `Course` エンティティを取得し、`Person` エンティティの `Courses` ナビゲーションプロパティから選択したコースを削除します。 次に、変更内容をデータベースに保存し、ドロップダウンリストを再設定して、結果をすぐに表示できるようにします。

報告するエラーがないときにエラーメッセージが表示されないようにするコードを `Page_Load` メソッドに追加し、[講師] ドロップダウンリストの `DataBound` イベントと `SelectedIndexChanged` イベントのハンドラーを追加して、コースのドロップダウンリストを設定します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

ページを実行します。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

インストラクターを選択します。 [<strong>コースの割り当て</strong>] ドロップダウンリストには、インストラクターが学習していないコースが表示され、[<strong>コースの削除</strong>] ドロップダウンリストには、インストラクターが既に割り当てられているコースが表示されます。 [<strong>コースの割り当て</strong>] セクションでコースを選択し、[<strong>割り当て</strong>] をクリックします。 コースは [コースの<strong>削除</strong>] ドロップダウンリストに移動します。 [<strong>コースの削除</strong>] セクションでコースを選択し、[<strong>削除</strong>] をクリックし<em>ます。</em> コースが [コースの<strong>割り当て</strong>] ドロップダウンリストに移動します。

これで、関連データを操作するいくつかの方法が見られました。 次のチュートリアルでは、データモデルで継承を使用して、アプリケーションの保守性を向上させる方法について説明します。

> [!div class="step-by-step"]
> [前へ](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-6.md)
