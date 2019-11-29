---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
title: DataList の編集インターフェイスに検証コントロールを追加する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ユーザーがより安全に編集できるように、DataList の EditItemTemplate に検証コントロールを追加することがいかに簡単かを説明します。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 6b073fc6-524d-453d-be7c-0c30986de391
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: f952a7bb95e956a2ad935f8bdef5c3efa7437ecb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621962"
---
# <a name="adding-validation-controls-to-the-datalists-editing-interface-vb"></a>DataList の編集インターフェイスに検証コントロールを追加する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_VB.exe)または[PDF のダウンロード](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/datatutorial39vb1.pdf)

> このチュートリアルでは、簡単に編集できるユーザーインターフェイスを提供するために、DataList の EditItemTemplate に検証コントロールを追加することがいかに簡単かを説明します。

## <a name="introduction"></a>はじめに

これまでの DataList 編集チュートリアルでは、製品名や負の価格などの無効なユーザー入力によって例外が発生した場合でも、DataLists 編集インターフェイスにプロアクティブなユーザー入力の検証が含まれていません。 前の[チュートリアル](handling-bll-and-dal-level-exceptions-vb.md)では、発生した例外に関する情報をキャッチして適切に表示するために、DataList s `UpdateCommand` イベントハンドラーに例外処理コードを追加する方法を説明しました。 ただし、編集インターフェイスには、ユーザーがこのような無効なデータを最初に入力できないようにするための検証コントロールが含まれていることが理想的です。

このチュートリアルでは、簡単に編集できるユーザーインターフェイスを提供するために、DataList s `EditItemTemplate` に検証コントロールを追加することがいかに簡単かを説明します。 具体的には、このチュートリアルでは、前のチュートリアルで作成した例を使用して、適切な検証を含むように編集インターフェイスを強化します。

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-vbmd"></a>手順 1:[BLL および DAL レベルの例外の処理](handling-bll-and-dal-level-exceptions-vb.md)から例をレプリケートする

「 [BLL および DAL レベルの例外の処理](handling-bll-and-dal-level-exceptions-vb.md)」チュートリアルでは、2列の編集可能な DataList で製品の名前と価格を記載したページを作成しました。 このチュートリアルの目的は、DataList s 編集インターフェイスを拡張して検証コントロールを含めることです。 特に、検証ロジックは次のようになります。

- 製品名を指定する必要があります
- 価格に入力した値が有効な通貨書式であることを確認します。
- 負の `UnitPrice` 値が無効であるため、価格に入力した値が0以上であることを確認します。

前の例を補強して検証を含める方法を確認する前に、まず、`EditDeleteDataList` フォルダーの [`ErrorHandling.aspx`] ページから、このチュートリアルの `UIValidation.aspx`のページに例をレプリケートする必要があります。 これを実現するには、`ErrorHandling.aspx` ページの宣言型マークアップとソースコードの両方をコピーする必要があります。 次の手順を実行して、最初に宣言マークアップをコピーします。

1. Visual Studio で [`ErrorHandling.aspx`] ページを開く
2. ページの宣言マークアップにアクセスします (ページの下部にある [ソース] ボタンをクリックします)。
3. 図1に示すように、`<asp:Content>` タグと `</asp:Content>` タグ (行 3 ~ 32) 内のテキストをコピーします。

[&lt;asp: Content&gt; コントロール内のテキストをコピー ![には](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image1.png)

**図 2**: `<asp:Content>` コントロール内のテキストをコピー[する (クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image3.png)されます)

1. [`UIValidation.aspx`] ページを開く
2. ページの宣言型マークアップにアクセスする
3. `<asp:Content>` コントロール内にテキストを貼り付けます。

ソースコードをコピーするには、[`ErrorHandling.aspx.vb`] ページを開き、`EditDeleteDataList_ErrorHandling` クラス*内*のテキストだけをコピーします。 3つのイベントハンドラー (`Products_EditCommand`、`Products_CancelCommand`、`Products_UpdateCommand`) を `DisplayExceptionDetails` メソッドと共にコピーします。ただし、クラス宣言または `using` ステートメント**はコピーしないでください。** コピーしたテキストを `UIValidation.aspx.vb`の `EditDeleteDataList_UIValidation` クラス*内*に貼り付けます。

コンテンツとコードを `ErrorHandling.aspx` から `UIValidation.aspx`に移動したら、ブラウザーでページをテストしてみましょう。 同じ出力が表示され、これらの2つのページで同じ機能が使用されます (図2を参照)。

[UIValidation .aspx ページを ![と、ErrorHandling の機能が模倣されます。](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image4.png)

**図 2**: [`UIValidation.aspx`] ページでは `ErrorHandling.aspx` の機能を模倣しています ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image6.png)されます)。

## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>手順 2: DataList s EditItemTemplate に検証コントロールを追加する

データ入力フォームを構築するときは、ユーザーが必要なフィールドを入力し、指定されたすべての入力が有効で適切に書式設定された値であることが重要です。 ユーザーの入力が有効であることを確認するために、ASP.NET には、単一の入力 Web コントロールの値を検証するように設計された5つの組み込みの検証コントロールが用意されています。

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)は、値が指定されていることを確認します。
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)は、別の Web コントロール値または定数値に対して値を検証したり、指定されたデータ型に対して値の形式が有効であることを確認したりします。
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)値が値の範囲内にあることを確認します。
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) [正規表現](http://en.wikipedia.org/wiki/Regular_expression)に対して値を検証します。
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)カスタムのユーザー定義メソッドに対して値を検証します。

これらの5つのコントロールの詳細については、「[インターフェイスの編集と挿入](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)」チュートリアルの「検証コントロールの追加」を参照してください。または、 [ASP.NET のクイックスタートチュートリアル](https://quickstarts.asp.net)の[「検証コントロール」セクション](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx)をご覧ください。

このチュートリアルでは、RequiredFieldValidator を使用して製品名の値が指定されていることを確認し、入力した価格の値が0以上で、有効な通貨の形式で表示されるように CompareValidator を使用する必要があります。

> [!NOTE]
> ASP.NET 1.x には、これらと同じ5つの検証コントロールがありましたが、ASP.NET 2.0 にはいくつかの改善点が追加されており、Internet Explorer だけでなく、ページ上の検証コントロールをパーティション分割する機能も用意されています。検証グループ。 2\.0 の新しい検証コントロール機能の詳細については、「 [ASP.NET 2.0 の検証コントロールの解説」](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)を参照してください。

まず、必要な検証コントロールを DataList s `EditItemTemplate`に追加します。 このタスクを実行するには、デザイナーを使用して、DataList s スマートタグの [テンプレートの編集] リンクをクリックするか、宣言型の構文を使用します。 ここでは、デザインビューの [テンプレートの編集] オプションを使用してプロセスをステップ実行します。 DataList s `EditItemTemplate`の編集を選択したら、[ツールボックス] から [RequiredFieldValidator] を追加し、[`ProductName`] ボックスの後に配置します。

[RequiredFieldValidator を ProductName テキストボックスの後の EditItemTemplate に追加 ![には](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image7.png)

**図 3**: `ProductName` テキストボックス `EditItemTemplate After` に RequiredFieldValidator を追加する ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image9.png)されます)

すべての検証コントロールは、単一の ASP.NET Web コントロールの入力を検証することによって機能します。 そのため、追加した RequiredFieldValidator が `ProductName` TextBox に対して検証する必要があることを示す必要があります。これを行うには、[検証コントロール s [`ControlToValidate`] プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)を適切な Web コントロール (このインスタンスでは`ProductName`) の `ID` に設定します。 次に、 [`ErrorMessage` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)をに設定して、製品名と[`Text` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)を \*に指定する必要があります。 `Text` プロパティ値 (指定されている場合) は、検証が失敗した場合に検証コントロールによって表示されるテキストです。 必須である `ErrorMessage` プロパティ値は、ValidationSummary コントロールによって使用されます。`Text` プロパティ値を省略した場合、無効な入力に対して検証コントロールによって `ErrorMessage` プロパティ値が表示されます。

