---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: コントローラーとビューを使用して、リスティング/Details UI を実装します。Microsoft Docs
author: microsoft
description: 手順 4. では、モデルを利用してアプリケーションにコントローラーを追加し、ユーザーにデータリスト/詳細ナビゲーションエクスペリエンスを提供する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486220"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>コントローラーとビューを使用し、リスティング/詳細 UI を実装する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順4です。
> 
> 手順 4. では、モデルを利用してアプリケーションにコントローラーを追加し、ユーザーにディナーのデータリスト/詳細ナビゲーションエクスペリエンスを提供する方法を示します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-4-controllers-and-views"></a>ステップ 4: コントローラーとビューの操作

従来の web フレームワーク (classic ASP、PHP、ASP.NET Web Forms など) では、通常、着信 Url はディスク上のファイルにマップされます。 たとえば、"/-.Aspx" や "/" などの URL の要求は、"Products" ファイルまたは "Products. php" ファイルによって処理される場合があります。

Web ベースの MVC フレームワークでは、Url が少し異なる方法でサーバーコードにマップされます。 受信 Url をファイルにマッピングする代わりに、代わりに、Url をクラスのメソッドにマップします。 これらのクラスは "コントローラー" と呼ばれ、受信 HTTP 要求の処理、ユーザー入力の処理、データの取得と保存、クライアントに返信するための応答の決定 (HTML の表示、ファイルのダウンロード、別のファイルへのリダイレクトなど) を担当します。URL など)。

私たちは、このアプリケーションの基本的なモデルを構築したので、次のステップとして、アプリケーションにコントローラーを追加して、ユーザーにサイトのディナーのデータリスト/詳細ナビゲーションエクスペリエンスを提供します。

### <a name="adding-a-dinnerscontroller-controller"></a>Dinのコントローラーコントローラーの追加

