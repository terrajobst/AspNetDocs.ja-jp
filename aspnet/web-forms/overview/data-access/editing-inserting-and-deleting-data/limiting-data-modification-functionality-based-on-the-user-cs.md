---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
title: ユーザーに基づいてデータ変更機能を制限C#する () |Microsoft Docs
author: rick-anderson
description: ユーザーがデータを編集できるようにする web アプリケーションでは、ユーザーアカウントごとにデータ編集特権が異なる場合があります。 このチュートリアルでは、次の方法について説明します。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2b251c82-77cf-4e36-baa9-b648eddaa394
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
msc.type: authoredcontent
ms.openlocfilehash: c3cacaddb7e9b493ba39718f41dcaab360d36fd9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78478426"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-c"></a>ユーザーに基づいてデータ編集機能を制限する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_CS.exe)または[PDF のダウンロード](limiting-data-modification-functionality-based-on-the-user-cs/_static/datatutorial23cs1.pdf)

> ユーザーがデータを編集できるようにする web アプリケーションでは、ユーザーアカウントごとにデータ編集特権が異なる場合があります。 このチュートリアルでは、訪問しているユーザーに基づいてデータ変更機能を動的に調整する方法について説明します。

## <a name="introduction"></a>はじめに

多くの web アプリケーションは、ユーザーアカウントをサポートし、ログインしているユーザーに基づいてさまざまなオプション、レポート、および機能を提供します。 たとえば、このチュートリアルでは、サプライヤー企業のユーザーにサイトへのログオンを許可し、その製品に関する一般情報 (たとえば、会社名などのサプライヤー情報と共に) を更新することができます。アドレス、連絡先ユーザーの情報などです。 さらに、会社のユーザーのために、在庫の単位や並べ替えレベルなどの製品情報にログオンして更新できるユーザーアカウントを追加することもできます。 Web アプリケーションでは、匿名ユーザーがアクセスできるようにすることもできますが (ログオンしていないユーザー)、データの表示のみに制限することがあります。 このようなユーザーアカウントシステムを使用して、ASP.NET ページのデータ Web コントロールで、現在ログオンしているユーザーに適した挿入、編集、および削除の機能を提供する必要があります。

このチュートリアルでは、訪問しているユーザーに基づいてデータ変更機能を動的に調整する方法について説明します。 特に、編集可能な DetailsView の仕入先情報と、業者によって提供される製品を一覧表示する GridView を表示するページを作成します。 ページにアクセスしているユーザーが会社からのものである場合、仕入先の情報を表示できます。アドレスを編集します。仕入先から提供される製品の情報を編集します。 ただし、ユーザーが特定の会社からのものである場合は、自分の住所情報を表示および編集するだけで、廃止済みとしてマークされていない製品のみを編集することができます。

[会社のユーザーが仕入先の情報を編集できる ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image1.png)

**図 1**: 会社のユーザーが仕入先の情報を編集できる ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image3.png)されます)

[特定の業者からのユーザー ![、その情報の表示と編集のみを行うことができます](limiting-data-modification-functionality-based-on-the-user-cs/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image4.png)

**図 2**: 特定の業者のユーザーが自分の情報を表示および編集することはできません ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image6.png)されます)

始めましょう!

> [!NOTE]
> ASP.NET 2.0 s メンバーシップシステムは、ユーザーアカウントを作成、管理、および検証するための、標準化された拡張可能なプラットフォームを提供します。 メンバーシップシステムの検査はこれらのチュートリアルの範囲を超えているため、このチュートリアルでは、匿名の訪問者が特定の業者または会社のどちらからのものかを選択できるようにすることで、メンバーシップを "フェイク" します。 メンバーシップの詳細については、 [ASP.NET 2.0 s のメンバーシップ、ロール、およびプロファイル](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)に関する記事シリーズを参照してください。

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>手順 1: ユーザーが自分のアクセス権を指定できるようにする

実際の web アプリケーションでは、ユーザーが会社で働いているか、特定の業者に勤務しているかがユーザーのアカウント情報に含まれており、ユーザーがサイトにログオンした後、ASP.NET のページからこの情報にプログラムからアクセスできます。 この情報は、ASP.NET 2.0 s ロールシステムを通じて、プロファイルシステムを通じてユーザーレベルのアカウント情報として、またはカスタム手段を通じてキャプチャできます。

