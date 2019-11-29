---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 'チュートリアル: SignalR セルフホスト |Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、自己ホスト型 SignalR 2 サーバーを作成する方法と、JavaScript クライアントを使用してそれに接続する方法について説明します。 このチュートリアルで使用されているソフトウェアのバージョン...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74578577"
---
# <a name="tutorial-signalr-self-host"></a>チュートリアル: SignalR 自己ホスト

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> このチュートリアルでは、自己ホスト型 SignalR 2 サーバーを作成する方法と、JavaScript クライアントを使用してそれに接続する方法について説明します。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR バージョン2
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>このチュートリアルでの Visual Studio 2012 の使用
>
>
> このチュートリアルで Visual Studio 2012 を使用するには、次の手順を実行します。
>
> - [パッケージマネージャー](http://docs.nuget.org/docs/start-here/installing-nuget)を最新バージョンに更新します。
> - [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)をインストールします。
> - Web Platform Installer で、 **Visual Studio 2012 の ASP.NET and Web Tools 2013.1**を検索してインストールします。 これにより、 **Hub**などの SignalR クラスの Visual Studio テンプレートがインストールされます。
> - 一部のテンプレート ( **OWIN Startup クラス**など) は使用できません。これらの場合は、代わりにクラスファイルを使用します。
>
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの気に入った点と、ページの下部にあるコメントで改善できることについて、フィードバックをお寄せください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

## <a name="overview"></a>の概要

SignalR サーバーは通常、IIS の ASP.NET アプリケーションでホストされますが、自己ホストライブラリを使用して自己ホスト型 (コンソールアプリケーションや Windows サービスなど) にすることもできます。 このライブラリは、すべての SignalR 2 と同様に、OWIN ([Open Web Interface for .net](http://owin.org)) 上に構築されています。 OWIN は、.NET web サーバーと web アプリケーションの間の抽象化を定義します。 OWIN は、サーバーから web アプリケーションを分離します。これにより、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするために OWIN が理想的になります。

IIS でホストしない理由には、次のようなものがあります。

- Iis を使用しない既存のサーバーファームなど、IIS が利用できないか望ましくない環境。
- IIS のパフォーマンスのオーバーヘッドを回避する必要があります。
- SignalR 機能は、Windows サービス、Azure ワーカーロール、またはその他のプロセスで実行される既存のアプリケーションに追加されます。

パフォーマンス上の理由により、ソリューションが自己ホストとして開発されている場合は、IIS でホストされているアプリケーションをテストしてパフォーマンスの利点を確認することをお勧めします。

このチュートリアルは、次のセクションで構成されています。

- [サーバーの作成](#server)
- [JavaScript クライアントを使用したサーバーへのアクセス](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>サーバーの作成

このチュートリアルでは、コンソールアプリケーションでホストされているサーバーを作成しますが、サーバーは、Windows サービスや Azure worker ロールなどの任意の種類のプロセスでホストすることができます。 Windows サービスで SignalR サーバーをホストするためのサンプルコードについては、「 [Windows サービスでの自己ホスト SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)」を参照してください。

1. 管理者特権で Visual Studio 2013 を開きます。 **[ファイル]** 、 **[新しいプロジェクト]** を選択します。 **[テンプレート]** ウィンドウで、**ビジュアルC#** ノードの下にある **[Windows]** を選択し、 **[コンソールアプリケーション]** テンプレートを選択します。 新しいプロジェクトに "SignalRSelfHost" という名前を指定し、[ **OK]** をクリックします。

    ![](tutorial-signalr-self-host/_static/image1.png)
2. **[ツール]**  >  **[nuget パッケージマネージャー]**  >  **[パッケージマネージャーコンソール]** の順に選択して、nuget パッケージマネージャーコンソールを開きます。
3. パッケージマネージャーコンソールで、次のコマンドを入力します。

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    このコマンドは、SignalR 2 の自己ホストライブラリをプロジェクトに追加します。
4. パッケージマネージャーコンソールで、次のコマンドを入力します。

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    このコマンドは、Owin ライブラリをプロジェクトに追加します。 このライブラリは、ドメイン間のサポートに使用されます。これは、SignalR をホストするアプリケーションと、異なるドメインの web ページクライアントに必要です。 SignalR サーバーと web クライアントを別のポートでホストするため、これは、これらのコンポーネント間の通信に対してクロスドメインを有効にする必要があることを意味します。
5. Program.cs の内容を次のコードで置き換えます。

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    上記のコードには、次の3つのクラスがあります。

    - 実行のプライマリパスを定義する**Main**メソッドを含む**プログラム**。 このメソッドでは、 **Startup**という種類の web アプリケーションが、指定された URL (`http://localhost:8080`) で開始されます。 エンドポイントでセキュリティが必要な場合は、SSL を実装できます。 詳細については[、「方法: SSL 証明書を使用してポートを構成する](https://msdn.microsoft.com/library/ms733791.aspx)」を参照してください。
    - SignalR サーバーの構成を含むクラス (**このチュートリアル**で使用される唯一の構成は `UseCors`) と、`MapSignalR`への呼び出しで、プロジェクト内の任意のハブオブジェクトのルートが作成されます。
    - **Myhub**。アプリケーションがクライアントに提供する SignalR Hub クラスです。 このクラスには、**送信**される1つのメソッドがあります。このメソッドは、クライアントがを呼び出して、接続されている他のすべてのクライアントにメッセージをブロードキャストします。
6. アプリケーションをコンパイルして実行します。 サーバーが実行されているアドレスは、コンソールウィンドウに表示されます。

    ![](tutorial-signalr-self-host/_static/image2.png)
7. 例外 `System.Reflection.TargetInvocationException was unhandled`で実行が失敗した場合は、管理者特権で Visual Studio を再起動する必要があります。
8. 次のセクションに進む前に、アプリケーションを停止します。

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>JavaScript クライアントを使用したサーバーへのアクセス

このセクションでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)と同じ JavaScript クライアントを使用します。 クライアントに対して変更を1つだけ行います。これは、ハブの URL を明示的に定義するためのものです。 自己ホスト型アプリケーションでは、サーバーが接続 URL と (リバースプロキシおよびロードバランサーによる) 同じアドレスにあるとは限りません。そのため、URL を明示的に定義する必要があります。

1. **ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。 **[Web]** ノードを選択し、 **[ASP.NET web アプリケーション]** テンプレートを選択します。 プロジェクトに "JavascriptClient" という名前を指定し、[ **OK]** をクリックします。

    ![](tutorial-signalr-self-host/_static/image3.png)
2. **空**のテンプレートを選択し、残りのオプションは選択解除したままにします。 **[プロジェクトの作成]** を選択します。

    ![](tutorial-signalr-self-host/_static/image4.png)
3. パッケージマネージャーコンソールで、 **[既定のプロジェクト]** ドロップダウンで "JavascriptClient" プロジェクトを選択し、次のコマンドを実行します。

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    このコマンドを実行すると、クライアントに必要な SignalR および JQuery ライブラリがインストールされます。
4. プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 **[Web]** ノードを選択し、[HTML ページ] を選択します。 ページに「 **Default .html**」という名前を指定します。

    ![](tutorial-signalr-self-host/_static/image5.png)
5. 新しい HTML ページの内容を次のコードに置き換えます。 ここで参照されているスクリプトが、プロジェクトの Scripts フォルダー内のスクリプトと一致していることを確認します。

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    次のコード (上記のコードサンプルで強調表示されています) は、「SignalR バージョン 2 beta」にコードをアップグレードするだけでなく、入門チュートリアルで使用したクライアントに対する追加のコードです。 このコード行は、サーバー上の SignalR のベース接続 URL を明示的に設定します。

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. ソリューションを右クリックし、 **[スタートアッププロジェクトの設定]** ... を選択します。 **[マルチスタートアッププロジェクト]** オプションボタンを選択し、両方のプロジェクトの **[アクション]** を **[開始]** に設定します。

    ![](tutorial-signalr-self-host/_static/image6.png)
7. "Default .html" を右クリックし、 **[スタートページとして設定]** を選択します。
8. アプリケーションを実行します。 サーバーとページが起動します。 サーバーが起動する前にページが読み込まれた場合は、web ページの再読み込みが必要になることがあります (または、デバッガーで **[続行]** を選択します)。
9. ブラウザーで、プロンプトが表示されたらユーザー名を入力します。 ページの URL を別のブラウザータブまたはウィンドウにコピーし、別のユーザー名を指定します。 はじめにのチュートリアルのように、ブラウザーウィンドウ間でメッセージを送信することができます。
