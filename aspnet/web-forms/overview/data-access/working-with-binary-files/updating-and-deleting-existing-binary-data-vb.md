---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
title: 既存のバイナリデータを更新および削除する (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、GridView コントロールを使用してテキストデータを簡単に編集および削除する方法について説明しました。 このチュートリアルでは、GridView コントロールについても説明します。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 3a052ced-9cf5-47b8-a400-934f0b687c26
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 27ff6941008b4e7bf6d632e4c248fd1d35fb3589
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621253"
---
# <a name="updating-and-deleting-existing-binary-data-vb"></a>既存のバイナリ データの更新と削除 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_VB.exe)または[PDF のダウンロード](updating-and-deleting-existing-binary-data-vb/_static/datatutorial57vb1.pdf)

> 前のチュートリアルでは、GridView コントロールを使用してテキストデータを簡単に編集および削除する方法について説明しました。 このチュートリアルでは、GridView コントロールを使用してバイナリデータを編集および削除する方法についても説明します。バイナリデータがデータベースに保存されるか、ファイルシステムに格納されます。

## <a name="introduction"></a>はじめに

これまでの3つのチュートリアルでは、バイナリデータを操作するための機能が非常に追加されています。 まず、`Categories` テーブルに `BrochurePath` 列を追加し、それに応じてアーキテクチャを更新しました。 また、データアクセス層とビジネスロジック層のメソッドを追加して、カテゴリテーブル s の既存の `Picture` 列を操作します。この列には、イメージファイルのバイナリコンテンツが格納されています。 GridView にバイナリデータを表示する web ページをビルドしました。これは、`<img>` 要素にカテゴリ s の画像を表示し、ユーザーが新しいカテゴリを追加してそのパンフレットや画像データをアップロードできるようにするための DetailsView を追加したものです。

まだ実装されているのは、既存のカテゴリを編集および削除できることだけです。このチュートリアルでは、GridView の組み込みの編集および削除機能を使用します。 ユーザーは、カテゴリを編集するときに、必要に応じて新しい画像をアップロードすることも、既存の画像をそのまま使用することもできます。 パンフレットの場合は、既存のパンフレットを使用するか、新しいパンフレットをアップロードするか、カテゴリに関連付けられたパンフレットがないことを示すことができます。 始めましょう!

## <a name="step-1-updating-the-data-access-layer"></a>手順 1: データアクセス層を更新する

DAL には、`Insert`、`Update`、および `Delete` の各メソッドが自動生成されていますが、これらのメソッドは、`Picture` 列を含まない `CategoriesTableAdapter` s メインクエリに基づいて生成されました。 そのため、`Insert` および `Update` メソッドには、カテゴリの画像のバイナリデータを指定するためのパラメーターは含まれていません。 [前のチュートリアル](including-a-file-upload-option-when-adding-a-new-record-vb.md)で行ったように、バイナリデータを指定するときに、`Categories` テーブルを更新するための新しい TableAdapter メソッドを作成する必要があります。

型指定されたデータセットを開き、デザイナーで `CategoriesTableAdapter` s ヘッダーを右クリックし、コンテキストメニューの [クエリの追加] をクリックして、TableAdapter クエリの構成ウィザードを起動します。 このウィザードを開始するには、TableAdapter クエリでデータベースにアクセスする方法を確認します。 [SQL ステートメントを使用する] を選択し、[次へ] をクリックします。 次の手順では、生成するクエリの種類を指定します。 `Categories` テーブルに新しいレコードを追加するクエリを作成したので、[更新] を選択し、[次へ] をクリックします。

[![[更新] オプションを選択します。](updating-and-deleting-existing-binary-data-vb/_static/image2.png)](updating-and-deleting-existing-binary-data-vb/_static/image1.png)

**図 1**: [更新] オプションを選択[する (クリックすると、フルサイズの画像が表示](updating-and-deleting-existing-binary-data-vb/_static/image3.png)されます)

次に、`UPDATE` SQL ステートメントを指定する必要があります。 このウィザードでは、TableAdapter のメインクエリ (`CategoryName`、`Description`、`BrochurePath` の値を更新するクエリ) に対応する `UPDATE` ステートメントが自動的に提示されます。 次のように、`@Picture` パラメーターと共に `Picture` 列が含まれるようにステートメントを変更します。

[!code-sql[Main](updating-and-deleting-existing-binary-data-vb/samples/sample1.sql)]

ウィザードの最後の画面では、新しい TableAdapter メソッドに名前を指定するように求められます。 `UpdateWithPicture` を入力し、[完了] をクリックします。

[新しい TableAdapter メソッド UpdateWithPicture ![名前](updating-and-deleting-existing-binary-data-vb/_static/image5.png)](updating-and-deleting-existing-binary-data-vb/_static/image4.png)

**図 2**: 新しい TableAdapter メソッドに名前を指定[する `UpdateWithPicture` (クリックすると、フルサイズのイメージが表示](updating-and-deleting-existing-binary-data-vb/_static/image6.png)されます)

## <a name="step-2-adding-the-business-logic-layer-methods"></a>手順 2: ビジネスロジック層のメソッドを追加する

DAL を更新するだけでなく、カテゴリを更新および削除するためのメソッドを含めるように BLL を更新する必要があります。 これらのメソッドは、プレゼンテーション層から呼び出されます。

カテゴリを削除するには、`CategoriesTableAdapter` s 自動生成された `Delete` メソッドを使用します。 次のメソッドを `CategoriesBLL` クラスに追加します。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample2.vb)]

