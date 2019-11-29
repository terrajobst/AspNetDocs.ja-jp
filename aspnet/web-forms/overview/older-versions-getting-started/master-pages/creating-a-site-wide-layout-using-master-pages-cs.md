---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
title: マスターページを使用してサイト全体のレイアウトC#を作成する () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、マスターページの基本について説明します。 つまり、マスターページとは何か、どのようにしてマスターページを作成するか、コンテンツプレースホルダーとは何ですか。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 78f8d194-03b9-44a5-8255-90e7cd1c2ee1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a5e85c443a2a3642ec185ab1897c43cdb2ab1f7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619517"
---
# <a name="creating-a-site-wide-layout-using-master-pages-c"></a>マスター ページを利用してサイト全体レイアウトを作成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_CS.pdf)

> このチュートリアルでは、マスターページの基本について説明します。 つまり、マスターページとは何か、どのようにしてマスターページを作成するか、どのようにしてコンテンツプレースホルダーを作成するか、マスターページを使用する ASP.NET ページをどのように作成するか、マスターページの変更が関連するコンテンツページに自動的に反映されるかなどです。

## <a name="introduction"></a>はじめに

適切にデザインされた web サイトの1つの属性は、一貫したサイト全体のページレイアウトです。 たとえば、www.asp.net web サイトに移動します。 このドキュメントの執筆時点では、ページの上部と下部にすべてのページの内容が同じになっています。 図1に示すように、各ページの上部には、Microsoft コミュニティの一覧を含む灰色のバーが表示されます。 その下には、サイトのロゴ、サイトが翻訳された言語の一覧、および主要なセクションである [ホーム]、[はじめに]、[学習]、[ダウンロード] などがあります。 同様に、ページの下部には、www.asp.net の広告、著作権に関する声明、プライバシーに関する声明へのリンクが含まれています。

[www.asp.net の Web サイトでは、すべてのページで一貫したルックアンドフィールを採用している ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image1.png)

<strong>図 01</strong>: Www.asp.net web サイトは、すべてのページで一貫したルックアンドフィールを採用しています ([クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image3.png)されます)

適切に設計されたサイトのもう1つの属性は、サイトの外観を簡単に変更できるようにすることです。 図1は2008年3月の www.asp.net のホームページを示していますが、現在とこのチュートリアルの出版の間には、ルックアンドフィールが変更されている可能性があります。 場合によっては、上部にあるメニュー項目が展開され、MVC フレームワークの新しいセクションが追加されます。 または、色、フォント、レイアウトが異なる、新しいデザインが公開される可能性もあります。 サイト全体にこのような変更を適用するのは、サイトを構成する数千の web ページを変更する必要がない、高速で単純なプロセスである必要があります。

ASP.NET でサイト全体のページテンプレートを作成するには、*マスターページ*を使用します。 簡単に言うと、マスターページは、コンテンツページごとにカスタマイズ可能な領域だけでなく、すべての*コンテンツページ*で共通のマークアップを定義する特別な種類の ASP.NET ページです。 (コンテンツページは、マスターページにバインドされている ASP.NET ページです)。マスターページのレイアウトまたは書式設定が変更されると、そのすべてのコンテンツページの出力も同様に直ちに更新されるため、1つのファイル (つまり、マスターページ) を更新および展開するのと同じように、サイト全体の外観の変更が簡単に適用されます。

これは、マスターページの使用について説明する一連のチュートリアルの最初のチュートリアルです。 このチュートリアルシリーズでは、次のことを行います。

- マスターページとそれに関連するコンテンツページを作成する方法を確認します。
- さまざまなヒント、テクニック、およびトラップについて説明します。
- 一般的なマスターページの落とし穴を特定し、回避策を調べる
- コンテンツページからマスターページにアクセスする方法と、その逆の方法を参照してください。
- 実行時にコンテンツページのマスターページを指定する方法について説明します。
- その他の高度なマスターページのトピック。

これらのチュートリアルは簡潔にすることを目的としており、プロセスを視覚的に説明するためのさまざまなスクリーンショットを含む詳細な手順を説明しています。 各チュートリアルは、およびC# Visual Basic バージョンで使用でき、使用されている完全なコードのダウンロードが含まれています。

この初めチュートリアルでは、まずマスターページの基本について説明します。 ここでは、マスターページの動作について説明し、Visual Web Developer を使用してマスターページと関連するコンテンツページを作成する方法について説明します。また、マスターページに対する変更がコンテンツページに直ちに反映されるしくみについても説明します。 では、始めましょう。

