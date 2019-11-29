---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-cs
title: データ Web コントロールにバイナリデータを表示するC#() |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、Web ページにバイナリデータを表示するためのオプションについて説明します。これには、イメージファイルの表示や、"ダウンロード" リンク (f...) のプロビジョニングなどが含まれます。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 5cbeb9f8-5f92-4ba8-87ae-0b4d460ae6d4
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: f38de7adcd77b3dc2622759646168cf533b8308f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642542"
---
# <a name="displaying-binary-data-in-the-data-web-controls-c"></a>データ Web コントロールにバイナリ データを表示する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_CS.exe)または[PDF のダウンロード](displaying-binary-data-in-the-data-web-controls-cs/_static/datatutorial55cs1.pdf)

> このチュートリアルでは、Web ページにバイナリデータを表示するためのオプションについて説明します。これには、画像ファイルの表示や PDF ファイルの ' ダウンロード ' リンクのプロビジョニングなどが含まれます。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、バイナリデータをアプリケーションの基になるデータモデルに関連付け、FileUpload コントロールを使用してブラウザーから web サーバーのファイルシステムにファイルをアップロードする2つの手法について説明しました。 アップロードしたバイナリデータをデータモデルに関連付ける方法については、まだ説明していません。 つまり、ファイルがアップロードされ、ファイルシステムに保存された後、ファイルへのパスが適切なデータベースレコードに格納されている必要があります。 データがデータベースに直接格納されている場合は、アップロードされたバイナリデータをファイルシステムに保存する必要はありませんが、データベースに挿入する必要があります。

データモデルにデータを関連付ける前に、まず、バイナリデータをエンドユーザーに提供する方法を見てみましょう。 テキストデータの表示は簡単ですが、バイナリデータを表示するにはどうすればよいでしょうか。 もちろん、バイナリデータの種類によって異なります。 イメージの場合、イメージを表示することが必要になることがあります。Pdf、Microsoft Word 文書、ZIP ファイル、およびその他の種類のバイナリデータについては、ダウンロードリンクを提供する方が適しています。

このチュートリアルでは、GridView や DetailsView などのデータ Web コントロールを使用して、関連するテキストデータと共にバイナリデータを表示する方法について説明します。 次のチュートリアルでは、アップロードしたファイルをデータベースに関連付けることに注目します。

## <a name="step-1-providingbrochurepathvalues"></a>手順 1:`BrochurePath`値を指定する

`Categories` テーブルの `Picture` 列には、さまざまなカテゴリイメージのバイナリデータが既に含まれています。 具体的には、各レコードの `Picture` 列には、粗く、低品質、16色のビットマップイメージのバイナリコンテンツが保持されます。 各カテゴリの画像は172ピクセル幅、高さは120ピクセル、約 11 KB を消費します。 さらに、[`Picture`] 列のバイナリコンテンツには、イメージを表示する前に削除する必要がある78バイトの[OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding)ヘッダーが含まれています。 このヘッダー情報は、Northwind データベースのルートが Microsoft Access にあるために存在します。 Access では、バイナリデータは OLE オブジェクトデータ型を使用して格納されます。このデータ型は、このヘッダーに tacks ます。 ここでは、画像を表示するために、これらの低品質のイメージからヘッダーを削除する方法について説明します。 今後のチュートリアルでは、category s `Picture` 列を更新するためのインターフェイスを作成し、OLE ヘッダーを使用するビットマップイメージを、不要な OLE ヘッダーを含まない同等の JPG イメージに置き換えます。

前のチュートリアルでは、FileUpload コントロールの使用方法を説明しました。 そのため、web サーバーのファイルシステムにパンフレットファイルを追加することができます。 ただし、この操作を行っても、`Categories` テーブルの `BrochurePath` 列は更新されません。 次のチュートリアルでは、これを実現する方法を説明しますが、ここでは、この列の値を手動で指定する必要があります。

このチュートリアルのダウンロードでは、[`~/Brochures`] フォルダーに7つの PDF パンフレットファイルがあり、シーフードを除く各カテゴリに対応しています。 ここでは、すべてのレコードにバイナリデータが関連付けられているわけではないシナリオの処理方法を示すために、シーフードのパンフレットの追加を省略しました。 これらの値を使用して `Categories` テーブルを更新するにはサーバーエクスプローラーから [`Categories`] ノードを右クリックし、[テーブルデータの表示] をクリックします。 次に、図1に示すように、各カテゴリのパンフレットファイルへの仮想パスを入力します。 シーフードカテゴリのパンフレットは存在しないため、`BrochurePath` 列の値は `NULL`としてそのままにします。