このチュートリアルの目的は、ログオンしたユーザーに基づいてデータ変更機能を調整することであり、ASP.NET 2.0 のメンバーシップ、役割、およびプロファイルシステムを示すことを目的としたものではないため、非常に単純なメカニズムを使用して、ページにアクセスするユーザーのための機能-ユーザーがサプライヤー情報を表示および編集できるようにする必要があるかどうか、または、表示および編集が可能な特定の仕入先情報を指定できます。 ユーザーがすべての仕入先情報を表示および編集できることを示している場合 (既定)、すべての業者に対してページを表示し、仕入先の住所情報を編集して、選択した業者によって提供される任意の製品の名前と数量を編集することができます。 ただし、ユーザーが特定の業者を表示および編集するだけであることを示している場合は、その仕入先の詳細と製品のみを表示できます。また、提供が中止されて*いない*製品の名前と数量ごとの情報のみを更新できます。

このチュートリアルの最初の手順として、この DropDownList を作成し、システムのサプライヤーを設定します。 `EditInsertDelete` フォルダーの [`UserLevelAccess.aspx`] ページを開き、`ID` プロパティが [`Suppliers`] に設定されている DropDownList を追加し、この DropDownList を `AllSuppliersDataSource`という名前の新しい ObjectDataSource にバインドします。