このチュートリアルでは、2つの方法でカテゴリを更新します。これは、バイナリ画像データを想定し、`CategoriesTableAdapter` に追加した `UpdateWithPicture` メソッドを呼び出し、`CategoryName`、`Description`、および `BrochurePath` の値のみを受け取り、クラスの自動生成された `CategoriesTableAdapter` ステートメントを使用します。 2つの方法を使用する場合の背後では、ユーザーが category s picture を他のフィールドと共に更新することが必要になる場合があります。この場合、ユーザーは新しい画像をアップロードする必要があります。 アップロードされた画像のバイナリデータは、`UPDATE` ステートメントで使用できます。 場合によっては、ユーザーが名前と説明を更新するだけでよい場合もあります。 ただし、`UPDATE` ステートメントで `Picture` 列のバイナリデータも必要な場合は、その情報も提供する必要があります。 この場合、編集中のレコードの画像データを戻すために、データベースへの追加のトリップが必要になります。 そのため、2つの `UPDATE` メソッドが必要です。 ビジネスロジックレイヤーでは、カテゴリの更新時に画像データが提供されるかどうかに基づいて、どちらを使用するかが決定されます。

これを容易にするために、2つのメソッドを `CategoriesBLL` クラスに追加します。どちらも `UpdateCategory`という名前です。 最初の1つは、3つの `String`、`Byte` 配列、および `Integer` を入力パラメーターとして受け取る必要があります。2つ目は、3つの `String` s と `Integer`です。 `String` 入力パラメーターは、カテゴリの名前、説明、およびパンフレットのファイルパス用で、`Byte` 配列は category s picture のバイナリコンテンツ用であり、`Integer` は更新するレコードの `CategoryID` を識別します。 渡された `Byte` 配列が `Nothing`場合、最初のオーバーロードは2番目のオーバーロードを呼び出します。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample3.vb)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>手順 3: 挿入と表示の機能をコピーする

前の[チュートリアル](including-a-file-upload-option-when-adding-a-new-record-vb.md)では、GridView のすべてのカテゴリを一覧表示し、システムに新しいカテゴリを追加するための DetailsView を提供する `UploadInDetailsView.aspx` という名前のページを作成しました。 このチュートリアルでは、GridView を拡張して、編集と削除のサポートを含めます。 `UploadInDetailsView.aspx`から作業を続行するのではなく、このチュートリアルの変更を同じフォルダーの `UpdatingAndDeleting.aspx` ページに配置します。 `~/BinaryData`を使用します。 宣言型のマークアップとコードをコピーして `UploadInDetailsView.aspx` から `UpdatingAndDeleting.aspx`に貼り付けます。

まず、[`UploadInDetailsView.aspx`] ページを開きます。 図3に示すように、`<asp:Content>` 要素内のすべての宣言構文をコピーします。 次に、`UpdatingAndDeleting.aspx` を開いて、`<asp:Content>` 要素内にこのマークアップを貼り付けます。 同様に、`UploadInDetailsView.aspx` ページの分離コードクラスから `UpdatingAndDeleting.aspx`にコードをコピーします。

[UploadInDetailsView から宣言型のマークアップをコピー ![には](updating-and-deleting-existing-binary-data-vb/_static/image8.png)](updating-and-deleting-existing-binary-data-vb/_static/image7.png)

**図 3**: `UploadInDetailsView.aspx` から宣言マークアップをコピー[する (クリックすると、フルサイズのイメージが表示](updating-and-deleting-existing-binary-data-vb/_static/image9.png)されます)

宣言型マークアップとコードをコピーした後、`UpdatingAndDeleting.aspx`にアクセスします。 同じ出力が表示され、前のチュートリアルの `UploadInDetailsView.aspx` ページと同じユーザーエクスペリエンスが得られます。

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>手順 4: ObjectDataSource および GridView への削除サポートの追加

[「データの挿入、更新、削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)」で説明したように、GridView には組み込みの削除機能が用意されており、基になるデータソースが削除をサポートしている場合は、チェックボックスの目盛りでこれらの機能を有効にすることができます。 現在、GridView がバインドされている ObjectDataSource (`CategoriesDataSource`) は、削除をサポートしていません。

これを解決するには、ObjectDataSource s スマートタグから [データソースの構成] オプションをクリックしてウィザードを起動します。 最初の画面は、ObjectDataSource が `CategoriesBLL` クラスで動作するように構成されていることを示しています。 [次へ] をクリックします。 現時点では、ObjectDataSource s `InsertMethod` および `SelectMethod` プロパティのみが指定されています。 ただし、[更新] タブと [削除] タブのドロップダウンリストには、`UpdateCategory` と `DeleteCategory` の各メソッドがそれぞれ自動的に設定されます。 これは、`CategoriesBLL` クラスでは、更新および削除の既定のメソッドとして `DataObjectMethodAttribute` を使用してこれらのメソッドをマークしたためです。

