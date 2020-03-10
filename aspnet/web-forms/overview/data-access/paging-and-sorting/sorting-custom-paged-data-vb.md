---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
title: カスタムページングデータの並べ替え (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、web ページにデータを表示するときにカスタムページングを実装する方法について学習しました。 このチュートリアルでは、前の手順を拡張する方法について説明します。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 4823a186-caaf-4116-a318-c7ff4d955ddc
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 934c7558d907611732ae6f04c553bc9e295c569b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78501712"
---
# <a name="sorting-custom-paged-data-vb"></a>カスタム ページングを適用したデータを並べ替える (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_VB.exe)または[PDF のダウンロード](sorting-custom-paged-data-vb/_static/datatutorial26vb1.pdf)

> 前のチュートリアルでは、web ページにデータを表示するときにカスタムページングを実装する方法について学習しました。 このチュートリアルでは、前の例を拡張してカスタムページングの並べ替えをサポートする方法について説明します。

## <a name="introduction"></a>はじめに

既定のページングと比較すると、カスタムページングを使用すると、データによるページングのパフォーマンスをいくつかの程度向上させることができます。これにより、大量のデータをページングするときに、事実上ページングの実装をカスタマイズできます。 ただし、カスタムページングの実装は、特に並べ替えをミックスに追加する場合に、既定のページングを実装するよりも複雑です。 このチュートリアルでは、前の例の例を拡張して、並べ替え*と*カスタムページングのサポートを追加します。

> [!NOTE]
> このチュートリアルは前のチュートリアルに基づいているため、先に進む前に、前のチュートリアルの web ページ (`EfficientPaging.aspx`) の `<asp:Content>` 要素内の宣言構文をコピーし、`SortParameter.aspx` ページの `<asp:Content>` 要素の間に貼り付けます。 ASP.NET ページの機能を別のページにレプリケートする方法の詳細については、「[編集および挿入インターフェイスに検証コントロールを追加する](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)」の手順1を参照してください。

## <a name="step-1-reexamining-the-custom-paging-technique"></a>手順 1: カスタムページング手法を再検査する

カスタムページングを正常に動作させるには、開始行インデックスおよび最大行数パラメーターを指定して、特定のレコードのサブセットを効率的に取得できるいくつかの手法を実装する必要があります。 この目標を達成するために使用できる手法がいくつかあります。 前のチュートリアルでは、Microsoft SQL Server 2005 s new `ROW_NUMBER()` 順位付け関数を使用してこれを実現しました。 つまり、`ROW_NUMBER()` 順位付け関数は、指定された並べ替え順序によって順位付けされたクエリによって返される各行に行番号を割り当てます。 レコードの適切なサブセットを取得するには、番号付きの結果の特定のセクションを返します。 次のクエリは、この手法を使用して、結果をアルファベット順に順位付けするときに、`ProductName`によって数値が 11 ~ 20 の製品を返す方法を示しています。

[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample1.sql)]

この手法は、特定の並べ替え順序 (この場合はアルファベット順に並べ替え`ProductName`) を使用したページングに適していますが、別の並べ替え式で並べ替えられた結果を表示するようにクエリを変更する必要があります。 このクエリは、次のように `OVER` 句のパラメーターを使用するように書き換えることが理想的です。

[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample2.sql)]

残念ながら、パラメーター化された `ORDER BY` 句は使用できません。 代わりに、`@sortExpression` 入力パラメーターを受け取るストアドプロシージャを作成する必要がありますが、次のいずれかの回避策を使用します。

