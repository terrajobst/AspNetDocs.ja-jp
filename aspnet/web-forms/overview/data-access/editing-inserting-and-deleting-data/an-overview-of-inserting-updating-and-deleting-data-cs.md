---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
title: データの挿入、更新、および削除の概要 (C#) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ObjectDataSource の Insert ()、Update ()、Delete () の各メソッドを BLL クラスのメソッドにマップする方法と、その方法について説明します。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: b651dc58-93c7-4f83-a74e-3b99f6d60848
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e26b8e841f86272a158b0c09b62ab2790d01d191
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479362"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-c"></a>データの挿入、更新、および削除の概要 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_CS.exe)または[PDF のダウンロード](an-overview-of-inserting-updating-and-deleting-data-cs/_static/datatutorial16cs1.pdf)

> このチュートリアルでは、ObjectDataSource の Insert ()、Update ()、Delete () の各メソッドを、BLL クラスのメソッドにマップする方法と、GridView、DetailsView、および FormView コントロールを構成してデータ変更機能を提供する方法について説明します。

## <a name="introduction"></a>はじめに

これまでのいくつかのチュートリアルでは、GridView、DetailsView、FormView コントロールを使用して ASP.NET ページにデータを表示する方法を説明しました。 これらのコントロールは、指定されたデータを操作するだけです。 一般的に、これらのコントロールは、ObjectDataSource などのデータソースコントロールを使用してデータにアクセスします。 ObjectDataSource が、ASP.NET ページと基になるデータの間のプロキシとしてどのように機能するかを見てきました。 GridView でデータを表示する必要がある場合は、ObjectDataSource の `Select()` メソッドを呼び出します。このメソッドは、適切なデータアクセス層 (DAL) TableAdapter のメソッドを呼び出し、さらに Northwind データベースに `SELECT` クエリを送信する、ビジネスロジック層 (BLL) からメソッドを呼び出します。

[最初のチュートリアル](../introduction/creating-a-data-access-layer-cs.md)では、DAL で tableadapter を作成したときに、基になるデータベーステーブルのデータの挿入、更新、および削除を行うためのメソッドが Visual Studio によって自動的に追加されたことを思い出してください。 さらに、[ビジネスロジック層を作成する際](../introduction/creating-a-business-logic-layer-cs.md)に、これらのデータ変更 DAL メソッドに呼び出される BLL のメソッドを設計しました。

`Select()` メソッドに加えて、ObjectDataSource には、`Insert()`、`Update()`、および `Delete()` メソッドもあります。 `Select()` メソッドと同様に、これら3つのメソッドは、基になるオブジェクトのメソッドにマップできます。 データの挿入、更新、または削除を行うように構成した場合、GridView、DetailsView、および FormView コントロールには、基になるデータを変更するためのユーザーインターフェイスが用意されています。 このユーザーインターフェイスは、ObjectDataSource の `Insert()`、`Update()`、および `Delete()` メソッドを呼び出します。このメソッドは、基になるオブジェクトの関連付けられたメソッドを呼び出します (図1を参照)。

[ObjectDataSource の Insert ()、Update ()、Delete () の各メソッドが、BLL にプロキシとして機能する ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image1.png)

**図 1**: ObjectDataSource の `Insert()`、`Update()`、および `Delete()` メソッドは、BLL にプロキシとして機能します ([クリックすると、フルサイズのイメージが表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image3.png)されます)。

このチュートリアルでは、ObjectDataSource の `Insert()`、`Update()`、および `Delete()` メソッドを BLL のクラスのメソッドにマップする方法と、GridView、DetailsView、および FormView コントロールを構成してデータ変更機能を提供する方法について説明します。

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>手順 1: 挿入、更新、および削除のチュートリアル Web ページの作成

データの挿入、更新、削除の方法を確認する前に、まず、このチュートリアルに必要な ASP.NET ページを web サイトプロジェクトに作成し、次のいくつかの作業を行います。 まず、`EditInsertDelete`という名前の新しいフォルダーを追加します。 次に、次の ASP.NET ページをそのフォルダーに追加します。各ページは `Site.master` マスターページに関連付けられていることを確認してください。

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![データ変更関連のチュートリアルの ASP.NET ページを追加する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image4.png)

**図 2**: データ変更に関連するチュートリアルの ASP.NET ページを追加する

他のフォルダーと同様に、`EditInsertDelete` フォルダー内の `Default.aspx` には、そのセクションのチュートリアルが一覧表示されます。 `SectionLevelTutorialListing.ascx` ユーザーコントロールがこの機能を提供していることを思い出してください。 そのため、ソリューションエクスプローラーからページのデザインビューにドラッグして、このユーザーコントロールを `Default.aspx` に追加します。

[SectionLevelTutorialListing ユーザーコントロールを default.aspx に追加 ![には](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image5.png)

**図 3**: `Default.aspx` に `SectionLevelTutorialListing.ascx` ユーザーコントロールを追加する ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image7.png)されます)

最後に、`Web.sitemap` ファイルにエントリとしてページを追加します。 具体的には、カスタマイズされた書式設定 `<siteMapNode>`後に、次のマークアップを追加します。

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample1.xml)]

`Web.sitemap`を更新した後、ブラウザーを使用してチュートリアル web サイトを表示します。 左側のメニューには、チュートリアルの編集、挿入、および削除を行うための項目が含まれています。

