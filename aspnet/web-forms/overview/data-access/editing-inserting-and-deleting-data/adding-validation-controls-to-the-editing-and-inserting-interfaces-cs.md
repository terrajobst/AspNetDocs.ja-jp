---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs
title: 編集および挿入インターフェイスに検証コントロールを追加するC#() |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、データ Web コントロールの EditItemTemplate と Insertitemposition に検証コントロールを簡単に追加する方法について説明します。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2086cb1a-ab78-49ae-9c0b-03891c69776a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs
msc.type: authoredcontent
ms.openlocfilehash: 110ee08f1d0707664ef6268f34ceab9da30a3e61
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589628"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-c"></a>編集および挿入インターフェイスに検証コントロールを追加する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_CS.exe)または[PDF のダウンロード](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/datatutorial19cs1.pdf)

> このチュートリアルでは、データ Web コントロールの EditItemTemplate と Insertitemposition に検証コントロールを追加して、より簡単なユーザーインターフェイスを提供することがいかに簡単かを説明します。

## <a name="introduction"></a>はじめに

前の3つのチュートリアルで調査した例の GridView および DetailsView コントロールはすべて、BoundFields と CheckBoxFields (GridView または DetailsView をデータソースにバインドするときに Visual Studio によって自動的に追加されたフィールド型) で構成されています。スマートタグを使用して制御します。 GridView または DetailsView で行を編集するときに、読み取り専用ではない連結されたフィールドは、エンドユーザーが既存のデータを変更できるテキストボックスに変換されます。 同様に、新しいレコードを DetailsView コントロールに挿入する場合、`InsertVisible` プロパティが `true` (既定値) に設定されている連結フィールドは空のテキストボックスとしてレンダリングされ、ユーザーは新しいレコードのフィールド値を指定できます。 同様に、標準の読み取り専用インターフェイスで無効になっている CheckBoxFields は、編集および挿入インターフェイスで有効なチェックボックスに変換されます。

BoundField と CheckBoxField の既定の編集および挿入インターフェイスは役に立ちますが、インターフェイスには何の種類の検証もありません。 ユーザーが `ProductName` フィールドを省略したり、`UnitsInStock` に無効な値 (-50 など) を入力したりしたときに、データ入力の誤りが発生した場合は、アプリケーションアーキテクチャの深さ内から例外が発生します。 この例外は、[前のチュートリアル](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)で説明したように適切に処理できますが、ユーザーが最初に無効なデータを入力しないようにするための検証コントロールが、編集または挿入ユーザーインターフェイスに含まれていることが理想的です。

カスタマイズされた編集または挿入インターフェイスを提供するには、BoundField または CheckBoxField を TemplateField に置き換える必要があります。 TemplateFields は、 [GridView コントロールでの TemplateFields の使用](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)に関するトピックであり、 [DetailsView コントロールのチュートリアルでは templatefields](../custom-formatting/using-templatefields-in-the-detailsview-control-cs.md)を使用して、さまざまな行の状態に対して個別のインターフェイスを定義する複数のテンプレートで構成されています。 TemplateField の `ItemTemplate` は、DetailsView コントロールまたは GridView コントロールで読み取り専用のフィールドまたは行を表示するときに使用されます。一方、`EditItemTemplate` と `InsertItemTemplate` は、それぞれ編集モードと挿入モードで使用するインターフェイスを示します。

このチュートリアルでは、TemplateField の `EditItemTemplate` に検証コントロールを追加して、より簡単なユーザーインターフェイスを提供する `InsertItemTemplate` 方法について説明します。 具体的には、このチュートリアルでは、「[挿入、更新、削除に関連するイベントの調査](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)」で作成した例を使用して、適切な検証を含むように編集および挿入インターフェイスを強化します。

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-csmd"></a>手順 1:[挿入、更新、および削除に関連付けられたイベントを調べる](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)例をレプリケートする

