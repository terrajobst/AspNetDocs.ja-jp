---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 'チュートリアル: MVC 5 Web アプリの高度な EF シナリオについて説明します。'
description: このチュートリアルでは、Entity Framework Code First を使用する ASP.NET web アプリケーションを開発する際の基本事項を理解するのに役立ついくつかのトピックを紹介します。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "58425276"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>チュートリアル: MVC 5 Web アプリの高度な EF シナリオについて説明します。

前のチュートリアルでは、階層ごとの継承を実装しています。 このチュートリアルでは、Entity Framework Code First を使用する ASP.NET web アプリケーションを開発する際の基本事項を理解するのに役立ついくつかのトピックを紹介します。 最初のいくつかのセクションでは、コードを順を追って説明し、Visual Studio を使用してタスクを完了する手順について説明します。詳細については、次のセクションでは、簡単な紹介とリソースへのリンクについて説明します。

これらのトピックのほとんどでは、既に作成したページを操作します。 生の SQL を使用して一括更新を行うには、データベース内のすべてのコースのクレジット数を更新する新しいページを作成します。

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * 生 SQL クエリを実行する
> * 追跡なしのクエリの実行
> * データベースに送信された SQL クエリの確認

以下についても説明します。

> [!div class="checklist"]
> * 抽象化レイヤーの作成
> * プロキシクラス
> * 変更の自動検出
> * 自動検証
> * Entity Framework パワーツール
> * Entity Framework ソースコード

## <a name="prerequisite"></a>必須コンポーネント

