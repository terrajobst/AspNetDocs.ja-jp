---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
title: オプションボタンの GridView 列を追加するC#() |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、オプションボタンの列を GridView コントロールに追加する方法を説明します。これにより、ユーザーは、次のような1つの行をより直観的に選択できます。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 32377145-ec25-4715-8370-a1c590a331d5
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
msc.type: authoredcontent
ms.openlocfilehash: b59cc64b14c6414e6558fdb8a281644db8386701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78477952"
---
# <a name="adding-a-gridview-column-of-radio-buttons-c"></a>ラジオ ボタンの GridView 列を追加する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_CS.exe)または[PDF のダウンロード](adding-a-gridview-column-of-radio-buttons-cs/_static/datatutorial51cs1.pdf)

> このチュートリアルでは、gridview コントロールにオプションボタンの列を追加して、ユーザーが GridView の単一の行をより直観的に選択できるようにする方法について説明します。

## <a name="introduction"></a>はじめに

GridView コントロールには、多くの組み込み機能が用意されています。 これには、テキスト、画像、ハイパーリンク、およびボタンを表示するためのさまざまなフィールドが含まれています。 詳細なカスタマイズのためのテンプレートをサポートしています。 マウスを数回クリックするだけで、ボタンを使用して各行を選択できる GridView を作成したり、編集または削除機能を有効にしたりできます。 多くの機能が用意されていますが、サポートされていない機能を追加する必要がある場合もあります。 このチュートリアルと次の2つのチュートリアルでは、追加の機能を含めるように GridView の機能を拡張する方法について説明します。

このチュートリアルと次の1つは、行選択プロセスの拡張に関するものです。 [詳細詳細ビューで選択可能なマスター GridView を使用してマスター/詳細](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)で確認したように、Select ボタンを含む Gridview に commandfield を追加できます。 クリックすると、ポストバック ensues と GridView s `SelectedIndex` プロパティが、Select ボタンがクリックされた行のインデックスに更新されます。 [詳細詳細ビューのチュートリアルで選択可能なマスター GridView を使用したマスター/詳細](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)では、この機能を使用して、選択した gridview 行の詳細を表示する方法を説明しました。

[選択] ボタンは多くの状況で動作しますが、他のユーザーに対しても機能しない場合があります。 ボタンを使用する代わりに、オプションボタンとチェックボックスの2つのユーザーインターフェイス要素を選択することがよくあります。 GridView を拡張して、Select ボタンの代わりに、各行にラジオボタンまたはチェックボックスを含めることができます。 ユーザーが GridView レコードの1つしか選択できない場合、[選択] ボタンよりもオプションボタンが優先されることがあります。 ユーザーが web ベースの電子メールアプリケーションなどで複数のレコードを選択できる場合、ユーザーは複数のメッセージを選択して、選択ボタンまたはラジオボタンでは使用できない機能を提供する場合があります。ユーザーインターフェイス。

このチュートリアルでは、オプションボタンの列を GridView に追加する方法について説明します。 このチュートリアルでは、チェックボックスの使用について説明します。

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>手順 1: GridView Web ページの拡張の作成

