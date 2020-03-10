---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC での Page Inspector の使用 |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。 統合ブラウザーで任意の要素を選択し、Page Inspector します...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432454"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a>ASP.NET MVC フォーム内での Page Inspector の使用

Tim Ammann

> Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。 統合ブラウザーで任意の要素を選択すると、Page Inspector 要素のソースと CSS が瞬時に強調表示されます。 任意の MVC ビューを参照したり、表示されているマークアップのソースをすばやく検索したり、Visual Studio 環境内でブラウザーツールを使用したりすることができます。
> 
> [ビデオを見る](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> このチュートリアルでは、検査モードを有効にし、web プロジェクト内でマークアップと CSS をすばやく検索して編集する方法について説明します。 このチュートリアルでは MVC プロジェクトを使用しますが、 [Web フォーム](https://go.microsoft.com/?linkid=9802001)や他の ASP.NET アプリケーションには Page Inspector を使用することもできます。
> 
> このチュートリアルには、次のセクションがあります。
> 
> - [前提条件](#_1_prerequisites)
> - [Web アプリケーションを作成する](#_2_creating_a)
> - [Page Inspector を使用してビューを参照する](#_3_using_page)
> - [検査モードを有効にする](#_4_inspection_mode)
> - [Page Inspector を使用してマークアップを変更する](#_5_using_page)
> - [検査モードと HTML ウィンドウ](#_6_inspection_mode)
> - [[スタイル] ウィンドウでの CSS の変更のプレビュー](#_7_previewing_css)
> - [CSS 自動同期](#css_auto_sync)
> - [CSS カラーピッカーの使用](#css_color_picker)
> - [動的ページ要素の JavaScript へのマッピング](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>前提条件

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)または[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。

> [!NOTE]
> 最新バージョンの Page Inspector を取得するには、 [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)を使用して WINDOWS Azure SDK for .net 2.0 をインストールします。

Page Inspector は Microsoft Web Developer Tools にバンドルされています。 最新バージョンは1.3 です。 使用しているバージョンを確認するには、Visual Studio を実行し、 **[ヘルプ]** メニューから バージョン **[情報 Microsoft Visual Studio]** を選択します。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>Web アプリケーションを作成する

まず、で Page Inspector 使用する web アプリケーションを作成します。 Visual Studio で、[**ファイル**&gt;**新しいプロジェクト**] を選択します。 左側で **[ C#ビジュアル]** を展開し、 **[Web]** を選択して、 **[ASP.NET MVC4 Web アプリケーション]** を選択します。

![新しい ASP.NET MVC アプリケーション](using-page-inspector-in-aspnet-mvc/_static/image2.png)

**[OK]** をクリックします。

**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択します。 既定のビューエンジンとして**Razor**をそのまま使用します。

![New ASP.NET MVC プロジェクト-インターネットアプリケーション](using-page-inspector-in-aspnet-mvc/_static/image4.png)

アプリケーションが**ソース**ビューで開きます。

![ソースビューの新しい ASP.NET MVC アプリケーション](using-page-inspector-in-aspnet-mvc/_static/image6.png)

アプリケーションを操作できるようになったので、Page Inspector を使用して確認し、変更することができます。

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>Page Inspector を使用してビューを参照する

Visual Studio 2012 では、プロジェクト内の任意のビューを右クリックして **[Page Inspector で表示]** を選択すると、ルートが Page Inspector 表示され、ページが表示されます。

**ソリューションエクスプローラー**で、 **Views**フォルダーを展開し、 **[ホーム]** フォルダーを展開します。 Index. cshtml ファイルを右クリックし、 **[Page Inspector で表示]** を選択します。

![Page Inspector でのインデックスの表示](using-page-inspector-in-aspnet-mvc/_static/image8.png)

既定では、Page Inspector は、Visual Studio 環境の左側にウィンドウとしてドッキングされます。 必要に応じて、他の場所にドッキングしたり、ウィンドウをドッキング解除したりすることができます。 「[方法: ウィンドウを整列およびドッキングする](https://msdn.microsoft.com/library/z4y0hsax.aspx)」を参照してください。

[Page Inspector] ウィンドウの上部ペインに、ブラウザーウィンドウに現在のページが表示されます。 下部のペインには、HTML マークアップのページと、ページのさまざまな側面を調べるためのタブが表示されます。 下のウィンドウは、Internet Explorer の[F12 開発者ツール](https://msdn.microsoft.com/ie/aa740478)に似ています。

![Page Inspector での ASP.NET MVC アプリケーション](using-page-inspector-in-aspnet-mvc/_static/image10.png)

このチュートリアルでは、 **[HTML]** タブと **[スタイル]** タブを使用してすばやく移動し、アプリケーションに変更を加えます。

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>EnableInspection モード

Page Inspector を検査モードに配置するには、 **[検査]** ボタンをクリックします。 検査モードでは、表示されるページの任意の部分にマウスポインターを置くと、対応するソースマークアップまたはコードが強調表示されます。

![検査モードの切り替え](using-page-inspector-in-aspnet-mvc/_static/image12.png)

次に、Page Inspector 内のページのさまざまな部分にマウスを移動します。 この操作を行うと、マウスポインターが大きなプラス記号に変わり、下の要素が強調表示されます。

![Div にカーソルを合わせる-ラッパー](using-page-inspector-in-aspnet-mvc/_static/image14.png)

マウスポインターを移動すると、Visual Studio によって、ソースファイル内の対応する Razor 構文が強調表示されます。 HTML 要素が別のソースファイルから取得された場合は、Visual Studio によってファイルが自動的に開きます。

Page Inspector では、Razor 構文から生成された HTML が **[html]** タブに表示されます。 マウスポインターを移動すると、HTML 要素が強調表示されます。 **[スタイル]** タブには、要素の CSS ルールが表示されます。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>Page Inspector を使用してマークアップを変更する

Page Inspector を使用すると、場所が明確でないマークアップを見つけることができます。 その後、マークアップを変更し、結果の変更を確認できます。

これを表示するには、**検査** をクリックし、Page Inspector ウィンドウでページの一番下までスクロールします。

マウスポインターをフッター領域に移動すると、Page Inspector によって \_Layout ファイルが開き、選択したレイアウトページのセクションが強調表示されます。 ご覧のように、フッターはレイアウトファイルで定義されており、ビュー自体では定義されていません。

![フッター](using-page-inspector-in-aspnet-mvc/_static/image16.png)

次に、著作権<a id="a"></a>に関する通知を使用して、マウスポインターを行の上に移動します。 \_Layout ページで、対応する行が強調表示されます。

![フッターの著作権線が強調表示されます](using-page-inspector-in-aspnet-mvc/_static/image18.png)

\_Layout. cshtml ファイル内の行の末尾にテキストを追加します。

&lt;p&gt;&amp;コピーです。@DateTime.Now.Year-マイ ASP.NET MVC アプリケーションは、&lt;/p&gt;

ここで、Ctrl + Alt + Enter キーを押すか、更新バーをクリックして Page Inspector ブラウザーウィンドウに結果を表示します。

![私の ASP.NET アプリケーションは岩を持っています。](using-page-inspector-in-aspnet-mvc/_static/image20.png)

このフッターは、Index. cshtml で定義されているように思われるかもしれませんが、\_Layout. cshtml に入っているので、Page Inspector 見つかりました。

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>検査モードと HTML ウィンドウ

次に、HTML ウィンドウと、要素をどのようにマップするかを簡単に説明します。

**[検査]** をクリックして、検査モードに Page Inspector を配置します。

ページの一番上の部分をクリックします。 [ここにロゴを入力してください] と表示されます。 特定の要素を詳細に調べているため、マウスポインターを移動しても、ブラウザーウィンドウの表示が変更されなくなりました。

次に、マウスポインターを**HTML**ウィンドウに移動します。 マウスポインターを移動すると、Page Inspector **HTML**ウィンドウ内の要素のアウトラインが表示され、ブラウザーウィンドウ内の対応する要素が強調表示されます。

![HTML ウィンドウ](using-page-inspector-in-aspnet-mvc/_static/image22.png)

以前と同様に、Page Inspector は、一時タブで \_Layout ファイルを開きます。 [\_Layout] をクリックすると、対応するマークアップが &lt;ヘッダー&gt; セクションで強調表示されます。

![強調表示されたマークアップ](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>[スタイル] ウィンドウでの CSS の変更のプレビュー

次に、[Page Inspector**スタイル**] ウィンドウを使用して、CSS の変更をプレビューします。

**[検査]** をクリックして、検査モードに Page Inspector を配置します。

Page Inspector ブラウザーウィンドウで、ホームページ セクションの上にマウスポインターを移動し、 **div** と表示されるようにします。

![Div にカーソルを合わせる-ラッパー](using-page-inspector-in-aspnet-mvc/_static/image26.png)

Div のコンテンツラッパーセクション内を1回クリックし、マウスポインターを **[スタイル]** ウィンドウに移動します。 **[スタイル]** ウィンドウには、この要素のすべての CSS ルールが表示されます。 下にスクロールして、... コンテンツラッパークラスセレクターを見つけます。 次に、[背景色] プロパティのチェックボックスをオフにします。

![背景色のクリア](using-page-inspector-in-aspnet-mvc/_static/image28.png)

Page Inspector ブラウザーウィンドウに変更がすぐに表示されます。

もう一度チェックボックスをオンにし、プロパティ値をダブルクリックして、赤に変更します。 変更はすぐに表示されます。

![赤の背景色](using-page-inspector-in-aspnet-mvc/_static/image30.png)

**[スタイル]** ウィンドウを使用すると、スタイルシート自体に変更をコミットする前に、CSS の変更を簡単にテストおよびプレビューできます。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自動同期

> [!NOTE]
> この機能には Page Inspector のバージョン1.3 が必要です。

CSS 自動同期機能を使用すると、CSS ファイルを直接編集し、Page Inspector ブラウザーですぐに変更を確認することができます。

**[検査]** をクリックして、検査モードに Page Inspector を配置します。

Page Inspector ブラウザーで、[ホームページ] セクションの上にマウスポインターを移動**します。このラベルが**表示されます。 この要素を選択するには、[1 回] をクリックします。

**[スタイル]** ウィンドウには、この要素のすべての CSS ルールが表示されます。 下にスクロールして、... コンテンツラッパークラスセレクターを見つけます。 [... コンテンツ-ラッパー] をクリックします。 Page Inspector によって、このスタイル (.css) を定義する CSS ファイルが開き、対応する CSS スタイルが強調表示されます。

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

次に、`background-color` の値を "red" に変更します。 変更は、Page Inspector ブラウザーに直ちに表示されます。

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>CSS カラーピッカーの使用

Visual Studio 2012 の CSS エディターには、色の選択と挿入を簡単に行うことができるカラーピッカーが用意されています。 カラーピッカーには標準の色パレットが含まれており、標準の色の名前、ハッシュコード、RGB、RGBA、HSL、および HSLA の色をサポートし、ドキュメントで最近使用した色の一覧を保持します。

前のセクションでは、`background-color` プロパティの値を変更しました。 カラーピッカーを呼び出すには、プロパティ名の後に挿入ポイントを置き、 **#** または**rgb (** ) を入力します。

![CSS カラーピッカーバー](using-page-inspector-in-aspnet-mvc/_static/image36.png)

色をクリックして選択するか、下方向キーを押して、左方向キーと右方向キーを使用して色を走査します。 色にアクセスすると、対応する16進値がプレビューされます。

![背景色のプロパティ値のプレビュー](using-page-inspector-in-aspnet-mvc/_static/image38.png)

カラーバーに必要な色が設定されていない場合は、カラーピッカーのポップアップを使用できます。 これを開くには、カラーバーの右端にある二重シェブロンをクリックするか、キーボードの下方向キーを1回または2回押します。

![CSS カラーピッカーのポップアップ](using-page-inspector-in-aspnet-mvc/_static/image40.png)

右側の垂直バーから色をクリックします。 これにより、メインウィンドウにその色のグラデーションが表示されます。 Enter キーを押して縦棒から直接色を選択するか、メインウィンドウ内の任意のポイントをクリックして有効桁数を高くします。

使用する色がコンピューターの画面に表示される場合は (Visual Studio のユーザーインターフェイス内に存在する必要はありません)、右下にあるスポイトツールを使用して値をキャプチャできます。

カラーピッカーの下部にあるスライダーを動かすことで、色の不透明度を変更することもできます。 これにより色の値が RGBA 値に変更されます。 RGBA 形式は不透明度を表す可能性があるためです。

色を選択したら、enter キーを押し、セミコロンを入力して、*サイトの .css*ファイルの背景色のエントリを完成させます。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Page Inspector 更新バー

Page Inspector は、直ちに*サイトの .css*ファイルへの変更を検出し、更新バーにアラートを表示します。

![更新バー](using-page-inspector-in-aspnet-mvc/_static/image42.png)

すべてのファイルを保存して Page Inspector ブラウザーを更新するには、Ctrl + Alt + Enter キーを押すか、更新バーをクリックします。 強調表示色の変更がブラウザーに表示されます。

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>動的ページ要素の JavaScript へのマッピング

最新の web アプリケーションでは、多くの場合、ページ内の要素が JavaScript で動的に生成されます。 つまり、これらのページ要素に対応する静的マークアップ (HTML または Razor) はありません。

バージョン1.3 では、Page Inspector は、ページに動的に追加された項目を対応する JavaScript コードにマップできるようになりました。 この機能を説明するために、[シングルページアプリケーション (SPA) テンプレート](../../../single-page-application/overview/introduction/knockoutjs-template.md)を使用します。

> [!NOTE]
> SPA テンプレートには、 [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650)の更新プログラムが必要です。

Visual Studio で、[**ファイル**&gt;**新しいプロジェクト**] を選択します。 左側で **[ C#ビジュアル]** を展開し、 **[Web]** を選択して、 **[ASP.NET MVC4 Web アプリケーション]** を選択します。 **[OK]** をクリックします。

**[新しい ASP.NET MVC 4 プロジェクト]** ダイアログで、 **[シングルページアプリケーション]** を選択します。

ソリューションエクスプローラーで、 **Views**フォルダーを展開し、 **[ホーム]** フォルダーを展開します。 Index. cshtml ファイルを右クリックし、 **[Page Inspector で表示]** を選択します。

Page Inspector ブラウザーに最初に表示されるのは、ログインページです。 [サインアップ] をクリックし、ユーザー名とパスワードを作成します。 サインアップすると、アプリケーションがログインし、いくつかのサンプル項目を含む to do リストを作成します。

**[検査]** をクリックして、検査モードに Page Inspector を配置します。 Page Inspector ブラウザーで、to do 項目の1つをクリックします。 青で強調表示されるのではなく、要素がオレンジ色で強調表示され、要素名の横に "JS" が付いていることに注意してください。 これは、要素がスクリプトによって動的に作成されたことを示します。

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

さらに、 **[呼び出し履歴]** タブにはオレンジ色の下線が表示されます。これは、 **[呼び出し履歴]** ウィンドウに要素に関する詳細情報が含まれていることを示します。

**[呼び出し履歴]** タブをクリックします。 **[呼び出し履歴]** ウィンドウには、要素を作成した JavaScript 呼び出しの呼び出し履歴が表示されます。 JQuery などの外部ライブラリへの呼び出しは折りたたまれているので、アプリケーションスクリプトの呼び出しを簡単に確認できます。

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

外部ライブラリの呼び出しを含め、完全なスタックを表示するには、"外部ライブラリ" というラベルが付いたノードを展開します。

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

呼び出し履歴の項目をクリックすると、Visual Studio によってコードファイルが開き、対応するスクリプトが強調表示されます。

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>参照

[Visual Studio での ASP.NET MVC 4 の概要](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)(ASP.net web サイト)

[Page Inspector の概要](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/)(Channel 9 ビデオ)

[Page Inspector のエラーメッセージ](https://go.microsoft.com/?linkid=9813062)(MSDN)