ここでは、[更新] タブのドロップダウンリストを [(なし)] に設定します。ただし、[削除] タブのドロップダウンリストは [`DeleteCategory`] に設定したままにします。 更新サポートを追加するには、手順6でこのウィザードに戻ります。

[DeleteCategory メソッドを使用するように ObjectDataSource を構成 ![には](updating-and-deleting-existing-binary-data-vb/_static/image11.png)](updating-and-deleting-existing-binary-data-vb/_static/image10.png)

**図 4**: `DeleteCategory` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](updating-and-deleting-existing-binary-data-vb/_static/image12.png))

> [!NOTE]
> ウィザードを完了すると、フィールドとキーを更新するかどうかを確認するメッセージが表示され、データ Web コントロールのフィールドが再生成されます。 [はい] を選択すると、実行したフィールドのカスタマイズがすべて上書きされます。

ObjectDataSource には、`DeleteMethod` プロパティの値と `DeleteParameter`が含まれるようになりました。 ウィザードを使用してメソッドを指定する場合、Visual Studio は ObjectDataSource s `OldValuesParameterFormatString` プロパティを `original_{0}`に設定します。これにより、update メソッドと delete メソッドの呼び出しで問題が発生します。 このため、このプロパティを完全に削除するか、既定の `{0}`にリセットしてください。 この ObjectDataSource プロパティのメモリを更新する必要がある場合は、[データの挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)に関するチュートリアルを参照してください。

ウィザードを完了し、`OldValuesParameterFormatString`を修正した後、ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample4.aspx)]

ObjectDataSource を構成した後、gridview s スマートタグから [削除を有効にする] チェックボックスをオンにして、削除する機能を GridView に追加します。 これにより、`ShowDeleteButton` プロパティが `True`に設定されている GridView に CommandField が追加されます。

[GridView での削除のサポートを有効に ![](updating-and-deleting-existing-binary-data-vb/_static/image14.png)](updating-and-deleting-existing-binary-data-vb/_static/image13.png)

**図 5**: GridView での削除のサポートを有効に[する (クリックしてフルサイズのイメージを表示する](updating-and-deleting-existing-binary-data-vb/_static/image15.png))

削除機能をテストしてみましょう。 `Products` table s `CategoryID` と `Categories` table s `CategoryID`の間に外部キーがあります。そのため、最初の8つのカテゴリのいずれかを削除しようとすると、外部キー制約違反例外が発生します。 この機能をテストするには、パンフレットと画像の両方を提供する新しいカテゴリを追加します。 図6に示すテストカテゴリには、`Test.pdf` という名前のテスト用のパンフレットファイルと、テスト用の画像が含まれています。 図7は、テストカテゴリが追加された後の GridView を示しています。

[パンフレットと画像を含むテストカテゴリを追加 ![には](updating-and-deleting-existing-binary-data-vb/_static/image17.png)](updating-and-deleting-existing-binary-data-vb/_static/image16.png)

**図 6**: パンフレットと画像を含むテストカテゴリを追加[する (クリックすると、フルサイズの画像が表示](updating-and-deleting-existing-binary-data-vb/_static/image18.png)されます)

[テストカテゴリを挿入した後 ![、GridView に表示されます。](updating-and-deleting-existing-binary-data-vb/_static/image20.png)](updating-and-deleting-existing-binary-data-vb/_static/image19.png)

**図 7**: テストカテゴリを挿入すると、そのカテゴリが GridView に表示されます ([クリックすると、フルサイズのイメージが表示](updating-and-deleting-existing-binary-data-vb/_static/image21.png)されます)

Visual Studio で、ソリューションエクスプローラーを更新します。 `~/Brochures` フォルダーに新しいファイルが表示されます (図 8 `Test.pdf` を参照)。

次に、テストカテゴリ行の [削除] リンクをクリックして、ページをポストバックし、`CategoriesBLL` クラス s `DeleteCategory` メソッドを起動します。 これにより、DAL の `Delete` メソッドが呼び出され、適切な `DELETE` ステートメントがデータベースに送信されます。 その後、データが GridView に再バインドされ、テストカテゴリが存在しない状態でクライアントにマークアップが送り返されます。

削除ワークフローによって `Categories` テーブルからテストカテゴリレコードが正常に削除されましたが、web サーバー s ファイルシステムからパンフレットファイルが削除されませんでした。 ソリューションエクスプローラーを更新すると、`Test.pdf` が `~/Brochures` フォルダーにまだ残っていることがわかります。

![テスト .pdf ファイルは Web サーバーのファイルシステムから削除されませんでした](updating-and-deleting-existing-binary-data-vb/_static/image1.gif)

**図 8**: `Test.pdf` ファイルが Web サーバーのファイルシステムから削除されていない

## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>手順 5: 削除されたカテゴリ s パンフレットファイルを削除する

データベースの外部にバイナリデータを格納する場合の欠点の1つは、関連付けられているデータベースレコードが削除されたときに、これらのファイルをクリーンアップするために余分な手順を実行する必要があることです。 GridView および ObjectDataSource は、delete コマンドが実行される前と後の両方で起動するイベントを提供します。 実際には、アクション前イベントと事後アクションイベントの両方に対してイベントハンドラーを作成する必要があります。 `Categories` レコードを削除する前に、PDF ファイルのパスを決定する必要がありますが、例外が発生し、カテゴリが削除されていない場合は、カテゴリが削除される前に PDF を削除する必要はありません。

