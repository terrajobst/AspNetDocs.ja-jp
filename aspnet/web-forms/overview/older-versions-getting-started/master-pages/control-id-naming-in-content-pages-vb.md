---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
title: コンテンツページでのコントロール ID の名前付け (VB) |Microsoft Docs
author: rick-anderson
description: ContentPlaceHolder コントロールが名前付けコンテナーとして機能するしくみを示します。したがって、プログラムでコントロールを操作する際には、(FindControl を使用した) 作業が困難になります。
ms.author: riande
ms.date: 06/10/2008
ms.assetid: dbb024a6-f043-4fc5-ad66-56556711875b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 3cb8dec47040bc65f1a024325c91590729ffbdb7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519238"
---
# <a name="control-id-naming-in-content-pages-vb"></a>コンテンツ ページのコントロール ID の名前付け (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_VB.pdf)

> ContentPlaceHolder コントロールが名前付けコンテナーとして機能するしくみを説明します。そのため、コントロールをプログラムで操作することが困難になります (FindControl を介して)。 この問題と回避策について見ていきます。 また、結果として得られる ClientID 値にプログラムでアクセスする方法についても説明します。

## <a name="introduction"></a>はじめに

すべての ASP.NET サーバーコントロールには、コントロールを一意に識別する `ID` のプロパティが含まれています。このプロパティは、コントロールが分離コードクラスでプログラムによってアクセスされる手段です。 同様に、HTML ドキュメント内の要素には、要素を一意に識別する `id` 属性を含めることができます。これらの `id` 値は、クライアント側スクリプトで、プログラムによって特定の HTML 要素を参照するために使用されます。 これにより、ASP.NET サーバーコントロールが HTML にレンダリングされるときに、その `ID` 値が、レンダリングされた HTML 要素の `id` 値として使用されると想定できます。 特定の状況では、1つの `ID` 値を持つ1つのコントロールが、レンダリングされたマークアップで複数回出現する可能性があるため、必ずしもそうであるとは限りません。 `ID` 値が `ProductName`のラベル Web コントロールを含む TemplateField を含む GridView コントロールについて考えてみます。 実行時に GridView がそのデータソースにバインドされている場合、このラベルは GridView 行ごとに1回繰り返されます。 表示される各ラベルには、一意の `id` 値が必要です。

このようなシナリオを処理するために、ASP.NET では、特定のコントロールを名前付けコンテナーとして示すことができます。 名前付けコンテナーは、新しい `ID` 名前空間として機能します。 名前付けコンテナー内に表示されるすべてのサーバーコントロールには、名前付けコンテナーコントロールの `ID` の先頭に `id` 値が付加されます。 たとえば、`GridView` クラスと `GridViewRow` クラスは両方ともコンテナーに名前を付けます。 その結果、GridView の TemplateField に定義された Label コントロール `ID` `ProductName` には、`GridViewID_GridViewRowID_ProductName`の `id` 値が表示されます。 *GridViewRowID*は各 GridView 行に対して一意であるため、結果として得られる `id` 値は一意になります。

> [!NOTE]
> [`INamingContainer` インターフェイス](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx)は、特定の ASP.NET サーバーコントロールが名前付けコンテナーとして機能する必要があることを示すために使用されます。 `INamingContainer` インターフェイスは、サーバーコントロールが実装する必要のあるメソッドをスペルチェックしません。代わりに、マーカーとして使用されます。 レンダリングされたマークアップを生成するときに、コントロールがこのインターフェイスを実装する場合、ASP.NET エンジンは、その `ID` 値の前に、その子孫の `id` 属性値を自動的にプレフィックスします。 このプロセスの詳細については、手順 2. で説明します。

コンテナーに名前を付けると、レンダリングされた `id` 属性値が変更されるだけでなく、ASP.NET ページの分離コードクラスからコントロールをプログラムで参照する方法にも影響します。 `FindControl("controlID")` メソッドは、通常、プログラムによって Web コントロールを参照するために使用されます。 ただし、`FindControl` は、名前付けコンテナーには浸透しません。 その結果、GridView または他の名前付けコンテナー内のコントロールを参照するために、`Page.FindControl` メソッドを直接使用することはできません。

Surmised があるかもしれませんが、マスターページと ContentPlaceHolders はどちらも名前付けコンテナーとして実装されています。 このチュートリアルでは、マスターページが HTML 要素 `id` 値に与える影響と、`FindControl`を使用してコンテンツページ内の Web コントロールをプログラムで参照する方法について説明します。

