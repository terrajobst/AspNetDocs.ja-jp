---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
title: マスターページからコンテンツページと対話する (C#) |Microsoft Docs
author: rick-anderson
description: マスターページのコードから、コンテンツページのメソッドの呼び出し、プロパティの設定などを行う方法について説明します。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 3282df5e-516c-4972-8666-313828b90fb5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 2cf57665aa584285351d874267949d61db69c7fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635674"
---
# <a name="interacting-with-the-content-page-from-the-master-page-c"></a>マスター ページからコンテンツ ページと対話する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_CS.pdf)

> マスターページのコードから、コンテンツページのメソッドの呼び出し、プロパティの設定などを行う方法について説明します。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、コンテンツページをプログラムでマスターページと対話させる方法を説明しました。 マスターページが更新され、最後に追加された5つの製品が一覧表示された GridView コントロールが追加されたことを思い出してください。 次に、ユーザーが新しい製品を追加できるコンテンツページを作成しました。 新しい製品を追加すると、追加した製品が含まれるように、マスターページに GridView を更新するように指示するために必要なコンテンツページが表示されます。 この機能を実現するには、GridView にバインドされたデータを更新するマスターページにパブリックメソッドを追加し、コンテンツページからそのメソッドを呼び出します。

コンテンツページとマスターページの操作の最も一般的な形式は、コンテンツページからです。 ただし、マスターページで現在のコンテンツページを動作させることができます。また、マスターページにユーザーインターフェイス要素が含まれていて、ユーザーがコンテンツページにも表示されるデータを変更できるようにすることもできます。 GridView コントロールに製品情報を表示するコンテンツページと、クリックしたときにすべての製品の価格を倍にしたボタンコントロールを含むマスターページを考えてみましょう。 前のチュートリアルの例と同様に、GridView は新しい価格を表示するために、[二重価格] ボタンをクリックした後に更新する必要がありますが、このシナリオでは、コンテンツページのアクションを作成する必要があるマスターページです。

このチュートリアルでは、コンテンツページで定義されているマスターページの機能を実行する方法について説明します。

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>Instigating イベントハンドラーとイベントハンドラーを使用したプログラムによる対話

マスターページからコンテンツページ機能を呼び出すことは、他の方法よりも難しくなります。 コンテンツページには1つのマスターページがあるため、コンテンツページからプログラムによる操作を instigating するときには、どのようなパブリックメソッドとプロパティが破棄されているかがわかります。 ただし、マスターページにはさまざまなコンテンツページがあり、それぞれに独自のプロパティとメソッドのセットがあります。 その後、ランタイムまでどのコンテンツページが呼び出されるかわからない場合に、マスターページにコードを記述して、コンテンツページで何らかのアクションを実行できます。

Button コントロールなどの ASP.NET Web コントロールについて考えてみましょう。 ボタンコントロールは、任意の数の ASP.NET ページに表示でき、クリックされたことをページに通知するためのメカニズムを必要とします。 これは、*イベント*を使用して行います。 特に、ボタンコントロールがクリックされると、その `Click` イベントが発生します。ボタンを含む ASP.NET ページは、必要に応じて、*イベントハンドラー*を介してその通知に応答できます。

この同じパターンを使用して、マスターページのコンテンツページで機能をトリガーすることができます。

1. マスターページにイベントを追加します。
2. マスターページがそのコンテンツページと通信する必要がある場合は常に、イベントを発生させます。 たとえば、マスターページで、ユーザーが価格を2倍にしたことをコンテンツページに通知する必要がある場合、価格が2倍になった直後にそのイベントが発生します。
3. アクションを実行する必要があるコンテンツページにイベントハンドラーを作成します。

このチュートリアルの残りの部分では、概要で説明されている例を実装します。つまり、データベース内の製品と、価格を倍にするボタンコントロールが含まれているマスターページを一覧表示するコンテンツページです。

## <a name="step-1-displaying-products-in-a-content-page"></a>手順 1: コンテンツページで製品を表示する

最初のビジネスの順序は、Northwind データベースから製品を一覧表示するコンテンツページを作成することです。 (前のチュートリアルでは、[[*コンテンツ] ページからマスターページと対話*](interacting-with-the-master-page-from-the-content-page-cs.md)するために Northwind データベースをプロジェクトに追加しました)。まず、`Products.aspx`という名前の `~/Admin` フォルダーに新しい ASP.NET ページを追加し、`Site.master` マスターページにバインドします。 図1は、このページが web サイトに追加された後のソリューションエクスプローラーを示しています。

[新しい ASP.NET ページを管理フォルダーに追加 ![には](interacting-with-the-content-page-from-the-master-page-cs/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image1.png)

**図 01**: `Admin` フォルダーに新しい ASP.NET ページを追加する ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image3.png)されます)