GridView s [`RowDeleting` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)は、ObjectDataSource s delete コマンドが呼び出される前に発生しますが、その後、 [`RowDeleted` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx)が発生します。 次のコードを使用して、これら2つのイベントのイベントハンドラーを作成します。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample5.vb)]

`RowDeleting` イベントハンドラーでは、削除される行の `CategoryID` が GridView の `DataKeys` コレクションからグラブされます。このコレクションには、このイベントハンドラーで `e.Keys` コレクションを介してアクセスできます。 次に、`CategoriesBLL` クラス s `GetCategoryByCategoryID(categoryID)` を呼び出して、削除されているレコードに関する情報を返します。 返された `CategoriesDataRow` オブジェクトに`NULL``BrochurePath` 以外の値がある場合は、`RowDeleted` イベントハンドラーでファイルを削除できるように、ページ変数 `deletedCategorysPdfPath` に格納されます。

> [!NOTE]
> `RowDeleting` イベントハンドラーで削除される `Categories` レコードの `BrochurePath` の詳細を取得するのではなく、その `BrochurePath` を GridView s `DataKeyNames` プロパティに追加して、`e.Keys` コレクションを介してレコードの値にアクセスすることもできます。 このようにすると、GridView のビューステートのサイズが若干増加しますが、必要なコードの量が減り、データベースへのトリップが保存されます。

ObjectDataSource s の基になる delete コマンドが呼び出されると、GridView s `RowDeleted` イベントハンドラーが起動します。 データの削除中に例外が発生せず、`deletedCategorysPdfPath`の値がある場合は、PDF がファイルシステムから削除されます。 この追加のコードは、その画像に関連付けられているカテゴリのバイナリデータをクリーンアップするために必要ではないことに注意してください。 これは、画像データがデータベースに直接格納されているため、`Categories` 行を削除すると、そのカテゴリの画像データも削除されるためです。

2つのイベントハンドラーを追加した後、このテストケースを再度実行します。 カテゴリを削除すると、関連付けられている PDF も削除されます。

既存のレコードに関連付けられているバイナリデータを更新すると、いくつかの興味深い課題が生じます。 このチュートリアルの残りの部分では、更新機能をパンフレットや画像に追加する方法について詳しく検証します。 手順6では、パンフレットの情報を更新する方法について説明します。手順7では、図の更新について説明します。

## <a name="step-6-updating-a-category-s-brochure"></a>手順 6: カテゴリ s のパンフレットを更新する

「データの挿入、更新、削除の概要」のチュートリアルで説明したように、GridView は、基になるデータソースが適切に構成されている場合にチェックボックスの目盛りによって実装できる、組み込みの行レベルの編集サポートを提供します。 現時点では、`CategoriesDataSource` ObjectDataSource はまだ更新サポートを含むように構成されていないため、でを追加します。

ObjectDataSource s ウィザードの [データソースの構成] リンクをクリックして、2番目の手順に進みます。 `CategoriesBLL`で使用 `DataObjectMethodAttribute` ため、[更新] ドロップダウンリストには、4つの入力パラメーター (すべての列については、`Picture`) を受け入れる `UpdateCategory` オーバーロードが自動的に入力されます。 これを変更して、5つのパラメーターを持つオーバーロードを使用するようにします。

[画像のパラメーターを含む UpdateCategory メソッドを使用するように ObjectDataSource を構成 ![には](updating-and-deleting-existing-binary-data-vb/_static/image23.png)](updating-and-deleting-existing-binary-data-vb/_static/image22.png)

**図 9**: `Picture` のパラメーターを含む `UpdateCategory` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](updating-and-deleting-existing-binary-data-vb/_static/image24.png))

ObjectDataSource には、`UpdateMethod` プロパティの値、および対応する `UpdateParameter` s が含まれるようになりました。 手順 4. で説明したように、Visual Studio では、データソースの構成ウィザードを使用するときに、ObjectDataSource s `OldValuesParameterFormatString` プロパティが `original_{0}` に設定されます。 これにより、update メソッドと delete メソッドの呼び出しで問題が発生します。 このため、このプロパティを完全に削除するか、既定の `{0}`にリセットしてください。

ウィザードを完了し、`OldValuesParameterFormatString`を修正した後、ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample6.aspx)]

GridView の組み込み編集機能をオンにするには、GridView s スマートタグの [編集を有効にする] オプションをオンにします。 これにより、CommandField s `ShowEditButton` プロパティが `True`に設定されます。その結果、編集ボタン (編集中の行の [更新] ボタンと [キャンセル] ボタン) が追加されます。

[編集をサポートするように GridView を構成 ![には](updating-and-deleting-existing-binary-data-vb/_static/image26.png)](updating-and-deleting-existing-binary-data-vb/_static/image25.png)

**図 10**: GridView で編集をサポートするように構成する ([クリックしてフルサイズのイメージを表示する](updating-and-deleting-existing-binary-data-vb/_static/image27.png))

