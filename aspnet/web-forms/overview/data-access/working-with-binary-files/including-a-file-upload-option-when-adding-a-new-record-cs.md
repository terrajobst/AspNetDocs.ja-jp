---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
title: 新しいレコードを追加するときにファイルアップロードオプションをC#含める () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ユーザーがテキストデータを入力し、バイナリファイルをアップロードするための Web インターフェイスを作成する方法について説明します。 使用可能なオプションについて説明します...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 362ade25-3965-4fb2-88d2-835c4786244f
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
msc.type: authoredcontent
ms.openlocfilehash: f1287e180151b3034a7b90ef4b3f1fbe68354a09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576991"
---
# <a name="including-a-file-upload-option-when-adding-a-new-record-c"></a>新しいレコードを追加するとき、ファイル アップロード オプションを含める (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_CS.exe)または[PDF のダウンロード](including-a-file-upload-option-when-adding-a-new-record-cs/_static/datatutorial56cs1.pdf)

> このチュートリアルでは、ユーザーがテキストデータを入力し、バイナリファイルをアップロードするための Web インターフェイスを作成する方法について説明します。 バイナリデータを格納するために使用できるオプションを示すために、1つのファイルはデータベースに保存され、もう一方のファイルはファイルシステムに格納されます。

## <a name="introduction"></a>はじめに

前の2つのチュートリアルでは、application s データモデルに関連付けられているバイナリデータを格納する方法について説明しました。 FileUpload コントロールを使用してクライアントから web サーバーにファイルを送信する方法、およびこのバイナリデータをデータに表示する方法について説明しました。eb コントロール。 ただし、アップロードしたデータをデータモデルに関連付ける方法については、まだ説明していません。

このチュートリアルでは、新しいカテゴリを追加するための web ページを作成します。 カテゴリの名前と説明のテキストボックスに加えて、このページには2つの FileUpload コントロールを含める必要があります。1つは新しいカテゴリの画像用で、もう1つはパンフレット用です。 アップロードした画像は、[新しいレコード s `Picture`] 列に直接保存されます。一方、[新しいレコード] `BrochurePath` 列に保存されたファイルへのパスを使用して、`~/Brochures` フォルダーにパンフレットが保存されます。

この新しい web ページを作成する前に、アーキテクチャを更新する必要があります。 `CategoriesTableAdapter` s メインクエリでは、`Picture` 列は取得されません。 このため、自動生成される `Insert` メソッドには、`CategoryName`、`Description`、および `BrochurePath` の各フィールドの入力のみがあります。 そのため、4つのすべての `Categories` フィールドを入力するように求める、TableAdapter に追加のメソッドを作成する必要があります。 ビジネスロジック層の `CategoriesBLL` クラスも更新する必要があります。

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>手順 1:`CategoriesTableAdapter` に`InsertWithPicture`メソッドを追加する

「[データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)」チュートリアルで `CategoriesTableAdapter` を作成したときに、メインクエリに基づいて `INSERT`、`UPDATE`、および `DELETE` ステートメントを自動的に生成するように構成しました。 さらに、`Insert`、`Update`、および `Delete`メソッドを作成した DB Direct アプローチを採用するように TableAdapter に指示しました。 これらのメソッドは、自動生成された `INSERT`、`UPDATE`、および `DELETE` ステートメントを実行し、その結果、メインクエリによって返される列に基づいて入力パラメーターを受け取ります。 ファイルの[アップロード](uploading-files-cs.md)に関するチュートリアルでは、`BrochurePath` 列を使用するように `CategoriesTableAdapter` s メインクエリを拡張しました。

`CategoriesTableAdapter` s メインクエリは `Picture` 列を参照しないため、新しいレコードを追加したり、`Picture` 列の値を持つ既存のレコードを更新したりすることはできません。 この情報を取得するには、バイナリデータを含むレコードを挿入するために特に使用される、TableAdapter に新しいメソッドを作成するか、自動生成される `INSERT` ステートメントをカスタマイズします。 自動生成される `INSERT` ステートメントのカスタマイズに関する問題は、カスタマイズがウィザードによって上書きされる危険性があるということです。 たとえば、`Picture` 列を使用するように `INSERT` ステートメントをカスタマイズしたとします。 これにより、TableAdapter の `Insert` メソッドが更新され、category s picture s バイナリデータに対する追加の入力パラメーターが追加されます。 その後、ビジネスロジック層でメソッドを作成して、この DAL メソッドを使用し、プレゼンテーション層を介してこの BLL メソッドを呼び出すことができます。これにより、すべての処理がてされます。 つまり、次に TableAdapter 構成ウィザードを使用して TableAdapter を構成するまでの間です。 ウィザードが完了するとすぐに、`INSERT` ステートメントに対するカスタマイズが上書きされ、`Insert` メソッドが古い形式に戻り、コードはコンパイルされなくなります。

