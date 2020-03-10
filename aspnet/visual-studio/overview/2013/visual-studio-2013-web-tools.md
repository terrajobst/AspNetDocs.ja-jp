---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'ハンズオンラボ: Visual Studio 2013 Web ツール |Microsoft Docs'
author: rick-anderson
description: Visual Studio は、の優れた開発環境です。NET ベースの Windows および web プロジェクト。 これには、簡単に使用できる強力なテキストエディターが含まれています。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505006"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a>ハンズオンラボ: Visual Studio 2013 Web ツール

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

> Visual Studio は、の優れた開発環境です。NET ベースの Windows および web プロジェクト。 これには、プロジェクトなしでスタンドアロンファイルを編集するために簡単に使用できる強力なテキストエディターが含まれています。
> 
> Visual Studio では、各ファイルを編集するときに、すべての機能を備えた解析ツリーが維持されます。 これにより、Visual Studio は比類のないオートコンプリートとドキュメントベースのアクションを提供しながら、開発環境をはるかに高速かつ快適にすることができます。 これらの機能は、HTML および CSS ドキュメントで特に強力です。
> 
> また、拡張機能でもこの機能を利用できるため、必要に応じて強力な新機能を使用してエディターを簡単に拡張できます。 Web Essentials は、ほとんどの場合、Visual Studio の web 関連の拡張機能のコレクションです。 これには、多くの新しい IntelliSense 入力候補 (特に、CSS の場合)、新しいブラウザーリンク機能、JavaScript ファイルの自動 JSHint、HTML と CSS の新しい警告、および最新の web 開発に不可欠なその他多くの機能が含まれています。
> 
> すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。

<a id="Overview"></a>
## <a name="overview"></a>概要

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- 豊富な HTML5 コードスニペットや Zen コーディングなど、Web Essentials に含まれる新しい HTML エディター機能を使用する
- カラーピッカーやブラウザーマトリックスのツールヒントなど、Web Essentials に含まれる新しい CSS エディター機能を使用する
- すべての HTML 要素のファイルや IntelliSense の抽出など、Web Essentials に含まれる新しい JavaScript エディター機能を使用する
- ブラウザーリンクを使用してブラウザーと Visual Studio の間でデータを交換する

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このハンズオンラボを完了するには、次のものが必要です。

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)以上
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。

1. Windows エクスプローラーウィンドウを開き、ラボの**ソース**フォルダーを参照します。
2. **[Setup.exe]** を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。
3. ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。

> [!NOTE]
> セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>コードスニペットの使用

ラボドキュメント全体で、コードブロックを挿入するように指示されます。 便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。

> [!NOTE]
> 各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。 演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。 演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。 このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。

