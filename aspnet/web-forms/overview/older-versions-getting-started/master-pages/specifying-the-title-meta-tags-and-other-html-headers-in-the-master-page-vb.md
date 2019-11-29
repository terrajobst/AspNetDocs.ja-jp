---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb
title: マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定する (VB) |Microsoft Docs
author: rick-anderson
description: コンテンツページからマスターページ内の &lt;head&gt; 要素を定義するためのさまざまな手法について見ていきます。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: ea8196f5-039d-43ec-8447-8997ad4d3900
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 160af664cdf27f9ede1273aaf915da749a39ad48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74637705"
---
# <a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb"></a>マスター ページでタイトル、メタ タグ、その他の HTML ヘッダーを指定する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_VB.pdf)

> コンテンツページからマスターページ内の &lt;head&gt; 要素を定義するためのさまざまな手法について見ていきます。

## <a name="introduction"></a>はじめに

Visual Studio 2008 で作成された新しいマスターページには、既定で2つの ContentPlaceHolder コントロールがあります。1つは `head`という名前で、もう1つは `<head>` 要素にあります。また、Web フォーム内に配置された `ContentPlaceHolder1`という名前のものがあります。 `ContentPlaceHolder1` の目的は、ページごとにカスタマイズできる、Web フォームの領域を定義することです。 `head` ContentPlaceHolder を使用すると、ページは `<head>` セクションにカスタムコンテンツを追加できます。 (もちろん、これら2つの ContentPlaceHolders は変更または削除でき、追加の ContentPlaceHolder をマスターページに追加することもできます。 現在のマスターページ `Site.master`には、4つの ContentPlaceHolder コントロールがあります)。

HTML `<head>` 要素は、ドキュメント自体に含まれていない web ページドキュメントに関する情報のリポジトリとして機能します。 これには、web ページのタイトル、検索エンジンまたは内部クローラーで使用されるメタ情報、RSS フィード、JavaScript、CSS ファイルなどの外部リソースへのリンクなどの情報が含まれます。 この情報の一部は、web サイトのすべてのページに関連している場合があります。 たとえば、すべての ASP.NET ページに対して同じ CSS 規則と JavaScript ファイルをグローバルにインポートすることができます。 ただし、`<head>` 要素にはページ固有の部分があります。 ページタイトルは、代表的な例です。

このチュートリアルでは、マスターページとそのコンテンツページで、グローバルおよびページ固有の `<head>` セクションマークアップを定義する方法について説明します。

## <a name="examining-the-master-pagesheadsection"></a>マスターページの`<head>`セクションを調べる

Visual Studio 2008 によって作成される既定のマスターページファイルには、`<head>` セクションに次のマークアップが含まれています。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample1.aspx)]