[「挿入、更新、および削除](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)」チュートリアルに関連するイベントを確認すると、編集可能な GridView で製品の名前と価格を記載したページが作成されました。 また、ページには、`DefaultMode` プロパティが `Insert`に設定されている DetailsView が含まれており、これによって常に挿入モードでレンダリングされます。 この DetailsView から、ユーザーは新しい製品の名前と価格を入力し、[挿入] をクリックして、システムに追加することができます (図1を参照)。

[前の例を ![すると、新しい製品を追加したり、既存の製品を編集したりすることができます。](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image1.png)

**図 1**: 前の例では、ユーザーが新しい製品を追加し、既存の製品を編集できるようにします ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image3.png)されます)

このチュートリアルの目的は、検証コントロールを提供するように DetailsView と GridView を拡張することです。 特に、検証ロジックは次のようになります。

- 製品の挿入時または編集時に名前を指定する必要があります
- レコードを挿入するときに価格を指定する必要があります。レコードを編集する場合でも価格は必要ですが、前のチュートリアルで既に存在している GridView の `RowUpdating` イベントハンドラーでプログラムロジックを使用します。
- 価格に入力した値が有効な通貨書式であることを確認します。

前の例を補強して検証を含める方法については、まず、`DataModificationEvents.aspx` ページからこのチュートリアルのページ (`UIValidation.aspx`) にこの例をレプリケートする必要があります。 これを実現するには、`DataModificationEvents.aspx` ページの宣言型マークアップとソースコードの両方をコピーする必要があります。 次の手順を実行して、最初に宣言マークアップをコピーします。

1. Visual Studio で [`DataModificationEvents.aspx`] ページを開く
2. ページの宣言型マークアップにアクセスします (ページの下部にある [ソース] ボタンをクリックします)。
3. 図2に示すように、`<asp:Content>` タグと `</asp:Content>` タグ (行 3 ~ 44) 内のテキストをコピーします。

[&lt;asp: Content&gt; コントロール内のテキストをコピー ![には](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image4.png)

**図 2**: `<asp:Content>` コントロール内のテキストをコピー[する (クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image6.png)されます)

1. [`UIValidation.aspx`] ページを開く
2. ページの宣言型マークアップにアクセスする
3. `<asp:Content>` コントロール内にテキストを貼り付けます。

ソースコードをコピーするには、[`DataModificationEvents.aspx.cs`] ページを開き、`EditInsertDelete_DataModificationEvents` クラス*内*のテキストだけをコピーします。 3つのイベントハンドラー (`Page_Load`、`GridView1_RowUpdating`、および `ObjectDataSource1_Inserting`) をコピーしますが、クラス宣言または `using` ステートメント**をコピーしないでください。** コピーしたテキストを `UIValidation.aspx.cs`の `EditInsertDelete_UIValidation` クラス*内*に貼り付けます。

コンテンツとコードを `DataModificationEvents.aspx` から `UIValidation.aspx`に移動したら、ブラウザーで進行状況をテストしてみましょう。 同じ出力が表示され、これらの2つの各ページで同じ機能が使用されます (「操作中」 `DataModificationEvents.aspx` のスクリーンショットについては、図1を参照してください)。

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>手順 2: BoundFields を TemplateFields に変換する

編集および挿入インターフェイスに検証コントロールを追加するには、DetailsView コントロールと GridView コントロールで使用される BoundFields を TemplateFields に変換する必要があります。 これを実現するには、GridView および DetailsView のスマートタグの [列の編集] リンクと [フィールドの編集] リンクをそれぞれクリックします。 ここで、各 BoundFields を選択し、[このフィールドを TemplateField に変換する] リンクをクリックします。

[各 DetailsView のおよび GridView の BoundFields を TemplateFields に変換 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image7.png)

**図 3**: DetailsView の各フィールドと GridView の Boundfields を templatefields に変換[する (クリックしてフルサイズのイメージを表示する](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image9.png))

[フィールド] ダイアログボックスを使用して BoundField を TemplateField に変換すると、BoundField 自体と同じ読み取り専用、編集、および挿入インターフェイスを示す TemplateField が生成されます。 次のマークアップは、TemplateField に変換された後の DetailsView の `ProductName` フィールドの宣言構文を示しています。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample1.aspx)]