GridView を拡張してラジオボタンの列を追加する前に、まず、このチュートリアルで必要な ASP.NET ページを web サイトプロジェクトに作成し、次の2つのページを作成してみましょう。 まず、`EnhancedGridView`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`

![SqlDataSource 関連のチュートリアルの ASP.NET ページを追加する](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.gif)

**図 1**: SqlDataSource 関連のチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`EnhancedGridView` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 したがって、ソリューションエクスプローラーからページデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.png)

**図 2**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.png)されます)

最後に、これらの4つのページをエントリとして `Web.sitemap` ファイルに追加します。 具体的には、SqlDataSource コントロール `<siteMapNode>`を使用して、の後に次のマークアップを追加します。

[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、チュートリアルの編集、挿入、および削除を行うための項目が含まれています。

![サイトマップに、GridView チュートリアルを強化するためのエントリが含まれるようになりました。](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.gif)

**図 3**: サイトマップに GridView チュートリアルを強化するためのエントリが含まれるようになりました。

## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>手順 2: GridView での仕入先の表示

このチュートリアルでは、を使用して、USA の仕入先を一覧表示する GridView を作成します。各 GridView 行にはオプションボタンが用意されています。 オプションボタンを使用して仕入先を選択すると、ユーザーはボタンをクリックして仕入先の製品を表示できます。 このタスクは自明であると思われますが、特に注意が必要な微妙なことがいくつかあります。 これらの微妙な点について詳しく説明する前に、まず、サプライヤーを一覧表示する GridView を取得してみましょう。

まず、[ツールボックス] から GridView をデザイナーにドラッグして、`EnhancedGridView` フォルダー内の `RadioButtonField.aspx` のページを開きます。 GridView の `ID` を `Suppliers` に設定し、そのスマートタグから新しいデータソースの作成を選択します。 具体的には、`SuppliersBLL` オブジェクトからデータをプルする `SuppliersDataSource` という名前の ObjectDataSource を作成します。

[SuppliersDataSource という名前の新しい ObjectDataSource を作成 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.png)

**図 4**: `SuppliersDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.png)される)

[SuppliersBLL クラスを使用するように ObjectDataSource を構成 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.png)

**図 5**: `SuppliersBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.png))

ここでは、米国の業者を一覧表示するだけなので、[選択] タブのドロップダウンリストから `GetSuppliersByCountry(country)` 方法を選択します。

[SuppliersBLL クラスを使用するように ObjectDataSource を構成 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.png)

**図 6**: `SuppliersBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.png))

[更新] タブで [(なし)] オプションを選択し、[次へ] をクリックします。

[SuppliersBLL クラスを使用するように ObjectDataSource を構成 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.png)

**図 7**: `SuppliersBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.png))

`GetSuppliersByCountry(country)` メソッドはパラメーターを受け取るため、データソースの構成ウィザードでは、そのパラメーターのソースの入力を求められます。 ハードコーディングされた値 (この例では USA) を指定するには、[パラメーターのソース] ドロップダウンリストを [なし] のままにして、テキストボックスに既定値を入力します。 [完了] をクリックしてウィザードを終了します。

[country パラメーターの既定値として USA を使用 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.png)

**図 8**: `country` パラメーターの既定値として USA を使用[する (クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.png))

ウィザードを完了すると、GridView には、各仕入先データフィールドの BoundField が含まれます。 `CompanyName`、`City`、および `Country` BoundFields 以外のすべてを削除し、`CompanyName` BoundFields `HeaderText` プロパティの名前を Supplier に変更します。 その後、GridView と ObjectDataSource の宣言構文は次のようになります。

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample2.aspx)]

このチュートリアルでは、を使用して、ユーザーが仕入先リストと同じページまたは別のページで選択した仕入先製品を表示できるようにします。 これに対応するには、2つのボタン Web コントロールをページに追加します。 ここでは、これら2つのボタンの `ID` を `ListProducts` と `SendToProducts`に設定しました。 `ListProducts` をクリックすると、ポストバックが発生し、選択した仕入先の製品は同じページに表示されますが、`SendToProducts` がクリックされると、ユーザーは製品を一覧表示する別のページに whisked されます。

図9に、ブラウザーで表示したときの `Suppliers` GridView と2つのボタンの Web コントロールを示します。

[米国の仕入先 ![、名前、市区町村、および国の情報が記載されています。](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.png)

**図 9**: 米国の仕入先は、名前、市区町村、および国の情報を一覧表示します ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.png)されます)

## <a name="step-3-adding-a-column-of-radio-buttons"></a>手順 3: ラジオボタンの列の追加

この時点で、`Suppliers` GridView には、米国の各業者の会社名、市区町村、および国を表示する、3つの連結されたフィールドがあります。 ただし、ラジオボタンの列はまだありません。 残念ながら、GridView には組み込みの RadioButtonField が含まれていません。それ以外の場合は、グリッドに追加するだけで完了です。 代わりに、TemplateField を追加し、オプションボタンを表示するように `ItemTemplate` を構成して、各 GridView 行に対してオプションボタンが表示されるようにすることができます。

最初は、TemplateField の `ItemTemplate` に RadioButton Web コントロールを追加することによって、目的のユーザーインターフェイスを実装できると想定することがあります。 これにより、GridView の各行に1つのオプションボタンが追加されますが、オプションボタンはグループ化できないため、相互に排他的ではありません。 つまり、エンドユーザーは、GridView から複数のオプションボタンを同時に選択できます。

RadioButton Web コントロールの TemplateField を使用しても必要な機能が提供されない場合でも、では、この方法を実装します。これは、結果として得られるオプションボタンがグループ化されていない理由を調べるのに役立ちます。 まず、TemplateField を [仕入先] GridView に追加して、左端のフィールドにします。 次に、GridView s スマートタグから、[テンプレートの編集] リンクをクリックし、RadioButton Web コントロールをツールボックスから TemplateField s `ItemTemplate` にドラッグします (図10を参照)。 RadioButton s `ID` プロパティを `RowSelector` に設定し、`GroupName` プロパティを `SuppliersGroup`に設定します。

[ItemTemplate に RadioButton Web コントロールを追加 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.png)

**図 10**: `ItemTemplate` に RadioButton Web コントロールを追加する ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.png)されます)

デザイナーを使用してこれらを追加すると、GridView のマークアップは次のようになります。

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample3.aspx)]

RadioButton s [`GroupName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx)は、一連のオプションボタンをグループ化するために使用されるものです。 同じ `GroupName` 値を持つ RadioButton コントロールはすべてグループ化されていると見なされます。グループから選択できるラジオボタンは一度に1つだけです。 `GroupName` プロパティは、表示されるオプションボタン s `name` 属性の値を指定します。 ブラウザーは、オプションボタンの `name` 属性を調べて、オプションボタンのグループを決定します。

