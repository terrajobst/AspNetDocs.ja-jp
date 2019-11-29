---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
title: Batch の削除C#() |Microsoft Docs
author: rick-anderson
description: 1回の操作で複数のデータベースレコードを削除する方法について説明します。 ユーザーインターフェイスレイヤーでは、以前の tut で作成された拡張 GridView に基づいて構築されます。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: ac6916d0-a5ab-4218-9760-7ba9e72d258c
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: ed832c38b4972f440ab64c141e29c85f0a9df920
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588917"
---
# <a name="batch-deleting-c"></a>一括削除 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip)または[PDF のダウンロード](batch-deleting-cs/_static/datatutorial65cs1.pdf)

> 1回の操作で複数のデータベースレコードを削除する方法について説明します。 ユーザーインターフェイスレイヤーでは、前のチュートリアルで作成した拡張された GridView に基づいて構築されます。 データアクセス層では、複数の削除操作をトランザクション内にラップして、すべての削除が成功するか、すべての削除がロールバックされるようにします。

## <a name="introduction"></a>はじめに

[前のチュートリアル](batch-updating-cs.md)では、完全に編集可能な GridView を使用してバッチ編集インターフェイスを作成する方法を説明しています。 ユーザーが頻繁に多くのレコードを編集している場合、バッチ編集インターフェイスでは、ポストバックとキーボードからマウスへのコンテキストの切り替えがはるかに少なくなるため、エンドユーザーの効率が向上します。 この手法は、ユーザーが1つの移動で多数のレコードを削除することがよくあるページでも同様に役立ちます。

オンライン電子メールクライアントを使用したユーザーは、既に、最も一般的なバッチ削除インターフェイスの1つに慣れています。対応するグリッドの各行にチェックボックスがあり、対応する [すべてのチェックされた項目を削除] ボタンが表示されます (図1を参照)。 このチュートリアルでは、前のチュートリアルでは、web ベースのインターフェイスと、一連のレコードを1つのアトミック操作として削除するメソッドの両方を作成するためのすべての作業が既に完了しているため、これは少しです。 [チェックボックスの Gridview 列の追加](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md)に関するチュートリアルでは、チェックボックスの列を含む gridview を作成し、[トランザクション内でのデータベース変更のラッピング](wrapping-database-modifications-within-a-transaction-cs.md)に関するチュートリアルでは、トランザクションを使用して `ProductID` 値の `List<T>` を削除するためのメソッドを BLL に作成しました。 このチュートリアルでは、前のエクスペリエンスを基にして、作業中のバッチの削除の例を作成します。

