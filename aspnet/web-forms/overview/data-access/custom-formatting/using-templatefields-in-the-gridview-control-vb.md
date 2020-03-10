---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-vb
title: GridView コントロールで TemplateFields を使用する (VB) |Microsoft Docs
author: rick-anderson
description: 柔軟性を提供するために、GridView には、テンプレートを使用してレンダリングする TemplateField が用意されています。 テンプレートには、静的な HTML、Web コントロール、および...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: a92cd6ed-609a-4e40-ad23-004b54afd436
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 3c090dbf65d9acbcc0e343cda5e8da7fff2d35d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78426850"
---
# <a name="using-templatefields-in-the-gridview-control-vb"></a>GridView コントロールで TemplateFields を使用する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_12_VB.exe)または[PDF のダウンロード](using-templatefields-in-the-gridview-control-vb/_static/datatutorial12vb1.pdf)

> 柔軟性を提供するために、GridView には、テンプレートを使用してレンダリングする TemplateField が用意されています。 テンプレートには、静的な HTML、Web コントロール、およびデータバインディングの構文を混在させることができます。 このチュートリアルでは、TemplateField を使用して、GridView コントロールでより高度なカスタマイズを実現する方法について説明します。

## <a name="introduction"></a>はじめに

GridView は、データの表示方法と共に、表示される出力に含まれる `DataSource` のプロパティを示す一連のフィールドで構成されます。 最も単純なフィールド型は BoundField で、データ値がテキストとして表示されます。 他のフィールドの種類では、代替 HTML 要素を使用してデータが表示されます。 たとえば、CheckBoxField は、指定されたデータフィールドの値に応じてチェックされた状態を持つチェックボックスとしてレンダリングされます。ImageField は、指定されたデータフィールドに基づいてイメージソースがあるイメージをレンダリングします。 基になるデータフィールド値に依存する状態を持つハイパーリンクおよびボタンは、hyperlink Field および ButtonField フィールド型を使用して表示できます。

CheckBoxField、ImageField、ハイパーリンクフィールド、および ButtonField の各フィールド型では、データの代替ビューを使用できますが、書式設定に関してかなり制限されています。 CheckBoxField は1つのチェックボックスのみを表示できますが、ImageField で表示できるのは1つのイメージだけです。 特定のフィールドにテキスト、チェックボックス、画像を表示する必要がある場合、それらはすべて異なるデータフィールド値に基づい*て*いますか。 または、チェックボックス、画像、ハイパーリンク、ボタン以外の Web コントロールを使用してデータを表示する場合はどうすればよいでしょうか。 さらに、BoundField は、表示を1つのデータフィールドに制限します。 1つの GridView 列に複数のデータフィールド値を表示したい場合はどうすればよいでしょうか。

このレベルの柔軟性に対応するために、GridView では、*テンプレート*を使用してレンダリングされる TemplateField が提供されています。 テンプレートには、静的な HTML、Web コントロール、およびデータバインディングの構文を混在させることができます。 さらに、TemplateField にはさまざまな状況でレンダリングをカスタマイズするために使用できるさまざまなテンプレートが用意されています。 たとえば、既定では、行ごとにセルを表示するために `ItemTemplate` が使用されますが、`EditItemTemplate` テンプレートを使用して、データを編集するときにインターフェイスをカスタマイズできます。

このチュートリアルでは、TemplateField を使用して、GridView コントロールでより高度なカスタマイズを実現する方法について説明します。 前の[チュートリアル](custom-formatting-based-upon-data-vb.md)では、`DataBound` および `RowDataBound` のイベントハンドラーを使用して、基になるデータに基づいて書式設定をカスタマイズする方法を説明しました。 基になるデータに基づいて書式設定をカスタマイズするもう1つの方法は、テンプレート内から書式指定メソッドを呼び出すことです。 このチュートリアルでは、この手法についても説明します。

このチュートリアルでは、TemplateFields を使用して、従業員のリストの外観をカスタマイズします。 具体的には、すべての従業員を一覧表示しますが、従業員の姓と名を1つの列に表示し、カレンダーコントロールに入社日を、会社で使用した日数を示す状態列を表示します。

[![3 つの TemplateFields を使用して、表示をカスタマイズします。](using-templatefields-in-the-gridview-control-vb/_static/image2.png)](using-templatefields-in-the-gridview-control-vb/_static/image1.png)

**図 1**: 3 つの Templatefields を使用してディスプレイをカスタマイズする ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image3.png)されます)