> [!NOTE]
> アドホック SQL ステートメントではなくストアドプロシージャを使用する場合、この問題は発生しません。 今後のチュートリアルでは、データアクセス層でアドホック SQL ステートメントの代わりにストアドプロシージャを使用する方法について説明します。

自動生成された SQL ステートメントをカスタマイズするのではなく、このような問題を回避するには、代わりに TableAdapter の新しいメソッドを作成します。 `InsertWithPicture`という名前のこのメソッドは、`CategoryName`、`Description`、`BrochurePath`、および `Picture` の各列の値を受け取り、4つのすべての値を新しいレコードに格納する `INSERT` ステートメントを実行します。

型指定されたデータセットを開き、デザイナーで `CategoriesTableAdapter` s ヘッダーを右クリックし、コンテキストメニューから [クエリの追加] を選択します。 これにより、tableadapter クエリの構成ウィザードが起動します。このウィザードでは、まず TableAdapter クエリがデータベースにアクセスする方法を尋ねます。 [SQL ステートメントを使用する] を選択し、[次へ] をクリックします。 次の手順では、生成するクエリの種類を指定します。 `Categories` テーブルに新しいレコードを追加するクエリを作成したので、[挿入] を選択し、[次へ] をクリックします。

[![[挿入] オプションを選択します。](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.png)

**図 1**: [挿入] オプションを選択[する (クリックすると、フルサイズの画像が表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.png)されます)

次に、`INSERT` SQL ステートメントを指定する必要があります。 このウィザードでは、TableAdapter のメインクエリに対応する `INSERT` ステートメントが自動的に提示されます。 この場合、`CategoryName`、`Description`、および `BrochurePath` の値を挿入する `INSERT` ステートメントです。 次のように、`@Picture` のパラメーターと共に `Picture` 列が含まれるようにステートメントを更新します。

[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample1.sql)]

ウィザードの最後の画面では、新しい TableAdapter メソッドに名前を指定するように求められます。 `InsertWithPicture` を入力し、[完了] をクリックします。

[新しい TableAdapter メソッド InsertWithPicture の ![名前](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.png)

**図 2**: 新しい TableAdapter メソッドに名前を指定[する `InsertWithPicture` (クリックすると、フルサイズのイメージが表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.png)されます)

## <a name="step-2-updating-the-business-logic-layer"></a>手順 2: ビジネスロジック層を更新する

プレゼンテーション層は、データアクセス層に直接アクセスするのをバイパスするのではなく、ビジネスロジック層とのみインターフェイスする必要があるため、先ほど作成した DAL メソッド (`InsertWithPicture`) を呼び出す BLL メソッドを作成する必要があります。 このチュートリアルでは、`InsertWithPicture` という名前の `CategoriesBLL` クラスにメソッドを作成します。このクラスは、3つの `string` s と `byte` の配列を入力として受け取ります。 `string` 入力パラメーターは、カテゴリの名前、説明、およびパンフレットファイルパス用であり、`byte` 配列は category s picture のバイナリコンテンツ用です。 次のコードに示すように、この BLL メソッドは対応する DAL メソッドを呼び出します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample2.cs)]

> [!NOTE]
> `InsertWithPicture` メソッドを BLL に追加する前に、型指定されたデータセットを保存したことを確認します。 `CategoriesTableAdapter` クラスコードは型指定されたデータセットに基づいて自動生成されるため、最初に変更を型指定されたデータセットに保存しない場合、`Adapter` プロパティは `InsertWithPicture` メソッドについて認識しません。

## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>手順 3: 既存のカテゴリとそのバイナリデータを一覧表示する

