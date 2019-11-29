---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
title: コンテンツページからマスターページと対話する (VB) |Microsoft Docs
author: rick-anderson
description: コンテンツページのコードからマスターページのメソッドの呼び出し、プロパティの設定などを行う方法について説明します。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 081fe010-ba0f-4e7d-b4ba-774840b601c2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
msc.type: authoredcontent
ms.openlocfilehash: fe1f7b80b26ff25c1ce744e4f823e3fb35eea074
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74577226"
---
# <a name="interacting-with-the-master-page-from-the-content-page-vb"></a>コンテンツ ページからマスター ページと対話する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_VB.pdf)

> コンテンツページのコードからマスターページのメソッドの呼び出し、プロパティの設定などを行う方法について説明します。

## <a name="introduction"></a>はじめに

これまでの5つのチュートリアルでは、マスターページを作成する方法、コンテンツ領域を定義する方法、マスターページに ASP.NET ページをバインドする方法、ページ固有のコンテンツを定義する方法を説明しました。 ビジターが特定のコンテンツページを要求すると、実行時にコンテンツおよびマスターページのマークアップが1つになり、その結果、統一された制御階層がレンダリングされます。 したがって、マスターページとそのコンテンツページの相互作用を可能にする方法の1つが既に見られています。コンテンツページでは、マスターページの ContentPlaceHolder コントロールに transfuse するマークアップが指定されています。

まだ確認していないのは、マスターページとコンテンツページがプログラムによって対話する方法です。 マスターページの ContentPlaceHolder コントロールのマークアップを定義するだけでなく、コンテンツページはマスターページのパブリックプロパティに値を割り当てて、そのパブリックメソッドを呼び出すこともできます。 同様に、マスターページはそのコンテンツページと対話する場合があります。 マスターとコンテンツページ間のプログラムによる対話は、宣言型のマークアップ間の相互作用よりも一般的ではありませんが、このようなプログラムによる操作が必要になるシナリオは多数あります。

このチュートリアルでは、コンテンツページをプログラムでマスターページと対話する方法について説明します。次のチュートリアルでは、マスターページと同様にコンテンツページを操作する方法について説明します。

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>コンテンツページとそのマスターページ間のプログラムによる対話の例

ページの特定の領域をページ単位で構成する必要がある場合は、ContentPlaceHolder コントロールを使用します。 しかし、ほとんどのページで特定の出力を生成する必要があるものの、他のページを表示するためにページをカスタマイズする必要がある場合はどうでしょうか。 このような例の1つは、[*複数の contentplaceholders と既定のコンテンツ*](multiple-contentplaceholders-and-default-content-vb.md)のチュートリアルで調査したもので、各ページにログインインターフェイスを表示することです。 ほとんどのページにはログインインターフェイスが含まれている必要がありますが、メインログインページ (`Login.aspx`) など、いくつかのページに対しては抑制する必要があります。[アカウントの作成] ページまた、認証されたユーザーだけがアクセスできるその他のページもあります。 [*複数の contentplaceholders および既定のコンテンツ*](multiple-contentplaceholders-and-default-content-vb.md)のチュートリアルでは、マスターページで ContentPlaceHolder の既定のコンテンツを定義する方法と、既定のコンテンツを必要としないページで上書きする方法を説明しました。

もう1つの方法は、ログインインターフェイスを表示するか非表示にするかを示す、マスターページ内のパブリックプロパティまたはメソッドを作成することです。 たとえば、マスターページには `ShowLoginUI` という名前のパブリックプロパティが含まれています。このプロパティを使用して、マスターページの Login コントロールの `Visible` プロパティを設定しています。 ログインユーザーインターフェイスを抑制する必要があるコンテンツページでは、プログラムによって `ShowLoginUI` プロパティを `False`に設定できます。

コンテンツページに表示されるデータは、何らかのアクションがコンテンツページに発生た後にマスターページに表示されるデータを更新する必要がある場合に、コンテンツやマスターページの相互作用の最も一般的な例になります。 特定のデータベーステーブルから最近追加された5つのレコードを表示する GridView を含むマスターページがあるとします。このページには、その同じテーブルに新しいレコードを追加するためのインターフェイスが含まれています。

