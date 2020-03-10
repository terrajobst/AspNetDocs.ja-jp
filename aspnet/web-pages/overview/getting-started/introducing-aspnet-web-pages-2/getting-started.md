---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: はじめに | Microsoft Docs
author: Rick-Anderson
description: WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。 Visual Studio または Visual Studio Code を使用します。 このガイドの内容...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: bb863f8605e6f8faca3b285607b63a3e88e83012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440242"
---
# <a name="getting-started"></a>作業の開始

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。 [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)または[Visual Studio Code](https://code.visualstudio.com/)を使用します。
> 
> 
> このガイダンスとアプリケーションでは、動的 web サイトを作成するための軽量フレームワークである ASP.NET Web ページ (バージョン2以降) と Razor 構文の概要を説明します。 また、ページやサイトを作成するためのツールである WebMatrix も導入されています。
> 
> **Level**: ASP.NET Web ページが新しくなります。  
> **想定**されるスキルは、HTML、基本的なカスケードスタイルシート (CSS) です。
> 
> このセットの最初のチュートリアルで学習する内容は次のとおりです。
> 
> - ASP.NET Web ページテクノロジとは何ですか。
> - WebMatrix とは
> - すべてをインストールする方法。
> - WebMatrix を使用して web サイトを作成する方法。
>   
> 
> 説明する機能/テクノロジ:
> 
> - Microsoft Web Platform Installer。
> - WebMatrix.
> - *cshtml*ページ
>   
> 
> Mike Pope はこのチュートリアルを最初に記述しました。 Tom FitzMacken は Microsoft WebMatrix 3 用に更新されました。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - WebMatrix 3

## <a name="what-should-you-know"></a>何を知る必要がありますか。

次のことを理解していることを前提としています。

- **HTML**。 詳細な専門知識は必要ありません。 HTML については説明しませんが、複雑なものは使用しません。 HTML チュートリアルへのリンクが用意されているので、それが役に立つと思います。
- **カスケードスタイルシート (CSS)** 。 HTML の場合と同じです。
- **基本的なデータベースアイデア**。 データにスプレッドシートを使用し、データの並べ替えとフィルター処理を行った経験があれば、このチュートリアルセットでは一般的に想定しています。

また、基本的なプログラミングの学習に関心があることを前提としています。 ASP.NET Web ページは、C# と呼ばれるプログラミング言語を使用します。 プログラミングの背景を必要とすることはありません。 以前に web ページで JavaScript を記述したことがある場合は、背景が十分にあります。

プログラミングに習熟している場合は、このチュートリアルの初期段階では、新しいプログラマが速度を向上させるため、このチュートリアルの設定が遅くなる可能性があることに注意してください。 ただし、最初のいくつかのチュートリアルでは説明しませんが、基本的なプログラミングについては説明しません。

## <a name="what-do-you-need"></a>必要なものは何ですか?

次のものが必要です。

- Windows 8、Windows 7、Windows Server 2008、または Windows Server 2012 を実行しているコンピューター。
- ライブインターネット接続。
- 管理者特権 (インストールプロセスに必要)。

## <a name="what-is-aspnet-web-pages"></a>ASP.NET Web ページとは

ASP.NET Web ページは、動的な Web ページを作成するために使用できるフレームワークです。 単純な HTML web ページは静的です。その内容は、ページ内の固定 HTML マークアップによって決定されます。 ASP.NET Web ページで作成したような動的ページでは、コードを使用して、その場でページコンテンツを作成できます。

動的ページを使用すると、あらゆる種類の操作を実行できます。 フォームを使用してユーザーに入力を要求してから、ページに表示される内容や外観を変更することができます。 ユーザーから情報を取得してデータベースに保存し、後で一覧表示することができます。 サイトから電子メールを送信できます。 Web 上の他のサービス (たとえば、マッピングサービス) と対話し、それらのソースの情報を統合するページを生成することができます。

## <a name="what-is-webmatrix"></a>WebMatrix とは

WebMatrix は、web ページエディター、データベースユーティリティ、ページをテストするための web サーバー、および web サイトをインターネットに公開する機能を統合するツールです。 WebMatrix は無料で、簡単にインストールでき、簡単に使用できます。 (これは、単純な HTML ページだけでなく、PHP などの他のテクノロジにも使用できます)。

実際には、WebMatrix を使用して ASP.NET Web ページを操作する*必要はあり*ません。 たとえば、アクセス権のある web サーバーを使用して、テキストエディターやテストページを使用してページを作成できます。 ただし、WebMatrix を使用すると非常に簡単になります。そのため、これらのチュートリアルでは、全体を通じて WebMatrix を使用します。

## <a name="about-these-tutorials"></a>これらのチュートリアルについて

このチュートリアルセットでは、ASP.NET Web ページの使用方法について説明します。 この入門用チュートリアルでは、合計9つのチュートリアルがあります。 これは、初心者向けの web サイトを作成するために ASP.NET Web ページ初心者からの一連のチュートリアルの一部です。

この最初のチュートリアルでは、ASP.NET Web ページを操作する方法の基本を示します。 完了したら、このチュートリアルの終了位置を確認し、Web ページをより詳細に調べるための追加のチュートリアルセットを操作できます。

詳細については、簡単に説明します。 また、このチュートリアルでは、理解しやすい方法を常に選択します。 後のチュートリアルでは、より詳細な説明を設定し、より効率的で柔軟なアプローチを示します (さらに楽しい)。 ただし、これらのチュートリアルでは、まず基本を理解する必要があります。

先ほど開始したチュートリアルでは、次の ASP.NET Web ページの機能について説明します。

- すべてのインストールについて説明します。 (これは、お読みのチュートリアルに含まれています)。
- ASP.NET Web ページプログラミングの基本。
- データベースを作成する。
- ユーザー入力フォームの作成と処理。
- データベース内のデータの追加、更新、および削除。

## <a name="what-will-you-create"></a>何を作成しますか?

このチュートリアルでは、次のチュートリアルを設定し、必要な映画を一覧表示できる web サイトを中心にしています。 映画を入力して編集し、一覧表示することができます。 このチュートリアルセットで作成するページのいくつかを次に示します。 最初の例では、作成するムービーリストページを示しています。

![ムービーの一覧を表示しているムービーアプリ](getting-started/_static/image1.png)

次のページで、サイトに新しい映画情報を追加できます。

![[ムービーの追加] ページを表示したムービーアプリが完成しました](getting-started/_static/image2.png)

以降のチュートリアルでは、このセットにビルドを設定し、画像のアップロード、個人のログイン、電子メールの送信、ソーシャルメディアとの統合などの機能を追加します。

## <a name="see-this-app-running-on-azure"></a>このアプリが Azure で実行されていることを確認する

完成したサイトがライブ web アプリとして実行されていることを確認しますか? 次のボタンをクリックするだけで、アプリの完全なバージョンを Azure アカウントにデプロイできます。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

このソリューションを Azure にデプロイするには、Azure アカウントが必要です。 まだアカウントを持っていない場合は、次のオプションがあります。

- [無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。
- [Msdn サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にする-msdn サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。

## <a name="installing-everything"></a>すべてをインストールする

Microsoft の Web Platform Installer を使用して、すべてをインストールできます。 実際には、インストーラーをインストールし、それを使用して他のすべてをインストールします。

Web ページを使用するには、Windows XP SP3 以降、または Windows Server 2008 以降がインストールされている必要があります。

ASP.NET web サイトの [ [Web ページ] ページ](../../../index.md)で、 **[インストール]** をクリックします。

![ASP.NET Web サイトを表示 &quot;WebMatrix&quot; ボタンをインストールする](getting-started/_static/image3.png)

WebMatrix をインストールする前に、ライセンス条項およびプライバシーに関する声明に同意するように求められます。

![条項に同意してインストールを開始する](getting-started/_static/image4.png)

**[実行]** をクリックしてインストールを開始します。 (インストーラーを保存する場合は、 **[保存]** をクリックし、保存したフォルダーからインストーラーを実行します)。

![](getting-started/_static/image5.png)

Web Platform Installer が表示され、WebMatrix をインストールできるようになります。 **[インストール]** をクリックします。

![](getting-started/_static/image6.png)

インストールプロセスでは、コンピューターにインストールする必要があることが確認され、プロセスが開始されます。 インストールが必要な内容によっては、処理に数分から数分かかることがあります。 [**同意**する] を選択して、ライセンス条項に同意します。

## <a name="hello-webmatrix"></a>Hello, WebMatrix

完了すると、インストールプロセスによって WebMatrix が自動的に起動されます。 そうでない場合は、Windows の **[スタート]** メニューから**Microsoft WebMatrix**を起動します。

WebMatrix を初めて起動すると、Microsoft アカウントで Microsoft Azure にサインインする機会が与えられます。 サインインすると、Azure を通じて10個の無料 web アプリを受け取ることができます。 これらの無料の web アプリは、アプリをテストするための便利な方法を提供します。 まだ Azure アカウントを持っていないが、MSDN サブスクリプションをお持ちの場合は、 [msdn サブスクリプションの特典を有効](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にすることができます。 それ以外の場合は、無料試用版アカウントを数分で作成できます。 詳細については、「[Azure の無料試用版サイト](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)」を参照してください。

このチュートリアルを続行するには、すぐにサインインする必要はありません。 サインインしていない場合でも、後でサインインすることができます。 このチュートリアルシリーズの最後の[トピック](publishing.md)では、web サイトを Azure にデプロイする方法について説明します。そのため、このトピックを完了するにはサインインする必要があります。

この時点で、Microsoft アカウントを使用してサインインするか、右下隅にある [いいえ]**を選択し**ます。

![Sign In (Azure: サインイン)](getting-started/_static/image7.png)

まず、空の web サイトを作成し、ページを追加します。 このセットの後のチュートリアルでは、組み込みの web サイトテンプレートの1つを使用します。

開始 ウィンドウで、**新規** をクリックします。

![WebMatrix の起動画面](getting-started/_static/image8.png)

テンプレートは、さまざまな種類の web サイトの事前に構築されたファイルとページです。 既定で使用できるすべてのテンプレートを表示するには、[テンプレートギャラリー] オプションを選択します。

![テンプレートギャラリーの選択](getting-started/_static/image9.png)

**[クイックスタート]** ウィンドウで、 **ASP.NET**グループの **[空のサイト]** を選択し、新しいサイトに "web 映画" という名前を指定します。

![空のサイトテンプレートが選択されている WebMatrix クイックスタートウィンドウ](getting-started/_static/image10.png)

**[次へ]** をクリックします。

Microsoft アカウントにサインインしている場合は、Azure にサイトを作成する機会が与えられます。 サイトの名前に基づいて、 **WebPagesMovies.azurewebsites.net**の既定の名前が推奨されます。ただし、感嘆符は、この名前が Windows Azure で使用できないことを示します。 わかりやすくするために、 **[スキップ]** を選択して、今すぐ Azure での web サイトの作成をバイパスします。 このシリーズの後半では、このサイトを Azure に発行します。

![azure サイトの作成](getting-started/_static/image11.png)

WebMatrix は、サイトを作成して開きます。

![WebMatrix で開かれる新しい Webweb ムービーサイト](getting-started/_static/image12.png)

上部には、クイックアクセスツールバーとリボンがあります。 左下には、タスク (**サイト**、**ファイル**、**データベース**、**レポート**) を切り替えるワークスペースセレクターが表示されます。 右側には、エディターのコンテンツウィンドウとレポートが表示されます。 下部には、メッセージの通知バーが表示されることがあります。

WebMatrix とその機能の詳細については、これらのチュートリアルを参照してください。

## <a name="creating-a-web-page"></a>Web ページの作成

WebMatrix と ASP.NET Web ページについて理解を深めるには、簡単なページを作成します。

ワークスペースセレクターで、 **[ファイル]** ワークスペースを選択します。 このワークスペースを使用すると、ファイルとフォルダーを操作できます。 左側のウィンドウには、サイトのファイル構造が表示されます。 リボンが変更され、ファイル関連のタスクが表示されます。

![WebMatrix のファイルワークスペース](getting-started/_static/image13.png)

リボンで、 **[新規]** の下の矢印をクリックし、 **[新しいファイル]** をクリックします。

![リボンの [新しい&quot; の &quot;] コマンドを使用して新しいファイルを作成する](getting-started/_static/image14.png)

WebMatrix では、ファイルの種類の一覧が表示されます。 **[CSHTML]** を選択し、 **[名前]** ボックスに「HelloWorld」と入力します。 CSHTML ページは ASP.NET Web ページページです。

![HelloWorld という名前の新しい CSHTML ページを作成します。](getting-started/_static/image15.png)

**[OK]** をクリックします。

WebMatrix によってページが作成され、エディターで開かれます。

![WebMatrix エディターの新しい HelloWorld ページ](getting-started/_static/image16.png)

ご覧のように、このページにはほとんどの通常の HTML マークアップが含まれています。ただし、上部には次のようなブロックがあります。

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

これはコードを追加するためのものです。後で説明します。

ページのさまざまな部分には、要素名、属性、テキスト、および上部にあるブロック &mdash;、すべて異なる色が付いていることに注意してください。 これを*構文の強調表示*と呼びます。これにより、すべてを明確に保つことができます。 これは、WebMatrix で web ページを簡単に操作できるようにする機能の1つです。

次の例のように、`<head>` と `<body>` の要素の内容を追加します。 (必要に応じて、次のブロックをコピーし、既存のページ全体をこのコードで置き換えることができます)。

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

クイックアクセスツールバーまたは **[ファイル]** メニューの **[保存]** をクリックします。

![WebMatrix クイックアクセスツールバーの [保存] ボタン](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>ページのテスト

**[ファイル]** ワークスペースで、 *HelloWorld*ページを右クリックし、 **[ブラウザーで起動]** をクリックします。

![WebMatrix リボンの [実行] ボタンを使用したページの実行](getting-started/_static/image18.png)

WebMatrix では、コンピューター上のページをテストするために使用できる、組み込みの web サーバー (IIS Express) を起動します。 (WebMatrix で IIS Express を使用しない場合は、テストする前に、web サーバーにページを発行する必要があります)。ページが既定のブラウザーに表示されます。

![ブラウザーで実行されている Hello World&quot; ページの &quot;](getting-started/_static/image19.png)

WebMatrix でページをテストすると、ブラウザーの URL は、 *localhost*がローカルサーバーを参照する `http://localhost:33651/HelloWorld.cshtml.` のようになります。つまり、ページは自分のコンピューター上の web サーバーによって処理されることに注意してください。 前述のように、WebMatrix には、ページの起動時に実行される IIS Express という名前の web サーバープログラムが含まれています。

*Localhost*の後の番号 ( *localhost: 33651*など) は、コンピューター上の*ポート番号*を参照します。 これは、この特定の web サイトに IIS Express が使用する "チャネル" の番号です。 ポート番号は、サイトの作成時に 1024 ~ 65536 の範囲でランダムに選択されます。これは、作成するサイトごとに異なります。 (独自のサイトをテストする場合、ポート番号は、ほぼ確実に33561とは異なる数値になります)。Web サイトごとに異なるポートを使用することにより、IIS Express は、通信先のサイトを直接保つことができます。

後でパブリック web サーバーにサイトを発行すると、URL に*localhost*が表示されなくなります。 その時点で、`http://myhostingsite/mywebsite/HelloWorld.cshtml` などの一般的な URL やページが表示されます。 サイトの発行の詳細については、このチュートリアルシリーズの後半で説明します。

## <a name="adding-some-server-side-code"></a>サーバー側コードの追加

ブラウザーを閉じて、WebMatrix のページに戻ります。

コードブロックに行を追加して、次のコードのようにします。

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

これは、いくつかの Razor コードです。 現在の日付と時刻が取得され、その値が `currentDateTime`という名前の*変数*に格納されていることは明らかです。 Razor 構文の詳細については、次のチュートリアルを参照してください。

ページの本文で、`<p>Hello World!</p>` 要素の後に次を追加します。

[!code-html[Main](getting-started/samples/sample4.html)]

このコードは、`currentDateTime` 変数に格納した値を上部に取得し、その値をページのマークアップに挿入します。 `@` 文字は、ページ内の ASP.NET Web ページコードをマークします。

ページをもう一度実行します (WebMatrix はページを実行する前に変更を保存します)。 今度は、ページに日付と時刻が表示されます。

![動的に生成された時間表示でブラウザーで実行されている Hello World&quot; ページを &quot;](getting-started/_static/image20.png)

しばらく待ってから、ブラウザーでページを更新してください。 日付と時刻の表示が更新されます。

ブラウザーでページソースを確認します。 次のマークアップに似ています。

[!code-html[Main](getting-started/samples/sample5.html)]

上部に `@{ }` ブロックがないことに注意してください。 また、日付と時刻`1/18/2012 2:49:50 PM` 表示に `@currentDateTime` は、 *..........................................* ここでの変更点は、ページを実行したときに、`@`でマークされたすべてのコード (この場合はごくわずか) が ASP.NET によって処理されたことです。 コードによって出力が生成され、その出力がページに挿入されました。

## <a name="this-is-what-aspnet-web-pages-are-about"></a>ASP.NET Web ページは次のとおりです。

ここでは、動的な Web コンテンツを作成 ASP.NET Web ページについて説明します。 先ほど作成したページには、前に見たものと同じ HTML マークアップが含まれています。 また、あらゆる種類のタスクを実行できるコードを含めることもできます。 この例では、現在の日付と時刻を取得するという単純なタスクを実行しました。 ご覧のとおり、HTML を使用してコードを intersperse し、ページに出力を生成することができます。 他の*ユーザーがブラウザーで ASP.NET ページを*要求すると、web サーバーの途中でページが処理されます。 ASP.NET は、コード (存在する場合) の出力を HTML としてページに挿入します。 コード処理が完了すると、ASP.NET によって、結果のページがブラウザーに送信されます。 すべてのブラウザーは HTML です。 次に図を示します。

![ASP.NET が HTML を動的に生成する方法の概念フロー](getting-started/_static/image21.png)

この考え方は単純ですが、コードが実行できる多くの興味深いタスクがあります。また、HTML コンテンツをページに動的に追加するための多くの興味深い方法があります。 また、HTML ページと同様に *、ASP.NET ページ*には、ブラウザー自体 (JavaScript および jQuery コード) で実行されるコードを含めることもできます。 ここでは、このチュートリアルセットとそれ以降の手順について説明します。

## <a name="coming-up-next"></a>次へ

このシリーズの次のチュートリアルでは、ASP.NET Web ページプログラミングについてもう少し詳しく説明します。

## <a name="additional-resources"></a>その他のリソース

[ASP.NET web サイトを最初から作成](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)します。 これは、(ASP.NET Web ページではなく) WebMatrix の使用について具体的に説明したチュートリアルです。 このチュートリアルでは説明しませんが、WebMatrix の追加機能のいくつかについてもう少し詳しく説明します。

> [!div class="step-by-step"]
> [Next](intro-to-web-pages-programming.md)
