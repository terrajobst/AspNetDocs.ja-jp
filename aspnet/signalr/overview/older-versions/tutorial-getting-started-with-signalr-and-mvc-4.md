---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 'チュートリアル: SignalR 1.x および MVC 4 でのはじめに |Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR と ASP.NET MVC 4 を使用して、リアルタイムチャットアプリケーションを作成します。
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468070"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>チュートリアル: SignalR 1.x および MVC 4 でのはじめに

([パトリック Fletcher](https://github.com/pfletcher)、 [Tim teebken](https://github.com/timlt) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このチュートリアルでは、ASP.NET SignalR を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。 SignalR を MVC 4 アプリケーションに追加し、メッセージを送信して表示するためのチャットビューを作成します。

## <a name="overview"></a>概要

このチュートリアルでは、ASP.NET SignalR と ASP.NET MVC 4 を使用したリアルタイムの web アプリケーション開発について説明します。 このチュートリアルでは、 [SignalR はじめにチュートリアル](tutorial-getting-started-with-signalr.md)と同じチャットアプリケーションコードを使用しますが、インターネットテンプレートに基づいて MVC 4 アプリケーションに追加する方法についても説明します。

このトピックでは、次の SignalR 開発タスクについて説明します。

- MVC 4 アプリケーションへの SignalR ライブラリの追加。
- クライアントにコンテンツをプッシュするハブクラスを作成する。
- Web ページで SignalR jQuery ライブラリを使用して、メッセージを送信し、ハブから更新を表示します。

次のスクリーンショットは、ブラウザーで実行されている、完了したチャットアプリケーションを示しています。

![チャットインスタンス](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

各項

- [プロジェクトを設定する](#setup)
- [サンプルを実行する](#run)
- [コードを確認する](#code)
- [次の手順](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>プロジェクトを設定する

前提条件:

- Visual Studio 2010 SP1、Visual Studio 2012、または Visual Studio 2012 Express。 Visual Studio がインストールされていない場合は、無料の Visual Studio 2012 Express 開発ツールを入手するには、「 [ASP.NET のダウンロード](https://www.asp.net/downloads)」を参照してください。
- Visual Studio 2010 の場合は、 [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)をインストールします。

このセクションでは、ASP.NET MVC 4 アプリケーションを作成し、SignalR ライブラリを追加して、チャットアプリケーションを作成する方法について説明します。

1. 1. Visual Studio で、ASP.NET MVC 4 アプリケーションを作成し、SignalRChat という名前を指定して、[OK] をクリックします。

        > [!NOTE]
        > VS 2010 では、Framework バージョン ドロップダウンコントロールで  **.NET Framework 4** を選択します。 SignalR コードは .NET Framework バージョン4および4.5 で実行されます。

        ![Mvc web の作成](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. [インターネットアプリケーション] テンプレートを選択し、[**単体テストプロジェクトを作成**する] オプションをオフにして、[OK] をクリックします。

         ![Mvc インターネットサイトの作成](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. **[ツール > NuGet パッケージマネージャー > パッケージマネージャーコンソール]** を開き、次のコマンドを実行します。 この手順では、SignalR 機能を有効にするスクリプトファイルとアセンブリ参照のセットをプロジェクトに追加します。

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. **ソリューションエクスプローラー** Scripts フォルダーを展開します。 SignalR のスクリプトライブラリがプロジェクトに追加されていることに注意してください。

         ![ライブラリ参照](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] を選択します。 **新しいフォルダーを作成**し、**ハブ**という名前の新しいフォルダーを追加します。
      6. **ハブ** フォルダーを右クリックし、追加 をクリックします。 **クラス**を作成し、 C# **ChatHub.cs**という名前の新しいクラスを作成します。 このクラスは、すべてのクライアントにメッセージを送信する SignalR サーバーハブとして使用します。

> [!NOTE]
> Visual Studio 2012 を使用していて[ASP.NET and Web Tools 2012.2 更新プログラム](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)がインストールされている場合は、new SignalR item テンプレートを使用してハブクラスを作成できます。 これを行うには、**ハブ** フォルダーを右クリックし、追加 をクリックします。 **新しい項目** を選択し、**SignalR Hub クラス (v1)** を選択して、クラスに**ChatHub.cs**という名前を指定します。

1. **ChatHub**クラスのコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. プロジェクトの**global.asax**ファイルを開き、`Application_Start` メソッドのコードの最初の行として `RouteTable.Routes.MapHubs();` メソッドの呼び出しを追加します。 このコードは、SignalR ハブの既定のルートを登録し、他のルートを登録する前に呼び出す必要があります。 完成した `Application_Start` メソッドは、次の例のようになります。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. **Controllers/HomeController**で見つかった `HomeController` クラスを編集し、次のメソッドをクラスに追加します。 このメソッドは、後の手順で作成する**チャット**ビューを返します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. 先ほど作成した `Chat` メソッド内を右クリックし、 **[ビューの追加]** をクリックして新しいビューファイルを作成します。
5. **[ビューの追加]** ダイアログボックスで、**レイアウトまたはマスターページを使用**するためのチェックボックスがオンになっていることを確認し (他のチェックボックスをオフにします)、 **[追加]** をクリックします。

    ![ビューを追加する](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. 「 **Chat. cshtml**」という名前の新しいビューファイルを編集します。 &lt;h2&gt; タグの後に、次の &lt;div&gt; セクションと `@section scripts` コードブロックをページに貼り付けます。 このスクリプトは、ページがチャットメッセージを送信し、サーバーからメッセージを表示できるようにします。 チャットビューの完全なコードは、次のコードブロックに表示されます。

    > [!IMPORTANT]
    > SignalR およびその他のスクリプトライブラリを Visual Studio プロジェクトに追加すると、パッケージマネージャーによって、このトピックに示されているバージョンよりも新しいバージョンのスクリプトがインストールされる場合があります。 コード内のスクリプト参照が、プロジェクトにインストールされているスクリプトライブラリのバージョンと一致していることを確認します。

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. プロジェクトの**すべてを保存**します。

<a id="run"></a>

## <a name="run-the-sample"></a>サンプルを実行する

1. F5 キーを押して、プロジェクトをデバッグモードで実行します。
2. ブラウザーのアドレスラインで、プロジェクトの既定のページの URL に **/home/chat**を追加します。 チャットページがブラウザーインスタンスに読み込まれ、ユーザー名の入力が求められます。

    ![ユーザー名の入力](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. ユーザー名を入力します。
4. ブラウザーのアドレス行から URL をコピーし、それを使用して2つ以上のブラウザーインスタンスを開きます。 各ブラウザーインスタンスで、一意のユーザー名を入力します。
5. 各ブラウザーインスタンスで、コメントを追加し、 **[送信]** をクリックします。 コメントは、すべてのブラウザーインスタンスに表示されます。

    > [!NOTE]
    > この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。 ハブは、現在のすべてのユーザーにコメントをブロードキャストします。 後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。
6. 次のスクリーンショットは、ブラウザーで実行されているチャットアプリケーションを示しています。

    ![チャットブラウザー](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. **ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。 ブラウザーとして Internet Explorer を使用している場合、このノードはデバッグモードで表示されます。 SignalR ライブラリによって実行時に動的に生成される**ハブ**という名前のスクリプトファイルがあります。 このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。 Internet Explorer 以外のブラウザーを使用する場合は、動的**ハブ**ファイルを直接参照してアクセスすることもできます (http://mywebsite/signalr/hubsなど)。

    ![生成されたハブスクリプト](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>コードを確認する

SignalR chat アプリケーションでは、2つの基本的な SignalR 開発タスクを示しています。サーバー上の主要な調整オブジェクトとしてハブを作成し、SignalR jQuery ライブラリを使用してメッセージを送受信します。

### <a name="signalr-hubs"></a>SignalR Hubs

コードサンプルでは、 **ChatHub**クラスは**SignalR**クラスから派生しています。 **ハブ**クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。 ハブクラスにパブリックメソッドを作成し、web ページの jQuery スクリプトからメソッドを呼び出すことによって、これらのメソッドにアクセスできます。

チャットコードでは、クライアントは**ChatHub**メソッドを呼び出して、新しいメッセージを送信します。 その後、ハブはすべてのクライアントにメッセージを送信します。これには、**すべての addNewMessageToPage**を呼び出します。

**Send**メソッドは、いくつかのハブの概念を示しています。

- クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。
- このハブに接続されているすべてのクライアントにアクセスするには、 **SignalR**プロパティを使用します。
- クライアントの jQuery 関数 (`addNewMessageToPage` 関数など) を呼び出して、クライアントを更新します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR と jQuery

コードサンプルの**Chat. cshtml**ビューファイルは、SignalR jQuery ライブラリを使用して SignalR hub と通信する方法を示しています。 コードの重要なタスクは、ハブに対して自動生成されたプロキシへの参照を作成し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言し、メッセージをハブに送信するための接続を開始することです。

次のコードでは、ハブのプロキシを宣言しています。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> JQuery では、サーバークラスとそのメンバーへの参照は camel 形式です。 このコードサンプルではC# 、jQuery の**ChatHub**クラスを**ChatHub**として参照しています。 でのC#ように、jQuery の `ChatHub` クラスを通常の Pascal 形式で参照する場合は、ChatHub.cs クラスファイルを編集します。 `Microsoft.AspNet.SignalR.Hubs` 名前空間を参照する `using` ステートメントを追加します。 次に、`HubName` 属性を `ChatHub` クラス (`[HubName("ChatHub")]`など) に追加します。 最後に、jQuery 参照を `ChatHub` クラスに更新します。

次のコードは、スクリプトでコールバック関数を作成する方法を示しています。 サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。 `htmlEncode` 関数の呼び出しは、スクリプトの挿入を防ぐ方法として、メッセージの内容をページに表示する前に HTML エンコードする方法を示しています。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

次のコードは、ハブとの接続を開く方法を示しています。 このコードは接続を開始し、チャットページの **[送信]** ボタンでクリックイベントを処理する関数を渡します。

> [!NOTE]
> この方法により、イベントハンドラーが実行される前に接続が確立されます。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>次の手順

SignalR は、リアルタイム web アプリケーションを構築するためのフレームワークであることを学習しました。 また、いくつかの SignalR 開発タスク (SignalR を ASP.NET アプリケーションに追加する方法、ハブクラスを作成する方法、ハブからメッセージを送受信する方法) についても学習しました。

より高度な SignalR 開発の概念を学習するには、次のサイトで SignalR ソースコードとリソースを参照してください。

- [SignalR プロジェクト](http://signalr.net)
- [SignalR Github とサンプル](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