## <a name="step-1-adding-a-new-aspnet-page"></a>手順 1: 新しい ASP.NET ページを追加する

このチュートリアルで説明されている概念を示すために、web サイトに新しい ASP.NET ページを追加してみましょう。 ルートフォルダーに `IDIssues.aspx` という名前の新しいコンテンツページを作成し、`Site.master` マスターページにバインドします。

![コンテンツページ IDIssues をルートフォルダーに追加します。](control-id-naming-in-content-pages-vb/_static/image1.png)

**図 01**: ルートフォルダーに `IDIssues.aspx` コンテンツページを追加する

Visual Studio では、マスターページの4つの ContentPlaceHolders のそれぞれに対して、コンテンツコントロールが自動的に作成されます。 [*複数の contentplaceholders と既定のコンテンツ*](multiple-contentplaceholders-and-default-content-vb.md)のチュートリアルで説明したように、コンテンツコントロールが存在しない場合は、代わりにマスターページの既定の ContentPlaceHolder コンテンツが生成されます。 `QuickLoginUI` および `LeftColumnContent` ContentPlaceHolders には、このページに適切な既定のマークアップが含まれているため、`IDIssues.aspx`から対応するコンテンツコントロールを削除します。 この時点では、コンテンツページの宣言型マークアップは次のようになります。

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample1.aspx)]

[ *「マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)する」チュートリアルでは、明示的に設定されていない場合にページのタイトルを自動的に構成するカスタム基本ページクラス (`BasePage`) を作成しました。 `IDIssues.aspx` ページでこの機能を使用するには、ページの分離コードクラスが `BasePage` クラス (`System.Web.UI.Page`ではなく) から派生している必要があります。 次のように、分離コードクラスの定義を変更します。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample2.vb)]

最後に、この新しいレッスンのエントリを含めるように `Web.sitemap` ファイルを更新します。 `<siteMapNode>` 要素を追加し、その `title` と `url` 属性をそれぞれ "Control ID 名前付け問題" と `~/IDIssues.aspx`に設定します。 この追加を行った後、`Web.sitemap` ファイルのマークアップは次のようになります。

[!code-xml[Main](control-id-naming-in-content-pages-vb/samples/sample3.xml)]

図2に示すように、`Web.sitemap` の新しいサイトマップエントリは、左側の列のレッスンセクションにすぐに反映されます。

![レッスンのセクションには、&quot;コントロール ID の名前付けの問題へのリンクが含まれるようになりました&quot;](control-id-naming-in-content-pages-vb/_static/image2.png)

**図 02**: レッスンのセクションに、"コントロール ID の名前付けに関する問題" へのリンクが含まれるようになりました。

## <a name="step-2-examining-the-renderedidchanges"></a>手順 2: レンダリングされた`ID`の変更を調べる

ASP.NET エンジンによってサーバーコントロールの表示 `id` 値に対して行われる変更について理解を深めるために、`IDIssues.aspx` ページにいくつかの Web コントロールを追加し、ブラウザーに送信される表示マークアップを表示してみましょう。 具体的には、"age:" というテキストを入力し、その後にテキストボックス Web コントロールを入力します。 ページの下に、ボタン Web コントロールとラベル Web コントロールが追加されます。 TextBox の `ID` と `Columns` プロパティをそれぞれ `Age` と3に設定します。 ボタンの `Text` と `ID` プロパティを "Submit" に設定し、`SubmitButton`します。 ラベルの `Text` プロパティをクリアし、その `ID` を `Results`に設定します。

この時点で、コンテンツコントロールの宣言型マークアップは次のようになります。

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample4.aspx)]

図3は、Visual Studio のデザイナーを使用して表示するときのページを示しています。

[ページには、テキストボックス、ボタン、およびラベルという3つの Web コントロールが含まれて ![ます。](control-id-naming-in-content-pages-vb/_static/image4.png)](control-id-naming-in-content-pages-vb/_static/image3.png)

**図 03**: ページには、テキストボックス、ボタン、およびラベルという3つの Web コントロールが含まれています ([クリックすると、フルサイズの画像が表示](control-id-naming-in-content-pages-vb/_static/image5.png)されます)

