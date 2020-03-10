---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-vb
title: プログラムによるマスターページの指定 (VB) |Microsoft Docs
author: rick-anderson
description: PreInit イベントハンドラーを使用して、プログラムによってコンテンツページのマスターページを設定する方法について見ていきます。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 0edcd653-f24a-41aa-aef4-75f868fe5ac2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b039b22bef38ae6ebf80be070820dc1638f87f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457306"
---
# <a name="specifying-the-master-page-programmatically-vb"></a>プログラムでマスター ページを指定する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_VB.pdf)

> PreInit イベントハンドラーを使用して、プログラムによってコンテンツページのマスターページを設定する方法について見ていきます。

## <a name="introduction"></a>はじめに

初めの例では、[*マスターページを使用してサイト全体のレイアウトを作成*](creating-a-site-wide-layout-using-master-pages-vb.md)しているため、すべてのコンテンツページは、`@Page` ディレクティブの `MasterPageFile` 属性を使用して、そのマスターページを宣言によって参照しています。 たとえば、次の `@Page` ディレクティブは、コンテンツページをマスターページ `Site.master`にリンクします。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample1.aspx)]

`System.Web.UI` 名前空間の[`Page` クラス](https://msdn.microsoft.com/library/system.web.ui.page.aspx)には、コンテンツページのマスターページへのパスを返す[`MasterPageFile` プロパティ](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx)が含まれています。このプロパティは、`@Page` ディレクティブによって設定されます。 このプロパティを使用して、プログラムでコンテンツページのマスターページを指定することもできます。 この方法は、ページにアクセスするユーザーなど、外部の要因に基づいてマスターページを動的に割り当てる場合に便利です。

このチュートリアルでは、web サイトに2番目のマスターページを追加し、実行時に使用するマスターページを動的に決定します。

## <a name="step-1-a-look-at-the-page-lifecycle"></a>手順 1: ページのライフサイクルを確認する

コンテンツページである ASP.NET ページに対して web サーバーに要求が到着するたびに、ASP.NET エンジンはページのコンテンツコントロールを、マスターページに対応する ContentPlaceHolder コントロールにヒューズする必要があります。 この fusion は、通常のページのライフサイクルを進めることができる1つのコントロール階層を作成します。

図1は、この fusion を示しています。 図1の手順1は、初期コンテンツとマスターページコントロールの階層を示しています。 PreInit 段階の末尾には、ページ内のコンテンツコントロールがマスターページ内の対応する ContentPlaceHolders (手順 2) に追加されます。 この fusion の後、マスターページは、ヒューズ制御階層のルートとして機能します。 次に、このような、このようにすることができないコントロールの階層をページに追加して、完了したコントロールの階層を生成します (手順 3)。 最終的な結果として、ページのコントロール階層には、ヒューズ制御階層が含まれます。

[PreInit ステージ中にマスターページとコンテンツページのコントロール階層が結合さ ![](specifying-the-master-page-programmatically-vb/_static/image2.png)](specifying-the-master-page-programmatically-vb/_static/image1.png)

**図 01**: マスターページとコンテンツページのコントロール階層は、PreInit ステージ中にまとめられています ([クリックすると、フルサイズの画像が表示](specifying-the-master-page-programmatically-vb/_static/image3.png)されます)

## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>手順 2: コードからの`MasterPageFile`プロパティの設定

この fusion に含まれるマスターページの内容は、`Page` オブジェクトの `MasterPageFile` プロパティの値によって異なります。 `@Page` ディレクティブで `MasterPageFile` 属性を設定すると、初期化段階で `Page`の `MasterPageFile` プロパティを割り当てることによる実質的な効果が得られます。これは、ページのライフサイクルの最初の段階です。 また、このプロパティをプログラムで設定することもできます。 ただし、このプロパティは、図1の fusion が実行される前に設定する必要があります。

PreInit 段階の開始時に、`Page` オブジェクトは[`PreInit` イベント](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx)を発生させ、その[`OnPreInit` メソッド](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)を呼び出します。 マスターページをプログラムによって設定するには、`PreInit` イベントのイベントハンドラーを作成するか、`OnPreInit` メソッドをオーバーライドします。 両方の方法を見てみましょう。

まず、サイトのホームページの分離コードクラスファイル `Default.aspx.vb`を開きます。 次のコードを入力して、ページの `PreInit` イベントのイベントハンドラーを追加します。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample2.vb)]