RequiredFieldValidator の3つのプロパティを設定した後、画面は図4のようになります。

[RequiredFieldValidator s ControlToValidate、ErrorMessage、および Text プロパティを設定 ![には](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image10.png)

**図 4**: RequiredFieldValidator s `ControlToValidate`、`ErrorMessage`、および `Text` の各プロパティを設定[する (クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image12.png)されます)

`EditItemTemplate`に追加された RequiredFieldValidator を使用して、製品の [価格] ボックスに必要な検証を追加します。 `UnitPrice` はレコードを編集するときには省略可能であるため、RequiredFieldValidator を追加する必要はありません。 ただし、CompareValidator を追加して、指定されている場合は、`UnitPrice`が通貨として正しく書式設定され、0以上であることを確認する必要があります。

`EditItemTemplate` に CompareValidator を追加し、その `ControlToValidate` プロパティを `UnitPrice`に設定します。その `ErrorMessage` プロパティには、0以上の値を指定する必要があります。また、通貨記号を含めることはできず、`Text` にはその \*プロパティを指定する必要があります。 `UnitPrice` 値が0以上である必要があることを示すには、CompareValidator s [`Operator` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)を `GreaterThanEqual`に、その[`ValueToCompare` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)を0に設定し、その[`Type` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)を `Currency`に設定します。

これら2つの検証コントロールを追加した後、DataList s `EditItemTemplate` s 宣言構文は次のようになります。

[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

これらの変更を行った後、ブラウザーでページを開きます。 製品を編集するときに名前を省略したり、無効な価格値を入力しようとしたりすると、テキストボックスの横にアスタリスクが表示されます。 図5に示すように、$19.95 などの通貨記号を含む価格値は無効と見なされます。 CompareValidator s `Currency` `Type` では、桁区切り記号 (カルチャの設定によってはコンマやピリオドなど) と先頭の正符号または負符号を使用できますが、通貨記号は許可*されません*。 この動作は、現在、編集インターフェイスが通貨書式を使用して `UnitPrice` を表示するときに、ユーザーによって変更される可能性があります。

[無効な入力のテキストボックスの横にアスタリスクが表示され ![](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image13.png)

**図 5**: 無効な入力のテキストボックスの横にアスタリスクが表示される ([クリックすると、フルサイズの画像が表示](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image15.png)されます)

検証はそのままの状態で機能しますが、ユーザーはレコードを編集するときに通貨記号を手動で削除する必要があります。これは許容できません。 さらに、編集インターフェイスに無効な入力がある場合、[Update] ボタンと [Cancel] ボタンをクリックしても、ポストバックが呼び出されます。 [キャンセル] ボタンは、ユーザーの入力が有効であるかどうかに関係なく、DataList を編集前の状態に戻すのが理想的です。 また、DataList s `UpdateCommand` イベントハンドラーで製品情報を更新する前に、ページのデータが有効であることを確認する必要があります。これは、ブラウザーが JavaScript をサポートしていないか、サポートが無効になっているユーザーが、検証コントロールのクライアント側ロジックをバイパスできるためです。

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>EditItemTemplate s UnitPrice テキストボックスから通貨記号を削除する

CompareValidator s `Currency``Type`を使用する場合、検証対象の入力に通貨記号を含めることはできません。 このようなシンボルが存在する場合、CompareValidator は入力を無効としてマークします。 ただし、現在の編集インターフェイスには、`UnitPrice` テキストボックスに通貨記号が含まれています。つまり、ユーザーは、変更を保存する前に通貨記号を明示的に削除する必要があります。 これを解決するには、次の3つのオプションがあります。

1. `UnitPrice` テキストボックスの値が通貨として書式設定されないように `EditItemTemplate` を構成します。
2. ユーザーが通貨記号を入力できるようにするには、CompareValidator を削除し、適切に書式設定された通貨値を確認する RegularExpressionValidator に置き換えます。 ここでの課題は、通貨の値を検証する正規表現が CompareValidator ほど単純ではなく、カルチャの設定を組み込む必要がある場合にコードを記述する必要があることです。
3. 検証コントロールを完全に削除し、GridView s `RowUpdating` イベントハンドラーでカスタムのサーバー側検証ロジックに依存します。

このチュートリアルでは、オプション1を使ってみましょう。 現在、`UnitPrice` は、`EditItemTemplate`: `<%# Eval("UnitPrice", "{0:c}") %>`のテキストボックスのデータバインド式により、通貨値として書式設定されます。 `Eval` ステートメントを `Eval("UnitPrice", "{0:n2}")`に変更します。これにより、結果が2桁の精度で数値として書式設定されます。 これを行うには、宣言型の構文を使用するか、DataList s `EditItemTemplate`の [`UnitPrice`] ボックスの [連結の編集] リンクをクリックします。

この変更により、編集インターフェイスの書式設定された価格には、桁区切り記号としてコンマが、小数点区切り文字としてピリオドが付きますが、通貨記号はオフのままになります。

> [!NOTE]
> 編集可能なインターフェイスから通貨書式を削除する場合は、テキストボックスの外側に通貨記号をテキストとして配置すると便利です。 これは、ユーザーが通貨記号を指定する必要がないことを示すヒントとして機能します。

## <a name="fixing-the-cancel-button"></a>[キャンセル] ボタンの修正

既定では、検証 Web コントロールは、クライアント側で検証を実行する JavaScript を生成します。 ボタン、LinkButton、または ImageButton がクリックされると、ポストバックが発生する前に、ページの検証コントロールがクライアント側でチェックされます。 無効なデータがある場合、ポストバックはキャンセルされます。 ただし、特定のボタンについては、データの有効性が問題でになることがあります。このような場合、データが無効であるためにポストバックがキャンセルされることは厄介です。

このような場合は、[キャンセル] ボタンが使用されます。 たとえば、製品名を省略した場合など、ユーザーが無効なデータを入力した後、製品を保存しないことを決定し、[キャンセル] ボタンをクリックしたとします。 現在、[キャンセル] ボタンをクリックすると、ページの検証コントロールがトリガーされ、製品名がないことを報告し、ポストバックを防止できます。 編集プロセスをキャンセルするには、ユーザーが `ProductName` テキストボックスにテキストを入力する必要があります。

幸いにも、ボタン、LinkButton、および ImageButton には、ボタンをクリックして検証ロジックを開始するかどうかを示す[`CausesValidation` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx)があります (既定では `True`)。 Cancel ボタン s `CausesValidation` プロパティを `False`に設定します。

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>UpdateCommand イベントハンドラーで入力が有効であることを確認する

検証コントロールによって出力されるクライアント側スクリプトにより、ユーザーが無効な入力を入力した場合、検証コントロールは、`CausesValidation` プロパティが `True` (既定値) になっているボタン、LinkButton、または ImageButton コントロールによって開始されたポストバックをキャンセルします。 ただし、ユーザーが時代遅れブラウザーを使用してアクセスしている場合、または JavaScript のサポートが無効になっている場合は、クライアント側の検証チェックは実行されません。

すべての ASP.NET 検証コントロールは、ポストバックの直後に検証ロジックを繰り返し、 [`Page.IsValid` プロパティ](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)を使用してページの入力の全体的な有効性を報告します。 ただし、`Page.IsValid`の値に基づいて、ページフローが中断または停止されることはありません。 開発者は、有効な入力データを想定したコードに進む前に、`Page.IsValid` プロパティの値が `True` であることを確認する必要があります。

ユーザーが JavaScript を無効にしている場合は、ページにアクセスして、製品を編集し、価格の値を大きくしてから、[更新] ボタンをクリックすると、クライアント側の検証がバイパスされ、ポストバックが議論されます。 ポストバック時に、ASP.NET ページ s `UpdateCommand` イベントハンドラーが実行され、`Decimal`に対して負荷が高すぎると、例外が発生します。 例外処理があるため、このような例外は適切に処理されますが、最初の場所で無効なデータが処理されるのを防ぐことができるのは、`Page.IsValid` の値が `True`の場合に `UpdateCommand` イベントハンドラーを続行することだけです。

`UpdateCommand` イベントハンドラーの先頭に、`Try` ブロックの直前に次のコードを追加します。

[!code-vb[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample2.vb)]

この追加により、送信されたデータが有効である場合にのみ、製品が更新されるようになります。 ほとんどのユーザーは、検証コントロールのクライアント側スクリプトによって無効なデータをポストバックすることはできませんが、ブラウザーが JavaScript をサポートしていないユーザーまたは JavaScript のサポートが無効になっているユーザーは、クライアント側のチェックをバイパスして、無効なデータを送信できます。

> [!NOTE]
> ずる賢い reader は、GridView を使用してデータを更新するときに、ページの分離コードクラスの `Page.IsValid` プロパティを明示的に確認する必要がないことを思い出しています。 これは、GridView が `Page.IsValid` プロパティを調べ、`True`の値を返す場合にのみ更新のみを処理するためです。

## <a name="step-3-summarizing-data-entry-problems"></a>手順 3: データ入力の問題の概要

5つの検証コントロールに加えて、ASP.NET には[Validationsummary コントロール](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)が含まれています。このコントロールには、無効なデータを検出した検証コントロールの `ErrorMessage` が表示されます。 この概要データは、web ページ上のテキストとして、またはモーダルのクライアント側のメッセージボックスを使用して表示できます。 このチュートリアルを強化し、検証の問題を要約したクライアント側のメッセージボックスを含めるようにしてみましょう。

これを実現するには、[ツールボックス] から [ValidationSummary] コントロールをデザイナーにドラッグします。 ValidationSummary コントロールの場所は、メッセージボックスとして概要のみを表示するように構成するため、実際には問題になりません。 コントロールを追加した後、その[`ShowSummary` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)を `False` に設定し、その[`ShowMessageBox` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)を `True`に設定します。 この追加により、クライアント側のメッセージボックスに検証エラーが集約されます (図6を参照)。

[検証エラーがクライアント側のメッセージボックスにまとめられている ![](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image16.png)

**図 6**: 検証エラーがクライアント側のメッセージボックスにまとめられている ([クリックしてフルサイズのイメージを表示する](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image18.png))

## <a name="summary"></a>要約

このチュートリアルでは、検証コントロールを使用して、ユーザーの入力が有効であることを事前に確認してから、更新ワークフローでの使用を試行する方法について説明しました。 ASP.NET には、特定の Web コントロールの入力を検査し、入力の有効性を報告するように設計された5つの検証 Web コントロールが用意されています。 このチュートリアルでは、RequiredFieldValidator と CompareValidator の2つのコントロールを使用して、製品名が指定されていること、および価格の値が0以上の通貨形式であることを確認しました。

DataList の編集インターフェイスに検証コントロールを追加するのは、ツールボックスから `EditItemTemplate` にドラッグし、いくつかのプロパティを設定するだけです。 既定では、検証コントロールはクライアント側の検証スクリプトを自動的に生成します。また、ポストバック時にサーバー側の検証も行い、累積結果を `Page.IsValid` プロパティに格納します。 ボタン、LinkButton、または ImageButton がクリックされたときにクライアント側の検証をバイパスするには、[`CausesValidation`] プロパティを `False`に設定します。 また、ポストバック時に送信されたデータを使用してタスクを実行する前に、`Page.IsValid` プロパティが `True`を返していることを確認してください。

これまでに説明したすべての DataList 編集チュートリアルでは、製品名のテキストボックスと価格について、非常に単純な編集インターフェイスが用意されています。 ただし、編集インターフェイスには、DropDownLists、カレンダー、Radiobutton、Checkbox など、さまざまな Web コントロールを混在させることができます。 次のチュートリアルでは、さまざまな Web コントロールを使用するインターフェイスの構築について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Patterson が、Ken PLiz Isa、および Shulok でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](handling-bll-and-dal-level-exceptions-vb.md)
> [次へ](customizing-the-datalist-s-editing-interface-vb.md)