[各行にチェックボックスが含まれて ![](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)

**図 1**: 各行にチェックボックスが含まれている ([クリックすると、フルサイズの画像が表示](batch-deleting-cs/_static/image2.png)されます)

## <a name="step-1-creating-the-batch-deleting-interface"></a>手順 1: Batch 削除インターフェイスを作成する

[Checkbox チュートリアルの「GridView 列の追加](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md)」のチュートリアルでは、batch の削除インターフェイスを既に作成しているため、最初から作成するのではなく、単に `BatchDelete.aspx` にコピーできます。 まず、`BatchData` フォルダーの `BatchDelete.aspx` ページと `EnhancedGridView` フォルダーの `CheckBoxField.aspx` ページを開きます。 [`CheckBoxField.aspx`] ページで、[ソース] ビューにアクセスし、図2に示すように、`<asp:Content>` タグの間にマークアップをコピーします。

[CheckBoxField の宣言型マークアップをクリップボードにコピー ![には](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)

**図 2**: `CheckBoxField.aspx` の宣言型マークアップをクリップボードにコピーする ([クリックすると、フルサイズのイメージが表示](batch-deleting-cs/_static/image4.png)されます)

次に、`BatchDelete.aspx` のソースビューにアクセスし、`<asp:Content>` タグ内にクリップボードの内容を貼り付けます。 また、`CheckBoxField.aspx.cs` の分離コードクラス内のコードをコピーして、`BatchDelete.aspx.cs` の分離コードクラス (`DeleteSelectedProducts` ボタン s `Click` イベントハンドラー、`ToggleCheckState` メソッド、および `Click` ボタンと `CheckAll` ボタンのイベントハンドラー) の内部に貼り付けることもできます。 このコンテンツをコピーした後、`BatchDelete.aspx` ページの分離コードクラスに次のコードが含まれている必要があります。

[!code-csharp[Main](batch-deleting-cs/samples/sample1.cs)]

宣言型マークアップとソースコードをコピーした後、ブラウザーで表示することで `BatchDelete.aspx` をテストしてみましょう。 GridView に最初の10個の製品が一覧表示され、各行に製品の名前、カテゴリ、価格がチェックボックスと共に表示されます。 [すべてを確認]、[すべてオフ]、[選択した製品を削除] の3つのボタンがあります。 [すべてを確認] ボタンをクリックすると、すべてのチェックボックスがオンになり、すべてのチェックボックスがオフになります。 [選択した製品を削除] をクリックすると、選択した製品の `ProductID` 値を示すメッセージが表示されますが、実際には製品は削除されません。

[CheckBoxField からのインターフェイスが BatchDeleting に移動されました。 ![](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)

**図 3**: `CheckBoxField.aspx` からのインターフェイスが `BatchDeleting.aspx` に移動されました ([クリックしてフルサイズのイメージを表示](batch-deleting-cs/_static/image6.png))

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>手順 2: トランザクションを使用してチェックされた製品を削除する

バッチ削除インターフェイスが `BatchDeleting.aspx`に正常にコピーされたので、[選択した製品の削除] ボタンが `ProductsBLL` クラスの `DeleteProductsWithTransaction` メソッドを使用してチェックされた製品を削除するようにコードを更新します。 このメソッドは、「[トランザクション内のデータベースの変更のラップ](wrapping-database-modifications-within-a-transaction-cs.md)」チュートリアルで追加され、`ProductID` 値の `List<T>` を入力として受け取り、対応する各 `ProductID` をトランザクションのスコープ内で削除します。

`DeleteSelectedProducts` Button s `Click` イベントハンドラーは、現在、次の `foreach` ループを使用して、各 GridView 行を反復処理します。

[!code-csharp[Main](batch-deleting-cs/samples/sample2.cs)]

各行に対して、`ProductSelector` CheckBox Web コントロールはプログラムによって参照されます。 このチェックボックスをオンにすると、行の `ProductID` が `DataKeys` コレクションから取得され、`DeleteResults` ラベル s `Text` プロパティが更新されて、行が削除対象として選択されたことを示すメッセージが表示されます。

上記のコードでは、`ProductsBLL` クラス s への呼び出しとして、実際にはレコードが削除されません `Delete` メソッドはコメントアウトされています。この削除ロジックが適用された場合、コードはアトミック操作内ではなく、製品を削除します。 つまり、シーケンス内の最初のいくつかの削除が成功したが、後で失敗した場合 (外部キー制約違反など)、例外がスローされますが、既に削除されている製品は削除されたままになります。

原子性を確保するために、代わりに `ProductsBLL` クラス s `DeleteProductsWithTransaction` メソッドを使用する必要があります。 このメソッドは `ProductID` 値のリストを受け入れるため、まずグリッドからこのリストをコンパイルし、それをパラメーターとして渡す必要があります。 まず、`int`型の `List<T>` のインスタンスを作成します。 `foreach` ループ内で、選択した製品 `ProductID` 値をこの `List<T>`に追加する必要があります。 ループの後、この `List<T>` は `ProductsBLL` クラス s `DeleteProductsWithTransaction` メソッドに渡す必要があります。 次のコードを使用して、`DeleteSelectedProducts` Button s `Click` イベントハンドラーを更新します。

[!code-csharp[Main](batch-deleting-cs/samples/sample3.cs)]

更新されたコードは、型 `int` (`productIDsToDelete`) の `List<T>` を作成し、削除する `ProductID` 値を設定します。 `foreach` ループの後、少なくとも1つの製品が選択されている場合は、`ProductsBLL` クラス s `DeleteProductsWithTransaction` メソッドが呼び出され、このリストが渡されます。 `DeleteResults` ラベルも表示され、データが GridView に再バインドされます (新しく削除されたレコードがグリッド内の行として表示されなくなります)。

図4に、削除対象として複数の行が選択された後の GridView を示します。 図5に、[選択した製品の削除] ボタンがクリックされた直後の画面を示します。 図5では、削除されたレコードの `ProductID` 値が GridView の下のラベルに表示され、これらの行は GridView に存在しなくなっていることに注意してください。

[選択した製品が削除され ![](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)

**図 4**: 選択した製品が削除されます ([クリックすると、フルサイズの画像が表示](batch-deleting-cs/_static/image8.png)されます)

[削除された製品の ProductID 値が GridView の下に一覧表示され ![](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)

**図 5**: 削除された製品 `ProductID` 値は GridView の下に一覧表示されます ([クリックすると、フルサイズの画像が表示](batch-deleting-cs/_static/image10.png)されます)

> [!NOTE]
> `DeleteProductsWithTransaction` メソッドの原子性をテストするには、`Order Details` テーブルに製品のエントリを手動で追加し、その製品を削除します (他のユーザーと一緒に)。 関連付けられた注文で製品を削除しようとすると、外部キー制約違反が発生しますが、選択した他の製品の削除がロールバックされる方法に注意してください。

## <a name="summary"></a>要約

バッチを削除するためのインターフェイスを作成するには、チェックボックスの列を含む GridView を追加します。ボタン Web コントロールは、クリックすると、選択したすべての行を1つのアトミック操作として削除します。 このチュートリアルでは、前の2つのチュートリアルで説明したように、このようなインターフェイスを構築し、[チェックボックスの GridView 列を追加](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md)して、[データベースの変更をトランザクション内にラップ](wrapping-database-modifications-within-a-transaction-cs.md)します。 最初のチュートリアルでは、チェックボックスの列を含む GridView を作成しました。後者では、`ProductID` 値の `List<T>` が渡されたときに、そのすべてをトランザクションのスコープ内で削除したメソッドを BLL に実装しました。

次のチュートリアルでは、バッチ挿入を実行するためのインターフェイスを作成します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow and Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](batch-updating-cs.md)
> [次へ](batch-inserting-cs.md)