`ItemTemplate`に RadioButton Web コントロールを追加した状態で、ブラウザーを使用してこのページにアクセスし、grid s 行のオプションボタンをクリックします。 オプションボタンがグループ化されていないことに注意してください。図11に示すように、すべての行を選択することができます。

[GridView s オプションボタンがグループ化されていない ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.png)

**図 11**: GridView のオプションボタンがグループ化されていない ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.png))

オプションボタンがグループ化されていない理由は、同じ `GroupName` プロパティの設定があるにもかかわらず、表示される `name` 属性が異なるためです。 これらの違いを確認するには、ブラウザーからビュー/ソースを実行し、ラジオボタンのマークアップを確認します。

[!code-html[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample4.html)]

`name` 属性と `id` 属性の両方が、プロパティウィンドウで指定されている正確な値ではなく、他の `ID` 値の前に付加されていることに注意してください。 表示される `id` と `name` 属性の前に追加の `ID` 値 `ID` が追加されています。親は、`GridViewRow` s、GridView の `ID`、コンテンツコントロール s `ID`、および Web フォーム s `ID`を制御します。`ID` これらの `ID` は、GridView でレンダリングされる各 Web コントロールに一意の `id` と `name` 値があるように追加されます。

レンダリングされた各コントロールは、クライアント側の各コントロールを一意に識別する方法と、ポストバック時にどのように動作または変更が発生したかを web サーバーに識別する方法に応じて、異なる `name` と `id` を必要とします。 たとえば、RadioButton s checked 状態が変更されたときに、一部のサーバー側コードを実行したいとします。 これを実現するには、RadioButton s `AutoPostBack` プロパティを `true` に設定し、`CheckChanged` イベントのイベントハンドラーを作成します。 ただし、すべてのオプションボタンの表示された `name` と `id` の値が同じである場合、ポストバック時に、どの特定の RadioButton がクリックされたかを判断できませんでした。

そのうち、RadioButton で RadioButton Web コントロールを使用してオプションボタンの列を作成できないということです。 代わりに、各 GridView 行に適切なマークアップが挿入されるように、むしろデプロイシステム手法を使用する必要があります。

