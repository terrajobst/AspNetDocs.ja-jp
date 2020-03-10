---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: ビューを追加する |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485368"
---
# <a name="adding-a-view"></a>ビューの追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

このセクションでは、`HelloWorldController` クラスを変更して、ビューテンプレートファイルを使用して、クライアントに HTML 応答を生成するプロセスを完全にカプセル化します。

ASP.NET MVC 3 で導入された[Razor ビューエンジン](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)を使用して、ビューテンプレートファイルを作成します。 Razor ベースのビューテンプレートには、ファイル拡張子が*cshtml*と、を使用してC#HTML 出力を作成するための洗練された方法が用意されています。 Razor では、ビューテンプレートを記述するときに必要な文字数とキーストロークの数が最小限に抑えられ、滑らかなコーディングワークフローが可能になります。

現在、`Index` メソッドは、コントローラー クラスでハード コーディングされるメッセージを含む文字列を返します。 次のコードに示すように、`View` オブジェクトを返すように `Index` メソッドを変更します。

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

上記の `Index` メソッドでは、ビューテンプレートを使用してブラウザーへの HTML 応答を生成します。 上の `Index` メソッドなどのコントローラーメソッド ([アクションメソッド](http://rachelappel.com/asp.net-mvc-actionresults-explained)とも呼ばれます) は、通常、文字列のようなプリミティブ型ではなく、 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (または[actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)から派生したクラス) を返します。

プロジェクトで、`Index` メソッドで使用できるビューテンプレートを追加します。 これを行うには、`Index` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。

![](adding-a-view/_static/image1.png)

**[ビューの追加]** ダイアログボックスが表示されます。 既定値のままにして、 **[追加]** ボタンをクリックします。

![](adding-a-view/_static/image2.png)

*MvcMovie\Views\HelloWorld*フォルダーと*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルが作成されます。 **ソリューションエクスプローラー**で確認できます。

![](adding-a-view/_static/image3.png)

作成された*インデックスの cshtml*ファイルを次に示します。

![HelloWorldIndex](adding-a-view/_static/image4.png)

`<h2>` タグの下に次の HTML を追加します。

[!code-html[Main](adding-a-view/samples/sample2.html)]

完全な*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルを次に示します。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

Visual Studio 2012 を使用している場合は、ソリューションエクスプローラーで、 *Index. cshtml*ファイルを右クリックし、 **[Page Inspector で表示]** を選択します。

![PI](adding-a-view/_static/image5.png)

この新しいツールの詳細については、 [Page Inspector チュートリアル](../../views/using-page-inspector-in-aspnet-mvc.md)を参照してください。

または、アプリケーションを実行し、`HelloWorld` コントローラー (`http://localhost:xxxx/HelloWorld`) を参照します。 コントローラーの `Index` メソッドでは、多くの作業が行われませんでした。単にステートメント `return View()`を実行しました。これは、メソッドがビューテンプレートファイルを使用してブラウザーに応答を表示する必要があることを指定します。 使用するビューテンプレートファイルの名前を明示的に指定していないので、ASP.NET MVC では、\Views\HelloWorld フォルダー内のファイルを使用するように既定で設定されてい*ます。* 次の画像は、ビューテンプレートから Hello &quot;文字列を示しています。&quot;、ビューにハードコーディングされています。

![](adding-a-view/_static/image6.png)

すばらしいですね。 ただし、ブラウザーのタイトルバーに &quot;Index My ASP.NET A&quot; が表示され、ページの上部にある大きなリンクには、ここでロゴの &quot;が示されています。ロゴ &quot;の下に&quot; ます。&quot; リンクは [登録] リンクと [ログイン] リンクです。 [ホーム]、[About]、[Contact] ページにリンクしています。 これらのいくつかを変更してみましょう。

## <a name="changing-views-and-layout-pages"></a>ビューおよびレイアウトページの変更

まず、ロゴ &quot;をここで変更します。ページの上部にあるタイトルを&quot; ます。 このテキストは、すべてのページに共通です。 実際には、アプリケーション内のすべてのページに表示される場合でも、プロジェクト内の1つの場所にのみ実装されます。 **ソリューションエクスプローラー**の [ */* ]/[共有] フォルダーにアクセスし、 *\_Layout*ファイルを開きます。 このファイルは*レイアウトページ*と呼ばれ、他のすべてのページで使用される共有 &quot;シェル&quot; です。

![_LayoutCshtml](adding-a-view/_static/image7.png)

レイアウトテンプレートを使用すると、サイトの HTML コンテナーレイアウトを1か所で指定し、サイト内の複数のページに適用できます。 `@RenderBody()` という行を見つけます。 `RenderBody` は、作成したビュー固有のページがすべて表示されるプレースホルダーで、レイアウト ページに&quot;ラップ&quot;されます。 たとえば、About リンクを選択すると、`RenderBody` メソッド内に*Views\Home\About.cshtml*ビューが表示されます。

レイアウト テンプレートの サイトタイトル 見出しは、ここにあるロゴ &quot;から、MVC Movie&quot;&quot;&quot; に変更します。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Title 要素の内容を次のマークアップに置き換えます。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

アプリケーションを実行し、[MVC Movie &quot;&quot;] と表示されていることを確認します。 **[About]** リンクをクリックすると、そのページに MVC ムービー&quot;の &quot;が表示されます。 レイアウトテンプレートで変更を1回行って、サイトのすべてのページに新しいタイトルを反映させることができました。

![](adding-a-view/_static/image8.png)

次に、インデックスビューのタイトルを変更してみましょう。

*MvcMovie\Views\HelloWorld\Index.cshtml*を開きます。 2つの場所で変更を行うことができます。最初に、ブラウザーのタイトルに表示されるテキスト、2番目のヘッダー (`<h2>` 要素) の順に移動します。 これを少し変えれば、コードのどの部分でアプリのどの部分が変更されるかを確認することができます。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

表示する HTML タイトルを示すために、上記のコードでは `ViewBag` オブジェクトの `Title` プロパティを設定しています (これは、*インデックスの cshtml*ビューテンプレートに含まれています)。 レイアウトテンプレートのソースコードを確認すると、テンプレートは、以前に変更した HTML の `<head>` セクションの一部として、`<title>` 要素内のこの値を使用していることがわかります。 この `ViewBag` アプローチを使用すると、ビューテンプレートとレイアウトファイルの間で、他のパラメーターを簡単に渡すことができます。

アプリケーションを実行し、`http://localhost:xx/HelloWorld`を参照します。 ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください (ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。 ブラウザーで Ctrl キーを押しながら F5 キーを押して、サーバーからの応答を強制的に読み込みます。)ブラウザーのタイトルは、 *Index. cshtml* view テンプレートで設定した `ViewBag.Title` で作成され、追加の &quot;ムービーアプリ&quot; レイアウトファイルに追加されます。

また、*インデックスの cshtml*ビューテンプレートの内容が *\_のレイアウト*にマージされ、1つの HTML 応答がブラウザーに送信されたことにも注目してください。 レイアウト テンプレートを使用すれば、アプリケーションのすべてのページに適用される変更をとても簡単に行うことができます。

![](adding-a-view/_static/image9.png)

ほとんどの &quot;データ&quot; (この場合は、ビューテンプレート!&quot; message から Hello &quot;) がハードコーディングされています。 MVC アプリケーションには &quot;V&quot; (ビュー) があり、&quot;C&quot; (コントローラー) がありますが、&quot;M&quot; (モデル) はまだありません。 ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。

## <a name="passing-data-from-the-controller-to-the-view"></a>コントローラーからビューへのデータの受け渡し

データベースにアクセスしてモデルについて説明する前に、まずコントローラーからビューに情報を渡す方法について説明します。 コントローラークラスは、受信 URL 要求に応答して呼び出されます。 コントローラークラスは、入力方向のブラウザー要求を処理し、データベースからデータを取得し、最終的にブラウザーに返す応答の種類を決定するコードを記述します。 これで、ビューテンプレートをコントローラーから使用して、ブラウザーに HTML 応答を生成して書式設定することができます。

コントローラーは、ビューテンプレートがブラウザーに応答を表示するために必要なすべてのデータまたはオブジェクトを提供する役割を担います。 ベストプラクティス:**ビューテンプレートでは、ビジネスロジックを実行したり、データベースを直接操作したりしないで**ください。 代わりに、ビューテンプレートは、コントローラーによって提供されるデータでのみ機能します。 この &quot;、問題の分離を維持することにより、コードをクリーンで、テストしやすく、保守しやすくなり&quot; ます。

現時点では、`HelloWorldController` クラスの `Welcome` アクションメソッドは `name` と `numTimes` パラメーターを受け取り、ブラウザーに値を直接出力します。 コントローラーがこの応答を文字列として表示するのではなく、ビューテンプレートを使用するようにコントローラーを変更してみましょう。 このビュー テンプレートでは動的応答が生成されます。これは、応答を生成するために、コントローラーからビューに適量のデータを渡す必要があることを意味します。 これを行うには、ビューテンプレートで必要とされる動的データ (パラメーター) をコントローラーに配置し、ビューテンプレートがアクセスできるように `ViewBag` オブジェクト内に表示します。

*HelloWorldController.cs*ファイルに戻り、`Welcome` メソッドを変更して、`ViewBag` オブジェクトに `Message` と `NumTimes` の値を追加します。 `ViewBag` は動的なオブジェクトであるため、任意のものを自由に配置できます。`ViewBag` オブジェクトには、その中に何かを配置するまで、定義されたプロパティはありません。 [ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)は、アドレスバーのクエリ文字列からメソッドのパラメーターに、名前付きパラメーター (`name` と `numTimes`) を自動的にマップします。 完全な *HelloWorldController.cs* ファイルは次のようになります。

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

現在、`ViewBag` オブジェクトには、ビューに自動的に渡されるデータが含まれています。

次に、ウェルカムビューテンプレートが必要です。 **[ビルド]** メニューの **[Mvcmovie のビルド]** を選択して、プロジェクトがコンパイルされていることを確認します。

次に、`Welcome` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。

![](adding-a-view/_static/image10.png)

**[ビューの追加]** ダイアログボックスは次のようになります。

![](adding-a-view/_static/image11.png)

**[追加]** をクリックし、新しい*Welcome. cshtml*ファイルの `<h2>` 要素の下に次のコードを追加します。 ユーザーが指定した回数だけ &quot;Hello&quot; というループを作成します。 次に、完全な*Welcome*ファイルを示します。

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

アプリケーションを実行し、次の URL を参照します。

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

これで、データは URL から取得され、[モデルバインダー](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)を使用してコントローラーに渡されます。 コントローラーは、データを `ViewBag` オブジェクトにパッケージ化し、そのオブジェクトをビューに渡します。 ビューには、データが HTML としてユーザーに表示されます。

![](adding-a-view/_static/image12.png)

上記のサンプルでは、`ViewBag` オブジェクトを使用して、コントローラーからビューにデータを渡しています。 チュートリアルの後半では、ビューモデルを使用して、コントローラーからビューにデータを渡します。 データを渡すビューモデルのアプローチは、一般にビューバッグアプローチよりもはるかに優先されます。 詳細については、「 [Dynamic V 厳密に型指定](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)されたビュー」のブログエントリを参照してください。

これは、モデルの &quot;M&quot; ですが、データベースの種類ではありませんでした。 学習したことを確認し、ムービーのデータベースを作成してみましょう。

> [!div class="step-by-step"]
> [前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)
