---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 7 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78488524"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート7

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="using-stored-procedures"></a>ストアド プロシージャの使用

前のチュートリアルでは、階層ごとのテーブル継承パターンを実装しています。 このチュートリアルでは、ストアドプロシージャを使用してデータベースアクセスをより細かく制御する方法について説明します。

Entity Framework では、データベースアクセスにストアドプロシージャを使用するように指定できます。 任意のエンティティ型について、その型のエンティティを作成、更新、または削除するために使用するストアドプロシージャを指定できます。 次に、データモデルで、エンティティのセットの取得などのタスクを実行するために使用できるストアドプロシージャへの参照を追加できます。

ストアドプロシージャの使用は、データベースアクセスの一般的な要件です。 場合によっては、データベース管理者は、セキュリティ上の理由により、すべてのデータベースアクセスでストアドプロシージャを通過することが必要になる場合があります。 場合によっては、Entity Framework がデータベースを更新するときに使用するプロセスの一部にビジネスロジックを組み込むこともできます。 たとえば、エンティティが削除されるたびに、そのエンティティをアーカイブデータベースにコピーすることができます。 または、行が更新されるたびに、変更を行ったユーザーを記録する行をログテーブルに書き込むことができます。 これらのタスクは、Entity Framework がエンティティを削除するかエンティティを更新するたびに呼び出されるストアドプロシージャで実行できます。

前のチュートリアルと同様に、新しいページは作成されません。 代わりに、既に作成した一部のページに対して Entity Framework がデータベースにアクセスする方法を変更します。

このチュートリアルでは、`Student` と `Instructor` エンティティを挿入するためのストアドプロシージャをデータベースに作成します。 これらのデータモデルをデータモデルに追加し、データベースに `Student` および `Instructor` エンティティを追加するために Entity Framework でそれらを使用するように指定します。 また、`Course` エンティティを取得するために使用できるストアドプロシージャも作成します。

## <a name="creating-stored-procedures-in-the-database"></a>データベースでのストアドプロシージャの作成

(このチュートリアルでダウンロード可能なプロジェクトの*School .mdf*ファイルを使用している場合は、ストアドプロシージャが既に存在しているため、このセクションをスキップできます)。

**サーバーエクスプローラー**で、[ *School .mdf*] を展開し、 **[ストアドプロシージャ]** を右クリックして、 **[新しいストアドプロシージャの追加]** を選択します。

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

