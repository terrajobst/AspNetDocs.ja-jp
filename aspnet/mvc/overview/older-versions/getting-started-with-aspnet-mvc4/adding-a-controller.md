---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: コントローラーの追加 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485446"
---
# <a name="adding-a-controller"></a>コントローラーの追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

MVC は、*モデルビューコントローラー*を表します。 MVC は、適切な設計、テスト、保守が容易なアプリケーションを開発するためのパターンです。 MVC ベースのアプリケーションには次のものが含まれます。

- **M** odels: アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。
- **V** iews: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。
- **C** ontrollers: 入力方向のブラウザー要求を処理し、モデルデータを取得し、ブラウザーに応答を返すビューテンプレートを指定するクラス。

このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。

まず、コントローラークラスを作成してみましょう。 **ソリューションエクスプローラー**で、[*コントローラー* ] フォルダーを右クリックし、 **[コントローラーの追加]** を選択します。

![](adding-a-controller/_static/image1.png)

新しいコントローラーに HelloWorldController&quot;&quot;名前を指定します。 既定のテンプレートは**空の MVC コントローラー**のままにして、 **[追加]** をクリックします。

![コントローラーの追加](adding-a-controller/_static/image2.png)

**ソリューションエクスプローラー**に、 *HelloWorldController.cs*という名前の新しいファイルが作成されていることに注意してください。 ファイルは IDE で開かれています。

![](adding-a-controller/_static/image3.png)

このファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

コントローラーメソッドは HTML の文字列を例として返します。 コントローラーには `HelloWorldController` という名前が付けられ、上記の最初のメソッドには `Index`という名前が付けられます。 ブラウザーから呼び出してみましょう。 アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。 ブラウザーで、&quot;HelloWorld&quot; をアドレスバーのパスに追加します。 (たとえば、次の図では `http://localhost:1234/HelloWorld.`)ブラウザーのページは次のスクリーンショットのようになります。 上記のメソッドでは、コードによって文字列が直接返されました。 HTML を返すだけでシステムに指示しました。

![](adding-a-controller/_static/image4.png)

ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。 ASP.NET MVC で使用される既定の URL ルーティングロジックでは、次のような形式を使用して、呼び出すコードを決定します。

`/[Controller]/[ActionName]/[Parameters]`

URL の最初の部分では、実行するコントローラークラスを指定します。 そのため、 *HelloWorld*は `HelloWorldController` クラスにマップされます。 URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。 したがって、 */HelloWorld/Index*は、`HelloWorldController` クラスの `Index` メソッドを実行します。 また、 *HelloWorld*を参照するだけで、`Index` メソッドが既定で使用されていたことに注意してください。 これは、`Index` という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。

[https://www.microsoft.com](`http://localhost:xxxx/HelloWorld/Welcome`) を参照します。 `Welcome` メソッドが実行され、文字列 &quot;返されます。これは、ウェルカムアクションメソッド...&quot;です。 既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]`。 この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。 URL の `[Parameters]` の部分はまだ使っていません。

![](adding-a-controller/_static/image5.png)

例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*)。 次のように2つのパラメーターを含めるように `Welcome` メソッドを変更します。 このコードでは、 C#省略可能なパラメーターの機能を使用して、パラメーターに値が渡されない場合に、`numTimes` パラメーターが既定値の1に設定されることを示していることに注意してください。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

アプリケーションを実行し、URL の例 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`を参照します。 URL の `name` と `numtimes` に違う値を指定してみてください。 [ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)では、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。

![](adding-a-controller/_static/image6.png)

これらの例では、コントローラーが MVC の &quot;VC&quot; の部分 (ビューとコントローラーが動作) を実行しています。 コントローラーは HTML を直接返しています。 通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。 代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。 次に、その方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](intro-to-aspnet-mvc-4.md)
> [次へ](adding-a-view.md)
