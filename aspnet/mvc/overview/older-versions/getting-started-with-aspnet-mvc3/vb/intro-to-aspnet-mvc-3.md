---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 の概要 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485494"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>ASP.NET MVC 3 入門 (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 必要に応じC#て[ C# ](../cs/intro-to-aspnet-mvc-3.md) 、このチュートリアルのバージョンに切り替えます。

このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。

- [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)

Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

このトピックには、VB ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB バージョンをこちらからダウンロードして](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)ください。 CSharp を使用する場合は、このチュートリアルの[csharp バージョン](../cs/intro-to-aspnet-mvc-3.md)に切り替えてください。

## <a name="what-youll-build"></a>作成するアプリケーション:

データベースからのムービーの作成、編集、および一覧表示をサポートする単純なムービーリスティングアプリケーションを実装します。 ビルドするアプリケーションの2つのスクリーンショットを次に示します。 これには、データベースからムービーの一覧を表示するページが含まれています。

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

また、このアプリケーションでは、ムービーの追加、編集、削除を行うことができます。また、個々のムービーの詳細も確認できます。 すべてのデータ入力シナリオには、データベースに格納されているデータが正しいことを確認するための検証が含まれます。

[CreateFormSo の ![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>学習内容

ここでは次の内容について学習します。

- 新しい ASP.NET MVC プロジェクトを作成する方法
- Entity Framework code first を使用して新しいデータベースを作成する方法
- ASP.NET MVC コントローラーとビューを作成する方法
- データを取得して表示する方法
- データを編集し、データの検証を有効にする方法

## <a name="getting-started"></a>作業の開始

Visual Web Developer 2010 Express (短い場合は "VWD") を実行し、**スタート**ページで **[新しいプロジェクト]** を選択します。

Visual Web Developer は、IDE または統合開発環境です。 Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。 Visual Web Developer には、さまざまなオプションが表示されているツールバーが上部にあります。 IDE でタスクを実行する別の方法を提供するメニューもあります。 (たとえば、**スタート**ページで **[新しいプロジェクト]** を選択する代わりに、メニューを使用して [**ファイル**&gt;**新しいプロジェクト**] を選択できます)。

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>最初のアプリケーションの作成

プログラミング言語として Visual Basic またはビジュアルC#のいずれかを選択して、アプリケーションを作成できます。 このチュートリアルでは、左側の Visual Basic を選択し、 **ASP.NET MVC 3 Web アプリケーション** を選択します。 プロジェクトに "MvcMovie" という名前を入力し、[ **OK]** をクリックします。

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

**[New ASP.NET MVC 3 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択します。 既定のビューエンジンとして**Razor**をそのまま使用します。

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

**[OK]** をクリックします。 Visual Web Developer では、作成した ASP.NET MVC プロジェクトの既定のテンプレートを使用しています。これにより、何も実行することなく、すぐに動作するアプリケーションが完成しました。 これは単純な "Hello World!" です。 プロジェクトは、アプリケーションを起動するのに適した場所です。

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

**[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

![](intro-to-aspnet-mvc-3/_static/image11.png)

デバッグを開始するためのキーボードショートカットが F5 キーになっていることに注意してください。

F5 キーを押すと、Visual Web Developer によって開発 web サーバーが起動され、web アプリケーションが実行されます。 その後、VWD はブラウザーを起動し、アプリケーションのホームページを開きます。 ブラウザーのアドレスバーには `localhost` が表示され、`example.com`のようなものではないことに注意してください。 これは、`localhost` が常に独自のローカルコンピューターを指しているためです。この場合は、先ほど作成したアプリケーションが実行されています。 VWD で web プロジェクトを実行する場合、プロジェクトにはランダムなポートが使用されます。 次の図では、ランダムポート番号は43246です。 プロジェクトでは、別のポート番号を使用することがあります。

![](intro-to-aspnet-mvc-3/_static/image12.png)

すぐに使用できる既定のテンプレートでは、2つのページにアクセスでき、基本的なログインページが表示されます。 このアプリケーションの動作を変更し、プロセスでの ASP.NET MVC について少し説明しましょう。 ブラウザーを閉じて、コードを変更してみましょう。

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
