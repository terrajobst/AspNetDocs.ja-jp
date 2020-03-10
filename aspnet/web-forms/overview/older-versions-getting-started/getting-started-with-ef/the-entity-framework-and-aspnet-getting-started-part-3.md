---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 3 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522640"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート3

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="filtering-ordering-and-grouping-data"></a>データのフィルター処理、並べ替え、およびグループ化

前のチュートリアルでは、`EntityDataSource` コントロールを使用してデータを表示および編集しています。 このチュートリアルでは、データのフィルター処理、並べ替え、およびグループ化を行います。 `EntityDataSource` コントロールのプロパティを設定してこの操作を行う場合、構文は他のデータソースコントロールとは異なります。 ただし、ここで説明するように、`QueryExtender` コントロールを使用して、これらの違いを最小限に抑えることができます。

*Students ページを*変更して、学生をフィルター処理し、名前で並べ替え、名前を検索します。 また *、[course] ページ*を変更して、選択した学科のコースを表示し、名前でコースを検索します。 最後に、student の統計情報を*About .aspx*ページに追加します。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>EntityDataSource "Where" プロパティを使用してデータをフィルター処理する

前のチュートリアルで作成した*student .aspx*ページを開きます。 現在構成されているように、ページの `GridView` コントロールには、`People` エンティティセットのすべての名前が表示されます。 ただし、学生だけを表示したい場合は、null 以外の登録日がある `Person` エンティティを選択します。

**デザイン**ビューに切り替え、[`EntityDataSource`] コントロールを選択します。 **[プロパティ]** ウィンドウで、 `Where` プロパティを `it.EnrollmentDate is not null`に設定します。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

`EntityDataSource` コントロールの `Where` プロパティで使用する構文は Entity SQL です。 Entity SQL は Transact-sql に似ていますが、データベースオブジェクトではなくエンティティで使用するようにカスタマイズされています。 `it.EnrollmentDate is not null`式では、`it` は、クエリによって返されたエンティティへの参照を表します。 したがって、`it.EnrollmentDate` は、`EntityDataSource` コントロールが返す `Person` エンティティの `EnrollmentDate` プロパティを参照します。

ページを実行します。 学生リストに学生のみが含まれるようになりました。 (登録日がない場所に表示される行はありません)。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>EntityDataSource "OrderBy" プロパティを使用してデータを並べ替える

また、この一覧が最初に表示されたときに名前の順序で表示されるようにします。 **[デザイン]** ビューで*student*ページを開いたまま、`EntityDataSource` コントロールを選択した状態で、 **[プロパティ]** ウィンドウで**OrderBy**プロパティを `it.LastName`に設定します。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

ページを実行します。 学生リストは、姓の順に並べられています。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>コントロールパラメーターを使用して "Where" プロパティを設定する

他のデータソースコントロールと同様に、パラメーター値を `Where` プロパティに渡すことができます。 チュートリアルのパート2で作成した [course *] ページで*、この方法を使用して、ユーザーがドロップダウンリストから選択した学科に関連付けられているコースを表示できます。

Course*を開き、[* **デザイン**] ビューに切り替えます。 2つ目の `EntityDataSource` コントロールをページに追加し、`CoursesEntityDataSource`という名前を指定します。 それを `SchoolEntities` モデルに接続し、[`Courses`] を**EntitySetName**値として選択します。

**[プロパティ]** ウィンドウで、 **[Where]** プロパティボックスの省略記号をクリックします。 ( **[プロパティ]** ウィンドウを使用する前に、`CoursesEntityDataSource` コントロールが選択されていることを確認してください)。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

**[式エディター]** ダイアログボックスが表示されます。 このダイアログボックスで、 **[指定されたパラメーターに基づいて Where 式を自動的に生成する]** を選択し、 **[パラメーターの追加]** をクリックします。 パラメーターに `DepartmentID`という名前を付け、 **[ソース]** の値として **[コントロール]** を選択し、 **ControlID**値として **[DepartmentsDropDownList]** を選択します。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