次の SQL ステートメントをコピーし、[ストアドプロシージャ] ウィンドウに貼り付けて、スケルトンストアドプロシージャを置き換えます。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` エンティティには、`PersonID`、`LastName`、`FirstName`、および `EnrollmentDate`の4つのプロパティがあります。 データベースは ID 値を自動的に生成し、ストアドプロシージャは他の3つのパラメーターを受け取ります。 このストアドプロシージャは、新しい行のレコードキーの値を返します。これにより、Entity Framework は、メモリ内に保持されているエンティティのバージョンで追跡できるようになります。

ストアドプロシージャウィンドウを保存して閉じます。

次の SQL ステートメントを使用して、同じ方法で `InsertInstructor` ストアドプロシージャを作成します。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

`Student` エンティティと `Instructor` エンティティの `Update` ストアドプロシージャも作成します。 (データベースには、`Instructor` と `Student` の両方のエンティティに対して機能する `DeletePerson` ストアドプロシージャが既に存在します。)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

このチュートリアルでは、各エンティティ型に対して、挿入、更新、および削除の3つのすべての関数をマップします。 Entity Framework version 4 では、これらの関数のうち1つまたは2つだけをストアドプロシージャにマップすることができます。ただし、次の例外があります。 update 関数をマップしても delete 関数をマップしない場合、Entity Framework は例外をスローします。エンティティを削除しようとしています。 Entity Framework バージョン3.5 では、ストアドプロシージャのマッピングがこれほど柔軟性がありませんでした。1つの関数をマップした場合は、3つすべてをマップする必要がありました。

更新データではなく読み取りを行うストアドプロシージャを作成するには、次の SQL ステートメントを使用して、すべての `Course` エンティティを選択するストアドプロシージャを作成します。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>ストアドプロシージャをデータモデルに追加する

これで、ストアドプロシージャがデータベースに定義されましたが、Entity Framework で使用できるようにするには、それらをデータモデルに追加する必要があります。 *SchoolModel*を開き、デザイン画面を右クリックして、 **[データベースからモデルを更新]** を選択します。 **[データベースオブジェクトの選択]** ダイアログボックスの **[追加]** タブで、 **[ストアドプロシージャ]** を展開し、新しく作成したストアドプロシージャと `DeletePerson` ストアドプロシージャを選択して、 **[完了]** をクリックします。

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>ストアドプロシージャのマッピング

データモデルデザイナーで、`Student` エンティティを右クリックし、 **[ストアドプロシージャマッピング]** を選択します。

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

**[マッピングの詳細]** ウィンドウが表示されます。このウィンドウでは、Entity Framework がこの種類のエンティティの挿入、更新、および削除に使用するストアドプロシージャを指定できます。

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

**挿入**関数を**insertstudent**に設定します。 このウィンドウには、ストアドプロシージャのパラメーターの一覧が表示されます。各パラメーターは、エンティティプロパティにマップされている必要があります。 これらの2つは、名前が同じであるため、自動的にマップされます。 `FirstName`という名前のエンティティプロパティはないため、使用可能なエンティティプロパティを示すドロップダウンリストから `FirstMidName` を手動で選択する必要があります。 (これは、最初のチュートリアルで `FirstName` プロパティの名前を `FirstMidName` に変更したためです)。

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

同じ **[マッピングの詳細]** ウィンドウで、`Update` 関数を `UpdateStudent` ストアドプロシージャにマップします (`Insert` ストアドプロシージャの場合と同様に、`FirstName`のパラメーター値として `FirstMidName` を指定していることを確認してください)。 `Delete` は `DeletePerson` ストアドプロシージャに対して関数を指定します。

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

同じ手順に従って、インストラクターの挿入、更新、および削除のストアドプロシージャを `Instructor` エンティティにマップします。

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

データを更新するのではなく、読み取りを行うストアドプロシージャの場合は、 **[モデルブラウザー]** ウィンドウを使用して、ストアドプロシージャを返すエンティティ型にマップします。 データモデルデザイナーでデザイン画面を右クリックし、 **[モデルブラウザー]** を選択します。 **SchoolModel**ノードを開き、 **[ストアドプロシージャ]** ノードを開きます。 次に `GetCourses` ストアドプロシージャを右クリックし、 **[関数インポートの追加]** を選択します。

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

**[関数インポートの追加]** ダイアログボックスの [選択した**エンティティ** **のコレクションを返す**] をクリックし、返されるエンティティ型として [`Course`] を選択します。 完了したら **[OK]** をクリックします。 *.Edmx*ファイルを保存して閉じます。

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>Insert、Update、Delete の各ストアドプロシージャの使用

データを挿入、更新、および削除するストアドプロシージャは、データモデルに追加して適切なエンティティにマップした後に、Entity Framework によって自動的に使用されます。 StudentsAdd ページを実行できるようになりました *。* 新しい Entity Framework 学生を作成するたびに、`InsertStudent` ストアドプロシージャを使用して `Student` テーブルに新しい行が追加されます。

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

*Student ページを*実行すると、新しい学生が一覧に表示されます。

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

名前を変更して update 関数が動作することを確認し、学生を削除して delete 関数が動作することを確認します。

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>Select ストアドプロシージャの使用

Entity Framework では、`GetCourses`などのストアドプロシージャは自動的には実行されず、`EntityDataSource` コントロールでは使用できません。 これらを使用するには、コードから呼び出します。

*InstructorsCourses.aspx.cs*ファイルを開きます。 `PopulateDropDownLists` メソッドは、LINQ to entities クエリを使用してすべての course エンティティを取得します。これにより、リストをループ処理し、インストラクターが割り当てられているものと割り当て解除されているエンティティを特定できます。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

これを次のコードに置き換えます。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

このページでは、`GetCourses` ストアドプロシージャを使用して、すべてのコースの一覧を取得します。 ページを実行して、以前と同じように動作することを確認します。

(ストアドプロシージャによって取得されたエンティティのナビゲーションプロパティは、`ObjectContext` の既定の設定によっては、それらのエンティティに関連するデータが自動的に設定されない場合があります。 詳細については、MSDN ライブラリの「[関連オブジェクトの読み込み](https://msdn.microsoft.com/library/bb896272.aspx)」を参照してください。)

次のチュートリアルでは、動的データ機能を使用して、データの書式設定と検証規則を簡単にプログラミングおよびテストできるようにする方法について説明します。 データ書式指定文字列などの各 web ページの規則に対してを指定する代わりに、フィールドが必要であるかどうかを指定する代わりに、データモデルのメタデータにこのような規則を指定して、すべてのページに自動的に適用されます。

> [!div class="step-by-step"]
> [前へ](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-8.md)
