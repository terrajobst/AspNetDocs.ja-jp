---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: ASP.NET AJAX を使用した部分ページの更新について |Microsoft Docs
author: scottcate
description: ASP.NET AJAX 拡張機能の中で最も見やすくなっているのは、完全なポストバックを行わずに、部分ページ更新または増分ページ更新を行う機能です。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4b87cb8f58dbd7f27b16bcb0d488ff361770d4fe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622952"
---
# <a name="understanding-partial-page-updates-with-aspnet-ajax"></a>ASP.NET AJAX の部分ページ更新について理解する

[Scott Cate](https://github.com/scottcate)

[PDF のダウンロード](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> ASP.NET AJAX 拡張機能の中で最も見やすくなっているのは、サーバーへの完全なポストバックを実行することなく、部分的または増分ページの更新を行う機能です。コードを変更したり、マークアップの変更を最小限に抑えたりすることはできません。 さまざまな利点があります。つまり、マルチメディア (Adobe Flash や Windows Media など) の状態は変化せず、帯域幅のコストが削減され、クライアントは通常、ポストバックに関連するちらつきを発生させません。

## <a name="introduction"></a>はじめに

Microsoft の ASP.NET テクノロジは、オブジェクト指向プログラミングモデルとイベントドリブンプログラミングモデルを提供し、コンパイル済みコードの利点と結び付けます。 ただし、そのサーバー側の処理モデルには、テクノロジに固有のいくつかの欠点があります。

- ページの更新には、ページの更新が必要なサーバーへのラウンドトリップが必要です。
- ラウンドトリップは、Javascript またはその他のクライアント側テクノロジ (Adobe Flash など) によって生成された効果を保持しません。
- ポストバック中、Microsoft Internet Explorer 以外のブラウザーでは、スクロール位置の自動復元はサポートされていません。 また、Internet Explorer でも、ページが更新されてもちらつきが発生します。
- 特に GridView コントロールやリピータなどのコントロールを扱う場合は、\_\_VIEWSTATE フォームフィールドのサイズが大きくなる可能性があるため、ポストバックには大量の帯域幅が必要になることがあります。
- JavaScript またはその他のクライアント側テクノロジを使用して Web サービスにアクセスするための統合モデルはありません。

Microsoft の ASP.NET AJAX extensions を入力します。 AJAX**は、Nd** **X** ML を同期している**ことを意味**します。これは、クロスプラットフォーム JavaScript を使用したインクリメンタルページ更新を提供するための統合フレームワークであり、microsoft ajax framework を構成するサーバー側コードと、microsoft ajax スクリプトライブラリと呼ばれるスクリプトコンポーネントで構成されます。 また、ASP.NET AJAX 拡張機能は、JavaScript を介して ASP.NET Web サービスにアクセスするためのクロスプラットフォームサポートも提供します。

このホワイトペーパーでは、ASP.NET AJAX Extensions の部分ページ更新機能について説明します。これには、ScriptManager コンポーネント、UpdatePanel コントロール、および UpdateProgress コントロールが含まれています。過大.

このホワイトペーパーは、Visual Studio 2008 のベータ2リリースと .NET Framework 3.5 に基づいています。これにより、ASP.NET AJAX 拡張機能が基本クラスライブラリ (以前は ASP.NET 2.0 で使用可能なアドオンコンポーネント) に統合されます。 また、このホワイトペーパーでは、visual Web Developer Express Edition ではなく、Visual Studio 2008 を使用していることを前提としています。参照されている一部のプロジェクトテンプレートは、Visual Web Developer Express ユーザーが使用できない場合があります。

## <a name="partial-page-updates"></a>部分ページ更新

ASP.NET AJAX 拡張機能の中で最も見やすくなっているのは、サーバーへの完全なポストバックを実行することなく、部分的または増分ページの更新を行う機能です。コードを変更したり、マークアップの変更を最小限に抑えたりすることはできません。 さまざまな利点があります。つまり、マルチメディア (Adobe Flash や Windows Media など) の状態は変化せず、帯域幅のコストが削減され、クライアントは通常、ポストバックに関連するちらつきを発生させません。

部分ページレンダリングを統合する機能は、プロジェクトへの変更を最小限に抑えて ASP.NET に統合されています。

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>チュートリアル: 部分レンダリングを既存のプロジェクトに統合する

1. Microsoft Visual Studio 2008 で、新しい ASP.NET Web サイトプロジェクトを作成します。そのためには、[<em>ファイル</em><em>-&gt; 新しい</em><em>-&gt; Web サイト</em>] に移動し、ダイアログボックスの [ASP.NET web site] を選択します。 任意の名前を付けることができ、ファイルシステムまたはインターネットインフォメーションサービス (IIS) にインストールすることができます。
2. ASP.NET の基本的なマークアップ (サーバー側フォームと `@Page` ディレクティブ) を含む空の既定のページが表示されます。 `Label1` という名前のラベルと、フォーム要素内のページに `Button1` というボタンをドロップします。 テキストプロパティを任意のものに設定できます。
3. デザインビューで、[`Button1`] をダブルクリックして、分離コードイベントハンドラーを生成します。 このイベントハンドラー内で `Label1.Text` を設定して、ボタンをクリックします。 を確認しています。

**リスト 1: 部分レンダリングが有効になる前の default.aspx のマークアップ**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**リスト 2: default.aspx.cs の分離コード (トリム)**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. F5 キーを押して、web サイトを起動します。 Visual Studio では、デバッグを有効にするために web.config ファイルを追加するように求められます。これを行います。 このボタンをクリックすると、ページが更新され、ラベル内のテキストが変更されます。ページが再描画されると、簡単なちらつきが発生します。
2. ブラウザーウィンドウを閉じた後、Visual Studio に戻り、マークアップページに戻ります。 Visual Studio の [ツールボックス] を下にスクロールし、[AJAX 拡張] というラベルの付いたタブを見つけます。 (以前のバージョンの AJAX またはアトラス拡張機能を使用しているためにこのタブが表示されない場合は、このホワイトペーパーの後半にある AJAX 拡張ツールボックスの項目の登録に関するチュートリアルを参照するか、Windows インストーラーダウンロード可能な最新バージョンをインストールしてください。web サイトから)。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

([クリックすると、フルサイズの画像が表示](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png)される)

1. <em>既知の問題:</em>ASP.NET 2.0 AJAX 拡張機能を使用して visual Studio 2005 が既にインストールされているコンピューターに Visual Studio 2008 をインストールすると、Visual Studio 2008 によって AJAX 拡張ツールボックス項目がインポートされます。 コンポーネントのツールヒントを調べることで、これが該当するかどうかを判断できます。これはバージョン3.5.0.0 と言う必要があります。 これらがバージョン2.0.0.0 の場合は、以前のツールボックスアイテムをインポートしたので、Visual Studio の [ツールボックスアイテムの選択] ダイアログボックスを使用して手動でインポートする必要があります。 デザイナーを使用してバージョン2のコントロールを追加することはできません。

2. `<asp:Label>` タグを開始する前に、空白行を作成し、ツールボックスの UpdatePanel コントロールをダブルクリックします。 新しい `@Register` ディレクティブがページの先頭に追加されていることに注意してください。これは、`asp:` プレフィックスを使用して、System.web 名前空間内のコントロールをインポートする必要があることを示しています。
3. 閉じる `</asp:UpdatePanel>` タグをボタン要素の末尾の後ろにドラッグして、要素が、ラップされたラベルとボタンコントロールを持つ適切な形式になるようにします。
4. `<asp:UpdatePanel>` タグを開いた後、新しいタグを開き始めます。 IntelliSense では2つのオプションが表示されることに注意してください。 この場合は、`<ContentTemplate>` タグを作成します。 マークアップが整形式になるように、ラベルとボタンの周りにこのタグをラップしてください。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

([クリックすると、フルサイズの画像が表示](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png)される)

1. `<form>` 要素内の任意の場所で、[ツールボックス] の `ScriptManager` 項目をダブルクリックして ScriptManager コントロールを含めます。
2. 属性 `EnablePartialRendering= true`を含むように `<asp:ScriptManager>` タグを編集します。

**リスト 3: 部分的なレンダリングが有効になっている default.aspx のマークアップ**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. Web.config ファイルを開きます。 Visual Studio によって、Web.config にコンパイル参照が自動的に追加されていることに注意してください。

1. Visual Studio 2008 の新機能: ASP.NET Web サイトプロジェクトテンプレートに付属する web.config には、ASP.NET AJAX 拡張機能に必要なすべての参照が含まれています。また、次のような構成情報のコメント付きセクションも含まれています。追加機能を有効にするためのコメントを解除します。 ASP.NET 2.0 AJAX 拡張機能がインストールされている場合、Visual Studio 2005 には同様のテンプレートがありました。 ただし、Visual Studio 2008 では、AJAX 拡張は既定でオプトアウトされます (つまり、既定で参照されますが、参照として削除できます)。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

([クリックすると、フルサイズの画像が表示](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png)される)

1. F5 キーを押して、web サイトを起動します。 部分表示のみのマークアップをサポートするためにソースコードの変更が必要ないことに注意してください。

Web サイトを起動すると、部分的なレンダリングが有効になっていることがわかります。ボタンをクリックしたときにちらつきが発生せず、ページのスクロール位置が変更されないためです (この例では説明しません)。 ボタンをクリックした後にページの表示されたソースを確認すると、実際にポストバックが発生していないことが確認されます。元のラベルテキストはまだソースマークアップの一部であり、そのラベルは JavaScript によって変更されています。

Visual Studio 2008 には、ASP.NET AJAX 対応 web サイト用に事前定義されたテンプレートが付属していません。 ただし、Visual Studio 2005 と ASP.NET 2.0 AJAX 拡張機能がインストールされている場合、このようなテンプレートは Visual Studio 2005 内で使用できました。 その結果、テンプレートには完全に構成された web.config ファイルが含まれている必要があるため、web サイトの構成と AJAX 対応 Web サイトテンプレートを使用する方がさらに簡単になります (Web サービスアクセスを含むすべての ASP.NET AJAX 拡張機能をサポートします)。と JSON のシリアル化-JavaScript Object Notation) には、既定でメインの Web フォームページ内に UpdatePanel と System.windows.controls.contentcontrol.contenttemplate が含まれています。 この既定のページで部分的なレンダリングを有効にすることは、このチュートリアルの手順10を再度実行し、コントロールをページにドロップするのと同じように簡単です。

## <a name="the-scriptmanager-control"></a>ScriptManager コントロール

## <a name="scriptmanager-control-reference"></a>ScriptManager コントロールリファレンス

マークアップが有効なプロパティ:

| **プロパティ名** | **Type** | **説明** |
| --- | --- | --- |
| AllowCustomErrors-リダイレクト | Bool | エラーを処理するために web.config ファイルのカスタムエラーセクションを使用するかどうかを指定します。 |
| AsyncPostBackError-メッセージ | 文字列型 | エラーが発生した場合にクライアントに送信されるエラーメッセージを取得または設定します。 |
| AsyncPostBack バック-タイムアウト | Int32 | クライアントが非同期要求の完了を待機する既定の時間を取得または設定します。 |
| EnableScript-グローバリゼーション | Bool | スクリプトのグローバリゼーションを有効にするかどうかを取得または設定します。 |
| EnableScript-ローカリゼーション | Bool | スクリプトのローカライズが有効かどうかを取得します。値の設定も可能です。 |
| ScriptLoadTimeout | Int32 | クライアントへのスクリプトの読み込みに許容される秒数を指定します |
| ScriptMode | Enum (Auto、Debug、Release、Inherit) | スクリプトのリリースバージョンを表示するかどうかを取得または設定します。 |
| ScriptPath | 文字列型 | クライアントに送信されるスクリプトファイルの場所へのルートパスを取得または設定します。 |

コードのみのプロパティ:

| **プロパティ名** | **Type** | **説明** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-マネージャー | クライアントに送信される ASP.NET Authentication Service プロキシに関する詳細を取得します。 |
| Isデバッグが有効 | Bool | スクリプトとコードのデバッグが有効かどうかを取得します。 |
| IsInAsyncPostback | Bool | ページが現在非同期ポストバック要求であるかどうかを取得します。 |
| ProfileService | ProfileService-マネージャー | クライアントに送信される ASP.NET プロファイリングサービスプロキシに関する詳細を取得します。 |
| スクリプト | コレクション&lt;スクリプト-リファレンス&gt; | クライアントに送信されるスクリプト参照のコレクションを取得します。 |
| Services | コレクション&lt;サービス-参照&gt; | クライアントに送信される Web サービスプロキシ参照のコレクションを取得します。 |
| SupportsPartialRendering | Bool | 現在のクライアントが部分的なレンダリングをサポートするかどうかを取得します。 このプロパティが**false**を返す場合、すべてのページ要求は標準ポストバックになります。 |

パブリックコードメソッド:

| **メソッド名** | **Type** | **説明** |
| --- | --- | --- |
| SetFocus (string) | Void | 要求が完了したときに、クライアントのフォーカスを特定のコントロールに設定します。 |

マークアップの子孫:

| **番号** | **説明** |
| --- | --- |
| &lt;AuthenticationService&gt; | ASP.NET 認証サービスに対するプロキシの詳細を提供します。 |
| &lt;ProfileService&gt; | ASP.NET プロファイリングサービスに対するプロキシの詳細を提供します。 |
| &lt;スクリプト&gt; | 追加のスクリプト参照を提供します。 |
| &lt;asp: System.web.ui.scriptreference&gt; | 特定のスクリプト参照を表します。 |
| &lt;サービス&gt; | プロキシクラスを生成する追加の Web サービス参照を提供します。 |
| &lt;asp: ServiceReference&gt; | 特定の Web サービス参照を表します。 |

ScriptManager コントロールは、ASP.NET AJAX 拡張に不可欠なコアです。 これにより、スクリプトライブラリ (広範なクライアント側のスクリプト型システムを含む) へのアクセスが可能になり、部分的なレンダリングがサポートされます。また、追加の ASP.NET サービス (認証やプロファイルなど、その他の Web サービス) も幅広くサポートされています。 ScriptManager コントロールでは、クライアントスクリプトのグローバリゼーションおよびローカリゼーションもサポートされています。

## <a name="providing-alternative-and-supplemental-scripts"></a>代替スクリプトと補足スクリプトの提供

Microsoft ASP.NET 2.0 AJAX 拡張機能には、参照されたアセンブリに埋め込まれたリソースとして、デバッグエディションとリリースエディションの両方でスクリプトコード全体が含まれますが、開発者は、ScriptManager コントロールをカスタマイズされたスクリプトファイルにリダイレクトし、登録することが可能です。その他の必要なスクリプト。

通常含まれているスクリプト (WebForms 名前空間とカスタム型システムをサポートするスクリプトなど) の既定のバインディングをオーバーライドするには、ScriptManager クラスの `ResolveScriptReference` イベントに登録します。 このメソッドが呼び出されると、イベントハンドラーは、問題のスクリプトファイルへのパスを変更できるようになります。スクリプトマネージャーは、スクリプトの別のコピーまたはカスタマイズされたコピーをクライアントに送信します。

また、スクリプト参照 (`ScriptReference` クラスによって表されます) は、プログラムまたはマークアップを使用して含めることができます。 これを行うには、プログラムを使用して `ScriptManager.Scripts` コレクションを変更するか、ScriptManager コントロールの第1レベルの子である `<Scripts>` タグの下に `<asp:ScriptReference>` タグを追加します。

## <a name="custom-error-handling-for-updatepanels"></a>UpdatePanels のカスタムエラー処理

更新は UpdatePanel コントロールによって指定されたトリガーによって処理されますが、エラー処理とカスタムエラーメッセージのサポートは、ページの ScriptManager コントロールインスタンスによって処理されます。 これを行うには、`AsyncPostBackError`のイベントをページに公開します。これにより、カスタム例外処理ロジックを提供できます。

AsyncPostBackError イベントを使用すると、`AsyncPostBackErrorMessage` プロパティを指定できます。これにより、コールバックの完了時に警告ボックスが生成されます。

既定のアラートボックスを使用する代わりに、クライアント側のカスタマイズも可能です。たとえば、既定のブラウザーモーダルダイアログではなく、カスタマイズされた `<div>` 要素を表示することができます。 この場合は、クライアントスクリプトでエラーを処理できます。

**リスト 5: カスタムエラーを表示するクライアント側スクリプト**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

簡単に言うと、上記のスクリプトでは、非同期要求が完了したときのクライアント側の AJAX ランタイムにコールバックを登録します。 次に、エラーが報告されたかどうかを確認し、エラーが発生した場合はその詳細を処理します。最後に、エラーがカスタムスクリプトで処理されたことをランタイムに示します。

## <a name="globalization-and-localization-support"></a>グローバリゼーションとローカリゼーションのサポート

ScriptManager コントロールは、スクリプト文字列とユーザーインターフェイスコンポーネントのローカライズを幅広くサポートしています。ただし、このトピックはこのホワイトペーパーの範囲外です。 詳細については、ASP.NET AJAX Extensions でのグローバリゼーションのサポートに関するホワイトペーパーを参照してください。

## <a name="the-updatepanel-control"></a>UpdatePanel コントロール

## <a name="updatepanel-control-reference"></a>UpdatePanel コントロールリファレンス

マークアップが有効なプロパティ:

| **プロパティ名** | **Type** | **説明** |
| --- | --- | --- |
| ChildrenAsTriggers | ブール | ポストバック時に、子コントロールが自動的に更新を呼び出すかどうかを指定します。 |
| RenderMode | enum (Block、Inline) | コンテンツを視覚的に表示する方法を指定します。 |
| UpdateMode | enum (常に、条件付き) | UpdatePanel が部分的なレンダリング中に常に更新されるか、またはトリガーにヒットしたときにのみ更新されるかを指定します。 |

コードのみのプロパティ:

| **プロパティ名** | **Type** | **説明** |
| --- | --- | --- |
| IsInPartialRendering | ブール | UpdatePanel が現在の要求に対する部分的なレンダリングをサポートしているかどうかを取得します。 |
| System.windows.controls.contentcontrol.contenttemplate | ITemplate | 更新要求のマークアップテンプレートを取得します。 |
| ContentTemplateContainer | Control | 更新要求のプログラムテンプレートを取得します。 |
| トリガー | UpdatePanel-TriggerCollection | 現在の UpdatePanel に関連付けられているトリガーの一覧を取得します。 |

パブリックコードメソッド:

| **メソッド名** | **Type** | **説明** |
| --- | --- | --- |
| Update () | Void | 指定した UpdatePanel をプログラムによって更新します。 サーバー要求が、トリガーされていない UpdatePanel の部分的なレンダリングをトリガーできるようにします。 |

マークアップの子孫:

| **番号** | **説明** |
| --- | --- |
| &lt;System.windows.controls.contentcontrol.contenttemplate&gt; | 部分的なレンダリングの結果を表示するために使用するマークアップを指定します。 &lt;asp: UpdatePanel&gt;の子。 |
| &lt;トリガー&gt; | この UpdatePanel の更新に関連付けられた*n 個*のコントロールのコレクションを指定します。 &lt;asp: UpdatePanel&gt;の子。 |
| &lt;asp: AsyncPostBackTrigger&gt; | 指定された UpdatePanel の部分ページレンダリングを呼び出すトリガーを指定します。 これは、対象となる UpdatePanel の子孫として、コントロールである場合とない場合があります。 イベント名を詳細に指定します。&lt;の子は&gt;トリガーします。 |
| &lt;asp: PostBackTrigger&gt; | ページ全体を更新するコントロールを指定します。 これは、対象となる UpdatePanel の子孫として、コントロールである場合とない場合があります。 詳細をオブジェクトに細分化します。 &lt;の子は&gt;トリガーします。 |

`UpdatePanel` コントロールは、AJAX 拡張機能の部分的なレンダリング機能の一部となるサーバー側のコンテンツを区切るコントロールです。 ページに配置できる UpdatePanel コントロールの数に制限はなく、入れ子にすることもできます。 各 UpdatePanel は分離されているので、それぞれが独立して動作できます (2 つの UpdatePanels を同時に実行し、ページのポストバックに依存せずにページの異なる部分をレンダリングできます)。

UpdatePanel コントロールは、主にコントロールトリガーを処理します。既定では、ポストバックを作成する UpdatePanel の `ContentTemplate` 内に含まれるコントロールは、UpdatePanel のトリガーとして登録されます。 つまり、UpdatePanel は、既定のデータバインドコントロール (GridView など) とユーザーコントロールを使用して操作でき、スクリプトでプログラミングできます。

既定では、部分ページレンダリングがトリガーされると、UpdatePanel がそのようなアクションに対して定義されたトリガーをコントロールするかどうかにかかわらず、ページ上のすべての UpdatePanel コントロールが更新されます。 たとえば、1つの UpdatePanel がボタンコントロールを定義し、そのボタンコントロールがクリックされた場合、そのページのすべての UpdatePanel コントロールが既定で更新されます。 これは、既定では、UpdatePanel の `UpdateMode` プロパティが `Always`に設定されているためです。 または、UpdateMode プロパティを `Conditional`に設定します。これは、特定のトリガーがヒットした場合にのみ、UpdatePanel が更新されることを意味します。

## <a name="custom-control-notes"></a>カスタムコントロールのメモ

UpdatePanel は、任意のユーザーコントロールまたはカスタムコントロールに追加できます。ただし、これらのコントロールが含まれているページには、EnablePartialRendering プロパティが**true**に設定されている ScriptManager コントロールも含まれている必要があります。

Web カスタムコントロールを使用するときにこのことを考慮する方法の1つとして、`CompositeControl` クラスの protected `CreateChildControls()` メソッドをオーバーライドする方法があります。 このようにすることで、ページで部分的なレンダリングがサポートされていると判断した場合に、コントロールの子と外部との間に UpdatePanel を挿入できます。それ以外の場合は、単に子コントロールをコンテナー `Control` インスタンスにレイヤー化できます。

## <a name="updatepanel-considerations"></a>UpdatePanel に関する考慮事項

UpdatePanel は、JavaScript XMLHttpRequest のコンテキスト内で ASP.NET ポストバックをラップする、ブラックボックスのように動作します。 ただし、動作と速度の両方において、パフォーマンスに関して大きな考慮事項があります。 UpdatePanel がどのように機能するかを理解するために、使用方法が適切であることを判断するために、AJAX の交換を調べる必要があります。 次の例では、既存のサイトと Mozilla Firefox を使用して、焼討バグ拡張機能を使用します (焼討バグは XMLHttpRequest データをキャプチャします)。

特に、フォームまたはコントロールの市区町村と都道府県フィールドに入力する郵便番号のテキストボックスを持つフォームがあるとします。 このフォームは最終的に、ユーザーの名前、住所、連絡先情報などのメンバーシップ情報を収集します。 特定のプロジェクトの要件に基づいて、さまざまな設計上の考慮事項を考慮する必要があります。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

([クリックすると、フルサイズの画像が表示](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png)される)

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

([クリックすると、フルサイズの画像が表示](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png)される)

このアプリケーションの最初のイテレーションでは、郵便番号、市区町村、都道府県など、ユーザー登録データ全体を組み込んだコントロールが作成されています。 コントロール全体が UpdatePanel 内でラップされ、Web フォームにドロップされました。 ユーザーが郵便番号を入力すると、UpdatePanel は、トリガーを指定するか、または true に設定された ChildrenAsTriggers プロパティを使用して、イベント (バックエンドの対応する TextChanged イベント) を検出します。 AJAX では、消火バグによってキャプチャされた、UpdatePanel 内のすべてのフィールドがポストされます (右側の図を参照してください)。

画面のキャプチャによって、UpdatePanel 内のすべてのコントロールからの値 (この場合はすべて空) と ViewState フィールドが配信されます。 この特定の要求を行うために必要なのは5バイトのデータのみである場合、9 kb を超えるデータが送信されます。 応答はさらに肥大化しています。つまり、57kb がクライアントに送信され、テキストフィールドとドロップダウンフィールドが更新されます。

また、ASP.NET AJAX がプレゼンテーションを更新する方法を確認することが重要な場合もあります。 UpdatePanel の更新要求の応答部分は、左側の 消火バグコンソールの表示に表示されます。これは、クライアントスクリプトによって分割され、ページ上で再構築される、特殊な形式のパイプで区切られた文字列です。 具体的には、ASP.NET AJAX は、UpdatePanel を表すクライアント上の HTML 要素の*innerHTML*プロパティを設定します。 ブラウザーによって DOM が再生成されると、処理する必要がある情報の量によって若干の遅延が発生します。

DOM の再生成により、いくつかの追加の問題が発生します。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

([クリックすると、フルサイズの画像が表示](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png)される)

- フォーカスされた HTML 要素が UpdatePanel 内にある場合、フォーカスは失われます。 そのため、Tab キーを押して郵便番号のテキストボックスを終了したユーザーについては、次の宛先は [City] テキストボックスになります。 ただし、UpdatePanel によって表示が更新されると、フォームにフォーカスがなくなり、Tab キーを押すとフォーカス要素 (リンクなど) の強調表示が開始されます。
- DOM 要素にアクセスする任意の種類のカスタムクライアント側スクリプトが使用されている場合、関数によって永続化された参照は、部分ポストバック後に機能しなくなる可能性があります。

UpdatePanels は、すべてをキャッチすることを目的としたものではありません。 むしろ、プロトタイプや小さなコントロールの更新など、特定の状況に対応した簡単なソリューションを提供し、.NET オブジェクトモデルについては理解しているが DOM を使用している ASP.NET 開発者向けの使い慣れたインターフェイスを提供します。 アプリケーションのシナリオによっては、パフォーマンスを向上させるための代替手段がいくつかあります。

- PageMethods と JSON (JavaScript Object Notation) を使用することを検討してください。開発者は、web サービス呼び出しが呼び出されているかのように、ページで静的メソッドを呼び出すことができます。 メソッドは静的であるため、状態は不要です。スクリプトの呼び出し元がパラメーターを指定すると、結果は非同期的に返されます。
- 1つのコントロールをアプリケーション全体で複数の場所で使用する必要がある場合は、Web サービスと JSON の使用を検討してください。 この場合も、特別な作業はほとんど必要ありません。非同期で動作します。

Web サービスまたはページのメソッドを使用した機能の組み込みも、欠点があります。 まず、ASP.NET の開発者は、通常、機能の小さなコンポーネントをユーザーコントロール (.ascx ファイル) にビルドする傾向があります。 ページメソッドをこれらのファイルでホストすることはできません。これらは、実際の .aspx ページクラス内でホストされている必要があります。 Web サービスも同様に、.asmx クラス内でホストする必要があります。 アプリケーションによっては、このアーキテクチャが単一責任の原則に違反することがあります。これは、1つのコンポーネントの機能が2つ以上の物理コンポーネントに分散されるようになったためです。

最後に、アプリケーションで UpdatePanels を使用する必要がある場合は、次のガイドラインを参考にしてトラブルシューティングとメンテナンスを行う必要があります。

- **UpdatePanels をできるだけ少ない数で入れ子にするだけでなく、コードの単位間で入れ子にすることもできます。** たとえば、コントロールをラップするページに UpdatePanel を使用し、そのコントロールには、updatepanel を含む別のコントロールを含む UpdatePanel も含まれているのに対して、単位の入れ子があります。 これにより、更新する必要がある要素を明確にし、子アップデートパネルへの予期しない更新を防ぐことができます。
- ***ChildrenAsTriggers*プロパティを false に設定したままにして、トリガーイベントを明示的に設定します。** `<Triggers>` コレクションを使用すると、イベントを処理しやすくなり、予期しない動作を防ぐことができます。これは、メンテナンスタスクを支援し、開発者がイベントをオプトインするように強制するためです。
- **機能を実現するには、可能な限り最小単位を使用します。** 郵便番号サービスの説明に記載されているように、サーバーへの時間を短縮するだけで、処理の合計と、クライアント/サーバー間の exchange のフットプリントをラップすることで、パフォーマンスを向上させることができます。

## <a name="the-updateprogress-control"></a>UpdateProgress コントロール

## <a name="updateprogress-control-reference"></a>UpdateProgress コントロールリファレンス

マークアップが有効なプロパティ:

| **プロパティ名** | **Type** | **説明** |
| --- | --- | --- |
| AssociatedUpdate-Pan d | 文字列型 | この UpdateProgress が報告する必要がある UpdatePanel の ID を指定します。 |
| DisplayAfter | Int | 非同期要求の開始後にこのコントロールが表示されるまでのタイムアウトをミリ秒単位で指定します。 |
| DynamicLayout | ブール | 進行状況を動的に表示するかどうかを指定します。 |

マークアップの子孫:

| **番号** | **説明** |
| --- | --- |
| &lt;ProgressTemplate&gt; | このコントロールに表示されるコンテンツに対して設定されたコントロールテンプレートを格納します。 |

UpdateProgress コントロールを使用すると、サーバーに転送するために必要な作業を行っているときに、ユーザーの関心を維持するためのフィードバックを行うことができます。 これにより、特に、ほとんどのユーザーがページの更新に使用され、ステータスバーが強調表示されているため、ユーザーは何もしないことがわかります。

注として、UpdateProgress コントロールはページ階層の任意の場所に表示されます。 ただし、部分ポストバックが子 UpdatePanel から開始された場合 (UpdatePanel が別の UpdatePanel 内に入れ子になっている場合)、子 UpdatePanel をトリガーするポストバックによって、子の UpdateProgress テンプレートが表示されます。UpdatePanel および親 UpdatePanel。 ただし、トリガーが親の UpdatePanel の直接の子である場合は、親に関連付けられている UpdateProgress テンプレートのみが表示されます。

## <a name="summary"></a>要約

Microsoft ASP.NET AJAX 拡張機能は、web コンテンツにアクセスしやすくし、web アプリケーションにより充実したユーザーエクスペリエンスを提供できるように設計された、洗練された製品です。 ASP.NET AJAX 拡張機能の一部として、ScriptManager、UpdatePanel、および UpdateProgress コントロールを含む部分ページレンダリングコントロールが、ツールキットの最も可視性の高いコンポーネントの一部になります。

ScriptManager コンポーネントは、拡張機能のクライアント JavaScript のプロビジョニングを統合するだけでなく、さまざまなサーバーおよびクライアント側コンポーネントが、最小限の開発投資で連携できるようにします。

UpdatePanel コントロールは見かけ上のマジックボックスであり、UpdatePanel 内のマークアップはサーバー側の分離コードを持つことができ、ページの更新をトリガーしません。 UpdatePanel コントロールは入れ子にすることができ、他の UpdatePanels のコントロールに依存できます。 既定では、UpdatePanels は、その子孫コントロールによって呼び出されるポストバックを処理します。ただし、この機能は、宣言的またはプログラムによってきめ細かく調整できます。

UpdatePanel コントロールを使用する場合、開発者は、発生する可能性があるパフォーマンスへの影響に注意する必要があります。 考えられる代替手段として、web サービスとページメソッドがあります。ただし、アプリケーションの設計は考慮する必要があります。

UpdateProgress コントロールを使用すると、ユーザーが無視しないこと、およびバックグラウンドでの要求が行われている間、ページがユーザー入力に応答する処理を実行していないことを知ることができます。 また、部分的なレンダリングの結果を中止する機能も含まれています。

これらのツールを一緒に使用すると、サーバーの動作をユーザーに明らかにせず、ワークフローを中断することで、豊富でシームレスなユーザーエクスペリエンスを実現できます。

## <a name="bio"></a>略歴

Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。 Scott は、 [scott.cate@myKB.com](mailto:scott.cate@myKB.com)または彼のブログ ( [ScottCate.com](http://ScottCate.com) ) で、電子メールで連絡を受けることができます。

> [!div class="step-by-step"]
> [次へ](understanding-asp-net-ajax-updatepanel-triggers.md)
