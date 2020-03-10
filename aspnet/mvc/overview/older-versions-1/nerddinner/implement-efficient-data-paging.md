---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 効率的なデータページングを実装する |Microsoft Docs
author: microsoft
description: 手順 8. 数千のディナーを一度に表示するのではなく、/Dinners の URL にページングサポートを追加する方法について説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486484"
---
# <a name="implement-efficient-data-paging"></a>効率的なデータ ページングを実装する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順8です。
> 
> 手順 8. では、/Dinners URL にページングサポートを追加して、ディナーの数千を一度に表示するのではなく、一度に10個のディナーが表示されるようにして、エンドユーザーがリスト全体を反復可能な方法でページバックして前方に移動できるようにする方法を示します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-8-paging-support"></a>ステップ 8: ページングのサポート

サイトが正常に実行されると、何千ものディナーがあります。 これらのすべてのディナーを処理し、ユーザーが参照できるように UI をスケーリングする必要があります。 これを有効にするには、 */Dinners* URL にページングサポートを追加します。これにより、数千 of ディナーを一度に表示するのではなく、一度に10個のディナーが表示されるようになり、エンドユーザーが SEO のわかりやすい方法でリスト全体をページバックおよび転送できるようになります。

### <a name="index-action-method-recap"></a>Index () アクションメソッドの要約

次のように、Dinのコントローラークラス内の Index () アクションメソッドは、現在は次のようになります。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

*/Dinners* URL に対して要求が行われると、今後のすべてのディナーの一覧を取得し、すべての一覧を表示します。

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>IQueryable&lt;T&gt; について

*IQueryable&lt;t&gt;* は、.net 3.5 の一部として LINQ で導入されたインターフェイスです。 これにより、ページングサポートを実装するために利用できる強力な "遅延実行" シナリオが可能になります。

このリポジトリでは、FindUpcomingDinners () メソッドから IQueryable&lt;ディナー&gt; シーケンスを返しています。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

FindUpcomingDinners () メソッドによって返される IQueryable&lt;ディナー&gt; オブジェクトは、LINQ to SQL を使用してデータベースからディナーオブジェクトを取得するクエリをカプセル化します。 重要なのは、クエリ内のデータに対してアクセスまたは反復処理を試みるか、そのデータに対して ToList () メソッドを呼び出すまで、データベースに対してクエリを実行しないことです。 FindUpcomingDinners () メソッドを呼び出すコードでは、必要に応じて、クエリを実行する前に、IQueryable&lt;ディナー&gt; オブジェクトに "チェーン" 操作/フィルターを追加することを選択できます。 その後、データが要求されたときにデータベースに対して結合クエリを実行するのに十分な LINQ to SQL です。

ページングロジックを実装するには、Din() を呼び出す前に、返された IQueryable&lt;ディナー&gt; シーケンスに追加の "Skip" 演算子と "Take" 演算子を適用するように、dinの Scontroller の Index () アクションメソッドを更新します。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上記のコードは、データベース内の最初の10個のディナーをスキップし、戻り値の20ディナーを返します。 LINQ to SQL は、web サーバーではなく、SQL database でこのスキップロジックを実行する最適化された SQL クエリを作成するのに十分なスマートです。 これは、データベースに数百万のディナーがある場合でも、必要な10のみをこの要求の一部として取得することを意味します (効率と拡張性を実現します)。

### <a name="adding-a-page-value-to-the-url"></a>URL への "ページ" 値の追加

特定のページ範囲をハードコーディングするのではなく、ユーザーが要求しているディナー範囲を示す "page" パラメーターを Url に含めるようにします。

#### <a name="using-a-querystring-value"></a>Querystring 値の使用

次のコードは、クエリ文字列パラメーターをサポートする Index () アクションメソッドを更新し、 */Dinners? page = 2*のような url を有効にする方法を示しています。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上記の Index () アクションメソッドには、"page" という名前のパラメーターがあります。 パラメーターが null 許容の整数として宣言されています (int? はを示します)。 これは、 */Dinners? page = 2* URL によって値 "2" がパラメーター値として渡されることを意味します。 */Dinners* URL (querystring 値なし) を指定すると、null 値が渡されます。