ユーザーがページにアクセスして新しいレコードを追加すると、マスターページに最後に追加された5つのレコードが表示されます。 新しいレコードの列の値を入力すると、彼女はフォームを送信します。 マスターページの GridView の `EnableViewState` プロパティが True (既定値) に設定されている場合、そのコンテンツはビューステートから再読み込みされます。その結果、データベースに新しいレコードが追加された場合でも、5つの同じレコードが表示されます。 これにより、ユーザーが混乱する可能性があります。

> [!NOTE]
> GridView のビューステートを無効にして、すべてのポストバックで基になるデータソースに再バインドする場合でも、配置に新しいレコードが追加されたときよりも前にデータがページのライフサイクルの前にバインドされるため、単に追加されたレコードは表示されません。ase.

これを解決するには、追加したレコードがポストバック時にマスターページの GridView に表示されるようにするには、新しいレコードがデータベースに追加され*た後*に、そのデータソースに再バインドするように GridView に指示する必要があります。 これには、新しいレコード (およびそのイベントハンドラー) を追加するためのインターフェイスがコンテンツページに含まれているが、更新する必要がある GridView がマスターページ内にあるため、コンテンツとマスターページ間の相互作用が必要です。

コンテンツページのイベントハンドラーからマスターページの表示を更新することは、コンテンツおよびマスターページの相互作用の最も一般的なニーズの1つであるため、このトピックの詳細について説明します。 このチュートリアルのダウンロードには、web サイトの `App_Data` フォルダーに `NORTHWIND.MDF` という名前の Microsoft SQL Server 2005 Express Edition データベースが含まれています。 Northwind データベースには、架空の会社である Northwind Traders の製品、従業員、および販売情報が格納されます。

手順1では、最後に追加した5つの製品を、マスターページの GridView に表示します。 手順 2. では、新しい製品を追加するためのコンテンツページを作成します。 手順 3. では、マスターページでパブリックプロパティとメソッドを作成する方法について説明します。手順4は、これらのプロパティとメソッドをコンテンツページからプログラムでインターフェイスする方法を示しています。

> [!NOTE]
> このチュートリアルでは、ASP.NET でのデータ操作の詳細については詳しく解説しません。 データを表示するためのマスターページとデータを挿入するためのコンテンツページを設定する手順は完了しましたが、まだ入力されていません。 データの表示と挿入、SqlDataSource コントロールと GridView コントロールの使用の詳細については、このチュートリアルの最後にある「詳細情報」セクションのリソースを参照してください。

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>手順 1: マスターページに最近追加された5つの製品を表示する

.Master マスターページを開き、ラベルと GridView コントロールを `leftContent` `<div>`に追加します。 ラベルの `Text` プロパティをクリアし、その `EnableViewState` プロパティを `False`に設定し、その `ID` プロパティを `GridMessage`に設定します。GridView の `ID` プロパティを `RecentProducts`に設定します。 次に、デザイナーから GridView のスマートタグを展開し、新しいデータソースにバインドするように選択します。 データソース構成ウィザードが起動します。 `App_Data` フォルダー内の Northwind データベースは Microsoft SQL Server データベースであるため、[] を選択して SqlDataSource の作成を選択します (図1を参照)。SqlDataSource `RecentProductsDataSource`という名前を指定します。

[GridView を RecentProductsDataSource という名前の SqlDataSource コントロールにバインド ![には](interacting-with-the-master-page-from-the-content-page-vb/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image1.png)

**図 01**: `RecentProductsDataSource` という名前の SqlDataSource コントロールに GridView をバインドする ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image3.png)されます)

次の手順では、接続先のデータベースを指定するように求められます。 ドロップダウンリストから `NORTHWIND.MDF` データベースファイルを選択し、[次へ] をクリックします。 このデータベースを初めて使用したので、このウィザードでは `Web.config`に接続文字列を格納することができます。 `NorthwindConnectionString`という名前を使用して接続文字列を格納します。

[Northwind データベースに接続 ![には](interacting-with-the-master-page-from-the-content-page-vb/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image4.png)

**図 02**: Northwind データベースに接続する ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image6.png)されます)

データソースの構成ウィザードには、データの取得に使用するクエリを指定できる2つの方法があります。

- カスタム SQL ステートメントまたはストアドプロシージャを指定することによって、または
- テーブルまたはビューを選択し、返す列を指定する

最近追加された5つの製品のみを取得するため、カスタム SQL ステートメントを指定する必要があります。 次の `SELECT` クエリを使用します。

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample1.sql)]