![サイトマップに、チュートリアルの編集、挿入、および削除のエントリが含まれるようになりました。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image8.png)

**図 4**: サイトマップに、チュートリアルの編集、挿入、および削除のエントリが含まれるようになりました。

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>手順 2: ObjectDataSource コントロールの追加と構成

GridView、DetailsView、および FormView はそれぞれデータ変更機能とレイアウトが異なるため、それぞれを個別に調べてみましょう。 ただし、各コントロールで独自の ObjectDataSource を使用するのではなく、3つのコントロールの例すべてで共有できる単一の ObjectDataSource を作成しましょう。

`Basics.aspx` ページを開き、ObjectDataSource をツールボックスからデザイナーにドラッグし、そのスマートタグから [データソースの構成] リンクをクリックします。 `ProductsBLL` は、編集、挿入、および削除メソッドを提供する唯一の BLL クラスであるため、このクラスを使用するように ObjectDataSource を構成します。

[製品の Bll クラスを使用するように ObjectDataSource を構成 ![には](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image9.png)

**図 5**: `ProductsBLL` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image11.png))

次の画面では、適切なタブを選択し、ドロップダウンリストからメソッドを選択することにより、`ProductsBLL` クラスのメソッドを ObjectDataSource の `Select()`、`Insert()`、`Update()`、および `Delete()` にどのようにマップするかを指定できます。 図6は今ではよく見られるはずですが、ObjectDataSource の `Select()` メソッドを `ProductsBLL` クラスの `GetProducts()` メソッドにマップします。 `Insert()`、`Update()`、および `Delete()` の各メソッドを構成するには、上部にある一覧から適切なタブを選択します。

[ObjectDataSource がすべての製品を返す ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image12.png)

**図 6**: ObjectDataSource によってすべての製品が返されるよう[にする (クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image14.png)されます)

図7、8、および9は、ObjectDataSource の [更新] タブ、[挿入] タブ、および [削除] タブを示しています。 これらのタブを構成して、`Insert()`、`Update()`、および `Delete()` メソッドが、それぞれ `ProductsBLL` クラスの `UpdateProduct`、`AddProduct`、および `DeleteProduct` メソッドを呼び出すようにします。

[ObjectDataSource の Update () メソッドを ProductBLL クラスの UpdateProduct メソッドにマップ ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image15.png)

**図 7**: ObjectDataSource の `Update()` メソッドを `ProductBLL` クラスの `UpdateProduct` メソッドにマップする ([クリックしてフルサイズのイメージを表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image17.png))

[ObjectDataSource の Insert () メソッドを ProductBLL クラスの AddProduct メソッドにマップ ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image18.png)

**図 8**: ObjectDataSource の `Insert()` メソッドを `ProductBLL` クラスの Add `Product` メソッドにマップする ([クリックしてフルサイズのイメージを表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image20.png))

[ObjectDataSource の Delete () メソッドを ProductBLL クラスの DeleteProduct メソッドにマップ ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image21.png)

**図 9**: ObjectDataSource の `Delete()` メソッドを `ProductBLL` クラスの `DeleteProduct` メソッドにマップする ([クリックしてフルサイズのイメージを表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image23.png))

[更新]、[挿入]、[削除] の各タブのドロップダウンリストには、これらのメソッドが既に選択されています。 これは、`ProductsBLL`のメソッドを装飾する `DataObjectMethodAttribute` を使用したことによるものです。 たとえば、DeleteProduct メソッドには次のシグネチャがあります。

[!code-csharp[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample2.cs)]

`DataObjectMethodAttribute` 属性は、選択、挿入、更新、または削除の各メソッドの目的を示し、既定値であるかどうかを示します。 BLL クラスの作成時にこれらの属性を省略した場合は、[更新]、[挿入]、[削除] の各タブからメソッドを手動で選択する必要があります。

適切な `ProductsBLL` メソッドが ObjectDataSource の `Insert()`、`Update()`、および `Delete()` の各メソッドにマップされていることを確認したら、[完了] をクリックしてウィザードを完了します。

## <a name="examining-the-objectdatasources-markup"></a>ObjectDataSource のマークアップを調べる

ウィザードを使用して ObjectDataSource を構成した後、ソースビューにアクセスして、生成された宣言マークアップを確認します。 `<asp:ObjectDataSource>` タグは、基になるオブジェクトと呼び出すメソッドを指定します。 さらに、`ProductsBLL` クラスの `AddProduct`、`UpdateProduct`、および `DeleteProduct` メソッドの入力パラメーターにマップされる `DeleteParameters`、`UpdateParameters`、および `InsertParameters` があります。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample3.aspx)]

ObjectDataSource には、関連付けられているメソッドの各入力パラメーターのパラメーターが含まれています。これは、ObjectDataSource が、入力パラメーター (`GetProductsByCategoryID(categoryID)`など) を必要とする select メソッドを呼び出すように構成されている場合に、`SelectParameter` のリストと同様に存在します。 後で説明するように、これらの `DeleteParameters`、`UpdateParameters`、および `InsertParameters` の値は、ObjectDataSource の `Insert()`、`Update()`、または `Delete()` メソッドを呼び出す前に、GridView、DetailsView、および FormView によって自動的に設定されます。 これらの値は、後のチュートリアルで説明するように、必要に応じてプログラムで設定することもできます。