## <a name="step-1-binding-the-data-to-the-gridview"></a>手順 1: データを GridView にバインドする

TemplateFields を使用して外観をカスタマイズする必要があるレポートのシナリオでは、最初に BoundFields だけを含む GridView コントロールを作成し、次に新しい TemplateFields を追加するか、既存の BoundFields をに変換します。必要に応じて TemplateFields。 したがって、このチュートリアルを開始するには、デザイナーを使用して GridView をページに追加し、従業員の一覧を返す ObjectDataSource にバインドします。 次の手順では、各 employee フィールドに対して BoundFields を含む GridView を作成します。

[`GridViewTemplateField.aspx`] ページを開き、[ツールボックス] から GridView をデザイナーにドラッグします。 GridView のスマートタグから、`EmployeesBLL` クラスの `GetEmployees()` メソッドを呼び出す新しい ObjectDataSource コントロールを追加します。

[GetEmployees () メソッドを呼び出す新しい ObjectDataSource コントロールを追加 ![には](using-templatefields-in-the-gridview-control-vb/_static/image5.png)](using-templatefields-in-the-gridview-control-vb/_static/image4.png)

**図 2**: `GetEmployees()` メソッドを呼び出す新しい ObjectDataSource コントロールを追加する ([クリックしてフルサイズのイメージを表示する](using-templatefields-in-the-gridview-control-vb/_static/image6.png))

この方法で GridView をバインドすると、`EmployeeID`、`LastName`、`FirstName`、`Title`、`HireDate`、`ReportsTo`、`Country`の各 employee プロパティの BoundField が自動的に追加されます。 このレポートでは、`EmployeeID`、`ReportsTo`、`Country` の各プロパティを表示しないようにします。 これらの BoundFields を削除するには、次の手順を実行します。

- [フィールド] ダイアログボックスを使用して、GridView のスマートタグから [列の編集] リンクをクリックすると、このダイアログボックスが表示されます。 次に、左下の一覧から BoundFields を選択し、赤い X ボタンをクリックして BoundField を削除します。
- ソースビューから手動で GridView の宣言構文を編集し、削除する BoundField の `<asp:BoundField>` 要素を削除します。

`EmployeeID`、`ReportsTo`、および `Country` BoundFields を削除した後、GridView のマークアップは次のようになります。

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample1.aspx)]

ブラウザーで進行状況を確認してください。 この時点で、各従業員のレコードを含むテーブルと4つの列が表示されます。1つは従業員の姓、もう1つは役職、もう1つは入社日を示します。

[![LastName、FirstName、Title、および HireDate の各フィールドが従業員ごとに表示されます。](using-templatefields-in-the-gridview-control-vb/_static/image8.png)](using-templatefields-in-the-gridview-control-vb/_static/image7.png)

**図 3**: 各従業員の `LastName`、`FirstName`、`Title`、および `HireDate` のフィールドが表示される ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image9.png)されます)

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>手順 2: 1 つの列に姓と名を表示する

現在、各従業員の姓と名は、別の列に表示されています。 代わりに、1つの列に結合すると便利な場合があります。 これを実現するには、TemplateField を使用する必要があります。 新しい TemplateField を追加し、必要なマークアップとデータバインド構文を追加してから、`FirstName` と `LastName` の連結フィールドを削除します。または、`FirstName` BoundField を TemplateField に変換し、TemplateField を編集して `LastName` の値を含め、`LastName` BoundField を削除することもできます。

どちらの方法でも同じ結果が得られますが、BoundField の外観と機能を模倣するために、変換によって `ItemTemplate` と `EditItemTemplate` が Web コントロールとデータバインド構文に自動的に追加されるため、可能な場合は、BoundFields を TemplateFields に変換することができます。 その利点は、変換プロセスによって一部の処理が実行されるため、TemplateField を使用して作業を減らす必要があることです。

既存の BoundField を TemplateField に変換するには、GridView のスマートタグから [列の編集] リンクをクリックし、[フィールド] ダイアログボックスを起動します。 左下隅の一覧から変換する BoundField を選択し、右下隅にある [このフィールドを TemplateField に変換する] リンクをクリックします。

[[フィールド] ダイアログボックスから BoundField を TemplateField に変換 ![には](using-templatefields-in-the-gridview-control-vb/_static/image11.png)](using-templatefields-in-the-gridview-control-vb/_static/image10.png)

**図 4**: [フィールド] ダイアログボックスから BoundField を TemplateField に変換する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image12.png)されます)

