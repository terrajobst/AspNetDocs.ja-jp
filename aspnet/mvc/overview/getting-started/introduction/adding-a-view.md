---
title: MVC アプリへのビューの追加
author: Rick-Anderson
description: MVC アプリへのビューの追加
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 4b369028aca1e8a6cace60466b8049ccc02a2ec2
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519064"
---
# <a name="adding-a-view"></a>ビューの追加

[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

このセクションでは、`HelloWorldController` クラスを変更して、ビューテンプレートファイルを使用して、クライアントに HTML 応答を生成するプロセスを完全にカプセル化します。 

[Razor ビューエンジン](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)を使用して、ビューテンプレートファイルを作成します。 Razor ベースのビュー テンプレートが、 *.cshtml*ファイル拡張子、および HTML 出力を C# を使用して作成する洗練された方法を提供します。 Razor では、ビューテンプレートを記述するときに必要な文字数とキーストロークの数が最小限に抑えられ、滑らかなコーディングワークフローが可能になります。

現在、`Index` メソッドは、コントローラー クラスでハード コーディングされるメッセージを含む文字列を返します。 次のコードに示すように、`Index` メソッドを変更して controllers[ビュー](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View)メソッドを呼び出します。

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

上記の `Index` メソッドでは、ビューテンプレートを使用してブラウザーへの HTML 応答を生成します。 上の `Index` メソッドなどのコントローラーメソッド ([アクションメソッド](http://rachelappel.com/asp.net-mvc-actionresults-explained)とも呼ばれます) は、通常、文字列のようなプリミティブ型ではなく、 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (または[actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)から派生したクラス) を返します。

*Views\HelloWorld*フォルダーを右クリックして **[追加]** をクリックし、 **[MVC 5 ビューページ (レイアウト (Razor))]** をクリックします。
  
![](adding-a-view/_static/image1.png)   
  
**[項目の名前の指定]** ダイアログボックスで、「 *Index*」と入力し、 **[OK]** をクリックします。  
  
![](adding-a-view/_static/image2.png)  
  
**[レイアウトページの選択]** ダイアログで、既定の **\_のレイアウト**をそのまま使用し、[ **OK]** をクリックします。  
  
![](adding-a-view/_static/image3.png)  
  
上のダイアログボックスの左側のウィンドウで、 *Views\Shared*フォルダーが選択されています。 カスタムレイアウトファイルが別のフォルダーにある場合は、それを選択できます。 このチュートリアルでは、後でレイアウトファイルについて説明します。

*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルが作成されます。

![](adding-a-view/_static/image4.png)

次の強調表示されたマークアップを追加します。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

*Index. cshtml*ファイルを右クリックし、 **[ブラウザーで表示]** を選択します。

![PI](adding-a-view/_static/image5.png)

また、*インデックスの cshtml*ファイルを右クリックし、 **[Page Inspector で表示]** を選択することもできます。 詳細については、 [Page Inspector チュートリアル](../../views/using-page-inspector-in-aspnet-mvc.md)を参照してください。

または、アプリケーションを実行し、`HelloWorld` コントローラー (`http://localhost:xxxx/HelloWorld`) を参照します。 コントローラーの `Index` メソッドでは、多くの作業が行われませんでした。単にステートメント `return View()`を実行しました。これは、メソッドがビューテンプレートファイルを使用してブラウザーに応答を表示する必要があることを指定します。 使用するビューテンプレートファイルの名前を明示的に指定していないので、ASP.NET MVC では、\Views\HelloWorld フォルダー内のファイルを使用するように既定で設定されてい*ます。* 次の画像は、ビューテンプレートから Hello &quot;文字列を示しています。&quot;、ビューにハードコーディングされています。

![](adding-a-view/_static/image6.png)

すばらしいですね。 ただし、ブラウザーのタイトルバーに "Index-My ASP.NET Application" と表示され、ページの上部にある大きなリンクに "アプリケーション名" と表示されていることに注意してください。 ブラウザーウィンドウのサイズによっては、右上にある3つのバーをクリックして、 **[ホーム]** 、 **[バージョン情報]** 、 **[連絡先**]、 **[登録]** 、 **[ログイン]** のリンクを表示することが必要になる場合があります。

## <a name="changing-views-and-layout-pages"></a>ビューおよびレイアウトページの変更

最初に、ページの上部にある [アプリケーション名の &quot;&quot;] リンクを変更します。 このテキストは、すべてのページに共通です。 実際には、アプリケーション内のすべてのページに表示される場合でも、プロジェクト内の1つの場所にのみ実装されます。 **ソリューションエクスプローラー**の [ */* ]/[共有] フォルダーにアクセスし、 *\_Layout*ファイルを開きます。 このファイルは*レイアウトページ*と呼ばれ、他のすべてのページで使用される共有フォルダーにあります。

![_LayoutCshtml](adding-a-view/_static/image7.png)

レイアウトテンプレートを使用すると、サイトの HTML コンテナーレイアウトを1か所で指定し、サイト内の複数のページに適用できます。 `@RenderBody()` という行を見つけます。 `RenderBody` は、作成したビュー固有のページがすべて表示されるプレースホルダーで、レイアウト ページに&quot;ラップ&quot;されます。 たとえば、 **About**リンクを選択すると、`RenderBody` メソッド内に*Views\Home\About.cshtml*ビューが表示されます。

タイトル要素の内容を変更します。 レイアウトテンプレートの[html.actionlink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx)を &quot;アプリケーション名&quot; から &quot;MVC Movie&quot; に変更し、コントローラーを `Home` から `Movies`に変更します。 完全なレイアウトファイルを次に示します。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

アプリケーションを実行し、[MVC Movie &quot;&quot;] と表示されていることを確認します。 **[About]** リンクをクリックすると、そのページに MVC ムービー&quot;の &quot;が表示されます。 レイアウトテンプレートで変更を1回行って、サイトのすべてのページに新しいタイトルを反映させることができました。

![](adding-a-view/_static/image8.png)

最初に*Views\HelloWorld\Index.cshtml*ファイルを作成したときに、次のコードが含まれていました。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

上記の Razor コードでは、レイアウトページが明示的に設定されています。 *ビュー\\_ViewStart*を調べます。このファイルには、まったく同じ Razor マークアップが含まれています。 *[_ViewStart\\ビュー](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* には、すべてのビューで使用する共通レイアウトが定義されているため、 *Views\HelloWorld\Index.cshtml*ファイルからコメントアウトまたは削除することができます。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

`Layout` プロパティを使用すれば、別のレイアウト ビューを設定することができます。また、`null` に設定して、レイアウト ファイルが使用されないようにすることができます。

次に、インデックスビューのタイトルを変更してみましょう。

*MvcMovie\Views\HelloWorld\Index.cshtml*を開きます。 2つの場所で変更を行うことができます。最初に、ブラウザーのタイトルに表示されるテキスト、2番目のヘッダー (`<h2>` 要素) の順に移動します。 これを少し変えれば、コードのどの部分でアプリのどの部分が変更されるかを確認することができます。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

表示する HTML タイトルを示すために、上記のコードでは `ViewBag` オブジェクトの `Title` プロパティを設定しています (これは、*インデックスの cshtml*ビューテンプレートに含まれています)。 レイアウトテンプレート ( *Views\Shared\\_Layout* ) では、以前に変更した HTML の `<head>` セクションの一部として、`<title>` 要素でこの値が使用されていることに注意してください。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

この `ViewBag` アプローチを使用すると、ビューテンプレートとレイアウトファイルの間で、他のパラメーターを簡単に渡すことができます。

アプリケーションを実行します。 ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください (ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。 ブラウザーで Ctrl キーを押しながら F5 キーを押して、サーバーからの応答を強制的に読み込みます。)ブラウザーのタイトルは、 *Index. cshtml* view テンプレートで設定した `ViewBag.Title` で作成され、追加の &quot;ムービーアプリ&quot; レイアウトファイルに追加されます。

また、*インデックスの cshtml*ビューテンプレートの内容が *\_のレイアウト*にマージされ、1つの HTML 応答がブラウザーに送信されたことにも注目してください。 レイアウト テンプレートを使用すれば、アプリケーションのすべてのページに適用される変更をとても簡単に行うことができます。

![](adding-a-view/_static/image9.png)

ほとんどの &quot;データ&quot; (この場合は、ビューテンプレート!&quot; message から Hello &quot;) がハードコーディングされています。 MVC アプリケーションには &quot;V&quot; (ビュー) があり、&quot;C&quot; (コントローラー) がありますが、&quot;M&quot; (モデル) はまだありません。 ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。

## <a name="passing-data-from-the-controller-to-the-view"></a>コントローラーからビューへのデータの受け渡し

データベースにアクセスしてモデルについて説明する前に、まずコントローラーからビューに情報を渡す方法について説明します。 コントローラークラスは、受信 URL 要求に応答して呼び出されます。 コントローラークラスは、入力方向のブラウザー要求を処理し、データベースからデータを取得し、最終的にブラウザーに返す応答の種類を決定するコードを記述します。 これで、ビューテンプレートをコントローラーから使用して、ブラウザーに HTML 応答を生成して書式設定することができます。

コントローラーは、ビューテンプレートがブラウザーに応答を表示するために必要なすべてのデータまたはオブジェクトを提供する役割を担います。 ベストプラクティス:**ビューテンプレートでは、ビジネスロジックを実行したり、データベースを直接操作したりしないで**ください。 代わりに、ビューテンプレートは、コントローラーによって提供されるデータでのみ機能します。 この &quot;、問題の分離を維持することにより、コードをクリーンで、テストしやすく、保守しやすくなり&quot; ます。

現時点では、`HelloWorldController` クラスの `Welcome` アクションメソッドは `name` と `numTimes` パラメーターを受け取り、ブラウザーに値を直接出力します。 コントローラーがこの応答を文字列として表示するのではなく、ビューテンプレートを使用するようにコントローラーを変更してみましょう。 このビュー テンプレートでは動的応答が生成されます。これは、応答を生成するために、コントローラーからビューに適量のデータを渡す必要があることを意味します。 これを行うには、ビューテンプレートで必要とされる動的データ (パラメーター) をコントローラーに配置し、ビューテンプレートがアクセスできるように `ViewBag` オブジェクト内に表示します。

*HelloWorldController.cs*ファイルに戻り、`Welcome` メソッドを変更して、`ViewBag` オブジェクトに `Message` と `NumTimes` の値を追加します。 `ViewBag` は動的なオブジェクトであるため、任意のものを自由に配置できます。`ViewBag` オブジェクトには、その中に何かを配置するまで、定義されたプロパティはありません。 [ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)は、アドレスバーのクエリ文字列からメソッドのパラメーターに、名前付きパラメーター (`name` と `numTimes`) を自動的にマップします。 完全な *HelloWorldController.cs* ファイルは次のようになります。

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

現在、`ViewBag` オブジェクトには、ビューに自動的に渡されるデータが含まれています。 次に、ウェルカムビューテンプレートが必要です。 **[ビルド]** メニューの **[ソリューションのビルド]** (または Ctrl + Shift + B) を選択して、プロジェクトがコンパイルされていることを確認します。 *Views\HelloWorld*フォルダーを右クリックして **[追加]** をクリックし、 **[MVC 5 ビューページ (レイアウト (Razor))]** をクリックします。
  
![](adding-a-view/_static/image10.png)   
  
**[項目の名前の指定]** ダイアログボックスで、「*ようこそ*」と入力し、 **[OK]** をクリックします。   
  
**[レイアウトページの選択]** ダイアログで、既定の **\_のレイアウト**をそのまま使用し、[ **OK]** をクリックします。  
  
![](adding-a-view/_static/image11.png)   

*MvcMovie\Views\HelloWorld\Welcome.cshtml*ファイルが作成されます。

*Welcome*ファイル内のマークアップを置き換えます。 ユーザーが指定した回数だけ &quot;Hello&quot; というループを作成します。 次に、完全な*Welcome*ファイルを示します。

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

アプリケーションを実行し、次の URL を参照します。

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

これで、データは URL から取得され、[モデルバインダー](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)を使用してコントローラーに渡されます。 コントローラーは、データを `ViewBag` オブジェクトにパッケージ化し、そのオブジェクトをビューに渡します。 ビューには、データが HTML としてユーザーに表示されます。

![](adding-a-view/_static/image12.png)

上記のサンプルでは、`ViewBag` オブジェクトを使用して、コントローラーからビューにデータを渡しています。 チュートリアルの後半で、ビュー モデルを使用して、コントローラーからビューにデータを渡します。 データを渡すビューモデルのアプローチは、一般にビューバッグアプローチよりもはるかに優先されます。 詳細については、「 [Dynamic V 厳密に型指定](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)されたビュー」のブログエントリを参照してください。 

これは、モデルの &quot;M&quot; ですが、データベースの種類ではありませんでした。 学習したことを確認し、ムービーのデータベースを作成してみましょう。

> [!div class="step-by-step"]
> [前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)
