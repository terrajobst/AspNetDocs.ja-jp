---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した同時実行の処理 (7/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9800a313879477f36a730e6a70c79bc06d403ae3
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074957"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a>ASP.NET MVC アプリケーションでの Entity Framework を使用した同時実行の処理 (7/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前の2つのチュートリアルでは、関連データを操作しました。 このチュートリアルでは、同時実行を処理する方法について説明します。 `Department` エンティティを使用する web ページを作成し、`Department` エンティティを編集および削除するページで同時実行エラーが処理されるようにします。 次の図は、同時実行の競合が発生した場合に表示されるいくつかのメッセージを含む、インデックスと削除ページを示しています。

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>コンカレンシーの競合

あるユーザーがあるエンティティのデータを編集目的で表示したとき、別のユーザーが同じエンティティのデータを最初のユーザーの変更がデータベースに書き込まれる前に更新すると、コンカレンシーの競合が発生します。 このような競合の検出を有効にしないと、最後にデータベースを更新したユーザーが他のユーザーの変更を上書きすることになります。 多くのアプリケーションでは、このリスクが許容されています。ユーザーや更新がわずかであれば、あるいは変更が一部上書きされても大きな問題なければ、コンカレンシーのプログラミングにかかるコストが利点よりも重視されることがあります。 その場合、コンカレンシーの競合を処理するようにアプリケーションを構成する必要はありません。

### <a name="pessimistic-concurrency-locking"></a>ペシミスティック同時実行 (ロック)

コンカレンシーで偶発的にデータが失われる事態をアプリケーションで回避する必要があれば、その方法としてデータベース ロックがあります。 これは、*ペシミスティック同時実行制御*と呼ばれます。 たとえば、データベースから行を読む前に、読み取り専用か更新アクセスでロックを要求します。 更新アクセスで行をロックすると、他のユーザーはその行を読み取り専用または更新アクセスでロックできなくなります。変更中のデータのコピーが与えられるためです。 読み取り専用で行をロックすると、他のユーザーはその行を読み取り専用でロックできますが、更新アクセスではロックできません。

ロックの利用には短所があります。 プログラムが複雑になります。 多くのデータベース管理リソースが必要であり、アプリケーションのユーザー数が増えるにつれてパフォーマンスの問題が発生する可能性があります (つまり、スケールが適切ではありません)。 そのような理由から、一部のデータベース管理システムはペシミスティック コンカレンシーに対応していません。 Entity Framework には、組み込みのサポートはありません。このチュートリアルでは、実装方法については説明しません。

### <a name="optimistic-concurrency"></a>オプティミスティック コンカレンシー

ペシミスティック同時実行制御の代替として、*オプティミスティック同時実行制御*があります。 オプティミスティック コンカレンシーでは、コンカレンシーの競合の発生を許し、発生したら適切に対処します。 たとえば、John は department Edit ページを実行し、英語部門の**予算**額を $350000.00 から $0.00 に変更します。

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John が **[Save]** \ (保存 \) をクリックする前に、加藤さんは同じページを実行し、 **[開始日]** フィールドを9/1/2007 から8/8/2013 に変更します。

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John は最初に **[保存]** をクリックすると、ブラウザーが Index ページに戻ったときに変更が表示され、加藤さんは **[保存]** をクリックします。 この後の動作は、コンカレンシーの競合の処理方法によって決定します。 次のようなオプションがあります。

- ユーザーが変更したプロパティを追跡記録し、それに該当する列だけをデータベースで更新できます。 例のシナリオでは、2 人のユーザーが異なるプロパティを更新したため、データは失われません。 次に他のユーザーが English department を閲覧すると、John と Jane の両方の変更 (開始日は8/8/2013、予算はゼロドル) が表示されます。

    この更新方法では、データの損失につながる可能性がある競合の数を減らすことができますが、あるエンティティの同じプロパティに対して行われた変更が競合する場合、データの損失は避けられません。 Entity Framework がこのように動作するかどうかは、更新コードの実装方法に依存します。 これは Web アプリケーションの場合、実用的ではない場合が多いです。あるエンティティの新しい値に加え、元のプロパティ値もすべて追跡記録するため、大量のステータスを更新することになるからです。 大量の状態を維持すると、アプリケーションのパフォーマンスに影響を与える可能性があります。これは、サーバーリソースが必要であるか、または web ページ自体に含まれている必要があるためです (非表示フィールドなど)。
- 加藤さんの変更によって John の変更が上書きされるようにすることができます。 次に、他のユーザーが English department を参照したときに、8/8/2013 と復元された $350000.00 値が表示されます。 これは *Client Wins* (クライアント側に合わせる) シナリオまたは *Last in Wins* (最終書き込み者優先) シナリオと呼ばれています。 (クライアントの値は、データストアの内容よりも優先されます)。このセクションの概要で説明したように、同時実行処理のコーディングを行わない場合は、自動的に行われます。
- Jane の変更がデータベースで更新されないようにすることができます。 通常は、エラーメッセージを表示して、データの現在の状態を表示します。その後、ユーザーが変更を行う場合は、その変更を再適用できるようにします。 これは *Store Wins* (ストア側に合わせる) シナリオと呼ばれています。 (データストアの値は、クライアントによって送信された値よりも優先されます)。このチュートリアルでは、ストア Wins シナリオを実装します。 この手法では、変更が上書きされるとき、それが必ずユーザーに警告されます。

### <a name="detecting-concurrency-conflicts"></a>同時実行の競合の検出

Entity Framework がスローする[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx)例外を処理することで、競合を解決できます。 このような例外がスローされるタイミングを認識する目的で、Entity Framework は競合を検出できなければなりません。 そのため、データベースとデータ モデルを適宜構成する必要があります。 競合検出を有効にするためのオプションには次のようなものがあります。

- 行が変更されたタイミングを判断するトラッキング列をデータベース テーブルに追加します。 次に、SQL `Update` または `Delete` コマンドの `Where` 句にその列を含めるように Entity Framework を構成できます。

    追跡列のデータ型は、通常は[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)です。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)値は、行が更新されるたびにインクリメントされる連続番号です。 `Update` または `Delete` コマンドでは、`Where` 句に追跡列の元の値 (元の行バージョン) が含まれます。 更新対象の行が別のユーザーによって変更されている場合、`rowversion` 列の値は元の値とは異なるため、`Update` または `Delete` ステートメントは、`Where` 句が原因で更新する行を見つけることができません。 Entity Framework が、`Update` または `Delete` コマンドによって更新された行がないことを検出した場合 (つまり、影響を受ける行の数が0の場合)、同時実行の競合として解釈されます。