**[詳細プロパティの表示]** をクリックし、 **[式エディター]** ダイアログボックスの **[プロパティ]** ウィンドウで、[`Type`] プロパティを `Int32`に変更します。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

完了したら **[OK]** をクリックします。

ドロップダウンリストの下で、ページに `GridView` コントロールを追加し、`CoursesGridView`という名前を指定します。 `CoursesEntityDataSource` データソースコントロールに接続し、 **[スキーマの更新]** をクリックし、 **[列の編集]** をクリックして、`DepartmentID` 列を削除します。 `GridView` コントロールのマークアップは、次の例のようになります。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

ユーザーがドロップダウンリストで選択した部署を変更すると、関連するコースの一覧が自動的に変更されます。 これを行うには、ドロップダウンリストを選択し、 **[プロパティ]** ウィンドウの [`AutoPostBack`] プロパティを `True`に設定します。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

デザイナーの使用が終了したので、**ソース**ビューに切り替えて、`CoursesEntityDataSource` コントロールの `ConnectionString` と `DefaultContainer` name プロパティを `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 属性に置き換えます。 完了すると、コントロールのマークアップは次の例のようになります。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

ページを実行し、ドロップダウンリストを使用して異なる部門を選択します。 選択した部門によって提供されるコースのみが、`GridView` コントロールに表示されます。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>EntityDataSource "GroupBy" プロパティを使用してデータをグループ化する

Contoso 大学が [About] ページに生徒の本文の統計をいくつか配置したいとします。 具体的には、学生の数の内訳を、登録した日付で表示したいと考えています。

*About .aspx*を開き、**ソース**ビューで、`BodyContent` コントロールの既存の内容を、`h2` タグの "Student Body Statistics" に置き換えます。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

見出しの後に `EntityDataSource` コントロールを追加し、`StudentStatisticsEntityDataSource`という名前を指定します。 `SchoolEntities`に接続し、`People` エンティティセットを選択して、ウィザードの **[選択**] ボックスを変更せずにそのままにします。 **[プロパティ]** ウィンドウで、次のプロパティを設定します。

- 学生のみをフィルター処理するには、[`Where`] プロパティを [`it.EnrollmentDate is not null`] に設定します。
- 登録日に結果をグループ化するには、`GroupBy` プロパティを `it.EnrollmentDate`に設定します。
- 学生の登録日と数を選択するには、`Select` プロパティを `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`に設定します。
- 登録日によって結果を並べ替えるには、`OrderBy` プロパティを `it.EnrollmentDate`に設定します。

**ソース**ビューで、`ConnectionString` と `DefaultContainer` name プロパティを `ContextTypeName` プロパティに置き換えます。 `EntityDataSource` コントロールのマークアップは、次の例のようになります。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

`Select`、`GroupBy`、および `Where` プロパティの構文は、現在のエンティティを指定する `it` キーワードを除き、Transact-sql に似ています。

次のマークアップを追加して、データを表示する `GridView` コントロールを作成します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

ページを実行して、登録日別に生徒の数を示す一覧を表示します。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>フィルター処理と順序付けに QueryExtender コントロールを使用する

`QueryExtender` コントロールは、マークアップでフィルター処理と並べ替えを指定する方法を提供します。 構文は、使用しているデータベース管理システム (DBMS) に依存しません。 また、一般に Entity Framework に依存しません。ただし、ナビゲーションプロパティに使用する構文は、Entity Framework に固有です。

チュートリアルのこの部分では、`QueryExtender` コントロールを使用してデータのフィルター処理と並べ替えを行います。また、いずれかの並べ替えフィールドがナビゲーションプロパティになります。

(マークアップではなくコードを使用して、`EntityDataSource` コントロールによって自動的に生成されるクエリを拡張する場合は、`QueryCreated` イベントを処理することによってこれを行うことができます。 これは、`QueryExtender` コントロールが `EntityDataSource` コントロールクエリも拡張する方法です)。

*[Course] ページを*開き、前の手順で追加したマークアップの下に、次のマークアップを挿入して、見出し、検索文字列を入力するためのテキストボックス、検索ボタン、および `Courses` エンティティセットにバインドされている `EntityDataSource` コントロールを作成します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

`EntityDataSource` コントロールの `Include` プロパティが `Department`に設定されていることに注意してください。 データベースでは、`Course` テーブルに部門名が含まれていません。これには、`DepartmentID` の外部キー列が含まれています。 データベースに対して直接クエリを実行した場合は、学科名をコースデータと共に取得するために、`Course` テーブルと `Department` テーブルを結合する必要があります。 `Include` プロパティを `Department`に設定することにより、Entity Framework が `Course` エンティティを取得するときに関連する `Department` エンティティを取得する処理を行う必要があることを指定します。 `Department` エンティティは、`Course` エンティティの `Department` ナビゲーションプロパティに格納されます。 (既定では、データモデルデザイナーによって生成された `SchoolEntities` クラスは、必要に応じて関連データを取得します。また、データソースコントロールをそのクラスにバインドしているので、`Include` プロパティを設定する必要はありません。 ただし、これを設定すると、ページのパフォーマンスが向上します。それ以外の場合、Entity Framework は、`Course` エンティティおよび関連する `Department` エンティティのデータを取得するためにデータベースを個別に呼び出します。

`EntityDataSource` コントロールを作成した後、次のマークアップを挿入して、その `EntityDataSource` コントロールにバインドされている `QueryExtender` コントロールを作成します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` 要素は、テキストボックスに入力された値にタイトルが一致するコースを選択するように指定します。 `SearchType` プロパティでは `StartsWith`が指定されているため、テキストボックスに入力した文字数だけが比較されます。