`<head>` 要素には `runat="server"` 属性が含まれていることに注意してください。これは、静的 HTML ではなく、サーバーコントロールであることを示します。 すべての ASP.NET ページは、`System.Web.UI` 名前空間にある[`Page` クラス](https://msdn.microsoft.com/library/system.web.ui.page.aspx)から派生します。 このクラスには、ページの `<head>` 領域へのアクセスを提供する[`Header` プロパティ](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx)が含まれています。 `Header` プロパティを使用して、ASP.NET ページのタイトルを設定したり、表示される `<head>` セクションにマークアップを追加したりできます。 次に、ページの `Page_Load` イベントハンドラーに少しコードを記述して、コンテンツページの `<head>` 要素をカスタマイズできます。 手順1でページのタイトルをプログラムによって設定する方法を確認します。

上の `<head>` 要素に示されているマークアップには、`head`という名前の ContentPlaceHolder コントロールも含まれています。 コンテンツページでは、`<head>` 要素にプログラムによってカスタムコンテンツを追加できるため、この ContentPlaceHolder コントロールは必要ありません。 ただし、静的なマークアップをプログラムによってではなく、対応するコンテンツコントロールに宣言的に追加できるため、コンテンツページで `<head>` 要素に静的マークアップを追加する必要がある場合に便利です。

`<title>` 要素と `head` ContentPlaceHolder に加えて、マスターページの `<head>` 要素には、すべてのページに共通のすべての `<head>`レベルのマークアップが含まれている必要があります。 Web サイトでは、すべてのページが `Styles.css` ファイルで定義されている CSS 規則を使用します。 そのため、「[*マスターページを使用したサイト全体のレイアウトの作成*](creating-a-site-wide-layout-using-master-pages-vb.md)」チュートリアルの `<head>` 要素を更新して、対応する `<link>` 要素を含めるようにしました。 `Site.master` マスターページの現在の `<head>` マークアップを次に示します。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>手順 1: コンテンツページのタイトルを設定する

Web ページのタイトルは、`<title>` 要素によって指定されます。 各ページのタイトルを適切な値に設定することが重要です。 ページにアクセスすると、ブラウザーのタイトルバーにタイトルが表示されます。 さらに、ページをブックマークするときに、ブラウザーはそのページのタイトルをブックマークの推奨される名前として使用します。 また、多くの検索エンジンでは、検索結果を表示するときにページのタイトルが表示されます。

> [!NOTE]
> 既定では、Visual Studio によって、マスターページの `<title>` 要素が "無題のページ" に設定されます。 同様に、新しい ASP.NET ページでも `<title>` が "無題のページ" に設定されています。 ページのタイトルを適切な値に設定するのは簡単ではないため、インターネット上には "無題のページ" というタイトルのページが多数あります。 このタイトルで web ページの Google を検索すると、約246万の結果が返されます。 Microsoft でも、"無題のページ" というタイトルの web ページを公開することはできます。 このドキュメントの執筆時点では、Google search は Microsoft.com ドメイン内のこのような web ページを236報告しました。

ASP.NET ページでは、次のいずれかの方法でタイトルを指定できます。

- `<title>` 要素内に値を直接配置する
- `<%@ Page %>` ディレクティブでの `Title` 属性の使用
- `Page.Title="title"` や `Page.Header.Title="title"`などのコードを使用して、プログラムによってページの `Title` プロパティを設定します。

コンテンツページには、マスターページで定義されているように `<title>` 要素はありません。 そのため、コンテンツページのタイトルを設定するには、`<%@ Page %>` ディレクティブの `Title` 属性を使用するか、プログラムによって設定します。

### <a name="setting-the-pages-title-declaratively"></a>ページのタイトルを宣言によって設定する

コンテンツページのタイトルは、 [`<%@ Page %>` ディレクティブ](https://msdn.microsoft.com/library/ydy4x04a.aspx)の `Title` 属性を使用して、宣言によって設定できます。 このプロパティを設定するには、`<%@ Page %>` ディレクティブを直接変更するか、プロパティウィンドウを使用します。 両方の方法を見てみましょう。

ソースビューで、ページの宣言型マークアップの一番上にある `<%@ Page %>` ディレクティブを見つけます。 `Default.aspx` の `<%@ Page %>` ディレクティブは次のとおりです。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample3.aspx)]

`<%@ Page %>` ディレクティブは、ページの解析とコンパイル時に ASP.NET エンジンによって使用されるページ固有の属性を指定します。 これには、マスターページファイル、コードファイルの場所、その他の情報などが含まれます。

既定では、新しいコンテンツページを作成するときに、Visual Studio によって `Title` 属性が "無題のページ" に設定されます。 `Default.aspx`の `Title` 属性を "無題のページ" から "マスターページチュートリアル" に変更し、ブラウザーを使用してそのページを表示します。 図1は、新しいページタイトルを反映するブラウザーのタイトルバーを示しています。

![ブラウザーのタイトルバーには、&quot;無題のページではなく&quot; &quot;マスターページのチュートリアルが表示されるようになりました&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image1.png)

**図 01**: ブラウザーのタイトルバーに "無題のページ" ではなく "マスターページのチュートリアル" が表示されるようになりました。

ページのタイトルは、プロパティウィンドウから設定することもできます。 プロパティウィンドウから、ドロップダウンリストから [ドキュメント] を選択して、`Title` プロパティを含むページレベルのプロパティを読み込みます。 図2は、`Title` が "マスターページチュートリアル" に設定された後のプロパティウィンドウを示しています。

![[プロパティ] ウィンドウからタイトルを構成することもできます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image2.png)

**図 02**: [プロパティ] ウィンドウからタイトルを構成することもできます。

### <a name="setting-the-pages-title-programmatically"></a>プログラムによるページのタイトルの設定

ASP.NET エンジンによってページがレンダリングされるときに、マスターページの `<head runat="server">` マークアップが[`HtmlHead` クラス](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx)のインスタンスに変換されます。 `HtmlHead` クラスには、表示される `<title>` 要素に値が反映される[`Title` プロパティ](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx)があります。 このプロパティは、`Page.Header.Title`を介して ASP.NET ページの分離コードクラスからアクセスできます。この同じプロパティには、`Page.Title`経由でアクセスすることもできます。

