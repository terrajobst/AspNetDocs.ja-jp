---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
title: BLL レベルおよび DAL レベルの例外の処理C#() |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、編集可能な DataList の更新ワークフロー中に発生した例外を tactfully に処理する方法について説明します。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: f8fd58e2-f932-4f08-ab3d-fbf8ff3295d2
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 35ff60be6ed67ea8d1bf226ae70f590100597757
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634105"
---
# <a name="handling-bll--and-dal-level-exceptions-c"></a>BLL レベルと DAL レベルの例外を処理する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_CS.exe)または[PDF のダウンロード](handling-bll-and-dal-level-exceptions-cs/_static/datatutorial38cs1.pdf)

> このチュートリアルでは、編集可能な DataList の更新ワークフロー中に発生した例外を tactfully に処理する方法について説明します。

## <a name="introduction"></a>はじめに

DataList チュートリアル[でのデータの編集と削除の概要](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)では、単純な編集および削除機能を提供する DataList を作成しました。 完全に機能している間は、編集または削除のプロセス中に発生したエラーによってハンドルされない例外が発生したため、ユーザーにとってはわかりませんでした。 たとえば、製品名を省略したり、製品を編集するときに価格を非常に手頃な価格で入力したりすると、例外がスローされます。 この例外はコードでキャッチされないため、ASP.NET ランタイムにバブルし、web ページに例外の詳細が表示されます。

「 [ASP.NET ページでの BLL と DAL レベルの例外の処理](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)」チュートリアルで説明したように、ビジネスロジックまたはデータアクセス層の深さから例外が発生すると、例外の詳細が ObjectDataSource に返され、次に GridView に返されます。 これらの例外を適切に処理する方法については、ObjectDataSource または GridView のイベントハンドラーを `Updated` または `RowUpdated` 作成し、例外を確認して、例外が処理されたことを示しています。

ただし、DataList チュートリアルでは、データの更新と削除に ObjectDataSource は使用しません。 代わりに、BLL に対して直接作業しています。 BLL または DAL から発生した例外を検出するには、ASP.NET ページの分離コード内で例外処理コードを実装する必要があります。 このチュートリアルでは、編集可能な DataList の更新ワークフロー中に発生した例外を tactfully に処理する方法について説明します。

> [!NOTE]
> *「Datalist チュートリアル」の「データの編集と削除の概要*」では、datalist のデータを編集および削除するためのさまざまな手法について説明しました。これは、更新と削除に ObjectDataSource を使用する手法です。 これらの手法を採用している場合は、ObjectDataSource または DAL の例外を ObjectDataSource s `Updated` または `Deleted` のイベントハンドラーを通じて処理できます。

## <a name="step-1-creating-an-editable-datalist"></a>手順 1: 編集可能な DataList の作成

更新ワークフロー中に発生した例外の処理について心配する前に、まず、編集可能な DataList を作成してみましょう。 `EditDeleteDataList` フォルダーの `ErrorHandling.aspx` ページを開き、DataList をデザイナーに追加し、その `ID` プロパティを `Products`に設定して、`ProductsDataSource`という名前の新しい ObjectDataSource を追加します。 `ProductsBLL` クラス s `GetProducts()` メソッドを使用してレコードを選択するように ObjectDataSource を構成します。[挿入]、[更新]、および [削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[GetProducts () メソッドを使用して製品情報を返す ![](handling-bll-and-dal-level-exceptions-cs/_static/image2.png)](handling-bll-and-dal-level-exceptions-cs/_static/image1.png)

**図 1**: `GetProducts()` メソッドを使用して製品情報を返す ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-cs/_static/image3.png)されます)

ObjectDataSource ウィザードを完了すると、Visual Studio によって DataList の `ItemTemplate` が自動的に作成されます。 これを、各製品の名前と価格を表示し、[編集] ボタンを含む `ItemTemplate` で置き換えます。 次に、[名前]、[価格]、[更新]、および [キャンセル] ボタンのテキストボックス Web コントロールを含む `EditItemTemplate` を作成します。 最後に、DataList s `RepeatColumns` プロパティを2に設定します。

これらの変更が完了すると、ページの宣言型マークアップは次のようになります。 [編集]、[キャンセル]、および [更新] の各ボタンの `CommandName` プロパティが、それぞれ [編集]、[キャンセル]、[更新] に設定されていることを確認します。

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample1.aspx)]

