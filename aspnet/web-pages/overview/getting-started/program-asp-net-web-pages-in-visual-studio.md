---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor) |Microsoft Docs
author: Rick-Anderson
description: この付録では、Visual Studio 2010 または Visual Web Developer 2010 Express を使用して、Razor 構文で ASP.NET Web ページをプログラミングする方法について説明します。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514294"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor)

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Visual Studio または Visual Web Developer Express を使用して ASP.NET Web ページ (Razor) web サイトをプログラミングする方法について説明します。
>
> 学習内容
>
> - お使いのバージョンの Visual Studio で ASP.NET Web ページを操作するために必要なもの (ある場合)。
> - Visual Web Developer 2010 Express に ASP.NET Web ページのサポートを追加する方法について説明します。
> - Visual Studio の機能を使用して、IntelliSense やデバッガーなどの ASP.NET Razor ページを操作する方法について説明します。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - ASP.NET Web ページ (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> このチュートリアルは、ASP.NET Web ページ2、Visual Studio 2012、Visual Studio 2010、および WebMatrix 2 でも動作します。

WebMatrix または他の多くのコードエディターを使用して Razor 構文で ASP.NET Web ページをプログラミングできます。 Microsoft Visual Studio を使用することもできます。これは、web サイトだけではなく、さまざまな種類のアプリケーションを作成するための強力なツールセットを提供する、フル機能の統合開発環境 (IDE) です。 ASP.NET Razor ページを操作するには、 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用できます。

ASP.NET Razor web ページを使用したプログラミングのために Visual Studio が提供する、次の2つの便利な機能があります。

- *IntelliSense*。 Visual Studio に組み込まれている IntelliSense 機能は、WebMatrix の IntelliSense よりも包括的です。
- *デバッガー*。 デバッガーを使用すると、実行中のプログラムを停止したり、変数を調べたり、コードを行ごとにステップ実行したりして、コードのトラブルシューティングを行うことができます。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>異なるバージョンの ASP.NET Web ページでの Visual Studio の使用

Visual Studio 2017 で ASP.NET web アプリを開発するには、 **ASP.NET と web 開発**ワークロードをインストールします。

Visual Studio 2012 および Visual Studio 2013 には ASP.NET Web ページのサポートが含まれています。 (ASP.NET Web ページをサポートするために必要なパッケージは、Visual Studio のインストール時にインストールされます)。

Visual Studio 2010 では、ASP.NET Web ページの既定のサポートは含まれていません。 Visual Studio 2010 で ASP.NET Web ページを使用するには、ASP.NET MVC パッケージをインストールする必要があります。 ASP.NET Web ページ2を取得するには、ASP.NET MVC 4 をインストールします。

次の表は、さまざまなバージョンの Visual Studio での ASP.NET Web ページのサポートをまとめたものです。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET Web ページ2** | ASP.NET MVC 4 をインストールする | 含める | 含める |
| **ASP.NET Web ページ3** |  | NuGet を使用して ASP.NET Web ページ3に更新する | 含める |

Visual Studio 2010 を使用するには、「 [Visual studio 2010 での ASP.NET Web ページのサポートのインストール](#vs2010support)」を参照してください。

## <a name="launching-visual-studio-from-webmatrix"></a>WebMatrix からの Visual Studio の起動

WebMatrix でプロジェクトを開始し、Visual Studio に切り替えたい場合は、Visual Studio で簡単にプロジェクトを開くためのボタンが WebMatrix に用意されています。 このボタンを有効にするには、コンピューターに Visual Studio がインストールされている必要があります。 次の図は、WebMatrix のボタンを示しています。

![Visual Studio を起動する](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

このボタンをクリックすると、Visual Studio でプロジェクトが開きます。 WebMatrix と Visual Studio は、問題なく切り替えることができます。 他の環境でファイルが変更された場合は通知されます。最新の変更を取得するには、ファイルを再読み込みする必要があります。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Visual Studio での ASP.NET Razor サイトの作成

Visual Studio で ASP.NET Razor web サイトを作成するには、次のようにします。

1. Visual Studio を開きます。
2. **[ファイル]** メニューの **[新しい Web サイト]** をクリックします。

    ![新しい web サイトの作成](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. **[新しい Web サイト]** ダイアログボックスで、使用する言語 (ビジュアルC#または Visual Basic) を選択します。
4. **[ASP.NET Web Site (Razor)]** テンプレートを選択します。

    ![razor サイト](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **[OK]** をクリックします。

新しいプロジェクトが存在し、作業を開始するのに役立ついくつかの既定の web ページが表示されます。

### <a name="using-intellisense"></a>IntelliSense の使用

サイトを作成したので、Visual Studio での IntelliSense の動作を確認できます。

1. 先ほど作成した web サイトで、既定の [ *cshtml* ] ページを開きます。
2. ページの `<h3>` タグの後に、「`@ServerInfo.` (ドットを含む)」と入力します。 IntelliSense によって、`ServerInfo` ヘルパーの使用可能なメソッドがドロップダウンリストに表示されることに注意してください。

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 一覧から `GetHtml` メソッドを選択し、enter キーを押します。 IntelliSense は、メソッドを自動的に入力します。 (のC#メソッドと同様に、メソッドの後に `()` 文字を追加する必要があります)。`GetHtml` メソッドの完成したコードは、次の例のようになります。

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Ctrl キーを押しながら F5 キーを押して、ページを実行します。 ブラウザーに表示された場合、ページは次のようになります。

    ![ブラウザーの既定のページ](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. ブラウザーを閉じます。

### <a name="using-the-debugger"></a>デバッガーの使用

1. *既定の cshtml*ページの先頭で、`Page.Title`で始まる行の後に、次のコード行を追加します。

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. コードの左側にあるエディターの灰色の余白で、*ブレークポイント*を追加するために、この新しい行の横をクリックします。 ブレークポイントは、その時点でプログラムの実行を停止するようにデバッガーに指示するマーカーで、何が起こっているかを確認できます。

    ![ブレークポイントの設定](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. `ServerInfo.GetHtml` メソッドの呼び出しを削除し、その場所に `@myTime` 変数の呼び出しを追加します。 この呼び出しでは、新しいコード行によって返される現在の時刻値が表示されます。
4. F5 キーを押して、デバッガーでページを実行します。 設定したブレークポイントでページが停止します。 次の図は、エディターでのページの表示とブレークポイント (黄色) を示しています。

    ![ブレークポイントのデバッグ](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. デバッグ ツールバーで、**ステップイン** ボタンをクリックするか、F11 キーを押して次のコード行を実行します。 このボタンをクリックするたびに、実行を次のコード行に進めます。

    ![[ステップイン] ボタン](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. `myTime` 変数の値を確認するには、マウスポインターをその上に置くか、 **[ローカル]** ウィンドウと **[呼び出し履歴]** ウィンドウに表示されている値を調べます。 Visual Studio では、変数の値が表示されます。

    ![時間値の表示](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 変数を調べてコードをステップ実行したら、F5 キーを押して、各行で停止することなくページの実行を続けます。 すべてのコードのステップ実行が完了すると、ブラウザーにページが表示されます。

デバッガーの詳細と、Visual Studio でコードをデバッグする方法の詳細については、「[チュートリアル: Visual Web Developer での Web ページのデバッグ](https://msdn.microsoft.com/library/z9e7w6cs.aspx)」を参照してください。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Visual Studio での ASP.NET MVC プロジェクトでの Razor の使用

Razor 構文は、ASP.NET MVC プロジェクトでも広く使用されています。 MVC は、動的な web サイトを構築するための強力なパターンベースの方法です。 ASP.NET Web ページサイトの保守が困難になった場合は、ASP.NET MVC アプリケーションに変換することを検討してください。 MVC アプリケーションを作成する例については、「[はじめに with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)」を参照してください。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010 での ASP.NET Web ページのサポートのインストール

このセクションでは、Visual Web Developer Express 2010 と ASP.NET Web ページ Tools for Visual Studio をインストールする方法について説明します。

1. Web Platform Installer をまだ持っていない場合は、次の URL からダウンロードしてください。

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Web Platform Installer を実行します。
3. **[製品]** タブをクリックします。

    ![WebPI 製品タブ](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. **ASP.NET MVC 4** (ASP.NET Web ページ 2) を検索し、 **[追加]** をクリックします。 これらの製品には、ASP.NET Razor web サイトをビルドするための Visual Studio ツールが含まれています。

    ![WebPi インストールオプション](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. **[インストール]** をクリックしてインストールを完了します。
