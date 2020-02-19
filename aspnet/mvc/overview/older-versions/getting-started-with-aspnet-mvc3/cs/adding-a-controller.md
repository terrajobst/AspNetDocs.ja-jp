---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: コントローラー (C#) を追加するMicrosoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457834"
---
# <a name="adding-a-controller-c"></a>コントローラーの追加 (C#)

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

MVC は、*モデルビューコントローラー*を表します。 MVC は、適切に設計され、保守しやすいアプリケーションを開発するためのパターンです。 MVC ベースのアプリケーションには次のものが含まれます。

- コントローラー: アプリケーションへの受信要求を処理し、モデルデータを取得して、クライアントに応答を返すビューテンプレートを指定するクラス。
- モデル: アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。
- Views: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。

このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。

まず、コントローラークラスを作成してみましょう。 **ソリューションエクスプローラー**で、[*コントローラー* ] フォルダーを右クリックし、 **[コントローラーの追加]** を選択します。

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

新しいコントローラーに "HelloWorldController" という名前を指定します。 既定のテンプレートは**空のコントローラー**のままにして、 **[追加]** をクリックします。

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

**ソリューションエクスプローラー**に、 *HelloWorldController.cs*という名前の新しいファイルが作成されていることに注意してください。 ファイルは IDE で開かれています。

![](adding-a-controller/_static/image5.png)

`public class HelloWorldController` ブロック内で、次のコードのような2つのメソッドを作成します。 コントローラーは HTML の文字列を例として返します。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

コントローラーには `HelloWorldController` という名前が付けられ、上記の最初のメソッドには `Index`という名前が付けられます。 ブラウザーから呼び出してみましょう。 アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。 ブラウザーで、アドレスバーのパスに "HelloWorld" を追加します。 (たとえば、次の図では `http://localhost:43246/HelloWorld.`)ブラウザーのページは次のスクリーンショットのようになります。 上記のメソッドでは、コードによって文字列が直接返されました。 HTML を返すだけでシステムに指示しました。

![](adding-a-controller/_static/image6.png)

ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。 ASP.NET MVC で使用される既定のマッピングロジックでは、次のような形式を使用して、呼び出すコードを決定します。

`/[Controller]/[ActionName]/[Parameters]`

URL の最初の部分では、実行するコントローラークラスを指定します。 そのため、 *HelloWorld*は `HelloWorldController` クラスにマップされます。 URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。 したがって、 */HelloWorld/Index*は、`HelloWorldController` クラスの `Index` メソッドを実行します。 また、 *HelloWorld*を参照するだけで、`Index` メソッドが既定で使用されていたことに注意してください。 これは、`Index` という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。

[https://www.microsoft.com](`http://localhost:xxxx/HelloWorld/Welcome`) を参照します。 `Welcome` メソッドが実行され、"This is the Welcome action method..." という文字列を返します。 既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]`。 この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。 URL の `[Parameters]` の部分はまだ使っていません。

![](adding-a-controller/_static/image7.png)

例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*)。 次のように2つのパラメーターを含めるように `Welcome` メソッドを変更します。 このコードでは、 C#省略可能なパラメーターの機能を使用して、パラメーターに値が渡されない場合に、`numTimes` パラメーターが既定値の1に設定されることを示していることに注意してください。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

アプリケーションを実行し、URL の例 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`を参照します。 URL の `name` と `numtimes` に違う値を指定してみてください。 システムは、アドレスバーのクエリ文字列の名前付きパラメーターを、メソッドのパラメーターに自動的にマップします。

![](adding-a-controller/_static/image8.png)

これらの例では、コントローラーが MVC の "VC" 部分を実行していました。つまり、ビューとコントローラーが動作します。 コントローラーは HTML を直接返しています。 通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。 代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。 次に、その方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](intro-to-aspnet-mvc-3.md)
> [次へ](adding-a-view.md)