ウィザードを使用して ObjectDataSource に構成する副作用の1つは、Visual Studio が[Oldvaluesparameterformatstring プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx)を `original_{0}`に設定することです。 このプロパティ値は、編集中のデータの元の値を含めるために使用され、次の2つのシナリオで役立ちます。

- レコードを編集するときに、ユーザーは主キーの値を変更できます。 この場合、元の主キー値を持つレコードが見つかり、それに応じて値が更新されるように、新しい主キー値と元の主キー値の両方を指定する必要があります。
- オプティミスティック同時実行制御を使用する場合。 オプティミスティック同時実行制御は、2人のユーザーが互いの変更を上書きしないようにするための手法であり、今後のチュートリアルのトピックです。

`OldValuesParameterFormatString` プロパティは、元の値の基になるオブジェクトの update メソッドと delete メソッドの入力パラメーターの名前を示します。 オプティミスティック同時実行制御の詳細については、このプロパティとその目的について詳しく説明します。 ただし、BLL のメソッドは元の値を予期していないため、このプロパティを削除することが重要です。 `OldValuesParameterFormatString` プロパティを既定値 (`{0}`) 以外に設定したままにすると、ObjectDataSource は、指定された `UpdateParameters` または `DeleteParameters` と元の値のパラメーターの両方を渡そうとするため、ObjectDataSource の `Update()` または `Delete()` メソッドを呼び出そうとするとエラーが発生します。

この時点ではそれほど明確でない場合は、今後のチュートリアルでこのプロパティとユーティリティを確認します。 ここでは、このプロパティの宣言を宣言構文から完全に削除するか、値を既定値 ({0}) に設定するだけであることを確認してください。

> [!NOTE]
> デザインビューのプロパティウィンドウから `OldValuesParameterFormatString` プロパティ値をクリアするだけの場合、プロパティは宣言構文に存在しますが、空の文字列に設定されます。 残念ながら、これまでに説明したのと同じ問題が発生します。 したがって、宣言構文からプロパティを完全に削除するか、プロパティウィンドウから、値を既定の `{0}`に設定します。

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>手順 3: データ Web コントロールを追加し、データ変更用に構成する

ObjectDataSource がページに追加され、構成されたら、データを表示するためのページにデータ Web コントロールを追加し、エンドユーザーがデータを変更するための手段を提供できるようになります。 これらのデータ Web コントロールはデータ変更機能と構成が異なるため、GridView、DetailsView、FormView を個別に見ていきます。

この記事の残りの部分で説明するように、GridView、DetailsView、および FormView コントロールを使用した基本的な編集、挿入、および削除のサポートの追加は、いくつかのチェックボックスをオンにするだけで簡単に行うことができます。 実際の世界には、ポイントアンドクリックだけでなく、このような機能を提供するという、多くの微妙な要素とエッジケースがあります。 ただし、このチュートリアルでは、単純データ変更機能の提供にのみ焦点を当てています。 今後のチュートリアルでは、現実世界の設定で発生する可能性がある問題を調査します。

## <a name="deleting-data-from-the-gridview"></a>GridView からのデータの削除

まず、GridView をツールボックスからデザイナーにドラッグします。 次に、gridview のスマートタグのドロップダウンリストから ObjectDataSource を選択して、その ObjectDataSource を GridView にバインドします。 この時点で、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample4.aspx)]

そのスマートタグを通じて、GridView を ObjectDataSource にバインドすると、次の2つの利点があります。

- BoundFields と CheckBoxFields は、ObjectDataSource によって返される各フィールドに対して自動的に作成されます。 さらに、BoundField プロパティと CheckBoxField プロパティは、基になるフィールドのメタデータに基づいて設定されます。 たとえば、`ProductID`、`CategoryName`、および `SupplierName` フィールドは `ProductsDataTable` で読み取り専用としてマークされているので、編集時に更新できないようにします。 これに対応するために、これらの BoundFields の[ReadOnly プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx)は `true`に設定されます。
- [いる datakeynames プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx)は、基になるオブジェクトの主キーフィールドに割り当てられます。 これは、データを編集または削除するために GridView を使用する場合に不可欠です。このプロパティは、一意に各レコードを識別するフィールド (またはフィールドのセット) を示します。 `DataKeyNames` プロパティの詳細については、「詳細情報ビューを使用し[た選択可能なマスター GridView を使用したマスター/詳細](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)」を参照してください。

GridView はプロパティウィンドウまたは宣言型の構文を通じて ObjectDataSource にバインドできますが、そのためには、適切な BoundField および `DataKeyNames` マークアップを手動で追加する必要があります。

GridView コントロールには、行レベルの編集と削除のサポートが組み込まれています。 構成の削除をサポートするために GridView 列の削除ボタンを追加します。 エンドユーザーは、特定の行の削除ボタンをクリックすると、ポストバックに陥ります、GridView は、次の手順を実行します。

1. ObjectDataSource の `DeleteParameters` 値が割り当てられています
2. ObjectDataSource の `Delete()` メソッドが呼び出され、指定されたレコードが削除されます。
3. GridView は、`Select()` メソッドを呼び出すことによって、それ自体を ObjectDataSource に再バインドします。

`DeleteParameters` に割り当てられた値は、[削除] ボタンがクリックされた行の `DataKeyNames` フィールドの値です。 そのため、GridView の `DataKeyNames` プロパティを正しく設定することが重要です。 存在しない場合は、手順 1. で `DeleteParameters` に `null` 値が割り当てられます。これにより、手順2で削除されたレコードが生成されることはありません。

