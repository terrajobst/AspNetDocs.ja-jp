---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
title: 2つのページでマスター/詳細をフィルター処理する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、マスター/詳細レポートを2ページに分割する方法について説明します。 ' マスター ' ページで、Repeater コントロールを使用して categ の一覧を表示しています...
ms.author: riande
ms.date: 10/30/2010
ms.assetid: f1a1be2c-6fd9-4a09-916e-aa1b98d5cf17
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 037e5f47efff88bfcbec57b11efa4fec04f9542d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591399"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>2 つのページでマスター/詳細をフィルター処理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_VB.exe)または[PDF のダウンロード](master-detail-filtering-acess-two-pages-datalist-vb/_static/datatutorial34vb1.pdf)

> このチュートリアルでは、マスター/詳細レポートを2ページに分割する方法について説明します。 [マスター] ページで、Repeater コントロールを使用してカテゴリの一覧を表示します。クリックすると、ユーザーは [詳細] ページに移動します。このページには、選択したカテゴリに属する製品が表示されます。

## <a name="introduction"></a>はじめに

[2 ページでのマスター/詳細のフィルター処理](../masterdetail/master-detail-filtering-across-two-pages-vb.md)のチュートリアルでは、システム内のすべてのサプライヤーを表示する GridView を使用して、このパターンを調べています。 この GridView には、2番目のページへのリンクとして表示されるハイパーリンクフィールドが含まれています。これは、クエリ文字列内の `SupplierID` に従って渡されます。 2番目のページでは、GridView を使用して、選択した業者によって提供される製品を一覧表示します。

このような2ページのマスター/詳細レポートは、DataList コントロールと Repeater コントロールを使用しても実行できます。 唯一の違いは、DataList も Repeater もハイパーリンクフィールドコントロールをサポートしないことです。 代わりに、コントロールの `ItemTemplate`内に、ハイパーリンク Web コントロールまたはアンカー HTML 要素 (`<a>`) を追加する必要があります。 ハイパーリンクの `NavigateUrl` プロパティまたはアンカーの `href` 属性は、宣言型またはプログラムによる方法を使用してカスタマイズできます。

このチュートリアルでは、Repeater コントロールを使用して、1ページの箇条書きのカテゴリを一覧表示する例を紹介します。 各リスト項目には、カテゴリの名前と説明が含まれ、カテゴリ名は2番目のページへのリンクとして表示されます。 このリンクをクリックすると、ユーザーが2番目のページに whisk ます。ここで、選択したカテゴリに属する製品が DataList によって表示されます。

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>手順 1: 箇条書きの一覧にカテゴリを表示する

マスター/詳細レポートを作成する最初の手順は、"マスター" レコードを表示することによって開始することです。 そのため、最初のタスクは、"マスター" ページにカテゴリを表示することです。 `DataListRepeaterFiltering` フォルダーの [`CategoryListMaster.aspx`] ページを開き、Repeater コントロールを追加し、スマートタグから新しい ObjectDataSource を追加することを選択します。 `CategoriesBLL` クラスの `GetCategories` メソッドからデータにアクセスするように新しい ObjectDataSource を構成します (図1を参照)。

[カテゴリ Bll クラスの GetCategories メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-filtering-acess-two-pages-datalist-vb/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image1.png)

**図 1**: `CategoriesBLL` クラスの `GetCategories` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-acess-two-pages-datalist-vb/_static/image3.png))

次に、各カテゴリの名前と説明を箇条書きの項目として表示するように、リピータのテンプレートを定義します。 ここでは、各カテゴリが詳細ページにリンクされていることについて心配する必要はありません。 Repeater および ObjectDataSource の宣言型マークアップを次に示します。

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample1.aspx)]

このマークアップが完了したら、ブラウザーで進行状況を確認してください。 図2に示すように、リピータは、各カテゴリの名前と説明を示す箇条書きリストとしてレンダリングします。

[各カテゴリ ![箇条書き項目として表示されます](master-detail-filtering-acess-two-pages-datalist-vb/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image4.png)

**図 2**: 各カテゴリは箇条書き項目として表示されます ([クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image6.png)されます)

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>手順 2: カテゴリ名を詳細ページへのリンクに変える

ユーザーが特定のカテゴリの "詳細" 情報を表示できるようにするには、各箇条書き項目へのリンクを追加する必要があります。これは、クリックすると、ユーザーが2番目のページ (`ProductsForCategoryDetails.aspx`) に移動します。 この2番目のページには、DataList を使用して、選択したカテゴリの製品が表示されます。 リンクがクリックされたカテゴリを確認するには、いくつかのメカニズムを使用して、クリックしたカテゴリの `CategoryID` を2番目のページに渡す必要があります。 1つのページから別のページにスカラーデータを転送する最も簡単で最も簡単な方法は、このチュートリアルで使用するオプションであるクエリ文字列を使用することです。 特に、[`ProductsForCategoryDetails.aspx`] ページでは、選択した *`categoryID`* 値が `CategoryID`という名前の querystring フィールドを介して渡されることを想定しています。 たとえば、`CategoryID` が1である飲み物カテゴリの製品を表示するには、ユーザーが `ProductsForCategoryDetails.aspx?CategoryID=1`にアクセスします。

リピータの箇条書き項目ごとにハイパーリンクを作成するには、ハイパーリンク Web コントロールまたは HTML アンカー要素 (`<a>`) を `ItemTemplate`に追加する必要があります。 ハイパーリンクが各行に対して同じように表示されるシナリオでは、どちらの方法でも十分です。 リピータの場合は、anchor 要素を使用します。 アンカー要素を使用するには、リピータの ItemTemplate を次のように更新します。

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample2.aspx)]