> [!NOTE]
> RadioButton Web コントロールと同様に、オプションボタンの HTML コントロールは、テンプレートに追加されると、一意の `name` 属性を含むようになり、グリッド内のオプションボタンはグループ化されません。 Html コントロールに慣れていない場合は、HTML コントロールがあまり使用されない (特に ASP.NET 2.0 では) ため、この点についてはおわかりにならないようにしてください。 詳細については、「 [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx) s のブログエントリ[WEB コントロールと HTML コントロール](http://www.odetocode.com/Articles/348.aspx)」を参照してください。

## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>Literal コントロールを使用してオプションボタンのマークアップを挿入する

GridView 内のすべてのオプションボタンを正しくグループ化するには、オプションボタンのマークアップを `ItemTemplate`に手動で挿入する必要があります。 各オプションボタンは、同じ `name` 属性を必要としますが、一意の `id` 属性を持つ必要があります (クライアント側スクリプトを使用してラジオボタンにアクセスする場合)。 ユーザーがラジオボタンを選択してページをポストバックすると、選択したオプションボタン s `value` 属性の値がブラウザーから返送されます。 したがって、各オプションボタンには、一意の `value` 属性が必要です。 最後に、ポストバック時に、選択されているオプションボタンに `checked` 属性を追加する必要があります。そうしないと、ユーザーが選択とポストバックを行った後、オプションボタンが既定の状態に戻ります (すべて選択解除されています)。

低レベルのマークアップをテンプレートに挿入するには、2つの方法があります。 1つは、マークアップと呼び出しを組み合わせて、分離コードクラスで定義された書式指定メソッドを呼び出すことです。 この手法については、 [GridView コントロールのチュートリアルの「Templatetemplatefields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 」で最初に説明しました。 この例では、次のようになります。

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample5.aspx)]

ここでは、`GetUniqueRadioButton` と `GetRadioButtonValue` は、各オプションボタンの適切な `id` および `value` 属性値を返す分離コードクラスで定義されたメソッドです。 この方法は、`id` 属性と `value` 属性を割り当てる場合に適していますが、データが最初に GridView にバインドされたときにのみデータバインド構文が実行されるため、`checked` 属性値を指定する必要がある場合は短すぎます。 したがって、GridView でビューステートが有効になっている場合は、ページが最初に読み込まれたとき (または GridView がデータソースに明示的に再バインドされたとき) にのみ、書式設定メソッドが起動されます。したがって、`checked` 属性を設定する関数はポストバック時に呼び出されません。 これは少し問題があり、この記事の範囲を超えているので、そのままにしておきます。 ただし、上記の方法を使用して、行き詰まってくるポイントまで処理することをお勧めします。 このような演習では、作業バージョンについては詳しく説明しませんが、GridView とデータバインドのライフサイクルをより深く理解するのに役立ちます。

テンプレートにカスタムの低レベルのマークアップを挿入するもう1つの方法と、このチュートリアルで使用する方法は、テンプレートに[リテラルコントロール](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx)を追加することです。 次に、GridView s `RowCreated` または `RowDataBound` イベントハンドラーで、リテラルコントロールにプログラムでアクセスし、その `Text` プロパティを出力するマークアップに設定します。

まず、TemplateField s `ItemTemplate`から RadioButton を削除し、Literal コントロールに置き換えます。 リテラルコントロール s `ID` を `RadioButtonMarkup`に設定します。

[リテラルコントロールを ItemTemplate に追加 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.png)

**図 12**: `ItemTemplate` にリテラルコントロールを追加する ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.png)されます)

次に、GridView s `RowCreated` イベントのイベントハンドラーを作成します。 `RowCreated` イベントは、データが GridView に再バインドされているかどうかにかかわらず、追加されたすべての行に対して1回発生します。 つまり、データがビューステートから再読み込みされた場合でも、ポストバック時には `RowCreated` イベントが発生します。これは、`RowDataBound` (データがデータ Web コントロールに明示的にバインドされている場合にのみ発生する) ではなく、このイベントが使用されるためです。