この TemplateField には、`ItemTemplate`、`EditItemTemplate`、`InsertItemTemplate`という3つのテンプレートが自動的に作成されていることに注意してください。 `ItemTemplate` には、ラベル Web コントロールを使用して1つのデータフィールド値 (`ProductName`) が表示されます。一方、`EditItemTemplate` と `InsertItemTemplate` では、双方向のデータバインディングを使用して、データフィールドをテキストボックスの `Text` プロパティに関連付けている TextBox Web コントロールにデータフィールド値が表示されます。 ここでは、挿入のためにこのページの DetailsView のみを使用しているので、2つの TemplateFields から `ItemTemplate` と `EditItemTemplate` を削除できますが、そのままにしても問題はありません。

GridView では DetailsView の組み込み挿入機能がサポートされていないため、GridView の `ProductName` フィールドを TemplateField に変換すると、`ItemTemplate` と `EditItemTemplate`のみになります。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample2.aspx)]

[このフィールドを TemplateField に変換する] をクリックすると、Visual Studio によって TemplateField が作成され、そのテンプレートが変換された BoundField のユーザーインターフェイスを模倣します。 これを確認するには、ブラウザーを使用してこのページにアクセスします。 代わりに、BoundFields が使用されていた場合は、TemplateFields の外観と動作が同じであることがわかります。

> [!NOTE]
> 必要に応じて、テンプレートの編集インターフェイスを自由にカスタマイズできます。 たとえば、`UnitPrice` TemplateFields のテキストボックスを、`ProductName` テキストボックスよりも小さなテキストボックスとして表示したい場合があります。 これを実現するには、TextBox の `Columns` プロパティを適切な値に設定するか、`Width` プロパティを使用して絶対幅を指定します。 次のチュートリアルでは、テキストボックスを代替データ入力 Web コントロールに置き換えることにより、編集インターフェイスを完全にカスタマイズする方法について説明します。

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>手順 3: GridView の`EditItemTemplate` s に検証コントロールを追加する

データ入力フォームを構築するときは、ユーザーが必要なフィールドを入力し、指定されたすべての入力が有効で適切に書式設定された値であることが重要です。 ユーザーの入力が有効であることを確認するために、ASP.NET には、単一の入力コントロールの値を検証するために使用するように設計された5つの組み込みの検証コントロールが用意されています。

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)は、値が指定されていることを確認します。
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)は、別の Web コントロール値または定数値に対して値を検証したり、指定されたデータ型に対して値の形式が有効であることを確認したりします。
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)値が値の範囲内にあることを確認します。
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) [正規表現](http://en.wikipedia.org/wiki/Regular_expression)に対して値を検証します。
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)カスタムのユーザー定義メソッドに対して値を検証します。

これらの5つのコントロールの詳細については、 [ASP.NET のクイックスタートチュートリアル](https://asp.net/QuickStart/aspnet/)の[「検証コントロール」セクション](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx)を参照してください。

このチュートリアルでは、DetailsView と GridView の `ProductName` TemplateFields の両方で RequiredFieldValidator と、DetailsView の `UnitPrice` TemplateField の RequiredFieldValidator を使用する必要があります。 さらに、入力した価格の値が0以上で、有効な通貨形式で表示されるように、両方のコントロールの `UnitPrice` TemplateFields に CompareValidator を追加する必要があります。

> [!NOTE]
> ASP.NET 1.x にはこれらの5つの検証コントロールがありましたが、ASP.NET 2.0 には、Internet Explorer 以外のブラウザーでのクライアント側スクリプトの主なサポートと、ページ上の検証コントロールをパーティション分割する機能の2つがあります。検証グループ。 2\.0 の新しい検証コントロール機能の詳細については、「 [ASP.NET 2.0 の検証コントロールの解説」](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)を参照してください。

まず、必要な検証コントロールを GridView の TemplateFields の `EditItemTemplate` に追加します。 これを実現するには、GridView のスマートタグの [テンプレートの編集] リンクをクリックして、テンプレート編集インターフェイスを表示します。 ここでは、ドロップダウンリストから編集するテンプレートを選択できます。 編集インターフェイスを拡張する必要があるため、`ProductName` と `UnitPrice`の `EditItemTemplate` に検証コントロールを追加する必要があります。

[![ProductName と UnitPrice の EditItemTemplates を拡張する必要があります。](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image10.png)

**図 4**: `ProductName` と `UnitPrice`の `EditItemTemplate` を拡張する必要があります ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image12.png)されます)

