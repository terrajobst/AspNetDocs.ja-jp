---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
title: マスター/詳細 (行頭文字付きのマスターレコードの一覧と詳細 DataList (VB) を使用した)Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、前のチュートリアルの2ページのマスター/詳細レポートを1つのページに圧縮します。これにより、名前の付いたカテゴリ名の一覧が t... で表示されます。
ms.author: riande
ms.date: 10/17/2006
ms.assetid: ee20742f-6fb7-49a0-a009-058fe363aacb
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 81d72c666925e89729464e7ea696bde8d323e277
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78490690"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb"></a>マスター レコードの箇条書きと詳細 DataList を使用してマスター/詳細を表示する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_VB.exe)または[PDF のダウンロード](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/datatutorial35vb1.pdf)

> このチュートリアルでは、前のチュートリアルの2ページのマスター/詳細レポートを1つのページに圧縮して、画面の左側にカテゴリ名の箇条書きリストを表示し、画面の右側に選択したカテゴリの製品を表示します。

## <a name="introduction"></a>はじめに

前の[チュートリアル](master-detail-filtering-acess-two-pages-datalist-vb.md)では、マスター/詳細レポートを2ページに分割する方法を見てきました。 マスターページでは、Repeater コントロールを使用して、カテゴリの箇条書きリストを表示していました。 各カテゴリ名はハイパーリンクでした。クリックすると、ユーザーは [詳細] ページに移動します。このページには、選択したカテゴリに属する製品が表示されます。

このチュートリアルでは、2ページのチュートリアルを1つのページに圧縮し、各カテゴリ名を LinkButton として表示し、画面の左側にカテゴリ名の箇条書きリストを表示します。 Category name LinkButtons のいずれかをクリックすると、ポストバックが誘発され、選択したカテゴリの製品が画面右側の2列の DataList にバインドされます。 各カテゴリの名前を表示するだけでなく、左側のリピータは特定のカテゴリの製品の合計数を示しています (図1を参照)。

[カテゴリの名前と製品の合計数が左側に表示され ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image1.png)

**図 1**: カテゴリの名前と製品の合計数が左側に表示される ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image3.png)されます)

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>手順 1: 画面の左側の部分にリピータを表示する

このチュートリアルでは、選択したカテゴリの製品の左側に、カテゴリの箇条書きの一覧が表示されている必要があります。 Web ページ内のコンテンツを配置するには、標準の HTML 要素の段落タグ、改行しないスペース、`<table>` s などを使用するか、カスケードスタイルシート (CSS) 手法を使用します。 これまでのすべてのチュートリアルでは、配置に CSS 手法が使用されていました。 [マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-vb.md)のチュートリアルで、マスターページにナビゲーションユーザーインターフェイスを構築したときに、ナビゲーションリストとメインコンテンツの正確なピクセルオフセットを示す*絶対配置*を使用していました。 または、CSS を使用して、1つの要素を別の要素の右側または左側に*フローティング*で配置することもできます。 DataList を使用して、選択したカテゴリの製品の左側に、DataList の左側にあるリストを表示できます。

`DataListRepeaterFiltering` フォルダーから `CategoriesAndProducts.aspx` ページを開き、Repeater と DataList というページに追加します。 Repeater の `ID` を `Categories` に設定し、DataList を `CategoryProducts`に設定します。 ソースビューに移動し、Repeater コントロールと DataList コントロールを独自の `<div>` 要素内に配置します。 つまり、まず `<div>` 要素内で Repeater を囲み、次に、独自の `<div>` 要素内の DataList をリピータの直後に記述します。 この時点で、マークアップは次のようになります。

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample1.aspx)]

Repeater を DataList の左側にフローティングさせるには、次のように `float` CSS スタイル属性を使用する必要があります。

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample2.html)]

`float: left;` は、最初の `<div>` 要素を2番目の要素の左側にフローティングします。 `width` と `padding-right` の設定は、最初の `<div>` s `width`、および `<div>` 要素のコンテンツとその右余白の間に追加される余白を示します。 CSS の浮動要素の詳細については、 [Floatutorial](http://css.maxdesign.com.au/floatutorial/)を参照してください。

最初の `<p>` element s `style` 属性を使用してスタイル設定を直接指定するのではなく、`FloatLeft`という名前の `Styles.css` に新しい CSS クラスを作成します。

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample3.css)]

