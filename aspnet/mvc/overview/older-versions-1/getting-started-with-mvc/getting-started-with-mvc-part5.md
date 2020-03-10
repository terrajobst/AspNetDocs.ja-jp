---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437368"
---
# <a name="accessing-your-models-data-from-a-controller"></a>コントローラーからモデルのデータにアクセスする

[Scott マン Selman](https://github.com/shanselman)

> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

このセクションでは、新しい Moviescontroller.cs クラスを作成し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。

Controllers フォルダーを右クリックし、新しい Moviescontroller.cs を作成します。

[コントローラーの追加 ![](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

これにより、プロジェクト内の \ Controllers フォルダーの下に新しい "MoviesController.cs" ファイルが作成されます。 MovieController を更新して、新しく設定されたデータベースから映画の一覧を取得してみましょう。

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

1984年の夏の後にリリースされた映画のみを取得するように LINQ クエリを実行しています。 このムービーの一覧を表示するにはビューテンプレートが必要です。そのため、メソッドを右クリックし、[ビューの追加] を選択して作成します。

[ビューの追加] ダイアログボックスで、ビューテンプレートに&lt;映画&gt; リストを渡していることを示します。 以前に [ビューの追加] ダイアログを使用し、"空の" テンプレートを作成することを選択したのとは異なり、今回は、Visual Studio が既定のコンテンツを含むビューテンプレートを自動的に "スキャフォールディング" するように指定します。 これを行うには、[コンテンツの表示] ドロップダウンメニュー内の [リスト] 項目を選択します。

新しいクラスを作成した場合は、[ビューの追加] ダイアログボックスに表示されるように、アプリケーションをコンパイルする必要があることに注意してください。

![ビューの追加](getting-started-with-mvc-part5/_static/image3.png)

[追加] をクリックすると、ムービーの一覧を表示するビューのコードが自動的に生成されます。 &lt;h2&gt; の見出しを、前に Hello World ビューで行ったような "マイムービーリスト" のように変更することをお勧めします。

[![映画-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

アプリケーションを実行し、アドレスバーで [/ムービー] にアクセスします。 これで、コントローラー内の基本的なクエリを使用してデータベースからデータを取得し、ムービーを認識するビューにデータを返しました。 その後、そのビューはムービーの一覧をスピンし、データのテーブルを作成します。

[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

このアプリケーションでは編集、詳細、削除機能を実装しません。そのため、スキャフォールディングテンプレートによって作成された既定のリンクは必要ありません。 /Movies/Index.aspx ファイルを開き、削除します。

更新されたビューテンプレートのソースコードを次に示します。これらの変更を行った後は、次のようになります。

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

必要のないリンクが作成されているので、この例ではリンクを削除します。 次に示すように、新しいリンクを作成しておきます。 この列を削除すると、アプリは次のようになります。

[![ムービーの一覧-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

これで、ムービーデータを簡単に一覧表示できるようになりました。 ただし、[新規作成] リンクをクリックすると、フックされていないためエラーが発生します。 Create Action メソッドを実装し、ユーザーがデータベースに新しい映画を入力できるようにしましょう。

> [!div class="step-by-step"]
> [前へ](getting-started-with-mvc-part4.md)
> [次へ](getting-started-with-mvc-part6.md)