このイベントハンドラーでは、データ行を処理している場合にのみ続行します。 データ行ごとに、プログラムを使用して `RadioButtonMarkup` リテラルコントロールを参照し、その `Text` プロパティを、出力するマークアップに設定します。 次のコードに示すように、出力されたマークアップは、`name` 属性が `SuppliersGroup`に設定されているオプションボタンを作成します。このボタンには、`id` 属性が `RowSelectorX`に設定されています。ここで、 *X*は gridview 行のインデックスで、`value` 属性は gridview 行のインデックスに設定されています。

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample6.cs)]

GridView 行が選択され、ポストバックが発生すると、選択した業者の `SupplierID` に関心があります。 したがって、各オプションボタンの値は、GridView 行のインデックスではなく、実際の `SupplierID` であると考えることができます。 これは特定の状況で動作する場合がありますが、`SupplierID`を無条件で受け入れて処理することによって、セキュリティ上のリスクが生じる可能性があります。 たとえば、GridView では、米国の仕入先のみが一覧表示されます。 ただし、`SupplierID` がオプションボタンから直接渡された場合、mischievous ユーザーがポストバック時に返された `SupplierID` 値を操作できないようにするにはどうすればよいでしょうか。 行インデックスを `value`として使用し、`DataKeys` コレクションからポストバックで `SupplierID` を取得することにより、ユーザーがいずれかの GridView 行に関連付けられている `SupplierID` 値の1つのみを使用していることを確認できます。

このイベントハンドラーコードを追加した後、ブラウザーでページをテストするために1分かかります。 まず、グリッド内のラジオボタンは一度に1つしか選択できないことに注意してください。 ただし、ラジオボタンを選択し、いずれかのボタンをクリックすると、ポストバックが発生し、ラジオボタンがすべて初期状態に戻ります (つまり、ポストバック時に、選択したオプションボタンが選択されなくなります)。 この問題を解決するには、ポストバックから送信された選択したオプションボタンのインデックスを調べて、一致する行インデックスの出力マークアップに `checked="checked"` 属性を追加するように、`RowCreated` イベントハンドラーを拡張する必要があります。

ポストバックが発生すると、ブラウザーは、選択したラジオボタンの `name` と `value` を返します。 この値は、`Request.Form["name"]`を使用してプログラムで取得できます。 [`Request.Form` プロパティ](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx)は、フォーム変数を表す[`NameValueCollection`](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx)を提供します。 フォーム変数は、web ページ内のフォームフィールドの名前と値であり、ポストバック ensues が行われるたびに web ブラウザーによって送信されます。 GridView のオプションボタンに表示される `name` 属性は `SuppliersGroup`ので、web ページがポストバックされると、ブラウザーは `SuppliersGroup=valueOfSelectedRadioButton` を web サーバーに送り返します (他のフォームフィールドと共に)。 この情報には、次を使用して `Request.Form` プロパティからアクセスできます: `Request.Form["SuppliersGroup"]`。

選択したオプションボタンのインデックスは `RowCreated` イベントハンドラーだけでなく、ボタン Web コントロールの `Click` イベントハンドラーでも決定する必要があるため、では、オプションボタンが選択されていない場合は `-1` を返すコードビハインドクラスに `SuppliersSelectedIndex` プロパティを追加し、オプションボタンのいずれかを選択した場合は選択したインデックスを追加します。

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample7.cs)]

このプロパティを追加すると、`SuppliersSelectedIndex` が `e.Row.RowIndex`に等しい場合に、`RowCreated` イベントハンドラーに `checked="checked"` マークアップを追加することがわかっています。 このロジックを含めるようにイベントハンドラーを更新します。

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample8.cs)]

この変更により、ポストバック後も選択したオプションボタンが選択されたままになります。 選択されているラジオボタンを指定できるようになったので、動作を変更して、ページが最初にアクセスされたときに、既定ではオプションボタンが選択されていません。動作)。 最初のオプションボタンが既定で選択されるようにするには、単に `if (SuppliersSelectedIndex == e.Row.RowIndex)` ステートメントを次のように変更します。 `if (SuppliersSelectedIndex == e.Row.RowIndex || (!Page.IsPostBack && e.Row.RowIndex == 0))`。