このチュートリアルでは、エンドユーザーがシステムに新しいカテゴリを追加するためのページを作成し、新しいカテゴリの画像とパンフレットを提供します。 前の[チュートリアル](displaying-binary-data-in-the-data-web-controls-cs.md)では、GridView と TemplateField と imagefield を使用して、各カテゴリの名前、説明、画像、およびそのパンフレットをダウンロードするためのリンクを表示しました。 このチュートリアルでは、この機能をレプリケートして、既存のすべてのカテゴリを一覧表示し、新しいものを作成できるページを作成します。

まず、`BinaryData` フォルダーから [`DisplayOrDownload.aspx`] ページを開きます。 ソースビューにアクセスし、GridView および ObjectDataSource s 宣言構文をコピーして、`UploadInDetailsView.aspx`の `<asp:Content>` 要素内に貼り付けます。 また、`DisplayOrDownload.aspx` の分離コードクラスから `UploadInDetailsView.aspx`に `GenerateBrochureLink` メソッドをコピーすることも忘れないでください。

[DisplayOrDownload から UploadInDetailsView .aspx に宣言型の構文をコピーして貼り付ける ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.png)

**図 3**: `DisplayOrDownload.aspx` から `UploadInDetailsView.aspx` に宣言構文をコピーして貼り付ける ([クリックしてフルサイズのイメージを表示する](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.png))

宣言構文と `GenerateBrochureLink` メソッドを `UploadInDetailsView.aspx` ページにコピーした後、ブラウザーを使用してページを表示し、すべてが正しくコピーされたことを確認します。 この GridView には、パンフレットと category s 画像をダウンロードするためのリンクを含む8つのカテゴリが一覧表示されています。

[![各カテゴリがそのバイナリデータと共に表示されるようになります。](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.png)

**図 4**: 各カテゴリがバイナリデータと共に表示されるようになりました ([クリックすると、フルサイズの画像が表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.png)される)

## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>手順 4: 挿入をサポートするための`CategoriesDataSource`の構成

現在 `Categories` GridView によって使用されている `CategoriesDataSource` ObjectDataSource では、データを挿入する機能が提供されていません。 このデータソースコントロールの挿入をサポートするには、その `Insert` メソッドを、基になるオブジェクトのメソッドにマップする必要があり `CategoriesBLL`ます。 特に、手順2、`InsertWithPicture`で追加した `CategoriesBLL` メソッドにマップする必要があります。

最初に、ObjectDataSource s スマートタグから [データソースの構成] リンクをクリックします。 最初の画面には、データソースが使用するように構成されているオブジェクト (`CategoriesBLL`) が表示されます。 この設定はそのままにして [次へ] をクリックし、[データメソッドの定義] 画面に進みます。 [挿入] タブに移動し、ドロップダウンリストから `InsertWithPicture` メソッドを選択します。 [完了] をクリックしてウィザードを終了します。

[InsertWithPicture メソッドを使用するように ObjectDataSource を構成 ![には](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.png)

**図 5**: `InsertWithPicture` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.png))

> [!NOTE]
> ウィザードを完了すると、フィールドとキーを更新するかどうかを確認するメッセージが表示され、データ Web コントロールのフィールドが再生成されます。 [はい] を選択すると、実行したフィールドのカスタマイズがすべて上書きされます。

ウィザードを完了すると、次の宣言型マークアップに示すように、ObjectDataSource には `InsertMethod` プロパティの値と4つのカテゴリの列の `InsertParameters` が含まれるようになります。

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>手順 5: 挿入インターフェイスの作成

[「データの挿入、更新、および削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)」で最初に説明したように、DetailsView コントロールには、挿入をサポートするデータソースコントロールを操作するときに使用できる組み込みの挿入インターフェイスが用意されています。 ここでは、挿入インターフェイスを永続的にレンダリングする GridView の上のページに DetailsView コントロールを追加します。これにより、ユーザーが新しいカテゴリをすばやく追加できるようになります。 DetailsView に新しいカテゴリを追加すると、その下にある GridView が自動的に更新され、新しいカテゴリが表示されます。

まず、[ツールボックス] から [DetailsView] を GridView のデザイナーにドラッグし、その `ID` プロパティを `NewCategory` に設定して、`Height` と `Width` のプロパティ値をクリアします。 DetailsView s スマートタグから既存の `CategoriesDataSource` にバインドし、[挿入を有効にする] チェックボックスをオンにします。