> [!NOTE]
> `DataKeys` コレクションは GridView s コントロール状態に格納されます。つまり、GridView のビューステートが無効になっている場合でも、ポストバック全体で `DataKeys` 値が記憶されます。 ただし、編集または削除 (既定の動作) をサポートする GridViews では、ビューステートが有効なままであることが非常に重要です。 GridView の `EnableViewState` プロパティを `false`に設定した場合、編集と削除の動作は1人のユーザーに対して正常に機能しますが、同時実行ユーザーがデータを削除している場合は、これらの同時実行ユーザーが意図していないレコードを誤って削除または編集する可能性があります。 詳細については、「マイブログの記事、[警告: 編集や削除をサポートし、ビューステートが無効になっている ASP.NET 2.0 GridViews/DetailsView/formviews での同時実行の問題](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx)」を参照してください。

この警告は、[表示] ビューおよび [フォーム] ビューにも当てはまります。

GridView に削除機能を追加するには、単にそのスマートタグにアクセスし、[削除を有効にする] チェックボックスをオンにします。

![有効にするチェック ボックスを削除するを確認してください。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image24.png)

**図 10**: [削除を有効にする] チェックボックスをオンにする

スマートタグから [削除を有効にする] チェックボックスをオンにすると、GridView に CommandField が追加されます。 CommandField は、GridView の列に、レコードの選択、レコードの編集、レコードの削除という1つ以上のタスクを実行するためのボタンを表示します。 前に、[詳細詳細ビューのチュートリアルで選択可能なマスター GridView を使用して、マスター/詳細](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)でレコードを選択する操作の commandfield を確認しました。

CommandField には、CommandField に表示される一連のボタンを示す `ShowXButton` のプロパティが多数含まれています。 [削除を有効にする] チェックボックスをオンにすると、`ShowDeleteButton` プロパティが `true` である CommandField が GridView の Columns コレクションに追加されます。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample5.aspx)]

信じられないかもしれませんが、GridView に削除サポートを追加しています。 図 11 に示すようとブラウザーの削除ボタンの列からこのページにアクセスが存在します。

[CommandField ![Delete ボタンの列が追加されます。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image25.png)

**図 11**: Commandfield に Delete ボタンの列が追加される ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image27.png)されます)

このチュートリアルを独自に作成したことがある場合は、このページをテストするときに、[削除] ボタンをクリックすると例外が発生します。 これらの例外が発生した理由とその修正方法については、「」を参照してください。

> [!NOTE]
> このチュートリアルに付属しているダウンロードを使用している場合は、これらの問題は既に記載されています。 ただし、以下に示す詳細を読んで、発生する可能性のある問題と適切な回避策を特定することをお勧めします。

製品を削除しようとしたときに、メッセージが "Objectdatasource ' ObjectDataSource1 ' に類似しているという例外が発生した場合は、*パラメーター: productid、original\_productid*、" objectdatasource から `OldValuesParameterFormatString` プロパティを削除し忘れた可能性があります。 `OldValuesParameterFormatString` プロパティが指定されている場合、ObjectDataSource は、`productID` と `original_ProductID` 入力パラメーターの両方を `DeleteProduct` メソッドに渡すことを試みます。 ただし `DeleteProduct`では、1つの入力パラメーターのみを受け入れるため、例外が発生します。 `OldValuesParameterFormatString` プロパティを削除する (またはそれを `{0}`に設定する) 場合、ObjectDataSource は元の入力パラメーターを渡さないように指示します。

[OldValuesParameterFormatString プロパティがクリアされていることを ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image28.png)

**図 12**: `OldValuesParameterFormatString` プロパティがクリアされていることを確認[する (クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image30.png)されます)

`OldValuesParameterFormatString` プロパティを削除した場合でも、次のようなメッセージで製品を削除しようとすると例外が発生します。 "*delete ステートメントは、参照制約 ' FK\_Order\_Details\_Products ' と競合*しています。Northwind データベースには、`Order Details` と `Products` テーブル間の外部キー制約が含まれています。つまり、`Order Details` テーブルに1つ以上のレコードがある場合、製品をシステムから削除することはできません。 Northwind データベースのすべての製品には `Order Details`に少なくとも1つのレコードがあるため、製品に関連付けられている注文明細レコードを最初に削除するまで、製品を削除することはできません。

[外部キー制約を ![と、製品の削除が禁止されます。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image31.png)

**図 13**: 外部キー制約によって製品の削除が禁止される ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image33.png)されます)

このチュートリアルでは、`Order Details` テーブルからすべてのレコードを削除してみましょう。 実際のアプリケーションでは、次のいずれかを行う必要があります。

- 注文の詳細情報を管理する別の画面を用意する
- 指定された製品の注文の詳細を削除するロジックを含めるように `DeleteProduct` メソッドを強化します。
- 指定された製品の注文の詳細の削除を含むように、TableAdapter によって使用される SQL クエリを変更します。

`Order Details` テーブルからすべてのレコードを削除して、foreign key 制約を回避してみましょう。 Visual Studio のサーバーエクスプローラーにアクセスし、[`NORTHWND.MDF`] ノードを右クリックして、[新しいクエリ] を選択します。 次に、クエリウィンドウで、次の SQL ステートメントを実行します。 `DELETE FROM [Order Details]`