`TOP 5` キーワードは、クエリから最初の5つのレコードのみを返します。 `Products` テーブルの主キーである `ProductID`は `IDENTITY` 列です。これにより、テーブルに追加された各新しい製品の値は、前のエントリよりも大きくなります。 したがって、結果を降順に並べ替えると、最後に作成された製品が返されます。これは、`ProductID` によって降順に並べ替えられます。

[最近追加された5つの製品を返す ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image7.png)

**図 03**: 最近追加した5つの製品を返す ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image9.png)されます)

ウィザードを完了すると、Visual Studio によって、データベースから返された `ProductName` フィールドと `UnitPrice` フィールドを表示するための2つの BoundFields が GridView によって生成されます。 この時点で、マスターページの宣言型マークアップには、次のようなマークアップを含める必要があります。

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample2.aspx)]

ご覧のように、マークアップには、ラベル Web コントロール (`GridMessage`) が含まれています。2つの BoundFields を含む GridView `RecentProducts`。最後に追加された5つの製品を返す SqlDataSource コントロールです。

この GridView を作成し、SqlDataSource コントロールを構成したら、ブラウザーを使用して web サイトにアクセスします。 図4に示すように、最後に追加された5つの製品を一覧表示するグリッドが左下隅に表示されます。

[GridView に ![、最近追加された5つの製品が表示されます。](interacting-with-the-master-page-from-the-content-page-vb/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image10.png)

**図 04**: GridView には、最近追加された5つの製品が表示されます ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image12.png)されます)

> [!NOTE]
> GridView の外観を自由にクリーンアップしてください。 一部の提案には、表示された `UnitPrice` 値を通貨として書式設定する、背景色とフォントを使用してグリッドの外観を向上させることが含まれます。

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>手順 2: 新しい製品を追加するためのコンテンツページの作成

次のタスクでは、ユーザーが新しい製品を `Products` テーブルに追加できるコンテンツページを作成します。 `AddProduct.aspx`という名前の `Admin` フォルダーに新しいコンテンツページを追加し、`Site.master` マスターページにバインドするようにします。 図5は、このページが web サイトに追加された後のソリューションエクスプローラーを示しています。

[新しい ASP.NET ページを管理フォルダーに追加 ![には](interacting-with-the-master-page-from-the-content-page-vb/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image13.png)

**図 05**: `Admin` フォルダーに新しい ASP.NET ページを追加する ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image15.png)されます)

[ *「マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)する」チュートリアルでは、明示的に設定されていない場合にページのタイトルを生成する `BasePage` という名前のカスタム基本ページクラスを作成しました。 `AddProduct.aspx` ページの分離コードクラスにアクセスし、`System.Web.UI.Page`からではなく `BasePage` から派生させます。

最後に、このレッスンのエントリを含めるように `Web.sitemap` ファイルを更新します。 コントロール ID の名前付けの問題に関するレッスンの `<siteMapNode>` の下に、次のマークアップを追加します。

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample3.xml)]

図6に示すように、この `<siteMapNode>` 要素の追加はレッスンの一覧に反映されています。

`AddProduct.aspx`に戻ります。 `MainContent` ContentPlaceHolder のコンテンツコントロールで、DetailsView コントロールを追加し、`NewProduct`という名前を指定します。 DetailsView を `NewProductDataSource`という名前の新しい SqlDataSource コントロールにバインドします。 手順 1. の SqlDataSource と同様に、Northwind データベースを使用するようにウィザードを構成し、カスタム SQL ステートメントを指定します。 DetailsView はデータベースに項目を追加するために使用されるため、`SELECT` ステートメントと `INSERT` ステートメントの両方を指定する必要があります。 次の `SELECT` クエリを使用します。

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample4.sql)]

次に、[挿入] タブで、次の `INSERT` ステートメントを追加します。

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample5.sql)]

ウィザードが完了したら、DetailsView のスマートタグにアクセスし、[挿入を有効にする] チェックボックスをオンにします。 これにより、`ShowInsertButton` プロパティが True に設定された CommandField が DetailsView に追加されます。 この DetailsView はデータを挿入するためだけに使用されるため、DetailsView の `DefaultMode` プロパティを `Insert`に設定します。

必要な作業は以上です。 このページをテストしてみましょう。 ブラウザーを使用して `AddProduct.aspx` にアクセスし、名前と価格を入力します (図6を参照)。

