---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: ASP.NET AJAX UpdatePanel トリガーについてMicrosoft Docs
author: scottcate
description: Visual Studio のマークアップエディターで作業するときに、UpdatePanel コントロールの2つの子要素があることを (IntelliSense から) 確認できます。 Wh のいずれか
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: b1cc869f373d4f8283b4d92af74707c3f11fef61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440542"
---
# <a name="understanding-aspnet-ajax-updatepanel-triggers"></a>ASP.NET AJAX UpdatePanel トリガーについて理解する

[Scott Cate](https://github.com/scottcate)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Visual Studio のマークアップエディターで作業するときに、UpdatePanel コントロールの2つの子要素があることを (IntelliSense から) 確認できます。 そのうちの1つは、要素が存在する UpdatePanel コントロールの部分的なレンダリングをトリガーする、ページ上のコントロール (または、使用している場合はユーザーコントロール) を指定する Triggers 要素です。

## <a name="introduction"></a>はじめに

Microsoft の ASP.NET テクノロジは、オブジェクト指向プログラミングモデルとイベントドリブンプログラミングモデルを提供し、コンパイル済みコードの利点と結び付けます。 ただし、そのサーバー側の処理モデルには、テクノロジに固有のいくつかの欠点があります。その多くは、Microsoft ASP.NET 3.5 AJAX 拡張機能に含まれる新機能によって対処できます。 これらの拡張機能により、ページの完全な更新を必要としないページの部分的なレンダリング、クライアントスクリプト (ASP.NET プロファイリング API を含む) を使用した Web サービスへのアクセス機能、広範なクライアント側 API など、多くの豊富なクライアント機能が有効になります。ASP.NET のサーバー側コントロールセットで見られる多くのコントロールスキームをミラー化するように設計されています。

このホワイトペーパーでは、ASP.NET AJAX `UpdatePanel` コンポーネントの XML トリガー機能について考察します。 XML トリガーを使用すると、特定の UpdatePanel コントロールに部分的なレンダリングを発生させる可能性のあるコンポーネントを細かく制御できます。

このホワイトペーパーは、.NET Framework 3.5 と Visual Studio 2008 のベータ2リリースに基づいています。 ASP.NET AJAX 拡張機能は、以前は ASP.NET 2.0 を対象としたアドオンアセンブリであり、.NET Framework の基本クラスライブラリに統合されています。 また、このホワイトペーパーでは、visual Web Developer Express ではなく Visual Studio 2008 を使用することを前提としています。また、Visual Studio のユーザーインターフェイスに従ってチュートリアルを提供します (ただし、コード一覧は、次の項目に関係なく完全に互換性があります)。開発環境)。

## <a name="triggers"></a>*トリガー*

既定では、特定の UpdatePanel のトリガーには、ポストバックを呼び出す子コントロールが自動的に含まれます。たとえば、`AutoPostBack` プロパティが**true**に設定されているテキストボックスコントロールなどです。 ただし、トリガーは、マークアップを使用して宣言的に含めることもできます。これは、UpdatePanel コントロール宣言の `<triggers>` セクション内で行います。 トリガーには、`Triggers` コレクションプロパティを使用してアクセスできますが、`Page_Load` イベント内で、ページの ScriptManager オブジェクトの `RegisterAsyncPostBackControl(Control)` メソッドを使用して、実行時に部分的な render トリガーを登録することをお勧めします (たとえば、デザイン時にコントロールを使用できない場合など)。 ページはステートレスであるため、作成するたびにこれらのコントロールを再登録する必要があることに注意してください。

自動子トリガーの追加を無効にすることもできます (したがって、ポストバックを作成する子コントロールは、`ChildrenAsTriggers` プロパティを**false**に設定することによって、部分的なレンダリングを自動的にトリガーしません)。 これにより、ページレンダリングを呼び出すことができる特定のコントロールを柔軟に割り当てることができ、推奨されるので、開発者はイベントに応答して、発生する可能性のあるイベントを処理することはできません。

UpdatePanel コントロールが入れ子になっている場合、UpdateMode が**Conditional**に設定されているときに、子 updatepanel がトリガーされても、親がではない場合は、子 updatepanel だけが更新されることに注意してください。 ただし、親 UpdatePanel が更新されると、子 UpdatePanel も更新されます。

