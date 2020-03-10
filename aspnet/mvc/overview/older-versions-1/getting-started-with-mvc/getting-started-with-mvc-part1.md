---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC の概要 |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469798"
---
# <a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 入門

[Scott マン Selman](https://github.com/shanselman)

> > [!NOTE]
> > このチュートリアルが使用可能な場合は、 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)を[使用して](../../getting-started/introduction/getting-started.md)更新されたバージョンです。 このチュートリアルでは、ASP.NET MVC 5 を使用します。このチュートリアルでは、多くの機能強化が行われています。
>
>
> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)を使用して最初の ASP.NET MVC Web アプリケーションを作成しましょう。 ムービーの作成と一覧表示を行うための小さなムービーリストアプリケーションを作成します。

## <a name="what-youll-build"></a>作成するアプリケーション:

ここでは、作成するアプリケーションの2つのスクリーンショットを示します。 さまざまな列を含む単純な映画のテーブルが作成されます。

[![ムービーの一覧-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

また、ムービーをリストに追加できるように、フォームが作成されます。

[![ムービーを作成する-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>学習内容

このチュートリアルでは、Visual Studio を使用して ASP.NET MVC Web アプリケーションを構築する方法の基本について説明します。 学習内容:

- 新しい ASP.NET MVC プロジェクトを作成する方法
- SQL Server を使用して新しいデータベースを作成する方法
- ASP.NET MVC コントローラーとビューを作成する方法
- データを取得して表示する方法
- データを編集し、データの検証を有効にする方法
- データベーススキーマを更新する方法

## <a name="get-started"></a>開始するには

まず、Visual Web Developer 2010 Express を実行します (ここでは "VWD" と呼ばれます)。スタート画面から [新しいプロジェクト] を選択します。

Visual Web Developer は、IDE または統合開発環境です。 Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。 上部には、使用可能なさまざまなオプションが表示されているツールバーがあります。また、[ファイル] を選択するために使用できるメニューもあります。新しいプロジェクト。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>最初のアプリケーションの作成

Visual Basic または Visual C# を使用してアプリケーションを作成することができます。 ここで、選択 Visual C#、左側の「ASP.NET MVC 2 Web アプリケーション」を選択し、 プロジェクトに"Movies"という名前し、[ok] をクリックします。

[新しいプロジェクトの ![](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

右側には、アプリケーション内のすべてのファイルとフォルダーが表示されるソリューションエクスプローラーます。 中央の大きなウィンドウでは、コードを編集し、ほとんどの時間を費やすことができます。 Visual Studio では、先ほど作成した ASP.NET MVC プロジェクトの既定のテンプレートが使用されているため、何もしなくても、すぐに動作するアプリケーションがあります。 これは単純な "Hello World です。 プロジェクトは、アプリケーションを開始するのに最適な場所です。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

ツールバーの [再生] ボタンを選択します。

![[デバッグ]](getting-started-with-mvc-part1/_static/image11.png)

これは、プログラムをコンパイルし、web ブラウザーでアプリケーションを起動する、右側を指す緑色の矢印です。

*注: 代わりに、キーボードの F5 キーを押すか、[デバッグ] メニューの [デバッグ] を選択して [デバッグ] を&gt;ます。*

これにより、Visual Web Developer は開発 web サーバーを起動し、web アプリケーションを実行します (これを有効にするために必要な構成や手動の手順はありません)。 その後、ブラウザーが起動し、アプリケーションのホームページを参照するように構成されます。 以下のように、ブラウザーのアドレスバーには "localhost" と表示されており、example.com のようなものではないことに注意してください。 これは、localhost は常に独自のローカルコンピューターを指しているためです。この場合、この例では、先ほど作成したアプリケーションが実行されています。

[![ホームページ](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

すぐに使用できる既定のテンプレートでは、2つのページにアクセスでき、基本的なログインページが表示されます。 このアプリケーションの動作を変更し、プロセスでの ASP.NET MVC について少し説明しましょう。 ブラウザーを閉じ、コードを変更します。

> [!div class="step-by-step"]
> [Next](getting-started-with-mvc-part2.md)