[![手動でカテゴリテーブル s BrochurePath 列の値を入力する](displaying-binary-data-in-the-data-web-controls-cs/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image1.png)

**図 1**: `Categories` Table s `BrochurePath` 列の値を手動で入力[する (クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image2.png)されます)

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>手順 2: GridView でのパンフレットへのダウンロードリンクの提供

`Categories` テーブルに指定された `BrochurePath` 値を使用して、各カテゴリとカテゴリ s パンフレットをダウンロードするためのリンクを一覧表示する GridView を作成する準備ができました。 手順4では、この GridView を拡張してカテゴリ s イメージも表示します。

まず、GridView をツールボックスから `BinaryData` フォルダーの [`DisplayOrDownloadData.aspx`] ページのデザイナーにドラッグします。 GridView s `ID` を `Categories` に設定し、GridView s スマートタグを使用して、新しいデータソースにバインドするように選択します。 具体的には、`CategoriesBLL` object s `GetCategories()` メソッドを使用してデータを取得する `CategoriesDataSource` という名前の ObjectDataSource にバインドします。

[新しい ObjectDataSource という名前の新しい名前のデータソースを作成 ![には](displaying-binary-data-in-the-data-web-controls-cs/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image3.png)

**図 2**: `CategoriesDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image4.png)される)

[カテゴリ Bll クラスを使用するように ObjectDataSource を構成 ![には](displaying-binary-data-in-the-data-web-controls-cs/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image5.png)

**図 3**: `CategoriesBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](displaying-binary-data-in-the-data-web-controls-cs/_static/image6.png))

[GetCategories () メソッドを使用してカテゴリの一覧を取得 ![には](displaying-binary-data-in-the-data-web-controls-cs/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image7.png)

**図 4**: `GetCategories()` メソッドを使用してカテゴリの一覧を取得[する (クリックしてフルサイズのイメージを表示する](displaying-binary-data-in-the-data-web-controls-cs/_static/image8.png))

データソースの構成ウィザードを完了すると、Visual Studio によって、`CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`、および `BrochurePath` `DataColumn` の `Categories` GridView に BoundField が自動的に追加されます。 `GetCategories()` メソッド s クエリがこの情報を取得しないため、`NumberOfProducts` BoundField を削除します。 また、`CategoryID` BoundField を削除し、`CategoryName` と `BrochurePath` BoundFields `HeaderText` プロパティの名前をそれぞれ Category とパンフレットにそれぞれ変更します。 これらの変更を行った後、GridView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample1.aspx)]

ブラウザーを使用してこのページを表示します (図5を参照)。 8つのカテゴリがそれぞれ一覧表示されます。 `BrochurePath` 値を持つ7つのカテゴリの `BrochurePath` 値は、それぞれの BoundField に表示されます。 `BrochurePath`の `NULL` 値を持つシーフードには、空のセルが表示されます。

[各カテゴリの [名前]、[説明]、および [BrochurePath] の値が表示されます。 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image9.png)

**図 5**: 各カテゴリの名前、説明、および `BrochurePath` 値が表示されます ([クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image10.png)されます)

`BrochurePath` 列のテキストを表示するのではなく、パンフレットへのリンクを作成します。 これを行うには、`BrochurePath` BoundField を削除し、ハイパーリンクフィールドに置き換えます。 新しいハイパーリンクフィールド s `HeaderText` プロパティを「パンフレット」に、その `Text` プロパティを「パンフレット」、`DataNavigateUrlFields` プロパティを「`BrochurePath`」に設定します。

![BrochurePath のハイパーリンクフィールドを追加する](displaying-binary-data-in-the-data-web-controls-cs/_static/image6.gif)

**図 6**: `BrochurePath` のハイパーリンクフィールドを追加する

これにより、図7に示すように、GridView にリンクの列が追加されます。 [パンフレットの表示] リンクをクリックすると、ブラウザーに PDF が直接表示されるか、または PDF リーダーがインストールされているかどうか、およびブラウザーの設定に応じて、ファイルのダウンロードをユーザーに促すメッセージが表示されます。

[[パンフレットの表示] リンクをクリックすると、カテゴリ s のパンフレットを表示でき ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image11.png)

**図 7**: [パンフレットを表示] リンクをクリックするとカテゴリ s のパンフレットを表示できる ([クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image12.png)されます)