## <a name="understanding-how-master-pages-work"></a>マスターページの動作について

サイト全体の一貫したページレイアウトで web サイトを構築するには、カスタムコンテンツに加えて、各 web ページで共通の書式設定マークアップを出力する必要があります。 たとえば、www.asp.net の各チュートリアルまたはフォーラムの投稿には独自のコンテンツがありますが、これらの各ページには、最上位のセクションリンク ([ホーム]、[はじめに]、[学習] など) を表示する一連の共通 `<div>` 要素も表示されます。

一貫したルックアンドフィールで web ページを作成するためのさまざまな方法があります。 単純な方法では、共通のレイアウトマークアップをコピーしてすべての web ページに貼り付けますが、この方法にはさまざまな欠点があります。 まず、新しいページが作成されるたびに、共有コンテンツをコピーしてページに貼り付ける必要があります。 共有マークアップのサブセットのみを新しいページに誤ってコピーする可能性があるため、このようなコピー操作や貼り付け操作はエラーに準備ます。 また、この方法では、サイト内のすべてのページを編集して新しいルックアンドフィールを使用する必要があるため、サイト全体の既存の外観を新しいものに置き換えることができます。

ASP.NET バージョン2.0 より前では、ページ開発者は通常、[ユーザーコントロール](https://msdn.microsoft.com/library/y6wb1a0e.aspx)に共通のマークアップを配置し、各ページにこれらのユーザーコントロールを追加しました。 この方法では、ページ開発者は、ユーザーコントロールをすべての新しいページに手動で追加することを覚えておく必要がありました。ただし、共通のマークアップを更新するときは、ユーザーコントロールのみを変更する必要があるため、サイト全体の変更が可能になります。 残念ながら、Visual Studio .NET 2002 および 2003-ASP.NET 1.x アプリケーションを作成するために使用される Visual Studio のバージョンは、灰色のボックスとしてデザインビューに表示されるユーザーコントロールです。 そのため、この方法を使用するページ開発者は、WYSIWYG デザイン時環境を利用できませんでした。

ユーザーコントロールを使用する場合の欠点は、ASP.NET バージョン2.0 と Visual Studio 2005 で、*マスターページ*の導入によって解決されました。 マスターページは、サイト全体のマークアップと、関連する*コンテンツページ*でカスタムマークアップが定義されている*領域*の両方を定義する、特殊な ASP.NET ページです。 手順1で説明したように、これらの領域は ContentPlaceHolder コントロールによって定義されています。 ContentPlaceHolder コントロールは、コンテンツページによってカスタムコンテンツを挿入できるマスターページのコントロール階層内の位置を示します。

> [!NOTE]
> マスターページの主要な概念と機能は、ASP.NET バージョン2.0 以降、変更されていません。 ただし、Visual Studio 2008 では、入れ子になったマスターページ (Visual Studio 2005 に欠けていた機能) のデザイン時サポートを提供しています。 入れ子になったマスターページの使用については、今後のチュートリアルで説明します。

図2は、www.asp.net のマスターページがどのように見えるかを示しています。 マスターページでは、一般的なサイト全体のレイアウトを定義しています。各ページの上部、下部、および右にマークアップがあります。また、ContentPlaceHolder は、各 web ページの固有のコンテンツが配置されている中央左にあります。

![マスターページでは、サイト全体のレイアウトと、コンテンツページごとに編集可能な領域を定義します。](creating-a-site-wide-layout-using-master-pages-cs/_static/image4.png)

**図 02**: マスターページでは、サイト全体のレイアウトと、コンテンツページごとに編集可能な領域を定義します。

マスターページを定義したら、チェックボックスの目盛りを通じて新しい ASP.NET ページにバインドすることができます。 これらの ASP.NET ページ (コンテンツページ) には、マスターページの ContentPlaceHolder コントロールごとにコンテンツコントロールが含まれています。 ブラウザーを使用してコンテンツページにアクセスすると、ASP.NET engine はマスターページのコントロール階層を作成し、コンテンツページのコントロール階層を適切な場所に挿入します。 この結合コントロール階層がレンダリングされ、結果の HTML がエンドユーザーのブラウザーに返されます。 その結果、コンテンツページは、マスターページで定義されている共通のマークアップを ContentPlaceHolder コントロールの外部に出力し、独自のコンテンツコントロール内に定義されているページ固有のマークアップを出力します。 図3は、この概念を示しています。

[要求されたページのマークアップがマスターページに ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image5.png)

**図 03**: 要求されたページのマークアップがマスターページに組み込まれている ([クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image7.png)されます)

これで、マスターページの動作について説明しました。次は、Visual Web Developer を使用してマスターページと関連するコンテンツページを作成する方法について説明します。

> [!NOTE]
> 最も多くのユーザーにリーチするために、このチュートリアルシリーズで作成する ASP.NET web サイトは、Microsoft の無償版の Visual Studio 2008、 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)を使用して ASP.NET 3.5 を使用して作成されます。 まだ ASP.NET 3.5 にアップグレードしていない場合は、心配しないでください。これらのチュートリアルで説明する概念は、ASP.NET 2.0 と Visual Studio 2005 でも同様に機能します。 ただし、一部のデモアプリケーションでは、.NET Framework バージョン3.5 の新機能を使用する場合があります。3.5 固有の機能が使用されている場合、バージョン2.0 で同様の機能を実装する方法について説明するメモを含めます。 各チュートリアルからダウンロードできるデモアプリケーションは .NET Framework バージョン3.5 を対象としているため、3.5 固有の構成要素を含む `Web.config` ファイルと、ASP.NET pages の分離コードクラスの `using` ステートメント内の3.5 固有の名前空間への参照が含まれていることに注意してください。 長期的には、コンピューターに .NET 3.5 をまだインストールしていない場合、`Web.config`から3.5 固有のマークアップを最初に削除しないと、ダウンロード可能な web アプリケーションは動作しません。 このトピックの詳細については、「[解説 ASP.NET Version 3.5 の `Web.config` ファイル](http://www.4guysfromrolla.com/articles/121207-1.aspx)」を参照してください。 また、3.5 固有の名前空間を参照する `using` ステートメントも削除する必要があります。

## <a name="step-1-creating-a-master-page"></a>手順 1: マスターページの作成

マスターページとコンテンツページの作成と使用の詳細については、まず ASP.NET web サイトが必要です。 まず、新しいファイルシステムベースの ASP.NET web サイトを作成します。 これを行うには、Visual Web Developer を起動して [ファイル] メニューにアクセスし、[新しい Web サイト] をクリックします。 [新しい Web サイト] ダイアログボックスが表示されます (図4を参照)。 ASP.NET Web サイトテンプレートを選択し、[場所] ドロップダウンリストを [ファイルシステム] に設定して、Web サイトを配置するフォルダーを選択C#し、言語をに設定します。 これにより、`Default.aspx` ASP.NET ページ、`App_Data` フォルダー、および `Web.config` ファイルを含む新しい web サイトが作成されます。

> [!NOTE]
> Visual Studio では、2つのプロジェクト管理モード (Web サイトプロジェクトと Web アプリケーションプロジェクト) がサポートされています。 Web サイトプロジェクトにはプロジェクトファイルがありませんが、Web アプリケーションプロジェクトは Visual Studio .NET 2002/2003 のプロジェクトアーキテクチャに似ています。プロジェクトファイルが含まれ、プロジェクトのソースコードが1つのアセンブリにコンパイルされ、`/bin` フォルダーに配置されます。 Visual Studio 2005 は、web[アプリケーションプロジェクトモデル](https://msdn.microsoft.com/library/aa730880(vs.80).aspx)が Service Pack 1 で導入されましたが、最初はサポートされている Web サイトプロジェクトのみです。Visual Studio 2008 では、両方のプロジェクトモデルが提供されます。 ただし、Visual Web Developer 2005 と2008の各エディションでは、Web サイトプロジェクトのみがサポートされます。 このチュートリアルシリーズのデモでは、Web サイトプロジェクトモデルを使用します。 Express 以外のエディションを使用していて、代わりに Web アプリケーションプロジェクトモデルを使用する場合は、自由に選択してください。ただし、画面に表示される内容と、表示される手順およびスクリーンショットと instructio の間にはいくつかの不一致がある可能性があることに注意してください。このチュートリアルで提供されている ns。

[新しいファイルシステムベースの Web サイトを作成 ![には](creating-a-site-wide-layout-using-master-pages-cs/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image8.png)

**図 04**: 新しいファイルシステムベースの Web サイトを作成[する (クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image10.png)されます)

次に、ルートディレクトリ内のサイトにマスターページを追加します。そのためには、プロジェクト名を右クリックし、[新しい項目の追加] を選択して、マスターページテンプレートを選択します。 マスターページの末尾には `.master`拡張子が付いていることに注意してください。 この新しいマスターページの名前を `Site.master`、[追加] をクリックします。

[Website という名前のマスターページを Web サイトに追加 ![には](creating-a-site-wide-layout-using-master-pages-cs/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image11.png)

**図 05**: `Site.master` という名前のマスターページを web サイトに追加する ([クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image13.png)されます)

Visual Web Developer を使用して新しいマスターページファイルを追加すると、次の宣言型マークアップを持つマスターページが作成されます。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample1.aspx)]

宣言マークアップの最初の行は、 [`@Master` ディレクティブ](https://msdn.microsoft.com/library/ms228176.aspx)です。 `@Master` ディレクティブは、ASP.NET ページに表示される[`@Page` ディレクティブ](https://msdn.microsoft.com/library/ydy4x04a.aspx)に似ています。 サーバー側の言語 (C#) と、マスターページの分離コードクラスの場所と継承に関する情報を定義します。

`DOCTYPE` とページの宣言マークアップが `@Master` ディレクティブの下に表示されます。 このページには、次の4つのサーバー側コントロールと共に、静的 HTML が含まれています。

- **Web フォーム (`<form runat="server">`)** 。通常、すべての ASP.NET ページには web フォームがあります。また、マスターページには web フォーム内に表示する必要がある web コントロールが含まれる場合があるため、web フォームを各コンテンツページに追加するのではなく、マスターページに追加してください。
- **`ContentPlaceHolder1`という名前の ContentPlaceHolder コントロール**-この ContentPlaceHolder コントロールは Web フォーム内に表示され、コンテンツページのユーザーインターフェイスの領域として機能します。
- **サーバー側の `<head>` 要素**-`<head>` 要素には `runat="server"` 属性があるため、サーバー側のコードを使用してアクセスできます。 `<head>` 要素は、ページのタイトルとその他の `<head>`関連のマークアップがプログラムによって追加または調整されるように、この方法で実装されます。 たとえば、ASP.NET ページの `Title` プロパティを設定すると、`<head>` サーバーコントロールによって表示される `<title>` 要素が変更されます。
- **`head`という名前の ContentPlaceHolder コントロール**-この ContentPlaceHolder コントロールは、`<head>` サーバーコントロール内に表示され、`<head>` 要素にコンテンツを宣言によって追加するために使用できます。

この既定のマスターページ宣言型マークアップは、独自のマスターページを設計するための出発点として機能します。 HTML を自由に編集したり、Web コントロールや ContentPlaceHolders をマスターページに追加したりすることができます。

> [!NOTE]
> マスターページをデザインするときは、マスターページに Web フォームが含まれていることと、少なくとも1つの ContentPlaceHolder コントロールがこの Web フォーム内に表示されていることを確認してください。

### <a name="creating-a-simple-site-layout"></a>単純なサイトレイアウトの作成

次に、`Site.master`の既定の宣言マークアップを展開して、すべてのページが共有するサイトレイアウトを作成します。共通ヘッダー。ナビゲーション、ニュース、およびその他のサイト全体のコンテンツを含む左の列。"電源付き Microsoft ASP.NET" アイコンが表示されるフッター。 図6は、そのコンテンツページの1つがブラウザーで表示されたときのマスターページの最終的な結果を示しています。 図6の赤い丸で囲まれた領域は、アクセスされているページ (`Default.aspx`) に固有です。その他のコンテンツはマスターページで定義されるため、すべてのコンテンツページで一貫しています。

[マスターページ ![、上、左、および下の部分のマークアップを定義します。](creating-a-site-wide-layout-using-master-pages-cs/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image14.png)

**図 06**: マスターページでは、上、左、下の部分のマークアップを定義します ([クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image16.png)されます)

図6に示されているサイトレイアウトを実現するには、まず `Site.master` マスターページを更新して、次の宣言型マークアップが含まれるようにします。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample2.aspx)]

マスターページのレイアウトは、一連の `<div>` HTML 要素を使用して定義されます。 `topContent` `<div>` には、各ページの上部に表示されるマークアップが含まれています。また、`mainContent`、`leftContent`、および `footerContent` `<div>` を使用して、ページのコンテンツ、左の列、および "機能強化 Microsoft ASP.NET" アイコンをそれぞれ表示します。 これらの `<div>` 要素を追加するだけでなく、プライマリ ContentPlaceHolder コントロールの `ID` プロパティの名前も `ContentPlaceHolder1` から `MainContent`に変更しました。

これらの類別された `<div>` 要素の書式設定とレイアウトの規則は、[カスケードスタイルシート (CSS)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets)ファイル `Styles.css`に記載されています。このファイルは、マスターページの &lt;ヘッド&gt; 要素の &lt;リンク&gt; 要素によって指定されます。 これらのさまざまな規則では、上記の各 `<div>` 要素の外観を定義します。 たとえば、"マスターページチュートリアル" のテキストとリンクを表示する `topContent` `<div>` 要素には、`Styles.css` で次のように指定された書式規則があります。

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample3.css)]

