---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Entity Framework 4.0 と ObjectDataSource コントロールの使用、パート 3: 並べ替えとフィルター |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework 4.0 チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512716"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>Entity Framework 4.0 と ObjectDataSource コントロールの使用、パート 3: 並べ替えとフィルター処理

[Tom Dykstra](https://github.com/tdykstra)

> このチュートリアルシリーズは、 [Entity Framework 4.0 チュートリアルシリーズを使用](https://asp.net/entity-framework/tutorials#Getting%20Started)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。 チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。 チュートリアルについてご質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)に投稿することができます。

前のチュートリアルでは、Entity Framework と `ObjectDataSource` コントロールを使用する n 層 web アプリケーションにリポジトリパターンを実装しました。 このチュートリアルでは、並べ替えとフィルター処理を行い、マスタ詳細シナリオを処理する方法について説明します。 次の拡張機能を department *.aspx*ページに追加します。

- ユーザーが名前で部門を選択できるようにするテキストボックス。
- グリッドに表示される各部署のコースの一覧。
- 列見出しをクリックして並べ替えることができます。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>GridView 列を並べ替える機能の追加

Department ページ*を開き、`DepartmentsObjectDataSource`* という名前の `ObjectDataSource` コントロールに `SortParameterName="sortExpression"` 属性を追加します。 (後で `sortExpression`という名前のパラメーターを受け取る `GetDepartments` メソッドを作成します)。コントロールの開始タグのマークアップは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

`GridView` コントロールの開始タグに `AllowSorting="true"` 属性を追加します。 コントロールの開始タグのマークアップは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

*Departments.aspx.cs*で、`Page_Load` メソッドから `GridView` コントロールの `Sort` メソッドを呼び出すことによって、既定の並べ替え順序を設定します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

ビジネスロジッククラスまたはリポジトリクラスで並べ替えまたはフィルター処理を行うコードを追加できます。 ビジネスロジッククラスでこれを行う場合は、データがデータベースから取得された後に並べ替えまたはフィルター処理が行われます。これは、ビジネスロジッククラスがリポジトリによって返された `IEnumerable` オブジェクトを操作しているためです。 リポジトリクラスに並べ替えとフィルター処理のコードを追加し、LINQ 式またはオブジェクトのクエリを `IEnumerable` オブジェクトに変換する前に、この操作を実行すると、コマンドが処理のためにデータベースに渡されます。これは通常、より効率的です。 このチュートリアルでは、データベース (つまり、リポジトリ) によって処理が実行されるように、並べ替えとフィルター処理を実装します。

並べ替え機能を追加するには、リポジトリインターフェイスおよびリポジトリクラスに加えて、ビジネスロジッククラスに新しいメソッドを追加する必要があります。 *ISchoolRepository.cs*ファイルに、返された部門の一覧の並べ替えに使用される `sortExpression` パラメーターを受け取る新しい `GetDepartments` メソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` パラメーターでは、並べ替える列と並べ替えの方向を指定します。

新しいメソッドのコードを*SchoolRepository.cs*ファイルに追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

新しいメソッドを呼び出すように、既存のパラメーターなしの `GetDepartments` メソッドを変更します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

テストプロジェクトで、次の新しいメソッドを*MockSchoolRepository.cs*に追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

このメソッドに依存し、並べ替えられたリストを返す単体テストを作成する場合は、リストを返す前に並べ替える必要があります。 このチュートリアルでは、このようなテストを作成するのではなく、並べ替えられていない部署のリストを返すことができます。

*SchoolBL.cs*ファイルで、ビジネスロジッククラスに次の新しいメソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

このコードは、sort パラメーターを repository メソッドに渡します。

Department *. .aspx*ページを実行します。

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

列見出しをクリックすると、その列で並べ替えることができるようになります。 列が既に並べ替えられている場合は、見出しをクリックすると並べ替えの方向が反転します。

## <a name="adding-a-search-box"></a>検索ボックスの追加

このセクションでは、検索テキストボックスを追加し、コントロールパラメーターを使用して `ObjectDataSource` コントロールにリンクします。また、ビジネスロジッククラスにメソッドを追加して、フィルター処理をサポートします。

Department *.aspx*ページを開き、見出しと最初の `ObjectDataSource` コントロールの間に次のマークアップを追加します。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

`DepartmentsObjectDataSource`という名前の `ObjectDataSource` コントロールで、次の操作を行います。

- `SearchTextBox` コントロールに入力された値を取得する `nameSearchString` という名前のパラメーターの `SelectParameters` 要素を追加します。
- `SelectMethod` 属性の値を `GetDepartmentsByName`に変更します。 (後でこのメソッドを作成します)。

`ObjectDataSource` コントロールのマークアップは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

*ISchoolRepository.cs*で、`sortExpression` と `nameSearchString` の両方のパラメーターを受け取る `GetDepartmentsByName` メソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

*SchoolRepository.cs*で、次の新しいメソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

このコードでは、`Where` メソッドを使用して、検索文字列を含む項目を選択します。 検索文字列が空の場合は、すべてのレコードが選択されます。 メソッド呼び出しを、このような1つのステートメント (`Include`、`OrderBy`、`Where`) のように指定する場合、`Where` メソッドは常に最後にある必要があることに注意してください。

新しいメソッドを呼び出すために `sortExpression` パラメーターを受け取る既存の `GetDepartments` メソッドを変更します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

テストプロジェクトの*MockSchoolRepository.cs*に、次の新しいメソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

*SchoolBL.cs*で、次の新しいメソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

Department *.aspx*ページを実行し、検索文字列を入力して、選択ロジックが動作することを確認します。 テキストボックスを空のままにして、すべてのレコードが返されることを確認します。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>各グリッド行の詳細列の追加

次に、グリッドの右側のセルに表示される各部門のすべてのコースを確認します。 これを行うには、入れ子になった `GridView` コントロールを使用し、`Department` エンティティの `Courses` ナビゲーションプロパティからデータにデータをバインドします。

Department *.aspx*を開き、`GridView` コントロールのマークアップで、`RowDataBound` イベントのハンドラーを指定します。 コントロールの開始タグのマークアップは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

`Administrator` テンプレートフィールドの後に新しい `TemplateField` 要素を追加します。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

このマークアップは、コースの一覧のコース番号とタイトルを表示する、入れ子になった `GridView` コントロールを作成します。 `RowDataBound` ハンドラーのコードにデータソースをバインドするので、データソースは指定しません。

*Departments.aspx.cs*を開き、`RowDataBound` イベントの次のハンドラーを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

このコードは、イベント引数から `Department` エンティティを取得し、`Courses` ナビゲーションプロパティを `List` コレクションに変換して、入れ子になった `GridView` をコレクションにバインドします。

*SchoolRepository.cs*ファイルを開き、`GetDepartmentsByName` メソッドで作成したオブジェクトクエリで `Include` メソッドを呼び出して、`Courses` ナビゲーションプロパティの一括読み込みを指定します。 `GetDepartmentsByName` メソッドの `return` ステートメントは、次の例のようになりました。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

ページを実行します。 前に追加した並べ替えとフィルター処理の機能に加えて、GridView コントロールには、各部門の入れ子になったコースの詳細が表示されるようになりました。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

これで、並べ替え、フィルター処理、およびマスタ詳細シナリオの概要が完成します。 次のチュートリアルでは、同時実行を処理する方法について説明します。

> [!div class="step-by-step"]
> [前へ](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [次へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