`ProductName` `EditItemTemplate`で、[ツールボックス] から RequiredFieldValidator を追加し、テキストボックスの後に配置します。

[RequiredFieldValidator を ProductName EditItemTemplate に追加 ![には](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image13.png)

**図 5**: `ProductName` `EditItemTemplate` に RequiredFieldValidator を追加する ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image15.png)されます)

すべての検証コントロールは、単一の ASP.NET Web コントロールの入力を検証することによって機能します。 そのため、追加した RequiredFieldValidator が `EditItemTemplate`のテキストボックスに対して検証する必要があることを示す必要があります。これは、検証コントロールの[ControlToValidate プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)を適切な Web コントロールの `ID` に設定することによって実現されます。 現在、テキストボックスには、`TextBox1`の nondescript `ID` がありますが、それをより適切なものに変更してみましょう。 テンプレートのテキストボックスをクリックし、プロパティウィンドウから、`ID` を `TextBox1` から `EditProductName`に変更します。

[テキストボックスの ID を EditProductName に変更 ![には](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image16.png)

**図 6**: テキストボックスの `ID` を `EditProductName` に変更する ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image18.png)されます)

次に、RequiredFieldValidator の `ControlToValidate` プロパティを `EditProductName`に設定します。 最後に、 [ErrorMessage プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)を "製品の名前を指定する必要があります" と[Text プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)を "\*" に設定します。 `Text` プロパティ値 (指定されている場合) は、検証が失敗した場合に検証コントロールによって表示されるテキストです。 必須である `ErrorMessage` プロパティ値は、ValidationSummary コントロールによって使用されます。`Text` プロパティ値を省略した場合、`ErrorMessage` プロパティ値は、無効な入力に対して検証コントロールによって表示されるテキストでもあります。

RequiredFieldValidator の3つのプロパティを設定した後、画面は図7のようになります。

[RequiredFieldValidator の ControlToValidate、ErrorMessage、および Text プロパティを設定 ![には](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image19.png)

**図 7**: RequiredFieldValidator の `ControlToValidate`、`ErrorMessage`、および `Text` の各プロパティを設定[する (クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image21.png)されます)

`ProductName` `EditItemTemplate`に追加された RequiredFieldValidator を使用すると、必要な検証が `UnitPrice` `EditItemTemplate`に追加されます。 このページでは、`UnitPrice` はレコードを編集するときには省略可能であると判断したため、RequiredFieldValidator を追加する必要はありません。 ただし、CompareValidator を追加して、指定されている場合は、`UnitPrice`が通貨として正しく書式設定され、0以上であることを確認する必要があります。

`UnitPrice` `EditItemTemplate`に CompareValidator を追加する前に、まず、TextBox Web コントロールの ID を `TextBox2` から `EditUnitPrice`に変更してみましょう。 この変更を行った後、CompareValidator を追加し、その `ControlToValidate` プロパティを `EditUnitPrice`に設定します。その `ErrorMessage` プロパティを「0以上である必要があり、通貨記号を含めることはできません」と `Text` プロパティを「\*」に設定します。

`UnitPrice` 値が0以上である必要があることを示すには、CompareValidator の[Operator プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)を `GreaterThanEqual`に、 [valuetocompare プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)を "0" に設定し、その[Type プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)を `Currency`に設定します。 次の宣言構文は、これらの変更が加えられた後の `UnitPrice` TemplateField の `EditItemTemplate` を示しています。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample3.aspx)]