* [継承の実装](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>生 SQL クエリを実行する

Entity Framework Code First API には、SQL コマンドをデータベースに直接渡すことができるようにするメソッドが含まれています。 次のオプションがあります。

- エンティティ型を返すクエリには、 [Dbset SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx)メソッドを使用します。 返されるオブジェクトは、 `DbSet`オブジェクトによって予期される型である必要があります。また、追跡をオフにしない限り、データベースコンテキストによって自動的に追跡されます。 ( [Asnotracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx)メソッドについては、次のセクションを参照してください)。
- エンティティではない型を返すクエリには、[データベースの SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx)メソッドを使用します。 このメソッドを使用してエンティティ型を取得する場合でも、返されるデータはデータベース コンテキストによって追跡されません。
- クエリ以外のコマンドには、[データベースの ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx)を使用します。

Entity Framework を使用する利点の 1 つは、データを格納する特定のメソッドにコードを過度に接近させなくてもよい点です。 SQL クエリとコマンドが生成されるため、自分でこれらを記述する必要がなくなります。 ただし、手動で作成した特定の SQL クエリを実行する必要がある場合は、例外的なシナリオがあります。これらのメソッドを使用すると、このような例外を処理できます。

Web アプリケーションで SQL コマンドを実行する場合は常に、SQL インジェクション攻撃から自身のサイトを保護する対策を講じる必要があります。 これを行う 1 つの方法として、パラメーター化されたクエリを使用して、Web ページによって送信された文字列が SQL コマンドとして解釈できないことを確認します。 このチュートリアルでは、ユーザー入力をクエリに統合するときに、パラメーター化されたクエリを使用します。

### <a name="calling-a-query-that-returns-entities"></a>エンティティを返すクエリの呼び出し

[&lt;DbsetTEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx)クラスには、型`TEntity`のエンティティを返すクエリを実行するために使用できるメソッドが用意されています。 このしくみを確認するには、 `Details` `Department`コントローラーのメソッドのコードを変更します。

*DepartmentController.cs* `Details`のメソッドで`db.Departments.SqlQuery` 、次の強調表示されたコードに示すように、メソッドの呼び出しをメソッドの呼び出しに置き換えます。`db.Departments.FindAsync`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

新しいコードが正しく動作することを確認するには、 **[Departments]\(部門\)** タブを選択し、いずれかの部門の **[Details]\(詳細\)** を選択します。 すべてのデータが想定どおりに表示されることを確認します。

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>他の種類のオブジェクトを返すクエリの呼び出し

以前に、登録日ごとの学生数を示す About ページ用に、学生の統計グリッドを作成しました。 *HomeController.cs*でこれを実行するコードは、LINQ を使用します。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

LINQ を使用するのではなく、このデータを直接 SQL で取得するコードを記述するとします。 そのためには、エンティティオブジェクト以外のものを返すクエリを実行する必要があります。これは、[データベースの SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx)メソッドを使用する必要があることを意味します。

*HomeController.cs*で、次の強調表示され`About`たコードに示すように、メソッド内の LINQ ステートメントを SQL ステートメントに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

[バージョン情報] ページを実行します。 前と同じデータが表示されていることを確認します。

### <a name="calling-an-update-query"></a>更新クエリの呼び出し

Contoso 大学の管理者が、すべてのコースのクレジットの数を変更するなど、データベースで一括変更を実行できるようにするとします。 大学に多くのコースがある場合は、それらすべてをエンティティとして取得し、それらを個別に変更するのは非効率的です。 このセクションでは、すべてのコースのクレジット数を変更する要素をユーザーが指定できるようにする web ページを実装します。これにより、SQL `UPDATE`ステートメントを実行して変更を行うことができます。 

*CourseController.cs*で、と`UpdateCourseCredits`の`HttpGet`メソッドを`HttpPost`追加します。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

コントローラーが`HttpGet`要求を処理すると、 `ViewBag.RowsAffected`変数に何も返されず、ビューに空のテキストボックスと [送信] ボタンが表示されます。

**[更新]** ボタンをクリック`HttpPost`すると、メソッド`multiplier`が呼び出され、テキストボックスに値が入力されます。 次に、このコードは、コースを更新する SQL を実行し、影響を受ける行の`ViewBag.RowsAffected`数を変数のビューに返します。 ビューがその変数の値を取得すると、テキストボックスと送信ボタンではなく、更新された行の数が表示されます。

*CourseController.cs*で、いずれかの`UpdateCourseCredits`メソッドを右クリックし、[ビューの**追加**] をクリックします。 **[ビューの追加]** ダイアログボックスが表示されます。 既定値のままにして、 **[追加]** を選択します。

*Views\Course\UpdateCourseCredits.cshtml*で、テンプレートコードを次のコードに置き換えます。

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

**[Courses]\(コース\)** タブを選択してから、ブラウザーのアドレス バーで URL の末尾に "/UpdateCourseCredits" を追加して (例: `http://localhost:50205/Course/UpdateCourseCredits`)、`UpdateCourseCredits` メソッドを実行します。 テキスト ボックスに数値を入力します。

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

**[更新]** をクリックします。 影響を受けた行の数が表示されます。

**[リストに戻る]** をクリックして、単位数が変更されたコースの一覧を表示します。

未加工の SQL クエリの詳細については、MSDN の「[未加工の Sql クエリ](https://msdn.microsoft.com/data/jj592907)」を参照してください。

## <a name="no-tracking-queries"></a>追跡なしのクエリ

データベース コンテキストは、テーブルの行を取得してそれらを表すエンティティ オブジェクトを作成するとき、既定では、メモリ内のエンティティがデータベース内のデータと同期されているかどうかを追跡します。 メモリ内のデータはキャッシュとして機能し、エンティティを更新するときに使われます。 Web アプリケーションでは、一般にコンテキスト インスタンスの存続期間は短く (要求ごとに新しいインスタンスが作成されて破棄されます)、通常、エンティティを読み取るコンテキストはエンティティが再び使われる前に破棄されるので、多くの場合、このようなキャッシュは必要ありません。

[Asnotracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)メソッドを使用して、メモリ内のエンティティオブジェクトの追跡を無効にすることができます。 追跡を無効にした方がよい一般的なシナリオを以下に示します。

- クエリでは、追跡を無効にする大量のデータを取得すると、パフォーマンスが著しく向上する可能性があります。
- エンティティを更新するためにアタッチする必要があるが、以前に別の目的で同じエンティティを取得した場合。 エンティティはデータベース コンテキストによって既に追跡されているため、変更するエンティティをアタッチできません。 この状況に対処する方法の`AsNoTracking` 1 つは、前のクエリでオプションを使用することです。

[Asnotracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)メソッドの使用方法を示す例については、[このチュートリアルの前のバージョン](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)を参照してください。 このバージョンのチュートリアルでは、編集メソッドでモデルバインダーによって作成されたエンティティに変更フラグが設定され`AsNoTracking`ていないため、必要ありません。

## <a name="examine-sql-sent-to-database"></a>データベースに送信された SQL を調べる

データベースに送信される実際の SQL クエリを確認できると役立つ場合があります。 前のチュートリアルでは、インターセプターコードでこれを行う方法を説明しました。ここで、インターセプターコードを記述せずにこれを実行するいくつかの方法について説明します。 これを試すには、単純なクエリを見て、一括読み込み、フィルター処理、並べ替えなどのオプションを追加したときに何が起こるかを見てみましょう。

の一括読み込みを一時的に停止`Index`するには、 *Controllers/CourseController*で、メソッドを次のコードに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

次に、 `return`ステートメントにブレークポイントを設定します (その行のカーソルを使用して、F9 キーを押します)。 **F5**キーを押してプロジェクトをデバッグモードで実行し、[Course Index] ページを選択します。 コードがブレークポイントに到達したら、 `sql`変数を調べます。 SQL Server に送信されるクエリが表示されます。 これは単純な`Select`ステートメントです。

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

虫眼鏡をクリックすると、**テキストビジュアライザー**でクエリが表示されます。

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

次に、ユーザーが特定の部門をフィルター処理できるように、[コースのインデックス] ページにドロップダウンリストを追加します。 コースはタイトルで並べ替えることができ、 `Department`ナビゲーションプロパティの一括読み込みを指定します。

*CourseController.cs*で、 `Index`メソッドを次のコードに置き換えます。

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

`return`ステートメントにブレークポイントを復元します。

メソッドは、 `SelectedDepartment`パラメーターのドロップダウンリストの選択された値を受け取ります。 何も選択されていない場合、このパラメーターは null になります。

すべての部門を含むコレクションがドロップダウンリストのビューに渡されます。`SelectList` `SelectList`コンストラクターに渡されるパラメーターは、値フィールド名、テキストフィールド名、および選択された項目を指定します。

このコードでは、 `Course`リポジトリの`Department` メソッドに対して、ナビゲーションプロパティのフィルター式、並べ替え順序、および一括読み込みを指定しています。`Get` ドロップダウンリストで何`true`も選択されていない場合 (つまり、 `SelectedDepartment`が null の場合)、フィルター式は常にを返します。

*Views\Course\Index.cshtml*の開始`table`タグの直前に、ドロップダウンリストと [送信] ボタンを作成する次のコードを追加します。

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

ブレークポイントを設定したまま、[コースのインデックス] ページを実行します。 コードが最初にブレークポイントにヒットしたときに、ページがブラウザーに表示されるようにします。 ドロップダウンリストから部門を選択し、 **[フィルター]** をクリックします。

今回は、ドロップダウンリストの部門クエリの最初のブレークポイントになります。 これをスキップし、 `query`次にコードがブレークポイントに到達したときに変数を表示`Course`して、クエリがどのように見えるかを確認します。 次のような内容が表示されます。

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

クエリが`JOIN` データと`Course`共にデータを読み込み`Department` 、句を`WHERE`含むクエリであることがわかります。

行を`var sql = courses.ToString()`削除します。

## <a name="create-an-abstraction-layer"></a>抽象化レイヤーを作成する

多くの開発者は、Entity Framework で動作するコードをラップするラッパーとして、Repository パターンと Unit of Work パターンを実装するためのコードを記述します。 これらのパターンは、アプリケーションのデータ アクセス層とビジネス ロジック層の間に抽象化レイヤーを作成するためのものです。 これらのパターンを実装すると、データ ストアの変更からアプリケーションを隔離でき、自動化された単体テストやテスト駆動開発 (TDD) を円滑化できます。 ただし、次のような理由から、これらのパターンを実装するための追加コードを記述することは、EF を使用するアプリケーションには必ずしも最適な選択肢とは言えません。

- EF コンテキスト クラス自体が、コードをデータ ストア固有のコードから隔離します。
- EF コンテキスト クラスは、EF を使用して行っているデータベースの更新の unit-of-work クラスとして動作できます。
- Entity Framework 6 で導入された機能を使用すると、リポジトリコードを記述しなくても TDD を簡単に実装できます。

リポジトリと作業単位パターンを実装する方法の詳細については、[このチュートリアルシリーズの Entity Framework 5 バージョン](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)を参照してください。 Entity Framework 6 で TDD を実装する方法の詳細については、次のリソースを参照してください。

- [EF6 による DbSets のモックの簡単な有効化](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [モックフレームワークを使用したテスト](https://msdn.microsoft.com/data/dn314429)
- [独自のテストの倍精度でテストする](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>プロキシクラス

Entity Framework がエンティティインスタンスを作成するとき (たとえば、クエリの実行時)、エンティティのプロキシとして機能する動的に生成された派生型のインスタンスとして作成されることがよくあります。 たとえば、次の2つのデバッガーイメージを参照してください。 最初の図では、エンティティをインスタンス`student`化した直後`Student`に変数が予期される型であることがわかります。 2番目のイメージでは、EF を使用してデータベースから student エンティティを読み取ると、プロキシクラスが表示されます。

![Before プロキシクラス](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![After プロキシクラス](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

このプロキシクラスは、プロパティにアクセスしたときにアクションを自動的に実行するフックを挿入するために、エンティティの一部の仮想プロパティをオーバーライドします。 このメカニズムを使用して遅延読み込みを行う関数が1つあります。

ほとんどの場合、このプロキシの使用を意識する必要はありませんが、例外があります。

- 場合によっては、Entity Framework がプロキシインスタンスを作成できないようにする必要があります。 たとえば、エンティティをシリアル化する場合、通常はプロキシクラスではなく、POCO クラスが必要です。 シリアル化の問題を回避する1つの方法は、「 [Using WEB API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md)チュートリアル」に示されているように、エンティティオブジェクトではなくデータ転送オブジェクト (dto) をシリアル化することです。 もう1つの方法は、[プロキシの作成を無効](https://msdn.microsoft.com/data/jj592886.aspx)にすることです。
- `new`演算子を使用してエンティティクラスをインスタンス化する場合、プロキシインスタンスは取得されません。 これは、遅延読み込みや自動変更追跡などの機能を利用できないことを意味します。 これは通常は問題ありません。通常、遅延読み込みは必要ありません。これは、データベースに存在しない新しいエンティティを作成しているためです。また、エンティティをとして`Added`明示的にマークしている場合は、通常、変更の追跡は必要ありません。 ただし、遅延読み込みが必要で、変更の追跡が必要な場合は、 `DbSet`クラスの[create](https://msdn.microsoft.com/library/gg679504.aspx)メソッドを使用して、プロキシを使用して新しいエンティティインスタンスを作成できます。
- プロキシ型から実際のエンティティ型を取得することもできます。 `ObjectContext`クラスの[GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx)メソッドを使用して、プロキシ型インスタンスの実際のエンティティ型を取得できます。

詳細については、MSDN の「[プロキシの](https://msdn.microsoft.com/data/JJ592886.aspx)使用」を参照してください。

## <a name="automatic-change-detection"></a>変更の自動検出

Entity Framework では、エンティティの現在の値と元の値を比較して、エンティティがどのように変更されたか (およびそれによって、どの更新プログラムをデータベースに送信する必要があるか) を判断します。 元の値は、エンティティが照会されるかアタッチされるときに格納されます。 変更の自動検出を行うメソッドには、次のようなものがあります。

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

多数のエンティティを追跡していて、これらのメソッドのいずれかをループ内で何度も呼び出す場合、 [autodetection の有効な](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx)プロパティを使用して自動変更検出を一時的に無効にすると、パフォーマンスが大幅に向上する可能性があります。 詳細については、MSDN の「[変更を自動的に検出](https://msdn.microsoft.com/data/jj556205)する」を参照してください。

## <a name="automatic-validation"></a>自動検証

`SaveChanges`メソッドを呼び出すと、既定では、Entity Framework は、データベースを更新する前に、変更されたすべてのエンティティのすべてのプロパティのデータを検証します。 多数のエンティティを更新していて、既にデータを検証している場合、この作業は不要であり、変更の保存プロセスを一時的に無効にすることによって時間を短縮することができます。 これは、 [Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx)プロパティを使用して行うことができます。 詳細については、MSDN の「[検証](https://msdn.microsoft.com/data/gg193959)」を参照してください。

## <a name="entity-framework-power-tools"></a>Entity Framework パワーツール

[Entity Framework パワーツール](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition)は、これらのチュートリアルで示すデータモデルダイアグラムを作成するために使用された Visual Studio アドインです。 また、このツールでは、既存のデータベース内のテーブルに基づいてエンティティクラスを生成するなど、他の機能を実行して、Code First でデータベースを使用できるようにすることもできます。 ツールをインストールすると、いくつかの追加オプションがコンテキストメニューに表示されます。 たとえば、**ソリューションエクスプローラー**でコンテキストクラスを右クリックすると、と**Entity Framework**  オプションが表示されます。 これにより、図を生成することができます。 Code First を使用している場合、図のデータモデルを変更することはできませんが、わかりやすくするために移動することができます。

![EF の図](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>Entity Framework ソースコード

Entity Framework 6 のソースコードは、 [GitHub](https://github.com/aspnet/EntityFramework6)で入手できます。 バグを提出することができます。また、EF ソースコードに独自の拡張機能を提供することもできます。

ソースコードは開かれていますが、Entity Framework は Microsoft 製品として完全にサポートされています。 Microsoft Entity Framework チームは、各リリースの品質を保証するため、受け入れる投稿を管理し、すべてのコード変更をテストしています。

## <a name="acknowledgments"></a>謝辞

- Tom Dykstra は、このチュートリアルの元のバージョンを作成し、EF 5 更新プログラムを併置し、EF 6 更新プログラムを記述しました。 Tom は、Microsoft Web Platform and Tools コンテンツチームのシニアプログラミングライターです。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/)(twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) は、ef 5 および MVC 4 のチュートリアルを更新し、ef 6 更新プログラムを共同作成しました。 Rick は、Microsoft が Azure と MVC に注力するシニアプログラミングライターです。
- Entity Framework チームの[Rowan 明美](http://www.romiller.com)とその他のメンバーは、コードレビューを支援し、ef 5 および ef 6 のチュートリアルを更新している間に発生した移行に関する多くの問題のデバッグを支援しました。

## <a name="troubleshoot-common-errors"></a>一般的なエラーのトラブルシューティング

### <a name="cannot-createshadow-copy"></a>作成/シャドウコピーできません

エラー メッセージ:

> ファイルが既に存在する&lt;場合&gt;は、' filename ' を作成/シャドウコピーできません。

ソリューション

数秒待ってから、ページを更新してください。

### <a name="update-database-not-recognized"></a>更新-データベースを認識できません

エラーメッセージ (PMC の`Update-Database`コマンドから):

> "データベースの更新" という用語は、コマンドレット、関数、スクリプトファイル、または操作可能なプログラムの名前として認識されません。 名前が正しく記述されていることを確認し、パスが含まれている場合はそのパスが正しいことを確認してから、再試行してください。

ソリューション

Visual Studio を終了します。 プロジェクトを再度開き、もう一度やり直してください。

### <a name="validation-failed"></a>検証失敗

エラーメッセージ (PMC の`Update-Database`コマンドから):

> 1つ以上のエンティティの検証に失敗しました。 詳細については、' EntityValidationErrors ' プロパティを参照してください。

ソリューション

この問題の原因の1つは、メソッド`Seed`の実行時の検証エラーです。 メソッドのデバッグに関するヒントについては、 `Seed` 「 [Entity Framework (EF) db のシード処理とデバッグ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)」を参照してください。

### <a name="http-50019-error"></a>HTTP 500.19 エラー

エラー メッセージ:

> HTTP エラー 500.19-内部サーバーエラーページの関連する構成データが無効なため、要求されたページにアクセスできません。

ソリューション

このエラーを発生させる1つの方法は、ソリューションの複数のコピーを保持し、それぞれが同じポート番号を使用することです。 通常、この問題を解決するには、Visual Studio のすべてのインスタンスを終了し、作業中のプロジェクトを再起動します。 それでもうまくいかない場合は、ポート番号を変更してみてください。 プロジェクトファイルを右クリックし、[プロパティ] をクリックします。 **[Web]** タブを選択し、 **[プロジェクトの Url]** テキストボックスでポート番号を変更します。

### <a name="error-locating-sql-server-instance"></a>SQL Server インスタンスの位置を特定しているときのエラー

エラー メッセージ:

> SQL Server への接続を確立しているときに、ネットワーク関連またはインスタンス固有のエラーが発生しました。 サーバーが見つからないかアクセスできません。 インスタンス名が正しいこと、および SQL Server がリモート接続を許可するように構成されていることを確認してください。 (プロバイダー:SQL ネットワーク インターフェイス、エラー:26 - 指定されたサーバーまたはインスタンスの位置を特定しているときにエラーが発生しました)

ソリューション

接続文字列を確認します。 データベースを手動で削除した場合は、構築文字列内のデータベースの名前を変更します。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトのダウンロード](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他の技術情報

 Entity Framework を使用してデータを操作する方法の詳細については、 [MSDN の EF ドキュメントページ](https://msdn.microsoft.com/data/ee712907)および[ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)に関するページを参照してください。

Web アプリケーションを構築した後にデプロイする方法の詳細については、MSDN ライブラリの「 [ASP.NET Web Deployment-推奨リソース](../../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。

認証や承認など、MVC に関連するその他のトピックについては、 [ASP.NET mvc の推奨リソース](../recommended-resources-for-mvc.md)を参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * 生 SQL クエリを実行した
> * 追跡なしのクエリを実行しました
> * データベースに送信された SQL クエリを調べています

以下についても学習しました。

> [!div class="checklist"]
> * 抽象化レイヤーの作成
> * プロキシクラス
> * 変更の自動検出
> * 自動検証
> * Entity Framework パワーツール
> * Entity Framework ソースコード

これで、ASP.NET MVC アプリケーションでの Entity Framework の使用に関するこの一連のチュートリアルは完了です。 EF Database First について学習する場合は、DB の最初のチュートリアルシリーズを参照してください。
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)