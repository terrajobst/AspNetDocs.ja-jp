---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 2012 での Page Inspector の使用 |Microsoft Docs
author: rick-anderson
description: このハンズオンラボでは、Visual Studio での web ページの問題を見つけて修正するための新しいツールを紹介します (Page Inspector)。 Page Inspector は新しいツールです。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473800"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a>Visual Studio 2012 で Page Inspector を使用する

[Web キャンプチーム](https://twitter.com/webcamps)別

> このハンズオンラボでは、Visual Studio での web ページの問題を見つけて修正するための新しいツールを紹介します (Page Inspector)。
> 
> Page Inspector は、ブラウザー診断ツールを Visual Studio に導入し、ブラウザー、ASP.NET、ソースコードの間で統合されたエクスペリエンスを提供する新しいツールです。 Web ページ (HTML、Web フォーム、ASP.NET MVC、または Web ページ) を Visual Studio IDE 内で直接レンダリングし、ソースコードと結果の出力の両方を調べることができます。 Page Inspector を使用すると、web サイトを簡単に分解したり、ページをすぐにすばやく構築したり、問題を迅速に診断したりすることができます。
> 
> 今日では、ASP.NET MVC や WebForms など、柔軟でスケーラブルな web サイトをタイムリーに作成できる Web フレームワークが数多く用意されています。 一方、IDE では、テンプレートベースのページと動的コンテンツのデザイナービューがサポートされていないため、ページの問題を見つけるのが困難になります。 そのため、これらの web サイトをユーザーに表示するには、ブラウザーで開いている必要があります。
> 
> Web 開発者は、外部ツールを使用して、ブラウザーで定期的に実行される問題を見つけます。 次に、IDE に戻り、修正を開始します。 これにより、IDE、ブラウザー、およびプロファイリングツールが非効率的になり、問題を再現するたびに、新しい配置とキャッシュのクリーニングが必要になる場合があります。
> 
> Page Inspector は、結合された一連の機能を使用して、両方の長所を組み合わせて、クライアント (ブラウザーツール) とサーバー (ASP.NET とソースコード) の間の Web 開発のギャップを橋渡しします。
> 
> Page Inspector を使用すると、ブラウザーに表示される HTML マークアップを生成したソースファイル内の要素 (サーバー側コードを含む) を確認できます。 また Page Inspector を使用すると、CSS のプロパティや DOM 要素の属性を変更して、変更がブラウザーに直ちに反映されるようにすることもできます。
> 
> このハンズオンラボでは、Page Inspector 機能について説明し、Web アプリケーションの問題を解決するためにそれらを使用する方法を示します。 **このラボには、似たフローを使用する2つの演習が含まれていますが、さまざまなテクノロジが対象ASP.NET MVC Developer の場合は、練習1を実行します。WebForms の開発者の場合は、練習2を実行**します。
> 
> このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。
> 
> すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- Page Inspector を使用して Web サイトを分解する
- Page Inspector を使用した CSS スタイルの変更の検査とプレビュー
- Page Inspector を使用して web ページの問題を検出して修正する

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このラボを完了するには、次の項目が必要です。

- Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。
- Internet Explorer 9 以降

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [演習 1: ASP.NET MVC プロジェクトでの Page Inspector の使用](#Exercise1)
2. [演習 2: WebForms プロジェクトでの Page Inspector の使用](#Exercise2)

> [!NOTE]
> 各演習には、演習の Begin フォルダーにある開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行できます。 演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む終了フォルダーも検索します。 このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。

このラボの推定所要時間: **30 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>演習 1: ASP.NET MVC プロジェクトでの Page Inspector の使用

この演習では、 **Page Inspector**を使用して**ASP.NET MVC 4**ソリューションをプレビューし、デバッグする方法について説明します。 まず、ツールについて簡単に説明して、Web デバッグプロセスを容易にする機能について学習します。 次に、スタイルの問題を含む web ページで作業を行います。 Page Inspector を使用して、問題を生成して修正するソースコードを見つける方法について説明します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>タスク 1-Page Inspector の調査

このタスクでは、フォトギャラリーを表示する ASP.NET MVC 4 プロジェクトのコンテキストで Page Inspector を使用する方法について説明します。

1. **Source/Ex1-MVC4/begin/** folder にある**begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. ソリューションエクスプローラーで、 **[/]** ビュー プロジェクトフォルダーの下にある **[インデックス]** を見つけて右クリックし、 **[Page Inspector で表示]** を選択します。

    ![プレビューするファイルを選択 Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "プレビューするファイルを選択 Page Inspector")

    *プレビューするファイルを選択 Page Inspector*
3. [Page Inspector] ウィンドウに、選択したソースビューにマップされている */Home/Index* URL が表示されます。

    ![PageInspector を使用した最初の連絡先](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *の最初の連絡先 Page Inspector*

    Page Inspector ツールは、Visual Studio 環境に統合されています。 インスペクターには、強力な HTML プロファイラーと共に、埋め込みブラウザーが含まれています。 ソリューションを実行して、ページの外観を確認する必要がないことに注意してください。

    > [!NOTE]
    > Page Inspector ブラウザーの幅が、開いているページの幅よりも小さい場合、ページは正しく表示されません。 そのような場合は、Page Inspector の幅を調整します。
4. Page Inspector の **[ファイル]** タブをクリックします。

    インデックスページを作成しているすべてのソースファイルが表示されます。 この機能は、すべての要素を一目で特定するのに役立ちます。特に、部分的なビューとテンプレートを操作する場合に役立ちます。 リンクをクリックすると、各ファイルを開くこともできます。

    ![-Files-tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *[ファイル] タブ*
5. タブの左側にある **[トグル検査モード]** ボタンをクリックします。

    このツールを使用すると、ページの任意の要素を選択し、HTML および Razor コードを表示できます。

    ![トグル/検査-モード-ボタン](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *検査モードボタンの切り替え*
6. Page Inspector ブラウザーで、ページ要素の上にマウスポインターを移動します。 表示されるページの任意の部分にマウスポインターを移動すると、要素の種類が表示され、対応するソースマークアップまたはコードが Visual Studio エディターで強調表示されます。

    ![検査モードが動作しています](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *検査モードが動作しています*

    > [!NOTE]
    > [Page Inspector] ウィンドウを最大化しないでください。または、ソースコードが表示されている [プレビュー] タブを表示できなくなります。 Page Inspector の要素をクリックすると、その要素が最大化されると、選択したソースコードが表示されますが、Page Inspector ウィンドウは非表示になります。

    **インデックスの cshtml**ファイルに注意を払うと、選択した要素を生成するソースコードの部分が強調表示されていることがわかります。 この機能により、長いソースファイルの編集が容易になり、コードに直接アクセスできるようになります。

    ![検査 (要素を)](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *検査 (要素を)*
7. **[検査モードの切り替え]** ボタンをクリックします ([![html] タブを選択すると、Page Inspector ブラウザーに表示される html コードが表示されます。](using-page-inspector-in-visual-studio-2012/_static/image7.png "[HTML] タブを選択すると、Page Inspector ブラウザーに表示される HTML コードが表示されます。") ) 、カーソルを無効にします。
8. **[Html]** タブを選択すると、Page Inspector ブラウザーに表示される html コードが表示されます。
9. HTML マークアップで、[オブジェクト] リンクがあるリスト項目を見つけて選択します。

    コードを選択すると、対応する出力がブラウザーで自動的に強調表示されることに注意してください。 この機能は、HTML ブロックがページにどのように表示されるかを確認するのに役立ちます。

    ![ページ内の HTML 要素の選択](using-page-inspector-in-visual-studio-2012/_static/image8.png "ページ内の HTML 要素の選択")

    *ページ内の HTML 要素の選択*
10. **[検査モードの切り替え]** ボタンをクリックして*検査モード*を有効にし、ナビゲーションバーをクリックします。 HTML コードの右側にある [スタイル] ペインに、選択した要素に CSS スタイルが適用された一覧が表示されます。

    > [!NOTE]
    > ヘッダーはサイトレイアウトの一部であるため、Page Inspector は \_Layout ファイルも開き、影響を受けるコードのセグメントを強調表示します。

    ![スタイルの検出](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *選択した要素のスタイルとソースファイルの検出*
11. トグルインスペクションポインターが有効になっている状態で、マウスポインターを青いおすすめバーの下に移動し、半円をクリックします。

    ![要素の選択](using-page-inspector-in-visual-studio-2012/_static/image10.png "要素の選択")

    *要素の選択*
12. スタイルペインで、 **[...]** グループの下にある**背景画像**項目を見つけます。 **背景イメージ**を**オフ**にして、何が起こるかを確認します。 ブラウザーに変更がすぐに反映され、円が非表示になっていることがわかります。

    > [!NOTE]
    > [Page Inspector スタイル] タブで適用した変更は、元のスタイルシートには影響しません。 スタイルの選択を解除したり、必要な数だけ値を変更したりできますが、ページを更新した後に復元されます。

    ![CSS スタイルの有効化と無効化](using-page-inspector-in-visual-studio-2012/_static/image11.png "CSS スタイルの有効化と無効化")

    *CSS スタイルの有効化と無効化*
13. 次に、検査モードを使用して、ヘッダーの "your**logo here**" テキストをクリックします。
14. **[スタイル]** タブで、 **[サイト-タイトル]** グループの下の **[フォントサイズ]** CSS 属性を見つけます。 属性値をダブルクリックし、2.3 em 値を**3 em**に**置き換えて、enter キーを**押します。 タイトルが大きくなっていることに注意してください。

    ![Page Inspector での CSS 値の変更](using-page-inspector-in-visual-studio-2012/_static/image12.png "Page Inspector での CSS 値の変更")

    *Page Inspector での CSS 値の変更*
15. Page Inspector の右ペインにある **[トレーススタイル]** タブをクリックします。 これは、選択に適用されているすべてのスタイルを属性名順に表示するための別の方法です。

    ![CSS スタイルのトレース](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *選択された要素の CSS スタイルのトレース*
16. Page Inspector のもう1つの機能は、レイアウトペインです。 検査モードを使用して、ナビゲーションバーを選択し、右側のウィンドウの **[レイアウト]** タブをクリックします。 選択した要素の正確なサイズに加え、オフセット、余白、余白、および境界線のサイズが表示されます。 このビューから値を変更することもできます。

    ![Page Inspector での要素のレイアウト](using-page-inspector-in-visual-studio-2012/_static/image14.png "Page Inspector での要素のレイアウト")

    *Page Inspector での要素のレイアウト*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>タスク 2-フォトギャラリーでのスタイルの問題の検出と修正

以前のバージョンの Visual Studio で Web ページの問題を診断するにはどうすればよいですか。 Internet Explorer 開発者ツールや焼討バグなど、Visual Studio IDE の外部で実行される web デバッグツールに慣れている場合があります。 ブラウザーは HTML、スクリプト、およびスタイルを理解するだけで、基になるフレームワークはレンダリングされる HTML を生成します。 そのため、多くの場合、サイト全体を展開して、web ページの外観を確認する必要があります。

Web サイトの問題を検出して修正する場合は、次の手順に従うことをお勧めします。

1. Visual Studio からソリューションを実行するか、web サーバーにページを配置します。
2. ブラウザーで、使用する開発者ツールを開くか、ソースコードとスタイルを開いて問題を解決します。 関連するファイルを見つけるには、&quot;検索&quot; を使用するか、スタイルクラスの名前を使用してファイル&quot; 機能を検索 &quot;ます。
3. エラーが検出されたら、Web ブラウザーとサーバーを停止します。
4. ブラウザーのキャッシュをクリアします。
5. 修正プログラムを適用するには、Visual Studio に戻ります。 テストするすべての手順を繰り返します。

ASP.NET MVC 4 には実際の WYSIWYG は存在しないため、web アプリケーションを実行またはデプロイした後で、スタイルの問題のほとんどが後の段階で検出されます。 現在、Page Inspector では、ソリューションを実行せずに任意のページをプレビューすることができます。

このタスクでは、Page inspector を使用して、フォトギャラリーアプリケーションのいくつかの問題を修正します。

1. Page Inspector を使用して、ヘッダーの左側にある**レジスタ**と**ログイン**リンクを見つけます。

    リンクは右側に期待される場所に表示されず、箇条書きリストのように表示されることに注意してください。 次に、リンクを右揃えにして、適切にスタイルを調整します。

    ![登録とログインのリンクの検索](using-page-inspector-in-visual-studio-2012/_static/image15.png "登録とログインのリンクの検索")

    *登録とログインのリンクの検索*
2. トグル検査モードを選択した状態で、[登録] リンクをクリックしてコードを開きます。

    リンクのソースコードは **\_LoginPartial**ファイルにあります。これは、最初に見られる場所である、インデックス番号と \_の形式ではありません。 正しいソースファイルに直接配置されています。
3. **[スタイル]** タブで、[ **\<] セクション**を見つけてクリックします。これは、これらのリンクの HTML コンテナーである #login 項目 > ます。

    クリックすると、 **[#login]** スタイルが **[.css]** に自動的に配置されます。 さらに、コードが強調表示されるようになりました。

    ![CSS スタイルの選択](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS スタイルの選択")

    *CSS スタイルの選択*
4. 強調表示されたコード内の**テキストの整列**属性のコメントを解除します。そのためには、開始文字と終了文字を削除して、**サイトの .css**ファイルを保存します。

    Page Inspector は、現在のページを構成するすべての異なるファイルを認識し、これらのファイルのいずれかが変更されたときに検出することができます。 ブラウザーの現在のページがソースファイルと同期されていない場合は、いつでもアラートが生成されます。
5. Page Inspector ブラウザーで、アドレスバーの下にあるバーをクリックして、ページを再度読み込みます。

    ![ページの再読み込み](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *ページの再読み込み*

    リンクは右側に表示されていますが、箇条書きのように見えます。 ここで、箇条書きを削除して、リンクを水平方向に揃えます。

    ![更新されたページ](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *更新されたページ*
6. 検査モードを使用して、&quot;レジスタ&quot; を含む任意の **&lt;li&gt;** 項目を選択し &quot;リンクを&quot; します。 次に、[ **&lt;] セクション&gt; #login**項目をクリックして、**スタイルの .css**コードにアクセスします。

    ![スタイルの検索](using-page-inspector-in-visual-studio-2012/_static/image19.png "スタイルの検索")

    *スタイルの検索*
7. **.Css**で **#login li**項目のコードをコメント解除します。 追加するスタイルによって、行頭文字が非表示になり、項目が横方向に表示されます。

    ![ログインリンクのスタイルを再設定する](using-page-inspector-in-visual-studio-2012/_static/image20.png "ログインリンクのスタイルを再設定する")

    *ログインリンクのスタイルを再設定する*
8. **スタイルの .css**ファイルを保存し、アドレスの下にあるバーで [1 回] をクリックして、ページを再度読み込みます。 リンクが正しく表示されていることを確認します。

    ![右側に合わせたリンク](using-page-inspector-in-visual-studio-2012/_static/image21.png "右側に合わせたリンク")

    *右側に合わせたリンク*
9. 最後に、ヘッダーのタイトルを変更します。 検査モードを使用して、**ここでロゴ**をクリックすると、そのテキストを生成するソースコードが表示されます。
10. これで、 **Layout\_** になりました。 '**logo**' のテキストを '**フォトギャラリー**' で置き換えます。 Page Inspector ブラウザーを保存して更新します。

    ![新しいタイトルの割り当て](using-page-inspector-in-visual-studio-2012/_static/image22.png "新しいタイトルの割り当て")

    *新しいタイトルの割り当て*

    ![フォトギャラリーページ](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *フォトギャラリーページが更新されました*
11. 最後に、 **Photogallery**プロジェクトを選択し、 **F5**キーを押してアプリを実行します。 すべての変更が期待どおりに動作することを確認します。

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>演習 2: WebForms プロジェクトでの Page Inspector の使用

この演習では、Page Inspector を使用して WebForms ソリューションをプレビューおよびデバッグする方法について説明します。 まず、ツールについて簡単に説明して、Web デバッグプロセスを容易にする Page Inspector 機能について学習します。 次に、スタイルの問題を含む web ページで作業を行います。 Page Inspector を使用して、問題を生成して修正するソースコードを見つける方法について説明します。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>タスク 1-Page Inspector の調査

このタスクでは、フォトギャラリーを表示する WebForms プロジェクトのコンテキストで Page Inspector 機能を使用する方法について説明します。

1. **Source/Ex2-WebForms/begin/** folder にある**begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. ソリューションエクスプローラーで**default.aspx**ページを検索し、右クリックして、 **[Page Inspector で表示]** を選択します。

    ![Page Inspector で default.aspx を開く](using-page-inspector-in-visual-studio-2012/_static/image24.png "Page Inspector で default.aspx を開く")

    *Page Inspector で default.aspx を開く*
3. Page Inspector ウィンドウに default.aspx が表示されます。

    ![Page Inspector で default.aspx を表示する](using-page-inspector-in-visual-studio-2012/_static/image25.png "Page Inspector で default.aspx を表示する")

    *Page Inspector で default.aspx を表示する*

    Page Inspector ツールは、Visual Studio 環境に統合されています。 インスペクターには、選択したコードを表示する強力な HTML プロファイラーと共に、埋め込みブラウザーが含まれています。 ソリューションを実行して、ページの外観を確認する必要がないことに注意してください。

    > [!NOTE]
    > Page Inspector ブラウザーの幅が、開いているページの幅よりも小さい場合、ページは正しく表示されません。 そのような場合は、Page Inspector の幅を調整します。
4. Page Inspector の **[ファイル]** タブをクリックします。

    レンダリングされた既定のページを作成しているすべてのソースファイルが表示されます。 これは、特にユーザーコントロールやマスターページを操作しているときに、すべての要素を一目で確認するのに便利な機能です。 各ファイルに移動することもできます。

    ![[ファイル] タブ](using-page-inspector-in-visual-studio-2012/_static/image26.png "[ファイル] タブ")

    *[ファイル] タブ*
5. タブの左側にある **[トグル検査モード]** ボタンをクリックします。

    このツールを使用すると、ページの任意の要素を選択し、その HTML コードと .aspx ソースを表示できます。

    ![検査モードボタンの切り替え](using-page-inspector-in-visual-studio-2012/_static/image27.png "検査モードボタンの切り替え")

    *検査モードボタンの切り替え*
6. Page Inspector ブラウザーで、ページ要素の上にマウスポインターを移動します。 表示されるページの任意の部分にマウスポインターを移動すると、要素の種類が表示され、対応するソースマークアップまたはコードが Visual Studio エディターで強調表示されます。

    ![検査モードが動作しています](using-page-inspector-in-visual-studio-2012/_static/image28.png "検査モードが動作しています")

    *検査モードが動作しています*

    > [!NOTE]
    > [Page Inspector] ウィンドウを最大化しないでください。または、ソースコードが表示されている [プレビュー] タブを表示できなくなります。 Page Inspector の要素をクリックすると、その要素が最大化されると、選択したソースコードが表示されますが、Page Inspector ウィンドウは非表示になります。

    **Default.aspx**ファイルに注意を払う場合は、選択した要素を生成するソースコードの部分が強調表示されていることがわかります。 この機能により、長いソースファイルのエディションが容易になり、コードに直接アクセスできるようになります。

    ![検査 (要素を)](using-page-inspector-in-visual-studio-2012/_static/image29.png "検査 (要素を)")

    *検査 (要素を)*
7. **[検査モードの切り替え]** ボタンをクリックします (![-HTML--html-tab](using-page-inspector-in-visual-studio-2012/_static/image30.png "[-HTML]-[-HTML-html----------------------]-[ブラウザー] を選択します。") ---------------)-ブラウザーをクリックします。 ) 、カーソルを無効にする、Page Inspector のタブにあります。
8. **[Html]** タブを選択すると、Page Inspector ブラウザーに表示される html コードが表示されます。
9. HTML コードで、[] リンクをクリックしてリスト項目を探し、それを選択します。

    コードを選択すると、対応する出力が自動的に強調表示されたブラウザーになります。 この機能は、HTML ブロックがページにどのように表示されるかを確認するのに役立ちます。

    ![ページ内の HTML 要素の選択](using-page-inspector-in-visual-studio-2012/_static/image31.png "ページ内の HTML 要素の選択")

    *ページ内の HTML 要素の選択*
10. **[検査モードの切り替え]** ボタンをクリックして*検査モード*を有効にし、ナビゲーションバーをクリックします。 HTML コードの右側にある [スタイル] ペインに、選択した要素に CSS スタイルが適用された一覧が表示されます。

    > [!NOTE]
    > ヘッダーはサイトレイアウトの一部であるため、Page Inspector によって、サイトのマスターファイルも開き、影響を受けるコードのセグメントが強調表示されます。

    ![スタイルの検出 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "選択した要素のスタイルとソースファイルの検出")

    *選択した要素のスタイルとソースファイルの検出*
11. トグルインスペクションポインターが有効になっている状態で、マウスポインターをメニューバーの下に移動し、空白の円をクリックします。

    ![要素の選択](using-page-inspector-in-visual-studio-2012/_static/image33.png "要素の選択")

    *要素の選択*
12. スタイルペインで、 **[...]** グループの下にある**背景画像**項目を見つけます。 **背景イメージ**を**オフ**にして、何が起こるかを確認します。 ブラウザーに変更がすぐに反映され、円が非表示になっていることがわかります。

    > [!NOTE]
    > [Page Inspector スタイル] タブで適用した変更は、元のスタイルシートには影響しません。 スタイルの選択を解除したり、必要な数だけ値を変更したりできますが、ページを更新した後に復元されます。

    ![CSS styles2 を有効または無効にする](using-page-inspector-in-visual-studio-2012/_static/image34.png "CSS スタイルの有効化と無効化")

    *CSS スタイルの有効化と無効化*
13. 次に、検査モードを使用**して、ヘッダーの "your** **logo here"** テキストをクリックします。
14. **[スタイル]** タブで、 **[サイト-タイトル]** グループの下の **[フォントサイズ]** CSS 属性を見つけます。 属性の値を編集するには、属性を1回ダブルクリックします。 2\.3 em 値を**3em**に置き換え、enter キーを押します。 タイトルが大きくなっていることに注意してください。

    ![ページ Inspector2 の CSS 値の変更](using-page-inspector-in-visual-studio-2012/_static/image35.png "Page Inspector での CSS 値の変更")

    *Page Inspector での CSS 値の変更*
15. Page Inspector の右ペインにある **[トレーススタイル]** タブをクリックします。 これは、選択に適用されているすべてのスタイルを属性名順に表示するための別の方法です。

    ![選択された要素の CSS スタイルのトレース](using-page-inspector-in-visual-studio-2012/_static/image36.png "選択された要素の CSS スタイルのトレース")

    *選択された要素の CSS スタイルのトレース*
16. Page Inspector のもう1つの機能は、レイアウトペインです。 検査モードを使用して、ナビゲーションバーを選択し、右側のウィンドウの **[レイアウト]** タブをクリックします。 選択した要素の正確なサイズに加え、オフセット、余白、余白、および境界線のサイズが表示されます。 このビューから値を変更することもできます。

    ![Page Inspector での要素のレイアウト](using-page-inspector-in-visual-studio-2012/_static/image37.png "Page Inspector での要素のレイアウト")

    *Page Inspector での要素のレイアウト*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>タスク 2-フォトギャラリーでのスタイルの問題の検出と修正

以前のバージョンの Visual Studio で Web ページの問題を診断するにはどうすればよいですか。 Internet Explorer 開発者ツールや焼討バグなど、Visual Studio IDE の外部で実行される web デバッグツールに慣れている場合があります。 ブラウザーは HTML、スクリプト、およびスタイルを理解するだけで、基になるフレームワークはレンダリングされる HTML を生成します。 そのため、多くの場合、サイト全体を展開して、web ページの外観を確認する必要があります。

Web サイトの問題を検出して修正する場合は、次の手順に従うことをお勧めします。

1. Visual Studio からソリューションを実行するか、web サーバーにページを配置します。
2. ブラウザーで、使用する開発者ツールを開くか、ソースコードとスタイルを開いて問題を解決します。 関連するファイルを見つけるには、&quot;検索&quot; を使用するか、スタイルクラスの名前を使用してファイル&quot; 機能を検索 &quot;ます。
3. エラーが検出されたら、Web ブラウザーとサーバーを停止します。
4. ブラウザーのキャッシュをクリアします。
5. 修正プログラムを適用するには、Visual Studio に戻ります。 テストするすべての手順を繰り返します。

ASP.NET WebForms に実際の WYSIWYG は存在しないため、いくつかのスタイルの問題は、実行中または配置後に、後の段階で検出されます。 現在、Page Inspector では、ソリューションを実行せずに任意のページをプレビューすることができます。

このタスクでは、Page inspector を使用して、フォトギャラリーアプリケーションのいくつかの問題を修正します。 次の手順では、ヘッダーのいくつかの簡単なスタイルの問題を検出して迅速に修正します。

1. ページ検査を使用して、ヘッダーの左側にある**レジスタ**と**ログイン**リンクを探します。

    右側の適切な場所にリンクが表示されないことに注意してください。 次に、リンクを右揃えにして、それに応じてスタイルを調整します。

    ![左側に配置されているログインリンク](using-page-inspector-in-visual-studio-2012/_static/image38.png "左側に配置されているログインリンク")

    *左側に配置されているログインリンク*
2. トグル検査モードを選択した状態で、[ログイン] リンクを選択してコードを開きます。

    リンクのソースコードは、default.aspx ページではなく、最初に表示される場所である、default.aspx ファイルにあることに注意し**てください。** 正しいソースファイルに直接配置されています。
3. **[スタイル]** タブで、[ **&lt;] セクション**を見つけてクリックします。これは、これらのリンクの HTML コンテナーである #login 項目&gt; ます。

    クリックすると、 **[#login]** スタイルが **[.css]** に自動的に配置されます。 さらに、コードが強調表示されるようになりました。

    ![CSS スタイルの選択](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS スタイルの選択")

    *CSS スタイルの選択*
4. 強調表示されたコード内の**テキストの整列**属性のコメントを解除します。そのためには、開始文字と終了文字を削除して、**サイトの .css**ファイルを保存します。

    Page Inspector は、現在のページを構成するすべての異なるファイルを認識し、これらのファイルのいずれかが変更されたときに検出することができます。 ブラウザーの現在のページがソースファイルと同期されていない場合は、いつでもアラートが生成されます。
5. Page Inspector ブラウザーで、アドレスバーの下にあるバーをクリックして変更を保存し、ページを再度読み込みます。

    ![ページの再読み込み](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *ページの再読み込み*

    リンクは右側に表示されていますが、箇条書きのように見えます。 ここで、箇条書きを削除して、リンクを水平方向に揃えます。

    ![更新されたページ](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *更新されたページ*
6. 検査モードを使用して、&quot;レジスタ&quot; を含む任意の **&lt;li&gt;** 項目を選択し &quot;リンクを&quot; します。 次に、[ **&lt;] セクション&gt; #login**項目をクリックして、**スタイルの .css**コードにアクセスします。

    ![スタイルの検索](using-page-inspector-in-visual-studio-2012/_static/image42.png "スタイルの検索")

    *スタイルの検索*
7. **.Css**で **#login li**項目のコードをコメント解除します。 追加するスタイルによって、行頭文字が非表示になり、項目が横方向に表示されます。

    ![ログインリンクのスタイルを再設定する](using-page-inspector-in-visual-studio-2012/_static/image43.png "ログインリンクのスタイルを再設定する")

    *ログインリンクのスタイルを再設定する*
8. **スタイルの .css**ファイルを保存し、アドレスの下にあるバーで [1 回] をクリックして、ページを再度読み込みます。 リンクが正しく表示されていることを確認します。

    ![右側に合わせたリンク](using-page-inspector-in-visual-studio-2012/_static/image44.png "右側に合わせたリンク")

    *右側に合わせたリンク*
9. 最後に、ヘッダーのタイトルを変更します。 すべてのファイルで ' your**logo here '** テキストを検索するのではなく、検査モードを使用してテキストをクリックし、それを生成するソースコードにアクセスします。

    ![サイトのタイトルの検索](using-page-inspector-in-visual-studio-2012/_static/image45.png "サイトのタイトルの検索")

    *サイトのタイトルの検索*
10. これで、"your**logo here**" というテキストを '**フォトギャラリー**' で置き換えることができ**ます。** Page Inspector ブラウザーを保存して更新します。

    ![フォトギャラリーページが更新されました](using-page-inspector-in-visual-studio-2012/_static/image46.png "フォトギャラリーページが更新されました")

    *フォトギャラリーページが更新されました*
11. 最後に、 **F5**キーを押してアプリを実行し、すべての変更が期待どおりに動作することを確認します。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、ブラウザーで Web サイトをリビルドして実行しなくても、Page Inspector を使用して Web アプリケーションをプレビューする方法を学習しました。 また、レンダリングされた出力からソースコードに直接アクセスして、バグをすばやく見つけて修正する方法を習得しました。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *VS Express for Web タイル*
