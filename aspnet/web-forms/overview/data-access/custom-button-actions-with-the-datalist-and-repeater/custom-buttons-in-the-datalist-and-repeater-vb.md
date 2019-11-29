---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
title: DataList と Repeater のカスタムボタン (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、Repeater を使用してシステムのカテゴリを一覧表示し、各カテゴリに associ を表示するボタンを提供するインターフェイスを作成します。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1afdb14d-6e49-4e1f-aead-2934730d472e
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: bc7e94e59226b739c2948434c1bfecb46b3d7856
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607669"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-vb"></a>DataList と Repeater のカスタム ボタン (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe)または[PDF のダウンロード](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)

> このチュートリアルでは、Repeater を使用してシステム内のカテゴリの一覧を表示するインターフェイスを作成します。各カテゴリには、BulletedList コントロールを使用して、関連付けられている製品を示すボタンが用意されています。

## <a name="introduction"></a>はじめに

これまでの17個 DataList および Repeater チュートリアルでは、読み取り専用の例を作成し、例を編集および削除しました。 DataList 内の編集および削除機能を容易にするために、`ItemTemplate` DataList にボタンを追加しました。これにより、クリックするとポストバックが発生し、ボタン s `CommandName` プロパティに対応する DataList イベントが発生します。 たとえば、`CommandName` プロパティ値が Edit の `ItemTemplate` にボタンを追加すると、その `EditCommand` DataList がポストバック時に起動します。1つは `CommandName` 削除を使用して、`DeleteCommand`を発生させます。

DataList コントロールと Repeater コントロールには、[編集] ボタンと [削除] ボタンに加えて、ボタン、リンクボタン、または ImageButtons を含めることもできます。このボタンは、クリックすると、カスタムのサーバー側ロジックを実行します。 このチュートリアルでは、リピータを使用してシステム内のカテゴリを一覧表示するインターフェイスを作成します。 各カテゴリについて、リピータには、BulletedList コントロールを使用してカテゴリに関連付けられた製品を表示するボタンが含まれています (図1を参照)。

[[製品の表示] リンクをクリック ![と、カテゴリの製品が箇条書きで表示されます。](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)

**図 1**: [製品の表示] リンクをクリックすると、箇条書きの一覧にカテゴリの製品が表示されます ([クリックすると、フルサイズの画像が表示](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png)されます)

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>手順 1: カスタムボタンチュートリアル Web ページの追加

カスタムボタンを追加する方法を確認する前に、まず、このチュートリアルで必要となる web サイトプロジェクトの ASP.NET ページを作成してみましょう。 まず、`CustomButtonsDataListRepeater`という名前の新しいフォルダーを追加します。 次に、次の2つの ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `CustomButtons.aspx`

![カスタムボタンに関連するチュートリアルの ASP.NET ページを追加する](custom-buttons-in-the-datalist-and-repeater-vb/_static/image4.png)

**図 2**: カスタムボタンに関連するチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`CustomButtonsDataListRepeater` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 このユーザーコントロールをソリューションエクスプローラーからページデザインビューにドラッグして、`Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)

**図 3**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png)されます)

最後に、`Web.sitemap` ファイルにエントリとしてページを追加します。 具体的には、ページングの後に次のマークアップを追加し、DataList および Repeater `<siteMapNode>`を使用して並べ替えます。

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、チュートリアルの編集、挿入、および削除を行うための項目が含まれています。

![サイトマップにカスタムボタンチュートリアルのエントリが含まれるようになりました。](custom-buttons-in-the-datalist-and-repeater-vb/_static/image8.png)

**図 4**: サイトマップにカスタムボタンチュートリアルのエントリが含まれるようになりました。

## <a name="step-2-adding-the-list-of-categories"></a>手順 2: カテゴリの一覧の追加

このチュートリアルでは、すべてのカテゴリを一覧表示する Repeater を作成する必要があります。これは、クリックすると、関連付けられているカテゴリの製品が箇条書きリストに表示されます。 まず、システム内のカテゴリを一覧表示する単純なリピータを作成します。 まず、`CustomButtonsDataListRepeater` フォルダーの [`CustomButtons.aspx`] ページを開きます。 Repeater をツールボックスからデザイナーにドラッグし、その `ID` プロパティを `Categories`に設定します。 次に、Repeater s スマートタグから新しいデータソースコントロールを作成します。 具体的には、`CategoriesBLL` クラス s `GetCategories()` メソッドからデータを選択する `CategoriesDataSource` という名前の新しい ObjectDataSource コントロールを作成します。

[GetCategories () メソッドを使用するように ObjectDataSource を構成 ![](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)

**図 5**: `CategoriesBLL` クラス s `GetCategories()` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png))

Visual Studio によってデータソースに基づいて既定の `ItemTemplate` が作成される DataList コントロールとは異なり、Repeater s テンプレートは手動で定義する必要があります。 さらに、リピータテンプレートは宣言によって作成および編集する必要があります (つまり、Repeater s スマートタグに [テンプレートの編集] オプションがありません)。

左下隅にある [ソース] タブをクリックし、`<h3>` 要素のカテゴリ名とその説明を段落タグに表示する `ItemTemplate` を追加します。各カテゴリ間の水平方向のルール (`<hr />`) を表示する `SeparatorTemplate` を含めます。 また、`Text` プロパティが [製品] に設定された LinkButton を追加します。 これらの手順を完了すると、ページ s の宣言型マークアップは次のようになります。

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample2.aspx)]

図6は、ブラウザーを使用して表示するときのページを示しています。 各カテゴリの名前と説明が表示されます。 [製品の表示] ボタンをクリックすると、ポストバックが発生しますが、まだ何も実行されていません。

[各カテゴリの名前と説明が表示され、[製品の表示] LinkButton と共に表示さ ![ます。](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)

**図 6**: 各カテゴリの名前と説明が表示され、製品の表示 LinkButton ([クリックすると、フルサイズの画像が表示](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png)されます)

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>手順 3: [製品の表示] LinkButton がクリックされたときのサーバー側ロジックの実行

DataList または Repeater 内のテンプレート内のボタン、LinkButton、または ImageButton がクリックされると、ポストバックが発生し、DataList または Repeater s `ItemCommand` イベントが発生します。 `ItemCommand` イベントに加えて、DataList コントロールは、ボタン s `CommandName` プロパティが予約済みの文字列 (Delete、Edit、Cancel、Update、または Select) のいずれかに設定されている場合に、より具体的な別のイベントを発生させることもありますが、`ItemCommand` イベントは*常に*発生します。

DataList または Repeater 内のボタンがクリックされたときに、クリックされたボタン ([編集] ボタンと [削除] ボタンの両方など) と、場合によっては (たとえば、[編集] ボタンと [削除] ボタンの両方のボタン) を渡す必要があります。ボタンがクリックされた項目の主キー値。 ボタン、LinkButton、および ImageButton は、値が `ItemCommand` イベントハンドラーに渡される2つのプロパティを提供します。

- テンプレートの各ボタンを識別するために通常使用される文字列を `CommandName` します。
- 主キーの値など、一部のデータフィールドの値を保持するために一般的に使用される `CommandArgument`

この例では、LinkButton の `CommandName` プロパティを ShowProducts に設定し、現在のレコード s 主キーの `CategoryID` 値を、データバインド構文 `CategoryArgument='<%# Eval("CategoryID") %>'`を使用して `CommandArgument` プロパティにバインドします。 これら2つのプロパティを指定すると、LinkButton の宣言構文は次のようになります。

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample3.aspx)]

このボタンをクリックすると、ポストバックが発生し、DataList または Repeater s `ItemCommand` イベントが発生します。 イベントハンドラーには、ボタン s `CommandName` と `CommandArgument` 値が渡されます。

Repeater s `ItemCommand` イベントのイベントハンドラーを作成し、イベントハンドラーに渡される2番目のパラメーター (名前は `e`) に注意してください。 この2番目のパラメーターは[`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx)型で、次の4つのプロパティがあります。

- クリックされたボタンの `CommandArgument` プロパティの値を `CommandArgument` します。
- ボタン s `CommandName` プロパティの値を `CommandName` します。
- クリックされたボタンコントロールへの参照を `CommandSource` します
- クリックされたボタンを含む[`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx)への参照を `Item` します。リピータにバインドされている各レコードは、`RepeaterItem` として示されます。

選択したカテゴリの `CategoryID` は `CommandArgument` プロパティを介して渡されるため、`ItemCommand` イベントハンドラーで選択したカテゴリに関連付けられている製品のセットを取得できます。 これらの製品は、`ItemTemplate` (まだ追加していない) の BulletedList コントロールにバインドできます。 それでも、BulletedList を追加し、それを `ItemCommand` イベントハンドラーで参照し、選択したカテゴリの一連の製品にバインドします。これについては、手順 4. で説明します。

> [!NOTE]
> DataList s `ItemCommand` イベントハンドラーには、 [`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)型のオブジェクトが渡されます。このオブジェクトには、`RepeaterCommandEventArgs` クラスと同じ4つのプロパティが用意されています。

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>手順 4: 選択したカテゴリの製品を箇条書きリストに表示する

選択したカテゴリの製品は、任意の数のコントロールを使用して `ItemTemplate` リピータ内に表示できます。 入れ子になった別のリピータ、DataList、DropDownList、GridView などを追加できます。 製品を箇条書きとして表示するため、BulletedList コントロールを使用します。 `CustomButtons.aspx` ページ s 宣言マークアップに戻り、[製品の表示] LinkButton の後に BulletedList コントロールを `ItemTemplate` に追加します。 BulletedLists s `ID` を `ProductsInCategory`に設定します。 BulletedList プロパティ `DataTextField` によって指定されたデータフィールドの値がに表示されます。このコントロールには製品情報がバインドされているため、`DataTextField` プロパティを `ProductName`に設定します。

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample4.aspx)]