ブラウザーを使用してページを参照し、行 s の編集ボタンの1つをクリックします。 `CategoryName` および `Description` BoundFields は、テキストボックスとしてレンダリングされます。 `BrochurePath` TemplateField には `EditItemTemplate`がないため、このパンフレットへのリンク `ItemTemplate` は引き続き表示されます。 `Picture` ImageField は、`Text` プロパティに ImageField s `DataImageUrlField` 値 (この場合は `CategoryID`) の値が割り当てられているテキストボックスとして表示されます。

[GridView に BrochurePath の編集インターフェイスがない ![](updating-and-deleting-existing-binary-data-vb/_static/image29.png)](updating-and-deleting-existing-binary-data-vb/_static/image28.png)

**図 11**: GridView に `BrochurePath` の編集インターフェイスがない ([クリックしてフルサイズのイメージを表示する](updating-and-deleting-existing-binary-data-vb/_static/image30.png))

## <a name="customizing-thebrochurepaths-editing-interface"></a>`BrochurePath`s 編集インターフェイスのカスタマイズ

`BrochurePath` TemplateField の編集インターフェイスを作成する必要があります。1つは、次のいずれかの方法をユーザーに許可します。

- カテゴリ s のパンフレットをそのままにしておきます。
- 新しいパンフレットをアップロードしてカテゴリ s のパンフレットを更新します。または、
- カテゴリ s のパンフレットをすべて削除します (カテゴリに関連付けられたパンフレットがなくなった場合)。

また、`Picture` ImageField s 編集インターフェイスも更新する必要がありますが、手順7ではこれについて説明します。

GridView s スマートタグから、テンプレートの編集 リンクをクリックし、ドロップダウンリストから `BrochurePath` TemplateField s `EditItemTemplate` を選択します。 このテンプレートに RadioButtonList Web コントロールを追加し、その `ID` プロパティを `BrochureOptions` に設定し、その `AutoPostBack` プロパティを `True`に設定します。 プロパティウィンドウから、`Items` プロパティの省略記号をクリックすると、`ListItem` コレクションエディターが表示されます。 次の3つのオプションを `Value` s 1、2、および3にそれぞれ追加します。

- 現在のパンフレットを使用する
- 現在のパンフレットの削除
- 新しいパンフレットのアップロード

最初の `ListItem` s `Selected` プロパティを `True`に設定します。

![RadioButtonList に3つの ListItems を追加します。](updating-and-deleting-existing-binary-data-vb/_static/image2.gif)

**図 12**: RadioButtonList に3つの `ListItem` s を追加する

RadioButtonList の下に、`BrochureUpload`という名前の FileUpload コントロールを追加します。 `Visible` プロパティを `False`に設定します。

[RadioButtonList および FileUpload コントロールを EditItemTemplate に追加 ![には](updating-and-deleting-existing-binary-data-vb/_static/image32.png)](updating-and-deleting-existing-binary-data-vb/_static/image31.png)

**図 13**: `EditItemTemplate` に RadioButtonList コントロールと FileUpload コントロールを追加する ([クリックすると、フルサイズの画像が表示](updating-and-deleting-existing-binary-data-vb/_static/image33.png)されます)

この RadioButtonList は、3つのオプションをユーザーに提供します。 FileUpload コントロールは、最後のオプションである [新しいパンフレットをアップロードする] が選択されている場合にのみ表示されるという考え方です。 これを実現するには、RadioButtonList s `SelectedIndexChanged` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample7.vb)]

RadioButtonList コントロールと FileUpload コントロールはテンプレート内にあるため、プログラムを使用してこれらのコントロールにアクセスするには、少しコードを記述する必要があります。 `SelectedIndexChanged` イベントハンドラーには、`sender` 入力パラメーターの RadioButtonList の参照が渡されます。 FileUpload コントロールを取得するには、RadioButtonList s 親コントロールを取得し、そこから `FindControl("controlID")` メソッドを使用する必要があります。 RadioButtonList と FileUpload の両方のコントロールへの参照を取得した後、FileUpload control s `Visible` プロパティは、RadioButtonList s `SelectedValue` が3に等しい場合にのみ `True` に設定されます。これは、Upload new パンフレット `ListItem`の `Value` です。

このコードが用意されているので、編集インターフェイスをテストしてみましょう。 行の [編集] ボタンをクリックします。 最初に、[現在のパンフレットを使用する] オプションを選択する必要があります。 選択されたインデックスを変更すると、ポストバックが発生します。 3番目のオプションが選択されている場合は、FileUpload コントロールが表示されます。それ以外の場合は非表示になります。 図14は、[編集] ボタンが最初にクリックされたときの編集インターフェイスを示しています。図15は、[新しいパンフレットをアップロードする] オプションが選択された後のインターフェイスを示しています。

[初期状態では、[現在のパンフレットを使用する] オプションが選択されてい ![](updating-and-deleting-existing-binary-data-vb/_static/image35.png)](updating-and-deleting-existing-binary-data-vb/_static/image34.png)

**図 14**: 最初に [現在のパンフレットを使用する] オプションが選択されている ([クリックすると、フルサイズの画像が表示](updating-and-deleting-existing-binary-data-vb/_static/image36.png)されます)

[[新しいパンフレットをアップロードする] オプションを選択する ![、FileUpload コントロールが表示されます。](updating-and-deleting-existing-binary-data-vb/_static/image38.png)](updating-and-deleting-existing-binary-data-vb/_static/image37.png)

