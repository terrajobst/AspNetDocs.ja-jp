---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: ASP.NET ページでの BLL レベルおよび DAL レベルの例外の処理 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、挿入、更新、または削除の操作中に例外が発生した場合に、わかりやすい情報を表示するエラーメッセージを表示する方法について説明します。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: ee277596ade18d2603892d134b47c2c8697836bb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620935"
---
# <a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>ASP.NET ページで BLL レベルと DAL レベルの例外を処理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe)または[PDF のダウンロード](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> このチュートリアルでは、ASP.NET データ Web コントロールの挿入、更新、または削除操作中に例外が発生した場合に、わかりやすいエラーメッセージを表示する方法について説明します。

## <a name="introduction"></a>はじめに

階層化されたアプリケーションアーキテクチャを使用して ASP.NET web アプリケーションのデータを操作するには、次の3つの一般的な手順を実行します。

1. ビジネスロジック層を呼び出す必要がある方法と、それに渡すパラメーター値を決定します。 パラメーター値は、ハードコーディングされているか、プログラムによって割り当てられるか、またはユーザーが入力する入力です。
2. メソッドを呼び出します。
3. 結果を処理します。 データを返す BLL メソッドを呼び出す場合、データをデータ Web コントロールにバインドすることが必要になることがあります。 データを変更する BLL メソッドの場合は、戻り値に基づいて何らかのアクションを実行したり、手順 2. で発生した例外を適切に処理したりすることができます。

[前のチュートリアル](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)で見たように、ObjectDataSource とデータ Web コントロールの両方で、手順 1. と 3. の機能拡張ポイントが提供されています。 たとえば、GridView は、フィールド値を ObjectDataSource の `UpdateParameters` コレクションに割り当てる前に、その `RowUpdating` イベントを発生させます。この `RowUpdated` イベントは、ObjectDataSource が操作を完了した後に発生します。

手順1で発生するイベントを既に調べており、それらを使用して入力パラメーターをカスタマイズしたり操作を取り消したりする方法について説明しました。 このチュートリアルでは、操作が完了した後に発生するイベントに注目します。 これらの投稿レベルのイベントハンドラーを使用すると、操作中に例外が発生したかどうかを判断し、適切に処理することができます。標準の ASP.NET を既定のままにするのではなく、わかりやすい情報を示すエラーメッセージが画面に表示されます。例外ページ。

これらの投稿レベルのイベントを使用する方法を示すために、編集可能な GridView で製品を一覧表示するページを作成してみましょう。 製品を更新するときに、例外が発生した場合、ASP.NET ページには、問題が発生したことを示す、GridView の上に短いメッセージが表示されます。 では、始めましょう。

## <a name="step-1-creating-an-editable-gridview-of-products"></a>手順 1: 編集可能な製品の GridView を作成する

前のチュートリアルでは、`ProductName` と `UnitPrice`の2つのフィールドだけを含む編集可能な GridView を作成しました。 これには、`ProductsBLL` クラスの `UpdateProduct` メソッドに対して追加のオーバーロードを作成する必要があります。1つは、各製品フィールドのパラメーターとしてではなく、3つの入力パラメーター (製品の名前、単価、および ID) のみを受け入れたものです。 このチュートリアルでは、この方法をもう一度実行して、製品の名前、単位あたりの数量、単価、および在庫数を表示する編集可能な GridView を作成します。ただし、在庫の名前、単価、および単位の編集のみが許可されます。

このシナリオに対応するには、`UpdateProduct` メソッドの別のオーバーロードが必要です。1つは、製品の名前、単価、在庫数量、および ID の4つのパラメーターを受け取ります。 次のメソッドを `ProductsBLL` クラスに追加します。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

このメソッドが完成したら、この4つの特定の製品フィールドを編集できる ASP.NET ページを作成できます。 `EditInsertDelete` フォルダーの [`ErrorHandling.aspx`] ページを開き、デザイナーを使用して GridView をページに追加します。 GridView を新しい ObjectDataSource にバインドし、`Select()` メソッドを `ProductsBLL` クラスの `GetProducts()` メソッドにマップし、`Update()` メソッドを、先ほど作成した `UpdateProduct` オーバーロードに割り当てます。

