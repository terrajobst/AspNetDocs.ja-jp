---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: ASP.NET AJAX デバッグ機能についてMicrosoft Docs
author: scottcate
description: コードをデバッグする機能は、使用しているテクノロジに関係なく、すべての開発者がコレクションに必要とするスキルです。 多くの開発者は...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 08ced380f3551407d757524dbc84b5feeeb5482b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510862"
---
# <a name="understanding-aspnet-ajax-debugging-capabilities"></a>ASP.NET AJAX デバッグ機能について理解する

[Scott Cate](https://github.com/scottcate)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> コードをデバッグする機能は、使用しているテクノロジに関係なく、すべての開発者がコレクションに必要とするスキルです。 多くの開発者は、Visual Studio .NET または Web Developer Express を使用して、VB.NET やC#コードを使用する ASP.NET アプリケーションをデバッグすることに慣れていますが、JavaScript などのクライアント側コードをデバッグする場合にも非常に便利であることを認識していません。 .NET アプリケーションのデバッグに使用するのと同じ種類の手法は、AJAX 対応アプリケーションや、より具体的に ASP.NET AJAX アプリケーションにも適用できます。

## <a name="debugging-aspnet-ajax-applications"></a>ASP.NET AJAX アプリケーションのデバッグ

Dan Wahlin

コードをデバッグする機能は、使用しているテクノロジに関係なく、すべての開発者がコレクションに必要とするスキルです。 使用可能なさまざまなデバッグオプションを理解することで、プロジェクトにかなりの時間を節約でき、場合によってはいくつかの悩みもあります。 多くの開発者は、Visual Studio .NET または Web Developer Express を使用して、VB.NET やC#コードを使用する ASP.NET アプリケーションをデバッグすることに慣れていますが、JavaScript などのクライアント側コードをデバッグする場合にも非常に便利であることを認識していません。 .NET アプリケーションのデバッグに使用するのと同じ種類の手法は、AJAX 対応アプリケーションや、より具体的に ASP.NET AJAX アプリケーションにも適用できます。

この記事では、Visual Studio 2008 と他のいくつかのツールを使用して ASP.NET AJAX アプリケーションをデバッグし、バグやその他の問題をすばやく特定する方法を説明します。 ここでは、デバッグのために Internet Explorer 6 以上を有効にする方法について説明します。 Visual Studio 2008 とスクリプトエクスプローラーを使用して、コードをステップ実行したり、Web 開発ヘルパーなどの他のフリーツールを使用したりすることができます。 また、他のツールを使用せずに、ブラウザーで直接 JavaScript コードをステップ実行できるようにする、焼討バグという名前の拡張機能を使用して、Firefox で ASP.NET AJAX アプリケーションをデバッグする方法についても説明します。 最後に、ASP.NET AJAX ライブラリのクラスについて説明します。これは、トレースやコードアサーションステートメントなど、さまざまなデバッグタスクに役立ちます。

Internet Explorer で表示されるページをデバッグする前に、デバッグを有効にするために実行する必要がある基本的な手順がいくつかあります。 開始するために実行する必要がある基本的なセットアップ要件をいくつか見てみましょう。

## <a name="configuring-internet-explorer-for-debugging"></a>デバッグ用の Internet Explorer の構成

ほとんどの人は、Internet Explorer で表示された Web サイトで発生した JavaScript の問題については知りません。 実際、平均的なユーザーは、エラーメッセージが表示された場合に何をするかを知ることはできません。 その結果、ブラウザーではデバッグオプションが既定でオフになります。 ただし、デバッグを有効にし、新しい AJAX アプリケーションを開発するときに使用できるようにするのは非常に簡単です。

デバッグ機能を有効にするには、Internet Explorer メニューの [ツール] [インターネットオプション] にアクセスし、[詳細設定] タブを選択します。[参照] セクションで、次の項目がオフになっていることを確認します。

- スクリプトのデバッグを無効にする (Internet Explorer)
- スクリプトのデバッグを無効にする (その他)

必須ではありませんが、アプリケーションをデバッグする場合は、ページ内の JavaScript エラーをすぐに表示し、明確にすることをお勧めします。 [すべてのスクリプトエラーに関する通知を表示する] チェックボックスをオンにすると、すべてのエラーをメッセージボックスに強制的に表示することができます。 これは、アプリケーションの開発中に有効にするための優れたオプションですが、JavaScript エラーが発生する可能性が非常に高いため、他の Web サイトをつい man している場合は、すぐに面倒になる可能性があります。

図1は、Internet Explorer の [詳細設定] ダイアログがデバッグ用に適切に構成された後にどのように表示されるかを示しています。

[デバッグ用に Internet Explorer を構成する ![ます。](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**図 1**: デバッグ用に Internet Explorer を構成する  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png)される)

デバッグが有効になると、[表示] メニューに [スクリプトデバッガー] という名前の新しいメニュー項目が表示されます。 これには、次のステートメントで開くと中断を含む2つのオプションがあります。 [開く] を選択すると、Visual Studio 2008 でページをデバッグするように求められます (Visual Web Developer Express はデバッグにも使用できることに注意してください)。 Visual Studio .NET が現在実行されている場合は、そのインスタンスを使用するか、新しいインスタンスを作成するかを選択できます。 [次のステートメントで中断] が選択されている場合は、JavaScript コードの実行時にページをデバッグするように求められます。 ページの onLoad イベントで JavaScript コードを実行する場合は、ページを更新してデバッグセッションをトリガーすることができます。 ボタンをクリックした後に JavaScript コードを実行すると、ボタンがクリックされた直後にデバッガーが実行されます。

> [!NOTE]
> ユーザー Access Control (UAC) が有効になっている Windows Vista で実行していて、Visual Studio 2008 が管理者として実行するように設定されている場合、アタッチを求めるメッセージが表示されると、Visual Studio はプロセスにアタッチできません。 この問題を回避するには、まず Visual Studio を起動し、そのインスタンスを使用してデバッグします。

次のセクションでは、Visual Studio 2008 内から直接 ASP.NET AJAX ページをデバッグする方法について説明しますが、Internet Explorer の [スクリプトデバッガー] オプションを使用すると、ページが既に開いていて、より詳細な検査を行う場合に便利です。

## <a name="debugging-with-visual-studio-2008"></a>Visual Studio 2008 を使用したデバッグ

Visual Studio 2008 は、世界中の開発者が .NET アプリケーションのデバッグに日常的に依存しているデバッグ機能を提供します。 組み込みのデバッガーを使用すると、コードをステップ実行したり、オブジェクトデータを表示したり、特定の変数を監視したり、呼び出し履歴を監視したりすることができます。 デバッガーは、VB.NET またはC#コードのデバッグに加えて、ASP.NET AJAX アプリケーションのデバッグにも役立ちます。また、JavaScript コードを1行ずつステップ実行できます。 次の詳細では、Visual Studio 2008 を使用してアプリケーションをデバッグするプロセス全体に discourse を提供するのではなく、クライアント側のスクリプトファイルのデバッグに使用できる手法に焦点を当てています。

Visual Studio 2008 でページをデバッグするプロセスは、いくつかの異なる方法で開始できます。 最初に、前のセクションで説明した Internet Explorer の [スクリプトデバッガー] オプションを使用できます。 これは、ページが既にブラウザーに読み込まれていて、デバッグを開始する場合に適しています。 または、ソリューションエクスプローラーで .aspx ページを右クリックし、メニューから [スタートページとして設定] を選択します。 ASP.NET のページをデバッグすることに慣れている場合は、前に実行したことがあります。 F5 キーを押すと、ページをデバッグできます。 ただし、通常は、VB.NET またはC#コード内の任意の場所にブレークポイントを設定できますが、次に示すように、JavaScript では常にそうであるとは限りません。

*埋め込みスクリプトと外部スクリプト*

Visual Studio 2008 デバッガーは、外部の JavaScript ファイルとは異なるページに埋め込まれた JavaScript を扱います。 外部スクリプトファイルを使用すると、ファイルを開き、選択した任意の行にブレークポイントを設定できます。 ブレークポイントを設定するには、コードエディターウィンドウの左側にある灰色のトレイ領域をクリックします。 `<script>` タグを使用して JavaScript がページに直接埋め込まれている場合は、灰色のトレイ領域をクリックしてブレークポイントを設定してもオプションはありません。 埋め込みスクリプトの行にブレークポイントを設定しようとすると、"これはブレークポイントの有効な場所ではありません" という警告が表示されます。

この問題を回避するには、コードを外部 .js ファイルに移動し、&lt;script&gt; タグの src 属性を使用して参照します。

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

コードを外部ファイルに移動することがオプションではない場合、または必要以上に多くの作業が必要な場合は、どうすればよいでしょうか。 エディターを使用してブレークポイントを設定することはできませんが、デバッガーステートメントを、デバッグを開始するコードに直接追加することはできます。 また、ASP.NET AJAX ライブラリにある Sys. Debug クラスを使用して、強制的にデバッグを開始することもできます。 この記事の後半で、このクラスの詳細について説明します。

`debugger` キーワードの使用例については、「リスト1」を参照してください。 この例では、更新関数の呼び出しが行われる前に、デバッガーを強制的に中断します。

**リスト 1.Debugger キーワードを使用して、Visual Studio .NET デバッガーを強制的に中断します。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

Debugger ステートメントがヒットすると、Visual Studio .NET を使用してページをデバッグするよう求められ、コードのステップ実行を開始できます。 この操作を行っているときに、ページで使用されている ASP.NET AJAX ライブラリスクリプトファイルにアクセスする際に問題が発生することがあります。そのため、Visual Studio の使用について見ていきましょう。NET のスクリプトエクスプローラー。

## <a name="using-visual-studio-net-windows-to-debug"></a>Visual Studio .NET ウィンドウを使用したデバッグ

デバッグセッションが開始され、既定の F11 キーを使用してコードを確認すると、図2のエラーダイアログが表示されることがあります。ただし、ページで使用されているすべてのスクリプトファイルが開いており、デバッグに使用できる場合を除きます。

[デバッグに使用できるソースコードがない場合、![のエラーダイアログが表示されます。](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**図 2**: デバッグに使用できるソースコードがない場合に表示されるエラーダイアログ。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png)される)

このダイアログが表示されるのは、ページによって参照される一部のスクリプトのソースコードへのアクセス方法が Visual Studio .NET によって確認されていないためです。 これは最初は非常に面倒ですが、簡単な修正があります。 デバッグセッションを開始し、ブレークポイントにヒットしたら、Visual Studio 2008 メニューの [Windows スクリプトエクスプローラーのデバッグ] ウィンドウにアクセスするか、Ctrl + Alt + N ホットキーを使用します。

> [!NOTE]
> スクリプトエクスプローラー メニューが表示されない場合は、Visual Studio .NET メニューの **ツール** >  > **コマンド**の**カスタマイズ** にアクセスしてください。 [カテゴリ] セクションで**デバッグ**エントリを見つけてクリックすると、使用可能なすべてのメニューエントリが表示されます。 [コマンド] ボックスの一覧で、[スクリプトエクスプローラー] まで下にスクロールし、先ほど説明した [デバッグ] ウィンドウにドラッグします。 これにより、Visual Studio .NET を実行するたびに [スクリプトエクスプローラー] メニューエントリが使用できるようになります。

スクリプトエクスプローラーを使用すると、ページで使用されているすべてのスクリプトを表示し、コードエディターで開くことができます。 スクリプトエクスプローラーが開いたら、現在デバッグ中の .aspx ページをダブルクリックして、コードエディターウィンドウで開きます。 スクリプトエクスプローラーに表示されている他のすべてのスクリプトに対して同じ操作を実行します。 すべてのスクリプトがコードウィンドウで開かれたら、F11 キーを押し (他のデバッグホットキーを使用)、コードをステップ実行できます。 図3は、スクリプトエクスプローラーの例を示しています。 ここには、デバッグ中の現在のファイル (Demo) と、2つのカスタムスクリプトと、ASP.NET AJAX ScriptManager によってページに動的に挿入された2つのスクリプトが一覧表示されます。

[![スクリプトエクスプローラーを使用すると、ページで使用されるスクリプトに簡単にアクセスできます。](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**図 3**. スクリプトエクスプローラーでは、ページで使用されているスクリプトに簡単にアクセスできます。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png)される)

ページ内のコードをステップ実行するときに役立つ情報を提供するために、他のいくつかのウィンドウを使用することもできます。 たとえば、[ローカル] ウィンドウを使用すると、ページで使用されているさまざまな変数の値を確認できます。また、[イミディエイト] ウィンドウでは、特定の変数または条件を評価し、出力を表示できます。 また、[出力] ウィンドウを使用して、トレースステートメントを表示することもできます。これについては、この記事の後半で説明するように、trace 関数を使用するか、Internet Explorer の Debug. writeln 関数を使用します。

デバッガーを使用してコードをステップ実行するときに、コード内の変数をマウスでポイントすると、割り当てられている値を表示できます。 ただし、スクリプトデバッガーでは、特定の JavaScript 変数にマウスを置いても何も表示されないことがあります。 値を表示するには、コードエディターウィンドウで表示しようとしているステートメントまたは変数を強調表示し、その上にマウスカーソルを合わせます。 この手法はすべての状況で動作するわけではありませんが、多くの場合、[ローカル] ウィンドウなどの別のデバッグウィンドウを参照しなくても値を確認できます。

ここで説明する機能の一部を示すビデオチュートリアルは、 [http://www.xmlforasp.net](http://www.xmlforasp.net)で見ることができます。

## <a name="debugging-with-web-development-helper"></a>Web 開発ヘルパーを使用したデバッグ

Visual Studio 2008 (および Visual Web Developer Express 2008) は、非常に優れたデバッグツールですが、より軽量なオプションを使用することもできます。 リリースされる最新のツールの1つは、Web 開発ヘルパーです。 Microsoft の Nikhil Kothari (Microsoft の主要な ASP.NET AJAX アーキテクト) は、単純なデバッグから HTTP 要求および応答メッセージを表示するためのさまざまなタスクを実行できる優れたツールを作成しました。 Web 開発ヘルパーは[http://projects.nikhilk.net/Projects/WebDevHelper.aspx](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)でダウンロードできます。

Web 開発ヘルパーは、を使用するのに便利な Internet Explorer 内で直接使用できます。 これを開始するには、Internet Explorer メニューから [ツール] [Web 開発ヘルパー] の順に選択します。 これにより、ブラウザーで HTTP 要求および応答メッセージのログ記録などのいくつかのタスクを実行する必要がないため、ブラウザーの下部にツールが表示されます。 図4は、Web 開発ヘルパーが動作中であることを示しています。

[![Web 開発ヘルパー](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**図 4**: Web 開発ヘルパー ([クリックしてフルサイズのイメージを表示する](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))

Web 開発ヘルパーは、Visual Studio 2008 と同様に行ごとにコードをステップ実行するために使用するツールではありません。 ただし、これを使用すると、トレース出力の表示、スクリプト内の変数の簡単な評価、JSON オブジェクト内のデータの探索などを行うことができます。 また、ASP.NET AJAX ページおよびサーバーとの間でやり取りされるデータを表示する場合にも非常に便利です。

Internet Explorer で Web 開発ヘルパーを開いたら、図4の前に示したように、[Web 開発ヘルパー] メニューの [スクリプトを有効にする] を選択して、スクリプトのデバッグを有効にする必要があります。 これにより、ページの実行中に発生したエラーをツールでインターセプトできます。 また、ページに出力されるトレースメッセージに簡単にアクセスすることもできます。 トレース情報を表示したり、ページ内のさまざまな機能をテストするスクリプトコマンドを実行したりするには、[Web 開発ヘルパー] メニューから [スクリプトコンソールを表示] を選択します。 これにより、コマンドウィンドウと単純な [イミディエイト] ウィンドウへのアクセスが可能になります。

*トレースメッセージと JSON オブジェクトデータの表示*

[イミディエイト] ウィンドウを使用すると、スクリプトコマンドを実行したり、ページ内のさまざまな機能をテストするために使用されるスクリプトを読み込んだり保存したりすることもできます。 コマンドウィンドウには、表示されているページによって書き込まれたトレースメッセージまたはデバッグメッセージが表示されます。 リスト2は、Internet Explorer の Debug. writeln 関数を使用してトレースメッセージを書き込む方法を示しています。

**リスト 2.Debug クラスを使用してクライアント側のトレースメッセージを書き込む。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

LastName プロパティに Doe という値が含まれている場合、Web 開発ヘルパーは、スクリプトコンソールのコマンドウィンドウに "Person name: Doe" というメッセージを表示します (デバッグが有効になっていることを前提としています)。 また、Web 開発ヘルパーは、トップレベルの debugService オブジェクトをページに追加して、トレース情報の書き出しや JSON オブジェクトのコンテンツの表示に使用できるページに追加します。 リスト3は、debugService クラスの trace 関数の使用例を示しています。

**リスト 3.Web 開発ヘルパーの debugService クラスを使用してトレースメッセージを書き込みます。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService クラスの優れた機能は、Internet Explorer でデバッグが有効になっていない場合でも機能します。これにより、Web 開発ヘルパーが実行されているときに常にトレースデータにアクセスすることが簡単になります。 ツールがページのデバッグに使用されていない場合、debugService を呼び出すと false が返されるため、トレースステートメントは無視されます。

DebugService クラスでは、Web 開発ヘルパーのインスペクターウィンドウを使用して JSON オブジェクトデータを表示することもできます。 リスト4は、個人データを含む単純な JSON オブジェクトを作成します。 オブジェクトが作成されると、debugService クラスの検査関数が呼び出され、JSON オブジェクトを視覚的に検査できるようになります。

**リスト 4.DebugService. 検査関数を使用した JSON オブジェクトデータの表示。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

ページまたは [イミディエイト] ウィンドウで GetPerson () 関数を呼び出すと、図5に示すように [オブジェクトインスペクター] ダイアログウィンドウが表示されます。 オブジェクト内のプロパティは、それらを強調表示し、[値] テキストボックスに表示されている値を変更し、[更新] リンクをクリックすることで、動的に変更できます。 オブジェクトインスペクターを使用すると、JSON オブジェクトデータを簡単に表示し、プロパティに異なる値を適用して実験できます。

*デバッグエラー*

Web 開発ヘルパーは、トレースデータと JSON オブジェクトを表示できるだけでなく、ページ内のエラーのデバッグにも役立ちます。 エラーが発生した場合は、次のコード行に進むか、スクリプトをデバッグするかを確認するメッセージが表示されます (図6を参照)。 [スクリプトエラー] ダイアログウィンドウには、完全なコールスタックと行番号が表示されます。これにより、スクリプト内の問題を簡単に特定できます。

[JSON オブジェクトを表示するには、[オブジェクトインスペクター] ウィンドウを使用 ![ます。](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**図 5**: [オブジェクトインスペクター] ウィンドウを使用した JSON オブジェクトの表示  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png)される)

[デバッグ] オプションを選択すると、Web 開発ヘルパーの [イミディエイト] ウィンドウでスクリプトステートメントを直接実行して、変数の値を表示したり、JSON オブジェクトを書き出したりすることができます。 エラーをトリガーした同じアクションが再度実行され、コンピューターで Visual Studio 2008 が使用できる場合は、前のセクションで説明したように、コードを1行ずつステップ実行できるように、デバッグセッションを開始するように求められます。

[![Web 開発ヘルパーのスクリプトエラーダイアログ](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**図 6**: Web 開発ヘルパーのスクリプトエラーダイアログ ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png)される)

*要求メッセージと応答メッセージの検査*

ASP.NET AJAX ページのデバッグ中に、ページとサーバーの間で送信される要求メッセージと応答メッセージを確認すると便利な場合がよくあります。 メッセージ内のコンテンツを表示すると、適切なデータが渡されているかどうか、およびメッセージのサイズを確認できます。 Web 開発ヘルパーには、データを未加工のテキストとして、または読みやすい形式で簡単に表示できる優れた HTTP メッセージロガー機能が用意されています。

ASP.NET AJAX の要求メッセージと応答メッセージを表示するには、Web 開発ヘルパーメニューから [http Enable HTTP Logging] を選択して HTTP logger を有効にする必要があります。 有効にすると、現在のページから送信されたすべてのメッセージが HTTP ログビューアーに表示されます。これにアクセスするには、http Show HTTP Logs を選択します。

各要求/応答メッセージで送信された未加工のテキスト (および Web 開発ヘルパーのオプション) を表示すると便利ですが、多くの場合、よりグラフィカルな形式でメッセージデータを表示する方が簡単です。 HTTP ログが有効化され、メッセージがログに記録されたら、HTTP ログビューアーでメッセージをダブルクリックしてメッセージデータを表示できます。 これにより、メッセージに関連付けられているすべてのヘッダーと、実際のメッセージの内容を表示できます。 図7は、[HTTP ログビューアー] ウィンドウで表示される要求メッセージと応答メッセージの例を示しています。

[HTTP ログビューアーを使用して、要求メッセージと応答メッセージデータを表示 ![ます。](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**図 7**: HTTP ログビューアーを使用して、要求メッセージと応答メッセージのデータを表示する  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png)される)

HTTP ログビューアーは、JSON オブジェクトを自動的に解析し、ツリービューを使用して表示します。これにより、オブジェクトのプロパティデータをすばやく簡単に表示できます。 ASP.NET AJAX ページで UpdatePanel が使用されている場合は、図8に示すように、ビューアーによってメッセージの各部分が個別の部分に分割されます。 これは、未加工のメッセージデータを表示する場合と比較して、メッセージの内容をより簡単に確認して理解できる優れた機能です。

[HTTP ログビューアーを使用して表示される UpdatePanel 応答メッセージを ![します。](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**図 8**: HTTP ログビューアーを使用して表示される UpdatePanel 応答メッセージ。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png)される)

Web 開発ヘルパーに加えて、要求メッセージと応答メッセージを表示するために使用できるツールは他にもいくつかあります。 もう1つの良いオプションは、 [http://www.fiddlertool.com](http://www.fiddlertool.com)で無料で利用できる Fiddler です。 Fiddler はここでは説明しませんが、メッセージのヘッダーとデータを十分に検査する必要がある場合にも適しています。

## <a name="debugging-with-firefox-and-firebug"></a>Firefox と消火バグによるデバッグ

Internet Explorer は、広く使用されているブラウザーでもありますが、Firefox などの他のブラウザーは非常に人気があり、多くの場合に使用されています。 その結果、アプリケーションが正しく動作することを確認するために、Firefox および Internet Explorer で ASP.NET AJAX ページを表示してデバッグすることができます。 Firefox は、デバッグのために Visual Studio 2008 に直接結び付けることはできませんが、ページのデバッグに使用できる、消火バグと呼ばれる拡張機能を備えています。 [http://www.getfirebug.com](http://www.getfirebug.com)に移動すると、焼討バグを無料でダウンロードできます。

消火バグは、完全な機能を備えたデバッグ環境を提供します。この環境を使用すると、コードを行ごとにステップ実行したり、ページ内で使用されるすべてのスクリプトにアクセスしたり、DOM 構造を表示したり、CSS スタイルを表示したり、ページで発生するイベントを追跡したりできます。 インストールが完了すると、[ツール]、[ツール]、[アドイン] メニューから [ツール]、[アドイン] の順に選択して、焼討バグにアクセスできます。 Web 開発ヘルパーと同様に、消火バグは、スタンドアロンアプリケーションとしても使用できますが、ブラウザーで直接使用されます。

消火バグが実行されると、スクリプトがページに埋め込まれているかどうかにかかわらず、JavaScript ファイルの任意の行にブレークポイントを設定できます。 ブレークポイントを設定するには、まず Firefox でデバッグする適切なページを読み込みます。 ページが読み込まれたら、[スクリプト] ドロップダウンリストからデバッグするスクリプトを選択します。 ページによって使用されるすべてのスクリプトが表示されます。 ブレークポイントを設定するには、ブレークポイントを設定する行の [消火バグの灰色のトレイ] 領域をクリックします。 Visual Studio 2008 で行うのと同じようにする必要があります。

消火バグにブレークポイントを設定したら、ボタンをクリックしたり、ブラウザーを更新して onLoad イベントをトリガーしたりするなど、デバッグが必要なスクリプトを実行するために必要なアクションを実行できます。 実行は、ブレークポイントを含む行で自動的に停止します。 図9は、消火バグでトリガーされたブレークポイントの例を示しています。

[![、消火バグのブレークポイントを処理します。](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**図 9**: 消火バグのブレークポイントを処理する  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png)される)

ブレークポイントにヒットしたら、矢印ボタンを使用してコードをステップオーバーまたはステップアウトすることができます。 コードをステップ実行すると、スクリプト変数がデバッガーの右側の部分に表示されるため、値を確認したり、オブジェクトにドリルダウンしたりすることができます。 また、消火バグには、デバッグ中の現在の行に到達するスクリプトの実行ステップを表示するための [呼び出し履歴] ドロップダウンリストも含まれています。

また、さまざまなスクリプトステートメントのテスト、変数の評価、およびトレース出力の表示に使用できるコンソールウィンドウも用意されています。 これにアクセスするには、消火バグウィンドウの上部にある [コンソール] タブをクリックします。 [検査] タブをクリックすると、デバッグ中のページを "検査済み" にして DOM の構造と内容を確認することもできます。インスペクターウィンドウに表示されているさまざまな DOM 要素をマウスでポイントすると、ページの適切な部分が強調表示されるため、ページ内で要素がどこで使用されているかを簡単に確認できます。 特定の要素に関連付けられている属性値を "live" に変更して、さまざまな幅やスタイルなどを要素に適用して実験することができます。 これは、ソースコードエディターと Firefox ブラウザーを常に切り替えて、単純な変更がページに与える影響を確認するための便利な機能です。

図10は、DOM inspector を使用して、ページ内で txtCountry という名前のテキストボックスを検索する例を示しています。 また、ページで使用される CSS スタイルや、マウスの動きの追跡、ボタンのクリックなどによって発生するイベントを表示するために、焼討バグインスペクターを使用することもできます。

[![、消火バグの DOM inspector を使用します。](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**図 10**: 消火バグの DOM inspector の使用  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png)される)

消火バグは、Firefox でページを直接デバッグするための軽量な方法と、ページ内のさまざまな要素を検査する優れたツールを提供します。

## <a name="debugging-support-in-aspnet-ajax"></a>ASP.NET AJAX でのデバッグのサポート

ASP.NET AJAX ライブラリには、AJAX 機能を Web ページに追加するプロセスを簡略化するために使用できるさまざまなクラスが含まれています。 これらのクラスを使用して、ページ内の要素を検索し、それらを操作したり、新しいコントロールを追加したり、Web サービスを呼び出したり、イベントを処理したりすることもできます。 ASP.NET AJAX ライブラリには、ページのデバッグプロセスを強化するために使用できるクラスも含まれています。 このセクションでは、Sys. Debug クラスについて紹介し、アプリケーションでの使用方法について説明します。

*Sys. Debug クラスの使用*

Sys. Debug クラス (Sys 名前空間にある JavaScript クラス) を使用すると、トレース出力の書き込み、コードアサーションの実行、コードの強制実行などのさまざまな機能を実行して、デバッグできるようになります。 ASP.NET AJAX ライブラリのデバッグファイル (既定では NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 にインストールされています) で、条件付きテストを実行するために広く使用されています (アサーションと呼びます。これにより、パラメーターが関数に適切に渡されること、オブジェクトには予期されるデータが含まれ、トレースステートメントが記述されます。

Sys. Debug クラスでは、表1に示すように、トレース、コードアサーション、またはエラーを処理するために使用できるいくつかの異なる関数が公開されています。

**表 1.Sys. Debug クラスの関数。**

| **関数名** | **説明** |
| --- | --- |
| assert (condition、message、displayCaller) | Condition パラメーターが true であることをアサートします。 テスト対象の条件が false の場合は、メッセージボックスを使用してメッセージパラメーター値が表示されます。 DisplayCaller パラメーターが true の場合、メソッドは呼び出し元に関する情報も表示します。 |
| clearTrace() | トレース操作から出力するステートメントを消去します。 |
| fail (メッセージ) | プログラムの実行を停止し、デバッガーを中断します。 メッセージパラメーターを使用して、エラーの理由を指定できます。 |
| トレース (message) | メッセージパラメーターをトレース出力に書き込みます。 |
| traceDump(object, name) | オブジェクトのデータを読み取り可能な形式で出力します。 Name パラメーターを使用して、トレースダンプのラベルを指定できます。 ダンプされるオブジェクト内のすべてのサブオブジェクトは、既定で書き出されます。 |

クライアント側のトレースは、ASP.NET で使用できるトレース機能とほぼ同じ方法で使用できます。 これにより、アプリケーションのフローを中断せずに、さまざまなメッセージを簡単に表示できます。 リスト5は、トレースログに書き込むためのトレース関数の使用例を示しています。 この関数は、パラメーターとして書き出す必要があるメッセージを単に受け取ります。

**リスト5。関数を使用します。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

リスト5に示されているコードを実行すると、ページにトレース出力が表示されません。 これを確認する唯一の方法は、Visual Studio .NET、Web 開発ヘルパー、または消火バグで使用できるコンソールウィンドウを使用することです。 ページにトレース出力を表示する場合は、TextArea タグを追加し、次に示すように、その id を TraceConsole に指定する必要があります。

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

ページ内のすべてのトレースステートメントは、TraceConsole TextArea に書き込まれます。

JSON オブジェクト内に含まれるデータを表示する場合は、traceDump クラスの関数を使用できます。 この関数は、トレースコンソールにダンプされるオブジェクトと、トレース出力でオブジェクトを識別するために使用できる名前を含む2つのパラメーターを受け取ります。 リスト6は、traceDump 関数の使用例を示しています。

**リスト6。TraceDump 関数を使用します。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

図11は、traceDump 関数を呼び出したときの出力を示しています。 Person オブジェクトのデータを書き出すだけでなく、アドレスサブオブジェクトのデータも書き込まれることに注意してください。

トレースに加えて、Sys. Debug クラスを使用してコードアサーションを実行することもできます。 アサーションは、アプリケーションの実行中に特定の条件が満たされたことをテストするために使用されます。 ASP.NET AJAX ライブラリスクリプトのデバッグバージョンには、さまざまな条件をテストするための assert ステートメントがいくつか含まれています。

リスト7は、条件をテストするために、assert 関数を使用する例を示しています。 このコードは、Person オブジェクトを更新する前に、アドレスオブジェクトが null かどうかをテストします。

[traceDump 関数の出力を ![します。](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**図 11**: traceDump 関数の出力。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png)される)

**リスト7。デバッグの assert 関数を使用します。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

評価する条件、アサーションが false を返した場合に表示するメッセージ、呼び出し元に関する情報を表示するかどうかなど、3つのパラメーターが渡されます。 アサーションが失敗した場合、3番目のパラメーターが true の場合、メッセージと呼び出し元情報が表示されます。 図12は、一覧7に示されているアサーションが失敗した場合に表示されるエラーダイアログの例を示しています。

カバーする最後の関数は、"Sys. Debug. fail" です。 スクリプト内の特定の行でコードを強制的に失敗させる場合は、JavaScript アプリケーションで通常使用されるデバッガーステートメントではなく、Sys. Debug. fail 呼び出しを追加できます。 次に示すように、失敗の理由を表す1つの文字列パラメーターを指定できます。

[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]

[![のエラーメッセージを表示します。](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**図 12**: "Sys. assert" エラーメッセージ。  ([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png)される)

スクリプトの実行中に、Sys. fail ステートメントが検出されると、Visual Studio 2008 などのデバッグアプリケーションのコンソールに message パラメーターの値が表示され、アプリケーションをデバッグするように求められます。 このことが非常に便利なケースの1つは、インラインスクリプトで Visual Studio 2008 のブレークポイントを設定できないが、変数の値を調べることができるように、コードが特定の行で停止するようにする必要がある場合です。

*ScriptManager コントロールの ScriptMode プロパティについて*

ASP.NET AJAX ライブラリには、既定で C:\Program NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 にインストールされるデバッグスクリプトとリリーススクリプトのバージョンが含まれています。 デバッグスクリプトは、適切に書式設定され、読みやすく、いくつかの Sys. Debug. assert 呼び出しが含まれていますが、リリーススクリプトには空白が除去されていますが、Sys. Debug クラスを使用して全体のサイズを最小限に抑えることができます。

ASP.NET AJAX ページに追加された ScriptManager コントロールは、web.config のコンパイル要素のデバッグ属性を読み取って、読み込むライブラリスクリプトのバージョンを決定します。 ただし、ScriptMode プロパティを変更することによって、デバッグスクリプトまたはリリーススクリプト (ライブラリスクリプトまたはカスタムスクリプト) を読み込むかどうかを制御できます。 ScriptMode では、Auto、Debug、Release、および Inherit を含むメンバーを持つ ScriptMode 列挙型が受け入れられます。

ScriptMode の既定値は Auto です。これは、ScriptManager が web.config の debug 属性をチェックすることを意味します。Debug が false の場合、ScriptManager は ASP.NET AJAX ライブラリスクリプトのリリースバージョンを読み込みます。 Debug が true の場合、スクリプトのデバッグバージョンが読み込まれます。 ScriptMode プロパティを Release または Debug に変更すると、デバッグ属性が web.config に保持している値に関係なく、ScriptManager によって適切なスクリプトが読み込まれます。リスト8は、ScriptManager コントロールを使用して ASP.NET AJAX ライブラリからデバッグスクリプトを読み込む例を示しています。

**リスト8。ScriptManager を使用してデバッグスクリプトを読み込ん**でいます。

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

また、リスト9に示すように、ScriptManager の Scripts プロパティを System.web.ui.scriptreference コンポーネントと共に使用して、独自のカスタムスクリプトの異なるバージョン (デバッグまたはリリース) を読み込むこともできます。

**リスト9。ScriptManager を使用したカスタムスクリプトの読み込み。**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> System.web.ui.scriptreference コンポーネントを使用してカスタムスクリプトを読み込む場合は、スクリプトの下部に次のコードを追加することで、スクリプトの読み込みが完了したことを ScriptManager に通知する必要があります。

[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

リスト9に示されているコードは、スクリプトのデバッグバージョンを検索するよう ScriptManager に指示します。これにより、ユーザーの .js ではなく、自動的にユーザーの node.js が検索されます。 ユーザーのデバッグファイルが見つからない場合は、エラーが発生します。

ScriptManager コントロールに設定されている ScriptMode プロパティの値に基づいてカスタムスクリプトのデバッグバージョンまたはリリースバージョンを読み込む場合は、System.web.ui.scriptreference コントロールの ScriptMode プロパティを Inherit に設定できます。 これにより、「リスト10」に示すように、ScriptManager の ScriptMode プロパティに基づいて、適切なバージョンのカスタムスクリプトが読み込まれます。 ScriptManager コントロールの ScriptMode プロパティは Debug に設定されているため、このページでは、ユーザーのデバッグスクリプトが読み込まれて使用されます。

**リスト10。カスタムスクリプト用に ScriptManager から ScriptMode を継承します。**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

ScriptMode プロパティを適切に使用することで、アプリケーションをより簡単にデバッグし、プロセス全体を簡略化することができます。 デバッグスクリプトがデバッグのために特別にフォーマットされている間は、コードの書式設定が削除されているので、ASP.NET AJAX ライブラリのリリーススクリプトは、ステップ実行や読み取りが困難です。

## <a name="conclusion"></a>まとめ

Microsoft の ASP.NET AJAX テクノロジは、エンドユーザーの全体的なエクスペリエンスを向上させることができる AJAX 対応アプリケーションを構築するための堅固な基盤を提供します。 ただし、プログラミングテクノロジと同様に、バグやその他のアプリケーションの問題は確実に発生します。 使用可能なさまざまなデバッグオプションを把握することで、時間を節約し、より安定した製品にすることができます。

この記事では、Visual Studio 2008、Web 開発ヘルパー、および焼討バグのある Internet Explorer を含む ASP.NET AJAX ページをデバッグするためのいくつかの手法について説明しました。 これらのツールを使用すると、変数データにアクセスしたり、コードを行ごとに表示したり、トレースステートメントを表示したりできるため、全体的なデバッグプロセスを簡略化できます。 説明したさまざまなデバッグツールに加えて、ASP.NET AJAX ライブラリの Sys. Debug クラスをアプリケーションで使用する方法と、ScriptManager クラスを使用してスクリプトのデバッグバージョンまたはリリースバージョンを読み込む方法についても説明しました。

## <a name="bio"></a>略歴

Dan Wahlin (ASP.NET と XML Web サービスの Microsoft の最も重要なプロフェッショナル) は、.NET 開発のインストラクターとアーキテクチャコンサルタントで、インターフェイス技術トレーニング ([www.interfacett.com)](http://www.interfacett.com)を使用しています。 XML for ASP.NET 開発者向け Web サイト ([www.XMLforASP.NET](http://www.XMLforASP.NET)) を設立した Dan は、Ineta スピーカー局にあり、複数のカンファレンスで講演を行っています。 Dan 共同で作成された Professional Windows DNA (Wrox)、ASP.NET: ヒント、チュートリアルとコード (Sams)、ASP.NET 1.1 Insider ソリューション、Professional ASP.NET 2.0 AJAX (Wrox)、ASP.NET 2.0 MVP ハッキング、および ASP.NET 開発者向け XML の作成 (Sams)。 コード、記事、または書籍を書いていない人は、音楽を書いて録音し、妻や子供と共にゴルフやバスケットボールを楽しんでいます。

Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。 Scott は、 [scott.cate@myKB.com](mailto:scott.cate@myKB.com)または彼のブログ ( [ScottCate.com](http://ScottCate.com) ) で、電子メールで連絡を受けることができます。

> [!div class="step-by-step"]
> [[戻る]](understanding-asp-net-ajax-web-services.md)
