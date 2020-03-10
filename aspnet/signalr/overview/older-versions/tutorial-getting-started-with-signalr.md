---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 'チュートリアル: SignalR 1.x を使用したはじめに |Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR を使用して、HTML ページでリアルタイムチャットアプリケーションを作成します。
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505750"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a>チュートリアル: SignalR 1.x でのはじめに

([パトリック Fletcher](https://github.com/pfletcher)、 [Tim teebken](https://github.com/timlt) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このチュートリアルでは、SignalR を使用してリアルタイムのチャット アプリケーションを作成する方法を示します。 SignalR を空の ASP.NET web アプリケーションに追加し、メッセージを送信および表示する HTML ページを作成します。

## <a name="overview"></a>概要

このチュートリアルでは、簡単なブラウザーベースのチャットアプリケーションを構築する方法を紹介することによって、SignalR の開発について説明します。 SignalR ライブラリを空の ASP.NET web アプリケーションに追加し、クライアントにメッセージを送信するためのハブクラスを作成して、ユーザーがチャットメッセージを送受信できるようにする HTML ページを作成します。 Mvc ビューを使用して MVC 4 でチャットアプリケーションを作成する方法について説明した同様のチュートリアルについては、「[はじめに With SignalR AND MVC 4](index.md)」を参照してください。

> [!NOTE]
> このチュートリアルでは、SignalR のリリース (1.x) バージョンを使用します。 SignalR 1.x と2.0 の間の変更の詳細については、「 [SignalR 1.X プロジェクトのアップグレード](../releases/upgrading-signalr-1x-projects-to-20.md)」を参照してください。

SignalR は、web アプリケーションを構築するためのオープンソースの .NET ライブラリであり、ライブユーザー操作やリアルタイムのデータ更新を必要とします。 例としては、ソーシャルアプリケーション、マルチユーザーゲーム、ビジネスコラボレーション、ニュース、気象、金融更新アプリケーションなどがあります。 これらは、多くの場合、リアルタイムアプリケーションと呼ばれます。

SignalR は、リアルタイムアプリケーションの構築プロセスを簡略化します。 これには、クライアントとサーバー間の接続の管理とクライアントへのコンテンツの更新のプッシュを容易にするための、ASP.NET サーバーライブラリと JavaScript クライアントライブラリが含まれています。 SignalR ライブラリを既存の ASP.NET アプリケーションに追加して、リアルタイムの機能を取得できます。

このチュートリアルでは、次の SignalR の開発タスクについて説明します。

- SignalR ライブラリを ASP.NET web アプリケーションに追加する。
- クライアントにコンテンツをプッシュするハブクラスを作成する。
- Web ページで SignalR jQuery ライブラリを使用して、メッセージを送信し、ハブから更新を表示します。

次のスクリーンショットは、ブラウザーで実行されているチャットアプリケーションを示しています。 新しいユーザーごとに、コメントを投稿し、ユーザーがチャットに参加した後に追加されたコメントを表示することができます。

![チャットインスタンス](tutorial-getting-started-with-signalr/_static/image1.png)

各項

- [プロジェクトを設定する](#setup)
- [サンプルを実行する](#run)
- [コードを確認する](#code)
- [次の手順](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>プロジェクトを設定する

このセクションでは、空の ASP.NET web アプリケーションを作成し、SignalR を追加して、チャットアプリケーションを作成する方法について説明します。

前提条件:

- Visual Studio 2010 SP1 または2012。 Visual Studio がインストールされていない場合は、無料の Visual Studio 2012 Express 開発ツールを入手するには、「 [ASP.NET のダウンロード](https://www.asp.net/downloads)」を参照してください。
- [Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)。 Visual Studio 2012 では、このインストーラーによって、SignalR テンプレートを含む新しい ASP.NET 機能が Visual Studio に追加されます。 Visual Studio 2010 SP1 では、インストーラーは使用できませんが、セットアップ手順の説明に従って SignalR NuGet パッケージをインストールすることによって、このチュートリアルを完了できます。

次の手順では、Visual Studio 2012 を使用して、空の ASP.NET Web アプリケーションを作成し、SignalR ライブラリを追加します。

1. Visual Studio で、ASP.NET 空の Web アプリケーションを作成します。

    ![空の web の作成](tutorial-getting-started-with-signalr/_static/image2.png)
2. [ツール] を選択して**パッケージマネージャーコンソール**を開きます。 **NuGet パッケージマネージャー |パッケージマネージャーコンソール**。 コンソールウィンドウに次のコマンドを入力します。

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    このコマンドは、SignalR 1.x の最新バージョンをインストールします。
3. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] を選択します。 **クラス**。 新しいクラスに**ChatHub**という名前を指定します。
4. **ソリューションエクスプローラー** [スクリプト] ノードを展開します。 JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。

    ![ライブラリ参照](tutorial-getting-started-with-signalr/_static/image3.png)
5. **ChatHub**クラスのコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **新しい項目**。 **[新しい項目の追加]** ダイアログで、 **[グローバルアプリケーションクラス]** を選択し、 **[追加]** をクリックします。

    ![グローバルの追加](tutorial-getting-started-with-signalr/_static/image4.png)
7. Global.asax.cs クラスの指定された `using` ステートメントの後に、次の `using` ステートメントを追加します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. SignalR hub の既定のルートを登録するには、グローバルクラスの `Application_Start` メソッドに次のコード行を追加します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **新しい項目**。 **[新しい項目の追加]** ダイアログで、Html ページ を選択し、 **[追加]** をクリックします。
10. **ソリューションエクスプローラー**で、先ほど作成した HTML ページを右クリックし、 **[スタートページとして設定]** をクリックします。
11. HTML ページの既定のコードを次のコードに置き換えます。

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. プロジェクトの**すべてを保存**します。

<a id="run"></a>

## <a name="run-the-sample"></a>サンプルを実行する

1. F5 キーを押して、プロジェクトをデバッグモードで実行します。 HTML ページがブラウザーインスタンスに読み込まれ、ユーザー名の入力が求められます。

    ![ユーザー名の入力](tutorial-getting-started-with-signalr/_static/image5.png)
2. ユーザー名を入力します。
3. ブラウザーのアドレス行から URL をコピーし、それを使用して2つ以上のブラウザーインスタンスを開きます。 各ブラウザーインスタンスで、一意のユーザー名を入力します。
4. 各ブラウザーインスタンスで、コメントを追加し、 **[送信]** をクリックします。 コメントは、すべてのブラウザーインスタンスに表示されます。

    > [!NOTE]
    > この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。 ハブは、現在のすべてのユーザーにコメントをブロードキャストします。 後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。

    次のスクリーンショットは、3つのブラウザーインスタンスで実行されているチャットアプリケーションを示しています。これらはすべて、1つのインスタンスがメッセージを送信したときに更新されます。

    ![チャットブラウザー](tutorial-getting-started-with-signalr/_static/image6.png)
5. **ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。 SignalR ライブラリによって実行時に動的に生成される**ハブ**という名前のスクリプトファイルがあります。 このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。

    ![生成されたハブスクリプト](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>コードを確認する

SignalR chat アプリケーションでは、2つの基本的な SignalR 開発タスクを示しています。サーバー上の主要な調整オブジェクトとしてハブを作成し、SignalR jQuery ライブラリを使用してメッセージを送受信します。

### <a name="signalr-hubs"></a>SignalR Hubs

コードサンプルでは、 **ChatHub**クラスは**SignalR**クラスから派生しています。 **ハブ**クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。 ハブクラスにパブリックメソッドを作成し、web ページの jQuery スクリプトからメソッドを呼び出すことによって、これらのメソッドにアクセスできます。

チャットコードでは、クライアントは**ChatHub**メソッドを呼び出して、新しいメッセージを送信します。 ハブは、 **broadcastMessage**を呼び出すことによって、すべてのクライアントにメッセージを送信します。

**Send**メソッドは、いくつかのハブの概念を示しています。

- クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。
- このハブに接続されているすべてのクライアントにアクセスするには、 **SignalR**動的プロパティを使用します。
- クライアントの jQuery 関数 (`broadcastMessage` 関数など) を呼び出して、クライアントを更新します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR と jQuery

コードサンプルの HTML ページは、SignalR jQuery ライブラリを使用して SignalR hub と通信する方法を示しています。 コードの重要なタスクは、ハブを参照するようにプロキシを宣言し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言し、ハブにメッセージを送信するための接続を開始することです。

次のコードでは、ハブのプロキシを宣言しています。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> JQuery では、サーバークラスとそのメンバーへの参照は camel 形式です。 このコードサンプルではC# 、jQuery の**ChatHub**クラスを**ChatHub**として参照しています。

次のコードは、スクリプトでコールバック関数を作成する方法を示しています。 サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。 HTML でコンテンツを表示する前にエンコードする2行は省略可能であり、スクリプトインジェクションを防ぐ簡単な方法を示しています。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

次のコードは、ハブとの接続を開く方法を示しています。 このコードは接続を開始し、HTML ページの **[送信]** ボタンでクリックイベントを処理する関数に渡します。

> [!NOTE]
> この方法では、イベントハンドラーが実行される前に接続が確立されることを保証します。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>次の手順

SignalR は、リアルタイム web アプリケーションを構築するためのフレームワークであることを学習しました。 また、いくつかの SignalR 開発タスク (SignalR を ASP.NET アプリケーションに追加する方法、ハブクラスを作成する方法、ハブからメッセージを送受信する方法) についても学習しました。

このチュートリアルまたは他の SignalR アプリケーションのサンプルアプリケーションは、ホストプロバイダーに展開することで、インターネット経由で利用できます。 Microsoft では、無料の[Windows Azure 試用版アカウント](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)で最大10個の web サイトを無料で提供しています。 サンプル SignalR アプリケーションをデプロイする方法のチュートリアルについては、「 [Windows Azure Web サイトとしての SignalR はじめにサンプルの発行](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)」を参照してください。 Visual Studio web プロジェクトを Windows Azure の Web サイトに配置する方法の詳細については、「 [Windows azure Web サイトへの ASP.NET アプリケーションの配置](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」を参照してください。 (注: WebSocket トランスポートは、現在、Windows Azure Websites ではサポートされていません。 WebSocket トランスポートが使用できない場合、SignalR は、 [SignalR の概要](index.md)に関するトピックの「トランスポート」セクションで説明されている他の利用可能なトランスポートを使用します。)

より高度な SignalR 開発の概念を学習するには、次のサイトで SignalR ソースコードとリソースを参照してください。

- [SignalR プロジェクト](http://signalr.net)
- [SignalR Github とサンプル](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
