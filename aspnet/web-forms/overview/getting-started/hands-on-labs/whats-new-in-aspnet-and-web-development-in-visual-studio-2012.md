---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 での ASP.NET と Web 開発の新機能 |Microsoft Docs
author: rick-anderson
description: 新しいバージョンの Visual Studio では、Web テクノロジを使用する際のエクスペリエンスとパフォーマンスの向上に焦点を合わせた多くの拡張機能が導入されています。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422098"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>Visual Studio 2012 の ASP.NET と Web 開発の新機能

[Web キャンプチーム](https://twitter.com/webcamps)別

> 新しいバージョンの Visual Studio では、Web テクノロジを使用する際のエクスペリエンスとパフォーマンスの向上に焦点を合わせた多くの拡張機能が導入されています。 CSS、JavaScript、HTML 用の Visual Studio エディターは、IntelliSense や自動インデントなど、最も多くのオンデマンドコード機能を含むように完全に改良されています。 パフォーマンスに関しては、バンドルと縮小が組み込み機能として統合され、ページの読み込み時間を短縮できるようになりました。
> 
> Visual Studio では、最新の web サイトテクノロジを使用することができます。 クロスブラウザーの CSS3 スニペットを使用すると、新しい HTML5 の要素と機能を利用しながら、クライアントプラットフォームに関係なく、サイトが機能することを確認できます。
> 
> この Visual Studio のバージョンでは、JavaScript コードの記述とプロファイルを簡単に行うことができます。 IntelliSense の一覧、統合された XML ドキュメントおよびナビゲーション機能を JavaScript コードで使用できるようになりました。 これで、JavaScript カタログをすぐに使用できるようになりました。 さらに、スクリプトに対する ECMAScript5 の準拠を確認し、初期段階で構文エラーを検出することもできます。
> 
> 最新ではありませんが、この Visual Studio のバージョンでは、組み込みのバンドルと縮小が実装されています。 スクリプトファイルとスタイルシートは、サイトの実行速度が速くなるように、パックされて圧縮されます。
> 
> このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。
> 
> すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目標

この実習では、次の方法を学習します。

- CSS エディターでの新機能と強化された機能の使用
- HTML エディターでの新機能と強化された機能の使用
- JavaScript エディターの新機能と機能強化を使用する
- バンドルと縮小の構成と使用

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

- Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) (セットアップスクリプトの場合-windows 8 および windows Server 2008 R2 に既にインストールされています)
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home)または HTML5 に準拠したブラウザー

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [演習 1: CSS エディターの新機能](#Exercise1)
2. [演習 2: HTML エディターの新機能](#Exercise2)
3. [演習 3: JavaScript エディターの新機能](#Exercise3)
4. [演習 4: バンドルと縮小](#Exercise4)

このラボの推定所要時間: **60 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>演習 1: CSS エディターの新機能

Web 開発者は、CSS 編集に関連する多くの問題に精通している必要があります。 CSS スタイルの最大の問題の1つは、ブラウザー間の互換性です。 場合によっては、サイトにスタイルを適用した後で、別のブラウザーやデバイスでそのスタイルを開いたときに表示が変わることがよくあります。 そのため、これらの視覚的な問題を修正するにはかなりの時間がかかることがあります。これは、最終的に1つのブラウザーで動作していると、他のブラウザーでは動作しなくなったことを認識します。

Visual Studio には、開発者が CSS スタイルシートに効果的にアクセスし、作業し、整理するのに役立つ機能が含まれるようになりました。 この演習では、有効な組織とエディションの新機能に加え、ブラウザー間の互換性のための CSS3 コードスニペットを使用します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>タスク 1-新しいエディター機能

このタスクでは、CSS エディターの新機能について説明します。 この新しいエディターでは、新しいスマートインデント、強化されたコードコメント、および拡張された IntelliSense リストを利用して生産性を向上させることができます。

1. **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。
2. ソリューションエクスプローラーで、 **[スタイル]** フォルダーの下にある**サイトの .css**ファイルを開きます。 ツールバーに **[テキストエディター]** ツールが表示されていることを確認します。 これを行うには、[ | **ツールバー**の**表示**] メニューオプションを選択し、 **[テキストエディター]** オプションをオンにします。 この新しいバージョンでは、 **[コメント]** ボタン (![コメントボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) と [コメント解除] ボタン (![コメント**解除ボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)** ) が CSS エディターでも有効になっていることがわかります。

    ![エディターと CSS ツールの有効化](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "エディターと CSS ツールの有効化")

    *エディターと CSS ツールの有効化*
3. コードをスクロールし、任意の CSS クラス定義を選択します。 **コメント**(![コメントボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) ボタンをクリックして、選択した行にコメントをコメントします。 次に、**コメント**解除ボタン (![コメント解除ボタン](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)) をクリックして、変更を元に戻します。
4. **[折りたたみ]** (![折りたたみ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)) をクリックし、テキストの左余白にある [(![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) 展開)] ボタンを**展開**します。 これで、使用していないスタイルを表示しないようにすることができます。

    ![CSS クラスの折りたたみ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "CSS クラスの折りたたみ")

    *CSS クラスの折りたたみ*
5. スマートインデント機能が有効になっていることを確認します。 [**ツール** | **オプション**] メニューオプションを選択し、画面の左側のウィンドウにある **[テキストエディター]**  | [ **CSS** | **書式設定**] ページを選択します。 **[階層インデント]** オプションをオンにします。

    ![階層インデントの有効化](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "階層インデントの有効化")

    *階層インデントの有効化*
6. メインクラス定義 (. main) を見つけて、div 要素にスタイルを追加します。 このコードは自動的に調整されるので、ユーザーは親クラスを一目で確認できます。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![CSS での階層的な配置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS での階層的な配置")

    *CSS での階層的な配置*
7. **Main div**クラスの中で、境界の最後にある**0px;** カーソルを探し、 **enter**キーを押して、IntelliSense の一覧を表示します。 「 **Top** 」と入力すると、入力に応じて一覧がどのようにフィルター処理されるかがわかります。 この一覧には、単語の任意の部分に**top**が含まれている要素が表示されます (以前のバージョンの Visual Studio では、一覧は用語で*始まる*項目によってフィルター処理されます)。

    ![CSS における IntelliSense の機能強化](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS における IntelliSense の機能強化")

    *CSS における IntelliSense の機能強化*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>タスク 2-カラーピッカー

このタスクでは、Visual Studio IntelliSense に統合された新しい CSS カラーピッカーを見つけます。

1. **.Css**で、ヘッダークラス定義 (. header) を見つけて、 **[背景色]** 属性の横にカーソルを置きます。 &quot;:&quot; と &quot;、**そのコード行**の &quot; 文字を #します。

    ![カーソルを検索する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "カーソルを検索する")

    *カーソルを検索する*
2. **コロン**(:) を削除します。カラーピッカーを表示するには、もう一度書き込みます。 最初に表示される色は、サイトで最も頻繁に使用される色です。 白い色をクリックすると、その HTML カラーコード (#fff) によって、スタイルシート内の現在のカラーコードが置き換えられます。

    ![カラーピッカー](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")

    *カラーピッカー*
3. カラーピッカーの**展開**(![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) ボタンを押して色のグラデーションを表示し、グラデーションカーソルをドラッグして別の色を選択します。 その後、**スポイト**ボタンをクリックし、画面から任意の色を選択します。 カーソルを移動すると、背景色の値が動的に変化することに注意してください。

    ![カラーピッカーのグラデーション](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "カラーピッカーのグラデーション")

    *カラーピッカーのグラデーション*
4. **不透明度**スライダーで、セレクターをバーの中央に移動して不透明度を下げます。 背景色の値が、そのスケールが RGBA に変わることに注意してください。

    ![カラーピッカーの不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "カラーピッカーの不透明度")

    *カラーピッカーの不透明度*

    > [!NOTE]
    > CSS3 で RGBA (赤、緑、青、アルファ) の色の定義を使用すると、1つの項目の色の不透明度を定義できます。 **不透明度**とは異なり、同様の CSS 属性 **-** RGBA 色も最新のブラウザーと互換性があります。

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>タスク 3-CSS と互換性のあるコードスニペット

このタスクでは、web サイトにいくつかの機能を実装するために、ブラウザーと互換性のある CSS3 スニペットを使用する方法について説明します。

1. サイトの **.css**ファイルで、**ヘッダー**の css クラス定義 (. header) を見つけて、 **/\*罫線の半径\*/** プレースホルダーの下にカーソルを置き、新しいスニペットを追加します。 Enter キーを押して、IntelliSense の一覧を表示し、「 **Radius** **」** と入力してリストをフィルター処理します。 リストから **[罫線-半径]** オプションをダブルクリックして選択し、 **tab**キーを押してスニペットを挿入します。 次に、半径のサイズをピクセル単位で**入力し、enter キーを**押します。 たとえば、「 **15px**」と入力します。

    スニペットによって追加された CSS3 属性は、Mozilla および WebKit ベースのブラウザーを含むほとんどの HTML5 準拠ブラウザーで、丸みのある境界線を表示します。

    ![境界線を使用する-半径スニペット](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "境界線を使用する-半径スニペット")

    *境界線を使用する-半径スニペット*
2. ページスタイル (. ページ) に同じ**罫線**スニペットを適用します。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. F5 キーを押して、ソリューションを実行します。 各ページの罫線が丸くなっていることに注意してください。

    ![角の丸み](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "角の丸み")

    *角の丸み*
4. ブラウザーを閉じて、Visual Studio に戻ります。
5. **[スタイル]** フォルダーの下にある**カスタム .css**ファイルを開き、div 内にカーソルを置き**ます。 ul li img**クラスの定義。
6. Enter キーを押して IntelliSense の一覧を表示し、「 **box-Shadow** 」と入力し、 **TAB**キーを2回押して、クラス定義内に既定のシャドウコードスニペットを挿入します。 Shadow 値を**10px 10px 5px #888**に設定します。 次に、「 **border-radius** 」と入力し、コードスニペットを挿入します。 「 **15px** 」と入力して半径のサイズを設定し、 **enter**キーを押します。

    ![影付きの角の丸み](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "影付きの角の丸み")

    *影付きの角の丸み*

    > [!NOTE]
    > 現時点では、Mozilla と Webkit (Chrome、Safari、Konkeror) ブラウザーをサポートするために、対応するプレフィックス (moz、webkit、o) を使用して shadow 属性が挿入されます。
7. 新しいクラスの div を作成**します。 images ul li img:** **div**の下にマウスポインターを移動し、その中にカーソルを**置きます。**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. 変換スニペットを挿入するには、「 **transform** 」と入力し、 **tab**キーを2回押します。 次に、[**回転] (-15deg)** を入力して、イメージがホバーされるときの回転角度の値を変更します。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. **F5**キーを押してソリューションを実行し、CSS3 ページに移動します。 画像の角が丸く、ボックスの影が付いていることに注意してください。 画像の上にマウスポインターを移動し、回転します。

    ![イメージを回転する Transform スニペット](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "イメージを回転する Transform スニペット")

    *イメージを回転する Transform スニペット*

    > [!NOTE]
    > Internet Explorer 10 を使用していて、影が表示されない場合は、ドキュメントモードが IE10 標準に設定されていることを確認してください。 **F12**キーを押して Internet Explorer 開発者ツールを開き、 **[ドキュメントモード]** をクリックして IE10 標準に変更します。

    ![about-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>演習 2: HTML エディターの新機能

Visual Studio には、HTML エディターが強化されています。 このバージョンに含まれる機能強化の一部は、HTML ドキュメントのスマートインデント、HTML5 スニペット、HTML 開始タグと終了タグの一致、および HTML 検証です。 この演習では、web サイトマークアップで作業するときに、これらの変更によって自在がどのように改善されるかを確認します。

CSS エディターと同様に、HTML エディターも改善されました。 これらの改善点のほとんどは、Web 開発者の作業が容易になる小さなものです。 HTML ドキュメント DOCTYPE を対象とする編集や検証を行うときに、HTML5、スマートインデント、一致する開始タグと終了タグのようなものもありますが、これらの機能強化が行われています。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>タスク 1-DOCTYPE 検証の機能強化

HTML エディターでは、マスターページに定義が存在する場合でも、ページの DOCTYPE をチェックできるようになりました。 ページの DOCTYPE に応じて、HTML エディターは正しい規則セットで検証し、DOCTYPE 要素を考慮して IntelliSense リストをフィルター処理します。

このタスクでは、ページの DOCTYPE を変更して、HTML エディターの動作がそれに応じてどのように変化するかを確認します。

1. まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。
2. **[.Master]** ページを開きます。
3. 検証ツールバーのターゲットスキーマに注意してください。 HTML エディターがどのように動作するか (検証、IntelliSense など) は、Doctype が選択された場合に適切に変更されます。

    ![HTML ソース編集ツールバーで Doctype を使用する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML ソース編集ツールバーで Doctype を使用する")

    *HTML ソース編集ツールバーで Doctype を使用する*
4. ターゲットスキーマを HTML 4.01 に変更します。

    ![HTML ソース編集ツールバーでの Doctype の変更](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML ソース編集ツールバーでの Doctype の変更")

    *HTML ソース編集ツールバーでの Doctype の変更*
5. **Body**要素の下にカーソルを置き、HTML5 要素の名前 ( **video**など) の入力を開始します。 この要素は、IntelliSense の一覧では使用できないことに注意してください。

    ![HTML5 要素が一覧に含まれていません](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 要素が一覧に含まれていません")

    *HTML5 要素が一覧に含まれていません*
6. 検証ツールバーのターゲットスキーマへの変更を元に戻します。ドロップダウンリストから [DOCTYPE: XHTML5] を選択します。

    ![HTML ソース編集ツールバーで Doctype を使用する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML ソース編集ツールバーで Doctype を使用する")

    *HTML ソース編集ツールバーで Doctype をリセットする*
7. **Body**要素の下にカーソルを置き、HTML5 要素の入力を開始します (**ビデオ**など)。 HTML5 要素が IntelliSense の一覧で使用できるようになったことに注意してください。

    ![表示されている HTML5 要素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "表示されている HTML5 要素")

    *表示されている HTML5 要素*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>タスク 2-開始タグと終了タグの自動更新

Visual Studio で、編集中の要素の HTML の開始タグまたは終了タグが相互に一致するように更新されるようになりました。 この新機能により、HTML タグを編集するときの生産性が向上します。

1. **Default.aspx**ページで、タイトルを含む**H3**要素 (たとえば、Visual Studio 2012 の岩!) を追加します。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. **H3**タグを変更し、「 **H2** 」または「H1」と入力し**ます。**

    終了タグが自動的に更新されることに注意してください。 また、終了タグを変更して、それに応じて開始タグが更新されていることを確認することもできます。

    ![終了タグの自動更新](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "終了タグの自動更新")

    *終了タグの自動更新*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>タスク 3-新しい HTML5 コードスニペット

Visual Studio に HTML5 コードスニペットがいくつか追加されました。 このタスクでは、これらのスニペットのいくつかを使用します。

1. Web サイトフォルダーのルートに、 **audio**という名前の新しいフォルダーを追加します。 Windows エクスプローラーを開き、 **WhatsNewASPNET**ソリューションの**オーディオ**フォルダーにオーディオファイルをコピーします。
2. **Default.aspx**ページで、Web11 の下にあるカーソルを探します。 ヘッダー。 「 **AUDIO** 」と入力し、tab キーを押します。

    新しい HTML エディターには、HTML5 コンテンツ用のコードスニペットが含まれています。 HTML5 スニペットを有効にするには、必ず適切な DOCTYPE 定義を使用するようにしてください。

    ![HTML5 コードスニペットの挿入](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 コードスニペットの挿入")

    *HTML5 コードスニペットの挿入*
3. 既存のオーディオファイルを指すようにオーディオソースを更新します。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > この場合、オーディオファイルをソリューションに追加する必要があります。
4. **F5**キーを押してサイトを実行し、オーディオを再生します。

    ![オーディオコントロールの実行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "オーディオコントロールの実行")

    *オーディオコントロールの実行*

    > [!NOTE]
    > また、Visual Studio に含まれているその他のスニペット (ビデオ、図など) を試すこともできます。
5. 次に、ページの一部にコントロールを挿入してみます。 たとえば、 **GridView**コントロールを挿入しようとしますが、 **&lt;合わせるを**入力するのではなく、 **&lt;GV**の入力を開始します。 IntelliSense の一覧に**asp: GridView**コントロールが表示されていることに注意してください。

    HTML エディターの IntelliSense では、タイトルの大文字と小文字の区別と、部分的な一致 (用語を含むすべての要素の取得) が提供されるようになりました。

    ![IntelliSense リストを使用した GridView の挿入](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense リストを使用した GridView の挿入")

    *IntelliSense リストを使用した GridView の挿入*

    **&lt;grid**と入力すると、用語に一致するすべての項目が表示されますが、Visual Studio は**gridview**コントロールを提案します。

    ![IntelliSense リストと部分一致を含む GridView の挿入](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense リストと部分一致を含む GridView の挿入")

    *IntelliSense リストと部分一致を含む GridView の挿入*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>タスク 4-HTML エディターのスマートタグ

HTML エディターのもう1つの改良点は、スマートタグ機能です。 スマートタグを使用すると、一般的な開発タスクや繰り返し発生する開発タスクを、コントロールごとに簡単に実行できます。 この機能は、html デザイナーでは既に使用可能ですが、HTML エディターでは使用できませんでした。

1. **[.Master]** を開き、[ **Asp: Menu]** 要素を探します。 開始タグにカーソルを置き、要素の下部に表示されている小さなグリフをクリックして、[スマートタスク] メニューを開きます。 メニューコントロールに関連する一部のタスクにすばやくアクセスできることに注意してください。

    ![メニューコントロールのスマートタスク](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "メニューコントロールのスマートタスク")

    *メニューコントロールのスマートタスク*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>タスク 5-スマートインデント

HTML のベストプラクティスの1つは、コードを読みやすくするために、入れ子になった要素をインデントすることです。 Visual Studio 2012 では、コードの記述中にエディターによって要素が自動的にインデントされることがわかります。

> [!NOTE]
> 以前のバージョンの Visual Studio では、スマートインデントは XML エディターでは使用できましたが、HTML エディターでは使用できませんでした。

1. HTML エディターのインデントの構成がスマートインデントに設定されていることを確認します。 これを行うには、[ツール] を選択します。 **[オプション**] メニューオプションをクリックし、[テキストエディター] を選択します。 **HTML |** 画面の左側のウィンドウにある [タブ] ページ。 [スマートインデント] オプションを選択します。

    ![HTML エディターの設定](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML エディターの設定")

    *HTML エディターの設定*
2. **Default.aspx**ページで、audio 要素の下にあるすべてのコンテンツを削除します。
3. 開いている**オーディオ**要素の末尾にカーソルを置き、 **ENTER キーを**押します。

    カーソルの新しい位置にインデントレベルが追加されていることに注意してください。

    ![HTML エディターでのスマートインデント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML エディターでのスマートインデント")

    *HTML エディターでのスマートインデント*
4. 削除したコンテンツを使用してオーディオタグを復元するか、変更を保存せずに**default.aspx**を閉じます。

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>タスク 6-ユーザーコントロールに抽出する

コードの一部を関数に抽出するなど、Visual Studio に含まれるリファクタリングツールは、改善を促進し、既存のコードをリファクタリングするための優れた機能です。 ASP.NET ページに対応するのは、ユーザーコントロールへの HTML コードの抽出です。 手動で実行するには、新しいユーザーコントロールの作成、ユーザーコントロールへのコードセクションの移動、ユーザーコントロールのタグプレフィックスの登録、最後にページ上のユーザーコントロールのインスタンス化など、いくつかの手順を実行します。 これで、*ユーザーコントロールへ*の新しい Extract ツールによって、これらのすべての手順が自動的に実行されるようになりました。

このタスクでは、新しい Extract to User Control コンテキスト操作を使用して、選択したコードから新しいユーザーコントロールを生成します。

1. **Default.aspx**ページで、 **H2**要素と**audio**要素を選択します。
2. 右クリックして **[ユーザーコントロールに展開]** を選択します。

    ![[ユーザーコントロールに展開] メニューオプション](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "[ユーザーコントロールに展開] メニューオプション")

    *[ユーザーコントロールに展開] メニューオプション*
3. 新しいユーザーコントロールの名前を入力します。 たとえば、「 **Jukebox**」と入力し、[ **OK]** をクリックします。

    ![抽出されたユーザーコントロールを保存しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "抽出されたユーザーコントロールを保存しています")

    *抽出されたユーザーコントロールを保存しています*
4. 選択したコードがユーザーコントロールに抽出され、選択したコードの元の場所が新しいユーザーコントロールのインスタンスに置き換えられたことに注意してください。

    ![新しいユーザーコントロールを使用するために自動的に更新されたページ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "新しいユーザーコントロールを使用するために自動的に更新されたページ")

    *新しいユーザーコントロールを使用するために自動的に更新されたページ*
5. **F5**キーを押してページを実行し、コントロールが動作することを確認します。

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>演習 3: JavaScript エディターの新機能

JavaScript コードの記述や編集は、特にアプリケーションのサイズが大きくなり、長いファイルや数百の関数を扱う場合には、簡単なタスクではありません。 通常、スクリプト開発者は、コードの読みやすさを維持し、ファイル間を移動するために、余分な作業を行う必要があります。 JQuery のような JavaScript ライブラリが含まれているので、コードの長さが原因でスクリプトナビゲーションが困難になっています。

Visual Studio によって JavaScript エディターが更新され、コードモードをアクセス可能にして整理できるようになりました。 または VB エディターにC#既に存在していた Visual Studio の多くの機能は、JavaScript エディターで実装されるようになりました。 [定義へ]、[自動インデント]、[ドキュメントと検証] を記述するときに使用します。 IntelliSense の一覧を更新すると、JavaScript 関数カタログをすぐに使用できるようになります。

この演習では、JavaScript エディターの新機能と改善点について学習します。 ここでは、サンプルファイルを参照し、Visual Studio 2012 内で JavaScript プログラミングをより効率的にするための新しい各特性について説明します。

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>タスク 1-JavaScript エディターの新機能

このタスクでは、コードの整理とユーザーエクスペリエンスの向上に重点を置いた、JavaScript エディターの新機能の一部を紹介します。

1. まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。
2. **F5**キーを押してアプリケーションを実行し、ナビゲーションバーの JavaScript リンクをクリックします。 ページを何度も更新して、カウンターの増加を確認します。

    ![ページカウンター](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "ページカウンター")

    *ページカウンター*
3. ブラウザーを閉じて、Visual Studio に戻ります。
4. **Default.aspx**ページを開き、 **&lt;スクリプト&gt;** ブロック (下図参照) を探します。

    次のコードでは、HTML5 ローカルストレージを使用して、現在のユーザーがページにアクセスした回数を格納する*Pageloadcount*変数を格納します。 ローカルストレージは、HTML5 標準で導入されたクライアント側のキー値データベースです。 データは、ユーザーのブラウザー内のローカルコンピューターに保存されます。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > 次の手順に進む前に、DOCTYPE が XHTML5 に設定されていることを確認します。
5. コードを編集します。 JavaScript 用の IntelliSense には、ローカルストレージやその内部メソッドなどの HTML5 機能が含まれていることに注意してください。

    ![HTML5 JavaScript の javascript 機能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript の javascript 機能")

    *HTML5 JavaScript の javascript 機能*
6. スクリプトコードから左中かっこ ( **{** ) をクリックすると、角かっこが強調表示されます。

    ![角かっこが強調表示される](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "角かっこが強調表示される")

    *角かっこが強調表示される*
7. 関数**Testautoalign ()** をコメント解除します (3 行を選択すると、 **CTRL** + **K**を使用できます。**CTRL** + **U**) を押して、関数コード内でカーソルを見つけます。 2行目を追加するには、enter キーを押します。 コードが**アラ**インされ、**自動インデント**されていることに注意してください。

    ![JavaScript コードは自動的にアラインされます](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript コードは自動的にアラインされます")

    *JavaScript コードは自動的にアラインされます*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>タスク 2-JavaScript の検証

このタスクでは、ECMAScript5 標準の新しい JavaScript 検証について説明します。 この機能を使用すると、準拠している JavaScript コードを記述しながら、サイトを展開する前にスクリプトの問題を回避できます。

> [!NOTE]
> Visual Studio 2010 では ECMAStript3 準拠が実装されていますが、Visual Studio 2012 では ECMAScript5 準拠が提供されています。

1. **スクリプト \ カスタム**プロジェクトフォルダーの下にある**ECMA5script5 を**開きます。 次に、ECMAScript5 standard の検証をテストします。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    ファイルの最初の行で**strict** &quot; direction &quot; 使用して、ECMAScript5 **strict モード**を有効にすることができます。 このモードは、過去のエディションのあいまいさを明確にする言語のサブセットで構成され、getter や setter、JSON のライブラリサポート、オブジェクトのプロパティに対する完全なリフレクションなど、いくつかの新機能が追加されています。
2. まだ開いていない場合は**エラー一覧**を開きます ( **[表示]** メニュー |**エラー一覧**)。 **関数**の宣言に下線が引かれていることに注意してください。 これは、ECMA5 標準関数を言語構造体内で入れ子にすることができないためです。 下の [エラー一覧] には、警告の詳細が表示されます。

    ![JavaScript の検証エラーメッセージ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript の検証エラーメッセージ")

    *JavaScript の検証エラーメッセージ*
3. 厳密な&quot;方向を**使用する&quot;** をコメントアウトすると、エラーが消えますが、警告は残ります。
4. ファイルの最後の行に **&quot;test&quot;** のような文字列を記述します (文字列として指定するには引用符を含めます)。 文字列の横にピリオドを書き込んで、IntelliSense の一覧を表示し、 **[トリム]** オプションを選択します。

    ECMAScript5 standard では、文字列値と変数にも、trim、大文字、検索、置換などの文字列メソッドが定義されています。

    ![JavaScript での IntelliSense の一覧](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript での IntelliSense の一覧")

    *JavaScript での IntelliSense の一覧*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>タスク 3-JavaScript の XML ドキュメント

このタスクでは、Visual Studio の JavaScript での XML ドキュメントの機能について説明します。 JavaScript IntelliSense の一覧に、各関数の XML ドキュメントが表示されるようになります。 さらに、JavaScript のナビゲーション機能についても説明します。

1. [**スクリプト]/[カスタム**プロジェクトフォルダー] にある、 **XMLDoc**ファイルを開きます。 このファイルには、各 JavaScript 関数に関する XML ドキュメントが含まれています。

    ![IntelliSense に統合された JavaScript XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "IntelliSense に統合された JavaScript XML ドキュメント")

    *IntelliSense に統合された JavaScript XML ドキュメント*
2. 次に、 **XMLDoc**ファイルの関数を**追加**し、 **test**という名前の新しい関数を作成します。
3. **テスト**関数で、2つのパラメーターを受け取る**乗算**関数を呼び出します。 [ツールヒント] ボックスに、**乗算**関数のドキュメントが表示されていることを確認します。

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![JavaScript 関数の XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 関数の XML ドキュメント")

    *JavaScript 関数の XML ドキュメント*
4. 関数呼び出しステートメントを完了し、*ドット*を入力して、戻り値の IntelliSense リストを開きます。 Visual Studio では、値を数値として扱うドキュメント内の**戻り**値が検出されていることに注意してください。

    ![戻り値の型に関する XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "戻り値の型に関する XML ドキュメント")

    *戻り値の型に関する XML ドキュメント*
5. 次に、add 関数の呼び出しを挿入します。 JavaScript エディターが関数のオーバーロードをサポートするようになったことに注意してください。 関数名を記述する場合は、ドキュメントで指定されている使用可能なオーバーロードのいずれかを選択できます。

    ![オーバーロードに関する XML ドキュメント](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "オーバーロードに関する XML ドキュメント")

    *オーバーロードに関する XML ドキュメント*
6. **GotoDefinition**ファイルを開き、 **$ () .html ()** 関数呼び出しを見つけます。 **Html**でカーソルを見つけます。
7. **F12**キーを押して、定義に移動します。 **検索**ツールを使用せずに、JavaScript コードにアクセスして閲覧できるようになりました。
8. コードファイルの一番下にあるシグネチャブロックの前にある jQuery 命令でカーソルを探します。 **F12**キーを押します。 JQuery ライブラリファイルに移動します。 また、 **F12 キー**を使用して jQuery ファイル間を移動することもできます。

    ![JQuery 定義への移動](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "JQuery 定義への移動")

    *JQuery 定義への移動*

> [!NOTE]
> ファイルを保存する前に、GotoDefinition に構文エラーがないことを確認してください。

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>演習 4: バンドルと縮小

Web サイトに複数の JavaScript または CSS ファイルが含まれている回数 これは、バンドルと縮小によってファイルサイズを縮小し、サイトのパフォーマンスを向上させるために役立つ、非常に一般的なシナリオです。 ASP.NET 4.5 の新しいバンドル機能は、一連の JS または CSS ファイルを1つの要素にパックし、コンテンツを縮小することによってサイズを縮小します (つまり、不要な空白を削除したり、コメントを削除したり、識別子を減らしたりします)。

ASP.NET 4.5 でのバンドルと縮小は実行時に実行されるため、プロセスでユーザーエージェント (たとえば、IE、Mozilla など) を識別できます。したがって、ユーザーブラウザーを対象にして圧縮を改善します (たとえば、Mozilla 固有のものを削除するなど)。要求が IE から取得された場合)。

この演習では、ASP.NET 4.5 でさまざまな種類のバンドルと縮小を有効にして使用する方法について説明します。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>タスク 1-NuGet からのバンドルと縮小パッケージのインストール

1. まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。
2. NuGet パッケージマネージャーコンソールを開きます。 そのためには、メニュー**ビュー** | **その他の Windows** | **パッケージマネージャーコンソール**を使用します。

    ![パッケージマネージャー file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole を開く](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "パッケージマネージャーコンソールを開く")

    *パッケージマネージャーコンソールを開く*
3. **パッケージマネージャーコンソールで、** 「 **Install-Package Microsoft web.config** 」と入力し、 **enter**キーを押します。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>タスク 2-既定のバンドル

バンドルと縮小を使用する最も簡単な方法は、既定のバンドルを有効にすることです。 この方法では、規則を使用して、フォルダー内の JS ファイルと CSS ファイルのバンドルされたバージョンと縮小版を参照できます。

このタスクでは、バンドルされた、縮小された JS および CSS ファイルを有効にして参照し、結果の出力を表示する方法を学習します。

1. まだ開いていない場合は、 **Visual Studio**を起動し、このラボの**Source\WhatsNewASPNET**フォルダーにある**WhatsNewASPNET**ソリューションを開きます。
2. **ソリューションエクスプローラー**で、**スタイル**、**スクリプト**作成、および**スクリプト**作成フォルダーを展開します。

    アプリケーションで複数の CSS および JS ファイルが使用されていることに注意してください。

    ![アプリケーション内の複数のスタイルシートと JavaScript ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "アプリケーション内の複数のスタイルシートと JavaScript ファイル")

    *アプリケーション内の複数のスタイルシートと JavaScript ファイル*
3. **Global.asax.cs**ファイルを開きます。

    新しい**web.config**名前空間がファイルの先頭でコメントアウトされていることに注意してください。 Using ディレクティブをコメント解除して、バンドル機能と縮小機能を含めます。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. **Application\_Start**メソッドを見つけます。

    このメソッドでは、次のスニペットに示すように、EnableDefaultBundles の呼び出しをコメント解除します。 これにより、そのフォルダーへのパス、および &quot;CSS&quot; または &quot;JS&quot; サフィックスを使用して、フォルダー内の CSS ファイルのバンドルされたコレクションを参照できます。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. **最適化 .aspx**ファイルを開き、**コンテンツのヘッド**のコンテンツコントロールを探します。

    CSS ファイルと JS ファイルに参照されるタグが1つあることに注意してください。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > このコードはデモを目的としています。 サイトのマスターファイルでバンドルを参照するのが理想的です。 このサンプルコードでは、一部のバンドルファイルも、この最後の参照が冗長になるように、サイトのマスターファイルによって参照されていることがわかります。
6. リンクは**href**属性でバンドル規則を使用して、スタイルとスクリプト \ カスタムフォルダーからすべての CSS または JS ファイルを取得することに注意してください。

    次に示すように、path **scripts/custom/JS**を使用して、**スクリプト/カスタム**フォルダー内のすべての JS ファイルのバンドルと縮小を行うことができます。 これは、既定のバンドルでの既定の動作です。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. **Styles\Site.css**ファイルを開きます。

    元の CSS ファイルには、インデントされたコード、空白、およびファイルを拡大するコメントが含まれていることに注意してください。 (JavaScript ファイルにも空白とコメントが含まれています)。

    ![Scripts フォルダー内の元の CSS ファイルの1つ](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts フォルダー内の元の CSS ファイルの1つ")

    *Scripts フォルダー内の元の CSS ファイルの1つ*
8. **F5**キーを押してアプリケーションを実行し、 **[最適化]** ページに移動します。
9. **[CSS バンドル]** リンクをクリックして、ファイルをダウンロードして開きます。

    バンドルされている縮小されたファイルを確認します。 空白、コメント、およびインデントの文字がすべて削除され、より小さなファイルが生成されていることがわかります。

    ![バンドルの CSS ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "バンドルの CSS ファイル")

    *バンドルの CSS ファイル*
10. 次に、 **[JS バンドル]** リンクをクリックして、JavaScript のバンドルファイルを開きます。 エクスプローラーの警告は無視してかまいません。 **カスタム**フォルダーにある JavaScript ファイルもバンドルされ、縮小されていることに注意してください。

    ![バンドルした JavaScript ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "バンドルした JavaScript ファイル")

    *バンドルした JavaScript ファイル*

    CSS または JS ファイルの圧縮を有効にすることは、以前の ASP.NET バージョンでははるかに複雑でした。 ここでは、 *global.asax*ファイルに1行を追加して、バンドルを有効にした後、サイトからバンドルされたファイルを参照する必要があります。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>タスク 3-静的なバンドル

静的なバンドルアプローチでは、バンドルするファイルのセット、参照、および使用される縮小方法をカスタマイズできます。

このタスクでは、バンドルおよび縮小する特定のファイルセットを定義するように、静的なバンドルを構成します。

1. ブラウザーを閉じます。
2. **Global.asax.cs**ファイルを開き、 **Application\_Start**メソッドを見つけます。
3. 次のコードに示すように、静的バンドルコードのコメントを解除します。

    &quot; **~/staticバンドル**&quot; 仮想パスで参照される静的バンドルを定義し、 **addfile**メソッドを使用して指定されたすべてのファイルを縮小するために**JsMinify**を使用します。 最後に、静的なバンドルを**bundletable.enableoptimization とき**に追加し、それを有効にします。

    ファイルが同じ場所に配置されていないことに注意してください。これは、既定のバンドルを超えるもう1つの利点です。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. **最適化 .aspx**ファイルを開きます。

    **静的 JS バンドル**へのリンクでは、Global.asax.cs ファイルで静的バンドルを構成したときに宣言したパスが使用されていることに注意してください: **/staticバンドル**。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. **F5**キーを押してアプリケーションを実行し、 **[最適化]** ページに移動します。
6. **[静的な JS バンドル]** リンクをクリックして、ファイルを開きます。

    バンドルされている縮小された JavaScript ファイルが、パス &quot;/staticバンドル&quot;の下にある静的バンドルファイルに構成されているすべての JavaScript ファイルの出力になっていることに注意してください。

    ![静的な JavaScript ファイルバンドル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "静的な JavaScript ファイルバンドル")

    *静的な JavaScript ファイルバンドル*
7. ブラウザーを閉じて、Visual Studio に戻ります。

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>タスク 4-動的なフォルダーバンドル

このタスクでは、動的フォルダーバンドルを構成する方法について説明します。 動的バンドルの機能として、静的な JavaScript を含めることができます。また、JavaScript にコンパイルされる言語の他のファイルも含めることができるため、バンドルを実行する前に処理が必要になります。

この例では、 **Dynamicfolderbundle**クラスを使用して、CofeeScript で記述されたファイルの動的バンドルを作成する方法について説明します。 CofeeScript は javascript にコンパイルされるプログラミング言語で、javascript コードを記述するための簡単な構文を提供し、JavaScript の簡潔さと読みやすさを強化します。

1. **Global.asax.cs**ファイルを開き、 **Application\_Start**メソッドを見つけます。
2. 次のコードに示すように、動的バンドルコードのコメントを解除します。

    **CoffeeMinify**カスタム縮小プロセッサを使用する動的フォルダーバンドルを定義します **。** これは、&quot;の&quot; 拡張機能 (CoffeeScript files) を持つファイルにのみ適用されます。 検索パターンを使用して、フォルダー内にバンドルするファイルを選択することができます。たとえば、"\*. コーヒー" のようにします。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. NuGet パッケージマネージャーコンソールを開きます。 そのためには、メニュー**ビュー** | **その他の Windows** | **パッケージマネージャーコンソール**を使用します。
4. **パッケージマネージャーコンソールで、** 「 **CoffeeSharp** 」と入力し、 **enter**キーを押します。
5. **[ソリューションエクスプローラー]** ウィンドウの **[すべてのファイルを表示]** ボタンをクリックします。

    ![すべてのファイルを表示](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "すべてのファイルを表示")

    *すべてのファイルを表示*
6. **ソリューションエクスプローラー**で**CoffeeMinify.cs**ファイルを右クリックし、 **[プロジェクトに含める]** を選択します。

    ![CoffeeMinify.cs ファイルをプロジェクトに含める](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "CoffeeMinify.cs ファイルをプロジェクトに含める")

    *CoffeeMinify.cs ファイルをプロジェクトに含める*
7. **CoffeeMinify.cs**ファイルを開きます。

    このクラスは、JsMinify から継承して、CoffeeScript コードのコンパイルによって生成される JavaScript 出力を縮小します。 まず、CoffeeScript コンパイラを呼び出して JavaScript コードを生成します。次に、そのコードを JsMinify メソッドに送信して、結果のコードを縮小します。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. **Scripts/バンドル**フォルダーから**Script1**ファイルと**Script2**ファイルを開きます。

    これらのファイルには、CoffeeMinify クラスでのバンドルの実行中にコンパイルされる CoffeScript コードが含まれます。

    わかりやすくするために、提供される CoffeeScript ファイルには CoffeeScript サンプルコードのみが含まれています。 コメントは JsMinify プロセスによって除外されます。

    ![CoffeeScript ファイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript ファイル")

    *CoffeeScript ファイル*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/)は、javascript コードを記述したり、javascript の簡潔さと読みやすさを強化したり、配列の認識やパターンマッチングなどの他の機能を追加したりするための、より単純な構文を提供します。
9. **最適化 .aspx**ファイルを開き、バンドルリンクを見つけます。

    動的な**JS バンドル**へのリンクは、動的フォルダーバンドル用に構成した **/コーヒー**サフィックスを使用して、 **Scripts/バンドル**フォルダーを参照していることに注意してください。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. **F5**キーを押してアプリケーションを実行し、 **[最適化]** ページに移動します。
11. **[動的 JS バンドル]** リンクをクリックして、生成されたファイルを開きます。

    このバンドルに含まれていたコンテンツには、**コーヒー**ファイルのみが含まれていることに注意してください。 CoffeeScript コードが JavaScript にコンパイルされ、コメントアウトされた行が削除されていることを確認することもできます。

    ![動的 JS ファイルバンドル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "動的 JS ファイルバンドル")

    *動的 JS ファイルバンドル*

> [!NOTE]
> また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このラボでは、Visual Studio 2012 の ASP.NET および Web 開発の新機能と、Visual Studio 2012 のさまざまな拡張機能を活用する方法を理解することができます。

このハンズオンラボでは、CSS、JavaScript、HTML 用に Visual Studio 2012 エディターの新機能と機能強化を使用する方法について学習しました。 また、Visual Studio 2012 が組み込みのバンドルと縮小を実装する方法についても説明しました。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *VS Express for Web タイル*

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>タスク 1-Windows Azure ポータルから新しい Web サイトを作成する

1. [Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。

    > [!NOTE]
    > Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。 [ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。

    ![Windows Azure portal にログオンします。](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure portal にログオンします。")

    *Windows Azure 管理ポータルにログオンします。*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** から ip アドレスを選択して、 **[開始 Ip アドレス]** および **[終了 ip アドレス]** ボックスに貼り付けます。 規則の名前を入力し、[![の追加]](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) ボタンをクリックします。

    ![クライアント IP アドレスを追加しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *変更の確認*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します (例: *MVC4SampleDB*)。

     ![変換先の接続文字列を構成しています](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "データベース文字列の作成")

    *データベースの作成*
7. Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

    ![Windows Azure に発行されたアプリケーション](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure に発行されたアプリケーション")

    *Windows Azure に発行されたアプリケーション*
