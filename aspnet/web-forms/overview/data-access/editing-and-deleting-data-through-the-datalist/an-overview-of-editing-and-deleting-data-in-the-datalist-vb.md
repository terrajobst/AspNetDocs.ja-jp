---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
title: DataList (VB) でのデータの編集と削除の概要Microsoft Docs
author: rick-anderson
description: DataList には編集および削除機能が組み込まれていませんが、このチュートリアルでは、編集と削除をサポートする DataList を作成する方法について説明します。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 9410a23c-9697-4f07-bd71-e62b0ceac655
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 49b09cbf0f12f7c7233c3bb2a8b3b2c073bf117e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78495244"
---
# <a name="an-overview-of-editing-and-deleting-data-in-the-datalist-vb"></a>DataList のデータの編集と削除の概要 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_VB.exe)または[PDF のダウンロード](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/datatutorial36vb1.pdf)

> DataList には編集および削除機能が組み込まれていませんが、このチュートリアルでは、基になるデータの編集と削除をサポートする DataList を作成する方法について説明します。

## <a name="introduction"></a>はじめに

[「データの挿入、更新、削除の概要](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)」チュートリアルでは、アプリケーションアーキテクチャ、ObjectDataSource、GridView、DetailsView、および FormView コントロールを使用してデータを挿入、更新、および削除する方法について説明しました。 ObjectDataSource とこれら3つのデータ Web コントロールでは、単純なデータ変更インターフェイスの実装はスナップであり、単にスマートタグからチェックボックスをオンにするだけです。 コードを記述する必要はありません。

残念ながら、DataList には GridView コントロールに固有の組み込みの編集および削除機能がありません。 この欠けている機能は、宣言型のデータソースコントロールとコードフリーのデータ変更ページが使用できない場合に、DataList が以前のバージョンの ASP.NET の聖製品であることが原因です。 ASP.NET 2.0 の DataList では、GridView と同じデータ変更機能が提供されていませんが、ASP.NET 1. x の手法を使用してこの機能を含めることができます。 この方法には少しのコードが必要ですが、このチュートリアルで説明するように、DataList には、このプロセスを支援するためのイベントとプロパティがいくつか用意されています。

このチュートリアルでは、基になるデータの編集と削除をサポートする DataList を作成する方法について説明します。 今後のチュートリアルでは、入力フィールドの検証、データアクセスやビジネスロジックレイヤーから発生した例外の適切な処理など、より高度な編集と削除のシナリオについて説明します。

> [!NOTE]
> DataList と同様に、Repeater コントロールは、挿入、更新、または削除のためのすぐに使用する機能を備えていません。 このような機能を追加できますが、DataList には、このような機能の追加を簡略化する、リピータに見つからないプロパティとイベントが含まれています。 そのため、このチュートリアルと、編集と削除については、常に DataList に焦点を当てています。

## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>手順 1: チュートリアルの編集と削除の Web ページを作成する

DataList からデータを更新および削除する方法を確認する前に、まず、このチュートリアルに必要な ASP.NET ページを web サイトプロジェクトに作成し、次のいくつかについて説明します。 まず、`EditDeleteDataList`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![チュートリアルの ASP.NET ページを追加する](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image1.png)

**図 1**: チュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`EditDeleteDataList` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image2.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image4.png)されます)

最後に、`Web.sitemap` ファイルにエントリとしてページを追加します。 具体的には、DataList および Repeater `<siteMapNode>`を使用して、マスター/詳細レポートの後に次のマークアップを追加します。

