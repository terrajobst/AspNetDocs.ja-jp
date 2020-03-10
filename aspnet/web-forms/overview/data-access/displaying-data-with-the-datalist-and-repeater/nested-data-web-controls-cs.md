---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
title: 入れ子になったデータC#Web コントロール () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、別のリピータ内に入れ子になっているリピータを使用する方法について説明します。 例では、内部リピータを設定する方法について説明します。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: ad3cb0ec-26cf-42d7-b81b-184a34ec9f86
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8ef15bebb2c29976274b0cca1d6ace434ccc55ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481270"
---
# <a name="nested-data-web-controls-c"></a>入れ子になったデータ Web コントロール (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_CS.exe)または[PDF のダウンロード](nested-data-web-controls-cs/_static/datatutorial32cs1.pdf)

> このチュートリアルでは、別のリピータ内に入れ子になっているリピータを使用する方法について説明します。 これらの例では、内部リピータを宣言的およびプログラムによって設定する方法を示します。

## <a name="introduction"></a>はじめに

HTML およびデータバインドの静的な構文に加えて、テンプレートには Web コントロールやユーザーコントロールを含めることもできます。 これらの Web コントロールは、宣言型、データバインド構文、または適切なサーバー側イベントハンドラーでプログラムによってアクセスできるプロパティを持つことができます。

テンプレート内にコントロールを埋め込むことで、の外観とユーザーエクスペリエンスをカスタマイズおよび改善できます。 たとえば、 [Gridview コントロールのチュートリアルで使用している TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)のチュートリアルでは、TemplateField に Calendar コントロールを追加して、従業員の雇用日を示すように gridview の表示をカスタマイズする方法を説明しました。「[編集および挿入インターフェイスに検証コントロールを追加する](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)」および「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)」チュートリアルでは、検証コントロール、テキストボックス、dropdownlists、およびその他の Web コントロールを追加して、編集および挿入インターフェイスをカスタマイズする方法を説明しました。

テンプレートには、他のデータ Web コントロールを含めることもできます。 つまり、テンプレート内に別の DataList (または Repeater、GridView または DetailsView など) を含む DataList を設定できます。 このようなインターフェイスの課題は、内部データ Web コントロールに適切なデータをバインドすることです。 ObjectDataSource を使用する宣言型オプションからプログラム別の方法まで、いくつかの異なる方法を使用できます。

このチュートリアルでは、別のリピータ内に入れ子になっているリピータを使用する方法について説明します。 外部リピータには、データベース内のカテゴリごとに1つの項目が含まれ、カテゴリの名前と説明が表示されます。 各カテゴリ項目の内部リピータには、そのカテゴリに属する各製品の情報 (図1を参照) が箇条書きで表示されます。 この例では、内部リピータを宣言的およびプログラムによって設定する方法について説明します。

[各カテゴリとその製品が ![一覧表示されます。](nested-data-web-controls-cs/_static/image2.png)](nested-data-web-controls-cs/_static/image1.png)

**図 1**: 各カテゴリとその製品が一覧表示されます ([クリックすると、フルサイズの画像が表示](nested-data-web-controls-cs/_static/image3.png)されます)

## <a name="step-1-creating-the-category-listing"></a>手順 1: カテゴリの一覧を作成する

入れ子になったデータ Web コントロールを使用するページを構築する場合、入れ子になった内側のコントロールを気にすることなく、最も外側のデータ Web コントロールを設計、作成、およびテストすると便利です。 そのため、まず、各カテゴリの名前と説明を一覧表示する Repeater をページに追加するために必要な手順について説明します。

まず、`DataListRepeaterBasics` フォルダーの `NestedControls.aspx` ページを開き、Repeater コントロールをページに追加します。その `ID` プロパティを `CategoryList`に設定します。 Repeater s スマートタグから、`CategoriesDataSource`という名前の新しい ObjectDataSource を作成することを選択します。

[新しい ObjectDataSource カテゴリデータソースに名前を ![](nested-data-web-controls-cs/_static/image5.png)](nested-data-web-controls-cs/_static/image4.png)

**図 2**: 新しい ObjectDataSource `CategoriesDataSource` に名前[を指定する (クリックすると、フルサイズの画像が表示](nested-data-web-controls-cs/_static/image6.png)されます)

`CategoriesBLL` クラス s `GetCategories` メソッドからデータをプルするように ObjectDataSource を構成します。

[GetCategories メソッドを使用するように ObjectDataSource を構成 ![](nested-data-web-controls-cs/_static/image8.png)](nested-data-web-controls-cs/_static/image7.png)

**図 3**: `CategoriesBLL` クラス s `GetCategories` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](nested-data-web-controls-cs/_static/image9.png))

