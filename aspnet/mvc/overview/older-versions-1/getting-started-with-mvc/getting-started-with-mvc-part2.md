---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: コントローラーの追加 |Microsoft Docs
author: shanselman
description: このチュートリアルが使用可能な場合は、Visual Studio 2013 を使用して更新されたバージョンです。 新しいチュートリアルでは、ASP.NET MVC 5 を使用します。これにより、
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437566"
---
# <a name="adding-a-controller"></a>コントローラーの追加

[Scott マン Selman](https://github.com/shanselman)

> > [!NOTE]
> > このチュートリアルが使用可能な場合は、 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)を[使用して](../../getting-started/introduction/getting-started.md)更新されたバージョンです。 このチュートリアルでは、ASP.NET MVC 5 を使用します。このチュートリアルでは、多くの機能強化が行われています。
>
>
> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

MVC は、モデル、ビュー、コントローラーを表します。 MVC は、アプリケーションを開発するためのパターンであり、各部分が別の部分とは異なる責任を担います。

- モデル: アプリケーションのデータ
- Views: アプリケーションが HTML 応答を動的に生成するために使用するテンプレートファイル。
- コントローラー: アプリケーションへの受信 URL 要求を処理し、モデルデータを取得して、クライアントに応答を返すビューテンプレートを指定するクラス

このチュートリアルでは、これらのすべての概念について説明し、それらを使用してアプリケーションを構築する方法について説明します。

ソリューションエクスプローラーで controllers フォルダーを右クリックし、[コントローラーの追加] を選択して、新しいコントローラーを作成してみましょう。

[![Addコントローラーの追加](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

新しいコントローラーに "HelloWorldController" という名前を指定し、[追加] をクリックします。

[[コントローラーの追加] ダイアログ ![](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

右側のソリューションエクスプローラーに、HelloWorldController.cs という名前の新しいファイルが作成され、そのファイルが**IDE**で開かれていることがわかります。

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

新しいパブリッククラス HelloWorldController 内で、次のような2つの新しいメソッドを作成します。 例として、コントローラーから直接 HTML の文字列を返します。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

コントローラーは HelloWorldController という名前で、新しいメソッドは Index と呼ばれます。 先ほどと同じように、アプリケーションをもう一度実行します ([再生] ボタンをクリックするか、F5 キーを押します)。 ブラウザーが起動したら、アドレスバーのパスを `http://localhost:xx/HelloWorld` に変更します。ここで、xx はコンピューターが選択した任意の番号です。 これでブラウザーは次のスクリーンショットのようになります。 上記のメソッドでは、"Content" という名前のメソッドに渡された文字列を返しました。 システムが HTML を返すだけです。

ASP.NET MVC は、受信 URL に応じて、さまざまなコントローラークラス (およびその中のさまざまなアクションメソッド) を呼び出します。 ASP.NET MVC で使用される既定のマッピングロジックでは、次のような形式を使用して、実行されるコードを制御します。

/[Controller]/[ActionName]/[Parameters]

URL の最初の部分では、実行するコントローラークラスを指定します。 そのため、HelloWorld は HelloWorldController クラスにマップされます。 URL の2番目の部分では、実行するクラスのアクションメソッドを決定します。 したがって、/HelloWorld/Index では、HelloWorldController クラスの Index () メソッドが実行されます。 上の例にのみアクセスする必要があり、メソッドインデックスが暗黙的に示されていることに注意してください。 これは、"Index" という名前のメソッドが、明示的に指定されていない場合にコントローラーで呼び出される既定のメソッドであるためです。

[既定のアクション ![](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

ここで `http://localhost:xx/HelloWorld/Welcome.` にアクセスして、ウェルカムメソッドが実行され、HTML 文字列が返されるようになりました。

ここでも、/[Controller]/[ActionName]/[Parameters] のように、コントローラーは HelloWorld で、この場合は Welcome がメソッドです。 パラメーターはまだ完了していません。

[![開始アクションメソッド](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

サンプルを少し変更して、URL の一部の情報をコントローラーに渡すことができるようにします。たとえば、/HelloWorld/Welcome? name = Scott&amp;numtimes = 4 のようにします。 2つのパラメーターを含むように Welcome メソッドを変更し、次のように更新します。 C#省略可能なパラメーター機能を使用して、パラメーター numtimes が渡されなかった場合、既定値は1に設定されることに注意してください。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

アプリケーションを実行し、[名前] と [numtimes] の値を必要に応じて変更 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` にアクセスします。 システムによって、アドレスバーのクエリ文字列の名前付きパラメーターが、メソッドのパラメーターに自動的にマップされます。

これらの例では、コントローラーがすべての作業を行っており、HTML を直接返しています。 通常、コントローラーが HTML を直接返すことはありません。これは、コードが非常に面倒であるためです。 代わりに、通常は別のビューテンプレートファイルを使用して、HTML 応答を生成します。 これを実行する方法を見てみましょう。 ブラウザーを閉じて、IDE に戻ります。

> [!div class="step-by-step"]
> [前へ](getting-started-with-mvc-part1.md)
> [次へ](getting-started-with-mvc-part3.md)