[DetailsView をカテゴリデータソースにバインドし、挿入を有効に ![には](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.png)

**図 6**: DetailsView を `CategoriesDataSource` にバインドし、挿入を有効にする ([クリックすると、フルサイズの画像が表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image12.png)されます)

挿入インターフェイスで DetailsView を完全にレンダリングするには、その `DefaultMode` プロパティを `Insert`に設定します。

DetailsView には、`CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`、および `BrochurePath` の5つの連結されたフィールドがありますが、`CategoryID` のプロパティが `InsertVisible` に設定されているため、挿入インターフェイスに `false`BoundField はレンダリングされません。 これらの BoundFields は、`GetCategories()` メソッドによって返される列であるため存在します。これは、ObjectDataSource がデータを取得するために呼び出すものです。 ただし、挿入の場合は、`NumberOfProducts`の値をユーザーに指定させないようにする必要があります。 さらに、新しいカテゴリの画像をアップロードしたり、そのパンフレットの PDF をアップロードしたりできるようにする必要があります。

DetailsView から `NumberOfProducts` BoundField を完全に削除してから、`CategoryName` と `BrochurePath` BoundFields の `HeaderText` プロパティをそれぞれ Category とパンフレットに更新します。 次に、`BrochurePath` BoundField を TemplateField に変換し、画像の新しい TemplateField を追加して、この新しい TemplateField `HeaderText` に Picture という値を与えます。 `Picture` TemplateField を `BrochurePath` TemplateField と CommandField の間に移動します。

![DetailsView をカテゴリデータソースにバインドし、挿入を有効にする](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.gif)

**図 7**: DetailsView を `CategoriesDataSource` にバインドし、挿入を有効にする

[フィールドの編集] ダイアログボックスを使用して `BrochurePath` BoundField を TemplateField に変換した場合、TemplateField には、`ItemTemplate`、`EditItemTemplate`、および `InsertItemTemplate`が含まれます。 ただし、必要なのは `InsertItemTemplate` だけです。そのため、他の2つのテンプレートを削除してもかまいません。 この時点で、DetailsView s 宣言構文は次のようになります。

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>パンフレットと画像のフィールドの FileUpload コントロールを追加する

現在、`BrochurePath` TemplateField s `InsertItemTemplate` にはテキストボックスが含まれていますが、`Picture` の TemplateField にはテンプレートが含まれていません。 FileUpload コントロールを使用するには、これらの2つの TemplateField s `InsertItemTemplate` s を更新する必要があります。

DetailsView s スマートタグから、[テンプレートの編集] オプションを選択し、ドロップダウンリストから `BrochurePath` TemplateField s `InsertItemTemplate` を選択します。 テキストボックスを削除し、FileUpload コントロールをツールボックスからテンプレートにドラッグします。 FileUpload コントロール s `ID` を `BrochureUpload`に設定します。 同様に、FileUpload コントロールを `Picture` TemplateField s `InsertItemTemplate`に追加します。 この FileUpload コントロール s `ID` を `PictureUpload`に設定します。

[FileUpload コントロールを Insertitemposition に追加 ![には](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image13.png)

**図 8**: `InsertItemTemplate` に FileUpload コントロールを追加する ([クリックすると、フルサイズの画像が表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image14.png)されます)

これらの追加を行った後、2つの TemplateField s 宣言構文は次のようになります。

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample5.aspx)]

ユーザーが新しいカテゴリを追加するときに、パンフレットと画像が正しいファイルの種類であることを確認します。 パンフレットの場合、ユーザーは PDF を提供する必要があります。 画像の場合、ユーザーはイメージファイルをアップロードする必要がありますが、画像ファイルや、Gif や Jpg など、特定の種類のイメージファイルのみ*を許可し*ますか。 さまざまなファイルの種類に対応するために、`Categories` スキーマを拡張して、ファイルの種類をキャプチャする列を含める必要があります。これにより、`DisplayCategoryPicture.aspx`の `Response.ContentType` を通じてこの型をクライアントに送信できるようになります。 このような列を持っていないので、ユーザーが特定の画像ファイルの種類のみを提供するように制限することは賢明です。 `Categories` table s の既存の画像はビットマップですが、Jpg は web 経由で提供される画像に適したファイル形式です。

