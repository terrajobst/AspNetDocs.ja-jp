---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: マスターページとパーシャルを使用して UI を再利用する |Microsoft Docs
author: microsoft
description: 手順7では、ビューテンプレート内に "ドライ原理" を適用して、部分ビューテンプレートとマスターページを使用してコードの重複を排除する方法を見ていきます。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468724"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>マスター ページと部分を利用して UI を再使用する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順7です。
> 
> 手順7では、ビューテンプレート内で "ドライ原理" を適用して、部分ビューテンプレートとマスターページを使用してコードの重複を排除する方法を見ていきます。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-7-partials-and-master-pages"></a>手順 7: パーシャルとマスターページを操作する

ASP.NET MVC の開発理念の1つは、"何も繰り返さない" という原則 (一般に "ドライ" と呼ばれます) です。 ドライデザインは、コードとロジックの重複を排除するのに役立ちます。これにより、最終的にアプリケーションのビルドが高速化され、保守が容易になります。

私たちは、私たちのいくつかの例において、既にドライの原則が適用されています。 いくつかの例を次に示します。検証ロジックは、モデルレイヤー内に実装されています。これにより、コントローラーの編集シナリオと作成シナリオの両方で適用できます。Edit、Details、Delete アクションの各メソッドで "NotFound" ビューテンプレートを再利用しています。ここでは、ビューテンプレートで規則の命名パターンを使用しています。これにより、View () ヘルパーメソッドを呼び出すときに名前を明示的に指定する必要がなくなります。さらに、編集と作成アクションの両方のシナリオで Dinを再利用しています。

ここで、ビューテンプレート内に "ドライ原理" を適用して、コードの重複を排除する方法を見てみましょう。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>編集および作成ビューのテンプレートを再度閲覧する

現在、2つの異なるビューテンプレート ("Edit .aspx" と "default.aspx") を使用して、ディナーフォーム UI を表示しています。 視覚的な比較では、これらの類似点が強調表示されます。 作成フォームは次のようになります。

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

"Edit" フォームは次のようになります。

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

違いはほとんどありませんか。 タイトルとヘッダーのテキスト以外のフォームレイアウトと入力コントロールは同じです。

"Edit .aspx" ビューと ".aspx" ビューテンプレートを開くと、同一のフォームレイアウトと入力制御コードが含まれていることがわかります。 この重複は、新しいディナープロパティを導入または変更するたびに、変更を2回行う必要があることを意味します (これは適切ではありません)。

### <a name="using-partial-view-templates"></a>部分ビューテンプレートの使用

ASP.NET MVC では、ページのサブ部分のビューレンダリングロジックをカプセル化するために使用できる "部分ビュー" テンプレートを定義する機能がサポートされています。 "パーシャル" を使用すると、表示ロジックを1回だけ定義し、アプリケーションの複数の場所で再利用するための便利な方法が提供されます。

編集用の .aspx を "乾か" し、.aspx ビューテンプレートの複製を作成するには、両方に共通するフォームレイアウトと入力要素をカプセル化する "Din" という名前の部分ビューテンプレートを作成します。 この操作を行うには、/Views/Dinners ディレクトリを右クリックし、[&gt;ビューの追加] メニューコマンドを選択します。

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

[ビューの追加] ダイアログが表示されます。 "Dinフォーム" を作成する新しいビューに名前を指定し、ダイアログ内の [部分ビューを作成します] チェックボックスをオンにして、これを Dinに渡すことを示します。

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Din" ビューテンプレートが作成されます。

次に、Edit .aspx/Create .aspx ビューテンプレートから、複製されたフォームレイアウト/入力制御コードをコピーして、新しい "Din. .ascx" 部分ビューテンプレートに貼り付けます。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

次に、Edit および Create view テンプレートを更新して、Dinフォーム部分テンプレートを呼び出し、フォームの重複を除去します。 これを行うには、ビューテンプレート内で Html の RenderPartial ("Dinの形式") を呼び出します。

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

.Html 部分を呼び出すときに、必要な部分テンプレートのパスを明示的に修飾できます (例: ~ Views/ディナー/Din)。 上記のコードでは、ASP.NET MVC 内で規約ベースの命名パターンを利用しています。また、レンダリングする部分の名前として "Dinare Form" を指定するだけです。 この操作を行うと、規則ベースの views ディレクトリで ASP.NET MVC が最初に表示されます (/Views/Dinners)。 部分的なテンプレートが見つからない場合は、[/]/[共有] ディレクトリで検索します。

部分ビューの名前だけを使用して Html の RenderPartial () が呼び出されると、ASP.NET MVC は、呼び出し元のビューテンプレートによって使用されるのと同じモデルおよび ViewData dictionary オブジェクトを部分ビューに渡します。 または、Html. RenderPartial () のオーバーロードされたバージョンがあります。これにより、部分ビューで使用する代替モデルオブジェクトまたは ViewData dictionary を渡すことができます。 これは、完全なモデル/ビューモデルのサブセットのみを渡す必要がある場合に便利です。