[Order Details テーブルからすべてのレコードを削除 ![には](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image34.png)

**図 14**: `Order Details` テーブルからすべてのレコードを削除[する (クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image36.png)されます)

`Order Details` テーブルをクリアした後、[削除] ボタンをクリックすると、エラーが発生することなく製品が削除されます。 [削除] ボタンをクリックしても製品が削除されない場合は、GridView の `DataKeyNames` プロパティが主キーフィールド (`ProductID`) に設定されていることを確認します。

> [!NOTE]
> [削除] ボタンをクリックすると、ポストバック ensues とレコードが削除されます。 間違った行の [削除] ボタンを誤ってクリックすることは簡単であるため、これは危険になる可能性があります。 今後のチュートリアルでは、レコードの削除時にクライアント側の確認を追加する方法について説明します。

## <a name="editing-data-with-the-gridview"></a>GridView を使用したデータの編集

GridView コントロールでは、削除と共に、組み込みの行レベルの編集もサポートされています。 編集をサポートするように GridView を構成すると、編集ボタンの列が追加されます。 エンドユーザーの観点からは、行の [編集] ボタンをクリックすると、その行が編集可能になり、既存の値を含むテキストボックスにセルを変換し、[編集] ボタンを [更新] ボタンと [キャンセル] ボタンに置き換えます。 必要な変更を行った後、エンドユーザーは [更新] ボタンをクリックして変更をコミットするか、[キャンセル] ボタンをクリックして変更を破棄することができます。 どちらの場合も、[更新] または [キャンセル] をクリックすると、GridView は編集前の状態に戻ります。

ページ開発者としての観点から、エンドユーザーが特定の行の [編集] ボタンをクリックすると、ポストバック ensues と GridView によって次の手順が実行されます。

1. GridView の `EditItemIndex` プロパティは、編集ボタンがクリックされた行のインデックスに割り当てられます。
2. GridView は、`Select()` メソッドを呼び出すことによって、それ自体を ObjectDataSource に再バインドします。
3. `EditItemIndex` に一致する行インデックスは、"編集モード" で表示されます。 このモードでは、[編集] ボタンは、[更新] ボタンと [キャンセル] ボタン、および `ReadOnly` プロパティが False (既定値) になっている連結フィールドに置き換えられ、`Text` のプロパティがデータフィールドの値に割り当てられます。

この時点で、マークアップがブラウザーに返され、エンドユーザーは行のデータに変更を加えることができます。 ユーザーが [更新] ボタンをクリックすると、ポストバックが発生し、GridView は次の手順を実行します。

1. ObjectDataSource の `UpdateParameters` 値には、エンドユーザーが GridView の編集インターフェイスに入力した値が割り当てられます。
2. ObjectDataSource の `Update()` メソッドが呼び出され、指定されたレコードを更新しています
3. GridView は、`Select()` メソッドを呼び出すことによって、それ自体を ObjectDataSource に再バインドします。

手順 1. で `UpdateParameters` に割り当てられた主キー値は、`DataKeyNames` プロパティで指定された値から取得されますが、非主キー値は、編集された行のテキストボックス Web コントロールのテキストから取得されます。 削除と同様に、GridView の `DataKeyNames` プロパティを正しく設定することが重要です。 存在しない場合は、手順 1. で `UpdateParameters` 主キーの値に `null` 値が割り当てられます。これにより、手順 2. で更新されたレコードは生成されません。

編集機能は、GridView のスマートタグの [編集を有効にする] チェックボックスをオンにするだけでアクティブにすることができます。

![[編集を有効にする] チェックボックスをオンにします。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image37.png)

**図 15**: [編集を有効にする] チェックボックスをオンにする

[編集を有効にする] チェックボックスをオンにすると、必要に応じて CommandField が追加され、その `ShowEditButton` プロパティが `true`に設定されます。 前に説明したように、commandfield には、CommandField に表示される一連のボタンを示す `ShowXButton` のプロパティが多数含まれています。 [編集を有効にする] チェックボックスをオンにすると、既存の CommandField に `ShowEditButton` プロパティが追加されます。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample6.aspx)]

基本的な編集サポートを追加するだけです。 Figure16 が示すように、編集インターフェイスは、`ReadOnly` プロパティが `false` (既定) に設定されている各 BoundField をテキストボックスとしてレンダリングします。 これには、他のテーブルに対するキーである `CategoryID` や `SupplierID`などのフィールドが含まれます。

[[Chai s Edit] ボタンをクリック ![と、その行が編集モードで表示されます。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image38.png)

**図 16**: [Chai s] 編集ボタンをクリックすると、編集モードで行が表示されます ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image40.png)されます)

外部キーの値を直接編集するようにユーザーに依頼するだけでなく、編集インターフェイスのインターフェイスには次のような意味がありません。