[カテゴリ s のパンフレット PDF が表示され ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image13.png)

**図 8**: カテゴリ s のパンフレット PDF が表示される ([クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image14.png)されます)

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>パンフレットのないカテゴリのビューパンフレットのテキストを非表示にする

図7に示すように、[`BrochurePath` のハイパーリンク] フィールドには、`BrochurePath`に`NULL` 以外の値があるかどうかに関係なく、すべてのレコードの `Text` プロパティ値 (ビューのパンフレット) が表示されます。 もちろん、`BrochurePath` が `NULL`場合、シーフードカテゴリの場合と同様に、リンクはテキストとしてのみ表示されます (図7を参照)。 テキストビューのパンフレットを表示するのではなく、`BrochurePath` の値を持たないカテゴリには、利用可能なパンフレットがないなどの代替テキストを表示すると便利な場合があります。

この動作を実現するには、`BrochurePath` 値に基づいて適切な出力を生成するページメソッドへの呼び出しによって、コンテンツが生成される TemplateField を使用する必要があります。 この書式設定の手法については、最初に GridView コントロールのチュートリアルの[「TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 」で説明しています。

[ハイパーリンク] フィールドを TemplateField に変換します。そのためには、[`BrochurePath` ハイパーリンク] フィールドを選択し、[列の編集] ダイアログボックスの [このフィールドを TemplateField に変換] リンクをクリックします。

![ハイパーリンクフィールドを TemplateField に変換します。](displaying-binary-data-in-the-data-web-controls-cs/_static/image9.gif)

**図 9**: ハイパーリンクフィールドを TemplateField に変換する

これにより、`NavigateUrl` プロパティが `BrochurePath` 値にバインドされたハイパーリンク Web コントロールを含む `ItemTemplate` の TemplateField が作成されます。 このマークアップをメソッド `GenerateBrochureLink`の呼び出しに置き換え、`BrochurePath`の値を渡します。

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample2.aspx)]

次に、`string` を返し、入力パラメーターとして `object` を受け入れる `GenerateBrochureLink` という名前の ASP.NET page s 分離コードクラスに `protected` メソッドを作成します。

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample3.cs)]

このメソッドは、渡された `object` 値がデータベース `NULL` かどうかを確認し、存在する場合は、そのカテゴリにパンフレットがないことを示すメッセージを返します。 それ以外の場合、`BrochurePath` 値があると、その値はハイパーリンクに表示されます。 `BrochurePath` の値が存在する場合は、 [`ResolveUrl(url)` メソッド](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)に渡されることに注意してください。 このメソッドは、渡された*url*を解決し、`~` の文字を適切な仮想パスに置き換えます。 たとえば、アプリケーションが `/Tutorial55`をルートとしている場合、`ResolveUrl("~/Brochures/Meats.pdf")` は `/Tutorial55/Brochures/Meat.pdf`を返します。

図10は、これらの変更が適用された後のページを示しています。 シーフード category s `BrochurePath` フィールドに、[利用可能なパンフレットがありません] というテキストが表示されることに注意してください。

[テキスト ![、パンフレットのないカテゴリには [利用可能なパンフレットがありません] と表示されます。](displaying-binary-data-in-the-data-web-controls-cs/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image15.png)

**図 10**: パンフレットのないカテゴリには、[利用可能なパンフレットがありません] というテキストが表示されます ([クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image16.png)されます)

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>手順 3: カテゴリ s の画像を表示するための Web ページの追加

ユーザーが ASP.NET ページにアクセスすると、ASP.NET page s HTML が表示されます。 受信した HTML はテキストのみで、バイナリデータは含まれません。 画像、サウンドファイル、Macromedia Flash アプリケーション、埋め込みの Windows Media Player ビデオなどの追加のバイナリデータは、web サーバー上に個別のリソースとして存在します。 HTML にはこれらのファイルへの参照が含まれていますが、ファイルの実際の内容は含まれていません。

たとえば、HTML では、`<img>` 要素を使用して画像を参照し、次のように `src` 属性でイメージファイルをポイントします。

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample4.html)]

ブラウザーは、この HTML を受け取ると、web サーバーに対して別の要求を行い、イメージファイルのバイナリコンテンツを取得して、ブラウザーに表示します。 バイナリデータにも同じ概念が適用されます。 手順2では、ページ s HTML マークアップの一部として、このパンフレットはブラウザーに送信されませんでした。 代わりに、レンダリングされた HTML には、ブラウザーが PDF ドキュメントを直接要求したというハイパーリンクが用意されています。