[新しい製品をデータベースに追加 ![には](interacting-with-the-master-page-from-the-content-page-vb/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image16.png)

**図 06**: データベースに新しい製品を追加する ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image18.png)されます)

新しい製品の名前と価格を入力したら、[挿入] ボタンをクリックします。 これにより、フォームがポストバックされます。 ポストバック時に、SqlDataSource コントロールの `INSERT` ステートメントが実行されます。2つのパラメーターには、DetailsView の2つの TextBox コントロールにユーザーが入力した値が設定されます。 残念ながら、挿入が発生したことを示す視覚的なフィードバックはありません。 新しいレコードが追加されたことを確認するメッセージが表示されます。 この作業をリーダーの演習として残しておきます。 また、DetailsView から新しいレコードを追加した後も、マスターページの GridView には前と同じ5つのレコードが表示されます。これには、追加されたレコードは含まれません。 これを解決する方法については、次の手順で説明します。

> [!NOTE]
> 挿入が成功したという視覚的なフィードバックをいくつか追加するだけでなく、検証を含めるように DetailsView の挿入インターフェイスを更新することもお勧めします。 現在、検証は行われていません。 ユーザーが "高すぎる" などの `UnitPrice` フィールドに対して無効な値を入力すると、システムがその文字列を10進数に変換しようとしたときに、ポストバック時に例外がスローされます。 挿入インターフェイスをカスタマイズする方法の詳細については、データ[*変更インターフェイスのカスタマイズ*](https://asp.net/learn/data-access/tutorial-20-vb.aspx)に関するチュートリアルを参照して[ください。](../../data-access/index.md)

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>手順 3: マスターページでパブリックプロパティとパブリックメソッドを作成する

手順1では、マスターページの GridView の上に `GridMessage` という名前のラベル Web コントロールを追加しました。 このラベルは、必要に応じてメッセージを表示することを目的としています。 たとえば、`Products` テーブルに新しいレコードを追加した後、"*ProductName*がデータベースに追加されました。" というメッセージが表示される場合があります。 マスターページでこのラベルのテキストをハードコーディングするのではなく、[コンテンツ] ページでメッセージをカスタマイズできるようにすることをお勧めします。

ラベルコントロールは、マスターページ内の保護されたメンバー変数として実装されているため、コンテンツページから直接アクセスすることはできません。 コンテンツページ (または、マスターページ内の任意の Web コントロール) からマスターページ内のラベルを操作するには、Web コントロールを公開するマスターページでパブリックプロパティを作成するか、そのプロパティのいずれかを使用してプロキシとして機能させる必要があります。 できる. 次の構文をマスターページの分離コードクラスに追加して、ラベルの `Text` プロパティを公開します。

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample6.vb)]

コンテンツページから `Products` テーブルに新しいレコードが追加されたときに、マスターページ内の `RecentProducts` GridView は、基になるデータソースに再バインドする必要があります。 GridView を再バインドするには、その `DataBind` メソッドを呼び出します。 マスターページの GridView は、プログラムでコンテンツページにアクセスできないため、マスターページでパブリックメソッドを作成する必要があります。このメソッドを呼び出すと、データが GridView に再バインドされます。 マスターページの分離コードクラスに次のメソッドを追加します。

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample7.vb)]

`GridMessageText` プロパティと `RefreshRecentProductsGrid` メソッドを使用すると、任意のコンテンツページで `GridMessage` ラベルの `Text` プロパティの値をプログラムによって設定または読み取りたり、データを `RecentProducts` GridView に再バインドしたりできます。 手順 4. では、コンテンツページからマスターページのパブリックプロパティおよびメソッドにアクセスする方法を確認します。

> [!NOTE]
> マスターページのプロパティとメソッドを `Public`としてマークすることは忘れないでください。 これらのプロパティとメソッドを `Public`として明示的に指定していない場合、コンテンツページからアクセスすることはできません。

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>手順 4: コンテンツページからマスターページのパブリックメンバーを呼び出す