[AllSuppliersDataSource という名前の新しい ObjectDataSource を作成 ![には](limiting-data-modification-functionality-based-on-the-user-cs/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image7.png)

**図 3**: `AllSuppliersDataSource` という名前の新しい ObjectDataSource を作成[する (クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image9.png)される)

この DropDownList にすべての業者を含めるようにするため、`SuppliersBLL` クラス s `GetSuppliers()` メソッドを呼び出すように ObjectDataSource を構成します。 また、ObjectDataSource s `Update()` メソッドが `SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドにマップされていることを確認します。この ObjectDataSource は、手順 2. で追加する DetailsView によっても使用されるためです。

ObjectDataSource ウィザードの完了後、`CompanyName` データフィールドが表示されるように `Suppliers` DropDownList を構成して、各 `ListItem`の値として `SupplierID` データフィールドを使用するように、ステップを完了します。

[仕入先の DropDownList が CompanyName および仕入先のデータフィールドを使用するように構成 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image10.png)

**図 4**: `CompanyName` と `SupplierID` のデータフィールドを使用するように `Suppliers` DropDownList を構成する ([クリックしてフルサイズの画像を表示する](limiting-data-modification-functionality-based-on-the-user-cs/_static/image12.png))

この時点で、データベース内の仕入先の会社名が一覧表示されます。 ただし、DropDownList に [すべての仕入先を表示/編集] オプションを含める必要もあります。 これを行うには、`Suppliers` DropDownList s `AppendDataBoundItems` プロパティを `true` に設定してから、`Text` プロパティが "すべての仕入先の表示/編集" で、値が `-1`である `ListItem` を追加します。 これは、宣言マークアップまたはデザイナーを使用して直接追加できます。そのためには、プロパティウィンドウに移動し、DropDownList s `Items` プロパティの省略記号をクリックします。

> [!NOTE]
> [すべて選択] 項目をデータバインド DropDownList に追加する方法の詳細については、「DropDownList チュートリアルを使用した[*マスター/詳細のフィルター処理*](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)」を参照してください。

`AppendDataBoundItems` プロパティが設定され、`ListItem` が追加されると、DropDownList の宣言型マークアップは次のようになります。

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample1.aspx)]

図5に、ブラウザーで表示したときの現在の進行状況のスクリーンショットを示します。

[仕入先の DropDownList に [すべてのアイテムの表示] と、仕入先ごとに1つの ![が含まれている](limiting-data-modification-functionality-based-on-the-user-cs/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image13.png)

**図 5**: `Suppliers` DropDownList には、各仕入先に1つずつ、[すべて表示] `ListItem`が含まれます ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image15.png)されます)

ユーザーが選択内容を変更した直後にユーザーインターフェイスを更新する必要があるため、`Suppliers` DropDownList s `AutoPostBack` プロパティを `true`に設定します。 手順 2. では、DropDownList の選択に基づいて仕入先の情報を表示する DetailsView コントロールを作成します。 次に、手順3で、この DropDownList `SelectedIndexChanged` イベントのイベントハンドラーを作成します。ここでは、選択した業者に基づいて、適切な仕入先情報を DetailsView にバインドするコードを追加します。

## <a name="step-2-adding-a-detailsview-control"></a>手順 2: DetailsView コントロールの追加

ここでは、DetailsView を使用して仕入先情報を表示します。 すべての業者を表示および編集できるユーザーに対して、DetailsView はページングをサポートします。これにより、ユーザーは一度に1レコードずつ業者情報をステップ実行できます。 ただし、ユーザーが特定の業者に対して作業する場合、DetailsView には特定の供給業者の情報のみが表示され、ページングインターフェイスは含まれません。 どちらの場合も、DetailsView は、ユーザーが仕入先の住所、市区町村、および国のフィールドを編集できるようにする必要があります。

DetailsView を `Suppliers` DropDownList の下のページに追加し、その `ID` プロパティを `SupplierDetails`に設定して、前の手順で作成した `AllSuppliersDataSource` ObjectDataSource にバインドします。 次に、[ページングを有効にする] チェックボックスをオンにし、DetailsView s スマートタグから編集チェックボックスをオンにします。

> [!NOTE]
> DetailsView s スマートタグに [編集を有効にする] オプションが表示されない場合は、ObjectDataSource s `Update()` メソッドを `SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドにマップしていないためです。 前に戻ってこの構成を変更してください。その後、[編集を有効にする] オプションが DetailsView s スマートタグに表示されます。

`SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドは、`supplierID`、`address`、`city`、および `country` の4つのパラメーターのみを受け入れるため、`CompanyName` と `Phone` BoundFields が読み取り専用になるように DetailsView の BoundFields を変更します。 さらに、`SupplierID` BoundField を完全に削除します。 最後に、`AllSuppliersDataSource` ObjectDataSource の `OldValuesParameterFormatString` プロパティは `original_{0}`に設定されています。 このプロパティ設定を宣言構文から完全に削除するか、既定値の `{0}`に設定してください。

`SupplierDetails` の DetailsView と `AllSuppliersDataSource` ObjectDataSource を構成した後、次の宣言型マークアップがあります。

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample2.aspx)]

この時点で、DetailsView はページスルーでき、選択した業者のアドレス情報は、`Suppliers` DropDownList での選択に関係なく更新できます (図6を参照)。

[![は、すべてのサプライヤー情報を表示し、そのアドレスを更新することができます。](limiting-data-modification-functionality-based-on-the-user-cs/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image16.png)

**図 6**: 任意の仕入先情報を表示し、そのアドレスを更新する ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image18.png)されます)

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>手順 3: 選択した仕入先の情報のみを表示する

現在のページには、特定の供給業者が `Suppliers` DropDownList から選択されているかどうかに関係なく、すべての業者の情報が表示されます。 選択した業者の仕入先情報だけを表示するには、別の ObjectDataSource をページに追加する必要があります。1つは特定の業者に関する情報を取得するためのものです。

新しい ObjectDataSource をページに追加し、`SingleSupplierDataSource`名前を付けます。 そのスマートタグから、[データソースの構成] リンクをクリックし、`SuppliersBLL` クラスの `GetSupplierBySupplierID(supplierID)` 方法を使用します。 `AllSuppliersDataSource` ObjectDataSource と同様に、`SingleSupplierDataSource` ObjectDataSource s `Update()` メソッドを `SuppliersBLL` クラス s `UpdateSupplierAddress` メソッドにマップします。

[SingleSupplierDataSource ObjectDataSource が GetSupplierBySupplierID (仕入先) メソッドを使用するように構成 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image19.png)

**図 7**: `GetSupplierBySupplierID(supplierID)` メソッドを使用するように `SingleSupplierDataSource` ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](limiting-data-modification-functionality-based-on-the-user-cs/_static/image21.png))

次に、`GetSupplierBySupplierID(supplierID)` メソッド s `supplierID` 入力パラメーターのパラメーターソースを指定するように求められます。 DropDownList から選択された業者の情報を表示するため、`Suppliers` DropDownList s `SelectedValue` プロパティをパラメーターソースとして使用します。

[仕入先の DropDownList を仕入先パラメーターのソースとして使用 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image22.png)

**図 8**: `Suppliers` DropDownList を `supplierID` パラメーターソースとして使用する ([クリックしてフルサイズのイメージを表示する](limiting-data-modification-functionality-based-on-the-user-cs/_static/image24.png))

この2番目の ObjectDataSource を追加した場合でも、現在、DetailsView コントロールは `AllSuppliersDataSource` ObjectDataSource を常に使用するように構成されています。 選択した `Suppliers` の DropDownList 項目に応じて、DetailsView によって使用されるデータソースを調整するロジックを追加する必要があります。 これを実現するには、仕入先の DropDownList の `SelectedIndexChanged` イベントハンドラーを作成します。 これは、デザイナーで DropDownList をダブルクリックすることで、最も簡単に作成できます。 このイベントハンドラーは、使用するデータソースを決定し、データを DetailsView に再バインドする必要があります。 これは、次のコードを使用して行います。

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample3.cs)]

イベントハンドラーは、[すべての仕入先を表示/編集] オプションが選択されているかどうかを判断することから始まります。 含まれている場合は、`SupplierDetails` DetailsView s `DataSourceID` を `AllSuppliersDataSource` に設定し、`PageIndex` プロパティを0に設定して、ユーザーを一連のサプライヤーの最初のレコードに返します。 ただし、ユーザーが DropDownList から特定の供給業者を選択している場合は、DetailsView s `DataSourceID` が `SingleSuppliersDataSource`に割り当てられます。 使用されるデータソースに関係なく、`SuppliersDetails` モードは読み取り専用モードに戻され、`SuppliersDetails` コントロール s `DataBind()` メソッドの呼び出しによってデータが DetailsView に再バインドされます。

このイベントハンドラーを配置すると、[すべての仕入先を表示/編集] オプションが選択されていない限り、DetailsView コントロールは選択された業者を表示するようになります。この場合、すべてのサプライヤーがページングインターフェイスを通じて表示されます。 図9に、[すべての仕入先を表示/編集] オプションが選択されているページを示します。ページングインターフェイスが存在し、ユーザーが任意の業者にアクセスして更新できることに注意してください。 図10は、Ma Maison supplier が選択されているページを示しています。 この場合、Ma Maison s 情報のみが表示および編集できます。

[すべての仕入先情報を表示および編集できる ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image25.png)

**図 9**: すべての仕入先情報を表示および編集できる ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image27.png)されます)

[選択した仕入先の情報のみを表示および編集できる ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image28.png)

**図 10**: 選択した仕入先の情報のみを表示および編集できます ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image30.png)されます)

> [!NOTE]
> このチュートリアルでは、dropdownlist および DetailsView コントロール s `EnableViewState` を `true` (既定) に設定する必要があります。これは、DropDownList の `SelectedIndex` および DetailsView s `DataSourceID` プロパティの変更をポストバック間で記録する必要があるためです。

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>手順 4: 編集可能な GridView で仕入先製品を一覧表示する

DetailsView が完了したら、次の手順として、選択した業者によって提供される製品を一覧表示する編集可能な GridView を含めます。 この GridView では、`ProductName` フィールドと `QuantityPerUnit` フィールドだけを編集できます。 さらに、ページにアクセスしているユーザーが特定の業者からのものである場合は、提供が中止されて*いない*製品の更新のみを許可する必要があります。 これを実現するには、最初に、`ProductID`、`ProductName`、および `QuantityPerUnit` のフィールドだけを入力として受け取る `ProductsBLL` クラス s `UpdateProducts` メソッドのオーバーロードを追加する必要があります。 このプロセスは、多くのチュートリアルで事前に段階的に説明したので、次のコードを見てみましょう。 `ProductsBLL`に追加する必要があります。

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample4.cs)]

このオーバーロードを作成したので、GridView コントロールとそれに関連付けられた ObjectDataSource を追加する準備ができました。 新しい GridView をページに追加し、その `ID` プロパティを `ProductsBySupplier`に設定して、`ProductsBySupplierDataSource`という名前の新しい ObjectDataSource を使用するように構成します。 この GridView では、選択した業者によってこれらの製品が一覧表示されるようにするため、`ProductsBLL` クラス s `GetProductsBySupplierID(supplierID)` メソッドを使用します。 また、`Update()` メソッドを、先ほど作成した新しい `UpdateProduct` オーバーロードにマップします。

[作成したばかりの UpdateProduct オーバーロードを使用するように ObjectDataSource を構成 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image31.png)

**図 11**: 作成した `UpdateProduct` のオーバーロードを使用するように ObjectDataSource を構成する ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image33.png)されます)

`GetProductsBySupplierID(supplierID)` メソッド s `supplierID` 入力パラメーターのパラメーターソースを選択するように求められます。 DetailsView で選択された業者の製品を表示するため、`SuppliersDetails` DetailsView コントロール s `SelectedValue` プロパティをパラメーターソースとして使用します。

[SuppliersDetails DetailsView s SelectedValue プロパティをパラメーターソースとして使用 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image34.png)

**図 12**: `SuppliersDetails` DetailsView s `SelectedValue` プロパティをパラメーターソースとして使用する ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image36.png)されます)

GridView に戻り、`ProductName`、`QuantityPerUnit`、および `Discontinued`を除くすべての GridView フィールドを削除し、`Discontinued` CheckBoxField を読み取り専用としてマークします。 また、GridView s スマートタグの [編集を有効にする] オプションをオンにします。 これらの変更が行われると、GridView および ObjectDataSource の宣言型マークアップは次のようになります。

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample5.aspx)]

以前の ObjectDataSources ソースと同様に、この1つの `OldValuesParameterFormatString` プロパティは `original_{0}`に設定されています。これにより、製品名またはユニットあたりの数量を更新しようとしたときに問題が発生します。 このプロパティを宣言構文から完全に削除するか、既定の `{0}`に設定します。

この構成が完了すると、GridView で選択された業者によって提供された製品がページに表示されるようになります (図13を参照)。 現在 *、すべての*製品名またはユニットあたりの数量を更新できます。 ただし、特定の業者に関連付けられているユーザーの製品が廃止された場合は、ページロジックを更新する必要があります。 この最後の部分は、手順 5. で説明します。

[選択した業者によって提供される製品 ![表示されます](limiting-data-modification-functionality-based-on-the-user-cs/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image37.png)

**図 13**: 選択した業者によって提供される製品が表示されます ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image39.png)されます)

> [!NOTE]
> この編集可能な GridView を追加すると、`Suppliers` DropDownList s `SelectedIndexChanged` イベントハンドラーを更新して、GridView を読み取り専用の状態に戻す必要があります。 それ以外の場合、製品情報の編集中に別の業者が選択されていると、新しい業者の GridView の対応するインデックスも編集可能になります。 これを回避するには、`SelectedIndexChanged` イベントハンドラーで GridView s `EditIndex` プロパティを `-1` に設定するだけです。

また、GridView のビューステートが有効になっていることが重要であることを思い出してください (既定の動作)。 GridView s `EnableViewState` プロパティを `false`に設定すると、同時実行ユーザーが誤ってレコードを削除または編集する危険性があります。 「警告: 詳細については[、編集または削除をサポートし、ビューステートが無効になっている ASP.NET 2.0 GridViews/DetailsView/formviews での同時実行の問題](http://scottonwriting.net/sowblog/posts/10054.aspx)」を参照してください。

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>手順 5: [すべての業者を表示/編集] が選択されていないときに、廃止された製品の編集を禁止する

`ProductsBySupplier` GridView は完全に機能していますが、現在は特定の業者からのユーザーへのアクセスを許可しています。 Microsoft のビジネスルールに従って、このようなユーザーは、廃止された製品を更新できないようにする必要があります。 これを適用するには、仕入先からユーザーがページにアクセスしているときに、廃止された製品を含む GridView 行の [編集] ボタンを非表示 (または無効) にします。

GridView s `RowDataBound` イベントのイベントハンドラーを作成します。 このイベントハンドラーでは、ユーザーが特定の業者に関連付けられているかどうかを判断する必要があります。これは、このチュートリアルでは、supplier DropDownList `SelectedValue` プロパティをチェックすることによって決定できます。-1 以外の場合は、ユーザーが特定の業者に関連付けられます。 そのようなユーザーについては、製品が廃止されたかどうかを判断する必要があります。 Gridview の[*フッターに概要情報を表示*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md)する方法に関するページで説明されているように、`e.Row.DataItem` プロパティを使用して、gridview 行にバインドされている実際の `ProductRow` インスタンスへの参照を取得できます。 製品が廃止された場合は、前のチュートリアルで説明した手法を使用して、GridView の CommandField の [Edit] ボタンへのプログラムによる参照を取得し、[*削除時にクライアント側の確認を追加*](adding-client-side-confirmation-when-deleting-cs.md)することができます。 参照を取得したら、ボタンを非表示にしたり、無効にしたりできます。

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample6.cs)]

このイベントハンドラーが配置されている場合、特定の業者からのユーザーとしてこのページにアクセスすると、これらの製品の [編集] ボタンが非表示になっているため、廃止された製品は編集できません。 たとえば、Chef Anton s Gumbo Mix は、新しい Orleans Cajun Delights supplier で廃止された製品です。 この特定の業者のページにアクセスすると、この製品の [編集] ボタンが表示されません (図14を参照)。 ただし、[すべての仕入先を表示/編集する] を使用してアクセスする場合は、[編集] ボタンを使用できます (図15を参照)。

[仕入先固有のユーザーの ![、Chef Anton s Gumbo ミックスの [編集] ボタンが非表示になっています](limiting-data-modification-functionality-based-on-the-user-cs/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image40.png)

**図 14**: 仕入先固有のユーザーの場合は、Chef Anton s Gumbo ミックスの [編集] ボタンが非表示になります ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image42.png)されます)

[[すべてのサプライヤーユーザーの表示/編集] の ![、Chef Anton s Gumbo ミックスの [編集] ボタンが表示されます。](limiting-data-modification-functionality-based-on-the-user-cs/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image43.png)

**図 15**: [すべてのサプライヤーユーザーの表示/編集] では、Chef Anton s Gumbo ミックスの [編集] ボタンが表示されます ([クリックすると、フルサイズの画像が表示](limiting-data-modification-functionality-based-on-the-user-cs/_static/image45.png)されます)

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>ビジネスロジック層のアクセス権を確認しています

このチュートリアルでは、ASP.NET ページで、ユーザーに表示される情報と更新可能な製品に関して、すべてのロジックを処理します。 このロジックはビジネスロジックレイヤーにも存在するのが理想的です。 たとえば、`SuppliersBLL` クラス s `GetSuppliers()` メソッド (すべての業者を返す) には、現在ログオンしているユーザーが特定の業者に関連付けられて*いない*ことを確認するためのチェックが含まれる場合があります。 同様に、`UpdateSupplierAddress` 方法では、現在ログオンしているユーザーが会社で働いている (したがって、すべての仕入先住所情報を更新できる) か、データが更新される業者に関連付けられているかを確認することができます。

ここでは、このような BLL レイヤーチェックを含めませんでした。このチュートリアルでは、ユーザーの権利はページの DropDownList によって決定され、BLL クラスはアクセスできません。 メンバーシップシステムを使用する場合、または ASP.NET によって提供される既定の認証スキーム (Windows 認証など) のいずれかを使用する場合は、現在ログオンしているユーザーの情報とロール情報に BLL からアクセスして、そのようなアクセスを行うことができます。権限は、プレゼンテーション層と BLL レイヤーの両方で確認できます。

## <a name="summary"></a>まとめ

ユーザーアカウントを提供するほとんどのサイトでは、ログインしているユーザーに基づいてデータ変更インターフェイスをカスタマイズする必要があります。 管理ユーザーは任意のレコードを削除して編集できますが、管理者以外のユーザーは、自分が作成したレコードの更新または削除のみに制限される可能性があります。 シナリオに関係なく、データ Web コントロール、ObjectDataSource、およびビジネスロジックレイヤークラスを拡張して、ログオンしているユーザーに基づいて特定の機能を追加または拒否することができます。 このチュートリアルでは、ユーザーが特定の業者に関連付けられているかどうか、または会社で働いていたかに応じて、表示可能なデータと編集可能なデータを制限する方法について説明しました。

このチュートリアルでは、GridView、DetailsView、および FormView コントロールを使用したデータの挿入、更新、および削除についての調査を終了します。 次のチュートリアルから、ページングと並べ替えのサポートを追加することに注目します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](adding-client-side-confirmation-when-deleting-cs.md)
> [次へ](an-overview-of-inserting-updating-and-deleting-data-vb.md)