- データベースに存在しない `CategoryID` または `SupplierID` をユーザーが入力すると、`UPDATE` は foreign key 制約に違反し、例外が発生します。
- 編集インターフェイスには検証が含まれていません。 必要な値 (`ProductName`など) が指定されていない場合、または数値が求められる文字列値を入力する場合 ("多すぎる場合" など)。 [`UnitPrice`] ボックスに、例外がスローされます。 今後のチュートリアルでは、編集中のユーザーインターフェイスに検証コントロールを追加する方法を確認します。
- 現時点では、読み取り専用ではない*すべて*の製品フィールドを GridView に含める必要があります。 GridView からフィールドを削除すると `UnitPrice`、データを更新するときに、GridView によって `UnitPrice` `UpdateParameters` 値が設定されません。これにより、データベースレコードの `UnitPrice` が `NULL` 値に変更されます。 同様に、`ProductName`などの必須フィールドが GridView から削除された場合、更新は失敗し、前述の "*Column ' ProductName ' では null が許可されません*" という例外が表示されます。
- 編集インターフェイスの書式設定は、必要に応じて大きくなります。 `UnitPrice` は、4つの小数点を使用して表示されます。 `CategoryID` と `SupplierID` の値には、システム内のカテゴリとサプライヤーを一覧表示する DropDownLists があることが理想的です。

ここでは、このような欠点がありますが、今後のチュートリアルで対処する予定です。

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>DetailsView を使用したデータの挿入、編集、および削除

前のチュートリアルで見たように、DetailsView コントロールでは一度に1つのレコードが表示され、GridView と同様に、現在表示されているレコードを編集および削除できます。 DetailsView の項目の編集と削除に関するエンドユーザーの経験と、ASP.NET 側からのワークフローの両方が、GridView の項目と同じです。 DetailsView と GridView の違いは、組み込みの挿入サポートも用意されていることです。

GridView のデータ変更機能をデモンストレーションするには、まず、既存の GridView の上にある `Basics.aspx` ページに DetailsView を追加し、DetailsView のスマートタグを使用して既存の ObjectDataSource にバインドします。 次に、DetailsView の `Height` と `Width` プロパティを消去し、スマートタグの [ページングを有効にする] オプションをオンにします。 編集、挿入、および削除のサポートを有効にするには、[編集を有効にする]、[挿入を有効にする]、および [スマートタグの削除] チェックボックスをオンにするだけです。

![編集、挿入、および削除をサポートするように DetailsView を構成する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image41.png)

**図 17**: 編集、挿入、および削除をサポートするように DetailsView を構成する

GridView と同様に、編集、挿入、または削除のサポートを追加すると、次の宣言構文に示すように CommandField が DetailsView に追加されます。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample7.aspx)]

DetailsView の場合は、既定で Columns コレクションの最後に CommandField が表示されることに注意してください。 DetailsView のフィールドは行として表示されるため、CommandField は、DetailsView の下部にある [挿入]、[編集]、および [削除] の各ボタンがある行として表示されます。