ブラウザーを使用してページにアクセスし、HTML ソースを表示します。 次のマークアップに示されているように、テキストボックス、ボタン、およびラベル Web コントロールの HTML 要素の `id` 値は、Web コントロールの `ID` 値と、ページ内の名前付けコンテナーの `ID` 値の組み合わせです。

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample5.html)]

このチュートリアルで既に説明したように、マスターページとその ContentPlaceHolders は両方とも名前付けコンテナーとして機能します。 そのため、どちらも、入れ子になったコントロールの表示された `ID` 値に寄与します。 TextBox の `id` 属性を取得します。例: `ctl00_MainContent_Age`。 TextBox コントロールの `ID` 値が `Age`たことを思い出してください。 これには、ContentPlaceHolder コントロールの `ID` 値 `MainContent`がプレフィックスとして付けられます。 さらに、この値には、マスターページの `ID` 値 `ctl00`がプレフィックスとして付けられます。 純効果は、マスターページ、ContentPlaceHolder コントロール、およびテキストボックス自体の `ID` 値で構成される `id` 属性値です。

図4に、この動作を示します。 `Age` テキストボックスの表示されている `id` を確認するには、テキストボックスコントロールの `ID` の値を使用して `Age`を開始します。 次に、制御階層を操作します。 各名前付けコンテナー (ピーチ色のノード) で、現在表示されている `id` に名前付けコンテナーの `id`というプレフィックスを付けます。

![レンダリングされた id 属性は、名前付けコンテナーの ID 値に基づいています。](control-id-naming-in-content-pages-vb/_static/image6.png)

**図 04**: 表示される `id` 属性は、名前付けコンテナーの `ID` 値に基づいています。

> [!NOTE]
> 既に説明したように、表示される `id` 属性の `ctl00` 部分はマスターページの `ID` 値を構成しますが、この `ID` の値について疑問に思うかもしれません。 ここでは、マスターページまたはコンテンツページのどこにも指定しませんでした。 ASP.NET ページのほとんどのサーバーコントロールは、ページの宣言型マークアップによって明示的に追加されます。 `MainContent` ContentPlaceHolder コントロールが `Site.master`のマークアップで明示的に指定されました。`Age` TextBox は `IDIssues.aspx`のマークアップで定義されています。 これらのコントロールの `ID` 値は、プロパティウィンドウまたは宣言型の構文から指定できます。 マスターページ自体のような他のコントロールは、宣言型マークアップで定義されていません。 そのため、`ID` 値は自動的に生成される必要があります。 ASP.NET エンジンは、Id が明示的に設定されていないコントロールに対して、実行時に `ID` 値を設定します。 この例では、`ctlXX`という名前付けパターンを使用します。ここで、 *XX*は整数値を順番に増加させます。

マスターページ自体は名前付けコンテナーとして機能するため、マスターページで定義されている Web コントロールにも、表示される `id` 属性値が変更されています。 たとえば、「[*マスターページを使用したサイト全体のレイアウトの作成*](creating-a-site-wide-layout-using-master-pages-vb.md)」チュートリアルのマスターページに追加した `DisplayDate` ラベルには、次のように表示されるマークアップがあります。

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample6.html)]

`id` 属性には、マスターページの `ID` 値 (`ctl00`) と、ラベル Web コントロール (`DateDisplay`) の `ID` 値の両方が含まれていることに注意してください。

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>手順 3: プログラムを使用して`FindControl` によって Web コントロールを参照する

すべての ASP.NET サーバーコントロールには、コントロールの子孫が*controlID*という名前のコントロールを検索する `FindControl("controlID")` メソッドが含まれています。 このようなコントロールが見つかった場合は、が返されます。一致するコントロールが見つからない場合、`FindControl` は `Nothing`を返します。