コンピューターに従っている場合は、このチュートリアルに付属するコードをダウンロードし、`Styles.css` ファイルをプロジェクトに追加する必要があります。 同様に、Images という名前のフォルダーを作成し、ダウンロードしたデモ web サイトからプロジェクトに "Microsoft ASP.NET" をコピーすることも必要になります。

> [!NOTE]
> CSS と web ページの書式設定の詳細については、この記事では説明しません。 CSS の詳細については、 [W3Schools.com](http://www.w3schools.com/)の[css チュートリアル](http://www.w3schools.com/css/default.asp)を参照してください。 また、このチュートリアルの付随するコードをダウンロードし、`Styles.css` の CSS 設定を使用して、さまざまな書式規則の効果を確認することをお勧めします。

### <a name="creating-a-master-page-using-an-existing-design-template"></a>既存のデザインテンプレートを使用してマスターページを作成する

長年にわたり、小規模から中規模の企業向けに、多数の ASP.NET web アプリケーションを構築しました。 一部のクライアントには、使用したい既存のサイトレイアウトがあります。他の人は、有能なグラフィックスデザイナーを採用しています。 Web サイトのレイアウトを設計するためのいくつかの委任。 図6でわかるように、プログラマが web サイトのレイアウトを設計するための作業は、一般に、医師が税金を出している間にオープン・ハートの手術を行うようにしてください。

幸いなことに、HTML デザインテンプレートを無料で提供する web サイトがたくさんあります。 Google からは、"無料の web サイトテンプレート" という検索用語に対して600万を超える結果が返されました。 お気に入りの1つは[OpenDesigns.org](http://opendesigns.org/)です。好みの web サイトテンプレートが見つかったら、web サイトプロジェクトに CSS ファイルとイメージを追加し、そのテンプレートの HTML をマスターページに統合します。

> [!NOTE]
> Microsoft では、Visual Studio の [新しい Web サイト] ダイアログボックスに統合される、[無料の ASP.NET Design スタートキットテンプレート](https://msdn.microsoft.com/asp.net/aa336613.aspx)も多数用意されています。

## <a name="step-2-creating-associated-content-pages"></a>手順 2: 関連するコンテンツページを作成する

マスターページを作成したので、マスターページにバインドされている ASP.NET ページの作成を開始できます。 このようなページは、*コンテンツページ*と呼ばれます。

新しい ASP.NET ページをプロジェクトに追加し、`Site.master` マスターページにバインドしてみましょう。 ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] オプションを選択します。 [Web フォーム] テンプレートを選択して `About.aspx`名前を入力し、図7に示すように [マスターページの選択] チェックボックスをオンにします。 この操作を行うと、[マスターページの選択] ダイアログボックスが表示されます (図8を参照)。ここで、使用するマスターページを選択できます。

> [!NOTE]
> Web サイトプロジェクトモデルではなく、Web アプリケーションプロジェクトモデルを使用して ASP.NET web サイトを作成した場合は、図7に示すように、[新しい項目の追加] ダイアログボックスの [マスターページの選択] チェックボックスは表示されません。 Web アプリケーションプロジェクトモデルを使用するときにコンテンツページを作成するには、web フォームテンプレートではなく、Web コンテンツフォームテンプレートを選択する必要があります。 [Web コンテンツフォーム] テンプレートを選択し、[追加] をクリックすると、図8に示されているのと同じ [マスターページの選択] ダイアログボックスが表示されます。

[新しいコンテンツページを追加 ![には](creating-a-site-wide-layout-using-master-pages-cs/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image17.png)

**図 07**: 新しいコンテンツページを追加[する (クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image19.png)される)

[[] ![選択します。](creating-a-site-wide-layout-using-master-pages-cs/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image20.png)

**図 08**: `Site.master` マスターページを選択[する (クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image22.png)されます)

次の宣言型マークアップに示すように、新しいコンテンツページには `@Page` ディレクティブが含まれています。このディレクティブは、マスターページと、各マスターページの ContentPlaceHolder コントロールのコンテンツコントロールを参照します。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample4.aspx)]

> [!NOTE]
> 手順 1. の [単純なサイトレイアウトの作成] セクションで、`ContentPlaceHolder1` 名前を `MainContent`に変更しました。 同じ方法でこの ContentPlaceHolder コントロールの `ID` の名前を変更しなかった場合、コンテンツページの宣言型のマークアップは、上に示したマークアップとは若干異なります。 つまり、2番目のコンテンツコントロールの `ContentPlaceHolderID` には、マスターページ内の対応する ContentPlaceHolder コントロールの `ID` が反映されます。

コンテンツページをレンダリングする場合、ASP.NET エンジンは、ページのコンテンツコントロールとそのマスターページの ContentPlaceHolder コントロールをヒューズする必要があります。 ASP.NET エンジンは、`@Page` ディレクティブの `MasterPageFile` 属性からコンテンツページのマスターページを決定します。 上のマークアップに示すように、このコンテンツページは `~/Site.master`にバインドされています。

マスターページには `head` と `MainContent` の2つの ContentPlaceHolder コントロールがあるため、Visual Web Developer では2つのコンテンツコントロールが生成されました。 各コンテンツコントロールは、`ContentPlaceHolderID` プロパティを介して特定の ContentPlaceHolder を参照します。

以前のサイト全体のテンプレート手法を使用した場合、デザイン時サポートがあります。 図9に、Visual Web Developer のデザインビューで表示する場合の `About.aspx` コンテンツページを示します。 マスターページのコンテンツは表示されていても、グレーで表示され、変更できないことに注意してください。 ただし、マスターページの ContentPlaceHolders に対応するコンテンツコントロールは編集できます。 他の ASP.NET ページと同様に、ソースビューまたはデザインビューを介して Web コントロールを追加することにより、コンテンツページのインターフェイスを作成できます。

[コンテンツページのデザインビューにページ固有のコンテンツとマスターページのコンテンツの両方が表示される ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image23.png)

**図 09**: コンテンツページのデザインビューにページ固有のコンテンツとマスターページのコンテンツの両方が表示される ([クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image25.png)されます)

### <a name="adding-markup-and-web-controls-to-the-content-page"></a>コンテンツページにマークアップと Web コントロールを追加する

`About.aspx` ページのコンテンツを作成します。 図10に示すように、「著者について」という見出しとテキストの段落を入力しましたが、Web コントロールも自由に追加できます。 このインターフェイスを作成したら、ブラウザーを使用して `About.aspx` のページにアクセスします。

[ブラウザーから About .aspx ページにアクセス ![には](creating-a-site-wide-layout-using-master-pages-cs/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image26.png)

**図 10**: ブラウザーを使用して `About.aspx` のページにアクセス[する (クリックすると、フルサイズの画像が表示](creating-a-site-wide-layout-using-master-pages-cs/_static/image28.png)されます)

要求されたコンテンツページとそれに関連付けられているマスターページは、すべて web サーバー上で全体として表示されることを理解しておくことが重要です。 その後、エンドユーザーのブラウザーに、結果として、ヒューズが付いた HTML が送信されます。 これを確認するには、ブラウザーで受信した HTML を表示するには、[表示] メニューの [ソース] をクリックします。 2つの異なる web ページを1つのウィンドウに表示するためのフレームまたはその他の特別な技法はありません。

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>既存の ASP.NET ページへのマスターページのバインド

この手順で説明したように、新しいコンテンツページを ASP.NET web アプリケーションに追加するのは、[マスターページの選択] チェックボックスをオンにしてマスターページを選択するのと同じように簡単です。 残念ながら、既存の ASP.NET ページをマスターページに変換するのは簡単ではありません。

マスターページを既存の ASP.NET ページにバインドするには、次の手順を実行する必要があります。

1. ASP.NET ページの `@Page` ディレクティブに `MasterPageFile` 属性を追加して、適切なマスターページをポイントします。
2. マスターページ内の各 ContentPlaceHolders ホルダーのコンテンツコントロールを追加します。
3. ASP.NET ページの既存のコンテンツを選択的に切り取って、適切なコンテンツコントロールに貼り付けます。 ASP.NET ページには、マスターページで既に表現されているマークアップ (`DOCTYPE`、`<html>` 要素、Web フォームなど) が含まれている可能性があるため、ここでは "選択的" と言います。

このプロセスの詳細な手順については、「[マスターページとサイトナビゲーション](http://webproject.scottgu.com/CSharp/MasterPages/MasterPages.aspx)[の](https://weblogs.asp.net/scottgu/)使用」チュートリアルを参照してください。 これらの手順の詳細については、「マスターページを使用するための `Default.aspx` の更新と `DataSample.aspx`」セクションを参照してください。

既存の ASP.NET ページをコンテンツページに変換するよりも、新しいコンテンツページを作成する方がはるかに簡単であるため、新しい ASP.NET web サイトを作成するときは常に、マスターページをサイトに追加することをお勧めします。 すべての新しい ASP.NET ページをこのマスターページにバインドします。 最初のマスターページが非常に単純であるか、またはシンプルであるかは心配しないでください。マスターページは後で更新できます。

> [!NOTE]
> 新しい ASP.NET アプリケーションを作成するときに、Visual Web Developer によって、マスターページにバインドされていない `Default.aspx` ページが追加されます。 既存の ASP.NET ページをコンテンツページに変換する場合は、`Default.aspx`で実行します。 または、`Default.aspx` 削除してからもう一度追加することもできますが、今回は [マスターページの選択] チェックボックスをオンにします。

## <a name="step-3-updating-the-master-pages-markup"></a>手順 3: マスターページのマークアップの更新

マスターページの主な利点の1つは、1つのマスターページを使用して、サイト上の多数のページの全体的なレイアウトを定義できることです。 そのため、サイトの外観を更新するには、1つのファイル (マスターページ) を更新する必要があります。

この動作を説明するために、マスターページを更新して、現在の日付を左側の列の上部に追加してみましょう。 `DateDisplay` という名前のラベルを `leftContent` `<div>`に追加します。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample5.aspx)]

次に、マスターページの `Page_Load` イベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample6.cs)]