**図 15**: [新しいパンフレットをアップロードする] オプションを選択すると、FileUpload コントロールが表示されます ([クリックすると、フルサイズの画像が表示](updating-and-deleting-existing-binary-data-vb/_static/image39.png)されます)

## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>パンフレットファイルを保存して`BrochurePath`列を更新する

[GridView s Update] ボタンがクリックされると、その `RowUpdating` イベントが発生します。 ObjectDataSource s update コマンドが呼び出され、GridView s `RowUpdated` イベントが発生します。 削除ワークフローと同様に、これらのイベントの両方に対してイベントハンドラーを作成する必要があります。 `RowUpdating` イベントハンドラーでは、`BrochureOptions` RadioButtonList の `SelectedValue` に基づいて実行するアクションを決定する必要があります。

- `SelectedValue` が1の場合は、同じ `BrochurePath` 設定を使用し続けることをお勧めします。 そのため、ObjectDataSource s `brochurePath` パラメーターを、更新するレコードの既存の `BrochurePath` 値に設定する必要があります。 ObjectDataSource s `brochurePath` パラメーターは `e.NewValues["brochurePath"] = value`を使用して設定できます。
- `SelectedValue` が2の場合は、レコード s `BrochurePath` の値を `NULL`に設定します。 これを行うには、ObjectDataSource s `brochurePath` パラメーターを `Nothing`に設定します。これにより、`UPDATE` ステートメントでデータベース `NULL` が使用されます。 既存のパンフレットファイルが削除されている場合は、既存のファイルを削除する必要があります。 ただし、例外を発生させずに更新が完了した場合にのみ、この操作を行います。
- `SelectedValue` が3の場合は、ユーザーが PDF ファイルをアップロードしたことを確認し、ファイルシステムに保存して、レコード s `BrochurePath` 列の値を更新します。 さらに、置き換えられる既存のパンフレットファイルがある場合は、前のファイルを削除する必要があります。 ただし、例外を発生させずに更新が完了した場合にのみ、この操作を行います。

RadioButtonList s `SelectedValue` が3の場合に完了する必要がある手順は、DetailsView s `ItemInserting` イベントハンドラーで使用されるものとほぼ同じです。 このイベントハンドラーは、[前のチュートリアル](including-a-file-upload-option-when-adding-a-new-record-vb.md)で追加した DetailsView コントロールから新しいカテゴリレコードが追加されたときに実行されます。 このため、この機能を別の方法にリファクタリングする behooves ます。 具体的には、共通の機能を次の2つの方法に移行しました。

- `ProcessBrochureUpload(FileUpload, out bool)` は、FileUpload コントロールインスタンスを入力として受け入れ、削除操作または編集操作を続行するかどうか、または何らかの検証エラーによってキャンセルする必要があるかどうかを指定する出力ブール値を受け取ります。 このメソッドは、保存されたファイルへのパスを返します。ファイルが保存されていない場合は `null` します。
- `deletedCategorysPdfPath` が `null`ない場合は、ページ変数のパスで指定されたファイル `deletedCategorysPdfPath` 削除 `DeleteRememberedBrochurePath` ます。

これら2つのメソッドのコードは次のとおりです。 前のチュートリアルの `ProcessBrochureUpload` と DetailsView s `ItemInserting` イベントハンドラーの類似性に注意してください。 このチュートリアルでは、これらの新しいメソッドを使用するように DetailsView s イベントハンドラーを更新しました。 このチュートリアルに関連付けられているコードをダウンロードして、DetailsView s イベントハンドラーに加えられた変更を確認してください。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample8.vb)]

次のコードに示すように、GridView の `RowUpdating` イベントハンドラーと `RowUpdated` イベントハンドラーでは、`ProcessBrochureUpload` および `DeleteRememberedBrochurePath` メソッドが使用されます。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample9.vb)]

`RowUpdating` イベントハンドラーが一連の条件ステートメントを使用して、`BrochureOptions` RadioButtonList s `SelectedValue` プロパティ値に基づいて適切なアクションを実行する方法に注意してください。

このコードを使用すると、カテゴリを編集して、現在のパンフレットを使用したり、パンフレットを使用したり、新しいものをアップロードしたりすることができます。 試してみましょう。`RowUpdating` および `RowUpdated` のイベントハンドラーにブレークポイントを設定して、ワークフローを把握します。

## <a name="step-7-uploading-a-new-picture"></a>手順 7: 新しい画像をアップロードする

`Picture` ImageField s 編集インターフェイスは、`DataImageUrlField` プロパティの値が設定されたテキストボックスとしてレンダリングされます。 編集ワークフローの実行中に、GridView はパラメーターを指定して ObjectDataSource にパラメーターを渡します。このパラメーターの値には、ImageField s `DataImageUrlField` プロパティの値を指定し、パラメーター s 値を編集インターフェイスのテキストボックスに入力した値を渡します。 この動作は、イメージがファイルシステム上のファイルとして保存され、`DataImageUrlField` にイメージの完全な URL が含まれている場合に適しています。 このような状況では、編集インターフェイスによってテキストボックスにイメージの URL が表示されます。この URL は、ユーザーが変更してデータベースに保存し直すことができます。 この既定のインターフェイスでは、ユーザーが新しいイメージをアップロードすることを許可しませんが、イメージの URL を現在の値から別の値に変更することができます。 ただし、このチュートリアルでは、ImageField s の既定の編集インターフェイスでは不十分です。 `Picture` バイナリデータがデータベースに直接格納されており、`DataImageUrlField` プロパティが `CategoryID`だけを保持しているためです。