[ *「マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)する」チュートリアルでは、明示的に設定されていない場合にページのタイトルを生成する `BasePage` という名前のカスタム基本ページクラスを作成しました。 `Products.aspx` ページの分離コードクラスにアクセスし、`System.Web.UI.Page`からではなく `BasePage` から派生させます。

最後に、このレッスンのエントリを含めるように `Web.sitemap` ファイルを更新します。 次のマークアップを `<siteMapNode>` の下に追加して、マスターページへのコンテンツの相互作用に関するレッスンを行います。

[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample1.xml)]

この `<siteMapNode>` 要素の追加は、レッスンの一覧に反映されます (図5を参照)。

`Products.aspx`に戻ります。 `MainContent`のコンテンツコントロールで、GridView コントロールを追加し、`ProductsGrid`という名前を指定します。 GridView を `ProductsDataSource`という名前の新しい SqlDataSource コントロールにバインドします。

[GridView を新しい SqlDataSource コントロールにバインド ![には](interacting-with-the-content-page-from-the-master-page-cs/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image4.png)

**図 02**: GridView を新しい SqlDataSource コントロールにバインドする ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image6.png)されます)

Northwind データベースを使用するようにウィザードを構成します。 前のチュートリアルを実行していた場合は、`Web.config`に `NorthwindConnectionString` という名前の接続文字列が既に存在している必要があります。 図3に示すように、ドロップダウンリストからこの接続文字列を選択します。

[Northwind データベースを使用するように SqlDataSource を構成 ![には](interacting-with-the-content-page-from-the-master-page-cs/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image7.png)

**図 03**: Northwind データベースを使用するように SqlDataSource を構成する ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image9.png)されます)

次に、ドロップダウンリストから Products テーブルを選択し、`ProductName` 列と `UnitPrice` 列を返すことによって、データソースコントロールの `SELECT` ステートメントを指定します (図4を参照)。 [次へ] をクリックし、[完了] をクリックして、データソースの構成ウィザードを完了します。

[Products テーブルから ProductName フィールドと UnitPrice フィールドを返す ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image10.png)

**図 04**: `Products` テーブルから `ProductName` フィールドと `UnitPrice` フィールドを返す ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image12.png)されます)

必要な作業は以上です。 ウィザードを完了すると、Visual Studio によって2つの BoundFields が GridView に追加され、SqlDataSource コントロールによって返される2つのフィールドがミラー化されます。 GridView および SqlDataSource コントロールのマークアップは次のようになります。 図5は、ブラウザーを使用して表示した場合の結果を示しています。

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample2.aspx)]

[各製品とその価格が GridView に表示される ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image13.png)

**図 05**: 各製品とその価格が GridView に表示される ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image15.png)されます)

> [!NOTE]
> GridView の外観を自由にクリーンアップしてください。 いくつかの提案には、表示される UnitPrice 値を通貨として書式設定し、背景色とフォントを使用してグリッドの外観を向上させることがあります。 ASP.NET でのデータの表示と書式設定の詳細については、「[データチュートリアルシリーズの使用](../../data-access/index.md)」を参照してください。

## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>手順 2: マスターページに2つの価格ボタンを追加する

次のタスクでは、マスターページにボタン Web コントロールを追加します。クリックすると、データベース内のすべての製品の価格が2倍になります。 `Site.master` マスターページを開き、[ツールボックス] からボタンをデザイナーにドラッグして、前のチュートリアルで追加した `RecentProductsDataSource` SqlDataSource コントロールの下に配置します。 ボタンの `ID` プロパティを `DoublePrice` に設定し、その `Text` プロパティを "Double Product プライス" に設定します。

