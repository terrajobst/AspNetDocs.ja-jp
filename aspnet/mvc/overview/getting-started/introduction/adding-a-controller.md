---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: コントローラーの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 80000b366203eff4b9524b7a5995832753b9eed3
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519051"
---
# <a name="adding-a-controller"></a>コントローラーの追加

[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

MVC は、*モデルビューコントローラー*を表します。 MVC は、適切な設計、テスト、保守が容易なアプリケーションを開発するためのパターンです。 MVC ベースのアプリケーションには次のものが含まれます。

- **M** odels: アプリケーションのデータを表し、検証ロジックを使用してそのデータにビジネスルールを適用するクラス。
- **V** iews: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。
- **C** ontrollers: 入力方向のブラウザー要求を処理し、モデルデータを取得し、ブラウザーに応答を返すビューテンプレートを指定するクラス。

このチュートリアルシリーズでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。

まず、コントローラークラスを作成してみましょう。 **ソリューションエクスプローラー**で、 *Controllers*フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** の順にクリックします。

![](adding-a-controller/_static/image1.png)

**[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 コントローラー-空]** をクリックし、 **[追加]** をクリックします。

![](adding-a-controller/_static/image2.png)  

新しいコントローラーに "HelloWorldController" という名前を指定し、 **[追加]** をクリックします。

![コントローラーの追加](adding-a-controller/_static/image3.png)

*HelloWorldController.cs*という名前の新しいファイルと新しいフォルダー *Views\HelloWorld*が作成されたことを**ソリューションエクスプローラー**に注意してください。 コントローラーは IDE で開かれています。

![](adding-a-controller/_static/image4.png)

このファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

コントローラーメソッドは HTML の文字列を例として返します。 コントローラーには `HelloWorldController` という名前が付けられ、最初のメソッドには `Index`という名前が付けられます。 ブラウザーから呼び出してみましょう。 アプリケーションを実行します (F5 キーを押すか、Ctrl キーを押しながら F5 キーを押します)。 ブラウザーで、&quot;HelloWorld&quot; をアドレスバーのパスに追加します。 (たとえば、次の図では `http://localhost:1234/HelloWorld.`)ブラウザーのページは次のスクリーンショットのようになります。 上記のメソッドでは、コードによって文字列が直接返されました。 HTML を返すだけでシステムに指示しました。

![](adding-a-controller/_static/image5.png)

ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。 ASP.NET MVC で使用される既定の URL ルーティングロジックでは、次のような形式を使用して、呼び出すコードを決定します。

`/[Controller]/[ActionName]/[Parameters]`

アプリでルーティングの形式を設定するには *\_Start/RouteConfig*ファイルを使用します。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

アプリケーションを実行するときに、URL セグメントを指定しない場合、既定では、上記のコードの [既定] セクションで指定されている "Home" コントローラーと "Index" アクションメソッドが既定値になります。

URL の最初の部分では、実行するコントローラークラスを指定します。 そのため、 *HelloWorld*は `HelloWorldController` クラスにマップされます。 URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。 したがって、 */HelloWorld/Index*は、`HelloWorldController` クラスの `Index` メソッドを実行します。 また、 *HelloWorld*を参照するだけで、`Index` メソッドが既定で使用されていたことに注意してください。 これは、`Index` という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。 URL セグメントの 3 番目の部分 (`Parameters`) はルート データ用です。 ルートデータについては、このチュートリアルで後ほど説明します。

`http://localhost:xxxx/HelloWorld/Welcome` を参照します。 `Welcome` メソッドが実行され、文字列 &quot;返されます。これは、ウェルカムアクションメソッド...&quot;です。 既定の MVC マッピングは `/[Controller]/[ActionName]/[Parameters]`。 この URL では、コントローラーは `HelloWorld` で、`Welcome` がアクション メソッドです。 URL の `[Parameters]` の部分はまだ使っていません。

![](adding-a-controller/_static/image6.png)

例を少し変更して、URL からコントローラーにパラメーター情報を渡すことができるようにします (たとえば、 */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*)。 次のように2つのパラメーターを含めるように `Welcome` メソッドを変更します。 このコードでは、 C#省略可能なパラメーターの機能を使用して、パラメーターに値が渡されない場合に、`numTimes` パラメーターが既定値の1に設定されることを示していることに注意してください。

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> セキュリティに関する注意: 上記のコードでは、 [HttpUtility](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)を使用して、悪意のある入力 (つまり JavaScript) からアプリケーションを保護します。 詳細については[、「方法: HTML エンコーディングを文字列に適用](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)する」を参照してください。

 アプリケーションを実行し、URL の例 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) を参照します。 URL の `name` と `numtimes` に違う値を指定してみてください。 [ASP.NET MVC モデルバインドシステム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)では、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。

![](adding-a-controller/_static/image7.png)

上記のサンプルでは、URL セグメント (`Parameters`) は使用されず、`name` パラメーターと `numTimes` パラメーターは[クエリ文字列](http://en.wikipedia.org/wiki/Query_string)として渡されます。 ? 上記の URL の (疑問符) は区切り記号であり、クエリ文字列は次のようになります。 &amp; 文字は、クエリ文字列を区切ります。

Welcome メソッドを次のコードに置き換えます。

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

アプリケーションを実行し、次の URL を入力します。 `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

この時点で、3番目の URL セグメントがルートパラメーターと一致し `ID.` `Welcome` アクションメソッドには、`RegisterRoutes` メソッドの URL 指定に一致したパラメーター (`ID`) が含まれています。

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC アプリケーションでは、パラメーターをクエリ文字列として渡すよりも、ルートデータとしてパラメーターを渡す方が一般的です (上記の ID を使用した場合など)。 ルートを追加して、URL のルートデータとしてパラメーターに `name` と `numtimes` を渡すこともできます。 *アプリ\_Start\RouteConfig.cs*ファイルに、"Hello" ルートを追加します。

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

アプリケーションを実行し、`/localhost:XXX/HelloWorld/Welcome/Scott/3`を参照します。

![](adding-a-controller/_static/image9.png)

多くの MVC アプリケーションでは、既定のルートは正常に機能します。 このチュートリアルの後半では、モデルバインダーを使用してデータを渡す方法について学習します。そのための既定のルートを変更する必要もありません。

これらの例では、コントローラーが MVC の &quot;VC&quot; の部分を実行しています。つまり、ビューとコントローラーが動作します。 コントローラーは HTML を直接返しています。 通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に煩雑になるためです。 代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。 次に、その方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](getting-started.md)
> [次へ](adding-a-view.md)