この時点で、1つの GridView 行を選択し、ポストバック間で記憶できるようにするための、グループ化されたオプションボタンの列を GridView に追加しました。 次の手順では、選択した業者によって提供される製品を表示します。 手順4では、ユーザーを別のページにリダイレクトし、選択した `SupplierID`に従って送信する方法について説明します。 手順5では、選択した仕入先の製品を同じページの GridView に表示する方法について説明します。

> [!NOTE]
> TemplateField (この長い手順3の焦点) を使用するのではなく、適切なユーザーインターフェイスと機能をレンダリングするカスタム `DataControlField` クラスを作成することができます。 [`DataControlField` クラス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx)は、BoundField、CheckBoxField、TemplateField、およびその他の組み込み GridView および DetailsView フィールドが派生する基本クラスです。 カスタム `DataControlField` クラスを作成すると、オプションボタンの列が宣言型の構文を使用してのみ追加され、他の web ページや他の web アプリケーションにも機能を簡単にレプリケートできるようになります。

ただし、ASP.NET でカスタムのコンパイル済みコントロールを作成したことがある場合は、それを行うにはかなりの量の業務が必要であり、慎重に処理する必要がある微妙なものとエッジケースをホストしていることがわかっています。 そのため、ここでは、オプションボタンの列をカスタム `DataControlField` クラスとして実装し、TemplateField オプションを済ませるします。 今後のチュートリアルでは、カスタム `DataControlField` クラスの作成、使用、デプロイについて確認できる可能性があります。

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>手順 4: 選択した仕入先製品を別のページに表示する

ユーザーが GridView 行を選択したら、選択した仕入先製品を表示する必要があります。 状況によっては、これらの製品を別のページに表示することが必要になる場合があります。他の場合は、同じページで行うことをお勧めします。 まず、製品を別のページに表示する方法を見てみましょう。手順5では、選択した仕入先の製品を表示するために `RadioButtonField.aspx` に GridView を追加する方法について説明します。

現在、ページ `ListProducts` と `SendToProducts`の2つのボタン Web コントロールがあります。 `SendToProducts` ボタンをクリックすると、ユーザーを `~/Filtering/ProductsForSupplierDetails.aspx`に送信します。 このページは、「 [2 ページでのマスター/詳細のフィルター処理](../masterdetail/master-detail-filtering-across-two-pages-cs.md)」チュートリアルで作成され、`SupplierID`という名前のクエリ文字列フィールドを通じて `SupplierID` が渡される業者の製品を表示します。

この機能を提供するには、`SendToProducts` Button s `Click` イベントのイベントハンドラーを作成します。 手順3では、`SuppliersSelectedIndex` プロパティを追加しました。このプロパティは、オプションボタンが選択されている行のインデックスを返します。 対応する `SupplierID` を GridView の `DataKeys` コレクションから取得できます。ユーザーは `Response.Redirect("url")`を使用して `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` に送信できます。

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample9.cs)]

このコードは、オプションボタンの1つが GridView から選択されている限り、てで動作します。 初期状態では、GridView にオプションボタンが選択されておらず、ユーザーが [`SendToProducts`] ボタンをクリックした場合、`SuppliersSelectedIndex` は `-1`されます。これにより、`-1` は `DataKeys` コレクションのインデックス範囲を超えているため、例外がスローされます。 ただし、手順 3. で説明したように `RowCreated` イベントハンドラーを更新することにした場合は、GridView の最初のオプションボタンが最初に選択されます。

`-1`の `SuppliersSelectedIndex` 値に対応するには、GridView の上のページにラベル Web コントロールを追加します。 `ID` プロパティを `ChooseSupplierMsg`に、その `CssClass` プロパティを `Warning`に、`EnableViewState` プロパティと `Visible` プロパティを `false`に設定し、その `Text` プロパティをグリッドから業者を選択します。 CSS クラス `Warning` は、赤、斜体、太字、大きいフォントでテキストを表示し、`Styles.css`で定義されます。 `EnableViewState` および `Visible` プロパティを `false`に設定すると、コントロール s `Visible` プロパティがプログラムによって `true`に設定されているポストバックだけを除き、ラベルはレンダリングされません。

[GridView の上にラベル Web コントロールを追加 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image21.png)

