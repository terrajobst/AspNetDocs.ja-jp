---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: Create メソッドと Create View | を追加するMicrosoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437290"
---
# <a name="adding-a-create-method-and-create-view"></a>Create メソッドと Create ビューの追加

[Scott マン Selman](https://github.com/shanselman)

> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

このセクションでは、ユーザーがデータベースに新しい映画を作成できるようにするために必要なサポートを実装します。 これを行うには、/Movies/Create URL アクションを実装します。

/Movies/Create URL の実装は、2つの手順で行います。 ユーザーが最初に/Movies/Create URL にアクセスしたときに、新しいムービーを入力するために入力できる HTML フォームを表示したいと考えています。 次に、ユーザーがフォームを送信し、データをサーバーにポストバックするときに、ポストされた内容を取得してデータベースに保存します。

これらの2つの手順は、Moviescontroller.cs クラス内の2つの Create () メソッド内に実装します。 1つの方法では、ユーザーが新しいムービーを作成するために入力する必要のある &lt;フォーム&gt; を示します。 2番目の方法では、ユーザーが &lt;フォーム&gt; をサーバーに送り返し、データベース内に新しいムービーを保存するときに、ポストされたデータの処理を処理します。

Moviescontroller.cs クラスに追加して、これを実装するコードを次に示します。

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

上のコードには、コントローラー内で必要なすべてのコードが含まれています。

ここで、フォームをユーザーに表示するために使用する Create View テンプレートを実装しましょう。 最初の Create メソッドを右クリックし、[ビューの追加] を選択して、ムービーフォームのビューテンプレートを作成します。

ビューテンプレートに "Movie" を表示データクラスとして渡し、"スキャフォールディング" というテンプレートを "作成" することを指定します。

[ビューの追加 ![](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

[追加] ボタンをクリックすると、\Movies\Create.aspx View テンプレートが作成されます。 [View content] \ (コンテンツの表示 \) ドロップダウンから [作成] を選択したので、[ビューの追加] ダイアログボックスには既定のコンテンツが自動的に "スキャフォールディング" されます。 スキャフォールディングによって、HTML &lt;フォーム&gt;が作成され、検証エラーメッセージが表示されます。スキャフォールディングによってムービーが認識されるため、クラスの各プロパティのラベルとフィールドが作成されました。

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

このデータベースでは、ムービーに ID が自動的に付与されるため、モデルを参照するフィールドを削除してみましょう。[作成] ビューの Id。 凡例の&gt;フィールド&gt;&lt;[凡例] の &lt;7 行を削除します。これには、不要な ID フィールドが表示されます。

ここで、新しいムービーを作成し、データベースに追加しましょう。 この操作を行うには、アプリケーションをもう一度実行し、"/映画" の URL にアクセスし、[作成] リンクをクリックして新しいムービーを追加します。

[![作成-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

[作成] ボタンをクリックすると、このフォームのデータが、先ほど作成した/Movies/Create メソッドにポストバックされます (HTTP POST 経由)。 システムが URL から "numTimes" パラメーターと "name" パラメーターを自動的に取得して、以前のメソッドのパラメーターにマップした場合と同様に、システムは自動的に POST からフォームフィールドを取得し、オブジェクトにマップします。 この場合、"ReleaseDate" や "Title" などの HTML のフィールドの値は、ムービーの新しいインスタンスの正しいプロパティに自動的に挿入されます。

もう一度 Moviescontroller.cs から2つ目の Create メソッドを見てみましょう。 引数として "Movie" オブジェクトを取得する方法に注目してください。

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

その後、このムービーオブジェクトは、Create action メソッドの [HttpPost] バージョンに渡され、データベースに保存された後、ムービーリストに保存された結果を示す Index () アクションメソッドにリダイレクトされます。

[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

ただし、ムービーが正しいかどうかは確認しません。また、データベースでタイトルのないムービーを保存することはできません。 データベースがエラーをスローする前に、ユーザーに通知することもできます。 これを行うには、アプリケーションに検証サポートを追加します。

> [!div class="step-by-step"]
> [前へ](getting-started-with-mvc-part5.md)
> [次へ](getting-started-with-mvc-part7.md)