`CategoryID` は、アンカー要素の `href` 属性内に直接挿入できることに注意してください。ただし、そのためには、`href` 属性内の `Eval` メソッドが引用符で囲まれた文字列 (`"CategoryID"`) を区切るため、`href` 属性の値をアポストロフィ (および note 引用符) で区切る必要があります。 代わりに、HyperLink Web コントロールを使用することもできます。

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample3.aspx)]

URL の静的な部分 (`ProductsForCategoryDetails.aspx?CategoryID`) が、文字列の連結を使用してデータバインド構文内の `Eval("CategoryID")` の結果に直接追加されることに注意してください。

HyperLink コントロールを使用する利点の1つは、必要に応じて、Repeater の `ItemDataBound` イベントハンドラーからプログラムでアクセスできることです。 たとえば、商品が関連付けられていないカテゴリのリンクとしてではなく、カテゴリ名をテキストとして表示することができます。 このようなチェックは、プログラムで `ItemDataBound` イベントハンドラーで実行できます。製品が関連付けられていないカテゴリの場合、ハイパーリンクの `NavigateUrl` プロパティを空の文字列に設定すると、その結果、特定のカテゴリ名がリンクとしてではなくプレーンテキストとして表示される可能性があります。 `ItemDataBound` イベントハンドラーを使用してプログラムロジックに基づいて DataList と Repeater の内容を書式設定する方法の詳細については、「[データに基づいて datalist と repeater を書式設定](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md)する」のチュートリアルを参照してください。

フォローしている場合は、ページでアンカー要素またはハイパーリンクコントロールのいずれかの方法を自由に使用できます。 方法に関係なく、ブラウザーを使用してページを表示する場合は、各カテゴリ名を `ProductsForCategoryDetails.aspx`へのリンクとしてレンダリングし、該当する `CategoryID` 値を渡す必要があります (図3を参照)。