[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、DataList の編集と削除のチュートリアルの項目が含まれるようになりました。

![サイトマップに、DataList の編集と削除のチュートリアルのエントリが含まれるようになりました。](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image5.png)

**図 3**: サイトマップに、DataList の編集と削除のチュートリアルのエントリが含まれるようになりました。

## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>手順 2: データの更新と削除の手法を調べる

GridView を使用してデータを編集および削除するのは簡単です。これは、gridview と ObjectDataSource が連携して動作するためです。 「[挿入、更新、および削除に関連するイベントの調査](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)」で説明されているように、[行 s 更新] ボタンをクリックすると、GridView は、双方向のデータバインディングを使用したフィールドを objectdatasource の `UpdateParameters` コレクションに自動的に割り当て、その objectdatasource `Update()` メソッドを呼び出します。

残念ながら、DataList では、この組み込み機能は提供されません。 ユーザーの値が ObjectDataSource s パラメーターに割り当てられ、`Update()` メソッドが呼び出されるようにする必要があります。 この機能を利用するために、DataList には次のプロパティとイベントが用意されています。

- 更新または削除する場合、  **[`DataKeyField` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)は**、DataList 内の各項目を一意に識別できる必要があります。 このプロパティを、表示されるデータの [主キー] フィールドに設定します。 これにより、datalist s [`DataKeys` コレクション](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx)に、各 datalist 項目の指定された `DataKeyField` 値が設定されます。
- **[`EditCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)** は、`CommandName` プロパティが [編集] に設定されているボタン、LinkButton、または ImageButton がクリックされたときに発生します。
- **[`CancelCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)** は、`CommandName` プロパティが [キャンセル] に設定されているボタン、LinkButton、または ImageButton がクリックされたときに発生します。
- **[`UpdateCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)** は、`CommandName` プロパティが [更新] に設定されているボタン、LinkButton、または ImageButton がクリックされたときに発生します。
- **[`DeleteCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)** は、`CommandName` プロパティが [削除] に設定されているボタン、LinkButton、または ImageButton がクリックされたときに発生します。

これらのプロパティとイベントを使用して、DataList からデータを更新および削除するために使用できる4つの方法があります。

1. **ASP.NET 1.X 手法を使用**すると、DataList は ASP.NET 2.0 および objectdatasources ソースより前に存在し、プログラムによる手段を通じてデータを完全に更新および削除することができました。 この手法では、ObjectDataSource を完全に ditches し、表示するデータを取得するときとレコードを更新または削除するときの両方で、ビジネスロジック層からデータを DataList に直接バインドする必要があります。
2. DataList に固有の編集および削除機能がないときに、**ページで1つの ObjectDataSource コントロールを選択、更新、および削除するために使用**することはできません。そのため、これらを自分で追加することはできません。 この方法では、GridView の例と同様に ObjectDataSource を使用しますが、ObjectDataSource s パラメーターを設定し、その `Update()` メソッドを呼び出すために、DataList s `UpdateCommand` イベントのイベントハンドラーを作成する必要があります。
3. オプション2を使用するときに、 **ObjectDataSource コントロールを選択するときに ObjectDataSource コントロールを使用して、BLL に対して直接更新および削除**を行う必要があります。そのためには、`UpdateCommand` イベントに少しのコードを記述し、パラメーター値を割り当てる必要があります。 代わりに、ObjectDataSource を選択に使用してもかまいませんが、更新と削除の呼び出しを BLL に対して直接行うことができます (オプション1など)。 私の意見では、BLL に直接インターフェイスを使用してデータを更新することにより、ObjectDataSource を `UpdateParameters` し、その `Update()` メソッドを呼び出すよりも読みやすいコードになります。
4. **複数の ObjectDataSources ソースを介して宣言型の意味を使用**する前の3つの方法では、すべてのコードが必要になります。 可能な限り多くの宣言型の構文を使用する場合は、最後のオプションとして、ページに複数の ObjectDataSources ソースを含めることができます。 最初の ObjectDataSource は、BLL からデータを取得し、それを DataList にバインドします。 更新の場合、別の ObjectDataSource が追加されますが、DataList s `EditItemTemplate`内に直接追加されます。 削除のサポートを含めるには、`ItemTemplate`でもう1つの ObjectDataSource が必要になります。 この方法では、これらの埋め込み ObjectDataSource は `ControlParameters` を使用して、ObjectDataSource s パラメーターをユーザー入力コントロールに宣言によってバインドします (DataList s `UpdateCommand` イベントハンドラーでプログラムによって指定する必要はありません)。 この方法では、埋め込み ObjectDataSource `Update()` または `Delete()` コマンドを呼び出す必要がありますが、他の3つの方法よりもはるかに少ないコードが必要です。 ここでの欠点は、複数の ObjectDataSources がページを見やすくし、全体的に読みやすさを向上させることです。

これらの方法のいずれかのみを使用するように強制する場合は、オプション1を選択します。これは、最も柔軟性が高く、DataList がもともとこのパターンに対応するように設計されているためです。 DataList は、ASP.NET 2.0 データソースコントロールで動作するように拡張されましたが、公式の ASP.NET 2.0 データ Web コントロール (GridView、DetailsView、FormView) のすべての機能拡張ポイントまたは機能を備えていません。 ただし、オプション 2 ~ 4 は、メリットがありません。

このチュートリアルと今後の編集と削除のチュートリアルでは、表示するデータを取得するために ObjectDataSource を使用し、データを更新および削除するために BLL に直接呼び出します (オプション 3)。

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>手順 3: DataList を追加し、ObjectDataSource を構成する

このチュートリアルでは、製品情報を一覧表示する DataList を作成します。製品ごとに、ユーザーは、名前と価格を編集したり、製品を削除することができます。 特に、ObjectDataSource を使用して表示するレコードを取得しますが、BLL と直接やり取りすることで update アクションと delete アクションを実行します。 DataList に編集機能と削除機能を実装することを心配する前に、まず、読み取り専用インターフェイスに製品を表示するページを取得してみましょう。 前のチュートリアルでこれらの手順を確認したので、これらの手順をすぐに進めていきます。

まず、`EditDeleteDataList` フォルダーの [`Basics.aspx`] ページを開いて、デザインビューからページに DataList を追加します。 次に、DataList s スマートタグから新しい ObjectDataSource を作成します。 ここでは、製品データを操作しているため、`ProductsBLL` クラスを使用するように構成します。 *すべて*の製品を取得するには、[選択] タブで `GetProducts()` 方法を選択します。

[製品の Bll クラスを使用するように ObjectDataSource を構成 ![には](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image6.png)

**図 4**: `ProductsBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image8.png))

[GetProducts () メソッドを使用して製品情報を返す ![](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image9.png)

**図 5**: `GetProducts()` メソッドを使用して製品情報を返す ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image11.png)されます)

GridView と同様に、DataList は新しいデータを挿入するように設計されていません。そのため、[挿入] タブのドロップダウンリストから [(なし)] オプションを選択します。また、[更新] タブと [削除] タブの [(なし)] を選択します。これは、更新プログラムと削除が BLL を通じてプログラムによって実行されるためです。

[[ObjectDataSource s INSERT]、[UPDATE]、[DELETE] の各タブのドロップダウンリストが [(なし)] に設定されていることを ![確認します。](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image12.png)

**図 6**: ObjectDataSource s の [挿入]、[更新]、および [削除] の各タブのドロップダウンリストが [(なし)] に設定されていることを確認[する (クリックしてフルサイズの画像を表示する](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image14.png))

ObjectDataSource を構成したら、[完了] をクリックしてデザイナーに戻ります。 前の例で説明したように、ObjectDataSource 構成を完了すると、Visual Studio によって DropDownList の `ItemTemplate` が自動的に作成され、各データフィールドが表示されます。 この `ItemTemplate` を、製品の名前と価格だけを表示するものに置き換えます。 また、`RepeatColumns` プロパティを2に設定します。

> [!NOTE]
> *データの挿入、更新、削除の概要*に関するチュートリアルで説明したように、objectdatasource のアーキテクチャを使用してデータを変更する場合は、objectdatasource s 宣言マークアップから `OldValuesParameterFormatString` プロパティを削除する必要があります (または、既定値の `{0}`)。 ただし、このチュートリアルでは、データの取得に ObjectDataSource のみを使用しています。 したがって、ObjectDataSource s `OldValuesParameterFormatString` のプロパティ値を変更する必要はありません (ただし、これには害がありません)。

既定の DataList `ItemTemplate` をカスタマイズされたものに置き換えると、ページ上の宣言型マークアップは次のようになります。

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample2.aspx)]

ブラウザーで進行状況を確認してください。 図7に示すように、DataList は各製品の製品名と単価を2つの列に表示します。

[製品の名前と価格が2列の DataList に表示される ![](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image15.png)

**図 7**: 製品名と価格が2列の DataList で表示される ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image17.png)されます)

> [!NOTE]
> DataList には、更新および削除プロセスに必要ないくつかのプロパティがあり、これらの値はビューステートに格納されます。 そのため、データの編集または削除をサポートする DataList を構築する場合は、DataList s ビューステートが有効になっていることが重要です。  
>   
> ずる賢い reader は、編集可能な GridViews、の [表示] ビュー、および [FormViews] を作成するときに、ビューステートを無効にできることを思い出している可能性があります。 これは、ASP.NET 2.0 Web コントロールには、ビューステートなどのポストバック間で保持される状態である*コントロールの状態*を含めることができますが、これは必須であると見なされるためです。

GridView のビューステートを無効にすると、単純な状態情報が省略されますが、コントロールの状態 (編集および削除に必要な状態を含む) は維持されます。 ASP.NET 1.x 時間枠で作成された DataList はコントロールの状態を利用しないため、ビューステートが有効になっている必要があります。 制御状態とビューステートの違いの詳細については、「コントロールの状態と[ビューステート](https://msdn.microsoft.com/library/1whwt1k7.aspx)」を参照してください。

## <a name="step-4-adding-an-editing-user-interface"></a>手順 4: 編集ユーザーインターフェイスを追加する

GridView コントロールは、フィールド (BoundFields、CheckBoxFields、TemplateFields など) のコレクションで構成されています。 これらのフィールドは、表示されているマークアップをモードに応じて調整できます。 たとえば、読み取り専用モードの場合、BoundField はデータフィールドの値をテキストとして表示します。編集モードの場合は、`Text` プロパティにデータフィールド値が割り当てられている TextBox Web コントロールがレンダリングされます。

一方、DataList は、テンプレートを使用して項目をレンダリングします。 読み取り専用の項目は `ItemTemplate` を使用してレンダリングされますが、編集モードの項目は `EditItemTemplate`によってレンダリングされます。 この時点で、DataList には `ItemTemplate`のみが含まれています。 項目レベルの編集機能をサポートするには、編集可能な項目に対して表示されるマークアップを含む `EditItemTemplate` を追加する必要があります。 このチュートリアルでは、テキストボックス Web コントロールを使用して、製品の名前と単価を編集します。

`EditItemTemplate` は、宣言によって、またはデザイナーを使用して作成できます (DataList s スマートタグの [テンプレートの編集] オプションを選択します)。 [テンプレートの編集] オプションを使用するには、まずスマートタグの [テンプレートの編集] リンクをクリックし、ドロップダウンリストから `EditItemTemplate` 項目を選択します。

[![DataList s EditItemTemplate を使用することを選択します。](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image18.png)

**図 8**: DataList s `EditItemTemplate` を使用することを選択する ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image20.png)されます)

次に、[Product name:] と [Price] を入力します。次に、ツールボックスから2つのテキストボックスコントロールをデザイナーの `EditItemTemplate` インターフェイスにドラッグします。 テキストボックス `ID` プロパティを `ProductName` と `UnitPrice`に設定します。

[製品の名前と価格のテキストボックスを追加 ![には](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image21.png)

**図 9**: 製品名と価格のテキストボックスを追加する ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image23.png)されます)

対応する製品データフィールドの値を、2つのテキストボックスの `Text` プロパティにバインドする必要があります。 図10に示すように、テキストボックスのスマートタグから、[データバインディングの編集] リンクをクリックし、適切なデータフィールドを `Text` プロパティに関連付けます。

> [!NOTE]
> `UnitPrice` データフィールドを price TextBox s `Text` フィールドにバインドする場合は、通貨値 (`{0:C}`)、一般数値 (`{0:N}`) として書式設定するか、または書式設定しないままにすることができます。

![ProductName および UnitPrice データフィールドをテキストボックスのテキストプロパティにバインドする](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image24.png)

**図 10**: `ProductName` と `UnitPrice` のデータフィールドをテキストボックスの `Text` プロパティにバインドする

図10の [データ連結の編集] ダイアログボックスには、GridView または DetailsView で TemplateField を編集するときに存在する双方向のデータバインドチェックボックス、または FormView 内のテンプレートが含ま*れていない*ことに注意してください。 双方向のデータバインディング機能では、入力 Web コントロールに入力された値が、データを挿入または更新するときに、対応する ObjectDataSource s `InsertParameters` または `UpdateParameters` に自動的に割り当てられるようになりました。 DataList は、このチュートリアルで後ほど説明するように、双方向のデータバインディングをサポートしていません。ユーザーが変更を加えてデータを更新する準備ができたら、プログラムを使用してこれらのテキスト `Text` ボックスにアクセスし、その値を `ProductsBLL` クラスの適切な `UpdateProduct` メソッドに渡す必要があります。

最後に、[更新] ボタンと [キャンセル] ボタンを `EditItemTemplate`に追加する必要があります。 [詳細な DataList チュートリアルを含むマスターレコードの箇条書きリストを使用してマスター/詳細](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)を確認しましたが、`CommandName` プロパティが設定されているボタン、LinkButton、または ImageButton が repeater または datalist 内からクリックされると、repeater または datalist s `ItemCommand` イベントが発生します。 DataList の場合、`CommandName` プロパティが特定の値に設定されていると、追加のイベントも発生する可能性があります。 特別な `CommandName` プロパティ値には、次のようなものがあります。

- Cancel は `CancelCommand` イベントを発生させます
- Edit は `EditCommand` イベントを発生させます
- Update によって `UpdateCommand` イベントが発生します

これらのイベントは、`ItemCommand` イベント*に加え*て発生することに注意してください。

`CommandName` を更新するように設定し、もう一方をキャンセルに設定して、2つのボタンの Web コントロール `EditItemTemplate` に追加します。 これらの2つのボタン Web コントロールを追加すると、デザイナーは次のようになります。

[EditItemTemplate に [Update] ボタンと [Cancel] ボタンを追加 ![には](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image25.png)

**図 11**: [更新] ボタンと [キャンセル] ボタンを `EditItemTemplate` に追加[する (クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image27.png)されます)

`EditItemTemplate` 完了すると、DataList s 宣言型マークアップは次のようになります。

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>手順 5: 編集モードにするには、プラミングを追加します。

この時点で、DataList には `EditItemTemplate`を介して定義された編集インターフェイスがあります。ただし、現在のところ、ユーザーが製品の情報を編集することを示すためにページにアクセスする方法はありません。 [編集] ボタンを各製品に追加する必要があります。このボタンをクリックすると、DataList 項目が編集モードで表示されます。 まず、デザイナーを使用するか、宣言によって `ItemTemplate`に [編集] ボタンを追加します。 [Edit button s `CommandName`] プロパティを Edit に設定してください。

この編集ボタンを追加した後、ブラウザーを使用してページを表示します。 この追加では、各製品の一覧に [編集] ボタンが含まれている必要があります。

[EditItemTemplate に [Update] ボタンと [Cancel] ボタンを追加 ![には](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image28.png)

**図 12**: [更新] ボタンと [キャンセル] ボタンを `EditItemTemplate` に追加[する (クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image30.png)されます)

このボタンをクリックするとポストバックが発生しますが、製品リストが編集モードになる*ことはありません*。 製品を編集可能にするには、次のことを行う必要があります。

1. [DataList s [`EditItemIndex`] プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)を、[編集] ボタンがクリックされた `DataListItem` のインデックスに設定します。
2. データを DataList に再バインドします。 DataList を再描画すると、`ItemIndex` が DataList s `EditItemIndex` に対応する `DataListItem` が、その `EditItemTemplate`を使用して表示されます。

[編集] ボタンをクリックすると DataList s `EditCommand` イベントが発生するため、次のコードを使用して `EditCommand` イベントハンドラーを作成します。

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample4.vb)]

`EditCommand` イベントハンドラーは、`DataListCommandEventArgs` 型のオブジェクトで2番目の入力パラメーターとして渡されます。これには、Edit ボタンがクリックされた (`e.Item`) `DataListItem` への参照が含まれます。 イベントハンドラーは、最初に DataList s `EditItemIndex` を編集可能な `DataListItem` の `ItemIndex` に設定し、DataList s `DataBind()` メソッドを呼び出すことによってデータを DataList に再バインドします。

このイベントハンドラーを追加した後、ブラウザーでページを再度参照してください。 [編集] ボタンをクリックすると、クリックした製品が編集可能になります (図13を参照)。

[[編集] ボタンをクリック ![と、製品が編集可能になります](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image31.png)

**図 13**: [編集] ボタンをクリックすると、製品が編集可能になります ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image33.png)されます)

## <a name="step-6-saving-the-user-s-changes"></a>手順 6: ユーザーの変更を保存する

編集した製品の [更新] ボタンまたは [キャンセル] ボタンをクリックしても、この時点では何も行われません。この機能を追加するには、DataList s `UpdateCommand` イベントと `CancelCommand` イベントのイベントハンドラーを作成する必要があります。 まず、`CancelCommand` イベントハンドラーを作成します。このハンドラーは、編集した製品の [キャンセル] ボタンがクリックされたときに実行され、DataList を編集前の状態に戻します。

DataList が読み取り専用モードですべての項目を表示するには、次のことを行う必要があります。

1. DataList s [`EditItemIndex` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)に、存在しない `DataListItem` インデックスのインデックスを設定します。 `DataListItem` インデックスは `0`から開始されるため、`-1` は安全な選択肢です。
2. データを DataList に再バインドします。 `DataListItem` `ItemIndex` es が DataList s `EditItemIndex`に対応していないため、DataList 全体が読み取り専用モードで表示されます。

これらの手順は、次のイベントハンドラーコードを使用して実行できます。

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample5.vb)]

この追加により、[キャンセル] ボタンをクリックすると、DataList が編集前の状態に戻ります。

最後に完了する必要があるイベントハンドラーは、`UpdateCommand` イベントハンドラーです。 このイベントハンドラーは次のことを行う必要があります。

1. ユーザーが入力した製品名と価格だけでなく、編集した製品 `ProductID`にプログラムによってアクセスします。
2. `ProductsBLL` クラスで適切な `UpdateProduct` オーバーロードを呼び出して、更新プロセスを開始します。
3. DataList s [`EditItemIndex` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)に、存在しない `DataListItem` インデックスのインデックスを設定します。 `DataListItem` インデックスは `0`から開始されるため、`-1` は安全な選択肢です。
4. データを DataList に再バインドします。 `DataListItem` `ItemIndex` es が DataList s `EditItemIndex`に対応していないため、DataList 全体が読み取り専用モードで表示されます。

手順 1. と 2. では、ユーザーの変更を保存します。手順 3. および 4. では、変更が保存された後に、DataList が編集前の状態に戻り、`CancelCommand` イベントハンドラーで実行した手順と同じになります。

更新された製品名と価格を取得するには、`FindControl` メソッドを使用して、`EditItemTemplate`内のテキストボックス Web コントロールをプログラムで参照する必要があります。 また、編集した製品の `ProductID` 値を取得する必要があります。 最初に ObjectDataSource を DataList にバインドしたときに、Visual Studio によって、データソースからの主キーの値 (`ProductID`) に DataList s `DataKeyField` プロパティが割り当てられています。 この値は、DataList s `DataKeys` コレクションから取得できます。 `DataKeyField` プロパティが実際に `ProductID`に設定されていることを確認します。

次のコードは、4つの手順を実装しています。

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample6.vb)]

イベントハンドラーは、`DataKeys` コレクションから編集された製品の `ProductID` を読み取って開始します。 次に、`EditItemTemplate` 内の2つのテキストボックスが参照され、`Text` のプロパティがローカル変数である `productNameValue` および `unitPriceValue`に格納されます。 `Decimal.Parse()` メソッドを使用して `UnitPrice` テキストボックスから値を読み取って、入力された値が通貨記号を持っている場合でも、適切に `Decimal` 値に変換できるようにします。

> [!NOTE]
> [`ProductName`] ボックスと [`UnitPrice`] ボックスの値は、テキストボックスのテキストプロパティに値が指定されている場合にのみ、productNameValue 変数と unitPriceValue 変数に割り当てられます。 それ以外の場合、`Nothing` の値が変数に使用されます。これにより、データベース `NULL` 値を使用してデータを更新する効果があります。 つまり、このコードでは、空の文字列をデータベース `NULL` の値に変換します。これは、GridView、DetailsView、および FormView コントロールでの編集インターフェイスの既定の動作です。

値を読み取った後、`ProductsBLL` クラス s `UpdateProduct` メソッドが呼び出され、製品名、価格、および `ProductID`が渡されます。 イベントハンドラーは、`CancelCommand` イベントハンドラーとまったく同じロジックを使用して、DataList を編集前の状態に戻して完了します。

`EditCommand`、`CancelCommand`、`UpdateCommand` イベントハンドラーが完了すると、訪問者は製品の名前と価格を編集できます。 図14-16 は、この編集ワークフローの動作を示しています。

[![最初にページにアクセスしたときに、すべての製品が読み取り専用モードになります。](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image34.png)

**図 14**: 最初にページにアクセスしたときに、すべての製品が読み取り専用モードになっている ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image36.png)されます)

[製品の名前または価格を更新 ![には、[編集] ボタンをクリックします。](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image37.png)

**図 15**: 製品名または価格を更新するには、[編集] ボタンをクリックします ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image39.png)されます)

[![値を変更した後、[更新] をクリックして読み取り専用モードに戻ります。](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image40.png)

**図 16**: 値を変更した後、[更新] をクリックして読み取り専用モードに戻ります ([クリックすると、フルサイズの画像が表示](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image42.png)されます)

## <a name="step-7-adding-delete-capabilities"></a>手順 7: 削除機能の追加

DataList に削除機能を追加する手順は、編集機能を追加する手順と似ています。 つまり、クリックしたときに `ItemTemplate` に [削除] ボタンを追加する必要があります。

1. `DataKeys` コレクションを使用して、対応する製品の `ProductID` を読み取ります。
2. `ProductsBLL` クラス s `DeleteProduct` メソッドを呼び出すことによって削除を実行します。
3. データを DataList に再バインドします。

まず、[削除] ボタンを `ItemTemplate`に追加します。

クリックすると、`CommandName` が Edit、Update、または Cancel であるボタンによって、DataList s `ItemCommand` イベントが追加のイベントと共に発生します (たとえば、Edit を使用する場合、`EditCommand` イベントも発生します)。 同様に、DataList で `CommandName` プロパティが [削除] に設定されているボタン、LinkButton、または ImageButton は、`DeleteCommand` イベントが発生します (`ItemCommand`)。

`ItemTemplate`の [編集] ボタンの横にある削除ボタンを追加し、その `CommandName` プロパティを [削除] に設定します。 このボタンコントロールを追加した後、`ItemTemplate` の宣言構文は次のようになります。

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample7.aspx)]

次に、次のコードを使用して、DataList s `DeleteCommand` イベントのイベントハンドラーを作成します。

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample8.vb)]

[削除] ボタンをクリックすると、ポストバックが発生し、DataList s `DeleteCommand` イベントが発生します。 イベントハンドラーでは、クリックされた product s `ProductID` の値が `DataKeys` コレクションからアクセスされます。 次に、`ProductsBLL` クラス s `DeleteProduct` メソッドを呼び出すことによって、製品が削除されます。

製品を削除した後、データを DataList (`DataList1.DataBind()`) に再バインドすることが重要です。そうしないと、削除されたばかりの製品が DataList によって引き続き表示されます。

## <a name="summary"></a>まとめ

DataList はポイントを持たないのに対し、GridView によって使用されている編集および削除のサポートはわずかですが、これらの機能を含めるように拡張することができます。 このチュートリアルでは、削除して名前と価格を編集できる2列の製品の一覧を作成する方法を説明しました。 編集と削除のサポートを追加するには、適切な Web コントロールを `ItemTemplate` と `EditItemTemplate`に含め、対応するイベントハンドラーを作成し、ユーザーが入力したキーと主キーの値を読み取り、ビジネスロジック層とやり取りする必要があります。

DataList には基本的な編集機能と削除機能が追加されていますが、高度な機能はありません。 たとえば、入力フィールドの検証は行われません。ユーザーが高価な価格を入力した場合、`Decimal`に対してコストが高すぎると、`Decimal.Parse` によって例外がスローされます。 同様に、ビジネスロジックまたはデータアクセスレイヤーでデータを更新するときに問題が発生した場合は、標準のエラー画面が表示されます。 [削除] ボタンの確認を何も行わないと、誤って製品を削除してしまう可能性があります。

今後のチュートリアルでは、編集中のユーザーエクスペリエンスを向上させる方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Zack Jones、Ken PRandy Isa、および/Midt でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](customizing-the-datalist-s-editing-interface-cs.md)
> [次へ](performing-batch-updates-vb.md)