これらの変更を行った後、ブラウザーでページを開きます。 製品を編集するときに名前を省略したり、無効な価格値を入力しようとしたりすると、テキストボックスの横にアスタリスクが表示されます。 図8に示すように、$19.95 などの通貨記号を含む価格値は無効と見なされます。 CompareValidator の `Currency` `Type` では、桁区切り記号 (カルチャの設定によってはコンマやピリオドなど) と先頭の正符号または負符号を使用できますが、通貨記号は許可*されません*。 この動作は、現在、編集インターフェイスが通貨書式を使用して `UnitPrice` を表示するときに、ユーザーによって変更される可能性があります。

> [!NOTE]
> *挿入、更新、および削除のチュートリアルに関連付けられ*ているイベントで、BoundField の `DataFormatString` プロパティを `{0:c}` に設定して、通貨として書式設定することを思い出してください。 さらに、`ApplyFormatInEditMode` プロパティを true に設定すると、GridView の編集インターフェイスによって `UnitPrice` が通貨として書式設定されます。 BoundField を TemplateField に変換すると、Visual Studio はこれらの設定を書き留め、データバインド構文 `<%# Bind("UnitPrice", "{0:c}") %>`を使用して、テキストボックスの `Text` プロパティを通貨として書式設定します。

[無効な入力のテキストボックスの横にアスタリスクが表示され ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image22.png)

**図 8**: 無効な入力のテキストボックスの横にアスタリスクが表示される ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image24.png)されます)

検証はそのままの状態で機能しますが、ユーザーはレコードを編集するときに通貨記号を手動で削除する必要があります。これは許容できません。 これを解決するには、次の3つのオプションがあります。

1. `UnitPrice` の値が通貨として書式設定されないように `EditItemTemplate` を構成します。
2. ユーザーが通貨記号を入力できるようにするには、CompareValidator を削除し、適切に書式設定された通貨値を適切にチェックする RegularExpressionValidator に置き換えます。 ここでの問題は、通貨の値を検証する正規表現が、カルチャの設定を組み込む必要がある場合にコードを記述しなければならないということです。
3. 検証コントロールを完全に削除し、GridView の `RowUpdating` イベントハンドラーでサーバー側の検証ロジックに依存します。

この演習では、オプション #1 に移りましょう。 現在、`UnitPrice` は、`EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`のテキストボックスのデータバインド式により、通貨として書式設定されます。 Bind ステートメントを `Bind("UnitPrice", "{0:n2}")`に変更します。これにより、結果が2桁の精度で数値として書式設定されます。 これを行うには、宣言型の構文を使用するか、`UnitPrice` TemplateField の `EditItemTemplate` の [`EditUnitPrice`] ボックスの [連結の編集] リンクをクリックします (図9と10を参照)。