ユーザーが正しくないファイルの種類をアップロードした場合は、挿入をキャンセルし、問題を示すメッセージを表示する必要があります。 DetailsView の下にラベル Web コントロールを追加します。 `ID` プロパティを `UploadWarning`に設定し、`Text` プロパティをオフにします。 `CssClass` プロパティを Warning に設定し、`Visible` プロパティと `EnableViewState` プロパティを `false`に設定します。 `Warning` CSS クラスは `Styles.css` で定義され、大きな、赤、斜体、太字のフォントでテキストをレンダリングします。

> [!NOTE]
> 理想的には、`CategoryName` および `Description` BoundFields を TemplateFields に変換し、その挿入インターフェイスをカスタマイズします。 たとえば、`Description` の挿入インターフェイスは、複数行のテキストボックスを使用する方が適している場合があります。 また、`CategoryName` 列では `NULL` 値が受け付けられないため、RequiredFieldValidator を追加して、ユーザーが新しいカテゴリ名の値を確実に提供するようにする必要があります。 これらの手順は、読者のための演習として残されています。 データ変更インターフェイスの詳細については、「[データ変更インターフェイスのカスタマイズ](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)」を参照してください。

## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>手順 6: アップロードしたパンフレットを Web サーバーのファイルシステムに保存する

ユーザーが新しいカテゴリの値を入力して [挿入] ボタンをクリックすると、ポストバックが発生し、挿入ワークフローが上されます。 まず、DetailsView s [`ItemInserting` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx)が発生します。 次に、ObjectDataSource s `Insert()` メソッドが呼び出され、その結果、`Categories` テーブルに新しいレコードが追加されます。 その後、DetailsView s [`ItemInserted` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx)が発生します。

ObjectDataSource s `Insert()` メソッドが呼び出される前に、適切なファイルの種類がユーザーによってアップロードされたことを確認し、その後、web サーバーのファイルシステムにパンフレット PDF を保存する必要があります。 DetailsView s `ItemInserting` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample6.cs)]

イベントハンドラーは、DetailsView s テンプレートから `BrochureUpload` FileUpload コントロールを参照することによって開始されます。 次に、パンフレットがアップロードされている場合、アップロードされたファイルの拡張子が調べられます。 拡張機能がではない場合。PDF では、警告が表示され、挿入が取り消され、イベントハンドラーの実行が終了します。

> [!NOTE]
> アップロードしたファイルの拡張子に依存することは、アップロードされたファイルが PDF ドキュメントであることを保証するための、確実な方法ではありません。 ユーザーは、拡張子が `.Brochure`の有効な PDF ドキュメントを作成したり、PDF 以外のドキュメントを取得して `.pdf` の拡張子を付けたりすることができます。 ファイルの種類をさらに効果に確認するには、ファイルのバイナリコンテンツをプログラムで調べておく必要があります。 ただし、このような一般的なアプローチは過剰です。ほとんどのシナリオでは、拡張機能を確認するだけで十分です。

[ファイル](uploading-files-cs.md)のアップロードに関するチュートリアルで説明したように、ファイルをファイルシステムに保存するときは注意が必要です。これにより、1人のユーザーのアップロードで別のが上書きされることはありません。 このチュートリアルでは、アップロードしたファイルと同じ名前を使用しようとします。 ただし、同じファイル名のファイルが `~/Brochures` ディレクトリに既に存在する場合は、一意の名前が見つかるまで、末尾に数字を追加します。 たとえば、ユーザーが `Meats.pdf`という名前のパンフレットファイルをアップロードしても、`~/Brochures` フォルダーに `Meats.pdf` という名前のファイルが既に存在する場合は、保存したファイル名を `Meats-1.pdf`に変更します。 それが存在する場合は、一意のファイル名が見つかるまで、`Meats-2.pdf`します。