まず、web プロジェクト内の "Controllers" フォルダーを右クリックし、[ **&gt;コントローラー** ] メニューコマンドを選択します (このコマンドは、Ctrl + M キー、Ctrl + C キーを押して実行することもできます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

これにより、[コントローラーの追加] ダイアログボックスが表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

新しいコントローラーに "Din" という名前を指定し、[追加] ボタンをクリックします。 次に、DinnersController.cs ファイルが \ Controllers ディレクトリに追加されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

また、コードエディター内で新しい Dinのコントローラークラスも開きます。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Index () アクションメソッドと Details () アクションメソッドを Dinのコントローラークラスに追加する

アプリケーションを使用している訪問者が、今後のディナーの一覧を参照し、リスト内のディナーをクリックして、その詳細を確認できるようにしたいと考えています。 これを行うには、アプリケーションから次の Url を発行します。

| **[URL]** | **目的** |
| --- | --- |
| *ディナー* | 今後のディナーの HTML リストを表示する |
| *///[Id]* | URL 内に埋め込まれている "id" パラメーターによって示される特定のディナーに関する詳細を表示します。これは、データベース内の夕食の Dinid と一致します。 たとえば、次の例では、Dinid 値が2であるディナーに関する詳細を含む HTML ページが表示されます。 |

これらの Url の初期実装は、次のような2つのパブリック "アクションメソッド" を Dinのコントローラークラスに追加することによって発行されます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

次に、このアプリケーションを実行し、ブラウザーを使用して呼び出します。 *"/Din" と*いう URL を入力すると、 *Index ()* メソッドが実行され、次の応答が返されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

*"/Din/詳細/月"* の URL を入力すると、 *Details ()* メソッドが実行され、次の応答が返されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

ASP.NET MVC では、Dinのコントローラークラスを作成し、それらのメソッドを呼び出す方法について疑問に思うかもしれません。 ここでは、ルーティングのしくみについて簡単に見ていきましょう。

### <a name="understanding-aspnet-mvc-routing"></a>ASP.NET MVC ルーティングについて

ASP.NET MVC には、Url をコントローラークラスにマップする方法を柔軟に制御できる強力な URL ルーティングエンジンが用意されています。 これにより、ASP.NET MVC では、作成するコントローラークラスをどのように選択するか、どの方法を呼び出すか、また、変数が URL/Querystring から自動的に解析され、パラメーター引数としてメソッドに渡されるさまざまな方法を構成することができます。 また、SEO (検索エンジンの最適化) のためにサイトを完全に最適化し、必要な URL 構造をアプリケーションから発行できる柔軟性を備えています。

既定では、新しい ASP.NET MVC プロジェクトには、既に登録済みの URL ルーティングルールのセットが付属しています。 これにより、何も明示的に構成することなく、簡単にアプリケーションを開始できます。 既定のルーティング規則の登録は、プロジェクトの "Application" クラス内にあります。これは、プロジェクトのルートにある "global.asax" ファイルをダブルクリックして開くことができます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

既定の ASP.NET MVC ルーティング規則は、このクラスの "RegisterRoutes" メソッド内に登録されます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"ルート。MapRoute () "上記のメソッド呼び出しは、次の URL 形式を使用して、受信 Url をコントローラークラスにマップする既定のルーティング規則を登録します。"/{"コントローラー" は、インスタンス化するコントローラークラスの名前、"action" はそれに対して呼び出すパブリックメソッドの名前、"id" は、引数としてメソッドに渡すことができる URL 内に埋め込まれた省略可能なパラメーターである/{/} "MapRoute ()" メソッド呼び出しに渡される3番目のパラメーターは、URL (Controller = "Home"、Action = "Index"、Id = "") に存在しない場合に、コントローラー/アクション/id 値に使用する既定値のセットです。

次の表は、既定の "<em>/{controllers}/{action}/{id}"</em>ルート規則を使用してさまざまな url がどのようにマップされるかを示しています。

| **[URL]** | **コントローラークラス** | **アクションメソッド** | **渡されたパラメーター** |
| --- | --- | --- | --- |
| */月/月* | DinnersController | 詳細 (id) | id=2 |
| *//編集/5* | DinnersController | 編集 (id) | id=5 |
| */Din* | DinnersController | Create() | 該当なし |
| */Dinners* | DinnersController | Index () | 該当なし |
| */Home* | HomeController | Index () | 該当なし |
| */* | HomeController | Index () | 該当なし |

最後の3行は、使用されている既定値 (Controller = Home、Action = Index、Id = "") を示しています。 "Index" メソッドが指定されていない場合は、既定のアクション名として登録されるため、"/Dinners" と "/Home" の Url によって、コントローラークラスで Index () アクションメソッドが呼び出されます。 "Home" コントローラーが指定されていない場合、"Home" コントローラーは既定のコントローラーとして登録されるため、"/" URL によって HomeController が作成され、Index () アクションメソッドが呼び出されます。

これらの既定の URL ルーティングルールが気に入らない場合は、簡単に変更できます。上記の RegisterRoutes メソッド内で編集するだけです。 ただし、このアプリケーションでは、既定の URL ルーティングルールを変更することはありません。代わりにそのまま使用します。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>Dinのコントローラーからの Dinレポジトリの使用

ここでは、Dinの現在の実装である、() および Details () アクションメソッドを、モデルを使用する実装に置き換えます。

以前に構築した Dinのリポジトリクラスを使用して、動作を実装します。 まず、"using" ステートメントを追加し、"" を "使用" します。次に、"the" という名前空間を参照する "using" ステートメントを追加し、dinをコントローラークラスのフィールドとして、そのインスタンスを宣言します。

この章の後半では、"依存関係の挿入" の概念を紹介します。また、コントローラーが単体テストを有効にする Dinのリポジトリへの参照を取得するもう1つの方法を示しますが、ここでは、Dinレポジトリのインスタンスを作成するだけです。次のようにインライン化します。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

これで、取得したデータモデルオブジェクトを使用して HTML 応答を返す準備ができました。

### <a name="using-views-with-our-controller"></a>コントローラーでのビューの使用

HTML をアセンブルするためのアクションメソッド内にコードを記述し、それをクライアントに送信するために*Response ()* ヘルパーメソッドを使用することは可能ですが、この方法は非常に扱いにくくなります。 はるかに優れたアプローチは、アプリケーションとデータロジックを Dincontroller のアクションメソッド内でのみ実行し、html 応答のレンダリングに必要なデータを、HTML 表現の出力を行う別の "view" テンプレートに渡すことです。このようになります。 すぐにわかるように、"view" テンプレートは、通常、HTML マークアップと埋め込みのレンダリングコードの組み合わせを含むテキストファイルです。

ビューレンダリングからコントローラーロジックを分離すると、いくつかの大きな利点が得られます。 特に、アプリケーションコードと UI 書式設定/レンダリングコードの間で、明確な "問題の分離" を適用するのに役立ちます。 これにより、UI レンダリングロジックから分離されたアプリケーションロジックの単体テストがはるかに簡単になります。 これにより、アプリケーションコードを変更することなく、UI レンダリングテンプレートを後で簡単に変更できるようになります。 また、開発者やデザイナーがプロジェクトで共同作業を簡単に行えるようになります。

Dinの Scontroller クラスを更新して、ビューテンプレートを使用して、2つのアクションメソッドの戻り値の型を "void" にして、代わりに戻り値の型が "ActionResult" になるようにすることで、HTML UI の応答を返信するように指定できます。 次のように、コントローラーの基本クラスで*View ()* ヘルパーメソッドを呼び出して、"viewresult" オブジェクトを返すことができます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

上記で使用している*View ()* ヘルパーメソッドのシグネチャは次のようになります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View ()* ヘルパーメソッドの最初のパラメーターは、HTML 応答を表示するために使用するビューテンプレートファイルの名前です。 2番目のパラメーターは、ビューテンプレートが HTML 応答を表示するために必要なデータを含むモデルオブジェクトです。

Index () アクションメソッドでは、 *view ()* ヘルパーメソッドを呼び出し、"index" ビューテンプレートを使用してディナーの HTML リストを表示することを示しています。 ここでは、リストを生成するディナーオブジェクトのシーケンスをビューテンプレートに渡しています。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

詳細 () アクションメソッド内で、URL 内で指定された id を使用してディナーオブジェクトを取得しようとしています。 有効なディナーが見つかった場合は、 *view ()* ヘルパーメソッドを呼び出します。これは、取得したディナーオブジェクトを表示するために "Details" ビューテンプレートを使用することを示します。 無効なディナーが要求された場合は、"NotFound" ビューテンプレート (および、テンプレート名を受け取る*ビュー ()* ヘルパーメソッドのオーバーロードされたバージョン) を使用してディナーが存在しないことを示す役立つエラーメッセージが表示されます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

ここで、"NotFound"、"Details"、"Index" の各ビューテンプレートを実装しましょう。

### <a name="implementing-the-notfound-view-template"></a>"NotFound" ビューテンプレートの実装

まず、"NotFound" ビューテンプレートを実装します。これにより、要求されたディナーが見つからないことを示すわかりやすいエラーメッセージが表示されます。

コントローラーアクションメソッド内にテキストカーソルを配置し、右クリックして [ビューの追加] メニューコマンドを選択することによって、新しいビューテンプレートを作成します (Ctrl + M、Ctrl + V キーを押して、このコマンドを実行することもできます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

これにより、次のような [ビューの追加] ダイアログが表示されます。 既定では、ダイアログが起動されたときのアクションメソッド (この場合は "Details") の名前と一致するように、作成するビューの名前が事前に設定されます。 最初に "NotFound" テンプレートを実装するので、このビュー名をオーバーライドし、代わりに "NotFound" に設定します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "NotFound" ビューテンプレートを作成します (ディレクトリがまだ存在しない場合にも作成されます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

また、コードエディター内で新しい "NotFound" ビューテンプレートが開きます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

既定では、ビューテンプレートには、コンテンツとコードを追加できる2つの "コンテンツ領域" があります。 1つ目の方法では、返信した HTML ページの "タイトル" をカスタマイズできます。 2つ目の方法では、返信した HTML ページの "メインコンテンツ" をカスタマイズできます。

"NotFound" ビューテンプレートを実装するには、いくつかの基本的なコンテンツを追加します。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

その後、ブラウザー内で試してみることができます。 これを行うには、 *"/Din/9999"* の URL を要求します。 これは、データベースに現在存在していないディナーを指し、"NotFound" ビューテンプレートをレンダリングするために、Din() アクションメソッドによって表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

上のスクリーンショットでは、基本的なビューテンプレートによって、画面上のメインコンテンツを囲む HTML がいくつか継承されていることがわかります。 これは、ビューテンプレートが "マスターページ" テンプレートを使用しているためです。これにより、サイト上のすべてのビューで一貫したレイアウトを適用できるようになります。 このチュートリアルの後半では、マスターページがどのように機能するかについて説明します。

### <a name="implementing-the-details-view-template"></a>"Details" ビューテンプレートの実装

ここで、"Details" ビューテンプレートを実装します。これにより、単一のディナーモデルの HTML が生成されます。

これを行うには、詳細アクションメソッド内にテキストカーソルを配置し、右クリックして [ビューの追加] メニューコマンドを選択します (または、Ctrl + M キー、Ctrl キーを押しながら V キーを押します)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

[ビューの追加] ダイアログが表示されます。 既定のビュー名 ("Details") はそのままにします。 また、ダイアログの [厳密に型指定されたビューを作成する] チェックボックスをオンにし、コントローラーからビューに渡すモデルの種類の名前を選択します (コンボボックスのドロップダウンリストを使用します)。 このビューでは、ディナーオブジェクトを渡しています (この型の完全修飾名は次のとおりです。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

"空のビュー" の作成を選択した前のテンプレートとは異なり、今回は "詳細" テンプレートを使用してビューを自動的に "スキャフォールディング" することを選択します。 これを示すには、上のダイアログボックスの [コンテンツの表示] ドロップダウンを変更します。

"スキャフォールディング" は、渡されるディナーオブジェクトに基づいて、詳細ビューテンプレートの初期実装を生成します。 これにより、ビューテンプレートの実装を簡単に開始できるようになります。

[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Details" ビューテンプレートファイルが作成されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

また、コードエディター内で新しい "Details" ビューテンプレートが開きます。 これには、ディナーモデルに基づく詳細ビューの初期スキャフォールディング実装が含まれます。 スキャフォールディングエンジンは、.NET リフレクションを使用して、渡されたクラスで公開されているパブリックプロパティを確認し、見つかった各型に基づいて適切なコンテンツを追加します。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

*"/Dinners/Details/1"* という URL を要求して、ブラウザーでのこの "詳細" スキャフォールディング実装の外観を確認できます。 この URL を使用すると、最初にデータベースを作成したときにデータベースに手動で追加したディナーの1つが表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

これにより、すぐに稼働が開始され、詳細な .aspx ビューの初期実装が提供されます。 それを調整して、UI を満足できるようにカスタマイズすることができます。

詳細 .aspx テンプレートについて詳しく説明すると、静的な HTML と埋め込みの描画コードが含まれていることがわかります。 &lt;%%&gt; コードナゲットはビューテンプレートのレンダリング時にコードを実行し、&lt;% =%&gt; コードナゲットに含まれるコードを実行し、その結果をテンプレートの出力ストリームにレンダリングします。

このビューには、厳密に型指定された "モデル" プロパティを使用してコントローラーから渡された "ディナー" モデルオブジェクトにアクセスするコードを記述できます。 Visual Studio には、エディター内でこの "モデル" プロパティにアクセスするときに完全なコード intellisense が用意されています。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

最終的な詳細ビューテンプレートのソースが次のようになるように、いくつかの調整を行いましょう。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

*"/Dinners/Details/1"* URL にもう一度アクセスすると、次のように表示されるようになります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>"Index" ビューテンプレートの実装

"Index" ビューテンプレートを実装しましょう。これにより、今後のディナーの一覧が生成されます。 これを行うには、Index アクションメソッド内にテキストカーソルを置き、右クリックして [ビューの追加] メニューコマンドを選択します (または、Ctrl + M キー、Ctrl キーを押しながら V キーを押します)。

[ビューの追加] ダイアログボックスで、"Index" という名前のビューテンプレートを保持し、[厳密に型指定されたビューを作成する] チェックボックスをオンにします。 今回は、"リスト" ビューテンプレートを自動的に生成し、ビューに渡されるモデルの種類として "スキャフォールディング" を選択します。これは、"リスト" を作成すると、[ビューの追加] ダイアログでは次のようになります。コントローラーからビューにディナーオブジェクトのシーケンスを渡します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Index" ビューテンプレートファイルが作成されます。 ビューに渡すディナーの HTML テーブルリストを提供する、その内部の初期実装を "スキャフォールディング" します。

アプリケーションを実行して *"* ディナー" の URL にアクセスすると、次のような一覧が表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上のテーブルソリューションでは、ディナーデータのグリッド形式のレイアウトが提供されています。これは、お客様に向けたディナーのリストについてはあまり必要ではありません。 次のコードを使用して、インデックスの .aspx ビューテンプレートを更新し、それを変更してデータの列数を減らすことができます。また、&lt;ul&gt; 要素を使用して、テーブルではなくレンダリングします。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

上記の foreach ステートメントでは、モデルの各ディナーをループ処理する "var" キーワードを使用しています。 3\.0 にC#精通している方は、"var" を使用すると、ディナーオブジェクトが遅延バインディングされることを意味します。 代わりに、コンパイラが厳密に型指定された "Model" プロパティ ("IEnumerable&lt;ディナー&gt;") に対して型の推論を使用し、ローカルの "ディナー" 変数をディナー型としてコンパイルしていることを意味します。これは、intellisense を完全に取得し、コードブロック内でコンパイル時にチェックします。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

ブラウザーで */Dinners* URL の更新にヒットすると、更新されたビューは次のようになります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

この方が優れていますが、まだ完全ではありません。 最後の手順は、エンドユーザーがリスト内の個々のディナーをクリックして、その詳細を確認できるようにすることです。 これを実装するには、Dinのコントローラーの Details アクションメソッドにリンクする HTML ハイパーリンク要素をレンダリングします。

これらのハイパーリンクは、次の2つの方法のいずれかで、インデックスビュー内に生成できます。 1つ目は、次のような&gt; の要素 &lt;HTML を手動で作成することです。ここでは、&lt;%%&gt; ブロックを &lt;HTML 要素&gt; に埋め込みます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

別の方法として、ASP.NET MVC 内で組み込みの "Html.actionlink ()" ヘルパーメソッドを利用して、プログラムによって、コントローラー上の別のアクションメソッドにリンクする HTML &lt;&gt; 要素を作成することができます。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html の最初のパラメーター。 Html.actionlink () ヘルパーメソッドは、表示するリンクテキスト (この場合はディナーのタイトル)、2番目のパラメーターはリンクを生成するコントローラーアクション名 (この場合は詳細メソッド)、3番目のパラメーターはアクションに送信するパラメーターのセットです (プロパティ名/値を持つ匿名型として実装されます)。 この例では、リンク先のディナーの "id" パラメーターを指定しています。また、ASP.NET MVC の既定の URL ルーティングルールは "{Controller}/{action}/{Html.actionlink () ヘルパーメソッドによって次の出力が生成されます。

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

この例では、Html.actionlink () ヘルパーメソッドを使用して、リスト内の各ディナーを適切な詳細 URL にリンクします。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

*/Dinners*の URL にヒットすると、ディナーリストは次のようになります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

一覧でディナーのいずれかをクリックすると、その詳細が表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>規則ベースの名前付けおよび \ ビューのディレクトリ構造

既定では、ASP.NET MVC アプリケーションは、ビューテンプレートを解決するときに、規則ベースのディレクトリ名前付け構造を使用します。 これにより、開発者は、コントローラークラス内からビューを参照するときに、ロケーションパスを完全修飾する必要がなくなります。 既定では、ASP.NET MVC は、アプリケーションの下にある * \ Views\[ControllerName]\* ディレクトリ内のビューテンプレートファイルを検索します。

たとえば、"Index"、"Details"、"NotFound" という3つのビューテンプレートを明示的に参照する、Din: Controller クラスに取り組んでいます。 既定では、ASP.NET MVC は、アプリケーションのルートディレクトリの下にある *\Views\Dinners*ディレクトリ内でこれらのビューを検索します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

プロジェクト内に現在3つのコントローラークラスがあることに注目してください (HomeController と AccountController –プロジェクトの作成時に既定で最後の2つが追加されています)。サブディレクトリは3つあります (コントローラー) を参照してください。

ホームコントローラーとアカウントコントローラーから参照されているビューは、それぞれの *\Views\Home*ディレクトリと *\Views\Account*ディレクトリから、ビューテンプレートを自動的に解決します。 *ある \views\shared*サブディレクトリは、アプリケーション内の複数のコントローラー間で再利用されるビューテンプレートを格納するための方法を提供します。 ASP.NET MVC は、ビューテンプレートを解決しようとすると、最初に *\ Views\[Controller]* 特定のディレクトリ内をチェックし、ビューテンプレートが見つからない場合は*ある \views\shared*ディレクトリ内で確認します。

個々のビューテンプレートに名前を付ける場合は、ビューテンプレートでレンダリングの原因となったアクションメソッドと同じ名前を共有することをお勧めします。 たとえば、"Index" アクションメソッドの上では、"Index" ビューを使用してビューの結果を表示し、"Details" アクションメソッドは "Details" ビューを使用して結果を表示しています。 これにより、各アクションに関連付けられているテンプレートを簡単に確認できます。

ビューテンプレートの名前がコントローラーで呼び出されているアクションメソッドと同じである場合、開発者はビューテンプレート名を明示的に指定する必要はありません。 代わりに、モデルオブジェクトを "View ()" ヘルパーメソッドに渡すだけで (ビュー名を指定する必要はありません)、ASP.NET MVC は *\[ControllerName を\[* 使用してディスク上に ActionName] ビューテンプレートをレンダリングすることを自動的に推測します。

これにより、コントローラーコードを少しクリーンアップし、コードで名前を2回複製することを回避できます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

上記のコードは、サイトのディナーリスト/詳細エクスペリエンスを実装するために必要なすべてのものです。

#### <a name="next-step"></a>次の手順

これで、ディナーブラウズエクスペリエンスが作成されました。

CRUD (作成、読み取り、更新、削除) データフォーム編集サポートを有効にしましょう。

> [!div class="step-by-step"]
> [前へ](build-a-model-with-business-rule-validations.md)
> [次へ](provide-crud-create-read-update-delete-data-form-entry-support.md)