プログラムによってページのタイトルを設定する方法については、`About.aspx` ページの分離コードクラスに移動し、ページの `Load` イベントのイベントハンドラーを作成します。 次に、ページのタイトルを "マスターページチュートリアル:: About:: *date*" に設定します。ここで、 *date*は現在の日付です。 このコードを追加すると、`Page_Load` イベントハンドラーは次のようになります。

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample4.vb)]

図3は、`About.aspx` ページにアクセスするときのブラウザーのタイトルバーを示しています。

![ページのタイトルはプログラムによって設定され、現在の日付が含まれます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image3.png)

**図 03**: ページのタイトルがプログラムによって設定され、現在の日付が含まれる

## <a name="step-2-automatically-assigning-a-page-title"></a>手順 2: ページタイトルを自動的に割り当てる

手順 1. で見たように、ページのタイトルは宣言またはプログラムによって設定できます。 ただし、タイトルをさらにわかりやすいものに明示的に変更し忘れた場合、ページには既定のタイトル "無題のページ" が表示されます。 理想的には、ページのタイトルは、値を明示的に指定していない場合に自動的に設定されます。 たとえば、実行時にページのタイトルが "無題のページ" である場合、タイトルを自動的に更新して、ASP.NET ページのファイル名と同じにすることができます。 すばらしいのは、少しの初期作業で、タイトルを自動的に割り当てることができるということです。

すべての ASP.NET web ページは、System.web. UI 名前空間の `Page` クラスから派生します。 `Page` クラスは、ASP.NET ページに必要な最小限の機能を定義し、他の多くの `IsPostBack`、`IsValid`、`Request`、`Response`などの重要なプロパティを公開します。 多くの場合、web アプリケーションのすべてのページに追加の機能が必要です。 これを提供する一般的な方法は、カスタムの基本ページクラスを作成することです。 カスタム基本ページクラスは、`Page` クラスから派生し、追加の機能を含む、作成するクラスです。 この基本クラスを作成した後は、ASP.NET ページを (`Page` クラスではなく) 派生させて、ASP.NET ページに拡張機能を提供することができます。

この手順では、タイトルが明示的に設定されていない場合に、ページのタイトルを ASP.NET ページのファイル名に自動的に設定するベースページを作成します。 手順3は、サイトマップに基づいてページのタイトルを設定する方法を示しています。

> [!NOTE]
> カスタムベースページクラスの作成と使用の詳細については、このチュートリアルシリーズの範囲を超えています。 詳細については、「 [ASP.NET ページの分離コードクラスのカスタム基本クラスの使用」](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)を参照してください。

### <a name="creating-the-base-page-class"></a>基本ページクラスの作成

最初のタスクは、基本ページクラスを作成することです。これは、`Page` クラスを拡張するクラスです。 まず、ソリューションエクスプローラーでプロジェクト名を右クリックして [ASP.NET フォルダーの追加] を選択し、[`App_Code`] を選択して、プロジェクトに `App_Code` フォルダーを追加します。 次に、`App_Code` フォルダーを右クリックし、`BasePage.vb`という名前の新しいクラスを追加します。 図4は、`App_Code` フォルダーと `BasePage.vb` クラスが追加された後のソリューションエクスプローラーを示しています。

![App_Code フォルダーと、BasePage という名前のクラスを追加します。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image4.png)

**図 04**: `App_Code` フォルダーと `BasePage` という名前のクラスを追加する

> [!NOTE]
> Visual Studio では、2つのプロジェクト管理モード (Web サイトプロジェクトと Web アプリケーションプロジェクト) がサポートされています。 `App_Code` フォルダーは、Web サイトプロジェクトモデルと共に使用するように設計されています。 Web アプリケーションプロジェクトモデルを使用している場合は、`Classes`など、`App_Code`以外の名前のフォルダーに `BasePage.vb` クラスを配置します。 このトピックの詳細については、web[サイトプロジェクトの Web アプリケーションプロジェクトへの移行](http://webproject.scottgu.com/VisualBasic/Migration2/Migration2.aspx)に関するページを参照してください。

カスタムベースページは、ASP.NET ページの分離コードクラスの基底クラスとして機能するため、`Page` クラスを拡張する必要があります。

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample5.vb)]