その後、`<div>` を `<div class="FloatLeft">`に置き換えることができます。

CSS クラスを追加し、[`CategoriesAndProducts.aspx`] ページでマークアップを構成した後、デザイナーにアクセスします。 データソースまたはテンプレートをまだ構成していないので、このダイアログボックスの左側には [Repeater] が表示されます (ただし、現在は灰色のボックスとして表示されています)。

[![、Repeater が DataList の左側にフローティングされます。](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image4.png)

**図 2**: Repeater が DataList の左側にフロートする ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image6.png)されます)

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>手順 2: 各カテゴリの製品数を確認する

リピータと DataList を囲むマークアップが完了したら、カテゴリデータを Repeater コントロールにバインドする準備ができました。 ただし、図1のカテゴリの箇条書きリストが示されているように、各カテゴリの名前に加えて、カテゴリに関連付けられている製品の数も表示する必要があります。 この情報にアクセスするには、次のいずれかの方法があります。

- **この情報は、ASP.NET ページの分離コードクラスから確認してください。** 特定の *`categoryID`* を指定すると、`ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを呼び出すことによって、関連付けられている製品の数を特定できます。 このメソッドは `ProductsDataTable` オブジェクトを返します。この `Count` オブジェクトは、指定された *`categoryID`* の製品数である `ProductsRow` s の数を示します。 リピータにバインドされている各カテゴリについて、`ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを呼び出し、そのカウントを出力に含める、リピータの `ItemDataBound` イベントハンドラーを作成できます。
- **`NumberOfProducts` 列を含めるように、型指定されたデータセットの `CategoriesDataTable` を更新します。** 次に、`CategoriesDataTable` の `GetCategories()` メソッドを更新してこの情報を含めるか、または `GetCategories()` をそのままにして、`GetCategoriesAndNumberOfProducts()`という新しい `CategoriesDataTable` メソッドを作成できます。