マスターページに必要なパブリックプロパティとメソッドが用意されたので、[`AddProduct.aspx` コンテンツ] ページからこれらのプロパティとメソッドを呼び出すことができます。 具体的には、新しい製品をデータベースに追加した後で、マスターページの `GridMessageText` プロパティを設定し、その `RefreshRecentProductsGrid` メソッドを呼び出す必要があります。 すべての ASP.NET データ Web コントロールは、さまざまなタスクが完了する直前と直後にイベントを発生させます。これにより、ページの開発者は、タスクの前後でプログラムによるアクションを簡単に実行できます。 たとえば、エンドユーザーが DetailsView の Insert ボタンをクリックすると、ポストバック時に、挿入ワークフローを開始する前に、その `ItemInserting` イベントが発生します。 次に、レコードをデータベースに挿入します。 その後、DetailsView によって `ItemInserted` イベントが発生します。 そのため、新しい製品が追加された後にマスターページを操作するには、DetailsView の `ItemInserted` イベントのイベントハンドラーを作成します。

コンテンツページは、次の2つの方法でマスターページとプログラムによってインターフェイスできます。

- `Page.Master` プロパティを使用します。これは、マスターページへの疎型の参照を返します。
- `@MasterType` ディレクティブを使用して、ページのマスターページの種類またはファイルパスを指定します。これにより、厳密に型指定されたプロパティが `Master`という名前のページに自動的に追加されます。

両方の方法を検討してみましょう。

### <a name="using-the-loosely-typedpagemasterproperty"></a>緩やかに型指定された`Page.Master`プロパティの使用

すべての ASP.NET web ページは、`System.Web.UI` 名前空間にある `Page` クラスから派生する必要があります。 `Page` クラスには、ページのマスターページへの参照を返す[`Master` プロパティ](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx)が含まれています。 ページにマスターページがない場合 `Master` は `Nothing`を返します。

`Master` プロパティは、 [`MasterPage`](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx)型のオブジェクト (`System.Web.UI` 名前空間にもあります) を返します。これは、すべてのマスターページの派生元である基本型です。 そのため、web サイトのマスターページで定義されているパブリックプロパティまたはメソッドを使用するには、`Master` プロパティから返された `MasterPage` オブジェクトを適切な型にキャストする必要があります。 マスターページファイルに `Site.master`という名前を付けたので、分離コードクラスの名前は `Site`でした。 したがって、次のコードは、`Page.Master` プロパティを `Site` クラスのインスタンスにキャストします。

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample8.vb)]

これで、疎型の `Page.Master` プロパティがサイトの種類にキャストされました。ここでは、サイトに固有のプロパティとメソッドを参照できます。 図7に示すように、[パブリック] プロパティ `GridMessageText` は [IntelliSense] ドロップダウンに表示されます。

[![の IntelliSense は、マスターページのパブリックプロパティとメソッドを表示します](interacting-with-the-master-page-from-the-content-page-vb/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image19.png)

**図 07**: IntelliSense では、マスターページのパブリックプロパティとメソッドが表示されます ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image21.png)されます)

> [!NOTE]
> マスターページファイルに名前を付けた場合は、マスターページの分離コードクラス名が `MasterPage``MasterPage.master` ます。 これにより、型 `System.Web.UI.MasterPage` から `MasterPage` クラスにキャストするときに、あいまいなコードが発生する可能性があります。 つまり、キャスト先の型を完全修飾する必要があります。これは、Web サイトプロジェクトモデルを使用する場合には少し注意が必要です。 私の提案としては、マスターページを作成するときに `MasterPage.master` 以外の名前を使用するか、マスターページへの厳密に型指定された参照を作成することをお勧めします。

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>`@MasterType`ディレクティブを使用した厳密に型指定された参照の作成

詳細を見ると、ASP.NET ページの分離コードクラスが部分クラスであることがわかります (クラス定義の `Partial` キーワードに注意してください)。 部分クラスは、とC# Visual Basic with.NET Framework 2.0 で導入され、簡単に言うと、クラスのメンバーを複数のファイルにわたって定義できます。 たとえば、コードビハインドクラスファイル `AddProduct.aspx.vb`には、ページ開発者が作成するコードが含まれています。 ASP.NET エンジンは、コードに加えて、宣言型マークアップをページのクラス階層に変換するのプロパティとイベントハンドラーを含む個別のクラスファイルを自動的に作成します。

ASP.NET ページがアクセスされるたびに発生する自動コード生成は、興味深い、役に立つ可能性のある方法を道にしています。 マスターページの場合、コンテンツページによって使用されているマスターページを ASP.NET エンジンに通知すると、厳密に型指定された `Master` プロパティが生成されます。