次のコードでは、 [`File.Exists(path)` メソッド](https://msdn.microsoft.com/library/system.io.file.exists.aspx)を使用して、指定したファイル名のファイルが既に存在するかどうかを確認します。 その場合は、競合が見つからなくなるまで、パンフレットの新しいファイル名を試してみてください。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample7.cs)]

有効なファイル名が見つかったら、ファイルをファイルシステムに保存する必要があります。また、このファイル名がデータベースに書き込まれるように ObjectDataSource s `brochurePath``InsertParameter` 値を更新する必要があります。 *ファイルのアップロード*に関するチュートリアルに戻ってきたように、FileUpload control s `SaveAs(path)` メソッドを使用してファイルを保存できます。 ObjectDataSource s `brochurePath` パラメーターを更新するには、`e.Values` コレクションを使用します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample8.cs)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>手順 7: アップロードした画像をデータベースに保存する

アップロードした画像を新しい `Categories` レコードに保存するには、アップロードされたバイナリコンテンツを DetailsView s `ItemInserting` イベントの ObjectDataSource s `picture` パラメーターに割り当てる必要があります。 ただし、この割り当てを行う前に、アップロードした画像が、他の種類のイメージではなく、JPG であることを確認する必要があります。 手順 6. と同様に、アップロードした画像のファイル拡張子を使用して、その種類を確認します。

`Categories` テーブルでは `Picture` 列の値を `NULL` ことができますが、すべてのカテゴリには現在画像があります。 このページを使用して新しいカテゴリを追加するときに、によってユーザーに画像が提供されるようにします。 次のコードでは、画像がアップロードされていること、および適切な拡張子を持っていることを確認します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample9.cs)]

このコードは、手順6のコードの*前に*配置して、画像のアップロードで問題が発生した場合に、パンフレットファイルがファイルシステムに保存される前にイベントハンドラーが終了するようにする必要があります。

適切なファイルがアップロードされていることを前提として、アップロードしたバイナリコンテンツを picture parameter s 値に割り当てます。次のコード行を使用します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample10.cs)]

## <a name="the-completeiteminsertingevent-handler"></a>Complete`ItemInserting`イベントハンドラー

完全を期すために、`ItemInserting` イベントハンドラー全体を次に示します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample11.cs)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>手順 8:`DisplayCategoryPicture.aspx`ページを修正する

ここでは、最後のいくつかの手順で作成した、挿入インターフェイスと `ItemInserting` イベントハンドラーをテストします。 ブラウザーを使用して `UploadInDetailsView.aspx` のページにアクセスし、カテゴリを追加したり、画像を省略したり、JPG 以外の画像や PDF 以外のパンフレットを指定したりします。 いずれの場合も、エラーメッセージが表示され、挿入ワークフローが取り消されます。

[無効なファイルの種類がアップロードされた場合に警告メッセージが表示される ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image15.png)

**図 9**: 無効なファイルの種類がアップロードされた場合に警告メッセージが表示される ([クリックすると、フルサイズの画像が表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image16.png)されます)

ページで画像をアップロードする必要があることを確認し、PDF 以外のファイルまたは JPG 以外のファイルを受け入れないことを確認したら、有効な JPG 画像を含む新しいカテゴリを追加して、[パンフレット] フィールドを空のままにします。 [挿入] ボタンをクリックすると、ページがポストバックされ、`Categories` テーブルに新しいレコードが追加されます。アップロードした画像は、データベースに直接格納されています。 GridView が更新され、新しく追加されたカテゴリの行が表示されますが、図10に示すように、新しい category s 画像は正しくレンダリングされません。

[新しいカテゴリ s の画像が表示されていない ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image17.png)

**図 10**: 新しいカテゴリの画像は表示されません ([クリックすると、フルサイズの画像が表示](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image18.png)されます)

新しい画像が表示されない理由は、指定されたカテゴリの画像を返す `DisplayCategoryPicture.aspx` ページが OLE ヘッダーを持つビットマップを処理するように構成されているためです。 この78バイトヘッダーは、クライアントに返される前に、`Picture` の列のバイナリコンテンツから削除されます。 しかし、新しいカテゴリにアップロードした JPG ファイルには、この OLE ヘッダーがありません。そのため、有効なバイト数がイメージのバイナリデータから削除されます。

`Categories` テーブルに OLE ヘッダーと Jpg の両方のビットマップがあるため、元の8つのカテゴリの OLE ヘッダーを削除し、新しいカテゴリレコードに対してこの削除をバイパスするように `DisplayCategoryPicture.aspx` を更新する必要があります。 次のチュートリアルでは、既存のレコード s 画像を更新する方法を確認し、古いカテゴリの画像をすべて更新して Jpg にします。 ただし現時点では、`DisplayCategoryPicture.aspx` で次のコードを使用して、元の8つのカテゴリについてのみ OLE ヘッダーを削除します。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample12.cs)]