次に、`DoublePricesDataSource`に名前を付けて、SqlDataSource コントロールをマスターページに追加します。 この SqlDataSource は、`UPDATE` ステートメントを実行してすべての価格を2倍にするために使用されます。 具体的には、`ConnectionString` と `UpdateCommand` プロパティを適切な接続文字列と `UPDATE` ステートメントに設定する必要があります。 次に、[`DoublePrice`] ボタンをクリックしたときに、この SqlDataSource コントロールの `Update` メソッドを呼び出す必要があります。 `ConnectionString` と `UpdateCommand` のプロパティを設定するには、SqlDataSource コントロールを選択し、プロパティウィンドウにアクセスします。 `ConnectionString` プロパティには、`Web.config` に既に格納されている接続文字列がドロップダウンリストに表示されます。図6に示すように、`NorthwindConnectionString` オプションを選択します。

[NorthwindConnectionString を使用するように SqlDataSource を構成 ![には](interacting-with-the-content-page-from-the-master-page-cs/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image16.png)

**図 06**: `NorthwindConnectionString` を使用するように SqlDataSource を構成する ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image18.png)されます)

`UpdateCommand` プロパティを設定するには、プロパティウィンドウで UpdateQuery オプションを見つけます。 このプロパティを選択すると、ボタンが省略記号付きで表示されます。このボタンをクリックすると、図7に示す [コマンドおよびパラメーターエディター] ダイアログボックスが表示されます。 ダイアログボックスのテキストボックスに、次の `UPDATE` ステートメントを入力します。

[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample3.sql)]

このステートメントを実行すると、`Products` テーブル内の各レコードの `UnitPrice` 値が2倍になります。

[SqlDataSource の UpdateCommand プロパティを設定 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image19.png)

**図 07**: SqlDataSource の `UpdateCommand` プロパティを設定[する (クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image21.png)される)

これらのプロパティを設定した後、ボタンおよび SqlDataSource コントロールの宣言型マークアップは次のようになります。

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample4.aspx)]

残っているのは、`DoublePrice` ボタンをクリックしたときに `Update` メソッドを呼び出すことだけです。 `DoublePrice` ボタンの `Click` イベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample5.cs)]

この機能をテストするには、手順1で作成した `~/Admin/Products.aspx` のページにアクセスし、[Double Product プライス] \ (二重製品価格 \) ボタンをクリックします。 このボタンをクリックすると、ポストバックが発生し、`DoublePrice` ボタンの `Click` イベントハンドラーが実行され、すべての製品の価格が2倍になります。 ページが再レンダリングされ、マークアップが返されて、ブラウザーに再表示されます。 ただし、[コンテンツ] ページの GridView には、[二重の製品価格] ボタンがクリックされたときと同じ価格が表示されます。 これは、GridView に最初に読み込まれたデータの状態がビューステートに格納されているため、特に指示がない限りポストバックに再読み込みされないためです。 別のページにアクセスし、[`~/Admin/Products.aspx`] ページに戻ると、更新された価格が表示されます。

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>手順 3: 価格が2倍になったときにイベントを発生させる

`~/Admin/Products.aspx` ページの GridView には、価格の2倍がすぐに反映されていないので、ユーザーは [当然の製品価格] ボタンをクリックしなかったか、または機能していないと思われるかもしれません。 このボタンを数回クリックすると、もう一度もう一度料金が倍増します。 この問題を解決するには、コンテンツページのグリッドに、2倍になった後すぐに新しい価格が表示されるようにする必要があります。

このチュートリアルで既に説明したように、ユーザーが [`DoublePrice`] ボタンをクリックするたびに、マスターページでイベントを発生させる必要があります。 イベントは、1つのクラス (イベントパブリッシャー) が、興味深い問題が発生した他のクラス (イベントサブスクライバー) のセットを別のクラスに通知する方法です。 この例では、マスターページはイベントパブリッシャーです。`DoublePrice` ボタンをクリックしたときに注意するコンテンツページはサブスクライバーです。