[編集、挿入、および削除をサポートするように DetailsView を構成 ![には](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image42.png)

**図 18**: DetailsView を構成して編集、挿入、および削除をサポートする ([クリックしてフルサイズのイメージを表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image44.png))

[削除] ボタンをクリックすると、GridView: ポストバックと同じイベントのシーケンスが開始されます。その後に、`DataKeyNames` 値に基づいて ObjectDataSource の `DeleteParameters` を設定する DetailsView が続きます。とは、ObjectDataSource の `Delete()` メソッドを呼び出すことによって完了します。これにより、実際には、データベースから製品が削除されます。 DetailsView での編集は、GridView の場合と同じ方法でも機能します。

挿入の場合、エンドユーザーには新しいボタンが表示され、クリックすると、"挿入モード" で DetailsView がレンダリングされます。 "挿入モード" では、新しいボタンは [挿入] ボタンと [キャンセル] ボタンに置き換えられ、`InsertVisible` プロパティが `true` (既定) に設定されている連結フィールドのみが表示されます。 `ProductID`などの自動インクリメントフィールドとして識別されたこれらのデータフィールドの[Insertvisible プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx)は、スマートタグを介してデータソースに DetailsView をバインドするときに `false` に設定されます。

スマートタグを使用してデータソースを DetailsView にバインドすると、Visual Studio は、自動インクリメントフィールドに対してのみ、`InsertVisible` プロパティを `false` に設定します。 `CategoryName` や `SupplierName`などの読み取り専用フィールドは、`InsertVisible` プロパティが明示的に `false`に設定されていない限り、"挿入モード" ユーザーインターフェイスに表示されます。 この2つのフィールドの `InsertVisible` プロパティを `false`に設定します。そのためには、DetailsView の宣言構文を使用するか、スマートタグ内の [フィールドの編集] リンクを使用します。 図19は、[フィールドの編集] リンクをクリックして `false` する `InsertVisible` のプロパティを設定する方法を示しています。

[Northwind Traders ![では、Acme 紅茶を提供](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image45.png)

**図 19**: Northwind Traders が Acme 茶を提供するようになりました ([クリックしてフルサイズの画像を表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image47.png))

`InsertVisible` のプロパティを設定した後、ブラウザーで `Basics.aspx` ページを表示し、[新規] ボタンをクリックします。 図20に、新しい飲み物 (Acme 茶) を製品ラインに追加する場合の DetailsView を示します。

[Northwind Traders ![では、Acme 紅茶を提供](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image48.png)

**図 20**: Northwind Traders が Acme 茶を提供するようになりました ([クリックしてフルサイズの画像を表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image50.png))

Acme 紅茶の詳細を入力し、[挿入] ボタンをクリックすると、ポストバック ensues と新しいレコードが `Products` データベーステーブルに追加されます。 この DetailsView はデータベーステーブル内に存在する順に製品を一覧表示しているため、新しい製品を表示するには、最後の製品にページを表示する必要があります。

[Acme 茶の ![の詳細](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image51.png)

**図 21**: Acme 紅茶の詳細 ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image53.png)される)

> [!NOTE]
> DetailsView の[Currentmode プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx)は、表示されているインターフェイスを示します。 `Edit`、`Insert`、`ReadOnly`のいずれかの値を指定できます。 [Defaultmode プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx)は、編集または挿入が完了した後に detailsview が返すモードを示します。これは、編集モードまたは挿入モードで永続的に使用される detailsview を表示する場合に便利です。

ポイントとクリックによる DetailsView の挿入および編集機能は、GridView と同じ制限を受けません。ユーザーは、テキストボックスを使用して、既存の `CategoryID` と `SupplierID` 値を入力する必要があります。インターフェイスに検証ロジックがありません。`NULL` 値が許可されていないか、データベースレベルで既定値が指定されていないすべての product フィールドは、挿入インターフェイスに含める必要があります。

今後の記事で GridView の編集インターフェイスを拡張および強化するために検討する手法は、DetailsView コントロールの編集および挿入インターフェイスにも適用できます。

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>より柔軟なデータ変更ユーザーインターフェイスに FormView を使用する

FormView には、データの挿入、編集、および削除のための組み込みサポートが用意されていますが、フィールドではなくテンプレートが使用されているので、データを提供するために GridView および DetailsView コントロールによって使用される BoundFields や CommandField を追加する場所はありません。変更インターフェイス。 代わりに、このインターフェイスでは、新しい項目を追加するとき、または既存の項目を編集するときにユーザー入力を収集するための Web コントロールを、適切なテンプレートに手動で追加する必要があります。 幸い、Visual Studio では、スマートタグのドロップダウンリストを使用してデータソースに FormView をバインドするときに、必要なインターフェイスが自動的に作成されます。

これらの手法を説明するために、まず、FormView を `Basics.aspx` ページに追加し、FormView のスマートタグから、既に作成されている ObjectDataSource にバインドします。 これにより、[新規]、[編集]、[削除]、[挿入]、[更新]、および [キャンセル] の各ボタンのユーザーの入力およびボタン Web コントロールを収集するための、TextBox Web コントロールを含む FormView の `EditItemTemplate`、`InsertItemTemplate`、および `ItemTemplate` が生成されます。 さらに、FormView の `DataKeyNames` プロパティは、ObjectDataSource によって返されるオブジェクトの主キーフィールド (`ProductID`) に設定されます。 最後に、FormView のスマートタグの [ページングを有効にする] オプションをオンにします。

FormView が ObjectDataSource にバインドされた後の FormView の `ItemTemplate` の宣言型マークアップを次に示します。 既定では、各ブール値の product フィールドは、ラベル Web コントロールの `Text` プロパティにバインドされていますが、各ブール値フィールド (`Discontinued`) は、無効になっている CheckBox Web コントロールの `Checked` プロパティにバインドされています。 [新規]、[編集]、および [削除] の各ボタンをクリックしたときに特定の FormView 動作をトリガーするには、`CommandName` 値をそれぞれ `New`、`Edit`、および `Delete`に設定する必要があります。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample8.aspx)]

図22は、ブラウザーで表示したときに FormView の `ItemTemplate` を示しています。 各製品フィールドは、下部にある [新規]、[編集]、および [削除] の各ボタンと共に表示されます。

[既定 FormView ItemTemplate の ![[新規]、[編集]、および [削除] の各ボタンと共に各製品フィールドを一覧表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image54.png)

**図 22**: 既定 FormView `ItemTemplate` では、各 Product フィールドと、New、Edit、および Delete の各ボタンが一覧表示されます ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image56.png)されます)

GridView および DetailsView と同様に、[削除] ボタンをクリックするか、`CommandName` プロパティが [削除] に設定されているボタン、LinkButton、または ImageButton をクリックすると、ポストバックが発生し、FormView の `DataKeyNames` 値に基づいて ObjectDataSource の `DeleteParameters` が設定され、ObjectDataSource の `Delete()` メソッドが呼び出されます。

[編集] ボタンをクリックすると、ポストバック ensues が表示され、データが `EditItemTemplate`に再バインドされます。これは編集インターフェイスを表示する役割を担います。 このインターフェイスには、[更新] ボタンと [キャンセル] ボタンと共に、データを編集するための Web コントロールが含まれています。 Visual Studio によって生成される既定の `EditItemTemplate` には、自動インクリメントフィールド (`ProductID`) のラベル、非ブール値フィールドごとのテキストボックス、および各ブール値フィールドのチェックボックスが含まれています。 この動作は、GridView および DetailsView コントロールで自動生成された BoundFields によく似ています。

> [!NOTE]
> FormView の `EditItemTemplate` の自動生成に関する小さな問題の1つは、`CategoryName` や `SupplierName`など、読み取り専用のフィールドに対してテキストボックス Web コントロールをレンダリングすることです。 これについては、後で説明します。