[カテゴリ名を ![して、製品のカテゴリの詳細にリンクします。](master-detail-filtering-acess-two-pages-datalist-vb/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image7.png)

**図 3**: カテゴリ名が `ProductsForCategoryDetails.aspx` にリンクされる ([クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image9.png)されます)

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>手順 3: 選択したカテゴリに属する製品を一覧表示する

`CategoryListMaster.aspx` のページが完成したら、[詳細] ページの `ProductsForCategoryDetails.aspx`を実装することに注意する必要があります。 このページを開き、ツールボックスから DataList をデザイナーにドラッグし、その `ID` プロパティを `ProductsInCategory`に設定します。 次に、DataList のスマートタグから、ページに新しい ObjectDataSource を追加して、`ProductsInCategoryDataSource`名前を付けます。 `ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` メソッドを呼び出すように構成します。[挿入]、[更新]、および [削除] の各タブのドロップダウンリストを [(なし)] に設定します。

[製品の Bll クラスの Get$ Bycategoryid (categoryID) メソッドを使用するように ObjectDataSource を構成 ![](master-detail-filtering-acess-two-pages-datalist-vb/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image10.png)

**図 4**: `ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-filtering-acess-two-pages-datalist-vb/_static/image12.png))

`GetProductsByCategoryID(categoryID)` メソッドは入力パラメーター ( *`categoryID`* ) を受け入れるため、データソースの選択ウィザードでは、パラメーターのソースを指定することができます。 QueryStringField `CategoryID`を使用して、パラメーターソースを QueryString に設定します。

[パラメーターのソースとして Querystring フィールド CategoryID を使用 ![](master-detail-filtering-acess-two-pages-datalist-vb/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image13.png)

**図 5**: クエリ文字列フィールド `CategoryID` をパラメーターのソースとして使用する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image15.png)されます)

前のチュートリアルで見たように、データソースの選択ウィザードを完了すると、Visual Studio によって、各データフィールドの名前と値を一覧表示する DataList の `ItemTemplate` が自動的に作成されます。 このテンプレートを、製品の名前、供給業者、価格のみを一覧表示するものに置き換えます。 また、DataList の `RepeatColumns` プロパティを2に設定します。 これらの変更が完了すると、DataList および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample4.aspx)]

このページを実際に表示するには、[`CategoryListMaster.aspx`] ページから開始します。次に、[カテゴリ] 箇条書きのリンクをクリックします。 これにより、`ProductsForCategoryDetails.aspx`に移動し、クエリ文字列を使用して `CategoryID` を渡します。 `ProductsForCategoryDetails.aspx` の `ProductsInCategoryDataSource` ObjectDataSource は、指定されたカテゴリの製品だけを取得し、それを DataList に表示します。これにより、行ごとに2つの製品がレンダリングされます。 図6は、飲み物を表示するときに `ProductsForCategoryDetails.aspx` のスクリーンショットを示しています。

[飲み物が表示される ![、行ごとに2つ](master-detail-filtering-acess-two-pages-datalist-vb/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image16.png)

**図 6**: 飲み物が表示され、行ごとに2つ ([クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image18.png)されます)

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>手順 4: 製品のカテゴリ情報を表示する詳細 .aspx

ユーザーが `CategoryListMaster.aspx`でカテゴリをクリックすると、選択したカテゴリに属する製品が `ProductsForCategoryDetails.aspx` に表示されます。 ただし `ProductsForCategoryDetails.aspx` では、どのカテゴリが選択されたかについての視覚的な手掛かりはありません。 [飲み物] をクリックしたが、誤って Condiments をクリックしたユーザーは、`ProductsForCategoryDetails.aspx`になると誤ってその間違いを認識することはできません。 この潜在的な問題を軽減するには、[`ProductsForCategoryDetails.aspx`] ページの上部にある、選択したカテゴリ (名前と説明) に関する情報を表示します。

これを実現するには、`ProductsForCategoryDetails.aspx`で Repeater コントロールの上に FormView を追加します。 次に、`CategoryDataSource` という名前の FormView のスマートタグからページに新しい ObjectDataSource を追加し、`CategoriesBLL` クラスの `GetCategoryByCategoryID(categoryID)` メソッドを使用するように構成します。

[カテゴリ Bll クラスの Getcategory Bycategoryid (categoryID) メソッドを使用して、カテゴリに関する情報にアクセス ![](master-detail-filtering-acess-two-pages-datalist-vb/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image19.png)

**図 7**: `CategoriesBLL` クラスの `GetCategoryByCategoryID(categoryID)` メソッドを使用してカテゴリに関する情報にアクセス[する (クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image21.png)されます)

手順 3. で追加した `ProductsInCategoryDataSource` ObjectDataSource と同様に、`CategoryDataSource`のデータソース構成ウィザードによって、`GetCategoryByCategoryID(categoryID)` メソッドの入力パラメーターのソースが要求されます。 以前とまったく同じ設定を使用し、パラメーターソースを QueryString に、QueryStringField 値を `CategoryID` に設定します (図5を参照)。

ウィザードを完了すると、Visual Studio によって、FormView の `ItemTemplate`、`EditItemTemplate`、および `InsertItemTemplate` が自動的に作成されます。 読み取り専用のインターフェイスを提供しているので、`EditItemTemplate` と `InsertItemTemplate`を削除してもかまいません。 また、FormView の `ItemTemplate`を自由にカスタマイズすることもできます。 余分なテンプレートを削除し、ItemTemplate をカスタマイズした後、FormView および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample5.aspx)]

図8は、ブラウザーを使用してこのページを表示する際のスクリーンショットを示しています。

> [!NOTE]
> FormView に加えて、ユーザーがカテゴリの一覧 (`CategoryListMaster.aspx`) に戻るように、FormView の上に HyperLink コントロールも追加しました。 このリンクを他の場所に配置するか、完全に省略することをお勧めします。

[![カテゴリ情報がページの上部に表示されるようになりました](master-detail-filtering-acess-two-pages-datalist-vb/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image22.png)

**図 8**: カテゴリ情報がページの上部に表示されるようになりました ([クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image24.png)されます)

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>手順 5: 選択したカテゴリに属している製品がない場合にメッセージを表示する

[`CategoryListMaster.aspx`] ページには、関連付けられている製品があるかどうかに関係なく、システム内のすべてのカテゴリが一覧表示されます。 製品が関連付けられていないカテゴリをユーザーがクリックした場合、そのデータソースには項目が含まれていないため、`ProductsForCategoryDetails.aspx` の DataList はレンダリングされません。 これまでのチュートリアルで説明したように、GridView には、データソースにレコードが存在しない場合に表示するテキストメッセージを指定するために使用できる `EmptyDataText` のプロパティが用意されています。 残念ながら、DataList も Repeater もこのようなプロパティを持っていません。

選択したカテゴリに一致する製品がないことをユーザーに通知するメッセージを表示するには、対応する製品がない場合に表示するメッセージが `Text` プロパティに割り当てられているページにラベルコントロールを追加する必要があります。 次に、DataList に項目が含まれているかどうかに基づいて、プログラムによって `Visible` プロパティを設定する必要があります。

これを実現するには、まず、DataList の下にラベルを追加します。 `ID` プロパティを `NoProductsMessage` に設定し、その `Text` プロパティを "選択したカテゴリの製品がありません..." に設定します。次に、データが `ProductsInCategory` DataList にバインドされているかどうかに基づいて、このラベルの `Visible` プロパティをプログラムで設定する必要があります。 この割り当ては、データが DataList にバインドされた後に行う必要があります。 GridView、DetailsView、および FormView では、コントロールの `DataBound` イベントのイベントハンドラーを作成できます。これは、データバインドが完了した後に発生します。 ただし、DataList も Repeater も `DataBound` イベントは使用できません。

この例では、ページの `Load` イベントの前に DataList にデータが割り当てられているため、`Page_Load` イベントハンドラーでラベルの `Visible` プロパティを割り当てることができます。 ただし、この方法は一般的なケースでは機能しません。これは、ObjectDataSource からのデータが、後でページのライフサイクルの DataList にバインドされる可能性があるためです。 たとえば、表示されたデータが別のコントロールの値に基づいている場合 (たとえば、DropDownList を使用してマスター/詳細レポートを表示し、"マスター" レコードを保持する場合など)、データはページのライフサイクルの `PreRender` 段階まで、データ Web コントロールに再バインドされない可能性があります。

どのような場合でも機能する1つの解決策は、`Item` または `AlternatingItem`の項目の種類をバインドするときに、DataList の `ItemDataBound` (または `ItemCreated`) イベントハンドラーの `False` に `Visible` プロパティを割り当てることです。 このような場合は、データソースに少なくとも1つのデータ項目があることがわかっているため、`NoProductsMessage` ラベルを非表示にすることができます。 このイベントハンドラーに加えて、DataList の `DataBinding` イベントのイベントハンドラーも必要です。ここでは、ラベルの `Visible` プロパティを `True`に初期化します。 `DataBinding` イベントは `ItemDataBound` イベントの前に発生するため、ラベルの `Visible` プロパティは最初は `True`に設定されます。ただし、データ項目がある場合は、`False`に設定されます。 次のコードは、このロジックを実装しています。

[!code-vb[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample6.vb)]

Northwind データベースのすべてのカテゴリは、1つまたは複数の製品に関連付けられています。 この機能をテストするには、このチュートリアルで Northwind データベースを手動で調整し、[生成] カテゴリに関連付けられているすべての製品 (`CategoryID` = 7) をシーフードカテゴリ (`CategoryID` = 8) に再割り当てします。 これを行うには、[新しいクエリ] を選択し、次の `UPDATE` ステートメントを使用して、サーバーエクスプローラーを実行します。

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample7.sql)]

必要に応じてデータベースを更新した後、[`CategoryListMaster.aspx`] ページに戻り、[生成] リンクをクリックします。 生成カテゴリに属する製品はなくなったため、"選択したカテゴリの製品はありません..." と表示されます。メッセージ (図9を参照)。

[選択したカテゴリに属する製品がない場合、メッセージが表示さ ![](master-detail-filtering-acess-two-pages-datalist-vb/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image25.png)

**図 9**: 選択したカテゴリに属する製品がない場合は、メッセージが表示されます ([クリックすると、フルサイズの画像が表示](master-detail-filtering-acess-two-pages-datalist-vb/_static/image27.png)されます)

## <a name="summary"></a>要約

マスター/詳細レポートでは、マスターレコードと詳細レコードの両方を1ページに表示できますが、多くの web サイトでは、2つの web ページに分割されています。 このチュートリアルでは、マスター/詳細レポートを実装する方法について説明しました。これには、"マスター" web ページでリピータを使用し、[詳細] ページに一覧表示されている関連する製品を使用して、リストにカテゴリを表示します。 マスター web ページの各リスト項目には、行の `CategoryID` 値に従って渡された詳細ページへのリンクが含まれていました。

詳細ページでは、指定された業者のこれらの製品を取得するために、`ProductsBLL` クラスの `GetProductsByCategoryID(categoryID)` 方法を使用しました。 *`categoryID`* パラメーターの値が、パラメーターソースとして `CategoryID` querystring の値を使用して宣言的に指定されました。 また、FormView を使用して詳細ページにカテゴリの詳細を表示する方法と、選択したカテゴリに属している製品がない場合にメッセージを表示する方法についても説明しました。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Zack Jones と Liz Shulok でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
> [次へ](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)