## <a name="the-lttriggersgt-element"></a>*&lt;は&gt; 要素をトリガーします*

Visual Studio のマークアップエディターで作業する場合、`UpdatePanel` コントロールの2つの子要素があることを (IntelliSense から) 確認できます。 最も頻繁に見られる要素は `<ContentTemplate>` 要素です。この要素は、基本的に、更新パネル (部分レンダリングを有効にするコンテンツ) によって保持されるコンテンツをカプセル化します。 もう1つの要素は `<Triggers>` 要素です。この要素は、ページ上のコントロール (使用している場合はユーザーコントロール) を指定します。これにより、&lt;トリガー&gt; 要素が存在する UpdatePanel コントロールの部分的なレンダリングがトリガーされます。

`<Triggers>` 要素には、`<asp:AsyncPostBackTrigger>` と `<asp:PostBackTrigger>`の2つの子ノードのそれぞれに任意の数を含めることができます。 2つの属性、`ControlID` と `EventName`を受け取り、現在のカプセル化の単位内で任意のコントロールを指定できます (たとえば、UpdatePanel コントロールが Web ユーザーコントロール内に存在する場合、ユーザーコントロールが配置されているページのコントロールを参照しないようにする必要があります)。

`<asp:AsyncPostBackTrigger>` 要素は、このトリガーが子である UpdatePanel だけでなく、カプセル化の単位で*任意*の updatepanel コントロールの子として存在するコントロールから任意のイベントを対象とすることができる場合に特に便利です。 したがって、部分ページ更新をトリガーするコントロールを作成できます。

同様に、`<asp:PostBackTrigger>` 要素を使用して部分ページレンダリングをトリガーすることもできますが、その場合はサーバーへの完全なラウンドトリップを必要とします。 また、このトリガー要素を使用して、コントロールが通常は部分ページレンダリングをトリガーする場合に、完全なページレンダリングを強制的に実行することもできます (たとえば、UpdatePanel コントロールの `<ContentTemplate>` 要素に `Button` コントロールが存在する場合)。 ここでも、PostBackTrigger 要素は、カプセル化の現在の単位で、任意の UpdatePanel コントロールの子である任意のコントロールを指定できます。

## <a name="lttriggersgt-element-reference"></a>*&lt;トリガー&gt; 要素参照*

*マークアップの子孫:*

| **Tag** | **説明** |
| --- | --- |
| &lt;asp: AsyncPostBackTrigger&gt; | このトリガー参照を含む UpdatePanel の部分ページ更新を発生させるコントロールとイベントを指定します。 |
| &lt;asp: PostBackTrigger&gt; | ページ全体の更新を発生させるコントロールとイベントを指定します (ページ全体の更新)。 このタグを使用すると、コントロールが部分的なレンダリングをトリガーする場合に、完全な更新を強制的に実行できます。 |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*チュートリアル: UpdatePanel 間トリガー*

1. 部分的なレンダリングを有効にする ScriptManager オブジェクトが設定された新しい ASP.NET ページを作成します。 2つの UpdatePanels をこのページに追加します。1つ目は、ラベルコントロール (Label1) と2つのボタンコントロール (Button1 および Button2) を含めます。 Button1 をクリックして両方を更新する必要があります。これを更新するには、[] をクリックする必要があります。 2番目の UpdatePanel では、ラベルコントロール (Label2) のみを含めますが、その ForeColor プロパティを既定値以外に設定して区別します。
2. 両方の UpdatePanel タグの UpdateMode プロパティを**条件付き**に設定します。

**リスティング 1: default.aspx のマークアップ:** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. Button1 の Click イベントハンドラーで、Label1 と Label2 を任意の時間に依存する (ToLongTimeString () など) に設定します。 Button2 の Click イベントハンドラーについては、Label1 を時間に依存する値に設定します。

**リスト 2: default.aspx.cs の分離コード (トリム):** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. F5 キーを押して、プロジェクトをビルドして実行します。 [両方のパネルを更新] をクリックすると、両方のラベルがテキストを変更することに注意してください。ただし、[このパネルを更新する] をクリックすると、Label1 の更新プログラムのみが表示できます。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png)される)

## <a name="under-the-hood"></a>*内部的な処理*

