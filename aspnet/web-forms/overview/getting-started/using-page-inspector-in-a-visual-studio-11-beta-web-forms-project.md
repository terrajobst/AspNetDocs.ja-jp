---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: ASP.NET Web Forms | で Visual Studio 2012 の Page Inspector を使用するMicrosoft Docs
author: rick-anderson
description: Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。 統合ブラウザーで任意の要素を選択し、Page Inspector...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464944"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>ASP.NET Web フォームで Visual Studio 2012 の Page Inspector を使用する

Tim Ammann

> Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。 統合ブラウザーで任意の要素を選択すると、Page Inspector 要素のソースと CSS が瞬時に強調表示されます。 アプリケーション内の任意のページを参照したり、表示されたマークアップのソースをすばやく検索したり、Visual Studio 環境内でブラウザーツールを使用したりすることができます。
> 
> このチュートリアルでは、検査モードを有効にし、web プロジェクト内の CSS ルールとテキストをすばやく検索および編集する方法について説明します。 このチュートリアルでは Web フォームアプリケーションプロジェクトを使用しますが、Web サイトプロジェクトおよび[MVC](https://go.microsoft.com/?linkid=9802002)アプリケーションに Page Inspector を使用することもできます。
> 
> このチュートリアルには、次のセクションがあります。
> 
> [前提条件](#_1_prerequisites)
> 
> [Web アプリケーションを作成する](#_2_creating_a)
> 
> [Page Inspector を使用してアプリケーションを表示する](#_3_using_page)
> 
> [検査モードを有効にする](#_4_inspection_mode)
> 
> [Page Inspector を使用してマークアップを変更する](#_5_using_page)
> 
> [検査モードと HTML ウィンドウ](#_6_inspection_mode)
> 
> [[スタイル] ウィンドウでの CSS の変更のプレビュー](#_7_previewing_css)
> 
> [CSS 自動同期](#css_auto_sync)
> 
> [CSS カラーピッカーの使用](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>前提条件

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)または[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。

> [!NOTE]
> 最新バージョンの Page Inspector を取得するには、 [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)を使用して Azure SDK for .net 2.0 をインストールします。

Page Inspector は Microsoft Web Developer Tools にバンドルされています。 最新バージョンは1.3 です。 使用しているバージョンを確認するには、Visual Studio を実行し、 **[ヘルプ]** メニューから バージョン **[情報 Microsoft Visual Studio]** を選択します。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>Web アプリケーションを作成する

まず、で Page Inspector 使用する web アプリケーションを作成します。 Visual Studio で、[**ファイル**&gt;**新しいプロジェクト**] を選択します。 左側で **[ C#ビジュアル]** を展開し、 **[web]** を選択して、 **[ASP.NET web フォームアプリケーション]** を選択します。

![新しい Web フォームアプリケーション](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

**[OK]** をクリックします。

アプリケーションが**ソース**ビューで開きます。

![ソースビューの新しい Web フォームアプリケーション](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

アプリケーションを操作できるようになったので、Page Inspector を使用して確認し、変更することができます。

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>Page Inspector を使用してアプリケーションを表示する

次に、Page Inspector でアプリケーションを表示します。 **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[Page Inspector で表示]** を選択します。

![Page Inspector で表示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

既定では Page Inspector 初めて起動されるときに、Visual Studio 環境の左側にナローウィンドウとしてドッキングされます。 左側にドッキングしたままにして、快適な幅に設定するか、上部、下部、または右にあるツール領域のいずれかにドッキングします。

![ドッキング位置の Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

[Page Inspector] ウィンドウをドッキング解除する場合は、Visual Studio の外部に配置するか、2つ目のモニター (存在する場合) に配置することもできます。 ただし、Page Inspector ウィンドウがドッキング解除されているときに、Page Inspector と Visual Studio の間で ALT + TAB キーを押すには、[&gt;**ツール**]、 **[オプション]** 、[&gt;**環境**&gt; タブ**とウィンドウ**] の順に移動し、 **[タブウェル]** で **[フローティングツールウィンドウを常にメインウィンドウの上部に]** 表示する チェックボックスをオフにします

![Visual Studio と [ドッキング解除された Page Inspector] ウィンドウの間で ALT + TAB キーを押してフローティングツールウィンドウのチェックボックスをオフにする](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

[Page Inspector] ウィンドウの上部ペインに、ブラウザーウィンドウに現在のページが表示されます。 下部のペインには、左側に HTML マークアップのページが表示されます。また、右側には、ページのさまざまな側面を調べるためのタブが表示されます。 下のウィンドウは、Internet Explorer の[F12 開発者ツール](https://msdn.microsoft.com/ie/aa740478)に似ています。 (ただし、開発者ツールとは異なり、Visual Studio 内で Page Inspector 権限を使用できます)。

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

このチュートリアルでは、Page Inspector ブラウザー ウィンドウと  **HTML** タブと **スタイル** タブを使用して、アプリケーションにすばやく移動し、変更を加えることができます。

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>検査モードを有効にする

次に、Page Inspector の検査モードのしくみについて説明します。 Page Inspector ウィンドウで、**検査** ボタンをクリックします。

![要素の検査](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

検査モードが動作していることを確認するには、Page Inspector ブラウザーウィンドウ内のページのさまざまな部分にマウスを移動します。 この操作を行うと、マウスポインターが大きなプラス記号に変わり、下の要素が強調表示されます。

![Div にカーソルを合わせる-ラッパー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

マウスポインターを移動すると、

- **ソース**ビューの内容が変更され、ページ上の選択した要素に対応するマークアップが表示されます。 関連するマークアップが強調表示されます。 ソースが別のファイルにある場合は、そのファイルがソースビューで開き、関連するマークアップが強調表示されます。

- Page Inspector の **[HTML]** タブに表示されるマークアップも、ページ上の選択した要素に対応するように変更されます。 **[HTML]** タブには、関連するマークアップの概要が示されます。

- **[スタイル]** タブには、現在の選択に関連する CSS ルールが表示されます。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>Page Inspector を使用してマークアップを変更する

ここでは、Page Inspector を使用して、場所がすぐにわからない可能性があるマークアップやテキストを検索し、変更を加える方法について説明します。

Page Inspector を検査モードに配置し、ホームページの一番下までスクロールします。

フッター領域を入力するとすぐに、他のタブの右側にある一時的なタブの **[ソース]** ビューにある [Page Inspector の*マスター*レイアウトファイル] が開き、選択したマスターページのセクションが強調表示されます。 ここでは、Page Inspector が、最初に開いたファイルとは別のファイルから取得したコンテンツを検索して表示する方法について説明します。

![検査モードでのフッターの強調表示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

Page Inspector ブラウザーウィンドウで、著作権<a id="a"></a>に関する通知を含む行の上にマウスポインターを移動します。

[ *.Master* ] ページで、対応する行が強調表示されます。

![フッターの著作権線が強調表示されます](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

*サイトのマスター*ファイル内の行の末尾にテキストを追加します。

&lt;p&gt;&amp;コピーです。&lt;%: DateTime. 今年%&gt;-My ASP.NET アプリケーションがありません。&lt;/p&gt;

ここで、Ctrl + Alt + Enter キーを押すか、更新バーをクリックして Page Inspector ブラウザーウィンドウに結果を表示します。

![私の ASP.NET アプリケーションは岩を持っています。](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

フッターは*default.aspx*ページにあると思ったかもしれませんが、[マスターレイアウト] ページに表示されるようになったので、それを見つける Page Inspector ます。

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>検査モードと HTML ウィンドウ

次に、HTML ウィンドウと、要素をどのようにマップするかを簡単に説明します。

検査モードに Page Inspector を配置します。

![要素の検査](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

ページの一番上の部分をクリックします。 [ここにロゴを入力してください] と表示されます。 特定の要素を詳細に調べているため、マウスポインターを移動しても、ブラウザーウィンドウの表示が変更されなくなりました。

次に、マウスポインターを**HTML**ウィンドウに移動します。 マウスポインターを移動すると、Page Inspector **HTML**ウィンドウ内の要素のアウトラインが表示され、ブラウザーウィンドウ内の対応する要素が強調表示されます。

![HTML ウィンドウ](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

以前と同様に、Page Inspector は、一時的なタブで、*サイトのマスター*ファイルを開きます。 [] タブをクリックすると、対応するマークアップが &lt;ヘッダー&gt; セクションで強調表示されます。

![強調表示されたマークアップ](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>[スタイル] ウィンドウでの CSS の変更のプレビュー

次に、[Page Inspector**スタイル**] ウィンドウを使用して、CSS の変更をプレビューする方法を確認します。

**[検査]** ボタンをクリックして、検査モードに Page Inspector を配置します。

Page Inspector ブラウザーウィンドウで、ホームページ セクションの上にマウスポインターを移動し、 **div** と表示されるようにします。

![要素の上にマウスポインターを置く](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

Div のコンテンツラッパーセクション内を1回クリックし、マウスポインターを **[スタイル]** ウィンドウに移動します。 [... コンテンツラッパークラスセレクター] で、[背景色] プロパティのチェックボックスをオフにして選択します。

![背景色のクリア](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

Page Inspector ブラウザーウィンドウに変更がすぐに表示されます。

もう一度チェックボックスをオンにし、プロパティ値をダブルクリックして、`red`に変更します。 変更はすぐに表示されます。

![赤の背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

**[スタイル]** ウィンドウを使用すると、スタイルシート自体に変更をコミットする前に、CSS の変更を簡単にテストおよびプレビューできます。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自動同期

> [!NOTE]
> この機能には Page Inspector のバージョン1.3 が必要です。

CSS 自動同期機能を使用すると、CSS ファイルを直接編集し、Page Inspector ブラウザーですぐに変更を確認することができます。

**[検査]** をクリックして、検査モードに Page Inspector を配置します。

Page Inspector ブラウザーで、[ホームページ] セクションの上にマウスポインターを移動**します。このラベルが**表示されます。 この要素を選択するには、[1 回] をクリックします。

**[スタイル]** ウィンドウには、この要素のすべての CSS ルールが表示されます。 下にスクロールして、... コンテンツラッパークラスセレクターを見つけます。 [... コンテンツ-ラッパー] をクリックします。 Page Inspector によって、このスタイル (.css) を定義する CSS ファイルが開き、対応する CSS スタイルが強調表示されます。

![CSS ファイル](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

次に、`background-color` の値を "red" に変更します。 変更は、Page Inspector ブラウザーに直ちに表示されます。

![Page Inspector ブラウザー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>CSS カラーピッカーの使用

次に、Page Inspector を使用して、既定のアプリケーションで強調表示されているテキストの CSS をすばやく検索して変更する方法について説明します。 この例では、青の強調表示を希望せず、別の色に変更することを決定しました。

**[検査]** ボタンをクリックします。

![要素の検査](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

Page Inspector ブラウザーウィンドウで、強調表示されている "ビデオ、チュートリアル、サンプル" テキストの上にマウスポインターを移動し、CSS の "mark" ラベルが表示されるようにします。

![マーク要素にマウスポインターを合わせる](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

テキストをクリックして選択します。 対応する CSS マークセレクターが **[スタイル]** ウィンドウの下部に表示されます。

![[スタイル] ウィンドウのマークセレクター](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

[マーク] セレクターをクリックします。 これにより、web アプリケーションの *.css*ファイルが開きます。 [.Css] タブをクリックすると、セレクターに対応する CSS が強調表示されます。

![スタイルシートのマークセレクター](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

背景色のプロパティを使用して、線を選択して削除します。

新しい Visual Studio 2012 CSS カラーピッカーを使用し**て、[背景色**の設定] プロパティに新しい色を選択できるようになります。

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>Visual Studio 2012 CSS カラーピッカーの使用

Visual Studio 2012 の CSS エディターには、色の選択と挿入を簡単に行うことができるカラーピッカーが用意されています。 簡易カラーバーと "ポップアップ" ピッカーが用意されており、より細かい制御ができます。

カラーピッカーには標準の色パレットが含まれており、標準の色の名前、ハッシュコード、RGB、RGBA、HSL、および HSLA の色をサポートし、ドキュメントで最近使用した色の一覧を保持します。

背景色のプロパティがの行で、「bc」と入力し、下矢印を1回押します。

ハイフンで区切られた各単語の最初の文字を "背景色" のようなプロパティに入力すると、IntelliSense によってリストがフィルター処理され、一致するプロパティのみが表示されます。

![Intellisense のフィルター処理された値](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

ここで、コロンを入力します。 この操作を行うと、完全な背景色のプロパティ名が挿入されます。 「 **#** または**rgb (** )」と入力すると、カラーピッカーバーが表示されます。

![CSS カラーピッカーバー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

カラーピッカーバーがどのように動作するかを確認するには、マウスポインターで色をクリックするか、下方向キーを押してから、左右の方向キーを使用して色を走査します。 色にアクセスすると、背景色のプロパティに対応する値がプレビューされます。

![背景色のプロパティ値のプレビュー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

この時点で、enter キーを押して値を選択し、セミコロン (;)を入力して、CSS エントリを完成させます。 ここでは、カラーピッカーのポップアップがどのように機能するかを確認できるように、次のセクションに進んでください。

#### <a name="using-the-color-picker-pop-down"></a>カラーピッカーのポップアップを使用する

カラーバーに探している色が正確でない場合は、カラーピッカーのポップアップを使用できます。

これを開くには、カラーバーの右端にある二重シェブロンをクリックするか、キーボードの下方向キーを1回または2回押します。

![CSS カラーピッカーのポップアップ](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

右側の垂直バーから色をクリックします。 これにより、メインウィンドウにその色のグラデーションが表示されます。 Enter キーを押して縦棒から直接色を選択するか、メインウィンドウ内の任意のポイントをクリックして有効桁数を高くします。

使用する色がコンピューターの画面に表示される場合は (Visual Studio のユーザーインターフェイス内に存在する必要はありません)、右下にあるスポイトツールを使用して値をキャプチャできます。

カラーピッカーの下部にあるスライダーを動かすことで、色の不透明度を変更することもできます。 これにより、RGBA 形式は不透明度を表すことができるため、色の値が RGBA 値に変更されます。

色を選択したら、enter キーを押し、セミコロンを入力して、*サイトの .css*ファイルの背景色のエントリを完成させます。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Page Inspector 更新バー

Page Inspector は、直ちに、*サイトの .css*ファイル (またはアプリケーション内の任意のファイル) に対する変更を検出し、更新バーにアラートを表示します。

![更新バー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

すべてのファイルを保存して Page Inspector ブラウザーを更新するには、Ctrl + Alt + Enter キーを押すか、更新バーをクリックします。 強調表示色の変更がブラウザーに表示されます。

![強調表示色の変更](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>Visual Studio 環境内から Page Inspector ブラウザーをすぐに更新することに注意してください。 外部ブラウザーではなく Page Inspector を使用すると、web アプリケーションを開発するときにエディターを使用したままにすることができます。

## <a name="see-also"></a>参照

[Page Inspector の概要](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector)(Channel 9 ビデオ)

[Page Inspector のエラーメッセージ](https://go.microsoft.com/?linkid=9813062)(MSDN)
