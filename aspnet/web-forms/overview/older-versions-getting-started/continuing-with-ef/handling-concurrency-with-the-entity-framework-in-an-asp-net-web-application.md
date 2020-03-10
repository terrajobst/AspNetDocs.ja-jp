---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 Web アプリケーションでの Entity Framework 4.0 での同時実行の処理Microsoft Docs
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework 4.0 チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513502"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 Web アプリケーションでの Entity Framework 4.0 での同時実行の処理

[Tom Dykstra](https://github.com/tdykstra)

> このチュートリアルシリーズは、 [Entity Framework 4.0 チュートリアルシリーズを使用](https://asp.net/entity-framework/tutorials#Getting%20Started)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。 チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。 チュートリアルについてご質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)に投稿することができます。

前のチュートリアルでは、`ObjectDataSource` コントロールと Entity Framework を使用してデータの並べ替えとフィルター処理を行う方法について学習しました。 このチュートリアルでは、Entity Framework を使用する ASP.NET web アプリケーションで同時実行を処理するためのオプションについて説明します。 講師のオフィスの割り当てを更新するための専用の新しい web ページを作成します。 このページと、前に作成した部門ページで同時実行の問題を処理します。

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>コンカレンシーの競合

同時実行の競合は、1人のユーザーがレコードを編集したときに、最初のユーザーの変更がデータベースに書き込まれる前に別のユーザーが同じレコードを編集したときに発生します。 このような競合を検出するように Entity Framework を設定しなかった場合、最後にデータベースを更新すると、その他のユーザーの変更が上書きされます。 多くのアプリケーションでは、このリスクが許容されるため、同時実行の競合を処理するようにアプリケーションを構成する必要はありません。 (ユーザー数が少ない場合、または更新プログラムがほとんどない場合、または一部の変更が上書きされても本当に重要でない場合は、同時実行のプログラミングのコストが利点を上回る可能性があります)。同時実行の競合について心配する必要がない場合は、このチュートリアルをスキップできます。このシリーズの残りの2つのチュートリアルは、この記事で作成したものに依存していません。

### <a name="pessimistic-concurrency-locking"></a>ペシミスティック同時実行 (ロック)

コンカレンシーで偶発的にデータが失われる事態をアプリケーションで回避する必要があれば、その方法としてデータベース ロックがあります。 これは、*ペシミスティック同時実行制御*と呼ばれます。 たとえば、データベースから行を読む前に、読み取り専用か更新アクセスでロックを要求します。 更新アクセスで行をロックすると、他のユーザーはその行を読み取り専用または更新アクセスでロックできなくなります。変更中のデータのコピーが与えられるためです。 読み取り専用で行をロックすると、他のユーザーはその行を読み取り専用でロックできますが、更新アクセスではロックできません。

ロックの管理にはいくつかの欠点があります。 プログラムが複雑になります。 多くのデータベース管理リソースが必要であり、アプリケーションのユーザー数が増えるにつれてパフォーマンスの問題が発生する可能性があります (つまり、スケールが適切ではありません)。 そのような理由から、一部のデータベース管理システムはペシミスティック コンカレンシーに対応していません。 Entity Framework には、組み込みのサポートはありません。このチュートリアルでは、実装方法については説明しません。

### <a name="optimistic-concurrency"></a>オプティミスティック コンカレンシー

ペシミスティック同時実行制御の代替として、*オプティミスティック同時実行制御*があります。 オプティミスティック コンカレンシーでは、コンカレンシーの競合の発生を許し、発生したら適切に対処します。 たとえば、John は、*学科の .aspx*ページを実行し、履歴部門の **[編集]** リンクをクリックして、**予算**の金額を $1000000.00 から $125000.00 に減らします。 (John は競争部門を管理しており、自分の部署の資金を解放する必要があります)。

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John が**Update**をクリックする前に、加藤さんは同じページを実行し、履歴部門の **[編集]** リンクをクリックして、 **[開始日]** フィールドを1/10/2011 から1/1/1999 に変更します。 (加藤さんは履歴部門を管理しており、より多くの勤続を提供したいと考えています)。

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

最初に **[update]** をクリックし、加藤さんは **[更新]** をクリックします。 Jane のブラウザーでは、**予算**の金額が $1000000.00 と表示されるようになりましたが、この金額は John から $125000.00 に変更されているため、正しくありません。

このシナリオで実行できる操作には、次のようなものがあります。

- ユーザーが変更したプロパティを追跡記録し、それに該当する列だけをデータベースで更新できます。 例のシナリオでは、2 人のユーザーが異なるプロパティを更新したため、データは失われません。 次にだれかが履歴部門を参照したときに、1/1/1999 と $125000.00 が表示されます。 

    これは Entity Framework の既定の動作であり、データの損失につながる可能性がある競合の数を大幅に減らすことができます。 ただし、この動作は、エンティティの同じプロパティに対して競合する変更が行われた場合に、データの損失を回避するものではありません。 また、この動作は常に可能であるとは限りません。ストアドプロシージャをエンティティ型にマップすると、エンティティに対する変更がデータベースで行われたときに、エンティティのすべてのプロパティが更新されます。
- 加藤さんの変更によって John の変更が上書きされるようにすることができます。 加藤さんが**Update**をクリックすると、**予算**の金額は $1000000.00 に戻ります。 これは *Client Wins* (クライアント側に合わせる) シナリオまたは *Last in Wins* (最終書き込み者優先) シナリオと呼ばれています。 (クライアントの値は、データストアの内容よりも優先されます)。
- Jane の変更がデータベースで更新されないようにすることができます。 通常は、エラーメッセージを表示して、データの現在の状態を表示し、それでも変更したい場合は自分の変更を再入力できるようにします。 さらに、入力を保存し、再入力することなく再適用する機会を与えることで、プロセスを自動化できます。 これは *Store Wins* (ストア側に合わせる) シナリオと呼ばれています。 (クライアントが送信した値よりデータストアの値が優先されます。)

### <a name="detecting-concurrency-conflicts"></a>同時実行の競合の検出

Entity Framework では、Entity Framework がスローする `OptimisticConcurrencyException` 例外を処理することで、競合を解決できます。 このような例外がスローされるタイミングを認識する目的で、Entity Framework は競合を検出できなければなりません。 そのため、データベースとデータ モデルを適宜構成する必要があります。 競合検出を有効にするためのオプションには次のようなものがあります。

- データベースで、行がいつ変更されたかを判断するために使用できるテーブル列を含めます。 次に、SQL `Update` または `Delete` コマンドの `Where` 句にその列を含めるように Entity Framework を構成できます。

    これは、`OfficeAssignment` テーブルの `Timestamp` 列の目的です。

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    `Timestamp` 列のデータ型は `Timestamp`とも呼ばれます。 ただし、列には実際には日付または時刻の値が含まれていません。 この値は、行が更新されるたびにインクリメントされる連続番号です。 `Update` または `Delete` コマンドでは、`Where` 句に元の `Timestamp` 値が含まれます。 更新対象の行が別のユーザーによって変更されている場合、`Timestamp` の値は元の値とは異なるため、`Where` 句は更新する行を返しません。 現在の `Update` または `Delete` コマンドによって更新された行がないことを Entity Framework が検出した場合 (つまり、影響を受ける行の数が0の場合)、同時実行の競合として解釈されます。
- Entity Framework を構成して、テーブル内のすべての列の元の値を、`Update` および `Delete` コマンドの `Where` 句に含めます。

    最初のオプションと同様に、行の最初の読み取り以降に行の内容が変更された場合、`Where` 句は更新する行を返しません。この場合、Entity Framework は同時実行の競合として解釈されます。 このメソッドは `Timestamp` フィールドを使用するのと同じように有効ですが、非効率的になる可能性があります。 多数の列を含むデータベーステーブルの場合は、非常に大きな `Where` 句になることがあります。また、web アプリケーションでは、大量の状態を維持することが必要になる場合があります。 大量の状態を維持すると、アプリケーションのパフォーマンスに影響を与える可能性があります。これは、サーバーリソース (セッション状態など) が必要であるか、web ページ自体に含まれる必要がある (たとえば、ビューステート) 必要があるためです。

このチュートリアルでは、追跡プロパティ (`Department` エンティティ) と、追跡プロパティ (`OfficeAssignment` エンティティ) を持つエンティティのオプティミスティック同時実行の競合に対するエラー処理を追加します。

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>追跡プロパティを使用せずにオプティミスティック同時実行制御を処理する

追跡 (`Timestamp`) プロパティを持たない `Department` エンティティに対してオプティミスティック同時実行制御を実装するには、次のタスクを実行します。

- `Department` エンティティの同時実行の追跡を有効にするようにデータモデルを変更します。
- `SchoolRepository` クラスで、`SaveChanges` メソッドの同時実行例外を処理します。
- Department ページで、試行された変更が失敗したことを示すメッセージをユーザーに表示して、同時実行例外を処理*します。* ユーザーは現在の値を確認し、必要に応じて変更を再試行することができます。

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>データモデルでの同時実行追跡の有効化

Visual Studio で、このシリーズの前のチュートリアルで使用していた Contoso 大学 web アプリケーションを開きます。

*SchoolModel*を開き、データモデルデザイナーで `Department` エンティティ内の `Name` プロパティを右クリックし、 **[プロパティ]** をクリックします。 **プロパティ** ウィンドウで、`ConcurrencyMode` プロパティを `Fixed`に変更します。

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

その他の非主キースカラープロパティ (`Budget`、`StartDate`、および `Administrator`に対しても同じ操作を行います。(ナビゲーションプロパティに対してこれを行うことはできません)。これにより、Entity Framework が `Update` または `Delete` SQL コマンドを生成してデータベースの `Department` エンティティを更新するときに、これらの列 (元の値を含む) を `Where` 句に含める必要があることを指定します。 `Update` または `Delete` コマンドの実行時に行が見つからない場合、Entity Framework はオプティミスティック同時実行例外をスローします。

データモデルを保存して閉じます。

### <a name="handling-concurrency-exceptions-in-the-dal"></a>DAL での同時実行例外の処理

*SchoolRepository.cs*を開き、`System.Data` 名前空間に対して次の `using` ステートメントを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

オプティミスティック同時実行例外を処理する次の新しい `SaveChanges` メソッドを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

このメソッドが呼び出されたときに同時実行エラーが発生した場合、メモリ内のエンティティのプロパティ値は、現在データベース内にある値に置き換えられます。 Web ページが処理できるように、同時実行の例外が再スローされます。

`DeleteDepartment` メソッドと `UpdateDepartment` メソッドで、新しいメソッドを呼び出すために、`context.SaveChanges()` の既存の呼び出しを `SaveChanges()` への呼び出しに置き換えます。

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>プレゼンテーション層での同時実行例外の処理

Department *.aspx*を開き、`OnDeleted="DepartmentsObjectDataSource_Deleted"` 属性を `DepartmentsObjectDataSource` コントロールに追加します。 コントロールの開始タグは、次の例のようになります。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

次の例に示すように、`DepartmentsGridView` コントロールで、`DataKeyNames` 属性のすべてのテーブル列を指定します。 これにより、非常に大きなビューステートフィールドが作成されることに注意してください。これは、通常、追跡フィールドを使用して同時実行の競合を追跡する方法として推奨される理由の1つです。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

*Departments.aspx.cs*を開き、`System.Data` 名前空間に対して次の `using` ステートメントを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

次の新しいメソッドを追加します。このメソッドは、データソースコントロールの `Updated` から呼び出され、同時実行例外を処理するためのイベントハンドラーを `Deleted` します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

このコードは、例外の種類を確認します。同時実行例外の場合、コードは動的に `CustomValidator` コントロールを作成し、`ValidationSummary` コントロールにメッセージを表示します。

先ほど追加した `Updated` イベントハンドラーから新しいメソッドを呼び出します。 また、同じメソッドを呼び出す新しい `Deleted` イベントハンドラーを作成します (それ以外は何も実行しません)。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>[部門] ページでオプティミスティック同時実行制御をテストする

Department *. .aspx*ページを実行します。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

行の **[編集]** をクリックし、 **[予算]** 列の値を変更します。 (既存の `School` データベースレコードに無効なデータが含まれているため、このチュートリアルで作成したレコードのみを編集できます。 経済部門のレコードは、試してみるのに安全です。)

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

新しいブラウザーウィンドウを開き、再度ページを実行します (最初のブラウザーウィンドウの [アドレス] ボックスから2番目のブラウザーウィンドウに URL をコピーします)。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

前に編集したものと同じ行の **[編集]** をクリックし、**予算**の値を別の値に変更します。

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

2番目のブラウザーウィンドウで、 **[更新]** をクリックします。 **予算**金額は、この新しい値に正常に変更されました。

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

最初のブラウザーウィンドウで、 **[更新]** をクリックします。 更新は失敗します。 2番目のブラウザーウィンドウで設定した値を使用して**予算**金額が再表示され、エラーメッセージが表示されます。

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>追跡プロパティを使用したオプティミスティック同時実行制御の処理

Tracking プロパティを持つエンティティのオプティミスティック同時実行制御を処理するには、次のタスクを実行します。

- `OfficeAssignment` エンティティを管理するためのストアドプロシージャをデータモデルに追加します。 (追跡のプロパティとストアドプロシージャを一緒に使用する必要はありません。これらは、ここでは説明のためにグループ化されています)。
- Dal に CRUD メソッドを追加し、DAL でオプティミスティック同時実行例外を処理するコードを含む `OfficeAssignment` エンティティの BLL を追加します。
- Office の割り当て web ページを作成します。
- 新しい web ページでオプティミスティック同時実行制御をテストします。

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>データモデルへの OfficeAssignment ストアドプロシージャの追加

モデルデザイナーで*SchoolModel*ファイルを開き、デザイン画面を右クリックして、 **[データベースからモデルを更新]** をクリックします。 **[データベースオブジェクトの選択]** ダイアログボックスの **[追加]** タブで、 **[ストアドプロシージャ]** を展開し、3つの `OfficeAssignment` ストアドプロシージャ (次のスクリーンショットを参照) を選択して、 **[完了]** をクリックします。 (これらのストアドプロシージャは、スクリプトを使用してダウンロードまたは作成したときにデータベースに既に存在していました)。

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

`OfficeAssignment` エンティティを右クリックし、 **[ストアドプロシージャマッピング]** を選択します。

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

対応するストアドプロシージャを使用するように、 **Insert**、 **Update**、および**Delete**の各関数を設定します。 `Update` 関数の `OrigTimestamp` パラメーターについては、**プロパティ**を `Timestamp` に設定し、[**元の値を使用**する] オプションを選択します。

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

Entity Framework が `UpdateOfficeAssignment` ストアドプロシージャを呼び出すと、`OrigTimestamp` パラメーターの `Timestamp` 列の元の値が渡されます。 ストアドプロシージャは、`Where` 句でこのパラメーターを使用します。

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

また、このストアドプロシージャでは、更新後の `Timestamp` 列の新しい値も選択されるため、Entity Framework はメモリ内の `OfficeAssignment` エンティティを対応するデータベース行と同期させることができます。

(オフィスの割り当てを削除するストアドプロシージャには、`OrigTimestamp` パラメーターがありません。 このため、Entity Framework でエンティティが変更されていないことを確認してから削除することはできません)。

データモデルを保存して閉じます。

### <a name="adding-officeassignment-methods-to-the-dal"></a>DAL に OfficeAssignment メソッドを追加する

*ISchoolRepository.cs*を開き、`OfficeAssignment` エンティティセットに対して次の CRUD メソッドを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

次の新しいメソッドを*SchoolRepository.cs*に追加します。 `UpdateOfficeAssignment` メソッドでは、`context.SaveChanges`ではなく、ローカルの `SaveChanges` メソッドを呼び出します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

テストプロジェクトで*MockSchoolRepository.cs*を開き、次の `OfficeAssignment` collection メソッドと CRUD メソッドをそれに追加します。 (モックリポジトリは、リポジトリインターフェイスを実装する必要があります。そうでない場合、ソリューションはコンパイルされません)。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>BLL に OfficeAssignment メソッドを追加する

メインプロジェクトで*SchoolBL.cs*を開き、`OfficeAssignment` エンティティセットに対して次の CRUD メソッドを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>OfficeAssignments Web ページの作成

*.Master*マスターページを使用する新しい web ページを作成し、「 *officeassignments*」という名前を指定します。 `Content2`という名前の `Content` コントロールに次のマークアップを追加します。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

`DataKeyNames` 属性では、マークアップによって、`Timestamp` プロパティとレコードキー (`InstructorID`) が指定されていることに注意してください。 `DataKeyNames` 属性でプロパティを指定すると、コントロールはコントロールの状態 (ビューステートに似ています) に保存します。これにより、ポストバック処理中に元の値を使用できるようになります。

`Timestamp` の値を保存していない場合、Entity Framework では、SQL `Update` コマンドの `Where` 句の値は使用できません。 そのため、何も更新する必要はありません。 その結果、`OfficeAssignment` エンティティが更新されるたびに、Entity Framework はオプティミスティック同時実行例外をスローします。

*OfficeAssignments.aspx.cs*を開き、データアクセス層の次の `using` ステートメントを追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

次の `Page_Init` メソッドを追加します。これにより、動的データ機能が有効になります。 同時実行エラーを確認するために、`ObjectDataSource` コントロールの `Updated` イベントの次のハンドラーも追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>[OfficeAssignments] ページでオプティミスティック同時実行制御をテストする

*Officeassignments .aspx*ページを実行します。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

行の **[編集]** をクリックし、 **[場所]** 列の値を変更します。

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

新しいブラウザーウィンドウを開き、再度ページを実行します (最初のブラウザーウィンドウから2番目のブラウザーウィンドウに URL をコピーします)。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

前に編集した同じ行の **[編集]** をクリックし、 **[場所]** の値を別の値に変更します。

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

2番目のブラウザーウィンドウで、 **[更新]** をクリックします。

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

最初のブラウザーウィンドウに切り替えて、 **[更新]** をクリックします。

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

エラーメッセージが表示され、 **[場所]** の値が更新され、2番目のブラウザーウィンドウで変更した値が表示されます。

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>EntityDataSource コントロールでの同時実行の処理

`EntityDataSource` コントロールには、データモデルの同時実行設定を認識し、それに応じて更新操作と削除操作を処理する組み込みのロジックが含まれています。 ただし、すべての例外と同様に、ユーザーにわかりやすいエラーメッセージを提供するために、`OptimisticConcurrencyException` 例外を自分で処理する必要があります。

次に、更新操作と削除操作を許可し、同時実行の競合が発生した場合にエラーメッセージを表示するために、(`EntityDataSource` コントロールを使用する) *course ページを*構成します。 `Course` エンティティには、同時実行追跡列がないため、`Department` エンティティで行ったのと同じメソッドを使用します。すべての非キープロパティの値を追跡します。

*SchoolModel*ファイルを開きます。 `Course` エンティティ (`Title`、`Credits`、および `DepartmentID`) の非キープロパティについては、 **Concurrency Mode**プロパティを `Fixed`に設定します。 次に、データモデルを保存して閉じます。

[Course *] ページを開き*、次のように変更します。

- `CoursesEntityDataSource` コントロールで、`EnableUpdate="true"` 属性と `EnableDelete="true"` 属性を追加します。 そのコントロールの開始タグは、次の例のようになります。

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- `CoursesGridView` コントロールで、`DataKeyNames` 属性の値を `"CourseID,Title,Credits,DepartmentID"`に変更します。 次に、 **[編集]** ボタンと **[削除]** ボタン (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`) を表示する `Columns` 要素に `CommandField` 要素を追加します。 `GridView` コントロールは、次の例のようになります。

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

ページを実行し、[部門] ページで行ったのと同じように競合状態を作成します。 2つのブラウザーウィンドウでページを実行し、各ウィンドウで同じ行の **[編集]** をクリックして、それぞれに異なる変更を加えます。 1つのウィンドウで **[更新]** をクリックし、その他のウィンドウで **[更新]** をクリックします。 **[更新]** をクリックすると、未処理の同時実行例外の結果として発生するエラーページが表示されます。

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

このエラーは、`ObjectDataSource` コントロールの処理方法と非常によく似た方法で処理されます。 *[Course] ページを*開き、`CoursesEntityDataSource` コントロールで、`Deleted` イベントと `Updated` イベントのハンドラーを指定します。 コントロールの開始タグは、次の例のようになります。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

`CoursesGridView` コントロールの前に、次の `ValidationSummary` コントロールを追加します。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

*Courses.aspx.cs*で、`System.Data` 名前空間の `using` ステートメントを追加し、同時実行例外をチェックするメソッドを追加して、`EntityDataSource` コントロールの `Updated` および `Deleted` ハンドラーのハンドラーを追加します。 コードは次のようになります。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

このコードと `ObjectDataSource` コントロールの唯一の違いは、この場合の同時実行例外は、その例外の `InnerException` プロパティではなく、イベント引数オブジェクトの `Exception` プロパティにあるという点です。

ページを実行し、同時実行の競合を再度作成します。 今度は、次のエラーメッセージが表示できます。

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

コンカレンシーの競合処理の入門編はこれで終わりです。 次のチュートリアルでは、Entity Framework を使用する web アプリケーションのパフォーマンスを向上させる方法について説明します。

> [!div class="step-by-step"]
> [前へ](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [次へ](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
