---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 追加すると表示されます (C#) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498844"
---
# <a name="adding-a-view-c"></a>ビュー (C#) を追加します。

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。
> 
> 
> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。 [バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)に切り替えてください。

このセクションでは、`HelloWorldController` クラスを変更して、ビューテンプレートファイルを使用して、クライアントに HTML 応答を生成するプロセスを完全にカプセル化します。

ASP.NET MVC 3 で導入された新しい[Razor ビューエンジン](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)を使用して、ビューテンプレートファイルを作成します。 Razor ベースのビューテンプレートには、ファイル拡張子が*cshtml*と、を使用してC#HTML 出力を作成するための洗練された方法が用意されています。 Razor では、ビューテンプレートを記述するときに必要な文字数とキーストロークの数が最小限に抑えられ、滑らかなコーディングワークフローが可能になります。

まず、ビューテンプレートと、`HelloWorldController` クラスの `Index` メソッドを使用します。 現在、`Index` メソッドは、コントローラー クラスでハード コーディングされるメッセージを含む文字列を返します。 次に示すように、`View` オブジェクトを返すように `Index` メソッドを変更します。

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

このコードでは、ビューテンプレートを使用してブラウザーへの HTML 応答を生成します。 プロジェクトで、`Index` メソッドで使用できるビューテンプレートを追加します。 これを行うには、`Index` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。

![](adding-a-view/_static/image1.png)

**[ビューの追加]** ダイアログボックスが表示されます。 既定値のままにして、 **[追加]** ボタンをクリックします。

![](adding-a-view/_static/image2.png)

*MvcMovie\Views\HelloWorld*フォルダーと*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルが作成されます。 **ソリューションエクスプローラー**で確認できます。

![](adding-a-view/_static/image3.png)

作成された*インデックスの cshtml*ファイルを次に示します。

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

`<h2>` タグの下に HTML を追加します。 変更した*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルを次に示します。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

アプリケーションを実行し、`HelloWorld` コントローラー (`http://localhost:xxxx/HelloWorld`) に移動します。 コントローラーの `Index` メソッドでは、多くの作業が行われませんでした。単にステートメント `return View()`を実行しました。これは、メソッドがビューテンプレートファイルを使用してブラウザーに応答を表示する必要があることを指定します。 使用するビューテンプレートファイルの名前を明示的に指定していないので、ASP.NET MVC では、\Views\HelloWorld フォルダー内のファイルを使用するように既定で設定されてい*ます。* 次の画像は、ビューにハードコーディングされた文字列を示しています。

![](adding-a-view/_static/image6.png)

すばらしいですね。 ただし、ブラウザーのタイトルバーに "Index" と表示され、ページの大きなタイトルに "My MVC Application" と表示されていることに注意してください。 これらを変更してみましょう。

## <a name="changing-views-and-layout-pages"></a>ビューおよびレイアウトページの変更

最初に、ページの上部にある "My MVC Application" タイトルを変更します。 このテキストは、すべてのページに共通です。 実際には、アプリケーション内のすべてのページに表示される場合でも、プロジェクト内の1つの場所にのみ実装されます。 **ソリューションエクスプローラー**の [ */* ]/[共有] フォルダーにアクセスし、 *\_Layout*ファイルを開きます。 このファイルは*レイアウトページ*と呼ばれ、他のすべてのページが使用する共有の "シェル" です。

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

レイアウトテンプレートを使用すると、サイトの HTML コンテナーレイアウトを1か所で指定し、サイト内の複数のページに適用できます。 ファイルの下部付近の `@RenderBody()` 行に注意してください。 `RenderBody` は、作成するすべてのビュー固有ページがレイアウトページに表示されるプレースホルダーです。 レイアウトテンプレートのタイトル見出しを "My MVC Application" から "MVC Movie App" に変更します。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

アプリケーションを実行し、"MVC Movie App" と表示されていることを確認します。 **[About]** リンクをクリックすると、そのページに "MVC Movie App" が表示されます。 レイアウトテンプレートで変更を1回行って、サイトのすべてのページに新しいタイトルを反映させることができました。

![](adding-a-view/_static/image9.png)

次に、完全な *\_Layout*ファイルを示します。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

次に、インデックスページ (ビュー) のタイトルを変更してみましょう。

*MvcMovie\Views\HelloWorld\Index.cshtml*を開きます。 2つの場所で変更を行うことができます。最初に、ブラウザーのタイトルに表示されるテキスト、2番目のヘッダー (`<h2>` 要素) の順に移動します。 これを少し変えれば、コードのどの部分でアプリのどの部分が変更されるかを確認することができます。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

表示する HTML タイトルを示すために、上記のコードでは `ViewBag` オブジェクトの `Title` プロパティを設定しています (これは、*インデックスの cshtml*ビューテンプレートに含まれています)。 レイアウトテンプレートのソースコードを確認すると、このテンプレートでは、HTML の `<head>` セクションの一部として、`<title>` 要素でこの値が使用されていることがわかります。 この方法を使用すると、ビューテンプレートとレイアウトファイルの間で、他のパラメーターを簡単に渡すことができます。

アプリケーションを実行し、`http://localhost:xx/HelloWorld`を参照します。 ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください (ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。 ブラウザーで Ctrl + F5 キーを押して、サーバーからの応答が強制的に読み込まれるようにしてください)。

また、*インデックスの cshtml*ビューテンプレートの内容が *\_のレイアウト*にマージされ、1つの HTML 応答がブラウザーに送信されたことにも注目してください。 レイアウト テンプレートを使用すれば、アプリケーションのすべてのページに適用される変更をとても簡単に行うことができます。

![](adding-a-view/_static/image10.png)

ここでは、"データ" のごく一部 (この場合は "Hello from our View Template!" というメッセージ) を ハード コーディングしました。 MVC アプリケーションには "V" (ビュー) があり、"C" (コントローラー) もありますが、"M" (モデル) はまだありません。 ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。

## <a name="passing-data-from-the-controller-to-the-view"></a>コントローラーからビューへのデータの受け渡し

データベースにアクセスしてモデルについて説明する前に、まずコントローラーからビューに情報を渡す方法について説明します。 コントローラークラスは、受信 URL 要求に応答して呼び出されます。 コントローラークラスは、入力パラメーターを処理し、データベースからデータを取得し、最終的にブラウザーに返す応答の種類を決定するコードを記述します。 これで、ビューテンプレートをコントローラーから使用して、ブラウザーに HTML 応答を生成して書式設定することができます。

コントローラーは、ビューテンプレートがブラウザーに応答を表示するために必要なすべてのデータまたはオブジェクトを提供する役割を担います。 ビューテンプレートでは、ビジネスロジックを実行したり、データベースを直接操作したりすることはできません。 代わりに、コントローラーによって提供されるデータでのみ機能します。 この "問題の分離" を維持することにより、コードをクリーンアップし、保守が容易になります。

現時点では、`HelloWorldController` クラスの `Welcome` アクションメソッドは `name` と `numTimes` パラメーターを受け取り、ブラウザーに値を直接出力します。 コントローラーがこの応答を文字列として表示するのではなく、ビューテンプレートを使用するようにコントローラーを変更してみましょう。 このビュー テンプレートでは動的応答が生成されます。これは、応答を生成するために、コントローラーからビューに適量のデータを渡す必要があることを意味します。 これを行うには、ビューテンプレートで必要とされる動的データを、ビューテンプレートがアクセスできる `ViewBag` オブジェクトに配置します。

*HelloWorldController.cs*ファイルに戻り、`Welcome` メソッドを変更して、`ViewBag` オブジェクトに `Message` と `NumTimes` の値を追加します。 `ViewBag` は動的なオブジェクトであるため、任意のものを自由に配置できます。`ViewBag` オブジェクトには、その中に何かを配置するまで、定義されたプロパティはありません。 完全な *HelloWorldController.cs* ファイルは次のようになります。

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

現在、`ViewBag` オブジェクトには、ビューに自動的に渡されるデータが含まれています。

次に、ウェルカムビューテンプレートが必要です。 **[デバッグ]** メニューの **[Mvcmovie のビルド]** を選択して、プロジェクトがコンパイルされていることを確認します。

[BuildHelloWorld の ![](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

次に、`Welcome` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。 **[ビューの追加]** ダイアログボックスは次のようになります。

![](adding-a-view/_static/image13.png)

**[追加]** をクリックし、新しい*Welcome. cshtml*ファイルの `<h2>` 要素の下に次のコードを追加します。 ユーザーが必要としている回数だけ "Hello" というループを作成します。 次に、完全な*Welcome*ファイルを示します。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

アプリケーションを実行し、次の URL を参照します。

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

これで、データは URL から取得され、コントローラーに自動的に渡されます。 コントローラーは、データを `ViewBag` オブジェクトにパッケージ化し、そのオブジェクトをビューに渡します。 ビューには、データが HTML としてユーザーに表示されます。

![](adding-a-view/_static/image14.png)

"M" (モデル) については学習しましたが、データベースについてはまだです。 学習したことを確認し、ムービーのデータベースを作成してみましょう。

> [!div class="step-by-step"]
> [前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)