Repeater テンプレートの内容を指定するには、ソースビューにアクセスし、宣言型の構文を手動で入力する必要があります。 `<h4>` 要素にカテゴリ名を表示する `ItemTemplate` と、段落要素 (`<p>`) のカテゴリの説明を追加します。 さらに、各カテゴリを水平方向のルール (`<hr>`) で区切ることができます。 これらの変更を行った後、ページには、次のようなリピータおよび ObjectDataSource の宣言構文が含まれている必要があります。

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample1.aspx)]

図4は、ブラウザーを使用して表示したときの進行状況を示しています。

[各カテゴリの名前と説明が、水平方向のルールで区切られた ![ます。](nested-data-web-controls-cs/_static/image11.png)](nested-data-web-controls-cs/_static/image10.png)

**図 4**: 各カテゴリの名前と説明は、水平方向のルールで区切られて表示されます ([クリックすると、フルサイズの画像が表示](nested-data-web-controls-cs/_static/image12.png)されます)

## <a name="step-2-adding-the-nested-product-repeater"></a>手順 2: 入れ子になった製品リピータを追加する

カテゴリの一覧が完成したら、次に、適切なカテゴリに属する製品に関する情報を表示するリピータを `CategoryList` s `ItemTemplate` に追加します。 この内部リピータのデータを取得するには、次の2つの方法があります。 ここでは、`CategoryList` リピータ s `ItemTemplate`内に製品のリピータを作成するだけです。 具体的には、製品リピータに各製品の名前と価格を含む箇条書きのリストを表示します。

このリピータを作成するには、内部リピータの宣言構文とテンプレートを `CategoryList` s `ItemTemplate`に手動で入力する必要があります。 `CategoryList` リピータ s `ItemTemplate`内に次のマークアップを追加します。

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>手順 3: カテゴリ固有の製品を製品 Bycategory リストリピータにバインドする

この時点でブラウザーを使用してページにアクセスすると、図4のような画面が表示されます。これは、データをリピータにバインドする処理がまだ完了していないためです。 適切な製品レコードを取得してリピータにバインドするには、いくつかの方法がありますが、他の方法よりも効率的です。 ここでの主な課題は、指定されたカテゴリの適切な製品を取得することです。

内部リピータコントロールにバインドするデータは、ASP.NET ページの分離コードページから、`CategoryList` リピータ s `ItemTemplate`の ObjectDataSource、またはプログラムによって、宣言によってアクセスできます。 同様に、このデータは内部リピータの `DataSourceID` プロパティを介して宣言によって、または宣言型のデータバインディング構文を介して内部リピータにバインドすることもできます。また、`CategoryList` リピータ s `ItemDataBound` イベントハンドラーの内部リピータを参照し、プログラムによって `DataSource` プロパティを設定し、その `DataBind()` メソッドを呼び出すことによって、プログラムでバインドする では、これらの各アプローチについて説明します。

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>ObjectDataSource コントロールと`ItemDataBound`イベントハンドラーを使用したデータへの宣言によるアクセス

このチュートリアルシリーズでは ObjectDataSource を多用しているため、この例のデータにアクセスする最も自然な選択肢は、ObjectDataSource を使用することです。 `ProductsBLL` クラスには、指定された *`categoryID`* に属する製品に関する情報を返す `GetProductsByCategoryID(categoryID)` メソッドがあります。 したがって、ObjectDataSource を `CategoryList` リピータ s `ItemTemplate` に追加し、このクラスのメソッドからそのデータにアクセスするように構成することができます。

残念ながら、リピータはデザインビューによるテンプレートの編集を許可しないため、この ObjectDataSource コントロールの宣言構文を手動で追加する必要があります。 次の構文は、この新しい ObjectDataSource (`ProductsByCategoryDataSource`) を追加した後の `CategoryList` リピータ `ItemTemplate` を示しています。

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample3.aspx)]

ObjectDataSource アプローチを使用する場合は、`ProductsByCategoryList` リピータ s `DataSourceID` プロパティを ObjectDataSource (`ProductsByCategoryDataSource`) の `ID` に設定する必要があります。 また、ObjectDataSource には、`GetProductsByCategoryID(categoryID)` メソッドに渡される *`categoryID`* 値を指定する `<asp:Parameter>` 要素が含まれていることに注意してください。 しかし、どのようにしてこの値を指定するのでしょうか。 次のように、データバインディング構文を使用して、`<asp:Parameter>` 要素の `DefaultValue` プロパティを設定するのが理想的です。

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample4.aspx)]

残念ながら、databinding 構文は、`DataBinding` イベントを持つコントロールでのみ有効です。 `Parameter` クラスにはこのようなイベントがないため、上記の構文は無効であり、実行時エラーが発生します。