`FindControl` は、コントロールにアクセスする必要があるが、直接参照がない場合に便利です。 たとえば、gridview のようなデータ Web コントロールを使用する場合、GridView のフィールド内のコントロールは宣言構文で1回定義されますが、実行時には、各 GridView 行に対してコントロールのインスタンスが作成されます。 その結果、実行時に生成されるコントロールは存在しますが、分離コードクラスから直接参照することはできません。 そのため、GridView のフィールド内の特定のコントロールをプログラムで操作するには、`FindControl` を使用する必要があります。 (`FindControl` を使用してデータ Web コントロールのテンプレート内のコントロールにアクセスする方法の詳細については、「[データに基づくカスタム書式](../../data-access/custom-formatting/custom-formatting-based-upon-data-vb.md)設定」を参照してください)。この同じシナリオは、web コントロールを Web フォームに動的に追加する場合にも発生します。これは、「[動的データエントリのユーザーインターフェイスの作成](https://msdn.microsoft.com/library/aa479330.aspx)」で説明されているトピックです。

`FindControl` メソッドを使用してコンテンツページ内のコントロールを検索する方法を示すために、`SubmitButton`の `Click` イベントのイベントハンドラーを作成します。 イベントハンドラーに次のコードを追加します。このコードは、`FindControl` メソッドを使用して `Age` TextBox と `Results` ラベルをプログラムによって参照し、ユーザーの入力に基づいて `Results` にメッセージを表示します。

> [!NOTE]
> もちろん、この例のラベルコントロールとテキストボックスコントロールを参照するために `FindControl` を使用する必要はありません。 `ID` のプロパティ値を使用して直接参照できます。 ここでは `FindControl` を使用して、コンテンツページから `FindControl` を使用した場合の動作を説明します。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample7.vb)]

`FindControl` メソッドの呼び出しに使用される構文は、`SubmitButton_Click`の最初の2行で若干異なりますが、意味は同じです。 ASP.NET のすべてのサーバーコントロールに `FindControl` メソッドが含まれていることを思い出してください。 これには `Page` クラスが含まれます。このクラスから、すべての ASP.NET 分離コードクラスを派生させる必要があります。 したがって、`FindControl("controlID")` を呼び出すことは、分離コードクラスまたはカスタム基本クラスで `FindControl` メソッドをオーバーライドしていないという前提で `Page.FindControl("controlID")`を呼び出すことと同じです。

このコードを入力したら、ブラウザーを使用して `IDIssues.aspx` のページにアクセスし、年齢を入力して、[送信] ボタンをクリックします。 [送信] ボタンをクリックすると `NullReferenceException` が発生します (図5を参照)。

[NullReferenceException が発生した ![](control-id-naming-in-content-pages-vb/_static/image8.png)](control-id-naming-in-content-pages-vb/_static/image7.png)

**図 05**: `NullReferenceException` が発生します ([クリックすると、フルサイズの画像が表示](control-id-naming-in-content-pages-vb/_static/image9.png)されます)

`SubmitButton_Click` イベントハンドラーにブレークポイントを設定すると、`FindControl` への両方の呼び出しが `Nothing`を返すことがわかります。 `NullReferenceException` は、`Age` TextBox の `Text` プロパティにアクセスしようとしたときに発生します。

問題は、`Control.FindControl` は、同じ名前付けコンテナー内にある*コントロール*の子孫のみを検索することです。 マスターページは新しい名前付けコンテナーを構成するので、`Page.FindControl("controlID")` を呼び出すと、マスターページオブジェクトの `ctl00`が permeates されることはありません。 (図4を参照してコントロール階層を表示します。これにより、`Page` オブジェクトがマスターページ `ctl00`オブジェクトの親として表示されます)。したがって、`Results` ラベルと `Age` テキストボックスは見つかりません。 `ResultsLabel` および `AgeTextBox` には `Nothing`の値が割り当てられます。

この課題には2つの回避策があります。一度に1つの名前付けコンテナーを適切なコントロールにドリルダウンできます。または、コンテナーの名前を permeates する独自の `FindControl` メソッドを作成することもできます。 これらの各オプションについて説明します。

### <a name="drilling-into-the-appropriate-naming-container"></a>適切な名前付けコンテナーへのドリルダウン

`FindControl` を使用して `Results` ラベルまたは `Age` TextBox を参照するには、同じ名前付けコンテナー内の先祖コントロールから `FindControl` を呼び出す必要があります。 図4に示すように、`MainContent` ContentPlaceHolder コントロールは、同じ名前付けコンテナー内にある `Results` または `Age` の唯一の先祖です。 言い換えると、次のコードスニペットに示すように、`MainContent` コントロールから `FindControl` メソッドを呼び出すと、`Results` または `Age` のコントロールへの参照が正しく返されます。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample8.vb)]