ASP.NET ページが要求されるたびに、HTML にレンダリングされる要求されたページ内のするの一連のステージに進みます。 `Page` クラスの `OnEvent` メソッドをオーバーライドすることによって、1つのステージをタップできます。 ベースページについては、`LoadComplete` ステージによって明示的に指定されていない場合は、自動的にタイトルが設定されます (これは、`Load` 段階の後に発生する可能性があります)。

これを実現するには、`OnLoadComplete` メソッドをオーバーライドし、次のコードを入力します。

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample6.vb)]

`OnLoadComplete` メソッドは、`Title` プロパティが明示的に設定されていないかどうかを判断することから始まります。 `Title` プロパティが `Nothing`、空の文字列、または値が "無題のページ" の場合は、要求された ASP.NET ページのファイル名に割り当てられます。 要求された ASP.NET `C:\MySites\Tutorial03\Login.aspx`ページへの物理パス (たとえば、) は `Request.PhysicalPath` プロパティを使用してアクセスできます。 `Path.GetFileNameWithoutExtension` メソッドを使用して、ファイル名の部分のみを取得し、このファイル名を `Page.Title` プロパティに割り当てます。

> [!NOTE]
> タイトルの形式を改善するために、このロジックを強化することをお勧めします。 たとえば、ページのファイル名が `Company-Products.aspx`場合、上記のコードでは "Company-Products" というタイトルが生成されますが、"会社の製品" のように、ダッシュはスペースで置き換えられるのが理想的です。 また、大文字小文字の変更がある場合は必ずスペースを追加することを検討してください。 つまり、ファイル名 `OurBusinessHours.aspx` を "当社の勤務時間" のタイトルに変換するコードを追加することを検討してください。

### <a name="having-the-content-pages-inherit-the-base-page-class"></a>コンテンツページが基本ページクラスを継承するようにする

ここでは、`Page` クラスではなく、カスタムベースページ (`BasePage`) から派生するようにサイトの ASP.NET ページを更新する必要があります。 これを実現するには、各分離コードクラスに移動し、クラス宣言を次のように変更します。

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample7.vb)]

宛先:

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample8.vb)]

その後、ブラウザーを使用してサイトにアクセスします。 `Default.aspx` や `About.aspx`など、タイトルが明示的に設定されているページにアクセスすると、明示的に指定されたタイトルが使用されます。 ただし、タイトルが既定値 ("無題のページ") から変更されていないページにアクセスする場合、ベースページクラスはタイトルをページのファイル名に設定します。

図5は、ブラウザーを使用して表示するときの `MultipleContentPlaceHolders.aspx` ページを示しています。 タイトルは、厳密にはページのファイル名 (拡張子が小さい) "MultipleContentPlaceHolders" であることに注意してください。

[![タイトルが明示的に指定されていない場合は、ページのファイル名が自動的に使用されます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image5.png)

**図 05**: タイトルが明示的に指定されていない場合は、ページのファイル名が自動的に使用されます ([クリックすると、フルサイズの画像が表示](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image7.png)されます)

## <a name="step-3-basing-the-page-title-on-the-site-map"></a>手順 3: サイトマップのページタイトルを基にする

ASP.NET には、サイトマップに関する情報を表示するための Web コントロールと共に、ページ開発者が外部リソース (XML ファイルやデータベーステーブルなど) で階層サイトマップを定義できるようにする、堅牢なサイトマップフレームワークが用意されています (SiteMapPath など)。メニューと TreeView コントロール)。

サイトマップ構造には、ASP.NET ページの分離コードクラスからプログラムからアクセスすることもできます。 この方法では、サイトマップ内の対応するノードのタイトルにページのタイトルを自動的に設定できます。 手順 2. で作成した `BasePage` クラスを拡張して、この機能を提供できるようにしましょう。 ただし、まず、サイトのサイトマップを作成する必要があります。

> [!NOTE]
> このチュートリアルでは、読者が既に ASP に精通していることを前提としています。NET のサイトマップ機能。 サイトマップの使用方法の詳細については、「マルチパート」を参照してください[。NET のサイトナビゲーション](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)。

### <a name="creating-the-site-map"></a>サイトマップの作成