先ほど作成した例を利用して、ASP.NET AJAX が行っていることと、UpdatePanel のクロスパネルトリガーの動作を確認できます。 これを行うには、生成されたページソース HTML と、消火バグと呼ばれる Mozilla Firefox 拡張機能を使用します。これにより、AJAX ポストバックを簡単に調べることができます。 また、Lutz Roeder によって .NET リフレクターツールを使用します。 これらのツールはいずれもオンラインで利用可能であり、インターネット検索で見つけることができます。

ページソースコードを確認すると、通常はほとんど何も表示されません。UpdatePanel コントロールは `<div>` コンテナーとしてレンダリングされ、`<asp:ScriptManager>`によって提供されるスクリプトリソースを確認できます。 AJAX クライアントスクリプトライブラリの内部にある PageRequestManager への新しい AJAX 固有の呼び出しもあります。 最後に、2つの UpdatePanel コンテナーが表示されます。1つは、`<span>` コンテナーとしてレンダリングされた2つの `<asp:Label>` コントロールを含む `<input>` ボタンを表示します。 (消火バグの DOM ツリーを調べると、ラベルが淡色表示され、表示可能なコンテンツが生成されていないことがわかります)。

[このパネルを更新] ボタンをクリックすると、上部の UpdatePanel が現在のサーバー時刻で更新されることがわかります。 [消火バグ] で、[コンソール] タブを選択して、要求を確認できるようにします。 POST 要求パラメーターを最初に確認します。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png)される)

UpdatePanel は、ScriptManager1 パラメーターを使用して起動されたコントロールツリーを正確にサーバー側の AJAX コードに示しています。これは、`UpdatePanel1` コントロールの `Button1` です。 次に、[両方のパネルを更新する] ボタンをクリックします。 次に、応答を調べると、パイプで区切られた一連の変数が文字列に設定されています。具体的には、上部の UpdatePanel (`UpdatePanel1`) がブラウザーに送信された HTML の全体を表示しています。 AJAX クライアントスクリプトライブラリは、`.innerHTML` プロパティを使用して、UpdatePanel の元の HTML コンテンツを新しいコンテンツに置き換えます。これにより、サーバーは変更されたコンテンツを HTML としてサーバーから送信します。

次に、[両方のパネルを更新] ボタンをクリックし、サーバーの結果を確認します。 結果は非常に似ています。どちらの UpdatePanels でも、サーバーから新しい HTML を受け取ります。 前のコールバックと同様に、追加のページ状態が送信されます。

ご覧のように、AJAX ポストバックの実行には特殊なコードが使用されていないため、AJAX クライアントスクリプトライブラリは、追加のコードを使用せずにフォームポストバックをインターセプトすることができます。 サーバーコントロールは自動的に JavaScript を利用して、自動的にフォームの検証と状態のコードを自動的に送信します。これは、主に自動スクリプトリソースのインクルード、PostBackOptions クラスによって実現されます。、および ClientScriptManager クラス。

たとえば、CheckBox コントロールについて考えてみます.NET リフレクターでクラスの逆アセンブリを確認します。 これを行うには、System.web アセンブリが開いていることを確認し、`RenderInputTag` メソッドを開いて `System.Web.UI.WebControls.CheckBox` クラスに移動します。 `AutoPostBack` プロパティをチェックする条件を探します。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png)される)

`CheckBox` コントロールで自動ポストバックが有効になっている場合 (AutoPostBack プロパティが true の場合)、結果の `<input>` タグは、その `onclick` 属性の ASP.NET イベント処理スクリプトを使用してレンダリングされます。 フォームの送信を傍受すると、ASP.NET AJAX がページ nonintrusively に挿入され、場合によっては不正確な文字列置換を使用することによって発生する可能性のある重大な変更を回避できます。 さらに、これにより、*任意の*カスタム ASP.NET コントロールで、UpdatePanel コンテナー内での使用をサポートするコードを追加しなくても、ASP.NET AJAX の機能を利用できるようになります。

`<triggers>` 機能は \_updateControls への PageRequestManager 呼び出しで初期化される値に対応しています (ASP.NET AJAX クライアントスクリプトライブラリでは、アンダースコアで始まるメソッド、イベント、およびフィールド名が内部としてマークされ、ライブラリ自体の外部で使用するためのものではないという規則が使用されています)。 このメソッドを使用すると、AJAX ポストバックの原因となっているコントロールを調べることができます。