ここでは、`MasterPageFile` プロパティを設定できます。 値 "~/Site. master" が `MasterPageFile` プロパティに割り当てられるように、コードを更新します。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample3.vb)]

ブレークポイントを設定し、デバッグを開始すると、`Default.aspx` ページがアクセスされるたびに、またはこのページへのポストバックが発生するたびに、`Page_PreInit` イベントハンドラーが実行され、`MasterPageFile` プロパティが "~/Site. マスター" に割り当てられます。

または、`Page` クラスの `OnPreInit` メソッドをオーバーライドし、そこに `MasterPageFile` プロパティを設定することもできます。 この例では、`BasePage`ではなく、特定のページにマスターページを設定しないようにします。 [*マスターページのチュートリアルで、タイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)して、カスタムベースページクラス (`BasePage`) を作成したことを思い出してください。 現在 `BasePage` は、`Page` クラスの `OnLoadComplete` メソッドをオーバーライドします。ここでは、サイトマップデータに基づいてページの `Title` プロパティを設定します。 `BasePage` を更新して、`OnPreInit` メソッドをオーバーライドして、プログラムを使用してマスターページを指定するようにします。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample4.vb)]

すべてのコンテンツページは `BasePage`から派生するので、すべてのページにプログラムで割り当てられたマスターページがあります。 この時点で、`Default.aspx.vb` の `PreInit` イベントハンドラーは不要です。削除してもかまいません。

### <a name="what-about-thepagedirective"></a>`@Page`ディレクティブについて

少し紛らわしいかもしれませんが、コンテンツページの `MasterPageFile` のプロパティは、`BasePage` クラスの `OnPreInit` メソッドでプログラムによって、また各コンテンツページの `@Page` ディレクティブの `MasterPageFile` 属性を使用して、2か所で指定されるようになりました。

ページライフサイクルの最初の段階は初期化段階です。 この段階では、`Page` オブジェクトの `MasterPageFile` プロパティに `@Page` ディレクティブの `MasterPageFile` 属性の値が割り当てられます (指定されている場合)。 PreInit 段階は初期化段階に従います。ここでは、プログラムによって `Page` オブジェクトの `MasterPageFile` プロパティを設定し、`@Page` ディレクティブから割り当てられた値を上書きします。 `Page` オブジェクトの `MasterPageFile` プロパティはプログラムによって設定されるため、エンドユーザーのエクスペリエンスに影響を与えずに、`@Page` ディレクティブから `MasterPageFile` 属性を削除することができます。 このことを納得するために、`Default.aspx` の `@Page` ディレクティブから `MasterPageFile` 属性を削除し、ブラウザーを使用してページにアクセスします。 予想されるように、出力は属性が削除される前と同じです。

`MasterPageFile` プロパティが `@Page` ディレクティブを使用して設定されるか、またはプログラムによってエンドユーザーのエクスペリエンスに重要ではないか。 ただし、`@Page` ディレクティブの `MasterPageFile` 属性は、デザイナーで WYSIWYG ビューを生成するために、デザイン時に Visual Studio によって使用されます。 Visual Studio で `Default.aspx` に戻り、デザイナーに移動すると、"マスターページエラー: マスターページ参照を必要とするコントロールはありますが、指定されていません" というメッセージが表示されます (図2を参照)。

つまり、Visual Studio の豊富なデザイン時エクスペリエンスを利用するには、`@Page` ディレクティブに `MasterPageFile` 属性を残しておく必要があります。

[![Visual Studio では、@Page ディレクティブの MasterPageFile 属性を使用してデザインビューを表示します。](specifying-the-master-page-programmatically-vb/_static/image5.png)](specifying-the-master-page-programmatically-vb/_static/image4.png)

**図 02**: Visual Studio では、`@Page` ディレクティブの `MasterPageFile` 属性を使用してデザインビューを表示します ([クリックすると、フルサイズの画像が表示](specifying-the-master-page-programmatically-vb/_static/image6.png)されます)

## <a name="step-3-creating-an-alternative-master-page"></a>手順 3: 代替マスターページの作成

コンテンツページのマスターページは実行時にプログラムによって設定できるため、一部の外部条件に基づいて特定のマスターページを動的に読み込むことができます。 この機能は、ユーザーに応じてサイトのレイアウトを変更する必要がある場合に役立ちます。 たとえば、ブログエンジン web アプリケーションでは、ユーザーが自分のブログのレイアウトを選択できるようにすることができます。この場合、各レイアウトは異なるマスターページに関連付けられています。 実行時には、ビジターがユーザーのブログを閲覧するときに、web アプリケーションがブログのレイアウトを決定し、対応するマスターページをコンテンツページに動的に関連付ける必要があります。