`FirstName` BoundField を TemplateField に変換します。 この変更の後、デザイナーには perceptive の違いはありません。 これは、BoundField を TemplateField に変換することで、BoundField のルックアンドフィールを維持する TemplateField が作成されるためです。 デザイナーのこの時点では、視覚的な違いはありませんが、この変換プロセスでは、BoundField の宣言構文 `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />`-次の TemplateField 構文に置き換えられています。

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample2.aspx)]

ご覧のように、TemplateField は2つのテンプレートで構成されており、`Text` プロパティが `FirstName` データフィールドの値に設定されている `ItemTemplate` と、`Text` プロパティが `FirstName` データフィールドにも設定されている TextBox コントロールを持つ `EditItemTemplate` です。 Databinding 構文 `<%# Bind("fieldName") %>`-は、 *`fieldName`* データフィールドが、指定された Web コントロールプロパティにバインドされていることを示します。

この TemplateField に `LastName` データフィールドの値を追加するには、`ItemTemplate` に別のラベル Web コントロールを追加し、その `Text` プロパティを `LastName`にバインドする必要があります。 これは、手動またはデザイナーを使用して行うことができます。 手動で行うには、適切な宣言構文を `ItemTemplate`に追加するだけです。

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample3.aspx)]

デザイナーを使用して追加するには、GridView のスマートタグの [テンプレートの編集] リンクをクリックします。 これにより、GridView のテンプレート編集インターフェイスが表示されます。 このインターフェイスのスマートタグは、GridView 内のテンプレートの一覧です。 この時点では TemplateField が1つしかないため、ドロップダウンリストに表示されるテンプレートは、`EmptyDataTemplate` と `PagerTemplate`と共に、`FirstName` TemplateField のテンプレートのみです。 GridView にバインドされたデータに結果がない場合、`EmptyDataTemplate` テンプレートを指定すると、GridView の出力を表示するために使用されます。`PagerTemplate`が指定されている場合は、ページングをサポートする GridView のページングインターフェイスを表示するために使用されます。

[![GridView のテンプレートをデザイナーを使用して編集できます。](using-templatefields-in-the-gridview-control-vb/_static/image14.png)](using-templatefields-in-the-gridview-control-vb/_static/image13.png)

**図 5**: GridView のテンプレートはデザイナーを使用して編集できます ([クリックすると、フルサイズのイメージが表示](using-templatefields-in-the-gridview-control-vb/_static/image15.png)されます)

また、`FirstName` TemplateField に `LastName` を表示するには、ツールボックスから Label コントロールを GridView のテンプレート編集インターフェイスの `FirstName` TemplateField の `ItemTemplate` にドラッグします。

[FirstName TemplateField の ItemTemplate にラベル Web コントロールを追加 ![には](using-templatefields-in-the-gridview-control-vb/_static/image17.png)](using-templatefields-in-the-gridview-control-vb/_static/image16.png)

**図 6**: `FirstName` TemplateField の ItemTemplate にラベル Web コントロールを追加する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image18.png)されます)

この時点で、TemplateField に追加されたラベル Web コントロールの `Text` プロパティは "Label" に設定されています。 このプロパティを変更して、このプロパティが代わりに `LastName` データフィールドの値にバインドされるようにする必要があります。 これを行うには、ラベルコントロールのスマートタグをクリックし、[連結の編集] オプションを選択します。

[ラベルのスマートタグから [連結の編集] オプションを選択 ![](using-templatefields-in-the-gridview-control-vb/_static/image20.png)](using-templatefields-in-the-gridview-control-vb/_static/image19.png)

**図 7**: ラベルのスマートタグから [連結の編集] オプションを選択[する (クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image21.png)されます)

[連結] ダイアログボックスが表示されます。 ここでは、左側の一覧からデータバインドに参加するプロパティを選択し、右側のドロップダウンリストからデータをバインドするフィールドを選択できます。 左側の [`Text`] プロパティを選択し、右側の [`LastName`] フィールドをクリックして、[OK] をクリックします。

[テキストプロパティを LastName データフィールドにバインド ![には](using-templatefields-in-the-gridview-control-vb/_static/image23.png)](using-templatefields-in-the-gridview-control-vb/_static/image22.png)

**図 8**: `LastName` データフィールドに `Text` プロパティをバインドする ([クリックしてフルサイズの画像を表示する](using-templatefields-in-the-gridview-control-vb/_static/image24.png))

