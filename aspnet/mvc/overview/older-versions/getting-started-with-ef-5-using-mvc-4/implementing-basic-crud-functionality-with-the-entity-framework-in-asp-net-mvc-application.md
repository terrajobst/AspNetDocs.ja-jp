---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した基本的な CRUD 機能の実装 (2/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: eba146d2975e0dcf243facf7c205c4acfe40b6f6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595331"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>ASP.NET MVC アプリケーションでの Entity Framework を使用した基本的な CRUD 機能の実装 (2/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、Entity Framework と SQL Server LocalDB を使用してデータを格納および表示する MVC アプリケーションを作成しました。 このチュートリアルでは、MVC スキャフォールディングによってコントローラーとビューに自動的に作成される CRUD (作成、読み取り、更新、削除) コードを確認し、カスタマイズします。

> [!NOTE]
> コントローラーとデータ アクセス層の間に抽象化レイヤーを作成するためにリポジトリ パターンを実装することは、よく行われることです。 これらのチュートリアルを簡単にするために、このシリーズの後のチュートリアルまではリポジトリを実装しません。

このチュートリアルでは、次の web ページを作成します。

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>詳細ページの作成

このプロパティにはコレクションが保持されているため、[Students `Index`] ページのスキャフォールディングコードは `Enrollments` プロパティの左側にあります。 [`Details`] ページには、コレクションの内容が HTML テーブルとして表示されます。

 *Controllers\StudentController.cs*では、`Details` ビューのアクションメソッドは、`Find` メソッドを使用して1つの `Student` エンティティを取得します。 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 キー値は `id` パラメーターとしてメソッドに渡され、インデックスページの**詳細**ハイパーリンクのルートデータから取得されます。 

1. *Views\Student\Details.cshtml*を開きます。 各フィールドは、次の例に示すように、`DisplayFor` ヘルパーを使用して表示されます。 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. `EnrollmentDate` フィールドの後、終了 `fieldset` タグの直前に、次の例に示すように、登録の一覧を表示するコードを追加します。

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    このコードは、`Enrollments` ナビゲーション プロパティ内のエンティティをループ処理します。 プロパティ内の `Enrollment` エンティティごとに、コースタイトルとグレードが表示されます。 コースタイトルは、`Enrollments` エンティティの `Course` ナビゲーションプロパティに格納されている `Course` エンティティから取得されます。 必要に応じて、すべてのデータがデータベースから自動的に取得されます。 (つまり、ここで遅延読み込みを使用しているとします。 `Courses` ナビゲーションプロパティに*一括読み込み*を指定しなかったため、そのプロパティに初めてアクセスしようとすると、データを取得するためのクエリがデータベースに送信されます。 遅延読み込みと一括読み込みの詳細については、このシリーズの後の「[関連データの読み取り](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)」チュートリアルを参照してください)。
3. **Students** タブを選択し、アレクサンドロス Carson の  **Details** リンクをクリックして、ページを実行します。 選んだ受講者のコースとグレードの一覧が表示されます。

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>Create ページを更新しています

1. *Controllers\StudentController.cs*で、`HttpPost``Create` アクションメソッドを次のコードに置き換えて、`try-catch` ブロックと[バインド属性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)をスキャフォールディングメソッドに追加します。 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    このコードは、ASP.NET MVC モデルバインダーによって作成された `Student` エンティティを `Students` エンティティセットに追加し、変更をデータベースに保存します。 (*モデルバインダー*とは、フォームによって送信されたデータを簡単に操作できるようにする ASP.NET MVC 機能のことです。モデルバインダーは、ポストされたフォーム値を CLR 型に変換し、パラメーターのアクションメソッドに渡します。 この場合、モデルバインダーは、`Form` コレクションのプロパティ値を使用して `Student` エンティティをインスタンス化します)。

    `ValidateAntiForgeryToken` 属性は、[クロスサイト要求偽造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻撃を防ぐのに役立ちます。

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. **[Students]** タブを選択し、 **[新規作成]** をクリックして、ページを実行します。

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    一部のデータの検証は、既定で動作します。 名前と無効な日付を入力し、 **[作成]** をクリックしてエラーメッセージを表示します。

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    次の強調表示されたコードは、モデルの検証チェックを示しています。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    日付を9/1/2005 などの有効な値に変更し、 **[作成]** をクリックして、新しい学生が**インデックス**ページに表示されることを確認します。

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>[投稿の編集] ページの更新

*Controllers\StudentController.cs*では、`HttpGet` `Edit` メソッド (`HttpPost` 属性を持たないメソッド) は、`Find` メソッドを使用して、`Student` メソッドで見たように、選択した `Details` エンティティを取得します。 このメソッドを変更する必要はありません。

ただし、`HttpPost` `Edit` アクションメソッドを次のコードに置き換えて、`try-catch` ブロックと[バインド属性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)を追加します。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

このコードは、`HttpPost` `Create` メソッドで見たものと似ています。 ただし、モデルバインダーによって作成されたエンティティをエンティティセットに追加するのではなく、このコードによってエンティティにフラグが設定され、変更されたことが示されます。 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)メソッドが呼び出されると、[変更](https://msdn.microsoft.com/library/system.data.entitystate.aspx)されたフラグによって ENTITY FRAMEWORK によって SQL ステートメントが作成され、データベース行が更新されます。 データベースの行のすべての列が更新されます。これには、ユーザーが変更していない列や同時実行の競合は無視されます。 (このシリーズの後のチュートリアルで、同時実行を処理する方法について説明します)。

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>エンティティの状態と Attach メソッドと SaveChanges メソッド

データベース コンテキストは、メモリ内のエンティティがデータベースの対応する行と同期しているかどうかを追跡しており、この情報により、`SaveChanges` メソッドを呼び出したときの処理が決まります。 たとえば、 [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)メソッドに新しいエンティティを渡すと、そのエンティティの状態が `Added`に設定されます。 次に、 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)メソッドを呼び出すと、データベースコンテキストによって SQL `INSERT` コマンドが発行されます。

エンティティは、次のいずれかの[状態](https://msdn.microsoft.com/library/system.data.entitystate.aspx)になることがあります。

- `Added`. エンティティがデータベースにまだ存在しません。 `SaveChanges` メソッドは、`INSERT` ステートメントを発行する必要があります。
- `Unchanged`. `SaveChanges` メソッドはこのエンティティに対し何も行う必要はありません。 データベースからエンティティを読み取ると、エンティティはこの状態で開始します。
- `Modified`. エンティティのプロパティ値の一部またはすべてが変更されています。 `SaveChanges` メソッドは、`UPDATE` ステートメントを発行する必要があります。
- `Deleted`. エンティティには削除のマークが付けられています。 `SaveChanges` メソッドは、`DELETE` ステートメントを発行する必要があります。
- `Detached`. エンティティはデータベース コンテキストによって追跡されていません。

デスクトップ アプリケーションにおいて、通常、状態の変更は自動的に設定されます。 デスクトップの種類のアプリケーションでは、エンティティを読み取り、そのプロパティ値の一部を変更します。 そのエンティティの状態は自動的に `Modified` に変更されます。 次に、`SaveChanges`を呼び出すと、変更した実際のプロパティのみを更新する SQL `UPDATE` ステートメントが Entity Framework によって生成されます。

Web apps の接続が切断されても、この連続シーケンスは許可されません。 エンティティを読み取る[Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)は、ページが表示された後に破棄されます。 `HttpPost` `Edit` アクションメソッドが呼び出されると、新しい要求が行われ、 [Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)の新しいインスタンスが作成されます。そのため、エンティティの状態を手動で `Modified.` に設定する必要があります。これにより、`SaveChanges`を呼び出すと、変更したプロパティを確認する方法がないため、Entity Framework はデータベース行のすべての列を更新します。

SQL `Update` ステートメントで、ユーザーが実際に変更したフィールドのみを更新する場合は、元の値を何らかの方法 (非表示フィールドなど) に保存して、`HttpPost` `Edit` メソッドが呼び出されたときに使用できるようにすることができます。 次に、元の値を使用して `Student` エンティティを作成し、その元のバージョンのエンティティで `Attach` メソッドを呼び出して、エンティティの値を新しい値に更新してから、`SaveChanges.` を呼び出します。詳細については、MSDN データデベロッパーセンターの「[エンティティの状態と SaveChanges](https://msdn.microsoft.com/data/jj592676)および[ローカルデータ](https://msdn.microsoft.com/data/jj592872)」を参照してください。

*Views\Student\Edit.cshtml*のコードは、例に似ています*が、変更*は必要ありません。

**[Students]** タブを選択し、 **[Edit]** ハイパーリンクをクリックして、ページを実行します。

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

データをいくつか変更し、 **[Save]** をクリックします。 変更したデータが [インデックス] ページに表示されます。

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>削除ページを更新しています

*Controllers\StudentController.cs*では、`HttpGet` `Delete` メソッドのテンプレートコードは `Find` メソッドを使用して、選択した `Student` エンティティを取得します。これは、`Details` メソッドと `Edit` メソッドで見たとおりです。 ただし、`SaveChanges` の呼び出しが失敗したときのカスタム エラー メッセージを実装するには、何らかの機能とその対応するビューをこのメソッドに追加します。

更新および作成操作で見たように、削除操作にも 2 つのアクション メソッドが必要です。 GET 要求への応答として呼び出されるメソッドは、ユーザーが削除操作を承認またはキャンセルする機会を提供するビューを表示します。 ユーザーが操作を承認すると、POST 要求が作成されます。 この場合、`HttpPost` `Delete` メソッドが呼び出され、そのメソッドが実際に削除操作を実行します。

`HttpPost` `Delete` メソッドに `try-catch` ブロックを追加して、データベースの更新時に発生する可能性のあるエラーを処理します。 エラーが発生した場合、`HttpPost` `Delete` メソッドは `HttpGet` `Delete` メソッドを呼び出し、エラーが発生したことを示すパラメーターを渡します。 次に、`HttpGet Delete` メソッドによって、確認ページがエラーメッセージと共に再表示され、ユーザーはキャンセルまたは再試行を行うことができます。

1. `HttpGet` `Delete` アクションメソッドを、エラー報告を管理する次のコードに置き換えます。 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    このコードは、変更の保存に失敗した後に呼び出されたかどうかを示す、[省略可能](https://msdn.microsoft.com/library/dd264739.aspx)なブール型パラメーターを受け取ります。 このパラメーターは、前のエラーを発生させずに `HttpGet` `Delete` メソッドが呼び出されたときに `false` ます。 データベース更新エラーに応答して `HttpPost` `Delete` メソッドによって呼び出された場合、パラメーターは `true` され、エラーメッセージがビューに渡されます。
2. `HttpPost` `Delete` アクションメソッド (名前付き `DeleteConfirmed`) を次のコードに置き換えます。このコードは、実際の削除操作を実行し、データベースの更新エラーをキャッチします。

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     このコードは、選択したエンティティを取得し、 [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)メソッドを呼び出して、エンティティの状態を `Deleted`に設定します。 `SaveChanges` が呼び出されると、SQL `DELETE` コマンドが生成されます。 また、アクション メソッドの名前を `DeleteConfirmed` から `Delete` に変更しています。 `HttpPost` `Delete` メソッドという名前のスキャフォールディングコードは、`HttpPost` メソッドに一意の署名を与える `DeleteConfirmed` ます。 (CLR では、オーバーロードされたメソッドで異なるメソッドパラメーターを持つ必要があります)。署名が一意であるため、MVC 規則を使用して、`HttpPost` と `HttpGet` delete メソッドに同じ名前を使用することができます。

     大規模なアプリケーションのパフォーマンスを向上させることが優先される場合は、`Find` および `Remove` メソッドを呼び出すコード行を、黄色の強調表示に示すように、次のコードに置き換えることにより、不要な SQL クエリを使用して行を取得することを回避できます。

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     このコードは、主キーの値のみを使用して `Student` エンティティをインスタンス化し、エンティティの状態を `Deleted`に設定します。 エンティティを削除するために Entity Framework に必要なものは主キーの値だけです

     前述のように、`HttpGet` `Delete` メソッドはデータを削除しません。 GET 要求に応答して削除操作を実行する (または、任意の編集操作、作成操作、またはデータを変更するその他の操作を実行する) と、セキュリティ上のリスクが生じます。 詳細については、「ASP.NET MVC Tip #46」を参照してください。 Stephen Walther のブログに[セキュリティホールが作成されるため、削除リンクは使用しない](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)でください。
3. *Views\Student\Delete.cshtml*で、次の例に示すように、`h2` 見出しと `h3` 見出しの間にエラーメッセージを追加します。

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     **[Students]** タブを選択し、 **[Delete]** hyperlink をクリックして、ページを実行します。

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. **[Delete]** をクリックします。 削除された学生を含まない [Index] ページが表示されます (このシリーズの後の「[同時実行の処理](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)」チュートリアルでは、エラー処理コードの例を示しています)。

## <a name="ensuring-that-database-connections-are-not-left-open"></a>データベース接続が開いたままになっていないことを確認する

データベース接続が適切に閉じられていることと、それらのリソースが解放されたことを確認するには、コンテキストインスタンスが破棄されていることがわかります。 このため、スキャフォールディングコードでは、次の例に示すように、 *StudentController.cs*の `StudentController` クラスの末尾に[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)メソッドが用意されています。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

基本 `Controller` クラスは、既に `IDisposable` インターフェイスを実装しているため、このコードは単にオーバーライドを `Dispose(bool)` メソッドに追加して、コンテキストインスタンスを明示的に破棄します。

## <a name="summary"></a>要約

これで、`Student` エンティティに対して単純な CRUD 操作を実行する一連のページが完成しました。 MVC ヘルパーを使用して、データフィールドの UI 要素を生成した。 MVC ヘルパーの詳細については、「 [HTML ヘルパーを使用したフォームのレンダリング](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx)」を参照してください (このページは mvc 3 用ですが、mvc 4 にも関連しています)。

次のチュートリアルでは、並べ替えとページングを追加して、インデックスページの機能を拡張します。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [次へ](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