いくつかの外部条件に基づいて実行時にマスターページを動的に読み込む方法を説明します。 Web サイトには現在1つのマスターページ (`Site.master`) しか含まれていません。 実行時にマスターページを選択するには、別のマスターページが必要です。 この手順では、新しいマスターページの作成と構成に焦点を当てます。 手順4では、実行時に使用するマスターページの決定について説明します。

`Alternate.master`という名前のルートフォルダーに新しいマスターページを作成します。 また、`AlternateStyles.css`という名前の web サイトに新しいスタイルシートを追加します。

[別のマスターページと CSS ファイルを Web サイトに追加 ![には](specifying-the-master-page-programmatically-vb/_static/image8.png)](specifying-the-master-page-programmatically-vb/_static/image7.png)

**図 03**: 別のマスターページと CSS ファイルを web サイトに追加[する (クリックすると、フルサイズの画像が表示](specifying-the-master-page-programmatically-vb/_static/image9.png)されます)

ここでは、ページの上部にタイトルが表示されるように `Alternate.master` マスターページをデザインしました。これは、中央と海軍の背景にあります。 左側の列をディスペンサーし、その内容を `MainContent` ContentPlaceHolder コントロールの下に移動しました。これにより、ページ全体の幅が広がります。 さらに、順序付けられていないレッスンリストを nixed し、`MainContent`上の水平方向のリストに置き換えました。 また、マスターページで使用されるフォントや色 (拡張機能では、コンテンツページ) も更新しました。 図4は、`Alternate.master` マスターページを使用する場合の `Default.aspx` を示しています。

> [!NOTE]
> ASP.NET には、*テーマ*を定義する機能が含まれています。 テーマとは、実行時にページに適用できる画像、CSS ファイル、スタイル関連の Web コントロールプロパティ設定のコレクションです。 テーマは、サイトのレイアウトが、表示されるイメージとその CSS ルールでのみ異なる場合に使用できます。 さまざまな Web コントロールを使用する場合や、大幅に異なるレイアウトを使用する場合など、レイアウトが大きく異なる場合は、別のマスターページを使用する必要があります。 テーマの詳細については、このチュートリアルの最後にある「参考資料」セクションを参照してください。

[コンテンツページで新しいルックアンドフィールを使用できるようになり ![](specifying-the-master-page-programmatically-vb/_static/image11.png)](specifying-the-master-page-programmatically-vb/_static/image10.png)

**図 04**: コンテンツページで新しいルックアンドフィールを使用できるようになりました ([クリックすると、フルサイズの画像が表示](specifying-the-master-page-programmatically-vb/_static/image12.png)されます)

マスターページとコンテンツページのマークアップがヒューズになっている場合、`MasterPage` クラスは、コンテンツページ内のすべてのコンテンツコントロールがマスターページ内の ContentPlaceHolder を参照していることを確認します。 存在しない ContentPlaceHolder を参照するコンテンツコントロールが見つかった場合は、例外がスローされます。 つまり、コンテンツページに割り当てられているマスターページには、コンテンツページのコンテンツコントロールごとに ContentPlaceHolder があることが必要です。

`Site.master` マスターページには、4つの ContentPlaceHolder コントロールがあります。

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

Web サイトのコンテンツページには、1つまたは2つのコンテンツコントロールのみが含まれています。他のユーザーには、利用可能な ContentPlaceHolders ごとにコンテンツコントロールが含まれています。 新しいマスターページ (`Alternate.master`) が、`Site.master` 内のすべての ContentPlaceHolders のコンテンツコントロールを持つコンテンツページに割り当てられている可能性がある場合、`Alternate.master` も `Site.master`と同じ ContentPlaceHolder コントロールを含める必要があります。

`Alternate.master` マスターページを手に見えるようにするには (図4を参照)、まず、`AlternateStyles.css` スタイルシートでマスターページのスタイルを定義します。 `AlternateStyles.css`に次の規則を追加します。

[!code-css[Main](specifying-the-master-page-programmatically-vb/samples/sample5.css)]

次に、次の宣言型マークアップを `Alternate.master`に追加します。 ご覧のように、`Alternate.master` には、`Site.master`の ContentPlaceHolder コントロールと同じ `ID` 値を持つ4つの ContentPlaceHolder コントロールが含まれています。 さらに、ASP.NET AJAX フレームワークを使用する web サイトのページに必要な ScriptManager コントロールも含まれています。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>新しいマスターページのテスト