> [!NOTE]
> [データバインディング] ダイアログボックスでは、双方向のデータバインディングを実行するかどうかを指定できます。 これをオフのままにすると、`<%# Bind("LastName")%>`の代わりに `<%# Eval("LastName")%>` データバインド構文が使用されます。 このチュートリアルでは、どちらの方法でも問題ありません。 データを挿入または編集する際には、双方向のデータバインディングが重要になります。 ただし、単にデータを表示する場合は、どちらの方法も同様に機能します。 この後のチュートリアルでは、双方向のデータバインディングについて詳しく説明します。

ブラウザーを使用してこのページを表示します。 ご覧のように、GridView には引き続き4つの列があります。ただし、`FirstName` 列には、`FirstName` と `LastName` の*両方*のデータフィールドの値が表示されるようになりました。

[FirstName と LastName の両方の値を1つの列に表示する ![](using-templatefields-in-the-gridview-control-vb/_static/image26.png)](using-templatefields-in-the-gridview-control-vb/_static/image25.png)

**図 9**: `FirstName` と `LastName` の両方の値が1つの列に表示される ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image27.png)されます)

この最初の手順を完了するには、`LastName` BoundField を削除し、`FirstName` TemplateField の `HeaderText` プロパティの名前を "Name" に変更します。 これらの変更を加えた後、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample4.aspx)]

[各従業員の姓と名が1つの列に表示される ![](using-templatefields-in-the-gridview-control-vb/_static/image29.png)](using-templatefields-in-the-gridview-control-vb/_static/image28.png)

**図 10**: 各従業員の姓と名が1つの列に表示される ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image30.png)されます)

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>手順 3: Calendar コントロールを使用して`HiredDate`フィールドを表示する

データフィールドの値を GridView のテキストとして表示することは、BoundField を使用するのと同じように簡単です。 ただし、特定のシナリオでは、テキストだけではなく、特定の Web コントロールを使用してデータを表現することをお勧めします。 TemplateFields を使用すると、データの表示をカスタマイズできます。 たとえば、従業員の雇用日をテキストとして表示するのではなく、カレンダー[コントロール](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)を使用してカレンダーを表示し、採用日を強調表示することができます。

これを実現するには、まず `HiredDate` BoundField を TemplateField に変換します。 GridView のスマートタグにアクセスして、[列の編集] リンクをクリックするだけで、[フィールド] ダイアログボックスが表示されます。 `HiredDate` BoundField を選択し、[このフィールドを TemplateField に変換する] をクリックします。

[HiredDate BoundField を TemplateField に変換 ![には](using-templatefields-in-the-gridview-control-vb/_static/image32.png)](using-templatefields-in-the-gridview-control-vb/_static/image31.png)

**図 11**: `HiredDate` BoundField を TemplateField に変換する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image33.png)されます)

手順 2. で説明したように、これにより、BoundField は、`ItemTemplate` を含む TemplateField に置き換えられます。また、`Text` プロパティが、データバインド構文 `<%# Bind("HiredDate")%>`を使用して `HiredDate` 値にバインドされているラベルとテキストボックスを使用して `EditItemTemplate` ます。

テキストをカレンダーコントロールに置き換えるには、ラベルを削除し、カレンダーコントロールを追加して、テンプレートを編集します。 デザイナーで、GridView のスマートタグから [テンプレートの編集] を選択し、ドロップダウンリストから `HireDate` TemplateField の `ItemTemplate` を選択します。 次に、ラベルコントロールを削除し、[ツールボックス] から [カレンダー] コントロールをテンプレート編集インターフェイスにドラッグします。

[HireDate TemplateField の ItemTemplate に Calendar コントロールを追加 ![には](using-templatefields-in-the-gridview-control-vb/_static/image35.png)](using-templatefields-in-the-gridview-control-vb/_static/image34.png)

**図 12**: `HireDate` TemplateField の `ItemTemplate` に Calendar コントロールを追加する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image36.png)されます)

この時点で、GridView の各行には、`HiredDate` TemplateField に Calendar コントロールが格納されます。 ただし、従業員の実際の `HiredDate` 値は Calendar コントロールのどこにも設定されていないため、各カレンダーコントロールは既定で現在の月と日付を表示します。 これを解決するには、各従業員の `HiredDate` を Calendar コントロールの[SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx)プロパティと[VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx)プロパティに割り当てる必要があります。

カレンダーコントロールのスマートタグから、[自動連結の編集] を選択します。 次に、`SelectedDate` と `VisibleDate` の両方のプロパティを `HiredDate` データフィールドにバインドします。