では、これらの両方の手法について説明します。 データアクセス層を更新する必要がないため、最初の方法は簡単に実装できます。ただし、データベースとの通信を増やす必要があります。 `ItemDataBound` イベントハンドラーの `ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを呼び出すと、リピータに表示される各カテゴリに対して、追加のデータベース呼び出しが追加されます。 この手法では、 *n* + 1 データベースが呼び出されます。ここで、 *n*はリピータに表示されるカテゴリの数です。 2番目の方法では、`CategoriesBLL` クラス s `GetCategories()` (または `GetCategoriesAndNumberOfProducts()`) メソッドから、各カテゴリに関する情報と共に製品数が返されます。これにより、データベースへのトリップが1回だけになります。

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>ItemDataBound バインドイベントハンドラー内の製品の数を確認する

リピータ s `ItemDataBound` イベントハンドラーの各カテゴリの製品数を特定しても、既存のデータアクセス層を変更する必要はありません。 すべての変更は、[`CategoriesAndProducts.aspx`] ページ内で直接行うことができます。 まず、Repeater s スマートタグを介して `CategoriesDataSource` という名前の新しい ObjectDataSource を追加します。 次に、`CategoriesBLL` クラス s `GetCategories()` メソッドからデータを取得するように `CategoriesDataSource` ObjectDataSource を構成します。

[GetCategories () メソッドを使用するように ObjectDataSource を構成 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image7.png)

**図 3**: `CategoriesBLL` クラス s `GetCategories()` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image9.png))

`Categories` リピータの各項目をクリック可能にする必要があります。クリックすると、`CategoryProducts` DataList によって選択したカテゴリの製品が表示されます。 これを行うには、前のチュートリアルで説明したように、各カテゴリにハイパーリンクを設定し、同じページ (`CategoriesAndProducts.aspx`) にリンクしてから、クエリ文字列を使用して `CategoryID` を渡します。 この方法の利点は、特定のカテゴリの製品を表示するページにブックマークを付けて、検索エンジンでインデックスを作成できることです。

または、各カテゴリを LinkButton にすることもできます。これは、このチュートリアルで使用するアプローチです。 LinkButton は、ユーザーのブラウザーでハイパーリンクとしてレンダリングされますが、クリックするとポストバックが誘発されます。ポストバック時に、DataList s ObjectDataSource を更新して、選択したカテゴリに属する製品を表示する必要があります。 このチュートリアルでは、ハイパーリンクを使用する方が、LinkButton を使用するよりもわかりやすくなります。ただし、LinkButton を使用する方が有利な場合もあります。 この例ではハイパーリンクのアプローチが理想的ですが、では、LinkButton の使用方法についても説明します。 ここで説明するように、LinkButton を使用すると、ハイパーリンクでは発生しないいくつかの課題が発生します。 このため、このチュートリアルで LinkButton を使用すると、これらの課題が強調表示されるため、ハイパーリンクの代わりに LinkButton を使用する必要があるシナリオに対するソリューションを提供できます。

> [!NOTE]
> このチュートリアルは、LinkButton の代わりに HyperLink コントロールまたは `<a>` 要素を使用して繰り返すことをお勧めします。

次のマークアップは、Repeater および ObjectDataSource の宣言型の構文を示しています。 Repeater テンプレートは、各項目を LinkButton として使用して箇条書きを表示することに注意してください。

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample4.aspx)]

> [!NOTE]
> このチュートリアルでは、リピータのビューステートが有効になっている必要があります (リピータの宣言構文からの `EnableViewState="False"` が省略されていることに注意してください)。 手順3では、`ItemCommand` イベントのイベントハンドラーを作成します。ここでは、DataList s ObjectDataSource s `SelectParameters` コレクションを更新します。 ただし、Repeater の `ItemCommand`は、ビューステートが無効になっている場合には起動しません。 Repeater s `ItemCommand` イベントの発生時にビューステートを有効にする必要がある理由の詳細については、 [ASP.NET の質問](http://scottonwriting.net/sowblog/posts/1263.aspx)と[その解決策](http://scottonwriting.net/sowBlog/posts/1268.aspx)に関する Stumper を参照してください。

`ViewCategory` の `ID` プロパティ値を持つ LinkButton の `Text` プロパティが設定されていません。 カテゴリ名を表示するだけの場合は、次のように、データバインディング構文を使用して、Text プロパティを宣言的に設定します。

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample5.aspx)]

ただし、カテゴリの名前*と*そのカテゴリに属する製品の数の両方を表示する必要があります。 この情報は、次のコードに示すように、`ProductBLL` クラス s `GetCategoriesByProductID(categoryID)` メソッドを呼び出し、結果の `ProductsDataTable`で返されるレコードの数を決定することによって、Repeater s `ItemDataBound` イベントハンドラーから取得できます。

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample6.vb)]

まず、データ項目 (`ItemType` が `Item` または `AlternatingItem`) を操作し、現在の `RepeaterItem`にバインドされたばかりの `CategoriesRow` インスタンスを参照していることを確認します。 次に、`ProductsBLL` クラスのインスタンスを作成し、その `GetCategoriesByProductID(categoryID)` メソッドを呼び出し、`Count` プロパティを使用して返されるレコードの数を決定することによって、このカテゴリの製品の数を決定します。 最後に、ItemTemplate の `ViewCategory` LinkButton は references で、その `Text` プロパティは [*区分*値] (*numberofproductsincategory*) に設定されます。ここで、 *numberofproductsincategory*は小数点以下をゼロにした数値として書式設定されます。

> [!NOTE]
> 別の方法として、ASP.NET ページの分離コードクラスに*書式関数*を追加して、カテゴリの `CategoryName` と `CategoryID` 値を受け取り、カテゴリの製品数と連結した `CategoryName` を返すこともできます (`GetCategoriesByProductID(categoryID)` メソッドを呼び出すことによって決定)。 このような書式設定関数の結果は、`ItemDataBound` イベントハンドラーの必要性を置き換えるために、LinkButton の Text プロパティに宣言によって割り当てられる可能性があります。 書式設定関数の使用方法の詳細については、 [GridView コントロールの Using TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)を参照するか、データのチュートリアルに[基づいて DataList と Repeater を書式設定](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md)してください。

このイベントハンドラーを追加した後、ブラウザーを使用してページをテストします。 各カテゴリが箇条書きで一覧表示され、カテゴリの名前とカテゴリに関連付けられている製品の数が表示されます (図4を参照)。

[各カテゴリの名前と製品数が ![表示されます。](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image10.png)

**図 4**: 各カテゴリの名前と製品の数が表示されます ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image12.png)されます)

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>各カテゴリの製品数を含むように`CategoriesDataTable`と`CategoriesTableAdapter`を更新する

各カテゴリの製品数をリピータにバインドするのではなく、データアクセス層の `CategoriesDataTable` と `CategoriesTableAdapter` を調整してこの情報をネイティブに含めることで、このプロセスを効率化できます。 これを実現するには、`CategoriesDataTable` に新しい列を追加して、関連付けられている製品の数を保持する必要があります。 DataTable に新しい列を追加するには、型指定されたデータセット (`App_Code\DAL\Northwind.xsd`) を開き、変更する DataTable を右クリックして、[追加/列] を選択します。 `CategoriesDataTable` に新しい列を追加します (図5を参照)。

[新しい列をカテゴリデータソースに追加 ![には](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image13.png)

**図 5**: `CategoriesDataSource` に新しい列を追加する ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image15.png)されます)

これにより、`Column1`という名前の新しい列が追加されます。これは、別の名前を入力するだけで変更できます。 この新しい列の名前を `NumberOfProducts`に変更します。 次に、この列のプロパティを構成する必要があります。 新しい列をクリックし、プロパティウィンドウにアクセスします。 図6に示すように、列の `DataType` プロパティを `System.String` から `System.Int32` に変更し、`ReadOnly` プロパティを `True`に設定します。

![新しい列の DataType プロパティと ReadOnly プロパティを設定します。](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image16.png)

**図 6**: 新しい列の `DataType` と `ReadOnly` のプロパティを設定する

`CategoriesDataTable` には `NumberOfProducts` の列がありますが、その値は、対応する TableAdapter のクエリによって設定されていません。 カテゴリ情報を取得するたびにこのような情報が返されるようにする場合は、`GetCategories()` メソッドを更新してこの情報を返すことができます。 ただし、少数のインスタンス (このチュートリアルの場合のみ) で、カテゴリに関連付けられている製品の数を取得する必要があるだけの場合は、`GetCategories()` をそのままにして、この情報を返す新しいメソッドを作成することができます。 この後者の方法を使用して、`GetCategoriesAndNumberOfProducts()`という名前の新しいメソッドを作成してみましょう。

この新しい `GetCategoriesAndNumberOfProducts()` メソッドを追加するには、`CategoriesTableAdapter` を右クリックし、[新しいクエリ] をクリックします。 これにより、前のチュートリアルで何度も使用されていた TableAdapter クエリ構成ウィザードが起動します。 この方法では、クエリで行を返すアドホック SQL ステートメントが使用されていることを示すことによって、ウィザードを開始します。

[アドホック SQL ステートメントを使用してメソッドを作成 ![には](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image17.png)

**図 7**: アドホック SQL ステートメントを使用してメソッドを作成[する (クリックすると、フルサイズのイメージが表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image19.png)されます)

[SQL ステートメントが行を返す ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image20.png)

**図 8**: SQL ステートメントによって行が返される ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image22.png)されます)

次のウィザード画面で、使用するクエリを入力するように求められます。 カテゴリに関連付けられている製品の数と共に、カテゴリ s `CategoryID`、`CategoryName`、および `Description` フィールドを返すには、次の `SELECT` ステートメントを使用します。

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample7.sql)]

[使用するクエリを指定 ![には](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image23.png)

**図 9**: 使用するクエリを指定する ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image25.png)されます)

カテゴリに関連付けられている製品の数を計算するサブクエリには、`NumberOfProducts`という別名が付いていることに注意してください。 この名前付けの一致により、このサブクエリによって返される値が `CategoriesDataTable` s `NumberOfProducts` 列に関連付けられます。

このクエリを入力したら、最後の手順として、新しいメソッドの名前を選択します。 `FillWithNumberOfProducts` と `GetCategoriesAndNumberOfProducts` を使用して DataTable にデータを格納し、それぞれ DataTable パターンを返します。

[新しい TableAdapter のメソッド FillWithNumberOfProducts と Getカテゴリおよび Getproducts の ![名前](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image26.png)

**図 10**: 新しい TableAdapter のメソッド `FillWithNumberOfProducts` と `GetCategoriesAndNumberOfProducts` の名前を指定[する (クリックすると、フルサイズのイメージが表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image28.png)されます)

この時点で、データアクセス層は、カテゴリごとの製品数を含むように拡張されています。 すべてのプレゼンテーション層は、別のビジネスロジックレイヤーを通じて DAL へのすべての呼び出しをルーティングするため、対応する `GetCategoriesAndNumberOfProducts` メソッドを `CategoriesBLL` クラスに追加する必要があります。

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample8.vb)]

DAL と BLL が完成したので、このデータを `CategoriesAndProducts.aspx`の `Categories` リピータにバインドする準備ができました。 [`ItemDataBound` イベントハンドラーで製品の数を決定する] セクションからリピータの ObjectDataSource を既に作成している場合は、この ObjectDataSource を削除し、Repeater s `DataSourceID` プロパティの設定を削除します。また、ASP.NET 分離コードクラスの `Handles Categories.OnItemDataBound` 構文を削除することによって、イベントハンドラーからリピータ s `ItemDataBound` イベントの送信を解除します。

リピータが元の状態に戻ったら、Repeater s スマートタグを介して `CategoriesDataSource` という名前の新しい ObjectDataSource を追加します。 `CategoriesBLL` クラスを使用するように ObjectDataSource を構成しますが、`GetCategories()` メソッドを使用するのではなく、代わりに `GetCategoriesAndNumberOfProducts()` を使用します (図11を参照)。

[Get分類 Andnumberofproducts メソッドを使用するように ObjectDataSource を構成 ![には](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image29.png)

**図 11**: `GetCategoriesAndNumberOfProducts` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image31.png))

次に、`ItemTemplate` を更新して、LinkButton `Text` プロパティが databinding 構文を使用して宣言に割り当てられ、`CategoryName` と `NumberOfProducts` の両方のデータフィールドが含まれるようにします。 リピータと `CategoriesDataSource` ObjectDataSource の完全な宣言マークアップは次のようになります。

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample9.aspx)]

`NumberOfProducts` 列を含むように DAL を更新することによって表示される出力は、`ItemDataBound` イベントハンドラーアプローチを使用する場合と同じです (図4を参照して、名前と製品の数を示すリピータのスクリーンショットを参照してください)。

## <a name="step-3-displaying-the-selected-category-s-products"></a>手順 3: 選択したカテゴリの製品を表示する

この時点で、`Categories` リピータは、カテゴリの一覧と各カテゴリの製品数を表示しています。 リピータは、各カテゴリに対して LinkButton を使用します。この場合、クリックするとポストバックが発生します。その時点で、選択したカテゴリの製品を `CategoryProducts` DataList に表示する必要があります。

私たちが直面する課題の1つは、DataList に、選択したカテゴリの製品のみが表示されるようにする方法です。 詳細な[detailsview チュートリアルで選択可能なマスター GridView を使用したマスター/詳細](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)では、選択した行の詳細が同じページの DetailsView に表示されている行を含む gridview を作成する方法を説明しました。 GridView は、`ProductsBLL` s `GetProducts()` メソッドを使用してすべての製品に関する情報を返しましたが、DetailsView は `GetProductsByProductID(productID)` メソッドを使用して選択された製品に関する情報を取得しました。 *`productID`* パラメーター値は、GridView の `SelectedValue` プロパティの値に関連付けて宣言によって指定されました。 残念ながら、リピータには `SelectedValue` プロパティがないため、パラメーターソースとして使用することはできません。

> [!NOTE]
> これは、リピータで LinkButton を使用するときに表示される問題の1つです。 代わりに、ハイパーリンクを使用してクエリ文字列を使用して `CategoryID` を渡すと、そのクエリ文字列フィールドをパラメーター s 値のソースとして使用できるようになりました。

ただし、リピータの `SelectedValue` プロパティがないことについて心配する前に、まず DataList を ObjectDataSource にバインドし、その `ItemTemplate`を指定してみましょう。

DataList s スマートタグから、`CategoryProductsDataSource` という名前の新しい ObjectDataSource を追加し、`ProductsBLL` class s `GetProductsByCategoryID(categoryID)` メソッドを使用するように構成します。 このチュートリアルの DataList には読み取り専用のインターフェイスが用意されているので、[挿入]、[更新]、および [削除] の各タブのドロップダウンリストを (なし) に自由に設定できます。

[製品の Bll クラス s Get$ Bycategoryid (categoryID) メソッドを使用するように ObjectDataSource を構成 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image32.png)

**図 12**: `ProductsBLL` クラス s `GetProductsByCategoryID(categoryID)` メソッドを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image34.png))

`GetProductsByCategoryID(categoryID)` メソッドは入力パラメーター ( *`categoryID`* ) を必要とするため、データソースの構成ウィザードを使用して、パラメーター s Source を指定できます。 GridView または DataList にカテゴリが一覧表示されているので、[パラメーターのソース] ドロップダウンリストを [制御] に設定し、ControlID をデータ Web コントロールの `ID` に設定します。 ただし、リピータには `SelectedValue` プロパティがないため、パラメーターソースとして使用することはできません。 このチェックボックスをオンにすると、[ControlID] ドロップダウンリストには、DataList の `ID` であるコントロール `ID``CategoryProducts`が1つだけ含まれていることがわかります。

ここでは、[パラメーターソース] ドロップダウンリストを [なし] に設定します。 ここでは、Repeater でカテゴリ LinkButton がクリックされたときに、プログラムによってこのパラメーター値を割り当てます。

[categoryID パラメーターのパラメーターソースを指定し ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image35.png)

**図 13**: *`categoryID`* パラメーターのパラメーターソースを指定しない ([クリックしてフルサイズのイメージを表示する](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image37.png))

データソースの構成ウィザードを完了すると、Visual Studio によって DataList s `ItemTemplate`が自動生成されます。 この既定の `ItemTemplate` を、前のチュートリアルで使用したテンプレートに置き換えます。また、[DataList s `RepeatColumns`] プロパティを [2] に設定します。 これらの変更を行った後、DataList の宣言型マークアップとそれに関連付けられている ObjectDataSource は次のようになります。

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample10.aspx)]

現時点では、`CategoryProductsDataSource` ObjectDataSource s *`categoryID`* パラメーターは設定されていないため、ページを表示するときに製品は表示されません。 このパラメーター値は、リピータでクリックしたカテゴリの `CategoryID` に基づいて設定する必要があります。 これには2つの課題があります。まず、リピータの `ItemTemplate` がクリックされたタイミングを判断する方法について説明します。次に、LinkButton がクリックされた対応するカテゴリの `CategoryID` を特定するにはどうすればよいでしょうか。

ボタンおよび ImageButton コントロールのような LinkButton には、`Click` イベントと[`Command` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)があります。 `Click` イベントは、LinkButton がクリックされたことを確認するために設計されています。 ただし、LinkButton がクリックされたことを示すだけでなく、イベントハンドラーに追加情報を渡す必要もあります。 この場合、LinkButton [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx)と[`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx)のプロパティにこの追加情報を割り当てることができます。 次に、LinkButton がクリックされると、その `Command` イベント (`Click` イベントではなく) が発生し、イベントハンドラーに `CommandName` および `CommandArgument` プロパティの値が渡されます。