---

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [ブラウザーリンクと Web Essentials の操作](#Exercise1)
2. [コードスニペットと IntelliSense の活用](#Exercise2)

> [!NOTE]
> Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。 定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。 このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。 開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>演習 1: ブラウザーリンクと Web Essentials の操作

**Web Essentials**は、最新の web 開発に役立つさまざまな機能を追加する Visual Studio の拡張機能であり、ほとんどの場合、web 開発のエクスペリエンスをはるかに高速かつ快適にすることに重点を置いています。 Web Essentials は、Visual Studio の拡張機能ギャラリーからインストールできます。

**ブラウザーリンク**は Visual Studio 2013 に含まれる新機能であり、VISUAL studio IDE と、web アプリケーションと visual studio の間でデータを交換するための任意のオープンブラウザーの間のチャネルを提供します。 Web Essentials は、ブラウザーリンクをツールと共に拡張し、DOM オブジェクトモデルと web ページの CSS スタイルをブラウザーから直接操作します。

この演習では、簡単なクイズページを強化するために、 **Web Essentials**と**ブラウザーリンク**でサポートされている機能をいくつか紹介します。

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>タスク 1-複数のブラウザーでプロジェクトを実行する

このタスクでは、複数のブラウザーで同時に実行されるように web アプリケーションを構成します。これは、ブラウザー間のテストに役立ちます。

1. **Microsoft Visual Studio**を開きます。
2. **ファイル** メニューの 開く を選択します。 **プロジェクト/ソリューション...** ラボの**ソース**フォルダー (C:\WebCampsTK\HOL\VSWebTooling\Source) で**Ex1-WorkingwithBrowserLinkandWebEssentials\Begin**を参照します。 **[開始]** を選択し、 **[開く]** をクリックします。
3. Visual Studio のツールバーで、ブラウザー メニューを展開し、**参照** をクリックします。

    ![メニューオプションを使用して参照](visual-studio-2013-web-tools/_static/image1.png "参照...ブラウザーメニュー内")

    *メニューオプションを使用して参照*
4. [**ブラウザー**の選択] ダイアログボックスで、 **CTRL**キーを押しながら [**既定と**して設定] をクリックして、 **Google Chrome**と**Internet Explorer**の両方を選択します。

    ![[参照] ダイアログボックス](visual-studio-2013-web-tools/_static/image2.png "[参照] ダイアログボックス")

    *複数の既定のブラウザーの選択*
5. Google Chrome と Internet Explorer の両方が既定のブラウザーとして表示されるようになります。 **[キャンセル]** をクリックして、ダイアログボックスを閉じます。

    ![既定のブラウザーとしての Google Chrome および Internet Explorer](visual-studio-2013-web-tools/_static/image3.png "Google Chrome と Internet Explorer の既定のブラウザー")

    *既定のブラウザーとしての Google Chrome および Internet Explorer*

    > [!NOTE]
    > 既定のブラウザーを構成した後、ブラウザー メニューで **複数のブラウザー** オプションが選択されます。
    > 
    > ![複数のブラウザー](visual-studio-2013-web-tools/_static/image4.png "複数のブラウザー")
6. **CTRL** + **F5**キーを押して、デバッグなしでアプリケーションを実行します。
7. 両方のブラウザーウィンドウを開いたときに、両方のブラウザーで同時に更新プログラムを表示するために、どちらか一方を配置します。 ブラウザーには、薄い青の四角形の付いた web ページが表示されます。

    ![1つのブラウザーを他のブラウザーの上に配置する](visual-studio-2013-web-tools/_static/image5.png "1つのブラウザーを他のブラウザーの上に配置する")

    *1つのブラウザーを他のブラウザーの上に配置する*
8. ブラウザーを閉じないでください。 これらは、次のタスクで使用します。

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>タスク 2-Zen コーディングを使用して HTML 要素を作成する

**Zen コーディング**は、高速 HTML、XML、XSL (またはその他の構造化されたコード形式) のコーディングおよび編集用のエディタープラグインです。 このプラグインの中核となるのは、CSS セレクターに似た式を HTML コードに展開できる強力な省略形エンジンです。 Zen コーディングは、CSS スタイルセレクター構文を使用して HTML を記述する高速な方法です。

この演習では、Web Essentials によって提供される Zen コーディング機能を使用して、質問のオプションを表す HTML ボタンを生成します。

1. Visual Studio に戻ります。
2. **Views** | **ホーム**フォルダーにある**インデックスの cshtml**ファイルを開きます。
3. **&lt;!--TODO: [オプションの追加]--&gt;** コメントを次のコードに置き換え、 **tab**キーを押します。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. コードは HTML に展開する必要があります。

    ![拡張 HTML](visual-studio-2013-web-tools/_static/image6.png "拡張 HTML")

    *拡張 HTML*

    > [!NOTE]
    > Zen コーディング構文の詳細については、次の[記事](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)を参照してください。
5. [リンクされた**ブラウザーの更新**] ボタンをクリックして、両方のブラウザーを更新します。

    ![リンクされたブラウザーの更新](visual-studio-2013-web-tools/_static/image7.png "リンクされたブラウザーの更新")

    *リンクされたブラウザーの更新*

    ![Internet Explorer-4 つのボタンで更新されたページ](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-4 つのボタンで更新されたページ")

    *Internet Explorer-4 つのボタンで更新されたページ*

    ![Google Chrome-4 つのボタンで更新されたページ](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-4 つのボタンで更新されたページ")

    *Google Chrome-4 つのボタンで更新されたページ*
6. Visual Studio に戻ります。
7. ボタンをページに追加しましたが、それでもテンプレートの質問を追加する必要があります。 これを行うには、 **Lorem Ipsum generator**と呼ばれる Web Essentials の新機能を使用します。 **クラス**属性**front**の**div**要素を見つけます。
8. 次のコードを**div**の最初の子要素として追加し、 **tab**キーを押します。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. コードは HTML に展開する必要があります。

    ![Lorem Ipsum 自動生成](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 自動生成")

    *Lorem Ipsum 自動生成*

    > [!NOTE]
    > Zen コーディングの一部として、HTML エディターで直接 Lorem Ipsum コードを生成できるようになりました。 「 **Lorem** And Hit **TAB」** と入力するだけで、30ワード lorem Ipsum text が挿入されます。 例: *lorem10*によって 10 Lorem Ipsum 単語が挿入されます。
10. **Lorem Pixel generator**と呼ばれる Web Essentials の別の新機能を使用して、質問の一番上にロゴを追加します。 次のコードを**div**要素の最初の子要素として、**コンテナー**を**クラス**値として追加し、 **tab**キーを押します。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. コードは HTML に展開する必要があります。

    ![Lorem ピクセル自動生成](visual-studio-2013-web-tools/_static/image11.png "Lorem ピクセル自動生成")

    *Lorem ピクセル自動生成*

    > [!NOTE]
    > Zen コーディングの一部として、HTML エディターで直接 Lorem ピクセルコードを生成することもできます。 「 **Pix-200 x 200-** animal And Hit **TAB」** と入力するだけで、animal の 200 x 200 イメージを含む**img**タグが挿入されます。 詳細については、「 [Lorem ピクセル](http://www.lorempixel.com)」を参照してください。
12. [リンクされた**ブラウザーの更新**] ボタンをクリックして、両方のブラウザーを更新します。

    ![Internet Explorer で自動生成されたイメージとテキスト](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer で自動生成されたイメージとテキスト")

    *Internet Explorer で自動生成されたイメージとテキスト*

    ![Google Chrome で自動生成されたイメージとテキスト](visual-studio-2013-web-tools/_static/image13.png "Google Chrome で自動生成されたイメージとテキスト")

    *Google Chrome で自動生成されたイメージとテキスト*

    > [!NOTE]
    > コードスニペットを追加すると、イメージがランダムに選択されるため、ブラウザーに表示されるイメージが異なる場合があります。
13. ブラウザーを閉じないでください。 これらは、次のタスクで使用します。

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>タスク 3-スタイルプロパティの更新

このタスクでは、ブラウザーリンクの**検査モード**機能を使用して、特定の DOM 要素が生成される場所を正確に検出し、Web Essentials によって提供されるカラーピッカーを使用してその要素の color プロパティを更新します。

1. Internet Explorer ブラウザーで、 **CTRL** + **ALT** + **I**キーを押して、検査モードを有効にします。
2. 薄い青の境界線の上にポインターを移動し、[] をクリックします。

    ![薄い青の境界線の上にポインターを移動する](visual-studio-2013-web-tools/_static/image14.png "薄い青の境界線の上にポインターを移動する")

    *薄い青の境界線の上にポインターを移動する*
3. Visual Studio に戻ります。 Visual Studio HTML エディターで、ブラウザーで選択した HTML 要素も選択されていることに注意してください。

    ![Visual Studio HTML エディターで選択された HTML 要素](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML エディターで選択された HTML 要素")

    *Visual Studio HTML エディターで選択された HTML 要素*
4. 次に、選択した要素のスタイルを変更するために、 **front** CSS クラスを更新します。 これを行うには 、CTRL ** + キーを押し**て、 **[移動]** 検索ボックスを開きます。 「 **Site .Css** 」と入力し、 **enter**キーを押してファイルを開きます。

    ![ファイルサイト .css を開いています](visual-studio-2013-web-tools/_static/image16.png "ファイルサイト .css を開いています")

    *ファイルサイト .css を開いています*
5. **CTRL** + **F**キーを押し、「」と入力**し**て CSS セレクターを検索します。
6. クラスの [border] プロパティで薄い青色の四角をクリックして、カラーピッカーを開きます。

    ![カラーピッカーを開く](visual-studio-2013-web-tools/_static/image17.png "カラーピッカーを開く")

    *カラーピッカーを開く*
7. シェブロンボタンをクリックしてカラーピッカーを展開し、新しい色を選択します。

    ![カラーピッカーを展開する](visual-studio-2013-web-tools/_static/image18.png "カラーピッカーを展開する")

    *カラーピッカーを展開する*
8. **CTRL** + **ALT** ** + 押して、** リンクされたブラウザーを更新します。
9. Internet Explorer に切り替えて、境界線の色がどのように変化したかを確認します。

    ![Internet Explorer-境界線の色が更新されました](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-境界線の色が更新されました")

    *Internet Explorer-境界線の色が更新されました*
10. Google Chrome に切り替え、境界線の色がどのように変化したかを確認します。

    ![Google Chrome-更新された境界線の色](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-更新された境界線の色")

    *Google Chrome-更新された境界線の色*
11. Visual Studio に戻ります。
12. **Btn**セレクターを見つけるには、**サイトの .css**ファイルの末尾に移動し、 **CTRL** + **F**キーを押します。
13. **-Webkit**プロパティが緑色で下線が引かれていることに注意してください。

    ![-webkit-btn selector の radius プロパティ](visual-studio-2013-web-tools/_static/image21.png "-webkit-btn selector の radius プロパティ")

    *-webkit-btn selector の radius プロパティ*
14. **-Webkit-radius**プロパティにカレットを置きます。 プロパティの最初の単語の最初の文字の下に青い線が表示されます。 これは**スマートタグ**です。
15. **Ctrl** + キーを押し**ます。** [候補] メニューを開き、[**存在しない標準プロパティの追加] (罫線-半径)** をクリックします。

    ![不足している標準プロパティの追加の提案](visual-studio-2013-web-tools/_static/image22.png "不足している標準プロパティの追加の提案")

    *不足している標準プロパティの追加の提案*
16. **境界線**のプロパティが CSS 規則に自動的に追加されます。

    ![欠落した標準プロパティが追加されました](visual-studio-2013-web-tools/_static/image23.png "欠落した標準プロパティが追加されました")

    *欠落した標準プロパティが追加されました*
17. **境界半径**プロパティの上にポインターを移動すると、**ブラウザーのマトリックスのツールヒント**が表示されます。 **ブラウザーのマトリックスのツールヒント**には、各ブラウザーでプロパティが利用可能かどうかが表示されます。

    ![ブラウザーマトリックスのツールヒント](visual-studio-2013-web-tools/_static/image24.png "ブラウザーマトリックスのツールヒント")

    *ブラウザーマトリックスのツールヒント*
18. **Border-radius**プロパティの値に下線が表示されていることに注意してください。 値の上にポインターを移動すると、警告メッセージが表示されます。

    ![罫線-radius プロパティ値-警告](visual-studio-2013-web-tools/_static/image25.png "罫線-radius プロパティ値-警告")

    *罫線-radius プロパティ値-警告*
19. ツールヒントで提案されているように、**境界半径**プロパティ値の単位を削除します。
20. **境界線**として、丸みのある境界線の角を定義するための標準プロパティとして、 **-webkit-radius**プロパティと値を CSS 規則から削除できます。
21. **"ワードラップ**" プロパティにカレットを置き、スマートタグも下に表示されることを確認します。
22. メニューを開き、[**不足**しているベンダの詳細の追加] をクリックします。

    ![不足しているベンダーの詳細の提案の追加](visual-studio-2013-web-tools/_static/image26.png "不足しているベンダーの詳細の提案の追加")

    *不足しているベンダーの詳細の提案の追加*
23. **-Ms-ワードラップ**プロパティは、CSS 規則に自動的に追加されます。

    ![仕入先固有のプロパティの追加](visual-studio-2013-web-tools/_static/image27.png "仕入先固有のプロパティの追加")

    *仕入先固有のプロパティの追加*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>タスク 4-ブラウザーから HTML コードを更新する

このタスクでは、ブラウザーリンクの**デザインモード**機能を使用して、ブラウザーから DOM オブジェクトを編集し、Visual STUDIO の HTML ソースファイルに変更を転送します。

1. Google Chrome で、 **CTRL** + **ALT** + **D**キーを押してデザインモードを有効にします。
2. **Lorem Ipsum dolor 座っ amet**ラベルの上にポインターを移動し、[] をクリックします。

    ![質問の編集](visual-studio-2013-web-tools/_static/image28.png "質問の編集")

    *質問の編集*
3. カーソルが表示されます。 元のテキストを、*長い質問を書いたときに表示される内容*に置き換え、 **ESC**キーを押してデザインモードを終了します。

    ![編集した質問](visual-studio-2013-web-tools/_static/image29.png "編集した質問")

    *編集した質問*
4. Visual Studio に戻り、(まだ開いていない場合は) **cshtml**を開きます。 **&lt;p&gt;** 要素の内部テキストが更新されていることに注意してください。

    ![HTML ページで更新された質問](visual-studio-2013-web-tools/_static/image30.png "HTML ページで更新された質問")

    *HTML ページで更新された質問*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>タスク 5 - 変更履歴の SEO に関連する警告

**検索エンジンの最適化**(SEO) は、検索エンジンの結果の一覧で web サイトの順位を高くするプロセスです。 サイトの順位が高く、より一貫して一覧表示されていれば、その検索エンジンからサイトが取得する訪問者の数が増えます。 Web Essentials には、HTML を検査して検出された問題を報告し、それらを修正するためのサポートを提供する分析ツールが組み込まれています。

1. **[表示]** メニューにアクセスし、 **[エラー一覧]** をクリックして **[エラー一覧]** ウィンドウを開きます。

    ![[表示] メニューのエラー一覧](visual-studio-2013-web-tools/_static/image31.png "[表示] メニューのエラー一覧")

    *[表示] メニューのエラー一覧*
2. **&lt;メタ&gt;** タグがページの説明に含まれていないことを通知する SEO 警告が表示されていることに注意してください。 SEO 警告エントリをダブルクリックして修正します。

    ![[エラー一覧] ウィンドウ](visual-studio-2013-web-tools/_static/image32.png "[エラー一覧] ウィンドウ")

    *[エラー一覧] ウィンドウ*
3. **[Web Essentials]** ダイアログボックスで、 **[はい]** をクリックして説明 &lt;meta&gt; タグに挿入します。

    ![[Web Essentials] ダイアログボックス](visual-studio-2013-web-tools/_static/image33.png "[Web Essentials] ダイアログボックス")

    *[Web Essentials] ダイアログボックス*
4. **\_Layout**のエディターが開き、 **&lt;meta&gt;** タグが HTML ファイルの**head**セクションに自動的に追加されます。

    ![_Layout ページに自動的に追加された Meta タグ](visual-studio-2013-web-tools/_static/image34.png "_Layout ページに自動的に追加された Meta タグ")

    *\_レイアウトページに自動的に追加された Meta タグ*
5. **Content**属性の値を*GeekQuiz*に変更し、ファイルを保存します。

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>演習 2: コードスニペットと IntelliSense の活用

Web Essentials では、HTML エディターは追加機能を使用して拡張されています。 この演習では、web アプリケーションを開発する際に役立ついくつかの新機能について紹介します。

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>タスク 1-HTML ドキュメントでの IntelliSense の使用

このタスクに表示される最初の新機能は、**動的 IntelliSense**と呼ばれます。 動的 IntelliSense では、他のタグや属性を読み取って、使用する可能性のある id を推測します。

このタスクでは、ラベルと入力フィールドを含む新しい HTML フォーム要素を作成します。 次に、の属性をラベルに追加して入力にバインドします。これにより、スコープ内の入力の id に基づいて IntelliSense**の**候補が表示されます。

1. **Web 用 Visual Studio Express 2013**を開き、 **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/begin**フォルダーにある**ソリューションを開きます。** または、前の演習で取得したソリューションを続行することもできます。
2. **ソリューションエクスプローラー**で、 **Views** | **ホーム**フォルダーにある**インデックスの cshtml**ファイルを開きます。
3. **&lt;section&gt;** 要素内に次のフォームを追加します。

    (コードスニペット- *VisualStudio2013WebTooling* - *Ex2* - *フォーム*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 入力タグの前には、フィールドの説明を含むラベルを付ける必要があります。 入力タグの前に次のラベルを追加します。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. ラベル**のバインド**先のフォーム要素を指定 **&gt;&lt;ラベル**の属性。 属性の値は、関連する要素の id と同じである必要があります。 **&lt;label&gt;** 要素に**for**属性を追加します。 次の図に示すように、同じスコープ (外側の **&lt;フォーム&gt;** ) 内の要素の id に基づいて、[IntelliSense] ボックスに &quot;名&quot; 値がポップアップ表示されます。

    ![IntelliSense で id を表示する](visual-studio-2013-web-tools/_static/image35.png "IntelliSense で id を表示する")

    *IntelliSense で id を表示する*
6. 最近追加された **&lt;フォーム&gt;** 要素とその内容を削除します。

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>タスク 2-HTML コードスニペットの使用

HTML5 では、25個を超える新しいセマンティックタグが導入されました。 Visual Studio には既にこれらのタグの IntelliSense がサポートされていましたが、Visual Studio 2013 新しいコードスニペットを追加することにより、マークアップの記述が高速で簡単になります。 これらのタグは複雑ではありませんが、*オーディオ*タグに適切なコーデックフォールバックを追加するなど、若干の微妙な違いがあります。 このタスクでは、オーディオタグの HTML コードスニペットを確認します。

1. **Index. cshtml**ファイルで、次の図に示すように、 **&lt;セクション&gt;** 要素内に **&lt;aud**と入力します。

    ![オーディオ要素の挿入](visual-studio-2013-web-tools/_static/image36.png "オーディオ要素の挿入")

    *オーディオ要素の挿入*
2. **Tab**キーを2回押して、ページに次のコードが追加され、カーソルが最初のソースの**src**属性に配置されていることを確認します。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > **Tab**キーを2回押すと、コードスニペットが挿入されます。 オーディオスニペットは、サポートを強化するために2つのソースファイルを使用して、*オーディオ*タグの標準的な使用方法を示しています。
3. 2行目を削除し、最初の行のソースを更新します。次のリンクを使用して、Webキャンプ Stv Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)にします。 結果のコードは次のようになります。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > ソースファイル*KatanaProject*が例として使用されています。 必要に応じて、別のソースを使用することもできます。
4. **Ctrl** + **S**キーを押して、ファイルを保存します。
5. **CTRL** + **F5**キーを押してアプリケーションを起動します。
6. オーディオプレーヤーがアプリケーションに追加されたことに注意してください。

    ![Internet Explorer のオーディオプレーヤー](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer のオーディオプレーヤー")

    *Internet Explorer のオーディオプレーヤー*

    ![Google Chrome のオーディオプレーヤー](visual-studio-2013-web-tools/_static/image38.png "Google Chrome のオーディオプレーヤー")

    *Google Chrome のオーディオプレーヤー*
7. ブラウザーを閉じないでください。 これらは、次のタスクで使用します。

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>タスク 3-JavaScript ドキュメントでの IntelliSense の使用

Web Essentials 2013 では、スタイルシートと HTML ページによって、Id とクラス名の一覧が生成されます。 このタスクでは、Web Essentials 2013 での JavaScript IntelliSense のサポートを向上させる方法について説明します。

1. **Index. cshtml**ファイルに次のコードを追加して、JavaScript コードの**スクリプト**タグを定義します。

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. **スクリプト**タグ内に次のコードを追加して、準備完了のコールバック関数を定義します。

    (コードスニペット- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. **スクリプト**タグにカレットを置き、 **ctrl** + キーを押し**ます。** を開き、[候補] メニューを開きます。
4. [ **Extract To File] を**クリックします。

    ![JavaScript によるファイルへの抽出の提案](visual-studio-2013-web-tools/_static/image39.png "JavaScript によるファイルへの抽出の提案")

    *JavaScript によるファイルへの抽出の提案*
5. **[名前を付けて保存]** ウィンドウで**Scripts**フォルダーを選択し、ファイルに「 **init** 」という名前を付けて、 **[保存]** をクリックします。

    ![ウィンドウとして保存](visual-studio-2013-web-tools/_static/image40.png "ウィンドウとして保存")

    *ウィンドウとして保存*

    > [!NOTE]
    > この場合、**初期化**ファイルが作成され、スクリプトの内容がファイルに移動されます。
    > 
    > ![含まれているコンテンツを使用して作成された初期化 .js ファイル](visual-studio-2013-web-tools/_static/image41.png "含まれているコンテンツを使用して作成された初期化 .js ファイル")
    > 
    > *含まれているコンテンツを使用して作成された初期化 .js ファイル*
6. インデックスの**cshtml**ファイルを開き、スクリプトタグが**初期化**ファイルへの参照に置き換えられていることを確認します。

    ![Js html リファレンス](visual-studio-2013-web-tools/_static/image42.png "Js html リファレンス")

    *Js html リファレンス*
7. **ソリューションエクスプローラー**にアクセスして、ソリューションに**初期化**ファイルが自動的に含まれていることを確認します。

    ![ソリューションに含まれている初期 .js ファイル](visual-studio-2013-web-tools/_static/image43.png "ソリューションに含まれている初期 .js ファイル")

    *ソリューションに含まれている初期 .js ファイル*
8. **Init**ファイルに戻り、**準備ができ**ている関数のコールバックを更新します。
9. *準備完了*に渡される関数コールバック定義内で、次のコードを追加して、特定のクラス属性によってすべての要素を取得します。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. **GetElementsByClassName**関数呼び出し内の引用符の間に、 **ctrl** + **Space**キーを押します。

    ![GetElementsByClassName 関数の IntelliSense を表示する](visual-studio-2013-web-tools/_static/image44.png "GetElementsByClassName 関数の IntelliSense を表示する")

    *GetElementsByClassName 関数の IntelliSense を表示する*

    > [!NOTE]
    > IntelliSense により、プロジェクトのスタイルシートで定義されているクラスが表示されることに注意してください。
11. 作成した行を次のコードで置き換えます。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. **GetElementsByTagName**関数の引用符内に、 **au**の後にカーソルを置き、 **ctrl** + **Space**キーを押します。

    ![GetElementByTagName メソッドの IntelliSense を表示する](visual-studio-2013-web-tools/_static/image45.png "GetElementByTagName メソッドの IntelliSense を表示する")

    *GetElementsByTagName メソッドの IntelliSense を表示する*
13. 一覧から [ **&quot;audio&quot;** ] を選択し、 **enter キーを**押します。 結果を次の例に示します。

    ![取得 (オーディオ要素を)](visual-studio-2013-web-tools/_static/image46.png "取得 (オーディオ要素を)")

    *取得 (オーディオ要素を)*
14. **ソリューションエクスプローラー**で、 **Scripts**フォルダー内の**init**ファイルを右クリックして、 **[Web Essentials]** メニューの **[minify JavaScript ファイル]** を選択します。

    ![JavaScript ファイルをミニする](visual-studio-2013-web-tools/_static/image47.png "JavaScript ファイルをミニにする")

    *JavaScript ファイルをミニする*
15. ソースファイルの変更時に自動縮小を有効にするように求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![自動縮小の警告を有効にする](visual-studio-2013-web-tools/_static/image48.png "自動縮小の警告を有効にする")

    *自動縮小の警告を有効にする*

    > [!NOTE]
    > 初期化された **.js** **ファイルの**依存関係として追加されます。
    > 
    > ![作成された、最小の .js ファイル](visual-studio-2013-web-tools/_static/image49.png "作成された、最小の .js ファイル")
    > 
    > *作成された、最小の .js ファイル*
16. ファイルが縮小されていることを確認**します。**

    ![.Js ファイルの内容を初期化します。](visual-studio-2013-web-tools/_static/image50.png ".Js ファイルの内容を初期化します。")

    *.Js ファイルの内容を初期化します。*
17. **GetElementsByTagName**関数の呼び出しの下に次のコードを**追加して**、すべてのオーディオ要素を再生します。

    (コードスニペット- *VisualStudio2013WebTooling* - *Ex2* - *playaudioelements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. CTRL + **S** **キーを押し**て、ファイルを保存します。 縮小表示ファイルは既に開かれているため、ファイルがソースエディターの外部で変更されたことを示すダイアログボックスが表示されます。 **[はい]** をクリックします。

    ![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
19. 新しいコードでファイルが更新されたことを確認するために、**初期の .js**ファイルに戻ります。

    ![初期の .js ファイルの更新](visual-studio-2013-web-tools/_static/image52.png "初期の .js ファイルの更新")

    *初期の .js ファイルの更新*
20. ブラウザーの**リンク**の [更新] ボタンをクリックします。
21. 両方のブラウザーが更新されると、前のタスクで表示されたオーディオプレーヤーが自動的に再生を開始します。

    ![オーディオプレーヤーがビューに含まれる](visual-studio-2013-web-tools/_static/image53.png "オーディオプレーヤーがビューに含まれる")

    *オーディオプレーヤーがビューに含まれる*

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了することで、次の方法を学習できました。

- 豊富な HTML5 コードスニペットや Zen コーディングなど、Web Essentials に含まれる新しい HTML エディター機能を使用する
- カラーピッカーやブラウザーマトリックスのツールヒントなど、Web Essentials に含まれる新しい CSS エディター機能を使用する
- すべての HTML 要素のファイルや IntelliSense の抽出など、Web Essentials に含まれる新しい JavaScript エディター機能を使用する
- ブラウザーリンクを使用してブラウザーと Visual Studio の間でデータを交換する