> [!NOTE]
> このチュートリアルでは、DataList s ビューステートを有効にする必要があります。

ブラウザーで進行状況を確認します (図2を参照)。

[各製品に [Edit] \ (編集 \) ボタンが含まれて ![](handling-bll-and-dal-level-exceptions-cs/_static/image5.png)](handling-bll-and-dal-level-exceptions-cs/_static/image4.png)

**図 2**: 各製品には、[編集] ボタンがあります ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-cs/_static/image6.png)されます)

現在、[編集] ボタンによってポストバックが発生するのは、まだ製品が編集可能になっていないためです。 編集を有効にするには、DataList s `EditCommand`、`CancelCommand`、および `UpdateCommand` イベントのイベントハンドラーを作成する必要があります。 `EditCommand` イベントと `CancelCommand` イベントは、単に DataList s `EditItemIndex` プロパティを更新し、データを DataList に再バインドします。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample2.cs)]

`UpdateCommand` イベントハンドラーはもう少し複雑です。 編集した製品の `ProductID` を `DataKeys` コレクションから、`EditItemTemplate`のテキストボックスの製品名と価格と共に読み取る必要があります。その後、DataList を編集前の状態に戻す前に、`ProductsBLL` クラス s `UpdateProduct` メソッドを呼び出します。

ここでは、「 *DataList チュートリアル」の「データの編集と削除の概要*」で、`UpdateCommand` イベントハンドラーとまったく同じコードを使用してみましょう。 手順 2. で例外を適切に処理するコードを追加します。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample3.cs)]

形式が無効な入力がある場合は、無効な形式の単価、-$5.00 のような無効な単価値、または製品名の省略によって例外が発生します。 `UpdateCommand` イベントハンドラーには、この時点で例外処理コードが含まれていないため、例外は ASP.NET ランタイムにバブルアップされ、エンドユーザーに表示されます (図3を参照)。

![未処理の例外が発生すると、エンドユーザーにエラーページが表示されます。](handling-bll-and-dal-level-exceptions-cs/_static/image7.png)

**図 3**: ハンドルされない例外が発生した場合、エンドユーザーにエラーページが表示される

## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>手順 2: UpdateCommand イベントハンドラーで例外を適切に処理する

更新中のワークフローでは、`UpdateCommand` イベントハンドラー、BLL、または DAL で例外が発生する可能性があります。 たとえば、ユーザーが高価な価格を入力した場合、`UpdateCommand` イベントハンドラーの `Decimal.Parse` ステートメントは `FormatException` 例外をスローします。 ユーザーが製品名を省略した場合、または価格に負の値が含まれている場合は、DAL によって例外が発生します。

例外が発生したときに、ページ内に情報メッセージを表示します。 `ID` が `ExceptionDetails`に設定されているページに、ラベル Web コントロールを追加します。 `Styles.css` ファイルで定義されている `Warning` CSS クラスに `CssClass` プロパティを割り当てることにより、ラベル s テキストを赤、特大、太字、斜体のフォントで表示するように構成します。

エラーが発生した場合、ラベルを一度だけ表示する必要があります。 つまり、それ以降のポストバックでは、ラベル s の警告メッセージが表示されなくなります。 これを実現するには、Label s `Text` プロパティをクリアするか `Visible` プロパティを設定して、`Page_Load` イベントハンドラーで `False` に戻します (「 [ASP.NET ページでの BLL および DAL レベルの例外の処理](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)」を参照してください)。または、ラベル s のビューステートのサポートを無効にします。 後者のオプションを使用してみましょう。

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample4.aspx)]

例外が発生したときに、例外の詳細を `ExceptionDetails` Label コントロール s `Text` プロパティに割り当てます。 ビューステートが無効になっているため、以降のポストバック時に `Text` プロパティのプログラムによる変更が失われ、既定のテキスト (空の文字列) に戻り、警告メッセージが非表示になります。