この値を設定するには、`CategoryList` リピータ s `ItemDataBound` イベントのイベントハンドラーを作成する必要があります。 `ItemDataBound` イベントは、リピータにバインドされている項目ごとに1回発生することを思い出してください。 このため、外部リピータに対してこのイベントが発生するたびに、現在の `CategoryID` 値を `ProductsByCategoryDataSource` ObjectDataSource s `CategoryID` パラメーターに割り当てることができます。

次のコードを使用して、`CategoryList` Repeater s `ItemDataBound` イベントのイベントハンドラーを作成します。

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample5.cs)]

このイベントハンドラーは、ヘッダー、フッター、または区切り記号の項目ではなく、データ項目を処理していることを確認してから開始します。 次に、現在の `RepeaterItem`にバインドされたばかりの実際の `CategoriesRow` インスタンスを参照します。 最後に、`ItemTemplate` の ObjectDataSource を参照し、その `CategoryID` パラメーター値を現在の `RepeaterItem`の `CategoryID` に割り当てます。

このイベントハンドラーを使用すると、各 `RepeaterItem` の `ProductsByCategoryList` リピータは `RepeaterItem` s カテゴリの製品にバインドされます。 図5に、結果の出力のスクリーンショットを示します。

[外部リピータを ![すると、各カテゴリが一覧表示されます。内部1つには、そのカテゴリの製品が一覧表示されます。](nested-data-web-controls-cs/_static/image14.png)](nested-data-web-controls-cs/_static/image13.png)

**図 5**: 外部リピータが各カテゴリを一覧表示する内側の1つは、そのカテゴリの製品を一覧表示します ([クリックすると、フルサイズの画像が表示](nested-data-web-controls-cs/_static/image15.png)されます)

## <a name="accessing-the-products-by-category-data-programmatically"></a>プログラムによるカテゴリデータによる製品へのアクセス

ObjectDataSource を使用して現在のカテゴリの製品を取得する代わりに、ASP.NET ページの分離コードクラス (または `App_Code` フォルダーまたは別のクラスライブラリプロジェクト) にメソッドを作成して、`CategoryID`に渡されたときに適切な製品セットを返すことができます。 たとえば、ASP.NET ページの分離コードクラスにこのようなメソッドがあり、`GetProductsInCategory(categoryID)`という名前が付けられているとします。 このメソッドを使用すると、次の宣言型構文を使用して、現在のカテゴリの製品を内部リピータにバインドできます。

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample6.aspx)]

Repeater s `DataSource` プロパティは、データが `GetProductsInCategory(categoryID)` メソッドから取得されることを示すために、databinding 構文を使用します。 `Eval("CategoryID")` は `Object`型の値を返すため、オブジェクトを `GetProductsInCategory(categoryID)` メソッドに渡す前に `Integer` にキャストします。 ここでは、データバインド構文を使用してアクセス `CategoryID` は、*外部*リピータ (`CategoryList`) の `CategoryID` であり、`Categories` テーブル内のレコードにバインドされていることに注意してください。 このため、`CategoryID` をデータベースの `NULL` 値にすることはできません。そのため、`DBNull`を処理するかどうかを確認せずに `Eval` メソッドを無条件にキャストできます。

この方法では、`GetProductsInCategory(categoryID)` メソッドを作成し、指定された *`categoryID`* に応じて適切な製品セットを取得する必要があります。 これを行うには、`ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドによって返された `ProductsDataTable` を返すだけです。 `NestedControls.aspx` ページの分離コードクラスに `GetProductsInCategory(categoryID)` メソッドを作成してみましょう。 これを行うには、次のコードを使用します。

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample7.cs)]

このメソッドは、単に `ProductsBLL` メソッドのインスタンスを作成し、`GetProductsByCategoryID(categoryID)` メソッドの結果を返します。 メソッドは `Public` または `Protected`としてマークされている必要があることに注意してください。メソッドが `Private`としてマークされている場合、ASP.NET ページ s の宣言マークアップからアクセスすることはできません。

この新しい手法を使用するようにこれらの変更を行った後は、ブラウザーでページを表示してみてください。 ObjectDataSource および `ItemDataBound` イベントハンドラーアプローチを使用する場合、出力は出力と同じである必要があります (図5を参照して、スクリーンショットを参照してください)。

> [!NOTE]
> Busywork のように、ASP.NET ページの分離コードクラスに `GetProductsInCategory(categoryID)` メソッドを作成するように思われるかもしれません。 結局のところ、このメソッドは単に `ProductsBLL` クラスのインスタンスを作成し、その `GetProductsByCategoryID(categoryID)` メソッドの結果を返します。 次のように、内部リピータの databinding 構文からこのメソッドを直接呼び出すのではないのでしょうか。たとえば、`DataSource='<%# ProductsBLL.GetProductsByCategoryID((int)(Eval("CategoryID"))) %>'`? この構文は `ProductsBLL` クラスの現在の実装では機能しませんが (`GetProductsByCategoryID(categoryID)` メソッドはインスタンスメソッドであるため)、静的 `GetProductsByCategoryID(categoryID)` メソッドを含めるように `ProductsBLL` を変更するか、`Instance()` クラスの新しいインスタンスを返す静的 `ProductsBLL` メソッドをクラスに含めることができます。

このような変更によって、ASP.NET ページの分離コードクラスの `GetProductsInCategory(categoryID)` メソッドが不要になりますが、コードビハインドクラスのメソッドを使用すると、すぐにわかるように、取得したデータをより柔軟に操作できます。

## <a name="retrieving-all-of-the-product-information-at-once"></a>すべての製品情報を一度に取得する

以前の2つの手法では、`ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを呼び出すことによって、現在のカテゴリのこれらの製品を取得します (最初の方法では、ObjectDataSource を通じて、2番目にコードビハインドクラスの `GetProductsInCategory(categoryID)` メソッドを使用します)。 このメソッドが呼び出されるたびに、ビジネスロジック層はデータアクセス層を呼び出します。この層は、指定された入力パラメーターと一致する `CategoryID` フィールドを持つ `Products` テーブルから行を返す SQL ステートメントを使用してデータベースにクエリを実行します。