この新しいマスターページをテストするには、`BasePage` クラスの `OnPreInit` メソッドを更新して、`MasterPageFile` プロパティに `"~/Alternate.maser"` 値が割り当てられるようにしてから、web サイトにアクセスします。 すべてのページはエラーなしで機能します。ただし、`~/Admin/AddProduct.aspx` と `~/Admin/Products.aspx`は除きます。 `~/Admin/AddProduct.aspx` の DetailsView に製品を追加すると、マスターページの `GridMessageText` プロパティを設定しようとするコード行から `NullReferenceException` が生成されます。 `~/Admin/Products.aspx` にアクセスすると、ページの読み込み時に `InvalidCastException` がスローされます。 "型 ' ASP のオブジェクトをキャストできません。別の\_マスター ' を型 ' ASP. サイト\_マスター ' にキャストしてください。

これらのエラーは、`Site.master` 分離コードクラスに、`Alternate.master`で定義されていないパブリックイベント、プロパティ、およびメソッドが含まれているために発生します。 これら2つのページのマークアップ部分には、`Site.master` マスターページを参照する `@MasterType` ディレクティブがあります。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample7.aspx)]

また、`~/Admin/AddProduct.aspx` の DetailsView の `ItemInserted` イベントハンドラーには、弱い型指定の `Page.Master` プロパティを `Site`型のオブジェクトにキャストするコードが含まれています。 `@MasterType` ディレクティブ (この方法で使用) と `ItemInserted` イベントハンドラーのキャストによって、`~/Admin/AddProduct.aspx` と `~/Admin/Products.aspx` のページが `Site.master` マスターページに密に結合されます。

この密結合を解除するには、`Site.master` `Alternate.master` して、パブリックメンバーの定義を含む共通の基本クラスから派生させることができます。 その後、この共通の基本型を参照するように `@MasterType` ディレクティブを更新できます。

### <a name="creating-a-custom-base-master-page-class"></a>カスタム基本マスターページクラスの作成

`BaseMasterPage.vb` という名前の `App_Code` フォルダーに新しいクラスファイルを追加し、`System.Web.UI.MasterPage`から派生させます。 `BaseMasterPage`で `RefreshRecentProductsGrid` メソッドと `GridMessageText` プロパティを定義する必要がありますが、これらのメンバーは `Site.master` マスターページ (`RecentProducts` GridView と `GridMessage` Label) に固有の Web コントロールで動作するため、単に `Site.master` から移動することはできません。

これらのメンバーが定義されているような方法で `BaseMasterPage` を構成する必要がありますが、実際には `BaseMasterPage`の派生クラス (`Site.master` および `Alternate.master`) によって実装されます。 この種の継承は、クラスを `MustInherit` とそのメンバーを `MustOverride`としてマークすることによって可能です。 つまり、これらのキーワードをクラスとその2つのメンバーに追加する `GridMessageText`と、`BaseMasterPage` が実装されておらず、その派生クラスであることが `RefreshRecentProductsGrid` になります。

また、`BaseMasterPage` で `PricesDoubled` イベントを定義し、派生クラスによってイベントを発生させる手段を提供する必要もあります。 この動作を容易にするために .NET Framework で使用されているパターンは、基本クラスでパブリックイベントを作成し、`OnEventName`という名前の保護されたオーバーライド可能なメソッドを追加することです。 派生クラスはこのメソッドを呼び出してイベントを発生させるか、またはイベントが発生する直前または直後にコードを実行するようにオーバーライドできます。

次のコードが含まれるように `BaseMasterPage` クラスを更新します。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample8.vb)]

次に、`Site.master` 分離コードクラスにアクセスし、`BaseMasterPage`から派生させます。 `BaseMasterPage` `MustOverride` マークされたメンバーが含まれているため、`Site.master`でこれらのメンバーをオーバーライドする必要があります。 メソッドとプロパティの定義に `Overrides` キーワードを追加します。 また、`DoublePrice` ボタンの `Click` イベントハンドラーの `PricesDoubled` イベントを発生させるコードを、基本クラスの `OnPricesDoubled` メソッドの呼び出しで更新します。

これらの変更を行った後、`Site.master` 分離コードクラスに次のコードが含まれている必要があります。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample9.vb)]

また、`BaseMasterPage` から派生し、2つの `MustOverride` メンバーをオーバーライドするように `Alternate.master`の分離コードクラスを更新する必要もあります。 ただし `Alternate.master` には、最新の製品を一覧表示する GridView や、新しい製品をデータベースに追加した後にメッセージを表示するラベルが含まれていないため、これらのメソッドは何もする必要はありません。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample10.vb)]

