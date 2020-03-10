---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC | の Entity Framework で CRUD 機能を実装するMicrosoft Docs'
description: MVC スキャフォールディングによってコントローラーとビューに自動的に作成される作成、読み取り、更新、削除 (CRUD) コードを確認し、カスタマイズします。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471148"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>チュートリアル: ASP.NET MVC での Entity Framework を使用した CRUD 機能の実装

前の[チュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、ENTITY FRAMEWORK (EF) 6 と SQL Server LocalDB を使用してデータを格納および表示する MVC アプリケーションを作成しました。 このチュートリアルでは、MVC スキャフォールディングによってコントローラーとビューに自動的に作成される作成、読み取り、更新、削除 (CRUD) コードを確認し、カスタマイズします。

> [!NOTE]
> コントローラーとデータ アクセス層の間に抽象化レイヤーを作成するためにリポジトリ パターンを実装することは、よく行われることです。 これらのチュートリアルを単純にし、EF 6 自体の使用方法を説明することに重点を置いて、リポジトリは使用しません。 リポジトリを実装する方法の詳細については、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

作成する web ページの例を次に示します。

![学生の詳細ページのスクリーンショット。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![学生作成ページのスクリーンショット。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![学生の削除ページのスクリーンショット。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 詳細ページを作成する
> * [作成] ページを更新する
> * HttpPost Edit メソッドを更新する
> * 削除ページを更新する
> * データベース接続を閉じる
> * トランザクションを処理する

## <a name="prerequisites"></a>前提条件

* [Entity Framework データモデルを作成する](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>詳細ページを作成する

このプロパティにはコレクションが保持されているため、[Students `Index`] ページのスキャフォールディングコードは `Enrollments` プロパティの左側にあります。 [`Details`] ページには、コレクションの内容が HTML テーブルとして表示されます。

*Controllers\StudentController.cs*では、`Details` ビューのアクションメソッドは、 [Find](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx)メソッドを使用して1つの `Student` エンティティを取得します。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

キー値は `id` パラメーターとしてメソッドに渡され、インデックスページの**詳細**ハイパーリンクの*ルートデータ*から取得されます。

### <a name="tip-route-data"></a>ヒント:**ルートデータ**

Route data は、モデルバインダーがルーティングテーブルで指定された URL セグメントで見つかったデータです。 たとえば、既定のルートでは、`controller`、`action`、および `id` セグメントが指定されています。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

次の URL では、既定のルートは、`Instructor` を `controller`としてマップし、`Index` `action` として、1を `id`としてマップします。これらはルートデータ値です。

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021` はクエリ文字列値です。 モデルバインダーは、`id` をクエリ文字列値として渡す場合にも機能します。

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

Url は、Razor ビューの `ActionLink` ステートメントによって作成されます。 次のコードでは、`id` パラメーターが既定のルートと一致するため、`id` がルートデータに追加されます。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

次のコードでは、`courseID` が既定のルートのパラメーターと一致しないため、クエリ文字列として追加されます。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>詳細ページを作成するには

1. *Views\Student\Details.cshtml*を開きます。

   各フィールドは、次の例に示すように、`DisplayFor` ヘルパーを使用して表示されます。

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. `EnrollmentDate` フィールドの後、終了 `</dl>` タグの直前に、次の例に示すように、強調表示されているコードを追加して登録の一覧を表示します。

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    コードを貼り付けた後でコードのインデントが正しくない場合は、 **ctrl**+**K**、 **ctrl**+**D**キーを押して書式設定します。

    このコードは、`Enrollments` ナビゲーション プロパティ内のエンティティをループ処理します。 プロパティ内の `Enrollment` エンティティごとに、コースタイトルとグレードが表示されます。 コースタイトルは、`Enrollments` エンティティの `Course` ナビゲーションプロパティに格納されている `Course` エンティティから取得されます。 必要に応じて、すべてのデータがデータベースから自動的に取得されます。 つまり、ここで遅延読み込みを使用しているとします。 `Courses` ナビゲーションプロパティの*一括読み込み*を指定しなかったので、学生を取得した同じクエリで登録を取得できませんでした。 代わりに、`Enrollments` ナビゲーションプロパティに初めてアクセスしようとすると、データを取得するために新しいクエリがデータベースに送信されます。 遅延読み込みと一括読み込みの詳細については、このシリーズの後の「[関連データの読み取り](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)」チュートリアルを参照してください。

3. 詳細 ページを開くには、プログラム (**Ctrl**+**F5**) を起動し、**Students** タブを選択して、アレクサンドロス Carson の  **details** リンクをクリックします。 (*詳細の cshtml*ファイルが開いている間に**Ctrl**+**F5**キーを押すと、HTTP 400 エラーが表示されます。 これは、Visual Studio が詳細ページを実行しようとしても、表示する学生を指定するリンクに達しなかったためです。 そのような場合は、URL から "Student/Details" を削除してもう一度やり直してください。または、ブラウザーを閉じてプロジェクトを右クリックし、[**ブラウザーで**ビュー > 表示] を**クリックして**ください)。

    選択した学生のコースとグレードの一覧が表示されます。

4. ブラウザーを閉じます。

## <a name="update-the-create-page"></a>[作成] ページを更新する

1. *Controllers\StudentController.cs*で、<xref:System.Web.Mvc.HttpPostAttribute> `Create` アクションメソッドを次のコードに置き換えます。 このコードは `try-catch` ブロックを追加し、スキャフォールディングメソッドの <xref:System.Web.Mvc.BindAttribute> 属性から `ID` を削除します。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    このコードは、ASP.NET MVC モデルバインダーによって作成された `Student` エンティティを `Students` エンティティセットに追加し、変更をデータベースに保存します。 *モデルバインダー*は、フォームによって送信されたデータを簡単に操作できるようにする ASP.NET MVC の機能を参照します。モデルバインダーは、ポストされたフォーム値を CLR 型に変換し、パラメーターのアクションメソッドに渡します。 この場合、モデルバインダーは、`Form` コレクションのプロパティ値を使用して、`Student` エンティティをインスタンス化します。

    バインド属性から `ID` を削除したのは、行が挿入されたときに SQL Server が自動的に設定する主キー値 `ID` であるためです。 ユーザーからの入力に `ID` 値が設定されていません。

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgery-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>セキュリティ警告-`ValidateAntiForgeryToken` 属性は、[クロスサイト要求偽造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻撃を防止するのに役立ちます。 ビューには、対応する `Html.AntiForgeryToken()` ステートメントが必要です。これについては後で説明します。

    `Bind` 属性は、作成シナリオで*過剰な投稿*から保護するための1つの方法です。 たとえば、`Student` エンティティに、この web ページを設定したくない `Secret` のプロパティが含まれているとします。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    Web ページに `Secret` フィールドがない場合でも、ハッカーは[fiddler](http://fiddler2.com/home)などのツールを使用するか、一部の JavaScript を記述して `Secret` フォーム値をポストすることができます。 モデルバインダーが `Student` インスタンスを作成するときに使用するフィールドを制限する <xref:System.Web.Mvc.BindAttribute> 属性がない場合<em>、</em>モデルバインダーは、その `Secret` フォーム値を取得し、それを使用して `Student` エンティティインスタンスを作成します。 その場合、`Secret` フォーム フィールドに対してハッカーが指定した値はすべて、データベースで更新されます。 次の図は、ポストされたフォーム値に `Secret` フィールド (値 "OverPost") を追加する fiddler ツールを示しています。

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    値 "OverPost" は挿入される行の `Secret` プロパティに正常に追加されますが、Web ページがそのプロパティを設定できることは意図したものではありません。

    `Include` パラメーターと `Bind` 属性を使用して、フィールドを*ホワイトリスト*に登録することをお勧めします。 `Exclude` パラメーターを使用して、除外するフィールドを*ブラック*リストに追加することもできます。 `Include` のセキュリティが強化されているのは、新しいプロパティをエンティティに追加したときに、新しいフィールドが `Exclude` の一覧によって自動的に保護されないことです。

    編集シナリオでの過剰な投稿を防ぐには、まずデータベースからエンティティを読み取り、次に `TryUpdateModel`を呼び出して、明示的に許可されているプロパティリストを渡します。 これは、これらのチュートリアルで使用されている方法です。

    多くの開発者にとって優先される過剰なポスティングを防ぐ別の方法として、モデルバインドを持つエンティティクラスではなく、ビューモデルを使用する方法があります。 更新するプロパティのみをビュー モデルに含めます。 MVC モデルバインダーが終了したら、必要に応じて[Automapper](http://automapper.org/)などのツールを使用して、ビューモデルのプロパティをエンティティインスタンスにコピーします。 Db を使用します。エンティティインスタンスのエントリを変更して状態を Unchanged に設定し、プロパティ ("PropertyName") を設定します。IsModified は、ビューモデルに含まれる各エンティティプロパティで true に変更されます。 この方法は、編集シナリオと作成シナリオの両方で利用できます。

    `Bind` 属性以外は、スキャフォールディングコードに対して行った変更は `try-catch` ブロックだけです。 変更を保存するときに、<xref:System.Data.DataException> から派生した例外がキャッチされた場合は、汎用的なエラー メッセージが表示されます。 <xref:System.Data.DataException> 例外は、プログラミング エラーではなくアプリケーション外の何かが原因で発生する場合があるので、再試行することをお勧めします。 このサンプルでは実装されていませんが、運用品質のアプリケーションでは例外をログに記録します。 詳細については、「**Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)** 」(監視とテレメトリ (Azure での実際のクラウド アプリの構築)) の「[Log for insight](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)」(洞察のためのログ) セクションをご覧ください。

    Views\Student\Create.cshtml のコードは、「 」で*説明*したものと似ていますが、`DisplayFor`ではなく、各フィールドに対して `EditorFor` および `ValidationMessageFor` ヘルパーが使用されている点が異なります。 関連するコードを次に示します。

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    また、`@Html.AntiForgeryToken()`も含まれています *。* これは、[クロスサイト要求偽造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻撃を防ぐために、コントローラーの `ValidateAntiForgeryToken` 属性と連携します。

    *Create. cshtml*に変更は必要ありません。

2. プログラムを起動し、 **[Students]** タブを選択し、 **[Create New]** をクリックして、ページを実行します。

3. 名前と無効な日付を入力し、 **[作成]** をクリックしてエラーメッセージを表示します。

    これは、既定で取得するサーバー側の検証です。 後のチュートリアルでは、クライアント側の検証用のコードを生成する属性を追加する方法について説明します。 次の強調表示されたコードは、 **Create**メソッドでのモデル検証チェックを示しています。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. 日付を有効な値に変更し、 **[Create]** をクリックして、新しい学生が **[Index]** ページに表示されることを確認します。

5. ブラウザーを閉じます。

## <a name="update-httppost-edit-method"></a>HttpPost Edit メソッドの更新

1. <xref:System.Web.Mvc.HttpPostAttribute> `Edit` アクションメソッドを次のコードに置き換えます。

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > *Controllers\StudentController.cs*では、`HttpGet Edit` メソッド (`HttpPost` 属性のないメソッド) は、`Find` メソッドを使用して、選択された `Student` エンティティを取得します。これは、`Details` メソッドで見たとおりです。 このメソッドを変更する必要はありません。

   これらの変更は、[過剰なポスティング](#overpost)を防ぐためにセキュリティのベストプラクティスを実装します。 scaffolder は、`Bind` 属性を生成し、モデルバインダーによって作成されたエンティティを、変更されたフラグを使用してエンティティセットに追加します。 このコードは、`Include` パラメーターに一覧表示されていないフィールド内の既存のデータを `Bind` 属性によってクリアするため、推奨されなくなりました。 今後、MVC コントローラー scaffolder は、Edit メソッドの `Bind` 属性を生成しないように更新されます。

   新しいコードは、既存のエンティティを読み取り、<xref:System.Web.Mvc.Controller.TryUpdateModel%2A> を呼び出して、ポストされたフォームデータのユーザー入力からフィールドを更新します。 Entity Framework の自動変更追跡では、エンティティの[EntityState](<xref:System.Data.EntityState.Modified>)フラグが設定されます。 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)メソッドが呼び出されると、<xref:System.Data.EntityState.Modified> フラグによって、Entity Framework はデータベース行を更新する SQL ステートメントを作成します。 [同時実行の競合](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)は無視され、データベースの行のすべての列が更新されます。これには、ユーザーが変更していないものも含まれます。 (後のチュートリアルでは、同時実行の競合を処理する方法について説明し[ます。](<xref:System.Data.EntityState.Unchanged>)また、データベース内で個々のフィールドを更新するだけの場合は、エンティティを EntityState に設定し、個々のフィールドを[EntityState](<xref:System.Data.EntityState.Modified>)に設定します)。

   過剰な投稿を防ぐために、[編集] ページで更新できるフィールドは、`TryUpdateModel` パラメーターにホワイトリストされています。 現在、他に保護しているフィールドはありませんが、モデル バインダーでバインドしたいフィールドをリストに入れておくと、後でデータ モデルにフィールドを追加した場合に、ここでフィールドを明示的に追加するまで、自動的にフィールドを保護できます。

   これらの変更の結果、HttpPost Edit メソッドのメソッドシグネチャは、HttpGet edit メソッドと同じになります。そのため、EditPost メソッドの名前を変更しました。

   > [!TIP]
   >
   > **エンティティの状態と Attach メソッドと SaveChanges メソッド**
   >
   > データベース コンテキストは、メモリ内のエンティティがデータベースの対応する行と同期しているかどうかを追跡しており、この情報により、`SaveChanges` メソッドを呼び出したときの処理が決まります。 たとえば、 [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)メソッドに新しいエンティティを渡すと、そのエンティティの状態が `Added`に設定されます。 次に、 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)メソッドを呼び出すと、データベースコンテキストによって SQL `INSERT` コマンドが発行されます。
   >
   > エンティティは、次のいずれかの[状態](xref:System.Data.EntityState)になることがあります。
   >
   > - [https://login.microsoftonline.com/consumers/](`Added`) エンティティがデータベースにまだ存在しません。 `SaveChanges` メソッドは、`INSERT` ステートメントを発行する必要があります。
   > - [https://login.microsoftonline.com/consumers/](`Unchanged`) `SaveChanges` メソッドはこのエンティティに対し何も行う必要はありません。 データベースからエンティティを読み取ると、エンティティはこの状態で開始します。
   > - [https://login.microsoftonline.com/consumers/](`Modified`) エンティティのプロパティ値の一部またはすべてが変更されています。 `SaveChanges` メソッドは、`UPDATE` ステートメントを発行する必要があります。
   > - [https://login.microsoftonline.com/consumers/](`Deleted`) エンティティには削除のマークが付けられています。 `SaveChanges` メソッドは、`DELETE` ステートメントを発行する必要があります。
   > - [https://login.microsoftonline.com/consumers/](`Detached`) エンティティはデータベース コンテキストによって追跡されていません。
   >
   > デスクトップ アプリケーションにおいて、通常、状態の変更は自動的に設定されます。 デスクトップの種類のアプリケーションでは、エンティティを読み取り、そのプロパティ値の一部を変更します。 そのエンティティの状態は自動的に `Modified` に変更されます。 次に、`SaveChanges`を呼び出すと、変更した実際のプロパティのみを更新する SQL `UPDATE` ステートメントが Entity Framework によって生成されます。
   >
   > Web apps の接続が切断されても、この連続シーケンスは許可されません。 エンティティを読み取る[Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)は、ページが表示された後に破棄されます。 `HttpPost` `Edit` アクションメソッドが呼び出されると、新しい要求が行われ、 [Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)の新しいインスタンスが作成されます。そのため、エンティティの状態を手動で `Modified.` に設定する必要があります。これにより、`SaveChanges`を呼び出すと、変更したプロパティを確認する方法がないため、Entity Framework はデータベース行のすべての列を更新します。
   >
   > SQL `Update` ステートメントで、ユーザーが実際に変更したフィールドのみを更新する場合は、元の値を何らかの方法 (非表示フィールドなど) に保存して、`HttpPost` `Edit` メソッドが呼び出されたときに使用できるようにすることができます。 次に、元の値を使用して `Student` エンティティを作成し、エンティティの元のバージョンで `Attach` メソッドを呼び出して、エンティティの値を新しい値に更新してから `SaveChanges.` を呼び出します。詳細については、「[エンティティの状態と SaveChanges](/ef/ef6/saving/change-tracking/entity-state)および[ローカルデータ](/ef/ef6/querying/local-data)」を参照してください。

   *Views\Student\Edit.cshtml*の HTML および Razor コードは、「 *cshtml*」で説明したものと似ていますが、変更は必要ありません。

2. このページを実行するには、プログラムを起動し、 **[Students]** タブを選択してから、**編集**ハイパーリンクをクリックします。

3. データをいくつか変更し、 **[Save]** をクリックします。 変更したデータが [インデックス] ページに表示されます。

4. ブラウザーを閉じます。

## <a name="update-the-delete-page"></a>削除ページを更新する

*Controllers\StudentController.cs*では、<xref:System.Web.Mvc.HttpGetAttribute> `Delete` メソッドのテンプレートコードは `Find` メソッドを使用して、選択した `Student` エンティティを取得します。これは、`Details` メソッドと `Edit` メソッドで見たとおりです。 ただし、`SaveChanges` の呼び出しが失敗したときのカスタム エラー メッセージを実装するには、何らかの機能とその対応するビューをこのメソッドに追加します。

更新および作成操作で見たように、削除操作にも 2 つのアクション メソッドが必要です。 GET 要求への応答として呼び出されるメソッドは、ユーザーが削除操作を承認またはキャンセルする機会を提供するビューを表示します。 ユーザーが操作を承認すると、POST 要求が作成されます。 この場合、`HttpPost` `Delete` メソッドが呼び出され、そのメソッドが実際に削除操作を実行します。

<xref:System.Web.Mvc.HttpPostAttribute> `Delete` メソッドに `try-catch` ブロックを追加して、データベースの更新時に発生する可能性のあるエラーを処理します。 エラーが発生した場合、<xref:System.Web.Mvc.HttpPostAttribute> `Delete` メソッドは <xref:System.Web.Mvc.HttpGetAttribute> `Delete` メソッドを呼び出し、エラーが発生したことを示すパラメーターを渡します。 その後、<xref:System.Web.Mvc.HttpGetAttribute> `Delete` メソッドによって、確認ページがエラーメッセージと共に再表示され、ユーザーはキャンセルまたは再試行することができます。

1. <xref:System.Web.Mvc.HttpGetAttribute> `Delete` アクションメソッドを、エラー報告を管理する次のコードに置き換えます。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    このコードは、変更の保存に失敗した後にメソッドが呼び出されたかどうかを示す[省略可能なパラメーター](https://msdn.microsoft.com/library/dd264739.aspx)を受け取ります。 このパラメーターは、前のエラーを発生させずに `HttpGet` `Delete` メソッドが呼び出されたときに `false` ます。 データベース更新エラーに応答して `HttpPost` `Delete` メソッドによって呼び出された場合、パラメーターは `true` され、エラーメッセージがビューに渡されます。

2. <xref:System.Web.Mvc.HttpPostAttribute> `Delete` アクションメソッド (名前付き `DeleteConfirmed`) を次のコードに置き換えます。このコードは、実際の削除操作を実行し、データベースの更新エラーをキャッチします。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    このコードは、選択したエンティティを取得し、 [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)メソッドを呼び出して、エンティティの状態を `Deleted`に設定します。 `SaveChanges` が呼び出されると、SQL `DELETE` コマンドが生成されます。 また、アクション メソッドの名前を `DeleteConfirmed` から `Delete` に変更しています。 `HttpPost` `Delete` メソッドという名前のスキャフォールディングコードは、`HttpPost` メソッドに一意の署名を与える `DeleteConfirmed` ます。 (CLR では、オーバーロードされたメソッドで異なるメソッドパラメーターを持つ必要があります)。署名が一意であるため、MVC 規則を使用して、`HttpPost` と `HttpGet` delete メソッドに同じ名前を使用することができます。

    大規模なアプリケーションのパフォーマンスを向上させることが優先される場合は、`Find` と `Remove` メソッドを呼び出すコード行を次のコードに置き換えることによって、不要な SQL クエリを使用して行を取得することを回避できます。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    このコードは、主キーの値のみを使用して `Student` エンティティをインスタンス化し、エンティティの状態を `Deleted`に設定します。 エンティティを削除するために Entity Framework に必要なものは主キーの値だけです

    前述のように、`HttpGet` `Delete` メソッドはデータを削除しません。 GET 要求に応答して削除操作を実行する (または、任意の編集操作、作成操作、またはデータを変更するその他の操作を実行する) と、セキュリティ上のリスクが生じます。 詳細については、「ASP.NET MVC Tip #46」を参照してください。 Stephen Walther のブログに[セキュリティホールが作成されるため、削除リンクは使用しない](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)でください。

3. *Views\Student\Delete.cshtml*で、次の例に示すように、`h2` 見出しと `h3` 見出しの間にエラーメッセージを追加します。

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. このページを実行するには、プログラムを起動し、 **[Students]** タブを選択し、 **[Delete]** hyperlink をクリックします。

5. ページで **[削除]** を選択します。これを削除します**か?**

    削除された学生を含まないインデックスページが表示されます。 ([同時実行のチュートリアル](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)で動作しているエラー処理コードの例については、「」を参照してください)。

## <a name="close-database-connections"></a>データベース接続を閉じる

データベース接続を閉じて、できるだけ早く保持するリソースを解放するには、終了時にコンテキストインスタンスを破棄します。 このため、スキャフォールディングコードでは、次の例に示すように、 *StudentController.cs*の `StudentController` クラスの末尾に[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)メソッドが用意されています。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

基本 `Controller` クラスは、既に `IDisposable` インターフェイスを実装しているため、このコードは単にオーバーライドを `Dispose(bool)` メソッドに追加して、コンテキストインスタンスを明示的に破棄します。

## <a name="handle-transactions"></a>トランザクションを処理する

既定では、Entity Framework はトランザクションを暗黙的に実装します。 複数の行またはテーブルを変更してから `SaveChanges`を呼び出す場合、Entity Framework によって自動的にすべての変更が成功するか、すべて失敗するかが自動的に決定されます。 一部の変更が完了した後でエラーが発生した場合、それらの変更は自動的にロールバックされます。 より多くの制御&mdash;必要なシナリオ (トランザクションで Entity Framework の外部で行われた操作を含める場合など) については&mdash;「[トランザクションの使用](/ef/ef6/saving/transactions)」を参照してください。

## <a name="get-the-code"></a>コードの入手

[完成したプロジェクトのダウンロード](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他のリソース

これで、`Student` エンティティに対して単純な CRUD 操作を実行する一連のページが完成しました。 MVC ヘルパーを使用して、データフィールドの UI 要素を生成した。 MVC ヘルパーの詳細については、「 [HTML ヘルパーを使用したフォームのレンダリング](/previous-versions/aspnet/dd410596(v=vs.98))」を参照してください (mvc 3 向けの記事ですが、mvc 5 には引き続き関連します)。

他の EF 6 リソースへのリンクについては、「 [ASP.NET Data Access-推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 詳細ページを作成しました
> * Create ページを更新した
> * HttpPost Edit メソッドを更新しました
> * Delete ページを更新した
> * データベース接続を閉じた
> * 処理されたトランザクション

次の記事に進み、並べ替え、フィルター処理、およびページングをプロジェクトに追加する方法を学習してください。
> [!div class="nextstepaction"]
> [並べ替え、フィルター処理、ページング](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