[VisibleDate プロパティとプロパティを HiredDate データフィールドにバインド ![には](using-templatefields-in-the-gridview-control-vb/_static/image38.png)](using-templatefields-in-the-gridview-control-vb/_static/image37.png)

**図 13**: `SelectedDate` と `VisibleDate` のプロパティを `HiredDate` データフィールドにバインドする ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image39.png)されます)

> [!NOTE]
> カレンダーコントロールの選択された日付は、必ずしも表示されている必要はありません。 たとえば、カレンダーには、選択した日付として1999年 8<sup>月1日</sup>がありますが、現在の月と年が表示される場合があります。 選択された日付と表示される日付は、カレンダーコントロールの `SelectedDate` と `VisibleDate` プロパティによって指定されます。 従業員の `HiredDate` を選択し、表示されていることを確認するために、両方のプロパティを `HireDate` データフィールドにバインドする必要があります。

ブラウザーでページを表示すると、カレンダーに従業員の雇用日の月が表示されるようになり、その特定の日付が選択されます。

[Calendar コントロールに従業員の HiredDate が表示される ![](using-templatefields-in-the-gridview-control-vb/_static/image41.png)](using-templatefields-in-the-gridview-control-vb/_static/image40.png)

**図 14**: 従業員の `HiredDate` が Calendar コントロールに表示される ([クリックしてフルサイズの画像を表示する](using-templatefields-in-the-gridview-control-vb/_static/image42.png))

> [!NOTE]
> これまでに説明したすべての例とは対照的に、このチュートリアルでは、この GridView の `False` に `EnableViewState` プロパティを設定し*ません*でした。 この決定の理由は、カレンダーコントロールの日付をクリックするとポストバックが発生し、カレンダーの選択した日付がクリックされた日付に設定されるためです。 ただし、GridView のビューステートが無効になっている場合、各ポストバックで、GridView のデータが基になるデータソースに再バインドされます。これにより、ユーザーが選択した日付が上書きされ、従業員の `HireDate`に対してカレンダーの選択した日付が*戻さ*れます。

このチュートリアルでは、ユーザーが従業員の `HireDate`を更新できないため、これは議論の説明です。 カレンダーコントロールは、その日付を選択できないように構成することをお勧めします。 このチュートリアルでは、状況によっては、特定の機能を提供するためにビューステートを有効にする必要があることを示しています。

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>手順 4: 従業員が会社に費やした日数を表示する

ここまでは、TemplateFields という2つのアプリケーションを見てきました。

- 2つ以上のデータフィールド値を1つの列に結合する
- テキストではなく Web コントロールを使用してデータフィールド値を表現する

TemplateFields の3番目の用途は、GridView の基になるデータに関するメタデータを表示することです。 たとえば、従業員の入社日を表示するだけでなく、ジョブに対する合計日数を表示する列も必要になる場合があります。

ただし、web ページレポートには、基になるデータをデータベースに格納されている形式とは異なる方法で表示する必要があるシナリオでは、TemplateFields の別の使用方法があります。 `Employees` テーブルに、従業員の性別を示すために文字 `M` または `F` を格納した `Gender` フィールドがあるとします。 この情報を web ページに表示する場合、"M" または "F" だけではなく、"男性" または "女性" として性別を表示することができます。

どちらのシナリオも、ASP.NET ページの分離コードクラス (または、`Shared` メソッドとして実装された別のクラスライブラリ) で、テンプレートから呼び出される*書式指定メソッド*を作成することによって処理できます。 このような書式設定メソッドは、前に示したのと同じデータバインディング構文を使用して、テンプレートから呼び出されます。 書式指定メソッドは、任意の数のパラメーターを受け取ることができますが、文字列を返す必要があります。 返される文字列は、テンプレートに挿入される HTML です。

この概念を説明するために、このチュートリアルを拡張して、従業員がジョブに対して行った日数の合計数を示す列を表示してみましょう。 この書式指定メソッドは、`Northwind.EmployeesRow` オブジェクトを受け取り、従業員が文字列として使用した日数を返します。 このメソッドは、ASP.NET ページの分離コードクラスに追加できますが、テンプレートからアクセスできるようにするには `Protected` または `Public` としてマークされて*いる必要があり*ます。

[!code-vb[Main](using-templatefields-in-the-gridview-control-vb/samples/sample5.vb)]