ユーザーがデータベース内に存在するバイナリデータを表示またはダウンロードできるようにするには、データを返す別の web ページを作成する必要があります。 このアプリケーションでは、1つのバイナリデータフィールドが、カテゴリの画像としてデータベースに直接格納されています。 そのため、呼び出されたときに特定のカテゴリの画像データを返すページが必要です。

`DisplayCategoryPicture.aspx`という名前の `BinaryData` フォルダーに新しい ASP.NET ページを追加します。 この場合、[マスターページの選択] チェックボックスはオフのままにしておきます。 このページでは、querystring に `CategoryID` 値が必要であり、そのカテゴリ `Picture` 列のバイナリデータを返します。 このページはバイナリデータを返すので、それ以外の場合は HTML セクションでマークアップを必要としません。 そのため、左下隅にある [ソース] タブをクリックし、`<%@ Page %>` ディレクティブ以外のすべてのページマークアップを削除します。 つまり、`DisplayCategoryPicture.aspx` s 宣言マークアップは単一行で構成する必要があります。

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample5.aspx)]

`<%@ Page %>` ディレクティブに `MasterPageFile` 属性が表示されている場合は、削除します。

ページの分離コードクラスで、`Page_Load` イベントハンドラーに次のコードを追加します。

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample6.cs)]

このコードでは、まず、`CategoryID` querystring の値を `categoryID`という名前の変数に読み取ります。 次に、`CategoriesBLL` クラス s `GetCategoryWithBinaryDataByCategoryID(categoryID)` メソッドの呼び出しを使用して画像データを取得します。 このデータは `Response.BinaryWrite(data)` メソッドを使用してクライアントに返されますが、このが呼び出される前に、`Picture` 列の値 s OLE ヘッダーを削除する必要があります。 これを行うには `strippedImageData` という名前の `byte` 配列を作成します。これにより、`Picture` 列の値よりも正確に78文字が保持されます。 [`Array.Copy` メソッド](https://msdn.microsoft.com/library/z50k9bft.aspx)を使用して、78の `category.Picture` の位置から `strippedImageData`にデータをコピーします。

`Response.ContentType` プロパティは、返されるコンテンツの[MIME の種類](http://en.wikipedia.org/wiki/MIME)を指定します。これにより、ブラウザーでのレンダリング方法が認識されます。 `Categories` table s `Picture` 列はビットマップイメージであるため、ここではビットマップ MIME タイプ (image/bmp) を使用します。 MIME の種類を省略した場合でも、ほとんどのブラウザーでイメージが正しく表示されます。これは、イメージファイルのバイナリデータの内容に基づいて型を推論できるためです。 ただし、可能な場合は、MIME の種類を含めることをお勧めします。 [MIME メディアの種類](http://www.iana.org/assignments/media-types/)の完全な一覧については、[インターネットの割り当て番号機関 s の web サイト](http://www.iana.org/)を参照してください。

このページを作成すると、`DisplayCategoryPicture.aspx?CategoryID=categoryID`にアクセスすることで、特定のカテゴリの画像を表示できます。 図11に、`DisplayCategoryPicture.aspx?CategoryID=1`から表示できる飲み物のカテゴリ s の画像を示します。

[飲料カテゴリ s の画像が表示され ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image17.png)

**図 11**: 飲料カテゴリ s の画像が表示される ([クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image18.png)されます)

`DisplayCategoryPicture.aspx?CategoryID=categoryID`を参照しているときに、' system.string ' 型のオブジェクトを ' system.string [] ' 型にキャストできないという例外が発生した場合は、次の2つの原因が考えられます。 まず、`Categories` table s `Picture` 列に `NULL` 値が許可されます。 ただし、`DisplayCategoryPicture.aspx` のページでは、`NULL` 以外の値が存在することを前提としています。 `NULL` 値がある場合、`CategoriesDataTable` の `Picture` プロパティに直接アクセスすることはできません。 `Picture` 列に `NULL` 値を許可する場合は、次の条件を含める必要があります。

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample7.cs)]

上のコードでは、`Images` フォルダーに `NoPictureAvailable.gif` という名前のイメージファイルがあり、画像を使用せずに表示することを前提としています。

この例外は、`CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` method s `SELECT` ステートメントがメインクエリの列一覧に戻された場合にも発生する可能性があります。これは、アドホック SQL ステートメントを使用していて、TableAdapter のメインクエリに対してウィザードを再実行した場合に発生する可能性があります。 `GetCategoryWithBinaryDataByCategoryID` メソッド s `SELECT` ステートメントに `Picture` 列が含まれていることを確認します。