`OrderByExpression` 要素は、結果セットが学科名内のコースタイトルで並べ替えられることを指定します。 部署名が指定されていることに注意してください: `Department.Name`。 `Course` エンティティと `Department` エンティティ間のアソシエーションは一対一であるため、`Department` ナビゲーションプロパティには `Department` エンティティが含まれます。 (これが一対多のリレーションシップである場合、プロパティにはコレクションが含まれます)。部署名を取得するには、`Department` エンティティの `Name` プロパティを指定する必要があります。

最後に、`GridView` コントロールを追加してコースの一覧を表示します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

最初の列は、部署名を表示するテンプレートフィールドです。 Databinding 式は、`QueryExtender` コントロールの場合と同様に `Department.Name`を指定します。

ページを実行します。 最初の表示では、すべてのコースの一覧が部署別、そしてコースタイトル別に表示されます。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

"M" を入力し、 **[検索]** をクリックすると、タイトルが "m" で始まるすべてのコースが表示されます (検索では大文字と小文字が区別されません)。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>"Like" 演算子を使用したデータのフィルター処理

`Like` コントロールの `EntityDataSource` プロパティで `Where` 演算子を使用することにより、`QueryExtender` コントロールの `StartsWith`、`Contains`、および `EndsWith` 検索の種類と同様の効果を得ることができます。 チュートリアルのこの部分では、`Like` 演算子を使用して、名前で学生を検索する方法について説明します。

**ソース**ビューで*student を*開きます。 `GridView` コントロールの後に、次のマークアップを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

このマークアップは、前に示したものと似ていますが、`Where` のプロパティ値は除きます。 `Where` 式の2番目の部分では、テキストボックスに入力されたものの姓と名の両方を検索する部分文字列検索 (`LIKE %FirstMidName% or LIKE %LastName%`) を定義します。

ページを実行します。 `StudentName` パラメーターの既定値は "%" であるため、最初はすべての学生が表示されます。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

テキストボックスに「g」という文字を入力し、 **[検索]** をクリックします。 姓または名のいずれかに "g" を持つ学生の一覧が表示されます。

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

個々のテーブルのデータの表示、更新、フィルター処理、並べ替え、およびグループ化が完了しました。 次のチュートリアルでは、関連データ (マスター詳細シナリオ) の操作を開始します。

> [!div class="step-by-step"]
> [前へ](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-4.md)