[4つの入力パラメーターを受け取る UpdateProduct メソッドのオーバーロードを使用 ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**図 1**: 4 つの入力パラメーターを受け取る `UpdateProduct` メソッドのオーバーロードを使用する ([クリックしてフルサイズのイメージを表示する](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png))

これにより、4つのパラメーターを持つ `UpdateParameters` コレクションを持つ ObjectDataSource と、product フィールドごとにフィールドを持つ GridView が作成されます。 ObjectDataSource の宣言型マークアップは、`OldValuesParameterFormatString` プロパティに値 `original_{0}`を割り当てます。これにより、BLL クラスでは `original_productID` という名前の入力パラメーターが渡されないため、例外が発生します。 この設定を宣言構文から完全に削除することを忘れないでください (または、既定値に設定して `{0}`)。

次に、`ProductName`、`QuantityPerUnit`、`UnitPrice`、および `UnitsInStock` BoundFields のみを含むように、GridView を省いします。 また、必要と思われるフィールドレベルの書式設定も自由に適用できます (`HeaderText` プロパティの変更など)。

前のチュートリアルでは、読み取り専用モードと編集モードの両方で、`UnitPrice` BoundField を通貨として書式設定する方法について説明しました。 ここでも同じ操作を行います。 図2に示すように、BoundField の `DataFormatString` プロパティを `{0:c}`、その `HtmlEncode` プロパティを `false`に設定し、その `ApplyFormatInEditMode` を `true`に設定する必要があることを思い出してください。

[UnitPrice BoundField を通貨として表示するように構成 ![には](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**図 2**: `UnitPrice` BoundField を通貨として表示するように構成する ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png)されます)

`UnitPrice` を編集インターフェイスで通貨として書式設定するには、`decimal` 値に通貨形式の文字列を解析する GridView の `RowUpdating` イベントのイベントハンドラーを作成する必要があります。 最後のチュートリアルの `RowUpdating` イベントハンドラーも、ユーザーが `UnitPrice` 値を指定したことを確認するためにチェックされていることを思い出してください。 ただし、このチュートリアルでは、ユーザーが価格を省略できるようにします。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

GridView には `QuantityPerUnit` BoundField が含まれていますが、この BoundField は表示のみを目的としているため、ユーザーが編集することはできません。 これを配置するには、単に BoundFields ' `ReadOnly` プロパティを `true`に設定します。

[QuantityPerUnit BoundField を読み取り専用にする ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**図 3**: `QuantityPerUnit` BoundField を読み取り専用[にする (クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png)されます)

最後に、GridView のスマートタグの [編集を有効にする] チェックボックスをオンにします。 これらの手順を完了すると、`ErrorHandling.aspx` ページのデザイナーは図4のようになります。

[必要な BoundFields 以外のすべてを削除して、[編集を有効にする] チェックボックスをオンに ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**図 4**: 必要な Boundfields 以外のすべてを削除し、[編集を有効にする] チェックボックスをオン[にする (クリックしてフルサイズのイメージを表示する](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png))

この時点で、すべての製品の `ProductName`、`QuantityPerUnit`、`UnitPrice`、および `UnitsInStock` の各フィールドの一覧が表示されます。ただし、編集できるのは、`ProductName`、`UnitPrice`、および `UnitsInStock` フィールドのみです。

[![ユーザーは、在庫フィールドの製品名、価格、単位を簡単に編集できるようになりました。](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**図 5**: ユーザーは在庫フィールドの製品名、価格、単位を簡単に編集できるようになりました ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png)されます)

## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>手順 2: DAL レベルの例外を適切に処理する

編集可能な GridView は、ユーザーが編集した製品の名前、価格、および在庫の単位に対して有効な値を入力したときにてになりますが、無効な値を入力すると例外が発生します。 たとえば、`ProductName` 値を省略すると、`ProductsRow` クラスの `ProductName` プロパティの `AllowDBNull` プロパティが `false`に設定されているため、 [system.data.nonullallowedexception](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp)がスローされます。データベースがダウンしている場合は、データベースに接続しようとすると、TableAdapter によって `SqlException` がスローされます。 アクションを実行しないと、これらの例外はデータアクセス層からビジネスロジック層、ASP.NET ページ、最後に ASP.NET ランタイムにバブルアップされます。

Web アプリケーションがどのように構成されているか、および `localhost`からアプリケーションにアクセスしているかどうかによって、ハンドルされない例外によって、汎用サーバーエラーページ、詳細エラーレポート、またはユーザーフレンドリな web ページのいずれかが発生する可能性があります。 ASP.NET ランタイムがキャッチされない例外に応答する方法の詳細については、「ASP.NET と[CustomErrors 要素](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx)の[Web アプリケーションエラー処理](http://www.15seconds.com/issue/030102.htm)」を参照してください。

図6は、`ProductName` 値を指定せずに製品を更新しようとしたときに発生した画面を示しています。 これは `localhost`を通じて表示される既定の詳細エラーレポートです。

[製品名を省略すると ![例外の詳細が表示されます](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**図 6**: 製品名を省略すると例外の詳細が表示される ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png)されます)

このような例外の詳細は、アプリケーションをテストする場合に役立ちますが、例外が発生したときに、このような画面をエンドユーザーに提示することは、理想よりも低くなります。 エンドユーザーは、`NoNullAllowedException` の内容や原因がわからない可能性があります。 より良い方法は、製品を更新しようとしたときに問題が発生したことを説明する、ユーザーにわかりやすいメッセージを表示することです。

操作の実行中に例外が発生した場合、ObjectDataSource と data Web control の両方のレベルイベントは、その例外を検出し、ASP.NET ランタイムまでのバブルから例外をキャンセルする手段を提供します。 この例では、GridView の `RowUpdated` イベントのイベントハンドラーを作成して、例外が発生したかどうかを判断し、その場合は、ラベル Web コントロールに例外の詳細を表示します。

まず、ラベルを ASP.NET ページに追加し、その `ID` プロパティを `ExceptionDetails` に設定して、その `Text` プロパティをクリアします。 このメッセージに対するユーザーの目を引くには、`CssClass` プロパティを `Warning`に設定します。これは、前のチュートリアルで `Styles.css` ファイルに追加した CSS クラスです。 この CSS クラスを使用すると、ラベルのテキストが赤、斜体、太字、特大のフォントで表示されることを思い出してください。

[ページにラベル Web コントロールを追加 ![には](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**図 7**: ページにラベル Web コントロールを追加する ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png)されます)

このラベル Web コントロールは、例外が発生した直後にのみ表示されるようにするため、`Page_Load` イベントハンドラーで `Visible` プロパティを false に設定します。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

このコードでは、最初のページにアクセスし、次のポストバックで、`ExceptionDetails` コントロールの `Visible` プロパティを `false`に設定します。 GridView の `RowUpdated` イベントハンドラーで検出できる DAL または BLL レベルの例外が発生した場合は、`ExceptionDetails` コントロールの `Visible` プロパティを true に設定します。 Web コントロールのイベントハンドラーは、ページのライフサイクルの `Page_Load` イベントハンドラーの後に発生するため、ラベルが表示されます。 ただし、次のポストバック時には、`Page_Load` イベントハンドラーによって `Visible` プロパティが `false`に戻され、再度ビューから非表示になります。

> [!NOTE]
> または、`Page_Load` で `ExceptionDetails` コントロールの `Visible` プロパティを設定する必要があります。これを行うには、宣言構文で `Visible` プロパティ `false` を割り当て、そのビューステートを無効にします (`EnableViewState` プロパティを `false`に設定します)。 この代替アプローチは、今後のチュートリアルで使用します。

ラベルコントロールが追加されたので、次のステップは GridView の `RowUpdated` イベントのイベントハンドラーを作成することです。 デザイナーで GridView を選択し、プロパティウィンドウにアクセスして、[稲妻] アイコンをクリックし、GridView のイベントを一覧表示します。 このチュートリアルの前半でこのイベントのイベントハンドラーを作成したので、GridView の `RowUpdating` イベントのエントリが既に存在している必要があります。 `RowUpdated` イベントのイベントハンドラーも作成します。

![GridView の RowUpdated イベントのイベントハンドラーを作成します。](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**図 8**: GridView の `RowUpdated` イベントのイベントハンドラーを作成する

> [!NOTE]
> イベントハンドラーは、分離コードクラスファイルの先頭にあるドロップダウンリストを使用して作成することもできます。 左側のドロップダウンリストから GridView を選択し、右側にある [`RowUpdated` イベント] をクリックします。

このイベントハンドラーを作成すると、ASP.NET ページの分離コードクラスに次のコードが追加されます。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

このイベントハンドラーの2番目の入力パラメーターは、 [GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx)型のオブジェクトで、例外を処理するための3つのプロパティがあります。

- スローされた例外への参照を `Exception` します。例外がスローされなかった場合、このプロパティの値はになり `null`
- 例外が `RowUpdated` イベントハンドラーで処理されたかどうかを示すブール値を `ExceptionHandled` します。`false` (既定値) の場合、例外が再スローされ、ASP.NET ランタイムまで実行されます。
- `KeepInEditMode` に設定 `true` すると、編集された GridView 行は編集モードのままになります。`false` (既定値) の場合、GridView 行は読み取り専用モードに戻ります。

次に、コードは `Exception` が `null`ないかどうかを確認する必要があります。つまり、操作の実行中に例外が発生したことを意味します。 この場合は、次のようにします。

- `ExceptionDetails` ラベルにわかりやすいメッセージを表示する
- 例外が処理されたことを示します。
- GridView 行を編集モードのままにする

次のコードは、これらの目的を達成します。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

このイベントハンドラーは、`e.Exception` が `null`かどうかを確認することによって開始されます。 そうでない場合は、`ExceptionDetails` ラベルの `Visible` プロパティが `true` に設定され、その `Text` プロパティが "製品の更新で問題が発生しました。" となります。 スローされた実際の例外の詳細は、`e.Exception` オブジェクトの `InnerException` プロパティに存在します。 この内部例外が調べられ、特定の型の場合は、追加の便利なメッセージが `ExceptionDetails` ラベルの `Text` プロパティに追加されます。 最後に、`ExceptionHandled` プロパティと `KeepInEditMode` プロパティの両方が `true`に設定されています。

図9に、製品名を省略した場合のこのページのスクリーンショットを示します。図10は、無効な `UnitPrice` 値 (-50) を入力した場合の結果を示しています。

[ProductName BoundField には値が含まれている必要があり ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**図 9**: `ProductName` BoundField に値が含まれている必要があります ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png)されます)

[![負の UnitPrice 値は使用できません](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**図 10**: 負の `UnitPrice` 値は使用できません ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png)されます)

`e.ExceptionHandled` プロパティを `true`に設定すると、`RowUpdated` イベントハンドラーによって例外が処理されたことが示されます。 このため、例外は ASP.NET ランタイムに反映されません。

> [!NOTE]
> 図9と10は、ユーザー入力が無効であるために発生した例外を適切に処理する方法を示しています。 ただし、ASP.NET ページでは、`ProductsBLL` クラスの `UpdateProduct` メソッドを呼び出す前に、ユーザーの入力が有効であることを確認する必要があるため、このような無効な入力はビジネスロジックレイヤーには適していません。 次のチュートリアルでは、ビジネスロジック層に送信されるデータがビジネスルールに準拠していることを確認するために、編集および挿入インターフェイスに検証コントロールを追加する方法について説明します。 検証コントロールは、ユーザーが指定したデータが有効になるまで `UpdateProduct` メソッドを呼び出すことができないようにするだけでなく、データ入力の問題を特定するためのより有益なユーザーエクスペリエンスも提供します。

## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>手順 3: BLL レベルの例外を適切に処理する

データの挿入、更新、または削除を行う場合、データアクセス層は、データ関連のエラーが発生したときに例外をスローすることがあります。 データベースがオフラインであるか、必要なデータベーステーブル列に値が指定されていないか、テーブルレベルの制約に違反している可能性があります。 ビジネスロジック層では、厳密なデータ関連の例外だけでなく、例外を使用してビジネスルールに違反したことを示すことができます。 たとえば、[ビジネスロジック層の作成](../introduction/creating-a-business-logic-layer-vb.md)に関するチュートリアルでは、元の `UpdateProduct` オーバーロードにビジネスルールチェックを追加しました。 具体的には、ユーザーが製品を廃止済みとしてマークしていた場合、その製品が供給業者によって提供される唯一の製品ではないことが必要でした。 この状態に違反した場合は、`ApplicationException` がスローされました。

このチュートリアルで作成した `UpdateProduct` のオーバーロードについては、`UnitPrice` フィールドが元の `UnitPrice` 値の2倍を超える新しい値に設定されることを禁止するビジネスルールを追加してみましょう。 これを実現するには、このチェックを実行し、規則に違反した場合に `ApplicationException` をスローするように `UpdateProduct` オーバーロードを調整します。 更新されたメソッドは次のとおりです。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

この変更により、既存の価格の2倍を超える価格更新によって `ApplicationException` がスローされます。 DAL から発生した例外と同様に、この BLL によって生成される `ApplicationException` は、GridView の `RowUpdated` イベントハンドラーで検出および処理できます。 実際には、書き込まれた `RowUpdated` イベントハンドラーのコードは、この例外を正しく検出し、`ApplicationException`の `Message` プロパティ値を表示します。 図11は、ユーザーが Chai の価格を $50.00 に更新しようとしたときのスクリーンショットを示しています。これは、現在の $19.95 の価格の2倍を超えています。

[ビジネスルールによって、製品の2倍以上の価格が適用されない ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**図 11**: ビジネスルールによって、製品の2倍以上の価格が適用されない場合 ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png)されます)

> [!NOTE]
> ビジネスロジックルールが `UpdateProduct` メソッドのオーバーロードから共通のメソッドにリファクタリングされるのが理想的です。 これは、リーダーの演習として残されています。

## <a name="summary"></a>要約

挿入、更新、削除の各操作では、データ Web コントロールと ObjectDataSource の両方が、実際の操作をもうする前レベルと後レベルのイベントを発生させます。 このチュートリアルと前のチュートリアルで説明したように、gridview の `RowUpdating` イベントが発生し、その後に ObjectDataSource の `Updating` イベントが発生します。この時点で、ObjectDataSource の基になるオブジェクトに対して update コマンドが実行されます。 操作が完了すると、ObjectDataSource の `Updated` イベントが発生し、その後に GridView の `RowUpdated` イベントが続きます。

事前レベルのイベントのイベントハンドラーを作成して、操作の結果を検査し、それに対応するために、入力パラメーターまたはポストレベルイベントをカスタマイズすることができます。 Post レベルのイベントハンドラーは、操作中に例外が発生したかどうかを検出するために最もよく使用されます。 例外が発生した場合、これらのポストレベルのイベントハンドラーは、必要に応じて独自の例外を処理できます。 このチュートリアルでは、わかりやすいエラーメッセージを表示することによって、このような例外を処理する方法を説明しました。

次のチュートリアルでは、データの書式設定の問題 (負の `UnitPrice`の入力など) によって発生する例外の可能性を軽減する方法について説明します。 具体的には、編集および挿入インターフェイスに検証コントロールを追加する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Liz Shulok でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
> [次へ](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
