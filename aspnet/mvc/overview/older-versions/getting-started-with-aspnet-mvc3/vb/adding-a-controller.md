---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: コントローラーの追加 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434596"
---
# <a name="adding-a-controller-vb"></a>コントローラーの追加 (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 必要に応じC#て[ C# ](../cs/adding-a-controller.md) 、このチュートリアルのバージョンに切り替えます。

MVC は、*モデルビューコントローラー*を表します。 MVC は、各部分に個別の責任があるアプリケーションを開発するためのパターンです。

- モデル: アプリケーションのデータ。
- Views: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。
- コントローラー: アプリケーションへの受信 URL 要求を処理し、モデルデータを取得して、クライアントへの応答を表示するビューテンプレートを指定するクラス。

このチュートリアルでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。

**ソリューションエクスプローラー**で*Controllers*フォルダーを右クリックし、 **[コントローラーの追加]** を選択して、新しいコントローラーを作成します。

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

新しいコントローラーに HelloWorldController&quot; という名前を &quot;、 **[追加]** をクリックします。

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

右側の**ソリューションエクスプローラー**に、 *HelloWorldController.cs*という名前の新しいファイルが作成され、そのファイルが IDE で開かれていることがわかります。

新しい `public class HelloWorldController` ブロック内で、次のコードのような2つの新しいメソッドを作成します。 例として、コントローラーから直接 HTML の文字列を返します。

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

コントローラーには `HelloWorldController` という名前が付けられ、新しいメソッドには `Index`という名前が付けられます。 アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。 ブラウザーが起動したら、&quot;HelloWorld&quot; をアドレスバーのパスに追加します。 (私のコンピューターでは `http://localhost:43246/HelloWorld`)ブラウザーは次のスクリーンショットのようになります。 上記のメソッドでは、コードによって文字列が直接返されました。 私たちは、HTML を返すだけをシステムに指示しました。

![](adding-a-controller/_static/image5.png)

ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。 ASP.NET MVC で使用される既定のマッピングロジックでは、次のような形式を使用して、呼び出されるコードを制御します。

`/[Controller]/[ActionName]/[Parameters]`

URL の最初の部分では、実行するコントローラークラスを指定します。 そのため、 *HelloWorld*は `HelloWorldController` クラスにマップされます。 URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。 したがって、 */HelloWorld/Index*は、`HelloWorldController` クラスの `Index` メソッドを実行します。 上にある */HelloWorld*にアクセスするだけで、`Index` メソッドが既定で使用されていたことに注意してください。 これは、`Index` という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。

[https://www.microsoft.com](`http://localhost:xxxx/HelloWorld/Welcome`) を参照します。 `Welcome` メソッドが実行され、文字列 &quot;返されます。これは、ウェルカムアクションメソッド...&quot;です。 既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]`。 この URL では、コントローラーは `HelloWorld`、`Welcome` はメソッドです。 URL の `[Parameters]` 部分はまだ使用していません。

![](adding-a-controller/_static/image6.png)

例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*)。 次のように2つのパラメーターを含めるように `Welcome` メソッドを変更します。 VB の省略可能なパラメーター機能を使用して、パラメーターに値が渡されない場合、`numTimes` パラメーターの既定値は1であることを示すことに注意してください。

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

アプリケーションを実行し、`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`を参照し**ます。** `name` と `numtimes`に対して異なる値を試すことができます。 システムは、アドレスバーのクエリ文字列の名前付きパラメーターを、メソッドのパラメーターに自動的にマップします。

![](adding-a-controller/_static/image7.png)

これらの例では、コントローラーが MVC の VC 部分を実行していました。これはビューとコントローラーの動作です。 コントローラーは HTML を直接返しています。 通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。 代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。 これを実行する方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](intro-to-aspnet-mvc-3.md)
> [次へ](adding-a-view.md)
