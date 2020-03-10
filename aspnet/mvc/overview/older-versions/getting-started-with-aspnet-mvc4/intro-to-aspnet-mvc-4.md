---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 | の概要Microsoft Docs
author: Rick-Anderson
description: このチュートリアルが使用可能な場合は、Visual Studio 2013 を使用して更新されたバージョンです。 新しいチュートリアルでは、ASP.NET MVC 5 を使用します。これにより、
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485278"
---
# <a name="intro-to-aspnet-mvc-4"></a>ASP.NET MVC 4 入門

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルが使用可能な場合は、 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)を[使用して](../../getting-started/introduction/getting-started.md)更新されたバージョンです。 このチュートリアルでは、ASP.NET MVC 5 を使用します。このチュートリアルでは、多くの機能強化が行われています。
>
> このチュートリアルでは、Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)または Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC 4 Web アプリケーションの構築の基本について説明します。 Visual Studio 2012 をお勧めします。このチュートリアルを完了するために、何もインストールする必要はありません。 Visual Studio 2010 を使用している場合は、以下のコンポーネントをインストールする必要があります。 これらのすべてをインストールするには、次のリンクをクリックします。
>
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 4 の WPI インストーラー](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、 [ASP.NET MVC 4 の Wpi インストーラー](https://go.microsoft.com/fwlink/?LinkId=243392)と: [visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)をインストールします。
>
> このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。 [バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)します。
>
> このチュートリアルでは、Visual Studio でアプリケーションを実行します。 また、ホストプロバイダーに展開することによって、インターネット経由でアプリケーションを利用できるようにすることもできます。 Microsoft では、無料の[Windows Azure 試用版アカウント](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)で最大10個の web サイトを無料で提供しています。 Visual Studio web プロジェクトを Windows Azure Web サイトにデプロイする方法の詳細については、「 [ASP.NET web サイトの作成とデプロイ」と「Visual studio での SQL Database](https://docs.microsoft.com/dotnet/azure/)」を参照してください。 このチュートリアルでは、Entity Framework Code First Migrations を使用して、SQL Server データベースを Windows Azure SQL Database (旧称 SQL Azure) に配置する方法についても説明します。
>
> このチュートリアルは、Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) によって作成されました。

## <a name="what-youll-build"></a>作成するアプリケーション:

> [!NOTE]
> このチュートリアルが使用可能な場合は、 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)を[使用して](../../getting-started/introduction/getting-started.md)更新されたバージョンです。 このチュートリアルでは、ASP.NET MVC 5 を使用します。このチュートリアルでは、多くの機能強化が行われています。

データベースからのムービーの作成、編集、検索、および一覧表示をサポートする単純なムービーリスティングアプリケーションを実装します。 ビルドするアプリケーションの2つのスクリーンショットを次に示します。 これには、データベースからムービーの一覧を表示するページが含まれています。

![](intro-to-aspnet-mvc-4/_static/image1.png)

また、このアプリケーションでは、ムービーの追加、編集、削除を行うことができます。また、個々のムービーの詳細も確認できます。 すべてのデータ入力シナリオには、データベースに格納されているデータが正しいことを確認するための検証が含まれます。

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>作業の開始

最初に Visual Studio Express 2012 または Visual Web Developer 2010 Express を実行します。 このシリーズのほとんどのスクリーンショットでは Visual Studio Express 2012 が使用されていますが、このチュートリアルは Visual Studio 2010/SP1、Visual Studio 2012、Visual Studio Express 2012、Visual Web Developer 2010 Express を使用して実行できます。 **スタート**ページで **[新しいプロジェクト]** を選択します。

Visual Studio は、IDE または統合開発環境です。 Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。 Visual Studio には、さまざまなオプションが表示されているツールバーが上部に表示されています。 IDE でタスクを実行する別の方法を提供するメニューもあります。 (たとえば、**スタート**ページで **[新しいプロジェクト]** を選択する代わりに、メニューを使用して [**ファイル**&gt;**新しいプロジェクト**] を選択できます)。

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>最初のアプリケーションの作成

プログラミング言語として Visual Basic または Visual C# を使用してアプリケーションを作成することができます。 左側にC#ある ビジュアル を選択し、 **ASP.NET MVC 4 Web アプリケーション** を選択します。 プロジェクトに MvcMovie Movie &quot;名前を指定し、 **[OK]** をクリックします。&quot;

![](intro-to-aspnet-mvc-4/_static/image4.png)

**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択します。 既定のビューエンジンとして**Razor**をそのまま使用します。

![](intro-to-aspnet-mvc-4/_static/image5.png)

**[OK]** をクリックします。 Visual Studio では、先ほど作成した ASP.NET MVC プロジェクトの既定のテンプレートが使用されているため、何もしなくても、すぐに動作するアプリケーションがあります。 これは単純な &quot;Hello World です。&quot; プロジェクトは、アプリケーションを起動するのに適した場所です。

![](intro-to-aspnet-mvc-4/_static/image6.png)

**[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

![](intro-to-aspnet-mvc-4/_static/image7.png)

デバッグを開始するためのキーボードショートカットが F5 キーになっていることに注意してください。

F5 キーを押すと、Visual Studio が IIS Express 起動し、web アプリケーションが実行されます。 その後、Visual Studio によってブラウザーが起動し、アプリケーションのホームページが開きます。 ブラウザーのアドレスバーには `localhost` が表示され、`example.com`のようなものではないことに注意してください。 これは、`localhost` が常に独自のローカルコンピューターを指しているためです。この場合は、先ほど作成したアプリケーションが実行されています。 Visual Studio で web プロジェクトを実行する場合、web サーバーにはランダムなポートが使用されます。 次の図では、ポート番号は41788です。 アプリケーションを実行すると、別のポート番号が表示されることがあります。

![](intro-to-aspnet-mvc-4/_static/image8.png)

すぐに使用できる既定のテンプレートでは、[ホーム]、[連絡先]、[About] の各ページが表示されます。 また、登録とログイン、および Facebook と Twitter へのリンクもサポートしています。 次の手順では、このアプリケーションの動作を変更し、ASP.NET MVC について少し説明します。 ブラウザーを閉じて、コードを変更してみましょう。

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