### <a name="referencing-the-base-master-page-class"></a>基本マスターページクラスの参照

これで `BaseMasterPage` クラスが完成し、2つのマスターページが拡張されました。最後に、この共通の型を参照するように `~/Admin/AddProduct.aspx` と `~/Admin/Products.aspx` のページを更新します。 まず、次のいずれかのページで `@MasterType` ディレクティブを変更します。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample11.aspx)]

変更後:

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample12.aspx)]

`@MasterType` プロパティは、ファイルパスを参照するのではなく、基本データ型 (`BaseMasterPage`) を参照するようになりました。 このため、両方のページの分離コードクラスで使用される厳密に型指定された `Master` プロパティは、型 `Site`ではなく `BaseMasterPage` 型になりました。 この変更を行った後、`~/Admin/Products.aspx`を再実行します。 以前は、ページは `Alternate.master` マスターページを使用するように構成されていますが、`@MasterType` ディレクティブは `Site.master` ファイルを参照しているため、キャストエラーが発生しました。 しかし、ページはエラーなしでレンダリングされるようになりました。 これは、`Alternate.master` マスターページが `BaseMasterPage` 型のオブジェクト (拡張されているため) にキャストできるためです。

`~/Admin/AddProduct.aspx`で行う必要がある小さな変更が1つあります。 DetailsView コントロールの `ItemInserted` イベントハンドラーは、厳密に型指定された `Master` プロパティと、緩やかに型指定された `Page.Master` プロパティの両方を使用します。 `@MasterType` ディレクティブを更新したときに、厳密に型指定された参照を修正しましたが、それでも緩やかに型指定された参照を更新する必要があります。 次のコード行を置き換えます。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample13.vb)]

次のを使用すると、`Page.Master` が基本型にキャストされます。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample14.vb)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>手順 4: コンテンツページにバインドするマスターページを決定する

`BasePage` クラスでは、現在、ページライフサイクルの PreInit ステージで、すべてのコンテンツページの `MasterPageFile` プロパティがハードコーディングされた値に設定されています。 このコードを更新して、マスターページの基礎を外部要因にすることができます。 場合によっては、マスターページは、現在ログオンしているユーザーの設定によって異なります。 その場合は、現在アクセスしているユーザーのマスターページの設定を検索する `BasePage` の `OnPreInit` メソッドにコードを記述する必要があります。

`Site.master` または `Alternate.master` を使用するマスターページをユーザーが選択し、この選択をセッション変数に保存できる web ページを作成してみましょう。 まず、`ChooseMasterPage.aspx`という名前のルートディレクトリに新しい web ページを作成します。 このページ (またはその他のコンテンツページその後) を作成する場合は、マスターページが `BasePage`でプログラムによって設定されるので、マスターページにバインドする必要はありません。 ただし、新しいページをマスターページにバインドしない場合、新しいページの既定の宣言マークアップには、マスターページによって提供される Web フォームとその他のコンテンツが含まれます。 このマークアップは、適切なコンテンツコントロールに手動で置き換える必要があります。 そのため、新しい ASP.NET ページをマスターページに簡単にバインドできます。

> [!NOTE]
> `Site.master` と `Alternate.master` は同じ ContentPlaceHolder コントロールのセットを持つため、新しいコンテンツページを作成するときにどのマスターページを選択するかは関係ありません。 一貫性を確保するために、`Site.master`を使用することをお勧めします。

[新しいコンテンツページを Web サイトに追加 ![には](specifying-the-master-page-programmatically-vb/_static/image14.png)](specifying-the-master-page-programmatically-vb/_static/image13.png)

**図 05**: web サイトに新しいコンテンツページを追加する ([クリックすると、フルサイズの画像が表示](specifying-the-master-page-programmatically-vb/_static/image15.png)されます)

このレッスンのエントリを含めるように `Web.sitemap` ファイルを更新します。 マスターページと ASP.NET AJAX レッスンの `<siteMapNode>` の下に次のマークアップを追加します。

[!code-xml[Main](specifying-the-master-page-programmatically-vb/samples/sample15.xml)]

コンテンツを `ChooseMasterPage.aspx` ページに追加する前に、ページの分離コードクラスを更新して、`BasePage` (`System.Web.UI.Page`ではなく) から派生するようにします。 次に、DropDownList コントロールをページに追加し、その `ID` プロパティを `MasterPageChoice`に設定します。さらに、"~/ListItems" の `Text` 値を持つ2つのを追加します。