クラスは、発生するイベントに応答して実行されるメソッドである*イベントハンドラー*を作成することによって、イベントをサブスクライブします。 発行元は、*イベントデリゲート*を定義することによって発生するイベントを定義します。 イベントデリゲートは、イベントハンドラーが受け入れる必要のある入力パラメーターを指定します。 .NET Framework では、イベントデリゲートは値を返さず、次の2つの入力パラメーターを受け取ります。

- イベントソースを識別する `Object`
- `System.EventArgs` から派生したクラス

イベントハンドラーに渡される2番目のパラメーターには、イベントに関する追加情報を含めることができます。 基本 `EventArgs` クラスは情報に沿って渡されませんが、.NET Framework には `EventArgs` を拡張し、追加のプロパティを含む多数のクラスが含まれています。 たとえば、`CommandEventArgs` インスタンスは、`Command` イベントに応答するイベントハンドラーに渡され、`CommandArgument` と `CommandName`の2つの情報プロパティが含まれます。

> [!NOTE]
> イベントの作成、発生、および処理の詳細については、「[単純な英語の](http://www.codeproject.com/KB/cs/eventdelegates.aspx)[イベントとデリゲート](https://msdn.microsoft.com/library/17sde2xt.aspx)およびイベントデリゲート」を参照してください。

イベントを定義するには、次の構文を使用します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample6.cs)]

ユーザーが [`DoublePrice`] ボタンをクリックし、他の追加情報を渡す必要がない場合にのみ、コンテンツページにアラートを通知する必要があるため、イベントデリゲート `EventHandler`を使用できます。これにより、`System.EventArgs`型のオブジェクトを2番目のパラメーターとして受け取るイベントハンドラーが定義されます。 マスターページでイベントを作成するには、マスターページの分離コードクラスに次のコード行を追加します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample7.cs)]

上記のコードでは、`PricesDoubled`という名前のマスターページにパブリックイベントを追加します。 価格が2倍になった後に、このイベントを発生させる必要があります。 イベントを発生させるには、次の構文を使用します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample8.cs)]

ここで、 *sender*と*eventArgs*は、サブスクライバーのイベントハンドラーに渡す値です。

次のコードを使用して、`DoublePrice` `Click` イベントハンドラーを更新します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample9.cs)]

前と同様に、`Click` イベントハンドラーは、`DoublePricesDataSource` SqlDataSource コントロールの `Update` メソッドを呼び出して、すべての製品の価格を2倍にしてから開始します。 次に、イベントハンドラーへの追加が2つあります。 まず、`RecentProducts` GridView のデータが更新されます。 この GridView は、前のチュートリアルのマスターページに追加されており、最近追加された5つの製品が表示されています。 このグリッドを更新して、これら5つの製品の2倍の価格が表示されるようにする必要があります。 その後、`PricesDoubled` イベントが発生します。 マスターページ自体 (`this`) への参照がイベントソースとしてイベントハンドラーに送信され、空の `EventArgs` オブジェクトがイベント引数として送信されます。

## <a name="step-4-handling-the-event-in-the-content-page"></a>手順 4: コンテンツページでイベントを処理する

この時点で、`DoublePrice` ボタンコントロールがクリックされるたびに、マスターページの `PricesDoubled` イベントが発生します。 ただし、これは戦いの半分に過ぎません。サブスクライバーでイベントを処理する必要があります。 これには、イベントハンドラーを作成し、イベントを発生させてイベントハンドラーが実行されるようにイベントの配線コードを追加するという2つのステップが含まれます。

まず、`Master_PricesDoubled`という名前のイベントハンドラーを作成します。 マスターページで `PricesDoubled` イベントを定義する方法により、イベントハンドラーの2つの入力パラメーターはそれぞれ `Object` と `EventArgs`の型である必要があります。 イベントハンドラーで `ProductsGrid` GridView の `DataBind` メソッドを呼び出して、データをグリッドに再バインドします。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample10.cs)]

イベントハンドラーのコードは完成しましたが、マスターページの `PricesDoubled` イベントをこのイベントハンドラーに送信していません。 サブスクライバーは、次の構文を使用してイベントハンドラーにイベントをワイヤで配線します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample11.cs)]