**図 13**: GridView の上にラベル Web コントロールを追加[する (クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image22.png)されます)

次に、`SuppliersSelectedIndex` が0未満の場合に `ChooseSupplierMsg` ラベルを表示するように `Click` イベントハンドラーを拡張し、それ以外の場合はユーザーを `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` にリダイレクトします。

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample10.cs)]

ブラウザーでページにアクセスし、GridView から業者を選択する前に [`SendToProducts`] ボタンをクリックします。 図14に示すように、`ChooseSupplierMsg` ラベルが表示されます。 次に、業者を選択し、[`SendToProducts`] ボタンをクリックします。 これにより、選択した業者によって提供される製品が一覧表示されたページに whisk ます。 図15は、Bigfoot Breweries supplier が選択されたときの `ProductsForSupplierDetails.aspx` ページを示しています。

[ChooseSupplierMsg ラベルは、業者が選択されていない場合に表示され ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image23.png)

**図 14**: 業者が選択されていない場合に `ChooseSupplierMsg` ラベルが表示される ([クリックしてフルサイズの画像を表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image24.png))

[選択した仕入先の製品 ![ProductsForSupplierDetails に表示されます。](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image25.png)

**図 15**: 選択した仕入先の製品が `ProductsForSupplierDetails.aspx` に表示される ([クリックしてフルサイズの画像を表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image26.png))

## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>手順 5: 選択した仕入先の製品を同じページに表示する

手順4では、ユーザーを別の web ページに送信して、選択した仕入先製品を表示する方法を説明しました。 または、選択した仕入先の製品を同じページに表示することもできます。 これを説明するために、`RadioButtonField.aspx` に別の GridView を追加して、選択した仕入先製品を表示します。

この GridView の製品は、業者を選択した後にのみ表示されるようにするため、`Suppliers` GridView の下に Panel Web コントロールを追加し、その `ID` を `ProductsBySupplierPanel` に設定し、その `Visible` プロパティを `false`に設定します。 パネル内で、選択した業者のテキスト製品を追加し、その後に `ProductsBySupplier`という名前の GridView を追加します。 GridView s スマートタグから、`ProductsBySupplierDataSource`という名前の新しい ObjectDataSource にバインドすることを選択します。

[製品 Bysupplier GridView を新しい ObjectDataSource にバインド ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image27.png)

**図 16**: `ProductsBySupplier` GridView を新しい ObjectDataSource にバインドする ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image28.png)されます)

次に、`ProductsBLL` クラスを使用するように ObjectDataSource を構成します。 選択した業者によって提供される製品のみを取得する必要があるため、ObjectDataSource が `GetProductsBySupplierID(supplierID)` メソッドを呼び出してそのデータを取得するように指定します。 [更新]、[挿入]、[削除] の各タブのドロップダウンリストから [(なし)] を選択します。

[Get$ By仕入先 (仕入先) メソッドを使用するように ObjectDataSource を構成 ![には](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image29.png)

**図 17**: `GetProductsBySupplierID(supplierID)` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image30.png))