ボタン Web コントロールをページに追加し、その `ID` と `Text` プロパティをそれぞれ `SaveLayout` および "レイアウト選択の保存" をそれぞれ設定します。 この時点で、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample16.aspx)]

ページに最初にアクセスしたときに、ユーザーが現在選択しているマスターページを表示する必要があります。 `Page_Load` イベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample17.vb)]

上記のコードは、最初のページにアクセスしたときにのみ実行されます (以降のポストバックでは実行されません)。 まず、セッション変数 `MyMasterPage` 存在するかどうかを確認します。 含まれている場合は、一致する ListItem を `MasterPageChoice` DropDownList で見つけようと試みます。 一致する ListItem が見つかった場合、その `Selected` プロパティは `True`に設定されます。

また、ユーザーの選択を `MyMasterPage` セッション変数に保存するコードも必要です。 `SaveLayout` ボタンの `Click` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample18.vb)]

> [!NOTE]
> ポストバック時に `Click` イベントハンドラーが実行されるまでに、マスターページは既に選択されています。 そのため、ユーザーのドロップダウンリストの選択は、次のページにアクセスするまで有効になりません。 `Response.Redirect` は、ブラウザーが `ChooseMasterPage.aspx`を再要求します。

`ChooseMasterPage.aspx` のページが完成したら、最後のタスクとして、`MyMasterPage` Session 変数の値に基づいて `MasterPageFile` プロパティ `BasePage` 割り当てる必要があります。 セッション変数が設定されていない場合は `BasePage` 既定で `Site.master`になります。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample19.vb)]

> [!NOTE]
> ここでは、`Page` オブジェクトの `MasterPageFile` プロパティを `OnPreInit` イベントハンドラーから、2つの別々のメソッドに割り当てるコードを移動しました。 この最初のメソッド `SetMasterPageFile`は、`MasterPageFile` プロパティを、`GetMasterPageFileFromSession`2 番目のメソッドによって返される値に割り当てます。 `BasePage` を拡張する今後のクラスが必要に応じて、必要に応じてカスタムロジックを実装できるように、`SetMasterPageFile` メソッドを `Overridable` マークしました。 `BasePage`の `SetMasterPageFile` プロパティをオーバーライドする例については、次のチュートリアルで説明します。

このコードを配置したら、`ChooseMasterPage.aspx` のページにアクセスします。 最初に、`Site.master` マスターページが選択されています (図6を参照)。ただし、ユーザーはドロップダウンリストから別のマスターページを選択できます。

[![コンテンツページは、サイトのマスターマスターページを使用して表示されます。](specifying-the-master-page-programmatically-vb/_static/image17.png)](specifying-the-master-page-programmatically-vb/_static/image16.png)

**図 06**: `Site.master` マスターページを使用してコンテンツページを表示[する (クリックすると、フルサイズの画像が表示](specifying-the-master-page-programmatically-vb/_static/image18.png)されます)

[代替のマスターページを使用して ![コンテンツページが表示されるようになりました。](specifying-the-master-page-programmatically-vb/_static/image20.png)](specifying-the-master-page-programmatically-vb/_static/image19.png)

**図 07**: `Alternate.master` マスターページを使用してコンテンツページが表示されるようになりました ([クリックしてフルサイズのイメージを表示](specifying-the-master-page-programmatically-vb/_static/image21.png))

## <a name="summary"></a>まとめ

コンテンツページにアクセスすると、そのコンテンツコントロールは、そのマスターページの ContentPlaceHolder コントロールと共に使用されます。 コンテンツページのマスターページは `Page` クラスの `MasterPageFile` プロパティによって示されます。このプロパティは、初期化段階で `@Page` ディレクティブの `MasterPageFile` 属性に割り当てられます。 このチュートリアルで説明したように、PreInit 段階の終了前に `MasterPageFile` 値を割り当てることができます。 プログラムを使用してマスターページを指定することで、外部要因に基づいてコンテンツページをマスターページに動的にバインドするなど、より高度なシナリオのためにドアを開くことができます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET Page ライフサイクル図](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET ページライフサイクルの概要](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET テーマとスキンの概要](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [マスターページ: ヒント、テクニック、およびトラップ](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET のテーマ](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは、Suchi になりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](master-pages-and-asp-net-ajax-vb.md)
> [次へ](nested-master-pages-vb.md)