たとえば、2つの追加のコントロールをページに追加し、1つのコントロールを UpdatePanels の外部に残して、UpdatePanel 内に1つ残しておきます。 上部の UpdatePanel 内に CheckBox コントロールを追加し、リスト内で定義されている多数の色を持つ DropDownList をドロップします。 新しいマークアップは次のとおりです。

**リスト 3: 新しいマークアップ**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

新しい分離コードを次に示します。

**リスト 4: 分離コード**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

このページの背後にあるのは、ドロップダウンリストでは、2つ目のラベルを表示するために3色のいずれかを選択し、チェックボックスで太字になっているかどうか、およびラベルに日付と時刻のどちらが表示されているかを確認するということです。 チェックボックスをオンにしても AJAX の更新は行われませんが、UpdatePanel 内に格納されていない場合でも、ドロップダウンリストは必要です。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png)される)

上のスクリーンショットでわかるように、クリックされた最新のボタンは、このパネルを更新する右側のボタンでした。このパネルは、一番下の時間に依存しないように更新します。 日付は一番下のラベルに表示されるため、クリックの間で日付も切り替えられました。 最後に、一番下のラベルの色が表示されます。ラベルのテキストよりも最近更新されました。これは、コントロールの状態が重要であり、ユーザーが AJAX ポストバックによって保存されることを期待していることを示しています。 *ただし*、時刻は更新されませんでした。 この時間は、ASP.NET ランタイムによって解釈されるページの \_\_VIEWSTATE フィールドの永続化を通じて、コントロールがサーバーで再レンダリングされたときに自動的に再設定されます。 ASP.NET AJAX サーバーコードでは、コントロールの状態が変化しているメソッドは認識されません。単にビューステートから再起動し、適切なイベントを実行します。

ただし、これは指摘されるはずですが、ページ\_読み込みイベント内の時間を初期化したので、時間が正しくインクリメントされました。 そのため、開発者は、適切なイベントハンドラーの実行中に適切なコードが実行されていることを慎重に考慮し、コントロールイベントハンドラーが適切な場合にページ\_の読み込みを使用しないようにする必要があります。

## <a name="summary"></a>まとめ

ASP.NET AJAX Extensions UpdatePanel コントロールは汎用性があり、更新を引き起こす可能性のあるコントロールイベントを識別するための多数のメソッドを利用できます。 子コントロールによって自動的に更新されることをサポートしますが、ページ上の他の場所にあるコントロールイベントに応答することもできます。

サーバー処理の負荷の可能性を低減するために、UpdatePanel の `ChildrenAsTriggers` プロパティを `false`に設定し、そのイベントを既定ではなくオプトインするように設定することをお勧めします。 これにより、検証や入力フィールドへの変更など、不要なイベントによって望ましくない可能性のある影響が発生するのを防ぐことができます。 この種のバグは、ページがユーザーに対して透過的に更新されるため、分離するのが困難な場合があります。したがって、原因がすぐに明らかになるとは限りません。

ASP.NET AJAX フォームポストインターセプトモデルの内部動作を調べることで、ASP.NET によって既に提供されているフレームワークを利用していることを確認できました。 これにより、同じフレームワークを使用して設計されたコントロールとの最大の互換性が維持され、ページ用に記述された追加の JavaScript に対して最小限の関与が実現します。

## <a name="bio"></a>略歴

渡 Paveza は、Terralever ([www.terralever.com](http://www.terralever.com)) にあるシニア .net アプリケーション開発者であり、tempe の主要な対話型マーケティング企業です。 AZ. 彼は[robpaveza@gmail.com](mailto:robpaveza@gmail.com)にアクセスできます。彼のブログは[http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/)にあります。

Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。 Scott は、 [scott.cate@myKB.com](mailto:scott.cate@myKB.com)または彼のブログ ( [ScottCate.com](http://ScottCate.com) ) で、電子メールで連絡を受けることができます。

> [!div class="step-by-step"]
> [前へ](understanding-partial-page-updates-with-asp-net-ajax.md)
> [次へ](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