ただし、ContentPlaceHolder がマスターページで定義されているため、上記の構文を使用して、コンテンツページの分離コードクラスから `MainContent` ContentPlaceHolder を操作することはできません。 代わりに、`FindControl` を使用して `MainContent`への参照を取得する必要があります。 `SubmitButton_Click` イベントハンドラーのコードを次のように変更します。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample9.vb)]

ブラウザーでページにアクセスする場合は、年齢を入力し、[Submit] \ (送信 \) ボタンをクリックすると `NullReferenceException` が発生します。 `SubmitButton_Click` イベントハンドラーにブレークポイントを設定すると、`MainContent` オブジェクトの `FindControl` メソッドを呼び出そうとしたときに、この例外が発生することがわかります。 `FindControl` メソッドが "MainContent" という名前のオブジェクトを見つけることができないため、`MainContent` オブジェクトは `Nothing` と同じです。 基になる理由は、`Results` Label および `Age` TextBox コントロールと同じです。 `FindControl` は、コントロール階層の最上位から検索を開始し、名前付けコンテナーには対応しませんが、`MainContent` ContentPlaceHolder は、名前付けコンテナーであるマスターページ内にあります。

`FindControl` を使用して `MainContent`への参照を取得できるようにするには、まずマスターページコントロールへの参照が必要です。 マスターページへの参照を取得したら、`FindControl` を介して `MainContent` ContentPlaceHolder への参照を取得し、そこから `Results` ラベルと `Age` TextBox への参照 (`FindControl`を使用して) を取得できます。 では、マスターページへの参照を取得するにはどうすればよいでしょうか。 レンダリングされたマークアップ内の `id` 属性を調べることで、マスターページの `ID` 値が `ctl00`ことが明らかになります。 したがって、`Page.FindControl("ctl00")` を使用してマスターページへの参照を取得し、そのオブジェクトを使用して `MainContent`への参照を取得することもできます。 次のスニペットは、このロジックを示しています。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample10.vb)]

このコードは確実に動作しますが、マスターページの自動生成された `ID` が常に `ctl00`であると想定しています。 自動生成された値についての仮定を作成することはお勧めできません。

幸いなことに、マスターページへの参照には、`Page` クラスの `Master` プロパティを使用してアクセスできます。 したがって、`MainContent` ContentPlaceHolder にアクセスするためにマスターページの参照を取得するために `FindControl("ctl00")` を使用するのではなく、代わりに `Page.Master.FindControl("MainContent")`を使用できます。 次のコードを使用して、`SubmitButton_Click` イベントハンドラーを更新します。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample11.vb)]

今度は、ブラウザーを使用してページにアクセスし、年齢を入力して、[Submit] \ (送信 \) ボタンをクリックすると、`Results` ラベルにメッセージが表示されます。

[ユーザーの年齢がラベルに表示される ![](control-id-naming-in-content-pages-vb/_static/image11.png)](control-id-naming-in-content-pages-vb/_static/image10.png)

**図 06**: ユーザーの年齢がラベルに表示される ([クリックすると、フルサイズの画像が表示](control-id-naming-in-content-pages-vb/_static/image12.png)されます)

### <a name="recursively-searching-through-naming-containers"></a>名前付けコンテナーを再帰的に検索する

前のコード例では、マスターページから `MainContent` ContentPlaceHolder コントロールを参照し、次に `MainContent`からの `Results` Label および `Age` TextBox コントロールを参照する理由は、`Control.FindControl` メソッドが*コントロール*の名前付けコンテナー内を検索するためです。 2つの異なる名前付けコンテナー内の2つのコントロールが同じ `ID` 値を持つ可能性があるので、ほとんどのシナリオでは、名前付けコンテナー内の `FindControl` を維持することは理にかなっています。 `ProductName` という名前のラベル Web コントロールを TemplateFields の1つ内に定義する GridView の場合を考えてみます。 実行時にデータが GridView にバインドされると、GridView 行ごとに `ProductName` ラベルが作成されます。 すべての名前付けコンテナーを検索 `FindControl`、`Page.FindControl("ProductName")`を呼び出した場合、`FindControl` が返すラベルのインスタンスはどのようなものでしょうか。 最初の GridView 行の `ProductName` ラベル 最後の行の1つ。

そのため、ほとんどの場合、*コントロール*の名前付けコンテナーだけを `Control.FindControl` 検索することが理にかなっています。 ただし、他のケースもあります。たとえば、すべての名前付けコンテナーに一意の `ID` があり、コントロール階層内の各名前付けコンテナーを参照してコントロールにアクセスする必要がないようにする場合などです。 すべての名前付けコンテナーを再帰的に検索する `FindControl` バリアントを使用することも意味があります。 残念ながら、.NET Framework にはこのようなメソッドは含まれていません。