> [!NOTE]
> `DisplayCategoryPicture.aspx` にアクセスするたびに、データベースにアクセスし、指定されたカテゴリの画像データが返されます。 ユーザーが最後に表示した後にカテゴリ s の画像が変更されていない場合、これは無駄な作業です。 幸い、HTTP では*条件付き*のを使用できます。 条件付きの GET を使用すると、HTTP 要求を行うクライアントは、クライアントがこのリソースを web サーバーから最後に取得した日時を示す[`If-Modified-Since` http ヘッダー](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)に従って送信されます。 この指定した日付以降にコンテンツが変更されていない場合、web サーバーは、変更されて[いない状態コード (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)で応答し、要求されたリソースのコンテンツを済ませる返送することができます。 つまり、この方法を使用すると、クライアントが最後にアクセスした後に変更されていない場合に、web サーバーはリソースのコンテンツを再度送信する必要がなくなります。

ただし、この動作を実装するには、`Picture` 列が最後に更新されたときにキャプチャする `Categories` テーブルに `PictureLastModified` 列を追加し、`If-Modified-Since` ヘッダーをチェックするコードを追加する必要があります。 `If-Modified-Since` ヘッダーと条件付き取得ワークフローの詳細については、「 [RSS ハッカー向け Http 条件付き get](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) 」と「 [ASP.NET ページでの Http 要求の実行](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)」を参照してください。

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>手順 4: GridView でカテゴリの画像を表示する

これで、特定のカテゴリの画像を表示する web ページが作成されました。ここで、[画像 web コントロール](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx)または HTML `<img>` 要素を使用して、`DisplayCategoryPicture.aspx?CategoryID=categoryID`をポイントします。 URL がデータベースデータによって決定される画像は、イメージフィールドを使用して GridView または DetailsView に表示できます。 ImageField には、ハイパーリンクフィールド s `DataNavigateUrlFields` および `DataNavigateUrlFormatString` プロパティのように機能するプロパティと `DataImageUrlFormatString` プロパティ `DataImageUrlField` が含まれています。

では、各カテゴリの画像を表示するために ImageField を追加することで、`DisplayOrDownloadData.aspx` の `Categories` GridView を強化します。 ImageField を追加し、その `DataImageUrlField` と `DataImageUrlFormatString` プロパティをそれぞれ `CategoryID` および `DisplayCategoryPicture.aspx?CategoryID={0}`に設定するだけです。 これにより、`src` 属性が `DisplayCategoryPicture.aspx?CategoryID={0}`を参照する `<img>` 要素を表示する GridView 列が作成されます。ここで {0} は GridView 行 s `CategoryID` 値に置き換えられます。

![ImageField を GridView に追加する](displaying-binary-data-in-the-data-web-controls-cs/_static/image12.gif)

**図 12**: GridView に imagefield を追加する

ImageField を追加した後、GridView の宣言構文は次のようになります。

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample8.aspx)]

ブラウザーを使用してこのページを表示します。 各レコードにカテゴリの画像が含まれるようになったことに注意してください。

[各行にカテゴリ s の画像が表示さ ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image19.png)

**図 13**: 各行にカテゴリ s の画像が表示される ([クリックすると、フルサイズの画像が表示](displaying-binary-data-in-the-data-web-controls-cs/_static/image20.png)されます)

## <a name="summary"></a>要約

このチュートリアルでは、バイナリデータを表示する方法について説明します。 データの表示方法は、データの種類によって異なります。 PDF のパンフレットファイルの場合、ユーザーに [ビューのパンフレット] リンクが用意されています。このリンクをクリックすると、ユーザーが直接 PDF ファイルに表示されます。 Category s picture では、まずデータベースからバイナリデータを取得して返すページを作成し、そのページを使用して、GridView に各カテゴリの画像を表示しました。

これで、バイナリデータを表示する方法を確認できました。次は、バイナリデータを使用してデータベースに対して挿入、更新、および削除を実行する方法について説明します。 次のチュートリアルでは、アップロードしたファイルを対応するデータベースレコードに関連付ける方法について説明します。 その後のチュートリアルでは、既存のバイナリデータを更新する方法と、関連付けられたレコードが削除されたときにバイナリデータを削除する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy と Dave Gardner でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](uploading-files-cs.md)
> [次へ](including-a-file-upload-option-when-adding-a-new-record-cs.md)