`ItemCommand` イベントハンドラーで、`e.Item.FindControl("ProductsInCategory")` を使用してこのコントロールを参照し、選択したカテゴリに関連付けられている製品のセットにバインドします。

[!code-vb[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample5.vb)]

`ItemCommand` イベントハンドラーで何らかのアクションを実行する前に、まず受信 `CommandName`の値を確認することをお勧めします。 `ItemCommand` イベントハンドラーは、ボタンがクリックされ*たときに発生するため*、テンプレートに複数のボタンがある場合は、`CommandName` の値を使用して、実行するアクションを識別します。 ここで `CommandName` をチェックするのは議論ですが、ボタンは1つだけなので、この方法をお勧めします。 次に、選択したカテゴリの `CategoryID` が `CommandArgument` プロパティから取得されます。 次に、テンプレート内の BulletedList コントロールが参照され、`ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドの結果にバインドされます。

Datalist の[データの編集と削除の概要](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)など、datalist 内のボタンを使用した前のチュートリアルでは、`DataKeys` コレクションを介して特定の項目の主キーの値を決定しました。 この方法は DataList ではうまく機能しますが、リピータには `DataKeys` のプロパティがありません。 代わりに、主キーの値を提供する別の方法を使用する必要があります。たとえば、ボタン s `CommandArgument` プロパティを介して、またはテンプレート内の隠しラベル Web コントロールに主キーの値を割り当て、`e.Item.FindControl("LabelID")`を使用して `ItemCommand` イベントハンドラーでその値を読み取ることができます。

`ItemCommand` イベントハンドラーを完了したら、ブラウザーでこのページをテストしてみてください。 図7に示すように、[製品の表示] リンクをクリックするとポストバックが発生し、選択したカテゴリの製品が BulletedList に表示されます。 さらに、他のカテゴリの [製品の表示] リンクがクリックされた場合でも、この製品情報は残されていることに注意してください。

> [!NOTE]
> このレポートの動作を変更する場合は、一度に1つのカテゴリの製品のみが一覧表示されるようにするには、BulletedList コントロール s `EnableViewState` プロパティを `False`に設定します。

[BulletedList を使用して、選択したカテゴリの製品を表示する ![](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)

**図 7**: BulletedList を使用して、選択したカテゴリの製品を表示する ([クリックすると、フルサイズの画像が表示](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png)されます)

## <a name="summary"></a>要約

DataList コントロールと Repeater コントロールには、テンプレート内に任意の数のボタン、リンクボタン、または ImageButtons を含めることができます。 このようなボタンをクリックすると、ポストバックが発生し、`ItemCommand` イベントが発生します。 カスタムサーバー側の操作をクリックされたボタンと関連付けるには、`ItemCommand` イベントのイベントハンドラーを作成します。 このイベントハンドラーでは、最初に受信 `CommandName` 値をチェックして、クリックされたボタンを判別します。 必要に応じて、ボタン s `CommandArgument` プロパティを使用して追加情報を指定することもできます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは、Patterson がになりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](custom-buttons-in-the-datalist-and-repeater-cs.md)