サイトマップシステムは、[プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)の上に構築されます。これにより、サイトマップ API は、メモリと永続ストアの間でサイトマップ情報をシリアル化するロジックから切り離されます。 .NET Framework には、既定のサイトマッププロバイダーである[`XmlSiteMapProvider` クラス](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)が付属しています。 その名前が示すように、`XmlSiteMapProvider` は、サイトマップストアとして XML ファイルを使用します。 このプロバイダーを使用して、サイトマップを定義してみましょう。

まず、`Web.sitemap`という名前の web サイトのルートフォルダーにサイトマップファイルを作成します。 これを行うには、ソリューションエクスプローラーで web サイト名を右クリックし、[新しい項目の追加] を選択して、[サイトマップ] テンプレートを選択します。 ファイルの名前が `Web.sitemap` であることを確認し、[追加] をクリックします。

[Web サイトのルートフォルダーに、web.sitemap という名前のファイルを追加 ![ます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image8.png)

**図 06**: `Web.sitemap` という名前のファイルを web サイトのルートフォルダーに追加する ([クリックすると、フルサイズの画像が表示](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image10.png)されます)

`Web.sitemap` ファイルに次の XML を追加します。

[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample9.xml)]

この XML は、図7に示す階層型サイトマップ構造を定義します。

![サイトマップは、現在、3つのサイトマップノードで構成されています。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image11.png)

**図 07**: サイトマップが現在3つのサイトマップノードで構成されている

新しい例を追加すると、今後のチュートリアルでサイトマップ構造が更新されます。

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>ナビゲーション Web コントロールを含むようにマスターページを更新する

サイトマップが定義されたので、ナビゲーション Web コントロールを含むようにマスターページを更新してみましょう。 具体的には、「レッスン」セクションの左側の列に ListView コントロールを追加して、サイトマップで定義されている各ノードのリスト項目を含む順序指定されていないリストを表示します。

> [!NOTE]
> ListView コントロールは、ASP.NET バージョン3.5 の新しいバージョンです。 以前のバージョンの ASP.NET を使用している場合は、代わりに Repeater コントロールを使用します。 ListView コントロールの詳細については、「 [ASP.NET 3.5 の Listview コントロールと DataPager コントロールの使用](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)」を参照してください。

まず、レッスンセクションから、既存の順序付けられていないリストのマークアップを削除します。 次に、ツールボックスから ListView コントロールをドラッグし、レッスンの見出しの下にドロップします。 ListView は、ツールボックスの [データ] セクションにあります。他のビューコントロール (GridView、DetailsView、FormView) と共に表示されます。 ListView の `ID` プロパティを `LessonsList`に設定します。

データソース構成ウィザードで、`LessonsDataSource`という名前の新しい SiteMapDataSource コントロールに ListView をバインドします。 SiteMapDataSource コントロールは、サイトマップシステムから階層構造を返します。

[SiteMapDataSource コントロールをない On ListView コントロールにバインドするには ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image12.png)

**図 08**: SiteMapDataSource コントロールをコントロールに連結する ([クリックしてフルサイズのイメージを表示する](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image14.png))

SiteMapDataSource コントロールを作成したら、ListView のテンプレートを定義して、SiteMapDataSource コントロールによって返される各ノードのリスト項目を含む順序指定されていないリストをレンダリングする必要があります。 これは、次のテンプレートマークアップを使用して実現できます。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample10.aspx)]

`LayoutTemplate` は、順序付けられていないリスト (`<ul>...</ul>`) のマークアップを生成します。一方、`ItemTemplate` は、特定のレッスンへのリンクを含むリスト項目 (`<li>`) として、SiteMapDataSource によって返される各項目をレンダリングします。

ListView のテンプレートを構成したら、web サイトにアクセスします。 図9に示すように、レッスンのセクションには、1つの箇条書き項目である [ホーム] が含まれています。 ContentPlaceHolder コントロールの概要と使用方法に関するレッスンはどこにありますか。 SiteMapDataSource は、階層構造のデータを返すように設計されていますが、ListView コントロールは階層の1つのレベルのみを表示できます。 その結果、SiteMapDataSource によって返されるサイトマップノードの最初のレベルのみが表示されます。

[レッスンセクションに1つのリスト項目が含まれて ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image15.png)

**図 09**: レッスンセクションに1つのリスト項目が含まれている ([クリックしてフルサイズの画像を表示する](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image17.png))