ページに有用なメッセージを表示するためにエラーが発生したタイミングを判断するには、`UpdateCommand` イベントハンドラーに `Try ... Catch` ブロックを追加する必要があります。 `Try` 部分には、例外の原因となる可能性のあるコードが含まれています。一方、`Catch` ブロックには、例外の発生時に実行されるコードが含まれています。 `Try ... Catch` ブロックの詳細については、.NET Framework のドキュメントの[例外処理の基礎](https://msdn.microsoft.com/library/2w8f0bss.aspx)に関するセクションを参照してください。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample5.cs)]

`Try` ブロック内のコードによって任意の型の例外がスローされると、`Catch` ブロックのコードが実行を開始します。 `DbException`、`NoNullAllowedException`、`ArgumentException`などによってスローされる例外の種類は、最初にエラーをよりしたものによって異なります。 データベースレベルで問題が発生すると、`DbException` がスローされます。 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、または `ReorderLevel` フィールドに無効な値が入力された場合、`ArgumentException` クラスでこれらのフィールド値を検証するコードを追加したため、`ProductsDataTable` がスローされます (「[ビジネスロジック層の作成](../introduction/creating-a-business-logic-layer-cs.md)」チュートリアルを参照してください)。

キャッチされた例外の種類に基づいてメッセージテキストを指定することにより、エンドユーザーにより役立つ説明を提供できます。 次のコードは、 [ASP.NET Page チュートリアルでの BLL と DAL レベルの例外の処理](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)について、ほぼ同じ形式で使用されています。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample6.cs)]

このチュートリアルを完了するには、キャッチされた `Exception` インスタンス (`ex`) を渡して、`Catch` ブロックから `DisplayExceptionDetails` メソッドを呼び出すだけです。

`Try ... Catch` ブロックが配置されていると、ユーザーには、図4と5に示すように、より詳細なエラーメッセージが表示されます。 例外が発生した場合、DataList は編集モードのままであることに注意してください。 これは、例外が発生すると、コントロールフローが直ちに `Catch` ブロックにリダイレクトされ、DataList を編集前の状態に返すコードがバイパスされるためです。

[ユーザーが必要なフィールドを省略した場合にエラーメッセージが表示される ![](handling-bll-and-dal-level-exceptions-cs/_static/image9.png)](handling-bll-and-dal-level-exceptions-cs/_static/image8.png)

**図 4**: ユーザーが必要なフィールドを省略した場合にエラーメッセージが表示される ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-cs/_static/image10.png)されます)

[負の価格を入力したときにエラーメッセージが表示される ![](handling-bll-and-dal-level-exceptions-cs/_static/image12.png)](handling-bll-and-dal-level-exceptions-cs/_static/image11.png)

**図 5**: 負の価格を入力したときにエラーメッセージが表示される ([クリックすると、フルサイズの画像が表示](handling-bll-and-dal-level-exceptions-cs/_static/image13.png)されます)

## <a name="summary"></a>要約

GridView および ObjectDataSource は、ワークフローの更新中や削除中に発生した例外に関する情報を含むポストレベルのイベントハンドラーを提供します。また、例外が発生したかどうかを示すために設定できるプロパティについても説明します。対応. ただし、DataList を使用して BLL を直接使用する場合、これらの機能は使用できません。 代わりに、例外処理を実装する責任があります。

このチュートリアルでは、`UpdateCommand` イベントハンドラーに `Try ... Catch` ブロックを追加して、編集可能な DataList s 更新ワークフローに例外処理を追加する方法を説明しました。 更新中のワークフロー中に例外が発生した場合、`Catch` ブロックのコードが実行され、`ExceptionDetails` ラベルに有用な情報が表示されます。

この時点で、DataList では、最初の段階で例外が発生しないようにする作業は行われません。 負の価格によって例外が発生することはわかっていますが、ユーザーがこのような無効な入力を事前に入力できないようにするための機能はまだ追加されていません。 次のチュートリアルでは、`EditItemTemplate`に検証コントロールを追加することによって、無効なユーザー入力によって発生する例外を軽減する方法について説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [例外のデザインのガイドライン](https://msdn.microsoft.com/library/ms298399.aspx)
- [エラーログモジュールとハンドラー (ELMAH)](http://workspaces.gotdotnet.com/elmah) (エラーをログに記録するためのオープンソースライブラリ)
- [.NET Framework 2.0 のエンタープライズライブラリ](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en)(例外管理アプリケーションブロックを含む)

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Ken による Isa です。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](performing-batch-updates-cs.md)
> [次へ](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