ユーザーが ImageField を使用して行を編集するときに、このチュートリアルで行われる処理について理解を深めるには、次の例を考えてみます。たとえば、ユーザーが `CategoryID` 10 の行を編集し、`Picture` ImageField を、値10のテキストボックスとしてレンダリングします。 ユーザーがこのテキストボックスの値を50に変更し、[更新] ボタンをクリックしたとします。 ポストバックが発生すると、GridView は、値が50の `CategoryID` という名前のパラメーターを最初に作成します。 ただし、GridView がこのパラメーター (および `CategoryName` パラメーターと `Description` パラメーター) を送信する前に、`DataKeys` コレクションの値が追加されます。 したがって、`CategoryID` パラメーターを、`CategoryID` 値の基になる現在の行 s (10) で上書きします。 簡単に言えば、ImageField s 編集インターフェイスは、このチュートリアルの編集ワークフローには影響しません。これは、ImageField s `DataImageUrlField` プロパティの名前と grid s `DataKey` 値が同じであるためです。

ImageField を使用すると、データベースのデータに基づいてイメージを簡単に表示できますが、編集インターフェイスにテキストボックスを用意する必要はありません。 代わりに、エンドユーザーがカテゴリの画像を変更するために使用できる FileUpload コントロールを提供する必要があります。 `BrochurePath` の値とは異なり、これらのチュートリアルでは、各カテゴリに画像が含まれている必要があると判断しました。 そのため、ユーザーが関連付けられている画像がないことをユーザーに通知させる必要はありません。ユーザーが新しい画像をアップロードするか、現在の画像をそのままにしておくことができます。

ImageField s 編集インターフェイスをカスタマイズするには、TemplateField に変換する必要があります。 GridView s スマートタグから、[列の編集] リンクをクリックし、ImageField を選択し、[このフィールドを TemplateField に変換する] リンクをクリックします。

![ImageField を TemplateField に変換します。](updating-and-deleting-existing-binary-data-vb/_static/image3.gif)

**図 16**: Imagefield を TemplateField に変換する

この方法で ImageField を TemplateField に変換すると、2つのテンプレートを持つ TemplateField が生成されます。 次の宣言型の構文に示すように、`ItemTemplate` には、ImageField s `DataImageUrlField` および `DataImageUrlFormatString` プロパティに基づく databinding 構文を使用して `ImageUrl` プロパティが割り当てられているイメージ Web コントロールが含まれています。 `EditItemTemplate` には、`Text` プロパティが `DataImageUrlField` プロパティによって指定された値にバインドされているテキストボックスが含まれています。

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample10.aspx)]

FileUpload コントロールを使用するには、`EditItemTemplate` を更新する必要があります。 GridView s スマートタグから、[テンプレートの編集] リンクをクリックし、ドロップダウンリストから `Picture` TemplateField s `EditItemTemplate` を選択します。 テンプレートにテキストボックスが表示されます。これを削除します。 次に、FileUpload コントロールをツールボックスからテンプレートにドラッグし、`ID` を `PictureUpload`に設定します。 また、カテゴリ s 画像を変更するためのテキストを追加し、新しい画像を指定します。 カテゴリの画像を同じ状態に保つには、そのフィールドをテンプレートに対して空のままにします。

[FileUpload コントロールを EditItemTemplate に追加 ![には](updating-and-deleting-existing-binary-data-vb/_static/image41.png)](updating-and-deleting-existing-binary-data-vb/_static/image40.png)

**図 17**: `EditItemTemplate` に FileUpload コントロールを追加する ([クリックすると、フルサイズの画像が表示](updating-and-deleting-existing-binary-data-vb/_static/image42.png)されます)

編集インターフェイスをカスタマイズしたら、ブラウザーで進行状況を確認します。 読み取り専用モードで行を表示する場合、カテゴリの画像は前と同じように表示されますが、[編集] ボタンをクリックすると、画像の列が FileUpload コントロールでテキストとしてレンダリングされます。

[編集インターフェイスに FileUpload コントロールが含まれている ![](updating-and-deleting-existing-binary-data-vb/_static/image44.png)](updating-and-deleting-existing-binary-data-vb/_static/image43.png)

**図 18**: 編集インターフェイスに FileUpload コントロールが含まれている ([クリックしてフルサイズのイメージを表示する](updating-and-deleting-existing-binary-data-vb/_static/image45.png))

