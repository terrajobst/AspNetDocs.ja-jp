---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: ビューを追加する |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469774"
---
# <a name="adding-a-view"></a>ビューの追加

[Scott マン Selman](https://github.com/shanselman)

> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

このセクションでは、HelloWorldController クラスがビューテンプレートファイルを使用して、HTML 応答の生成をクライアントに対して正常にカプセル化する方法を見ていきます。

まず、ビューテンプレートとインデックスメソッドを使用してみましょう。 このメソッドは Index と呼ばれ、HelloWorldController にあります。 現在、Index () メソッドは、コントローラークラス内にハードコードされたメッセージを含む文字列を返します。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

次のように、インデックスメソッドをに変更してみましょう。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

ここで、Index () メソッドに使用できるビューテンプレートをプロジェクトに追加してみましょう。 これを行うには、Index メソッドの途中でマウスを右クリックし、[ビューの追加] をクリックします。

![image](getting-started-with-mvc-part3/_static/image1.png)

[ビューの追加] ダイアログが表示されます。このダイアログでは、Index メソッドで使用できるビューテンプレートを作成する方法に関するいくつかのオプションを提供しています。 ここでは、何も変更せずに、[追加] ボタンをクリックするだけです。

[![ビューの追加 ダイアログ](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

[追加] をクリックすると、次に示すように、ソリューションフォルダーに新しいフォルダーと新しいファイルが表示されます。 これで、[ビュー] の下に HelloWorld フォルダーがあり、そのフォルダー内にインデックス .aspx ファイルが作成されました。

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

新しいインデックスファイルも既に開いていて、編集する準備ができています。 最初の &lt;h2&gt;Index&lt;/h2&gt; "Hello World" のようなテキストを追加します。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

アプリケーションを実行し、ブラウザーでもう一度[`http://localhost:xx/HelloWorld`](http://localhostxx)にアクセスします。 この例では、コントローラーの Index メソッドは何の処理も行いませんでしたが、"return View ()" を呼び出しました。これは、ビューテンプレートファイルを使用してクライアントに応答を返すことを示していました。 使用するビューテンプレートファイルの名前を明示的に指定しなかったため、ASP.NET MVC では、\Views\HelloWorld フォルダー内のインデックス .aspx ビューファイルを使用するように既定で設定されています。 これで、ビューにハードコーディングされた文字列が表示されます。

[![インデックス-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

すばらしいですね。 ただし、ブラウザーのタイトルには "Index" と表示され、ページの大きなタイトルは "My MVC Application" と表示されていることに注意してください。 これらを変更してみましょう。

### <a name="changing-views-and-master-pages"></a>ビューおよびマスターページの変更

まず、"My MVC Application" というテキストを変更してみましょう。 そのテキストは共有され、すべてのページに表示されます。 実際には、アプリ内のすべてのページにある場合でも、コード内の1つの場所にのみ表示されます。 ソリューションエクスプローラーの [/]/[共有] フォルダーにアクセスして、[] を開きます。 このファイルはマスターページと呼ばれ、他のすべてのページで使用される共有の "シェル" です。

このファイルに "MainContent" というテキストが ContentPlaceholder れていることに注意してください。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

このプレースホルダーには、作成したすべてのページが表示され、マスターページに "ラップ" されます。 タイトルを変更してから、アプリを実行して複数のページにアクセスしてみてください。 1つの変更が複数のページに表示されることがわかります。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

これで、すべてのページに、"マイ MVC ムービーアプリケーション" という主要な見出しが表示されるようになりました。 これにより、すべてのページで共有されている白いテキストが上に表示されます。

次に示すのは、変更されたタイトルを含む、次のような場合です。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

次に、インデックスページのタイトルを変更してみましょう。

/HelloWorld/Index.aspx. を開く 変更する場所は2つあります。 最初に、ブラウザーのタイトルに表示されるタイトル、2番目のヘッダー (H2) も表示されます。 アプリケーションのどの部分に変更が加えられたかを確認できるように、それぞれを少し異なるようにします。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

アプリを実行し、/Movies. にアクセスします。 ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください。 ビューに小さな変更を加えることで、アプリの大きな変更を簡単に行うことができます。

[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

"データ" の少しです (この例では "Hello World!")。 メッセージ) がハードコーディングされています。 V (Views) がありますが、C (コントローラー) を持っていますが、M (モデル) はまだありません。 ここでは、データベースを作成し、そこからモデルデータを取得する方法について説明します。

## <a name="passing-a-viewmodel"></a>ビューモデルの引き渡し

データベースにアクセスしてモデルについて説明する前に、まず "Viewmodel" について説明します。 これらは、HTML 応答をクライアントに返すためにビューテンプレートが必要とするものを表すオブジェクトです。 これらは通常、コントローラークラスによって作成され、ビューテンプレートに渡されます。また、ビューテンプレートに必要なデータだけを含める必要があります。

以前の HelloWorld サンプルでは、Welcome () アクションメソッドは名前と numTimes パラメーターを受け取り、ブラウザーに出力しました。 コントローラーがこの応答を直接レンダリングするのではなく、そのデータを保持する小さいクラスを作成し、それをビューテンプレートに渡して、それを使用して HTML 応答を表示します。 このようにして、コントローラーは1つの問題とビューテンプレートを考慮しています。これにより、アプリケーション内でクリーンな "問題の分離" を維持できるようになります。

HelloWorldController.cs ファイルに戻り、新しい "WelcomeViewModel" クラスを追加して、コントローラー内の Welcome メソッドを変更します。 同じファイル内の新しいクラスを含む完全な HelloWorldController.cs を次に示します。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

複数の行に存在していても、ようこそメソッドは実際には2つのコードステートメントにすぎません。 最初のステートメントは、2つのパラメーターをモデル化オブジェクトにパッケージ化し、2つ目のパラメーターは結果のオブジェクトをビューに渡します。

ここで、ウェルカムビューテンプレートが必要です。 [ようこそ] メソッドを右クリックし、[ビューの追加] を選択します。 今回は、[厳密に型指定されたビューを作成する] チェックボックスをオンにし、ドロップダウンリストから WelcomeViewModel クラスを選択します。 この新しいビューでは、WelcomeViewModels とその他の種類のオブジェクトは認識されません。

> *注: ドロップダウンリストに表示するには、WelcomeViewModel を追加した後に1回コンパイルする必要があります。*

[ビューの追加] ダイアログボックスは次のようになります。 [追加] ボタンをクリックします。 ![丸で囲んだビューの追加](getting-started-with-mvc-part3/_static/image10.png)

新しい Welcome の &lt;h2&gt; の下に次のコードを追加します。 ループを作成し、ユーザーが必要としている回数だけ Hello と言います。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

また、次のスクリーンショットに示されているように、モデルオブジェクトを参照するたびに便利な Intellisense が得られるので、このビューを入力している間に、WelcomeViewModel についての情報が表示されます。

[![NumTime ソースコード](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

アプリケーションを実行し、`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` にもう一度アクセスします。 これで、URL からデータを取得し、コントローラーに自動的に渡されます。コントローラーはデータをビューモデルにパッケージ化し、そのオブジェクトをビューに渡します。 ビューでは、データが HTML としてユーザーに表示されます。

[![ようこそ-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

それは、モデルの "M" ですが、データベースの種類ではありませんでした。 学習した内容を見て、映画のデータベースを作成しましょう。

> [!div class="step-by-step"]
> [前へ](getting-started-with-mvc-part2.md)
> [次へ](getting-started-with-mvc-part4.md)