システムで*n 個*のカテゴリが指定されている場合、この方法では、データベースの1つのクエリを呼び出してすべてのカテゴリを取得し、 *N*を呼び出して各カテゴリに固有の製品を取得します。 ただし、2つのデータベースのすべての必要なデータを取得して、すべてのカテゴリを取得するために1回の呼び出しを呼び出し、他のすべての製品を取得することができます。 すべての製品を用意したら、現在の `CategoryID` に一致する製品のみがそのカテゴリの内部リピータにバインドされるように、これらの製品をフィルター処理できます。

この機能を提供するには、ASP.NET ページの分離コードクラスの `GetProductsInCategory(categoryID)` メソッドにわずかな変更を加えるだけで済みます。 `ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドの結果を無条件に返すのではなく、最初に*すべて*の製品 (まだアクセスされていない場合) にアクセスし、渡された `CategoryID`に基づいて、製品のフィルターされたビューだけを返すことができます。

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample8.cs)]

ページレベル変数 `allProducts`の追加に注意してください。 これは、すべての製品に関する情報を保持し、`GetProductsInCategory(categoryID)` メソッドが初めて呼び出されたときに設定されます。 `allProducts` オブジェクトが作成および設定されたことを確認した後、メソッドは DataTable の結果をフィルター処理して、指定した `CategoryID` に一致する `CategoryID` を持つ行だけがアクセス可能になるようにします。 この方法により、データベースへのアクセス回数が*N* + 1 から2に減ります。

この拡張機能では、ページの表示されるマークアップに変更が加えられることはなく、他の方法よりも少数のレコードが返されることもありません。 単にデータベースへの呼び出しの回数を減らします。

> [!NOTE]
> 直感的な理由の1つは、データベースアクセスの数を減らすことで、パフォーマンスが確実に向上することです。 ただし、そうでない場合もあります。 たとえば、`CategoryID` が `NULL`されている多数の製品がある場合、`GetProducts` メソッドを呼び出すと、表示されない複数の製品が返されます。 さらに、カテゴリのサブセットのみを表示する場合は、すべての製品を返すことが無駄になる可能性があります。これは、ページングを実装している場合に当てはまります。

常に、2つの手法のパフォーマンスを分析する場合、唯一の surefire メジャーは、アプリケーションの一般的なケースシナリオに合わせて調整された制御されたテストを実行することです。

## <a name="summary"></a>まとめ

このチュートリアルでは、1つのデータ Web コントロールを別のデータ Web コントロールに入れ子にする方法を説明しました。具体的には、外部リピータが各カテゴリの項目を表示する方法について説明します。具体的には、各カテゴリの製品を箇条書きリストに一覧表示します。 入れ子になったユーザーインターフェイスを構築する際の主な課題は、にアクセスして、正しいデータを内部データ Web コントロールにバインドすることです。 このチュートリアルでは、次の2つの方法を使用できます。 最初の方法では、`DataSourceID` プロパティを使用して内部データ Web コントロールにバインドされた `ItemTemplate` 外側のデータ Web コントロールに ObjectDataSource を使用しました。 2番目の手法では、ASP.NET ページの分離コードクラスのメソッドを使用してデータにアクセスします。 このメソッドは、databinding 構文を通じて内部データ Web コントロール s `DataSource` プロパティにバインドできます。

このチュートリアルで検証した入れ子になったユーザーインターフェイスでは、リピータ内に入れ子になったリピータが使用されていますが、これらの手法は他のデータ Web コントロールに拡張できます。 Repeater は、GridView 内、または DataList 内の GridView の入れ子にすることができます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Zack Jones と Liz Shulok でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
> [次へ](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