[[更新]、[挿入]、[削除] の各タブで、ドロップダウンリストを [(なし)] に設定 ![ます。](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image31.png)

**図 18**: 更新、挿入、および削除の各タブでドロップダウンリストを (なし) に設定する ([クリックしてフルサイズの画像を表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image32.png))

[選択]、[更新]、[挿入]、[削除] の各タブを構成したら、[次へ] をクリックします。 `GetProductsBySupplierID(supplierID)` メソッドには入力パラメーターが必要であるため、データソースの作成ウィザードでは、パラメーター s の値のソースを指定するように求められます。

ここでは、パラメーター s 値のソースを指定するためのオプションがいくつかあります。 既定のパラメーターオブジェクトを使用して、`SuppliersSelectedIndex` プロパティの値を ObjectDataSource s `Selecting` イベントハンドラーのパラメーター s `DefaultValue` プロパティにプログラムで割り当てることができます。 プログラムから ObjectDataSource のパラメーターに値を割り当てる方法については、「 [objectdatasource のパラメーター値をプログラムによって設定](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)する」を参照してください。

または、ControlParameter を使用して、`Suppliers` GridView s [`SelectedValue` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx)を参照することもできます (図19を参照)。 GridView s `SelectedValue` プロパティは、 [`SelectedIndex` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)に対応する `DataKey` 値を返します。 このオプションを機能させるには、[`ListProducts`] ボタンをクリックしたときに、GridView の `SelectedIndex` プロパティを選択した行にプログラムで設定する必要があります。 追加の利点として、`SelectedIndex`を設定することにより、選択したレコードは `DataWebControls` テーマで定義されている `SelectedRowStyle` で実行されます (黄色の背景)。

[![ControlParameter を使用して、GridView の SelectedValue をパラメーターソースとして指定します。](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image33.png)

**図 19**: controlparameter を使用して GridView s SelectedValue をパラメーターソースとして指定する ([クリックしてフルサイズのイメージを表示する](adding-a-gridview-column-of-radio-buttons-cs/_static/image34.png))

ウィザードを完了すると、Visual Studio によって product のデータフィールドのフィールドが自動的に追加されます。 `ProductName`、`CategoryName`、および `UnitPrice` BoundFields 以外のすべてを削除し、`HeaderText` プロパティを製品、カテゴリ、および価格に変更します。 値が通貨として書式設定されるように、`UnitPrice` BoundField を構成します。 これらの変更を行った後、パネル、GridView、および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample11.aspx)]

この演習を完了するには、[GridView s `SelectedIndex`] プロパティを `SelectedSuppliersIndex` に設定し、[`ProductsBySupplierPanel` Panel s `Visible`] プロパティを [`true`] ボタンがクリックされたときに `ListProducts` に設定する必要があります。 これを行うには、[`ListProducts`] ボタン Web コントロール s `Click` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample12.cs)]

GridView からサプライヤーが選択されていない場合は、`ChooseSupplierMsg` ラベルが表示され、`ProductsBySupplierPanel` パネルは非表示になります。 それ以外の場合、業者が選択されると、`ProductsBySupplierPanel` が表示され、GridView s `SelectedIndex` プロパティが更新されます。

図20は、Bigfoot Breweries supplier が選択され、[ページに製品を表示] ボタンがクリックされた後の結果を示しています。

[Bigfoot Breweries によって提供される製品が同じページに表示される ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image35.png)

**図 20**: Bigfoot Breweries によって提供される製品は同じページに一覧表示されます ([クリックすると、フルサイズの画像が表示](adding-a-gridview-column-of-radio-buttons-cs/_static/image36.png)されます)

## <a name="summary"></a>まとめ

[詳細詳細ビューのチュートリアルで選択可能なマスター GridView を使用してマスター/詳細](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)に説明したように、`ShowSelectButton` プロパティが `true`に設定されている commandfield を使用して GridView からレコードを選択できます。 ただし、CommandField には、通常のプッシュボタン、リンク、または画像としてボタンが表示されます。 その他の行選択ユーザーインターフェイスは、各 GridView 行にオプションボタンまたはチェックボックスを提供することです。 このチュートリアルでは、ラジオボタンの列を追加する方法について説明します。

残念ながら、ラジオボタンの列を追加するのは、1つの場合と同じほど簡単ではありません。 ボタンをクリックして追加できる組み込みの RadioButtonField はありません。 TemplateField 内で RadioButton Web コントロールを使用すると、独自の問題のセットが導入されます。 最後に、このようなインターフェイスを提供するには、カスタム `DataControlField` クラスを作成するか、`RowCreated` イベント中に適切な HTML を TemplateField に挿入する方法を使用する必要があります。

ラジオボタンの列を追加する方法を説明したので、チェックボックスの列を追加することに注意してください。 ユーザーは、チェックボックスの列を使用して1つ以上の GridView 行を選択し、選択したすべての行に対して何らかの操作を実行できます (たとえば、web ベースの電子メールクライアントから電子メールのセットを選択し、選択したすべての電子メールを削除するように選択します)。 次のチュートリアルでは、このような列を追加する方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は David, u です。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](adding-a-gridview-column-of-checkboxes-cs.md)