- Entity Framework を構成して、テーブル内のすべての列の元の値を、`Update` および `Delete` コマンドの `Where` 句に含めます。

    最初のオプションと同様に、行の最初の読み取り以降に行の内容が変更された場合、`Where` 句は更新する行を返しません。この場合、Entity Framework は同時実行の競合として解釈されます。 多数の列を含むデータベーステーブルでは、この方法によって非常に大きな `Where` 句が生成され、大量の状態を維持することが必要になる場合があります。 既に説明したように、大量の状態を維持すると、アプリケーションのパフォーマンスが低下する可能性があります。これは、サーバーリソースが必要であるか、または web ページ自体に含まれる必要があるためです。 このため、この方法は一般的に推奨されません。この方法は、このチュートリアルでは使用しません。

    このアプローチを同時実行に実装する場合は、 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)属性を追加することで、同時実行を追跡するエンティティのすべての非プライマリキープロパティをマークする必要があります。 この変更により、Entity Framework は `UPDATE` ステートメントの SQL `WHERE` 句にすべての列を含めることができます。

このチュートリアルの残りの部分では、 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tracking プロパティを `Department` エンティティに追加し、コントローラーとビューを作成して、すべてが正しく動作するかどうかをテストします。

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>Department エンティティにオプティミスティック同時実行制御プロパティを追加する