| **サイドトピック: &lt;%&gt;ではなく%%&gt; を &lt;理由** |
| --- |
| 上記のコードでは、Html の RenderPartial () を呼び出すときに &lt;% =%&gt; ブロックではなく &lt;%%&gt; ブロックを使用していることがわかります。 &lt;% =%&gt; ASP.NET のブロックは、開発者が指定された値を表示しようとしていることを示します (例: &lt;% = "Hello"%&gt; は "Hello" を表示します)。 &lt;%%&gt; ブロックは、開発者がコードを実行しようとしていること、およびその中のレンダリングされた出力を明示的に実行する必要があることを示しています (例: &lt;% Response. 書き込み ("Hello")%&gt;。 ここでは、&lt;%%&gt; ブロックを Html. RenderPartial コードで使用しています。これは、Html. RenderPartial () メソッドが文字列を返さず、代わりに、呼び出し元ビューテンプレートの出力ストリームに直接コンテンツを出力するためです。 これは、パフォーマンスの効率を向上させるために行われます。これにより、(非常に大きな可能性がある) 一時文字列オブジェクトを作成する必要がなくなります。 これにより、メモリ使用量が減り、アプリケーション全体のスループットが向上します。 .Html 部分 () を使用する場合の一般的な間違いの1つは、呼び出しの末尾にセミコロンを追加することです。これは、&lt;%%&gt; ブロック内にあるときに忘れられます。 たとえば、次のコードではコンパイラエラーが発生します。% Html. RenderPartial ("din&lt;Form")%&gt; は、次のように記述する必要があります: &lt;% .Html ("Din)")。%&gt; これは、&lt;%%&gt; ブロックが自己完結型のコードステートメントであるためC#です。また、コードステートメントを使用する場合は、セミコロンで終了する必要があります。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>部分ビューテンプレートを使用してコードを明確にする

ビューレンダリングロジックが複数の場所に複製されないように、"Dinform" 部分ビューテンプレートを作成しました。 これは、部分ビューテンプレートを作成する最も一般的な理由です。

場合によっては、1つの場所でのみ呼び出される場合でも、部分ビューを作成するのが理にかなっていることもあります。 ビューのレンダリングロジックを抽出し、1つまたは複数の適切な名前付き部分テンプレートにパーティション分割すると、非常に複雑なビューテンプレートが読みやすくなります。

たとえば、次のコードスニペットは、プロジェクトのサイトの .master ファイルからのものであるとします (これについては後で説明します)。 画面の右上にログイン/ログアウトリンクを表示するロジックは、"LogOnUserControl" 部分にカプセル化されているため、このコードは比較的簡単に読むことができます。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

ビューテンプレート内の html/コードマークアップを解釈しようとすると混乱が見られる場合は、その一部を抽出して、適切な名前の部分ビューにリファクタリングしたかどうかを検討してください。

### <a name="master-pages"></a>マスター ページ

ASP.NET MVC では、部分ビューをサポートするだけでなく、サイトの共通レイアウトとトップレベル html を定義するために使用できる "マスターページ" テンプレートを作成する機能もサポートされています。 次に、コンテンツプレースホルダーコントロールをマスターページに追加して、上書きまたはビューによる "塗りつぶし" が可能な置換可能な領域を識別できます。 これにより、アプリケーション全体に共通のレイアウトを適用するための、非常に効果的な (ドライ) 方法が提供されます。

既定では、新しい ASP.NET MVC プロジェクトには、自動的に追加されたマスターページテンプレートがあります。 このマスターページは、"\Views\Shared\" という名前で、次のフォルダー内に存在します。

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

既定のサイトのマスターファイルは次のようになります。 ここでは、サイトの外部 html と、上部のナビゲーションのメニューを定義します。 これには、2つの置き換え可能なコンテンツのプレースホルダーコントロールが含まれています。タイトルの場合は、もう1つはページのプライマリコンテンツを置き換える必要がある場合はです。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

これまでに作成したすべてのビューテンプレート ("リスト"、"詳細"、"編集"、"作成"、"NotFound" など) は、このサイトのマスターテンプレートに基づいています。 これは、[ビューの追加] ダイアログボックスを使用してビューを作成したときに、既定で top &lt;% @ Page%&gt; ディレクティブに追加された "MasterPageFile" 属性によって示されます。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

これは、サイトのマスターコンテンツを変更し、ビューテンプレートをレンダリングするときに、変更が自動的に適用されて使用されることを意味します。

ここでは、アプリケーションのヘッダーが "My MVC Application" ではなく "" である "というように、Site. マスターのヘッダーセクションを更新してみましょう。 また、ナビゲーションメニューを更新して、最初のタブが "Find a ディナー" (HomeController の Index () アクションメソッドによって処理されます) になるようにします。次に、"Host a ディナー" という名前の新しいタブを追加します (Dinの Scontroller の Create () アクションメソッドによって処理されます)。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

サイトのマスターファイルを保存してブラウザーを更新すると、アプリケーション内のすべてのビューでヘッダーの変更が表示されます。 次に例を示します。

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

また、/// */[id]* URL を使用すると、次のようになります。

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>次の手順

パーシャルおよびマスターページでは、ビューをクリーンに整理するための非常に柔軟なオプションが提供されます。 ビューのコンテンツやコードを複製して、ビューテンプレートを読みやすくし、管理しやすくするために役立つことがわかります。

先ほど作成したリストシナリオにもう一度目を通して、スケーラブルなページングサポートを有効にしましょう。

> [!div class="step-by-step"]
> [前へ](use-viewdata-and-implement-viewmodel-classes.md)
> [次へ](implement-efficient-data-paging.md)