[テキストボックスの [連結の編集] リンクをクリック ![ます。](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image25.png)

**図 9**: テキストボックスの [相互接続の編集] リンクをクリック[する (クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image27.png)されます)

[![、バインドステートメントで書式指定子を指定します。](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image28.png)

**図 10**: `Bind` ステートメントで書式指定子を指定[する (クリックしてフルサイズのイメージを表示する](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image30.png))

この変更により、編集インターフェイスの書式設定された価格には、桁区切り記号としてコンマが、小数点区切り文字としてピリオドが付きますが、通貨記号はオフのままになります。

> [!NOTE]
> `UnitPrice` `EditItemTemplate` には RequiredFieldValidator が含まれていないため、議論にポストバックし、更新ロジックを開始することができます。 ただし、「*挿入、更新、および削除」チュートリアルに関連付けられているイベントを調べ*てからコピーした `RowUpdating` イベントハンドラーには、`UnitPrice` が確実に提供されるようにプログラムによる確認が含まれています。 このロジックを削除するか、そのままにしておくか、`UnitPrice` `EditItemTemplate`に RequiredFieldValidator を追加してください。

## <a name="step-4-summarizing-data-entry-problems"></a>手順 4: データ入力の問題の概要

5つの検証コントロールに加えて、ASP.NET には[Validationsummary コントロール](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)が含まれています。このコントロールには、無効なデータを検出した検証コントロールの `ErrorMessage` が表示されます。 この概要データは、web ページ上のテキストとして、またはモーダルのクライアント側のメッセージボックスを使用して表示できます。 このチュートリアルを強化し、検証の問題を要約するクライアント側のメッセージボックスを追加してみましょう。

これを実現するには、[ツールボックス] から [ValidationSummary] コントロールをデザイナーにドラッグします。 検証コントロールの場所は、概要を messagebox としてのみ表示するように構成するため、本当に重要ではありません。 コントロールを追加した後、 [Showsummary プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)を `false` に設定し、 [showsummary プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)を `true`に設定します。 この追加により、すべての検証エラーがクライアント側のメッセージボックスにまとめられます。

[検証エラーがクライアント側のメッセージボックスにまとめられている ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image31.png)

**図 11**: 検証エラーがクライアント側のメッセージボックスにまとめられている ([クリックしてフルサイズのイメージを表示する](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image33.png))

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>手順 5: DetailsView の`InsertItemTemplate` に検証コントロールを追加する

このチュートリアルでは、検証コントロールを DetailsView の挿入インターフェイスに追加します。 DetailsView のテンプレートに検証コントロールを追加するプロセスは、手順3で確認したものと同じです。このため、この手順では簡単に説明します。 GridView の `EditItemTemplate` で行ったように、テキストボックスの `ID` の名前を nondescript `TextBox1` から `InsertProductName` に変更し、`TextBox2` することをお勧めします。

`ProductName` `InsertItemTemplate`に RequiredFieldValidator を追加します。 `ControlToValidate` を、テンプレートのテキストボックスの `ID` に設定し、その `Text` プロパティを "\*" に設定し、その `ErrorMessage` プロパティを「製品の名前を指定する必要があります」に設定します。

新しいレコードを追加するときにこのページに `UnitPrice` が必要になるため、`UnitPrice` `InsertItemTemplate`に RequiredFieldValidator を追加し、その `ControlToValidate`、`Text`、および `ErrorMessage` の各プロパティを適切に設定します。 最後に、CompareValidator を `UnitPrice` `InsertItemTemplate` に追加して、`ControlToValidate`、`Text`、`ErrorMessage`、`Type`、`Operator`、および `ValueToCompare` の各プロパティを構成します。これは、GridView の `UnitPrice`で `EditItemTemplate`の CompareValidator を使用したのと同じです。

これらの検証コントロールを追加した後、名前が指定されていない場合、またはその価格が負の数値または不適切な形式である場合、システムに新しい製品を追加することはできません。

[![検証ロジックが DetailsView の挿入インターフェイスに追加されました](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image34.png)

**図 12**: DetailsView の挿入インターフェイスに検証ロジックが追加されました ([クリックすると、フルサイズのイメージが表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image36.png)されます)

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>手順 6: 検証コントロールを検証グループに分割する

このページは、論理的に異なる2つの検証コントロールセットで構成されています。これは、GridView の編集インターフェイスに対応するものと、DetailsView の挿入インターフェイスに対応するものです。 既定では、ポストバックが発生すると、ページ上の*すべて*の検証コントロールがチェックされます。 ただし、レコードを編集するときに、DetailsView の挿入インターフェイスの検証コントロールで検証を行わないようにします。 図13は、ユーザーが完全に有効な値を持つ製品を編集しているときの現在のジレンマを示しています。 [更新] をクリックすると、挿入インターフェイスの名前と価格値が空白になっているため、検証エラーが発生します。

[製品を更新 ![と、挿入インターフェイスの検証コントロールが起動されます。](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image37.png)

**図 13**: 製品を更新すると、挿入インターフェイスの検証コントロールが起動します ([クリックすると、フルサイズのイメージが表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image39.png)されます)

ASP.NET 2.0 の検証コントロールは、`ValidationGroup` プロパティを使用して検証グループにパーティション分割できます。 グループ内の一連の検証コントロールを関連付けるには、単に `ValidationGroup` プロパティを同じ値に設定します。 このチュートリアルでは、GridView の TemplateFields フィールドの検証コントロールの `ValidationGroup` プロパティを `EditValidationControls` に設定し、DetailsView の TemplateFields の `ValidationGroup` プロパティを `InsertValidationControls`に設定します。 これらの変更は、宣言マークアップで直接行うことも、デザイナーのテンプレートの編集インターフェイスを使用する場合はプロパティウィンドウを使用して行うこともできます。

検証コントロールに加えて、ASP.NET 2.0 のボタンおよびボタン関連のコントロールには `ValidationGroup` プロパティも含まれています。 検証グループの検証コントロールは、同じ `ValidationGroup` プロパティ設定を持つボタンによってポストバックが発生した場合にのみ、有効性がチェックされます。 たとえば、DetailsView の Insert ボタンを使用して `InsertValidationControls` 検証グループをトリガーするには、CommandField の `ValidationGroup` プロパティを `InsertValidationControls` に設定する必要があります (図14を参照)。 さらに、GridView の CommandField's `ValidationGroup` プロパティを `EditValidationControls`に設定します。

[DetailsView の CommandField's ValidationGroup プロパティを InsertValidationControls に設定 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image40.png)

**図 14**: DetailsView の commandfield's `ValidationGroup` プロパティを `InsertValidationControls` に設定する ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image42.png)されます)

これらの変更が完了すると、DetailsView および GridView の TemplateFields および CommandFields は次のようになります。

DetailsView の TemplateFields および CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample4.aspx)]

GridView の CommandField フィールドと TemplateFields

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample5.aspx)]

この時点で、編集固有の検証コントロールは、GridView の [更新] ボタンがクリックされ、DetailsView の [挿入] ボタンがクリックされたときにのみ、挿入固有の検証コントロールが起動し、図13で強調表示されている問題を解決します。 ただし、この変更により、無効なデータを入力したときに ValidationSummary コントロールが表示されなくなりました。 ValidationSummary コントロールには、`ValidationGroup` プロパティも含まれており、検証グループ内の検証コントロールの概要情報のみが表示されます。 したがって、このページには、`InsertValidationControls` 検証グループ用と `EditValidationControls`用の2つの検証コントロールが必要です。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample6.aspx)]