この変更により、JPG イメージが GridView で正しくレンダリングされるようになりました。

[新しいカテゴリの JPG イメージが正しくレンダリングされる ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image19.png)

**図 11**: 新しいカテゴリの JPG イメージが正しくレンダリングされる ([クリックしてフルサイズのイメージを表示する](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image20.png))

## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>手順 9: 例外が発生したときにパンフレットを削除する

バイナリデータを web サーバーのファイルシステムに格納する場合の課題の1つは、データモデルとそのバイナリデータの間に切断を導入することです。 したがって、レコードが削除されるたびに、ファイルシステム上の対応するバイナリデータも削除する必要があります。 これは、挿入時にも再生されることがあります。 次のシナリオを考えてみます。ユーザーは、有効な画像とパンフレットを指定して新しいカテゴリを追加します。 [挿入] ボタンをクリックすると、ポストバックが発生し、DetailsView s `ItemInserting` イベントが発生して、web サーバーのファイルシステムにパンフレットが保存されます。 次に、ObjectDataSource s `Insert()` メソッドが呼び出されます。このメソッドは、`CategoriesTableAdapter` s `InsertWithPicture` メソッドを呼び出す `CategoriesBLL` クラス s `InsertWithPicture` メソッドを呼び出します。

ここで、データベースがオフラインの場合、または `INSERT` SQL ステートメントにエラーがある場合はどうなるでしょうか。 明示的に挿入が失敗するため、新しいカテゴリ行はデータベースに追加されません。 しかし、web サーバー s ファイルシステム上には、アップロードされたパンフレットファイルが残っています。 このファイルは、挿入ワークフロー中に例外が発生したときに削除する必要があります。

前に説明したように、 [ASP.NET Page チュートリアルでは、BLL と DAL レベルの例外を処理](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)します。アーキテクチャの深度内から例外がスローされると、さまざまなレイヤーによってバブルアップされます。 プレゼンテーション層で、DetailsView s `ItemInserted` イベントから例外が発生したかどうかを判断できます。 このイベントハンドラーは、ObjectDataSource s `InsertParameters`の値も提供します。 そのため、例外が発生したかどうかを確認し、存在する場合は ObjectDataSource s `brochurePath` パラメーターによって指定されたファイルを削除する `ItemInserted` イベントのイベントハンドラーを作成できます。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample13.cs)]

## <a name="summary"></a>要約

バイナリデータを含むレコードを追加するための web ベースのインターフェイスを提供するために、いくつかの手順を実行する必要があります。 バイナリデータがデータベースに直接格納されている場合、アーキテクチャを更新し、バイナリデータが挿入されるケースを処理するための特定のメソッドを追加する必要が生じる可能性があります。 アーキテクチャが更新されたら、次の手順では挿入インターフェイスを作成します。これは、バイナリデータフィールドごとに FileUpload コントロールを含めるようにカスタマイズされた DetailsView を使用して実現できます。 アップロードされたデータは、web サーバーのファイルシステムに保存するか、または DetailsView s `ItemInserting` イベントハンドラーのデータソースパラメーターに割り当てることができます。

バイナリデータをファイルシステムに保存する場合は、データをデータベースに直接保存するよりも計画を立てる必要があります。 1人のユーザーのアップロードで別のが上書きされないようにするために、名前付けスキームを選択する必要があります。 また、データベースの挿入が失敗した場合に、アップロードされたファイルを削除するには、追加の手順を実行する必要があります。

これで、パンフレットや画像を使用してシステムに新しいカテゴリを追加できるようになりましたが、既存のカテゴリのバイナリデータを更新する方法や、削除されたカテゴリのバイナリデータを正しく削除する方法についても説明しています。 次のチュートリアルでは、これらの2つのトピックについて説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Dave Gardner、Teresa Murphy、Bernadette Leigh でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](displaying-binary-data-in-the-data-web-controls-cs.md)
> [次へ](updating-and-deleting-existing-binary-data-cs.md)