リピータ内のテンプレート内から `Command` イベントが発生すると、Repeater s [`ItemCommand` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx)が発生し、クリックされた LinkButton (またはボタンまたは ImageButton) の `CommandName` と `CommandArgument` の値が渡されます。 そのため、リピータのカテゴリ LinkButton がクリックされたことを確認するには、次の手順を実行する必要があります。

1. Repeater の `ItemTemplate` にある LinkButton の `CommandName` プロパティを、何らかの値に設定します (ListProducts を使用しました)。 この `CommandName` 値を設定すると、linkbutton がクリックされたときに LinkButton `Command` イベントが発生します。
2. LinkButton s `CommandArgument` プロパティを、現在の項目の `CategoryID`の値に設定します。
3. Repeater s `ItemCommand` イベントのイベントハンドラーを作成します。 イベントハンドラーで、`CategoryProductsDataSource` ObjectDataSource s `CategoryID` パラメーターを、渡された `CommandArgument`の値に設定します。

次の `ItemTemplate` のカテゴリリピータのマークアップは、手順 1. と 2. を実装しています。 Databinding 構文を使用して、データ項目 `CategoryID` に `CommandArgument` 値が割り当てられていることに注意してください。

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample11.aspx)]

`ItemCommand` イベントハンドラーを作成する場合は常に、必ず最初に受信 `CommandName` 値を確認することをお勧めします *。これは、Repeater*内の Button、LinkButton、または ImageButton によって発生した `Command`*イベントによっ*て `ItemCommand` イベントが発生するためです。 現在、このような LinkButton は1つしかありませんが、将来 (またはチームの他の開発者) は、Repeater にボタン Web コントロールを追加することがあります。これは、クリックすると同じ `ItemCommand` イベントハンドラーを生成します。 したがって、常に `CommandName` プロパティをチェックし、予想される値に一致する場合にのみプログラムロジックを続行することをお勧めします。