複数のレベルを表示するには、`ItemTemplate`内に複数の ListViews を入れ子にすることができます。 この手法は、「[データチュートリアルシリーズの使用](../../data-access/index.md)」の「 [*マスターページとサイトナビゲーション*のチュートリアル](../../data-access/introduction/master-pages-and-site-navigation-vb.md)」で確認しました。 ただし、このチュートリアルシリーズのサイトマップには、ホーム (最上位レベル) の2つのレベルのみが含まれます。そして、各レッスンはホームの子としてのものです。 入れ子になった ListView を構築するのではなく、その[`ShowStartingNode` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)を `False`に設定して、開始ノードを返さないように SiteMapDataSource に指示することができます。 実質的には、SiteMapDataSource は、サイトマップノードの第2層を返すことによって開始されます。

この変更により、ListView は、About and Using Multiple ContentPlaceHolder Controls レッスンの箇条書き項目を表示しますが、Home の箇条書き項目を省略します。 これを解決するには、`LayoutTemplate`に Home の箇条書き項目を明示的に追加します。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample11.aspx)]

開始ノードを省略し、Home 箇条書き項目を明示的に追加するように SiteMapDataSource を構成すると、レッスンのセクションには、意図した出力が表示されます。

[レッスンセクションに ![ホームと各子ノードの箇条書き項目が表示されます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image18.png)

**図 10**: レッスンのセクションには、ホームノードと各子ノードの箇条書き項目が含まれています ([クリックすると、フルサイズの画像が表示](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image20.png)されます)

### <a name="setting-the-title-based-on-the-site-map"></a>サイトマップに基づいてタイトルを設定する

サイトマップを使用して、`BasePage` クラスを更新して、サイトマップで指定されたタイトルを使用できるようにします。 手順2で行ったように、ページのタイトルがページの開発者によって明示的に設定されていない場合のみ、サイトマップノードのタイトルを使用します。 要求されているページに明示的に設定されたページタイトルがなく、サイトマップにも見つからない場合は、手順2で行ったように、要求されたページのファイル名 (拡張子の少ない方) を使用するようにフォールバックします。 図11は、この決定プロセスを示しています。

![ページタイトルが明示的に設定されていない場合は、対応するサイトマップノードのタイトルが使用されます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image21.png)

**図 11**: ページタイトルが明示的に設定されていない場合は、対応するサイトマップノードのタイトルが使用されます。

`BasePage` クラスの `OnLoadComplete` メソッドを更新して、次のコードを追加します。

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample12.vb)]

前と同様に、`OnLoadComplete` メソッドは、ページのタイトルが明示的に設定されているかどうかを判断することから始まります。 `Page.Title` が `Nothing`、空の文字列、または値 "無題のページ" が割り当てられている場合、コードは `Page.Title`に自動的に値を割り当てます。

使用するタイトルを決定するために、コードは、 [`SiteMap` クラス](https://msdn.microsoft.com/library/system.web.sitemap.aspx)の[`CurrentNode` プロパティ](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)を参照することによって開始されます。 `CurrentNode` は、現在要求されているページに対応するサイトマップ内の[`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)インスタンスを返します。 現在要求されているページがサイトマップ内に見つかった場合、`SiteMapNode`の `Title` プロパティがページのタイトルに割り当てられます。 現在要求されているページがサイトマップに含まれていない場合、`CurrentNode` は `Nothing` を返し、要求されたページのファイル名がタイトルとして使用されます (手順 2. で行ったとおり)。

図12は、ブラウザーを使用して表示するときの `MultipleContentPlaceHolders.aspx` ページを示しています。 このページのタイトルは明示的に設定されていないため、代わりに対応するサイトマップノードのタイトルが使用されます。

![MultipleContentPlaceHolders ページのタイトルがサイトマップからプルされます。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image22.png)

**図 12**: MultipleContentPlaceHolders ページのタイトルがサイトマップからプルされる

## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>手順 4:`<head>`セクションにページ固有のその他のマークアップを追加する

手順1、2、および3では、ページごとに `<title>` 要素をカスタマイズする方法を見てきました。 `<title>`に加えて、`<head>` セクションには `<meta>` 要素と `<link>` 要素が含まれる場合があります。 このチュートリアルで既に説明したように、`Site.master`の `<head>` セクションには `Styles.css`する `<link>` 要素が含まれています。 この `<link>` 要素はマスターページ内で定義されているため、すべてのコンテンツページの `<head>` セクションに含まれています。 しかし、`<meta>` と `<link>` の要素をページごとに追加するにはどうすればよいでしょうか。

`<head>` セクションにページ固有のコンテンツを追加する最も簡単な方法は、マスターページで ContentPlaceHolder コントロールを作成することです。 このような ContentPlaceHolder (名前は `head`) が既にあります。 したがって、カスタム `<head>` マークアップを追加するには、対応するコンテンツコントロールをページに作成し、そこにマークアップを配置します。

カスタム `<head>` マークアップをページに追加する方法を示すために、現在のコンテンツページのセットに `<meta>` description 要素を含めてみましょう。 `<meta>` description 要素は、web ページについての簡単な説明を提供します。ほとんどの検索エンジンでは、検索結果を表示するときに、この情報が何らかの形で組み込まれています。

`<meta>` description 要素には、次の形式があります。

[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample13.html)]