`EditItemTemplate` のテキストボックスコントロールには、*双方向*のデータバインディングを使用して、対応するデータフィールドの値にバインドされた `Text` プロパティがあります。 `<%# Bind("dataField") %>`によって示される双方向のデータバインディングでは、データをテンプレートにバインドするときと、レコードを挿入または編集するために ObjectDataSource のパラメーターを設定するときの両方で、データバインドが実行されます。 つまり、ユーザーが `ItemTemplate`の [編集] ボタンをクリックすると、`Bind()` メソッドは、指定されたデータフィールドの値を返します。 ユーザーが変更を行って [更新] をクリックすると、`Bind()` を使用して指定されたデータフィールドに対応するポストバックされた値が ObjectDataSource の `UpdateParameters`に適用されます。 または、`<%# Eval("dataField") %>`で示される一方向のデータバインディングでは、データをテンプレートにバインドするときにデータフィールドの値のみを取得し、ポストバック時にデータソースのパラメーターにユーザーが入力した値を返し*ません*。

次の宣言型マークアップは、FormView の `EditItemTemplate`を示しています。 ここでは、`Bind()` メソッドが databinding 構文で使用されています。また、[更新] ボタンと [キャンセル] ボタンの Web コントロールの `CommandName` プロパティは、それに応じて設定されています。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample9.aspx)]

この時点で、`EditItemTemplate`を使用しようとすると、例外がスローされます。 問題は、`CategoryName` フィールドと `SupplierName` フィールドが、`EditItemTemplate`で TextBox Web コントロールとしてレンダリングされることです。 これらのテキストボックスをラベルに変更するか、完全に削除する必要があります。 単純に単に `EditItemTemplate`から削除してみましょう。

図23では、[編集] ボタンをクリックすると、ブラウザーに FormView が表示されます。 `ItemTemplate` に表示されている `SupplierName` フィールドと `CategoryName` フィールドは、`EditItemTemplate`から削除したばかりのものではなくなっています。 [更新] ボタンがクリックされると、FormView は GridView および DetailsView コントロールと同じ一連の手順を実行します。

[![既定では、EditItemTemplate は、各編集可能な Product フィールドをテキストボックスまたはチェックボックスとして表示します。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image57.png)

**図 23**: 既定では、`EditItemTemplate` は、編集可能な各製品フィールドをテキストボックスまたはチェックボックスとして表示します ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image59.png)されます)

[挿入] ボタンをクリックすると、FormView の `ItemTemplate` ポストバック ensues になります。 ただし、新しいレコードが追加されているため、FormView にデータがバインドされていません。 `InsertItemTemplate` インターフェイスには、[挿入] ボタンと [キャンセル] ボタンと共に新しいレコードを追加するための Web コントロールが含まれています。 Visual Studio によって生成される既定の `InsertItemTemplate` には、ブール値以外の各フィールドのテキストボックスと、自動生成された `EditItemTemplate`のインターフェイスと同様に、各ブール値フィールドのチェックボックスが含まれています。 TextBox コントロールの `Text` プロパティは、双方向のデータバインディングを使用して、対応するデータフィールドの値にバインドされます。

次の宣言型マークアップは、FormView の `InsertItemTemplate`を示しています。 ここでは、`Bind()` メソッドが databinding 構文で使用されています。また、[挿入] ボタンと [キャンセル] ボタンの Web コントロールには、それに応じて `CommandName` プロパティが設定されています。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample10.aspx)]

`InsertItemTemplate`の FormView の自動生成にははらみがあります。 具体的には、テキストボックス Web コントロールは、`CategoryName` や `SupplierName`など、読み取り専用のフィールドに対しても作成されます。 `EditItemTemplate`と同様に、これらのテキストボックスを `InsertItemTemplate`から削除する必要があります。

図24は、新しい製品である Acme コーヒーを追加するときの、ブラウザーの FormView を示しています。 `ItemTemplate` に表示されている `SupplierName` フィールドと `CategoryName` フィールドは、削除したばかりで存在しないことに注意してください。 [挿入] ボタンがクリックされると、FormView は、DetailsView コントロールと同じ一連の手順を実行し、`Products` テーブルに新しいレコードを追加します。 図25は、挿入された後の FormView での Acme コーヒー製品の詳細を示しています。

[Insertitemposition が FormView の挿入インターフェイスを決定する ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image60.png)

**図 24**: `InsertItemTemplate` は、FormView の挿入インターフェイスを決定します ([クリックすると、フルサイズの画像が表示](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image62.png)されます)

[新しい製品の詳細 ![Acme コーヒーが FormView に表示されます。](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image63.png)

**図 25**: 新しい製品である Acme コーヒーの詳細が FormView に表示される ([クリックしてフルサイズの画像を表示する](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image65.png))

この FormView では、読み取り専用、編集、および挿入の各インターフェイスを3つの個別のテンプレートに分割することで、これらのインターフェイスを DetailsView および GridView より細かく制御できます。

> [!NOTE]
> DetailsView と同様に、FormView の `CurrentMode` プロパティは、表示されているインターフェイスを示し、その `DefaultMode` プロパティは、編集または挿入の完了後に FormView が返すモードを示します。

## <a name="summary"></a>まとめ

このチュートリアルでは、GridView、DetailsView、および FormView を使用したデータの挿入、編集、および削除の基本について説明します。 これら3つのコントロールは、データ Web コントロールと ObjectDataSource によって ASP.NET ページに1行のコードを記述しなくても使用できる、いくつかの組み込みデータ変更機能を提供します。 ただし、単純なポイントとクリックの手法では、非常に低速で単純なデータ変更のユーザーインターフェイスが表示されます。 検証を提供したり、プログラムの値を挿入したり、例外を適切に処理したり、ユーザーインターフェイスをカスタマイズしたりするには、次のいくつかのチュートリアルで説明する手法を活用する必要があります。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [Next](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