ObjectDataSource は `CategoriesBLL` クラス s `UpdateCategory` メソッドを呼び出すように構成されています。これは、`Byte` 配列として画像のバイナリデータを入力として受け入れます。 ただし、この配列が `Nothing`場合は、代替 `UpdateCategory` オーバーロードが呼び出されます。これにより、`Picture` 列を変更しない `UPDATE` SQL ステートメントが発行され、その結果、カテゴリの現在の画像はそのまま残ります。 そのため、GridView s `RowUpdating` イベントハンドラーでは、プログラムで `PictureUpload` FileUpload コントロールを参照し、ファイルがアップロードされたかどうかを判断する必要があります。 アップロードされていない場合は、`picture` パラメーターの値を指定し*ません*。 一方、`PictureUpload` FileUpload コントロールにファイルがアップロードされた場合は、それが JPG ファイルであることを確認する必要があります。 そのような場合は、`picture` パラメーターを使用して、そのバイナリコンテンツを ObjectDataSource に送信できます。

手順 6. で使用したコードと同様に、ここで必要なコードの多くは、既に DetailsView s `ItemInserting` イベントハンドラーに存在します。 このため、一般的な機能を新しいメソッドにリファクタリングし、`ValidPictureUpload`して、このメソッドを使用するように `ItemInserting` イベントハンドラーを更新しました。

GridView s `RowUpdating` イベントハンドラーの先頭に次のコードを追加します。 このコードは、パンフレットファイルを保存するコードの前に記述することが重要です。これは、無効な画像ファイルがアップロードされた場合に、web サーバーのファイルシステムにパンフレットを保存したくないからです。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample11.vb)]

`ValidPictureUpload(FileUpload)` メソッドは、唯一の入力パラメーターとして FileUpload コントロールを受け取り、アップロードしたファイルが JPG であることを確認するために、アップロードされたファイルの拡張子を確認します。画像ファイルがアップロードされた場合にのみ呼び出されます。 ファイルがアップロードされていない場合は、picture パラメーターが設定されていないため、`Nothing`の既定値が使用されます。 画像がアップロードされ、`ValidPictureUpload` が `True`を返す場合、`picture` パラメーターにはアップロードされたイメージのバイナリデータが割り当てられます。メソッドが `False`を返すと、更新ワークフローが取り消され、イベントハンドラーが終了します。

DetailsView s `ItemInserting` イベントハンドラーからリファクタリングされた `ValidPictureUpload(FileUpload)` メソッドコードは、次のとおりです。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample12.vb)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>手順 8: 元のカテゴリの画像を Jpg に置き換える

元の8つのカテゴリの画像は、OLE ヘッダーでラップされたビットマップファイルであることを思い出してください。 既存のレコード s 画像を編集する機能を追加したので、このビットマップを Jpg に置き換えてみましょう。 現在のカテゴリの画像を引き続き使用する場合は、次の手順を実行して Jpg に変換できます。

1. ビットマップイメージをハードドライブに保存します。 ブラウザーの [`UpdatingAndDeleting.aspx`] ページにアクセスし、最初の8つのカテゴリごとに画像を右クリックして、画像を保存することを選択します。
2. 選択したイメージエディターでイメージを開きます。 たとえば、Microsoft ペイントを使用することができます。
3. ビットマップを JPG イメージとして保存します。
4. JPG ファイルを使用して、編集インターフェイスでカテゴリ s 画像を更新します。

`DisplayCategoryPicture.aspx` ページは最初の8つのカテゴリの画像から最初の78バイトを削除しているので、カテゴリを編集して JPG イメージをアップロードした後、画像はブラウザーに表示されません。 これを修正するには、OLE ヘッダーの削除を実行するコードを削除します。 この操作を行った後、`DisplayCategoryPicture.aspx``Page_Load` イベントハンドラーには次のコードが含まれている必要があります。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample13.vb)]

> [!NOTE]
> `UpdatingAndDeleting.aspx` ページでは、インターフェイスの挿入と編集に少し多くの作業が使用されます。 DetailsView と GridView の `CategoryName` および `Description` BoundFields を TemplateFields に変換する必要があります。 `CategoryName` では `NULL` 値が許可されないため、RequiredFieldValidator を追加する必要があります。 `Description` テキストボックスは、複数行のテキストボックスに変換される可能性があります。 ここでは、これらの仕上げに触れます。

## <a name="summary"></a>要約

このチュートリアルでは、バイナリデータの使用方法について説明します。 このチュートリアルと前の3つでは、バイナリデータをファイルシステムに格納する方法、またはデータベース内に直接格納する方法について説明しました。 ユーザーは、ハードドライブからファイルを選択し、web サーバーにアップロードすることによって、システムにバイナリデータを提供します。このファイルは、ファイルシステムに格納したり、データベースに挿入したりすることができます。 ASP.NET 2.0 には、ドラッグアンドドロップと同様に、このようなインターフェイスを提供する FileUpload コントロールが含まれています。 ただし、[ファイルのアップロード](uploading-files-vb.md)に関するチュートリアルに記載されているように、FileUpload コントロールは、比較的小さなファイルのアップロードにのみ適しています。理想的には、メガバイトを超えてはなりません。 また、アップロードしたデータを基になるデータモデルに関連付ける方法と、既存のレコードからバイナリデータを編集および削除する方法についても説明しました。

次の一連のチュートリアルでは、さまざまなキャッシュ技法について説明します。 キャッシュは、負荷の高い操作から結果を取得し、より迅速にアクセスできる場所に格納することによって、アプリケーション全体のパフォーマンスを向上させる手段を提供します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](including-a-file-upload-option-when-adding-a-new-record-vb.md)
