---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: ビューの追加 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434518"
---
# <a name="adding-a-view-vb"></a>ビューの追加 (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 必要に応じC#て[ C# ](../cs/adding-a-view.md) 、このチュートリアルのバージョンに切り替えます。

このセクションでは、`HelloWorldController` クラスを変更して、ビューテンプレートファイルを使用して、クライアントに HTML 応答を生成するプロセスを完全にカプセル化します。

まず、ビューテンプレートと、`HelloWorldController` クラスの `Index` メソッドを使用します。 現在、`Index` メソッドは、コントローラークラス内でハードコーディングされたメッセージを含む文字列を返します。 次に示すように、`View` オブジェクトを返すように `Index` メソッドを変更します。

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

ここで、`Index` メソッドを使用して呼び出すことができるビューテンプレートをプロジェクトに追加しましょう。 これを行うには、`Index` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

**[ビューの追加]** ダイアログボックスが表示されます。 既定のエントリをそのまま使用し、 **[追加]** ボタンをクリックします。

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

*MvcMovie\Views\HelloWorld*フォルダーと*MvcMovie\Views\HelloWorld\Index.vbhtml*ファイルが作成されます。 **ソリューションエクスプローラー**で確認できます。

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

`<h2>` タグの下に HTML を追加します。 変更した*MvcMovie\Views\HelloWorld\Index.vbhtml*ファイルを次に示します。

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

アプリケーションを実行し、&quot;hello world&quot; controller (`http://localhost:xxxx/HelloWorld`) に移動します。 コントローラーの `Index` メソッドでは、多くの作業が行われませんでした。単にステートメント `return View()`を実行しました。これは、ビューテンプレートファイルを使用してクライアントに応答を表示するように指定したことを示しています。 使用するビューテンプレートファイルの名前を明示的に指定しなかったため、 *\Views\HelloWorld*フォルダー内の ASP.NET*ビューファイル*を使用するように既定で設定されています。 次の画像は、ビューにハードコーディングされた文字列を示しています。

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

すばらしいですね。 ただし、ブラウザーのタイトルバーに &quot;インデックス&quot; と表示され、ページ上のタイトルに [My MVC Application &quot;] と表示されていることに注意してください。&quot; 変更しましょう。

## <a name="changing-views-and-layout-pages"></a>ビューとレイアウト ページの変更

まず、MVC アプリケーション &quot;テキストを変更してみましょう。テキストが共有され、すべてのページに表示される&quot; ます。 アプリケーション内のすべてのページにある場合でも、実際にはプロジェクト内の1つの場所にのみ表示されます。 **ソリューションエクスプローラー**の [ */* ]/[共有] フォルダーにアクセスし、 *\_Layout*ファイルを開きます。 このファイルはレイアウトページと呼ばれ、他のすべてのページで使用される共有 &quot;シェル&quot; です。

ファイルの下部付近にあるコードの `@RenderBody()` 行に注意してください。 `RenderBody` は、作成したすべてのページが表示されるプレースホルダーであり &quot;レイアウト ページで&quot; ラップされます。 `<h1>` 見出しを、 **&quot;** の mvc アプリケーション&quot; から &quot;Mvc Movie アプリ&quot;に変更します。

[!code-html[Main](adding-a-view/samples/sample3.html)]

アプリケーションを実行して、&quot;MVC Movie App&quot;になっていることを確認します。 **[About]** リンクをクリックすると、そのページに &quot;MVC ムービーアプリ&quot;も表示されます。

完全な *\_のレイアウトの vbhtml*ファイルを次に示します。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

次に、インデックスページ (ビュー) のタイトルを変更してみましょう。

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

*MvcMovie\Views\HelloWorld\Index.vbhtml*を開きます。 2つの場所で変更を行うことができます。最初に、ブラウザーのタイトルに表示されるテキスト、2番目のヘッダー (`<h2>` 要素) の順に移動します。 アプリのどの部分でコードが変更されるかを確認できるように、これらを少し異なるものにします。

アプリケーションを実行し、`http://localhost:xx/HelloWorld`を参照します。 ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください ビューに小さな変更を加えることで、アプリケーションの大きな変更を簡単に行うことができます。 (ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。 ブラウザーで Ctrl + F5 キーを押して、サーバーからの応答が強制的に読み込まれるようにしてください)。

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

ほとんどの &quot;データ&quot; (この例では、&quot;Hello World!&quot; メッセージ) はハードコーディングされています。 MVC アプリケーションには V (ビュー) がありますが、C (コントローラー) はありますが、M (モデル) はまだありません。 ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。

## <a name="passing-data-from-the-controller-to-the-view"></a>コントローラーからビューへのデータの受け渡し

データベースにアクセスしてモデルについて説明する前に、まずコントローラーからビューに情報を渡す方法について説明します。 クライアントに HTML 応答を表示するために、ビューテンプレートで必要なものを渡す必要があります。 これらのオブジェクトは、通常、コントローラークラスによって作成され、ビューテンプレートに渡されます。また、ビューテンプレートに必要なデータのみが含まれている必要があります。

以前は、`HelloWorldController` クラスを使用して、`Welcome` アクションメソッドは `name` と `numTimes` パラメーターを受け取り、パラメーター値をブラウザーに出力していました。 コントローラーがこの応答を直接レンダリングするのではなく、そのデータをビューのバッグに配置します。 コントローラーとビューは、`ViewBag` オブジェクトを使用してそのデータを保持できます。 これはビューテンプレートに自動的に渡され、バッグの内容をデータとして使用して HTML 応答を表示するために使用されます。 このようにすることで、コントローラーは1つの機能とビューテンプレートを考慮し、アプリケーション内で&quot; の問題を明確に分離 &quot;分離を維持できるようになります。

または、カスタムクラスを定義してから、そのオブジェクトのインスタンスを独自に作成し、データを入力してビューに渡すこともできます。 これは、ビューのカスタムモデルであるため、通常はビューモデルと呼ばれます。 ただし、少量のデータの場合は、ViewBag が優れています。

*HelloWorldController*ファイルに戻り、メッセージと Numtimes を ViewBag に配置するように、コントローラー内の `Welcome` メソッドを変更します。 ViewBag は動的なオブジェクトです。 つまり、任意のものを自由に配置できます。 ViewBag には、その中に何かを配置するまで定義されたプロパティはありません。

同じファイル内の新しいクラスを持つ完全な `HelloWorldController.vb`。

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

これで、ViewBag には、自動的にビューに渡されるデータが含まれています。 ここでも、次のような独自のオブジェクトを渡すこともできます。

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

ここで、`WelcomeView` テンプレートが必要です。 アプリケーションを実行して、新しいコードがコンパイルされるようにします。 ブラウザーを閉じ、`Welcome` メソッド内を右クリックして、 **[ビューの追加]** をクリックします。

**[ビューの追加]** ダイアログボックスは次のようになります。

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

新しい [ようこそ] の `<h2>` 要素の下に次のコードを追加し<em>ます。</em>vbhtml ファイル。 ループを作成して、ユーザーが必要としている回数だけ &quot;Hello&quot; と言います。

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

アプリケーションを実行し、を参照して `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

これで、データは URL から取得され、コントローラーに自動的に渡されます。 コントローラーは、`Model` オブジェクトにデータをパッケージ化し、そのオブジェクトをビューに渡します。 ビューでは、データが HTML としてユーザーに表示されます。

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

これは、モデルの &quot;M&quot; ですが、データベースの種類ではありませんでした。 学習したことを確認し、ムービーのデータベースを作成してみましょう。

> [!div class="step-by-step"]
> [前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)