*Models\Department.cs*で、`RowVersion`という名前の追跡プロパティを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)属性は、この列が `Update` の `Where` 句と、データベースに送信される `Delete` コマンドに含まれることを指定します。 この属性は[timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)と呼ばれます。これは、以前のバージョンの SQL Server では、sql [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)によって置き換えられる前に sql [timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)データ型が使用されているためです。 `rowversion` の .Net 型はバイト配列です。 Fluent API を使用する場合は、次の例に示すように、 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)メソッドを使用して追跡プロパティを指定できます。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

GitHub の問題「 [IsConcurrencyToken By IsRowVersion](https://github.com/aspnet/AspNetDocs/issues/302)」を参照してください。

プロパティを追加し、データベース モデルを変更したので、別の移行を行う必要があります。 パッケージ マネージャー コンソール (PMC) で、次のコマンドを入力します。

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a>Department コントローラーを作成する

次の設定を使用して、他のコントローラーと同じように `Department` コントローラーとビューを作成します。

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

*Controllers\DepartmentController.cs*で、`using` ステートメントを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

このファイル内のすべての場所で "LastName" を "FullName" に変更します (4 回)。これにより、部門の管理者のドロップダウンリストには、姓だけではなく、インストラクターの完全な名前が含まれるようになります。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

`HttpPost` `Edit` メソッドの既存のコードを次のコードに置き換えます。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

ビューには、元の `RowVersion` 値が隠しフィールドに格納されます。 モデルバインダーが `department` インスタンスを作成すると、そのオブジェクトには、元の `RowVersion` プロパティ値と、ユーザーが編集ページで入力した他のプロパティの新しい値が設定されます。 Entity Framework によって SQL `UPDATE` コマンドが作成されると、そのコマンドには、元の `RowVersion` 値を持つ行を検索する `WHERE` 句が含まれます。

`UPDATE` コマンドの影響を受ける行がない場合 (元の `RowVersion` 値を持つ行は存在しません)、Entity Framework は `DbUpdateConcurrencyException` 例外をスローし、`catch` ブロック内のコードは、例外オブジェクトから影響を受ける `Department` エンティティを取得します。 このエンティティには、データベースから読み取られた値と、ユーザーによって入力された新しい値の両方があります。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

次に、ユーザーが編集ページで入力したものとは異なるデータベース値を持つ各列に対して、カスタムエラーメッセージを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

より長いエラーメッセージでは、何が起こったか、およびその対処方法が説明されています。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

最後に、`Department` オブジェクトの `RowVersion` 値を、データベースから取得した新しい値に設定します。 Edit ページが再表示されるとき、この新しい `RowVersion` 値が非表示フィールドに保存されます。今度ユーザーが **[保存]** をクリックすると、Edit ページの再表示後に発生したコンカレンシー エラーのみが取得されます。

*Views\Department\Edit.cshtml*で、`DepartmentID` プロパティの非表示フィールドの直後に `RowVersion` プロパティ値を保存する非表示フィールドを追加します。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

*Views\Department\Index.cshtml*で、既存のコードを次のコードに置き換えて、行のリンクを左に移動し、ページのタイトルと列の見出しを変更して、 **[管理者]** 列に `LastName` ではなく `FullName` を表示します。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a>オプティミスティック同時実行制御処理のテスト

サイトを実行し、 **[部門]** をクリックします。

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Kim Abercrombie の**編集**ハイパーリンクを右クリックし、[**新しいタブで開く]** を選択します。次に、Kim Abercrombie の **[編集]** ハイパーリンクをクリックします。 2つのウィンドウに同じ情報が表示されます。

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

最初のブラウザーウィンドウでフィールドを変更し、 **[保存]** をクリックします。

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

値が変更された Index ページがブラウザーに表示されます。

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

2番目のブラウザーウィンドウで任意のフィールドを変更し、 **[保存]** をクリックします。

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

2番目のブラウザーウィンドウで **[保存]** をクリックします。 エラー メッセージが表示されます。

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

**[保存]** を再びクリックします。 2番目のブラウザーで入力した値は、最初のブラウザーで変更したデータの元の値と共に保存されます。 Index ページが表示されると、保存した値を確認できます。

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>削除ページを更新しています

Delete ページの場合、Entity Framework は、同様の方法で部署を編集している他のユーザーが起こしたコンカレンシーの競合を検出します。 `HttpGet` の `Delete` メソッドで確認ビューが表示されると、ビューには、非表示フィールドに元の `RowVersion` 値が含まれます。 その値は、ユーザーが削除を確認したときに呼び出される `HttpPost` `Delete` メソッドで使用できます。 Entity Framework によって SQL `DELETE` コマンドが作成されると、元の `RowVersion` 値を持つ `WHERE` 句が含まれます。 コマンドによって影響を受ける行がゼロになる場合 (つまり、削除の確認ページが表示された後に行が変更された場合)、同時実行例外がスローされ、`HttpGet Delete` メソッドが呼び出されます。エラーフラグを `true` に設定すると、エラーメッセージと共に確認ページが再び表示されます。 また、行が別のユーザーによって削除されたために行が影響を受けていない可能性もあります。その場合、別のエラーメッセージが表示されます。

*DepartmentController.cs*で、`HttpGet` `Delete` メソッドを次のコードに置き換えます。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

このメソッドは、コンカレンシー エラー後にページが再表示されたかどうかを示すオプション パラメーターを受け取ります。 このフラグが `true`場合は、`ViewBag` プロパティを使用してエラーメッセージがビューに送信されます。

`HttpPost` `Delete` メソッド (名前付き `DeleteConfirmed`) 内のコードを次のコードに置き換えます。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

置き換えたスキャフォールディングされたコードで、このメソッドがレコード ID を 1 つだけ受け取りました。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

このパラメーターは、モデルバインダーによって作成された `Department` エンティティインスタンスに変更されました。 これにより、レコードキーに加えて `RowVersion` プロパティ値にアクセスできるようになります。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

また、アクション メソッドの名前を `DeleteConfirmed` から `Delete` に変更しています。 `HttpPost` `Delete` メソッドという名前のスキャフォールディングコードは、`HttpPost` メソッドに一意の署名を与える `DeleteConfirmed` ます。 (CLR では、オーバーロードされたメソッドで異なるメソッドパラメーターを持つ必要があります)。署名が一意であるため、MVC 規則を使用して、`HttpPost` と `HttpGet` delete メソッドに同じ名前を使用することができます。

コンカレンシー エラーがキャッチされた場合、このコードは削除確認ページを再表示し、コンカレンシー エラー メッセージを表示するかどうかを示すフラグを提供します。

*Views\Department\Delete.cshtml*で、スキャフォールディングコードをいくつかの書式設定を変更する次のコードに置き換えて、[エラーメッセージ] フィールドを追加します。 変更が強調表示されます。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

このコードは、`h2` と `h3` の見出しの間にエラーメッセージを追加します。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`LastName` は、`Administrator` フィールドの `FullName` に置き換えられます。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

最後に、`DepartmentID` および `RowVersion` プロパティの非表示フィールドを `Html.BeginForm` ステートメントの後に追加します。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

部門のインデックスページを実行します。 英語部署の **[削除]** ハイパーリンクを右クリックし、 **[新しいウィンドウで開く]** を選択します。次に、最初のウィンドウで、英語部門の **[編集]** ハイパーリンクをクリックします。

最初のウィンドウで値の1つを変更し、 **[保存]** をクリックします。

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

インデックスページによって変更が確認されます。

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

2番目のウィンドウで、 **[削除]** をクリックします。

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

コンカレンシー エラー メッセージが表示されます。Department 値がデータベースの現在の内容で更新されています。

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

**[削除]** をもう一度クリックすると、Index ページにリダイレクトされます。Index ページには、部署が削除されていることが表示されます。

## <a name="summary"></a>要約

コンカレンシーの競合処理の入門編はこれで終わりです。 さまざまな同時実行のシナリオを処理するその他の方法については、「[オプティミスティック同時実行制御パターン](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx)」と Entity Framework チームのブログの「[プロパティ値の操作](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx)」を参照してください。 次のチュートリアルでは、`Instructor` エンティティと `Student` エンティティに対して、階層構造の継承を実装する方法について説明します。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