渡された `CommandName` 値が ListProducts と等しいことを確認した後、イベントハンドラーは、渡された `CommandArgument`の値に `CategoryProductsDataSource` ObjectDataSource s `CategoryID` パラメーターを割り当てます。 ObjectDataSource s `SelectParameters` に対するこの変更により、自動的に DataList が自動的にデータソースに再バインドされ、新しく選択したカテゴリの製品が表示されます。

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample12.vb)]

これらの追加により、チュートリアルは完了です。 ブラウザーでテストしてみましょう。 図14に、最初にページにアクセスしたときの画面を示します。 カテゴリはまだ選択されていないため、製品は表示されません。 [生成] などのカテゴリをクリックすると、それらの製品が2列ビューで製品カテゴリに表示されます (図15を参照)。

[ページに最初にアクセスしたときに製品が表示されない ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image38.png)

**図 14**: 最初にページにアクセスしたときに製品が表示されない ([クリックしてフルサイズの画像を表示する](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image40.png))

[[生成] カテゴリをクリック ![と、一致する製品が右側に表示されます](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image41.png)

**図 15**: [生成] カテゴリをクリックすると、一致する製品が右側に表示されます ([クリックすると、フルサイズの画像が表示](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image43.png)されます)

## <a name="summary"></a>まとめ

このチュートリアルと前に説明したように、マスター/詳細レポートは、2つのページ間で分散することも、1つに統合することもできます。 ただし、マスター/詳細レポートを1ページに表示する場合は、ページ上のマスターレコードと詳細レコードのレイアウトを最適化するためのいくつかの課題が生じます。 詳細な DetailsView チュートリアルがある*選択可能なマスター GridView を使用したマスター/詳細*では、マスターレコードの上に詳細レコードが表示されていました。このチュートリアルでは、CSS の手法を使用して、マスターレコードを詳細の左側にフローティングしました。

マスター/詳細レポートの表示と共に、各カテゴリに関連付けられている製品の数を取得する方法に加えて、LinkButton (またはボタンまたは ImageButton) がリピータ内からクリックされたときにサーバー側のロジックを実行する方法についても説明しました。

このチュートリアルでは、DataList と Repeater を使用したマスター/詳細レポートの検査を完了します。 次の一連のチュートリアルでは、DataList コントロールに編集機能と削除機能を追加する方法について説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- CSS を使用したフローティング CSS 要素に関するチュートリアルの[Floatutorial](http://css.maxdesign.com.au/floatutorial/)
- [Css で](http://www.brainjar.com/css/positioning/)の要素の配置の詳細については、「css」を参照してください。
- `<table>` s とその他の HTML 要素を使用して配置するための[html を使用したコンテンツのレイアウト](http://www.w3schools.com/html/html_layout.asp)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Zack Jones でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](master-detail-filtering-acess-two-pages-datalist-vb.md)