`HiredDate` フィールドには `NULL` データベース値を含めることができるため、計算を続行する前に値が `NULL` されていないことを確認する必要があります。 `HiredDate` 値が `NULL`場合は、文字列 "Unknown" を返します。`NULL`ない場合は、現在の時刻と `HiredDate` の値の差を計算し、日数を返します。

このメソッドを使用するには、データバインディング構文を使用して GridView の TemplateField から呼び出す必要があります。 まず、GridView のスマートタグの [列の編集] リンクをクリックし、新しい TemplateField を追加して、GridView に新しい TemplateField を追加します。

[GridView に新しい TemplateField を追加 ![には](using-templatefields-in-the-gridview-control-vb/_static/image44.png)](using-templatefields-in-the-gridview-control-vb/_static/image43.png)

**図 15**: GridView に新しい TemplateField を追加する ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image45.png)されます)

この新しい TemplateField の `HeaderText` プロパティを "Days on Job" に設定し、その `ItemStyle`の `HorizontalAlign` プロパティを `Center`に設定します。 テンプレートから `DisplayDaysOnJob` メソッドを呼び出すには、`ItemTemplate` を追加し、次の databinding 構文を使用します。

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample6.aspx)]

`Container.DataItem` は、`GridViewRow`にバインドされている `DataSource` レコードに対応する `DataRowView` オブジェクトを返します。 `Row` プロパティは、厳密に型指定された `Northwind.EmployeesRow`を返します。これは `DisplayDaysOnJob` メソッドに渡されます。 このデータバインディング構文は、次の宣言構文に示すように `ItemTemplate` に直接指定することも、ラベル Web コントロールの `Text` プロパティに割り当てることもできます。

> [!NOTE]
> または、`EmployeesRow` インスタンスを渡す代わりに `<%# DisplayDaysOnJob(Eval("HireDate")) %>`を使用して `HireDate` 値を渡すこともできます。 ただし、`Eval` メソッドは `Object`を返します。そのため、`DisplayDaysOnJob` メソッドシグネチャを変更して `Object`型の入力パラメーターを受け入れる必要があります。 `Employees` テーブルの `HireDate` 列には `NULL` 値を含めることができるため、`Eval("HireDate")` 呼び出しを `DateTime` に対して無条件にキャストすることはできません。 したがって、`DisplayDaysOnJob` メソッドの入力パラメーターとして `Object` を受け入れる必要があります。データベース `NULL` 値 (`Convert.IsDBNull(objectToCheck)`を使用して実現できます) があるかどうかを確認し、それに従って処理を続行します。

これらの微妙な違いにより、`EmployeesRow` インスタンス全体を渡すことにしました。 次のチュートリアルでは、書式指定メソッドに入力パラメーターを渡すための `Eval("columnName")` 構文を使用するための、より多くの継ぎ手の例を示します。

TemplateField が追加された後の GridView の宣言型の構文と、`ItemTemplate`から呼び出された `DisplayDaysOnJob` メソッドを次に示します。

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample7.aspx)]

図16は、ブラウザーを使用して表示された場合の完成したチュートリアルを示しています。

[従業員がジョブに対して行った日数 ![表示されます](using-templatefields-in-the-gridview-control-vb/_static/image47.png)](using-templatefields-in-the-gridview-control-vb/_static/image46.png)

**図 16**: 従業員がジョブに対して行った日数が表示されます ([クリックすると、フルサイズの画像が表示](using-templatefields-in-the-gridview-control-vb/_static/image48.png)されます)

## <a name="summary"></a>まとめ

GridView コントロールの TemplateField を使用すると、他のフィールドコントロールで使用できるデータよりも高い柔軟性でデータを表示できます。 TemplateFields は、次のような場合に最適です。

- 複数のデータフィールドを1つの GridView 列に表示する必要がある
- データは、プレーンテキストではなく Web コントロールを使用して表現することをお勧めします。
- 出力は、メタデータの表示やデータの再フォーマットなど、基になるデータによって異なります。

データの表示をカスタマイズするだけでなく、テンプレートフィールドは、データの編集と挿入に使用されるユーザーインターフェイスをカスタマイズするためにも使用されます。これについては、今後のチュートリアルで説明します。

次の2つのチュートリアルでは、テンプレートについて詳しく説明します。まず、DetailsView で TemplateFields を使用します。 その後、FormView に切り替えます。これにより、フィールドの代わりにテンプレートを使用して、データのレイアウトと構造をより柔軟に設定できます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は Dan Jagers でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](custom-formatting-based-upon-data-vb.md)
> [次へ](using-templatefields-in-the-detailsview-control-vb.md)
