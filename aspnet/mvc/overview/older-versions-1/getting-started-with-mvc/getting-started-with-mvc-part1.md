---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC の概要 |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 読み取りと書き込みをデータベースから単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: dcc2e703829cfa0b77575870feff451fd0738f56
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59416494"
---
# <a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 入門

[Scott Hanselman](https://github.com/shanselman)による

> > [!NOTE]
> > このチュートリアルでは、使用可能な場合は、更新されたバージョン[ここ](../../getting-started/introduction/getting-started.md)を使用して[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)します。 新しいチュートリアルでは、このチュートリアルで多くの機能強化を提供する ASP.NET MVC 5 を使用します。
>
>
> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 読み取りと書き込みをデータベースから単純な web アプリケーションを作成します。 参照してください、 [ASP.NET MVC ラーニング センター](../../../index.md)チュートリアルとサンプルは、その他の ASP.NET MVC を検索します。


しましょう最初 ASP.NET MVC Web アプリケーションを使用して、 [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)します。 少しのムービー リスト アプリケーションをお知らせを作成し、ムービーの一覧を確認しましょう。

## <a name="what-youll-build"></a>構築します

ここでは、アプリケーションをビルドの 2 つのスクリーン ショットです。 さまざまな列を持つ映画の単純なテーブルがあります。

[![Mリスト - ovie Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

フォームの作成は、ムービーの一覧に追加できます必要があります。

[![CWindows Internet Explorer (2) - ムービーの作成 ()](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>学習内容

このチュートリアルでは、Visual Studio を使用して ASP.NET MVC Web アプリケーションの構築の基礎を説明します。 について説明します。

- 新しい ASP.NET MVC プロジェクトを作成する方法
- SQL Server で新しいデータベースを作成する方法
- ASP.NET MVC のコント ローラーとビューを作成する方法
- データ取得して表示する方法
- データを編集し、データの検証を有効にする方法
- データベース スキーマを更新する方法

## <a name="get-started"></a>開始するには

スタート画面から Visual Web Developer 2010 Express (名前を付けます"VWD"ようになりました) と新しいプロジェクトを選択を実行して開始します。

Visual Web Developer は、IDE、または統合開発環境です。 Microsoft Word を使用してドキュメントを記述するのにのと同じようにアプリケーションを作成、IDE を使用します。 およびファイルの選択にも使用してもメニューを使用できるさまざまなオプションを示す上部のツールバーが |新しいプロジェクト。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>最初のアプリケーションを作成します。

Visual Basic または Visual C# を使用してアプリケーションを作成することができます。 ここで、選択 Visual C#、左側の「ASP.NET MVC 2 Web アプリケーション」を選択し、 プロジェクトに"Movies"という名前し、[ok] をクリックします。

[![N新しいプロジェクト](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

右側にあるすべてのファイルとフォルダーを示す、アプリケーションで、ソリューション エクスプ ローラーです。 中央の大きなウィンドウは、コードを編集し、ほとんどの時間を費やす場所には。 Visual Studio は、何もせず、実用的なアプリケーションが現在あるため、作成した ASP.NET MVC プロジェクトの既定のテンプレートを使用! これは、単純な"Hello World! プロジェクト、およびそのは、アプリケーションを起動することをお勧めします。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

ツールバーに「再生」ボタンを選択します。

![デバッグの開始](getting-started-with-mvc-part1/_static/image11.png)

プログラムをコンパイルし、web ブラウザーでアプリケーションを起動する右側に緑色の矢印になります。

*注: 代わりに、キーボードの f5 キーを押して、デバッグを選択または&gt;[デバッグ] メニューからデバッグを開始します。*

これは、結果、Visual Web Developer を開発 web サーバーを起動し、(はありません構成や手動の手順がこれを有効にするために必要)、web アプリケーションを実行します。 ブラウザーを起動し、アプリケーションのホーム ページを参照するように構成には、します。 以下の"localhost"の example.com のようなものであり、ブラウザーのアドレス バーに表示されるに注意してください。 Localhost は常に、ここで作成したアプリケーションを実行している独自のローカル コンピューターをポイントするためです。

[![Home ページ](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

この既定のテンプレートはすぐする 2 つのページにアクセスして、基本的なログイン ページを示します。 このアプリケーションの動作を変更して、プロセスで ASP.NET MVC についてもう少し説明します。 ブラウザーを閉じて、いくつかのコードを変更することができます。

> [!div class="step-by-step"]
> [次へ](getting-started-with-mvc-part2.md)