上のコードでは、ラベルの `Text` プロパティが、曜日、月の名前、および2桁の日として書式設定された現在の日付と時刻に設定されています (図11を参照)。 この変更により、コンテンツページのいずれかを再利用します。 図11に示すように、結果として得られるマークアップは、マスターページへの変更を含むように直ちに更新されます。

[[コンテンツ] ページを表示すると、マスターページへの変更が反映され ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image29.png)

**図 11**: コンテンツページを表示するときにマスターページへの変更が反映される ([クリックしてフルサイズの画像を表示する](creating-a-site-wide-layout-using-master-pages-cs/_static/image31.png))

> [!NOTE]
> この例に示すように、マスターページには、サーバー側の Web コントロール、コード、およびイベントハンドラーが含まれている場合があります。

## <a name="summary"></a>要約

マスターページを使用すると、ASP.NET の開発者は、簡単に更新できる一貫したサイト全体のレイアウトを設計できます。 Visual Web Developer では、豊富なデザイン時サポートが提供されているため、マスターページとそれに関連するコンテンツページを作成するのは簡単です。

このチュートリアルで作成したマスターページの例には、`head` と `MainContent`という2つの ContentPlaceHolder コントロールがありました。 ただし、コンテンツページでは、`MainContent` ContentPlaceHolder コントロールにマークアップを指定しただけです。 次のチュートリアルでは、コンテンツページの複数のコンテンツコントロールの使用について説明します。 また、マスターページ内のコンテンツコントロールの既定のマークアップを定義する方法に加えて、マスターページで定義されている既定のマークアップを使用したり、コンテンツページからカスタムマークアップを提供したりする方法についても説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET for Designer: Web 標準を使用して ASP.NET Websites を構築するための無料の設計テンプレートとガイダンス](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET マスターページの概要](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [カスケードスタイルシート (CSS) のチュートリアル](http://www.w3schools.com/css/default.asp)
- [ページのタイトルを動的に設定する](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP.NET のマスターページ](http://www.odetocode.com/articles/419.aspx)
- [マスターページのクイックスタートチュートリアル](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [次へ](multiple-contentplaceholders-and-default-content-cs.md)