コンテンツページのマスターページの種類を ASP.NET エンジンに通知するには、 [`@MasterType` ディレクティブ](https://msdn.microsoft.com/library/ms228274.aspx)を使用します。 `@MasterType` ディレクティブは、マスターページの型名またはそのファイルパスを受け入れることができます。 `AddProduct.aspx` ページで `Site.master` をマスターページとして使用するように指定するには、`AddProduct.aspx`の先頭に次のディレクティブを追加します。

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample9.aspx)]

このディレクティブは、ASP.NET エンジンに対し、`Master`という名前のプロパティを使用して、厳密に型指定された参照をマスターページに追加するように指示します。 `@MasterType` ディレクティブを使用して、`Site.master` マスターページのパブリックプロパティとメソッドを、キャストなしで `Master` プロパティを使用して直接呼び出すことができます。

> [!NOTE]
> `@MasterType` ディレクティブを省略した場合、構文 `Page.Master` と `Master` は、ページのマスターページに対して厳密に型指定されたオブジェクトと同じものを返します。 `@MasterType` ディレクティブを含めた場合 `Master` は、指定されたマスターページへの厳密に型指定された参照を返します。 ただし `Page.Master`でも、疎型の参照が返されます。 詳細については、`@MasterType` ディレクティブが含まれている場合の `Master` のプロパティの作成方法については、「 [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx)'s blog entry [`@MasterType` in ASP.NET 2.0」](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)を参照してください。

### <a name="updating-the-master-page-after-adding-a-new-product"></a>新しい製品を追加した後にマスターページを更新する

これで、コンテンツページからマスターページのパブリックプロパティとメソッドを呼び出す方法がわかったので、新しい製品を追加した後にマスターページが更新されるように、`AddProduct.aspx` ページを更新する準備ができました。 手順4の開始時に、DetailsView コントロールの `ItemInserting` イベントのイベントハンドラーを作成しました。このイベントは、新しい製品がデータベースに追加された直後に実行されます。 そのイベントハンドラーに次のコードを追加します。

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample10.vb)]

上記のコードでは、緩やかに型指定された `Page.Master` プロパティと、厳密に型指定された `Master` プロパティの両方を使用します。 `GridMessageText` プロパティが "*ProductName*をグリッドに追加..." に設定されていることに注意してください。追加された製品の値には、`e.Values` コレクションからアクセスできます。ご覧のように、追加された `ProductName` 値は `e.Values("ProductName")`経由でアクセスされます。

図8は、新しい製品 (Scott のソーダ) がデータベースに追加された直後の `AddProduct.aspx` ページを示しています。 追加された製品名はマスターページのラベルに記載されており、GridView が更新され、製品とその価格が含まれていることに注意してください。

[マスターページのラベルと GridView に ![、追加した製品が表示されます。](interacting-with-the-master-page-from-the-content-page-vb/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image22.png)

**図 08**: マスターページのラベルと GridView は、追加された製品を表示します ([クリックすると、フルサイズの画像が表示](interacting-with-the-master-page-from-the-content-page-vb/_static/image24.png)されます)

## <a name="summary"></a>要約

マスターページとそのコンテンツページが相互に完全に分離されていることが理想的であり、操作のレベルは必要ありません。 マスターページとコンテンツページはその目標を念頭に置いて設計する必要がありますが、コンテンツページがマスターページとのインターフェイスを必要とする一般的なシナリオがいくつかあります。 最も一般的な理由の1つは、コンテンツページで発生する何らかのアクションに基づいて、マスターページの特定の部分を更新することです。

良いニュースとして、プログラムを使用してコンテンツページをマスターページと対話するのは比較的簡単です。 まず、コンテンツページから呼び出す必要がある機能をカプセル化した、マスターページでパブリックプロパティまたはメソッドを作成します。 次に、[コンテンツ] ページで、緩やかに型指定された `Page.Master` プロパティを使用してマスターページのプロパティとメソッドにアクセスするか、`@MasterType` ディレクティブを使用して、マスターページへの厳密に型指定された参照を作成します。

次のチュートリアルでは、マスターページがそのコンテンツページの1つをプログラムで操作する方法を確認します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET でのデータへのアクセスと更新](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET マスターページ: ヒント、テクニック、およびトラップ](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 2.0 の `@MasterType`](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [コンテンツとマスターページの間で情報を渡す](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET チュートリアルでのデータの操作](../../data-access/index.md)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Zack Jones でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](control-id-naming-in-content-pages-vb.md)
> [次へ](interacting-with-the-content-page-from-the-master-page-vb.md)