優れたニュースとして、すべての名前付けコンテナーを再帰的に検索する独自の `FindControl` メソッドを作成できるということです。 実際には、*拡張メソッド*を使用して、既存の `FindControl` メソッドに付随する `FindControlRecursive` メソッドを `Control` クラスに付加することができます。

> [!NOTE]
> 拡張メソッドは、 C# 3.0 および Visual Basic 9 の新機能であり、.NET Framework バージョン3.5 および Visual Studio 2008 に付属している言語です。 簡単に言えば、拡張メソッドを使用すると、開発者は特殊な構文を使用して既存のクラス型の新しいメソッドを作成できます。 この便利な機能の詳細については、「my article」 ([拡張メソッドを使用した基本型の機能の拡張](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)) を参照してください。

拡張メソッドを作成するには、`PageExtensionMethods.vb`という名前の `App_Code` フォルダーに新しいファイルを追加します。 `controlID`という名前の `String` パラメーターを入力として受け取る `FindControlRecursive` という名前の拡張メソッドを追加します。 拡張メソッドが適切に機能するためには、クラスが `Module` としてマークされ、拡張メソッドに `<Extension()>` 属性がプレフィックスとして付けられていることが重要です。 さらに、すべての拡張メソッドは、拡張メソッドが適用される型のオブジェクトを最初のパラメーターとして受け入れる必要があります。

次のコードを `PageExtensionMethods.vb` ファイルに追加して、この `Module` と `FindControlRecursive` 拡張メソッドを定義します。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample12.vb)]

このコードを配置したら、`IDIssues.aspx` ページの分離コードクラスに戻り、現在の `FindControl` メソッドの呼び出しをコメントアウトします。 これらを `Page.FindControlRecursive("controlID")`の呼び出しに置き換えます。 拡張メソッドは、IntelliSense のドロップダウンリスト内に直接表示されるという点で便利です。 図7に示すように、`Page` を入力し、[期間] をクリックすると、他の `Control` クラスのメソッドと共に、`FindControlRecursive` メソッドが IntelliSense のドロップダウンに含まれます。

[IntelliSense のドロップダウンには ![拡張メソッドが含まれています](control-id-naming-in-content-pages-vb/_static/image14.png)](control-id-naming-in-content-pages-vb/_static/image13.png)

**図 07**: 拡張メソッドが IntelliSense のドロップダウンに含まれる ([クリックしてフルサイズのイメージを表示する](control-id-naming-in-content-pages-vb/_static/image15.png))

`SubmitButton_Click` イベントハンドラーに次のコードを入力し、ページにアクセスして年齢を入力し、[Submit] \ (送信 \) ボタンをクリックしてテストします。 図6に示すように、結果として得られる出力は "年齢は歳です" というメッセージになります。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample13.vb)]

> [!NOTE]
> 拡張メソッドはC# 3.0 および Visual Basic 9 の新機能であるため、Visual Studio 2005 を使用している場合は、拡張メソッドを使用できません。 代わりに、ヘルパークラスに `FindControlRecursive` メソッドを実装する必要があります。 [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx)には、このような例が含まれています。この例は、ブログ投稿、 [ASP.NET メーザページ、および `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)です。

## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>手順 4: クライアント側スクリプトで正しい`id`属性値を使用する

このチュートリアルの概要で説明したように、Web コントロールの表示される `id` 属性は、プログラムによって特定の HTML 要素を参照するために、クライアント側スクリプトでよく使用されます。 たとえば、次の JavaScript は、`id` によって HTML 要素を参照し、その値をモーダルメッセージボックスに表示します。

[!code-csharp[Main](control-id-naming-in-content-pages-vb/samples/sample14.cs)]

名前付けコンテナーを含まない ASP.NET ページでは、レンダリングされた HTML 要素の `id` 属性は、Web コントロールの `ID` プロパティ値と同じであることを思い出してください。 このため、`id` 属性値を JavaScript コードにハードコーディングすることが魅力的です。 つまり、クライアント側スクリプトを使用して `Age` TextBox Web コントロールにアクセスすることがわかっている場合は、`document.getElementById("Age")`の呼び出しを使用します。