このマークアップをコンテンツページに追加するには、マスターページの `head` ContentPlaceHolder にマップされているコンテンツコントロールに上記のテキストを追加します。 たとえば、`Default.aspx`の `<meta>` description 要素を定義するには、次のマークアップを追加します。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample14.aspx)]

`head` ContentPlaceHolder は HTML ページの本文に含まれていないため、コンテンツコントロールに追加されたマークアップはデザインビューに表示されません。 `<meta>` description 要素を表示するには、ブラウザーを使用して `Default.aspx` にアクセスします。 ページが読み込まれたら、ソースを表示し、[`<head>`] セクションに、コンテンツコントロールで指定されたマークアップが含まれていることを確認します。

`About.aspx`、`MultipleContentPlaceHolders.aspx`、および `Login.aspx`に `<meta>` description 要素を追加します。

### <a name="programmatically-adding-markup-to-theheadregion"></a>プログラムによって`<head>`領域にマークアップを追加する

`head` ContentPlaceHolder を使用すると、マスターページの `<head>` 領域にカスタムマークアップを宣言によって追加できます。 カスタムマークアップは、プログラムで追加することもできます。 `Page` クラスの `Header` プロパティによって、マスターページ (`<head runat="server">`) で定義されている `HtmlHead` インスタンスが返されることを思い出してください。

`<head>` 領域にプログラムでコンテンツを追加できることは、追加するコンテンツが動的である場合に便利です。 たとえば、ページにアクセスしているユーザーに基づいています。データベースからプルされている可能性があります。 理由に関係なく、次のようにコントロールを `Controls` コレクションに追加することで、`HtmlHead` にコンテンツを追加できます。

[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample15.vb)]

上のコードでは、`<head>` 領域に `<meta>` keywords 要素を追加しています。これにより、ページを説明するキーワードのコンマ区切りリストが提供されます。 `<meta>` タグを追加するには、 [`HtmlMeta`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx)インスタンスを作成し、その `Name` と `Content` プロパティを設定して、`Header`の `Controls` コレクションに追加することに注意してください。 同様に、プログラムによって `<link>` 要素を追加するには、 [`HtmlLink`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx)オブジェクトを作成し、そのプロパティを設定して、`Header`の `Controls` コレクションに追加します。

> [!NOTE]
> 任意のマークアップを追加するには、 [`LiteralControl`](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx)インスタンスを作成し、その `Text` プロパティを設定して、`Header`の `Controls` コレクションに追加します。

## <a name="summary"></a>要約

このチュートリアルでは、`<head>` 領域のマークアップをページ単位で追加するさまざまな方法を見てきました。 マスターページには、ContentPlaceHolder を含む `HtmlHead` インスタンス (`<head runat="server">`) が含まれている必要があります。 `HtmlHead` インスタンスを使用すると、コンテンツページは、プログラムによって `<head>` 領域にアクセスしたり、ページのタイトルを宣言およびプログラムによって設定したりできます。ContentPlaceHolder コントロールを使用すると、カスタムマークアップをコンテンツコントロールを使用して宣言によって `<head>` セクションに追加できます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET でページのタイトルを動的に設定する](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP を調べています。NET のサイトナビゲーション](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [HTML メタタグの使用方法](http://searchenginewatch.com/showPage.html?page=2167931)
- [ASP.NET のマスターページ](http://www.odetocode.com/articles/419.aspx)
- [ASP.NET 3.5 の ListView コントロールと DataPager コントロールの使用](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET ページの分離コードクラスにカスタム基本クラスを使用する](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリーダーレビュー担当者は、Zack Jones と Suchi になりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](multiple-contentplaceholders-and-default-content-vb.md)
> [次へ](urls-in-master-pages-vb.md)