- 使用される可能性のある並べ替え式ごとに、ハードコーディングされたクエリを記述します。次に、`IF/ELSE` T-sql ステートメントを使用して、実行するクエリを決定します。
- `@sortExpressio` n 入力パラメーターに基づいて動的な `ORDER BY` 式を指定するには、`CASE` ステートメントを使用します。詳細については、「 [SQL `CASE` ステートメントの機能](http://www.4guysfromrolla.com/webtech/102704-1.shtml)」の「クエリ結果を動的に並べ替えるために使用する」を参照してください。
- ストアドプロシージャ内の文字列として適切なクエリを構築し、 [`sp_executesql` システムストアドプロシージャ](https://msdn.microsoft.com/library/ms188001.aspx)を使用して動的クエリを実行します。

これらの回避策にはいくつかの欠点があります。 1つ目のオプションは、考えられる各並べ替え式に対してクエリを作成する必要があるため、他の2つの方法ほど保守が容易ではありません。 したがって、後で並べ替え可能な新しいフィールドを GridView に追加する場合は、戻ってストアドプロシージャを更新する必要もあります。 2番目の方法には、文字列以外のデータベース列によって並べ替えを行うときにパフォーマンスに関する問題が発生し、1番目の方法と同じ保守容易性の問題が発生するという微妙な点があります。 また、動的 SQL を使用する3つ目の選択肢では、攻撃者が、選択した入力パラメーター値を渡してストアドプロシージャを実行できる場合、SQL インジェクション攻撃のリスクが生じます。

これらの方法は完全ではありませんが、3番目の方法が最も優れていると考えられます。 動的 SQL を使用することで、他の2つのレベルを柔軟に提供できます。 さらに、SQL インジェクション攻撃は、攻撃者が任意の入力パラメーターを渡してストアドプロシージャを実行できる場合にのみ、悪用される可能性があります。 DAL はパラメーター化クエリを使用するため、ADO.NET は、アーキテクチャを通じてデータベースに送信されるパラメーターを保護します。つまり、攻撃者がストアドプロシージャを直接実行できる場合にのみ、SQL インジェクション攻撃の脆弱性が存在します。

この機能を実装するには、`GetProductsPagedAndSorted`という名前の Northwind データベースに新しいストアドプロシージャを作成します。 このストアドプロシージャは、結果の並べ替え方法を指定する3つの入力パラメーター (`nvarchar(100`型の入力パラメーター) を受け取る必要があり `@sortExpression`ます。これは `OVER` 句の `ORDER BY` テキストの直後に挿入されます。および `@startRowIndex` と `@maximumRows`には、前のチュートリアルで検証した `GetProductsPaged` ストアドプロシージャと同じ2つの整数入力パラメーターがあります。 次のスクリプトを使用して、`GetProductsPagedAndSorted` ストアドプロシージャを作成します。

[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample3.sql)]

ストアドプロシージャは、最初に `@sortExpression` パラメーターの値が指定されていることを確認します。 指定されていない場合、結果は `ProductID`順に順位付けされます。 次に、動的 SQL クエリが作成されます。 ここでの動的 SQL クエリは、Products テーブルからすべての行を取得するために使用される前のクエリとは若干異なります。 前の例では、サブクエリを使用して、各製品に関連付けられているカテゴリと仕入先の名前を取得しました。 この決定は、[データアクセス層の作成](../introduction/creating-a-data-access-layer-vb.md)に関するチュートリアルで行ったもので、`JOIN` を使用する代わりに実行しました。このようなクエリに関連する insert、update、および delete メソッドを TableAdapter で自動的に作成することはできません。 ただし、`GetProductsPagedAndSorted` ストアドプロシージャでは、結果がカテゴリ名または仕入先名によって並べ替えられるために `JOIN` を使用する必要があります。

この動的クエリは、静的なクエリ部分と `@sortExpression`、`@startRowIndex`、および `@maximumRows` パラメーターを連結することによって構築されます。 `@startRowIndex` と `@maximumRows` は整数のパラメーターであるため、正しく連結されるためには、これらのパラメーターを nvarchars に変換する必要があります。 この動的 SQL クエリが構築されると、`sp_executesql`経由で実行されます。

`@sortExpression`、`@startRowIndex`、および `@maximumRows` パラメーターに対して異なる値を使用して、このストアドプロシージャをテストします。 サーバーエクスプローラーで、ストアドプロシージャ名を右クリックし、[実行] を選択します。 これにより、[ストアドプロシージャの実行] ダイアログボックスが表示されます。このダイアログボックスで、入力パラメーターを入力できます (図1を参照)。 カテゴリ名で結果を並べ替えるには、`@sortExpression` パラメーター値として [区分名] を使用します。仕入先の会社名で並べ替えるには、CompanyName を使用します。 パラメーターの値を指定したら、[OK] をクリックします。 結果が [出力] ウィンドウに表示されます。 図2は、`UnitPrice` によって降順に並べ替えられる場合に、11 ~ 20 の製品を返すと結果を示しています。

![ストアドプロシージャ s に異なる値を指定してください。3つの入力パラメーター](sorting-custom-paged-data-vb/_static/image1.png)

**図 1**: ストアドプロシージャ s の異なる値を使用する3つの入力パラメーター

[ストアドプロシージャの結果が ![出力ウィンドウに表示されます。](sorting-custom-paged-data-vb/_static/image3.png)](sorting-custom-paged-data-vb/_static/image2.png)

**図 2**: ストアドプロシージャの結果が出力ウィンドウに表示される ([クリックすると、フルサイズの画像が表示](sorting-custom-paged-data-vb/_static/image4.png)されます)

> [!NOTE]
> `OVER` 句の指定した `ORDER BY` 列によって結果を順位付けする場合、SQL Server は結果を並べ替える必要があります。 これは、結果が並べ替えられている列にクラスター化インデックスが存在する場合、またはカバリングインデックスがある場合はクイック操作ですが、それ以外の場合はコストが高くなります。 十分に大きなクエリのパフォーマンスを向上させるには、結果の並べ替えに使用する列に非クラスター化インデックスを追加することを検討してください。 詳細については[、SQL Server 2005 の順位付け関数とパフォーマンス](http://www.sql-server-performance.com/ak_ranking_functions.asp)に関する説明を参照してください。

## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>手順 2: データアクセスとビジネスロジック層を補強する

`GetProductsPagedAndSorted` ストアドプロシージャを作成したので、次の手順では、アプリケーションアーキテクチャを使用してストアドプロシージャを実行する手段を提供します。 これには、DAL と BLL の両方に適切なメソッドを追加する必要があります。 まず、DAL にメソッドを追加します。 `Northwind.xsd` 型指定されたデータセットを開き、`ProductsTableAdapter`を右クリックして、コンテキストメニューから [クエリの追加] オプションを選択します。 前のチュートリアルで行ったように、この新しい DAL メソッドを構成して既存のストアドプロシージャ (この場合は `GetProductsPagedAndSorted`) を使用する必要があります。 まず、新しい TableAdapter メソッドで既存のストアドプロシージャを使用することを指定します。

![既存のストアドプロシージャの使用を選択する](sorting-custom-paged-data-vb/_static/image5.png)

**図 3**: 既存のストアドプロシージャの使用を選択する

使用するストアドプロシージャを指定するには、次の画面のドロップダウンリストから `GetProductsPagedAndSorted` ストアドプロシージャを選択します。

![GetProductsPagedAndSorted ストアドプロシージャを使用する](sorting-custom-paged-data-vb/_static/image6.png)

**図 4**: GetProductsPagedAndSorted ストアドプロシージャを使用する

このストアドプロシージャは、一連のレコードを結果として返します。そのため、次の画面では、表形式のデータが返されることを示しています。

![ストアドプロシージャが表形式データを返すことを示します。](sorting-custom-paged-data-vb/_static/image7.png)

**図 5**: ストアドプロシージャが表形式データを返すことを示す

最後に、DataTable に Fill を使用し、DataTable パターンを返す DAL メソッドを作成します。これらのメソッドは、それぞれ `FillPagedAndSorted` と `GetProductsPagedAndSorted`に名前を付けます。

![メソッド名の選択](sorting-custom-paged-data-vb/_static/image8.png)

**図 6**: メソッド名を選択する

DAL を拡張したので、BLL に切り替える準備ができました。 `ProductsBLL` クラスファイルを開き、新しいメソッド `GetProductsPagedAndSorted`を追加します。 このメソッドでは、3つの入力パラメーター `sortExpression`、`startRowIndex`、および `maximumRows` を受け取る必要があります。また、次のように、単に DAL s `GetProductsPagedAndSorted` メソッドを呼び出す必要があります。

[!code-vb[Main](sorting-custom-paged-data-vb/samples/sample4.vb)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>手順 3: SortExpression パラメーターに渡す ObjectDataSource の構成

`GetProductsPagedAndSorted` ストアドプロシージャを利用するメソッドを含むように DAL と BLL を強化した後は、`SortParameter.aspx` ページで ObjectDataSource を構成して新しい BLL メソッドを使用し、ユーザーが結果を並べ替えるために要求した列に基づいて `SortExpression` パラメーターを渡す必要があります。

最初に、ObjectDataSource s `SelectMethod` を `GetProductsPaged` から `GetProductsPagedAndSorted`に変更します。 これは、データソースの構成ウィザード、プロパティウィンドウから、または宣言型の構文を使用して直接行うことができます。 次に、ObjectDataSource s [`SortParameterName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)の値を指定する必要があります。 このプロパティが設定されている場合、ObjectDataSource は GridView s `SortExpression` プロパティを `SelectMethod`に渡そうとします。 特に、ObjectDataSource は、`SortParameterName` プロパティの値と同じ名前を持つ入力パラメーターを検索します。 BLL s `GetProductsPagedAndSorted` メソッドには `sortExpression`という名前の並べ替え式の入力パラメーターがあるため、ObjectDataSource s `SortExpression` プロパティを sortExpression に設定します。

これらの2つの変更を行った後、ObjectDataSource s 宣言構文は次のようになります。

[!code-aspx[Main](sorting-custom-paged-data-vb/samples/sample5.aspx)]

> [!NOTE]
> 前のチュートリアルと同様に、ObjectDataSource には SelectParameters コレクションに sortExpression、startRowIndex、または maximumRows の入力パラメーターが含ま*れていない*ことを確認してください。

GridView で並べ替えを有効にするには、gridview s スマートタグの [並べ替えを有効にする] チェックボックスをオンにします。これにより、GridView s `AllowSorting` プロパティが `true` に設定され、各列のヘッダーテキストが LinkButton としてレンダリングされます。 エンドユーザーがヘッダーリンクボタンのいずれかをクリックすると、ポストバック ensues と次の手順が終了します。

1. GridView は、その[`SortExpression` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)を、ヘッダーリンクがクリックされたフィールドの `SortExpression` の値に更新します。
2. ObjectDataSource は、BLL s `GetProductsPagedAndSorted` メソッドを呼び出します。これには、GridView s `SortExpression` プロパティを、メソッド s `sortExpression` の入力パラメーターの値として渡します (適切な `startRowIndex` および `maximumRows` 入力パラメーター値と共に)。
3. BLL は、DAL の `GetProductsPagedAndSorted` メソッドを呼び出します。
4. DAL は `GetProductsPagedAndSorted` ストアドプロシージャを実行し、`@sortExpression` パラメーター (`@startRowIndex` および `@maximumRows` 入力パラメーター値と共に渡します。
5. このストアドプロシージャは、データの適切なサブセットを BLL に返します。これにより、データが ObjectDataSource に返されます。このデータは、GridView にバインドされ、HTML に表示され、エンドユーザーに送信されます。

図7に、`UnitPrice` によって昇順に並べ替えられた場合の結果の最初のページを示します。

[結果が UnitPrice によって並べ替えら ![](sorting-custom-paged-data-vb/_static/image10.png)](sorting-custom-paged-data-vb/_static/image9.png)

**図 7**: 結果が UnitPrice によって並べ替えられる ([クリックすると、フルサイズの画像が表示](sorting-custom-paged-data-vb/_static/image11.png)されます)

現在の実装では、製品名、カテゴリ名、数量/単位、および単価によって結果を正しく並べ替えることができますが、仕入先名によって結果を注文しようとすると、ランタイム例外が発生します (図8を参照)。

![仕入先によって結果を並べ替えようとすると、次のランタイム例外が発生します。](sorting-custom-paged-data-vb/_static/image12.png)

**図 8**: 仕入先によって結果を並べ替えようとすると、次のランタイム例外が発生する

この例外は、GridView `SupplierName` BoundField の `SortExpression` が `SupplierName`に設定されていることが原因で発生します。 ただし、`Suppliers` テーブルの仕入先の名前は、実際には `SupplierName`としてこの列名のエイリアスが `CompanyName` と呼ばれます。 ただし、`ROW_NUMBER()` 関数で使用される `OVER` 句は別名を使用できず、実際の列名を使用する必要があります。 したがって、`SupplierName` BoundField s `SortExpression` を SupplierName から CompanyName に変更します (図9を参照)。 図10に示すように、この変更を行うと、仕入先によって結果を並べ替えることができます。

![SupplierName BoundField s SortExpression を CompanyName に変更します。](sorting-custom-paged-data-vb/_static/image13.png)

**図 9**: SupplierName BoundField s SortExpression を CompanyName に変更する

[![結果を Supplier で並べ替えることができるようになりました](sorting-custom-paged-data-vb/_static/image15.png)](sorting-custom-paged-data-vb/_static/image14.png)

**図 10**: Supplier で結果を並べ替えることができる ([クリックすると、フルサイズの画像が表示](sorting-custom-paged-data-vb/_static/image16.png)されます)

## <a name="summary"></a>まとめ

前のチュートリアルで検証したカスタムページング実装では、デザイン時に結果の並べ替え順序を指定する必要がありました。 つまり、実装したカスタムページング実装は、並べ替え機能を提供することができなかったことを意味します。 このチュートリアルでは、最初からストアドプロシージャを拡張し、結果を並べ替えるための `@sortExpression` 入力パラメーターを含めることによって、この制限を克服しました。

このストアドプロシージャを作成し、DAL および BLL で新しいメソッドを作成した後、GridView を構成して、並べ替えとカスタムページングの両方を提供する GridView を実装できるようになりました。これにより、GridView の current `SortExpression` プロパティを BLL `SelectMethod`に渡すことができます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Carlos Santos でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](efficiently-paging-through-large-amounts-of-data-vb.md)
> [次へ](creating-a-customized-sorting-user-interface-vb.md)