*発行元*は、イベント*eventName*を提供するオブジェクトへの参照です。 *methodName*は、 *eventdelegate*に対応する署名を持つサブスクライバーで定義されているイベントハンドラーの名前です。 つまり、イベントデリゲートが `EventHandler`場合、 *methodName*は、値を返さないサブスクライバー内のメソッドの名前であり、それぞれ `Object` と `EventArgs`の2つの入力パラメーターを受け取る必要があります。

このイベント配線コードは、最初のページへのアクセスと後続のポストバックで実行する必要があり、イベントが発生する前のページのライフサイクルのポイントで発生する必要があります。 イベントの配線コードを追加するには、ページのライフサイクルの初期段階で PreInit 段階にあることをお勧めします。

`~/Admin/Products.aspx` を開き、`Page_PreInit` イベントハンドラーを作成します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample12.cs)]

この配線コードを完了するには、コンテンツページからマスターページへのプログラムによる参照が必要です。 前のチュートリアルで説明したように、これを行うには次の2つの方法があります。

- 緩く型指定された `Page.Master` プロパティを適切なマスターページ型にキャストする。
- `.aspx` ページで `@MasterType` ディレクティブを追加し、厳密に型指定された `Master` プロパティを使用します。

後者の方法を使用してみましょう。 ページの宣言型マークアップの先頭に、次の `@MasterType` ディレクティブを追加します。

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample13.aspx)]

次に、`Page_PreInit` イベントハンドラーに次のイベント配線コードを追加します。

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample14.cs)]

このコードを配置すると、[`DoublePrice`] ボタンがクリックされるたびにコンテンツページの GridView が更新されます。

図8と9はこの動作を示しています。 図8に、最初にアクセスしたときのページを示します。 `RecentProducts` GridView (マスターページの左側の列) と `ProductsGrid` GridView ([コンテンツ] ページ) の両方で価格値が指定されていることに注意してください。 図9は、[`DoublePrice`] ボタンがクリックされた直後の同じ画面を示しています。 ご覧のとおり、新しい価格は両方の GridViews に瞬時に反映されています。

[初期価格の値を ![する](interacting-with-the-content-page-from-the-master-page-cs/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image22.png)

**図 08**: 初期価格値 ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image24.png)されます)

[2倍の価格がグリッドビューに表示される ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image25.png)

**図 09**: 単純な価格がグリッドビューに表示される ([クリックすると、フルサイズの画像が表示](interacting-with-the-content-page-from-the-master-page-cs/_static/image27.png)されます)

## <a name="summary"></a>要約

マスターページとそのコンテンツページが相互に完全に分離されていることが理想的であり、操作のレベルは必要ありません。 ただし、マスターページまたはコンテンツページから変更できるデータを表示するマスターページまたはコンテンツページがある場合は、表示を更新できるようにデータが変更されたときに、マスターページに対してコンテンツページの警告 (またはその逆) の通知が必要になることがあります。 前のチュートリアルでは、プログラムによってマスターページと対話するコンテンツページを作成する方法を説明しました。このチュートリアルでは、マスターページで相互作用を開始する方法を見てきました。

コンテンツとマスターページ間のプログラムによる対話は、コンテンツまたはマスターページのどちらからでも行うことができますが、使用される相互作用パターンは、発信元によって異なります。 違いは、コンテンツページには1つのマスターページがありますが、マスターページにはさまざまなコンテンツページがあることがあるためです。 マスターページでコンテンツページを直接操作するのではなく、何らかのアクションが実行されたことを通知するイベントをマスターページで生成する方法をお勧めします。 アクションを考慮するコンテンツページでは、イベントハンドラーを作成できます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET でのデータへのアクセスと更新](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [イベントとデリゲート](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [コンテンツとマスターページの間で情報を渡す](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET チュートリアルでのデータの操作](../../data-access/index.md)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは、Suchi になりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](interacting-with-the-master-page-from-the-content-page-cs.md)
> [次へ](master-pages-and-asp-net-ajax-cs.md)