ページの値をページサイズ (この場合は10行) で乗算して、スキップするディナーの数を決定します。 Null 許容型を処理するときに役立つ、 [ C# null の "合体" 演算子 (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)を使用しています。 ページパラメーターが null の場合、上記のコードによって値0が割り当てられます。

#### <a name="using-embedded-url-values"></a>埋め込み URL 値の使用

Querystring 値を使用する代わりに、実際の URL 自体にページパラメーターを埋め込むこともできます。 たとえば、次のよう*になります*(例:// *page/page/* /)。 ASP.NET MVC には、このようなシナリオを簡単にサポートできる強力な URL ルーティングエンジンが含まれています。

任意の受信 URL または URL 形式を任意のコントローラークラスまたはアクションメソッドにマップするカスタムルーティング規則を登録できます。 必要なのは、プロジェクト内で global.asax ファイルを開くことだけです。

![](implement-efficient-data-paging/_static/image2.png)

次に、ルートの最初の呼び出しのような MapRoute () ヘルパーメソッドを使用して、新しいマッピング規則を登録します。MapRoute () 以下:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

上の例では、"UpcomingDinners" という名前の新しいルーティング規則を登録しています。 URL 形式が "ディナー/Page/{Page}" であることを示しています。 {Page} は、URL 内に埋め込まれているパラメーター値です。 MapRoute () メソッドの3番目のパラメーターは、この形式に一致する Url を、Dinの Scontroller クラスの Index () アクションメソッドにマップする必要があることを示しています。

以前に使用したものとまったく同じインデックス () コードをクエリ文字列シナリオで使用できます。ただし、"page" パラメーターは、querystring ではなく URL から取得されるようになりました。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

ここで、アプリケーションを実行し、 */Dinners*に「」と入力すると、次のディナーの最初の10が表示されます。

![](implement-efficient-data-paging/_static/image3.png)

*/Dinners/Page/1*に入力すると、ディナーの次のページが表示されます。

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>ページナビゲーション UI の追加

ページングシナリオを完了するための最後の手順は、ビューテンプレート内に "next" および "previous" ナビゲーション UI を実装して、ユーザーがディナーデータを簡単にスキップできるようにすることです。

これを正しく実装するには、データベースのディナーの合計数と、このが変換されるデータのページ数を把握しておく必要があります。 次に、現在要求されている "ページ" 値がデータの先頭または末尾にあるかどうかを計算し、それに従って "previous" と "next" UI を表示または非表示にする必要があります。 このロジックは、Index () アクションメソッド内に実装できます。 または、このロジックを再利用可能な方法でカプセル化するヘルパークラスをプロジェクトに追加することもできます。

次に示すのは、.NET Framework に組み込まれている&lt;T&gt; コレクションクラスのリストから派生する単純な "PaginatedList" ヘルパークラスです。 再利用可能なコレクションクラスを実装しています。このクラスを使用すると、IQueryable データの任意のシーケンスに改ページすることができます。 この例では、IQueryable&lt;ディナー&gt; の結果を処理していますが、その他のアプリケーションシナリオでは、IQueryable&lt;製品&gt; または IQueryable&lt;の結果に簡単に使用できます。&gt;

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

"PageIndex"、"PageSize"、"TotalCount"、"TotalPages" などのプロパティがどのように計算され、公開されるかに注目してください。 さらに、コレクション内のデータのページが元のシーケンスの先頭または末尾にあるかどうかを示す、2つのヘルパープロパティ "HasPreviousPage" と "HasNextPage" を公開します。 上記のコードでは、2つの SQL クエリが実行されます。1つ目は、1つは整数を返す "SELECT COUNT" ステートメントを実行し、もう1つはオブジェクトを返さず、次の行だけを取得するためです。データの現在のページについて、データベースから必要なデータを提供します。

次に、DinPaginatedList () ヘルパーメソッドを更新して、FindUpcomingDinners () 結果から&lt;ディナー&gt; を作成し、ビューテンプレートに渡すことができます。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

次に、\Views\Dinners\Index.aspx view テンプレートを更新して&lt;ViewPage&lt;IEnumerable&lt;ディナー&gt;&gt;ではなく PaginatedList&lt;ディナー&gt;&gt; を継承し、次のコードをビューテンプレートの下部に追加して、次のナビゲーション UI と前のナビゲーション UI を表示または非表示にすることができます。

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

この記事では、Html の Teltelink () ヘルパーメソッドを使用してハイパーリンクを生成する方法について説明します。 このメソッドは、以前に使用した Html.actionlink () ヘルパーメソッドに似ています。 違いは、global.asax ファイル内で設定する "UpcomingDinners" ルーティング規則を使用して URL を生成していることです。 これにより *、次の*形式の Index () アクションメソッドへの url が生成されます。 {Page} の値は、現在の PageIndex に基づいて前に指定した変数です。

アプリケーションをもう一度実行すると、ブラウザーに10のディナーが表示されるようになります。

![](implement-efficient-data-paging/_static/image5.png)

また、ページの下部にある &lt;&lt; と &gt;の &gt;&gt; ナビゲーション UI も &lt;します。これにより、検索エンジンのアクセス可能な Url を使用してデータの転送と逆方向のスキップを行うことができます。

![](implement-efficient-data-paging/_static/image6.png)

| **サイドトピック: IQueryable&lt;T&gt; の影響について** |
| --- |
| IQueryable&lt;T&gt; は、さまざまな興味深い実行シナリオ (ページングやコンポジションベースのクエリなど) を可能にする非常に強力な機能です。 すべての強力な機能と同様に、使用方法について慎重に検討し、悪用されないようにする必要があります。 リポジトリから IQueryable&lt;T&gt; 結果を返すことにより、呼び出し元のコードがチェーン演算子メソッドに追加され、最終的なクエリの実行に参加することを認識することが重要です。 この機能の呼び出しコードを指定しない場合は、既に実行されているクエリの結果を含む IList&lt;T&gt; または IEnumerable&lt;T&gt; 結果を返す必要があります。 改ページのシナリオでは、実際のデータ改ページロジックを、呼び出されるリポジトリメソッドにプッシュする必要があります。 このシナリオでは、FindUpcomingDinners () finder メソッドを更新して、PaginatedList を返したシグネチャを取得することがあります。 PaginatedList&lt; ディナー&gt; FindUpcomingDinners (int pageIndex, int pageSize) {} を返すか、IList&lt;ディナー&gt;を返し、"totalCount" out パラメーターを使用してディナー: IList&lt;ディナー&gt; FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) {} の合計数を返します。 |

### <a name="next-step"></a>次の手順

次に、認証と承認のサポートをアプリケーションに追加する方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](re-use-ui-using-master-pages-and-partials.md)
> [次へ](secure-applications-using-authentication-and-authorization.md)