この追加により、チュートリアルは完了です。

## <a name="summary"></a>要約

BoundFields は挿入と編集の両方のインターフェイスを提供できますが、インターフェイスはカスタマイズできません。 一般的には、ユーザーが必要な入力を正しい形式で入力できるように、編集および挿入インターフェイスに検証コントロールを追加します。 これを実現するには、BoundFields を TemplateFields に変換し、適切なテンプレートに検証コントロールを追加する必要があります。 このチュートリアルでは、「*挿入、更新、および削除」チュートリアルに関連付けられているイベントを調べ*、DetailsView の挿入インターフェイスと GridView の編集インターフェイスの両方に検証コントロールを追加して、この例を拡張しています。 さらに、ValidationSummary コントロールを使用して概要検証情報を表示する方法と、ページ上の検証コントロールを個別の検証グループに分割する方法についても説明しました。

このチュートリアルで説明したように、TemplateFields を使用すると、編集および挿入インターフェイスを拡張して検証コントロールを含めることができます。 TemplateFields を拡張して追加の入力 Web コントロールを含めることもできます。これにより、テキストボックスをより適切な Web コントロールに置き換えることができます。 次のチュートリアルでは、テキストボックスコントロールをデータバインド DropDownList コントロールに置き換える方法について説明します。これは、外部キー (`CategoryID`、`Products` テーブル内の `SupplierID` など) を編集する場合に最適です。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Liz Shulok と Zack Jones でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
> [次へ](customizing-the-data-modification-interface-cs.md)
