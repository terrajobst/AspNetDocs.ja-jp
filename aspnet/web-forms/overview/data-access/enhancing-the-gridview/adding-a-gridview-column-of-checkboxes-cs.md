---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: Checkbox (C#) | の GridView 列を追加するMicrosoft Docs
author: rick-anderson
description: このチュートリアルでは、GridView コントロールにチェックボックスの列を追加して、ユーザーに対して、複数の行を選択してわかりやすく表示する方法について説明します。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: b9d1ed50e8d88202c3286b4cd0e9ebf111dfbe21
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592700"
---
# <a name="adding-a-gridview-column-of-checkboxes-c"></a>チェックボックスの GridView 列を追加する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe)または[PDF のダウンロード](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> このチュートリアルでは、gridview コントロールにチェックボックスの列を追加して、ユーザーが GridView の複数の行を直感的に選択できるようにする方法について説明します。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、特定のレコードを選択する目的で、オプションボタンの列を GridView に追加する方法を説明します。 オプションボタンの列は、ユーザーがグリッドから最大で1つの項目を選択することに制限されている場合に適したユーザーインターフェイスです。 ただし、ユーザーがグリッドから任意の数の項目を選択できるようにすることが必要になる場合があります。 たとえば、Web ベースの電子メールクライアントでは、通常、メッセージの一覧とチェックボックスの列が表示されます。 ユーザーは任意の数のメッセージを選択して、他のフォルダーへのメールの移動や削除など、何らかの操作を実行できます。

このチュートリアルでは、チェックボックスの列を追加する方法と、ポストバック時にチェックされたチェックボックスを確認する方法について説明します。 特に、web ベースの電子メールクライアントのユーザーインターフェイスを模倣した例を作成します。 この例では、`Products` データベーステーブルに製品を一覧表示するページングされた GridView と、各行にチェックボックスがあります (図1を参照)。 [選択した製品の削除] ボタンをクリックすると、選択した製品が削除されます。

[各製品行にチェックボックスが含まれて ![](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**図 1**: 各製品行にチェックボックスが含まれている ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png)されます)

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>手順 1: 製品情報を一覧表示するページングされた GridView の追加

チェックボックスの列を追加することを心配する前に、まず、ページングをサポートする GridView で製品を一覧表示する方法を説明します。 まず、`EnhancedGridView` フォルダーの [`CheckBoxField.aspx`] ページを開き、GridView をツールボックスからデザイナーにドラッグし、`ID` を [`Products`] に設定します。 次に、GridView を `ProductsDataSource`という名前の新しい ObjectDataSource にバインドします。 `ProductsBLL` クラスを使用し、`GetProducts()` メソッドを呼び出してデータを返すように ObjectDataSource を構成します。 この GridView は読み取り専用であるため、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[![新しい ObjectDataSource Datasource を作成する](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**図 2**: `ProductsDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png)される)

[GetProducts () メソッドを使用してデータを取得するように ObjectDataSource を構成 ![には](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**図 3**: `GetProducts()` メソッドを使用してデータを取得するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))

[[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定 ![ます。](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**図 4**: [更新]、[挿入]、[削除] の各タブのドロップダウンリストを (なし) に設定する ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png))

データソースの構成ウィザードを完了すると、Visual Studio によって、BoundColumns と、製品関連のデータフィールドの CheckBoxColumn が自動的に作成されます。 前のチュートリアルで行ったように、`ProductName`、`CategoryName`、および `UnitPrice` BoundFields 以外のすべてを削除し、`HeaderText` のプロパティを製品、カテゴリ、および価格に変更します。 値が通貨として書式設定されるように、`UnitPrice` BoundField を構成します。 また、スマートタグの [ページングを有効にする] チェックボックスをオンにして、ページングをサポートするように GridView を構成します。

選択した製品を削除するためのユーザーインターフェイスも追加します。 GridView の下に Button Web コントロールを追加し、その `ID` を `DeleteSelectedProducts` に設定し、その `Text` プロパティを選択した製品を削除します。 この例では、実際にデータベースから製品を削除するのではなく、削除された製品を示すメッセージを表示するだけです。 これに対応するには、ボタンの下にラベル Web コントロールを追加します。 ID を `DeleteResults`に設定し、`Text` プロパティをオフにして、その `Visible` および `EnableViewState` プロパティを `false`に設定します。

これらの変更を行った後、GridView、ObjectDataSource、Button、および Label s の宣言マークアップは、次のようになります。

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

ブラウザーでページを表示します (図5を参照)。 この時点で、最初の10個の製品の名前、カテゴリ、価格が表示されます。

[最初の10個の製品の名前、カテゴリ、価格が表示され ![](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**図 5**: 最初の10個の製品の名前、カテゴリ、価格が表示されます ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png)されます)

## <a name="step-2-adding-a-column-of-checkboxes"></a>手順 2: チェックボックスの列の追加

ASP.NET 2.0 には CheckBoxField が含まれているため、GridView にチェックボックスの列を追加するために使用できると考えられるかもしれません。 残念ながら、CheckBoxField はブール型のデータフィールドを使用するように設計されているため、そうではありません。 つまり、CheckBoxField を使用するには、表示されているチェックボックスがオンになっているかどうかを判断する値を持つ基になるデータフィールドを指定する必要があります。 CheckBoxField を使用して、チェックボックスがオフの列だけを含めることはできません。

代わりに、TemplateField を追加し、チェックボックス Web コントロールを `ItemTemplate`に追加する必要があります。 `Products` GridView に TemplateField を追加し、最初 (左端) のフィールドに設定します。 GridView s スマートタグから、[テンプレートの編集] リンクをクリックし、[ツールボックス] から [CheckBox] Web コントロールを `ItemTemplate`にドラッグします。 この CheckBox s `ID` プロパティを `ProductSelector`に設定します。

[TemplateField s ItemTemplate に ProductSelector という名前の CheckBox Web コントロールを追加 ![には](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**図 6**: `ProductSelector` という名前の CheckBox Web コントロールを TemplateField s `ItemTemplate` に追加する ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png)されます)

TemplateField および CheckBox Web コントロールが追加され、各行にチェックボックスが追加されました。 図7に、TemplateField および CheckBox を追加した後にブラウザーで表示すると、このページが表示されます。

[各製品行にチェックボックスが含まれるようになりました ![](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**図 7**: 各製品行にチェックボックスが含まれるようになりました ([クリックしてフルサイズの画像を表示](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png))

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>手順 3: ポストバック時にチェックされたチェックボックスの確認

この時点では、チェックボックスの列がありますが、ポストバック時にチェックされたチェックボックスを確認する方法はありません。 ただし、[選択した製品の削除] ボタンをクリックしたときに、その製品を削除するためにチェックされたチェックボックスを確認する必要があります。

GridView s [`Rows` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx)は、gridview のデータ行へのアクセスを提供します。 これらの行を反復処理し、CheckBox コントロールにプログラムでアクセスして、その `Checked` プロパティを参照して、チェックボックスがオンになっているかどうかを判断します。

`DeleteSelectedProducts` ボタン Web コントロール s `Click` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

`Rows` プロパティは、GridView のデータ行を指定する `GridViewRow` インスタンスのコレクションを返します。 ここで `foreach` ループは、このコレクションを列挙します。 `GridViewRow` の各オブジェクトについて、行のチェックボックスは、`row.FindControl("controlID")`を使用してプログラムによってアクセスされます。 チェックボックスをオンにすると、`ProductID` 値に対応する行が `DataKeys` コレクションから取得されます。 この演習では、`DeleteResults` ラベルにわかりやすいメッセージを表示します。ただし、動作しているアプリケーションでは、代わりに `ProductsBLL` クラス s `DeleteProduct(productID)` メソッドを呼び出します。

このイベントハンドラーを追加すると、[選択した製品の削除] ボタンをクリックすると、選択した製品の `ProductID` が表示されるようになります。

[![[選択した製品の削除] ボタンをクリックすると、選択した Products Productids) が表示されます](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**図 8**: [選択した製品の削除] ボタンをクリックすると、選択した製品 `ProductID` が一覧表示されます ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png)されます)

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>手順 4: すべてのボタンを確認し、すべてのボタンをオフにする

現在のページのすべての製品を削除する場合は、10の各チェックボックスをオンにする必要があります。 [すべて確認] ボタンを追加することにより、このプロセスを迅速に実行できます。このボタンをクリックすると、グリッド内のすべてのチェックボックスがオンになります。 [すべてクリア] ボタンも同様に役立ちます。

2つのボタン Web コントロールをページに追加し、GridView の上に配置します。 最初の1つの `ID` を `CheckAll` に設定し、その `Text` プロパティを [すべてを確認] に設定します。2つ目の `ID` を `UncheckAll` に設定し、その `Text` プロパティを [すべてオフ] に設定します。

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

次に、`ToggleCheckState(checkState)` という名前の分離コードクラスにメソッドを作成します。このメソッドを呼び出すと、`Products` GridView s `Rows` collection が列挙され、各 CheckBox s `Checked` プロパティが渡された*Checkstate*パラメーターの値に設定されます。

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

次に、[`CheckAll`] および [`UncheckAll`] ボタンの `Click` イベントハンドラーを作成します。 `CheckAll` s イベントハンドラーでは、単に `ToggleCheckState(true)`を呼び出します。`UncheckAll`で `ToggleCheckState(false)`を呼び出します。

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

このコードでは、[すべてを確認] ボタンをクリックするとポストバックが発生し、GridView のすべてのチェックボックスがオンになります。 同様に、[すべてのチェックボックスをオフにする] チェックボックスをオンにします。 図9に、[すべて確認] ボタンがオンになった後の画面を示します。

[[すべてを確認] ボタンをクリックしてすべてのチェックボックスを選択 ![](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**図 9**: [すべてを確認] ボタンをクリックすると、すべてのチェックボックスがオンになります ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png)されます)

> [!NOTE]
> チェックボックスの列を表示する場合、すべてのチェックボックスをオンまたはオフにするには、ヘッダー行のチェックボックスを使用します。 また、すべての実装を確認し、すべての実装をオフにするには、ポストバックが必要です。 ただし、チェックボックスをオンまたはオフにすることはできますが、クライアント側のスクリプトでは、snappier のユーザーエクスペリエンスを提供します。 [すべてをチェック] の [ヘッダー行] チェックボックスを使用して詳細を確認するには、クライアント側の手法を使用する方法については、「クライアント側の[スクリプトを使用して GridView ですべて](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)のチェックボックスをチェックする」および「すべてを確認する」チェックボックスをオンにしてください。

## <a name="summary"></a>要約

続行する前にユーザーが GridView から任意の数の行を選択できるようにする必要がある場合は、チェックボックスの列を追加する方法が1つあります。 このチュートリアルで説明したように、GridView にチェックボックスの列を含めると、CheckBox Web コントロールで TemplateField を追加することができます。 (前のチュートリアルで行ったように) Web コントロールを使用して、ASP.NET が、ポストバック間でチェックされなかったチェックボックスを自動的に記憶します。 また、コード内のチェックボックスにプログラムでアクセスして、特定のチェックボックスがオンになっているかどうかを判断したり、チェックされた状態を変更したりすることもできます。

このチュートリアルと最後のチュートリアルでは、行セレクター列を GridView に追加しました。 次のチュートリアルでは、いくつかの作業を行い、GridView に挿入機能を追加できる方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](adding-a-gridview-column-of-radio-buttons-cs.md)
> [次へ](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