この方法の問題は、マスターページ (またはその他の名前付けコンテナーコントロール) を使用する場合、レンダリングされる HTML `id` が Web コントロールの `ID` プロパティと同義ではないことです。 最初の傾斜として、ブラウザーを使用してページにアクセスし、ソースを表示して実際の `id` 属性を確認することができます。 レンダリングされた `id` 値がわかれば、`getElementById` の呼び出しに貼り付けることで、クライアント側のスクリプトを使用して作業するために必要な HTML 要素にアクセスできます。 この方法は、ページのコントロール階層に対する特定の変更、または名前付けコントロールの `ID` プロパティの変更によって、結果の `id` 属性が変更され、その結果、JavaScript コードが破損するため、理想的な方法よりも小さくなります。

さいわいにも、表示される `id` 属性値は、Web コントロールの[`ClientID` プロパティ](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)を通じてサーバー側のコードでアクセスできるということです。 このプロパティを使用して、クライアント側スクリプトで使用する `id` 属性値を決定する必要があります。 たとえば、ページに JavaScript 関数を追加して、呼び出されたときに、モーダルメッセージボックスに `Age` TextBox の値を表示するには、`Page_Load` イベントハンドラーに次のコードを追加します。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample15.vb)]

上記のコードは、`Age` TextBox の `ClientID` プロパティの値を `getElementById`への JavaScript 呼び出しに挿入します。 ブラウザーを使用してこのページにアクセスし、HTML ソースを表示すると、次の JavaScript コードが表示されます。

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample16.html)]

`getElementById`の呼び出し内で、正しい `id` 属性値 `ctl00_MainContent_Age`がどのように表示されるかに注目してください。 この値は実行時に計算されるので、後でページコントロール階層に加えられた変更に関係なく動作します。

> [!NOTE]
> この JavaScript の例では、サーバーコントロールによってレンダリングされる HTML 要素を正しく参照する JavaScript 関数を追加する方法を示しています。 この関数を使用するには、ドキュメントの読み込み時または特定のユーザーアクションの発生時に関数を呼び出すために、追加の JavaScript を作成する必要があります。 これらのトピックと関連トピックの詳細については、「[クライアント側スクリプトの使用](https://msdn.microsoft.com/library/aa479302.aspx)」を参照してください。

## <a name="summary"></a>まとめ

特定の ASP.NET サーバーコントロールは、名前付けコンテナーとして機能します。これは、子孫コントロールの表示される `id` 属性値と、`FindControl` メソッドによって canvassed されるコントロールのスコープに影響します。 マスターページに関しては、マスターページ自体とその ContentPlaceHolder コントロールの両方がコンテナーに名前を付けています。 そのため、`FindControl`を使用してコンテンツページ内のコントロールをプログラムで参照するには、もう少し作業を行う必要があります。 このチュートリアルでは、ContentPlaceHolder コントロールへのドリルダウンと `FindControl` メソッドの呼び出しという2つの手法について説明します。また、すべての名前付けコンテナーを再帰的に検索する、独自の `FindControl` 実装をロールします。

参照先の Web コントロールに関して、コンテナーに名前を付けるサーバー側の問題に加えて、クライアント側の問題もあります。 名前付けコンテナーが存在しない場合、Web コントロールの `ID` プロパティ値と表示される `id` 属性値は同じになります。 ただし、名前付けコンテナーを追加すると、表示される `id` 属性には、Web コントロールの `ID` 値と、コントロール階層の先祖にある名前付けコンテナーの両方が含まれます。 これらの名前付けの問題は、Web コントロールの `ClientID` プロパティを使用して、クライアント側スクリプトで表示される `id` 属性値を決定する限り、問題にはなりません。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET マスターページと `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [動的データエントリのユーザーインターフェイスの作成](https://msdn.microsoft.com/library/aa479330.aspx)
- [拡張メソッドを使用した基本型の機能の拡張](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [方法: ASP.NET マスターページコンテンツを参照する](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [マスターページ: ヒント、テクニック、およびトラップ](http://www.odetocode.com/articles/450.aspx)
- [クライアント側スクリプトの操作](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリーダーレビュー担当者は、Zack Jones と Suchi Barnerjee でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](urls-in-master-pages-vb.md)
> [次へ](interacting-with-the-master-page-from-the-content-page-vb.md)
