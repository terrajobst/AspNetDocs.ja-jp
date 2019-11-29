---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'チュートリアル: SignalR 2 を使用したリアルタイムチャットMicrosoft Docs'
author: bradygaster
description: このチュートリアルでは、SignalR を使用してリアルタイムのチャット アプリケーションを作成する方法を示します。 空の ASP.NET web アプリケーションに SignalR を追加します。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600464"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>チュートリアル: SignalR 2 を使用したリアルタイムチャット

このチュートリアルでは、SignalR を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。 SignalR を空の ASP.NET web アプリケーションに追加し、メッセージを送信して表示する HTML ページを作成します。

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * プロジェクトを設定する
> * サンプルの実行
> * コードを確認する

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>必要条件

* **ASP.NET と web 開発**ワークロードを含む[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 。

## <a name="set-up-the-project"></a>プロジェクトを設定する

このセクションでは、Visual Studio 2017 と SignalR 2 を使用して空の ASP.NET web アプリケーションを作成し、SignalR を追加して、チャットアプリケーションを作成する方法について説明します。

1. Visual Studio で、ASP.NET Web アプリケーションを作成します。

    ![Web の作成](tutorial-getting-started-with-signalr/_static/image2.png)

1. **新しい ASP.NET プロジェクト-SignalRChat**ウィンドウで、**空**のままにして [ **OK]** を選択します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-signalrchat]** で、[**インストール済み** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。

1. クラスに*ChatHub*という名前を指定し、プロジェクトに追加します。

    この手順では、 *ChatHub.cs*クラスファイルを作成し、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。

1. 新しい*ChatHub.cs*クラスファイルのコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-signalrchat]** で、[**インストールされている** > **Visual C#**  > **Web** ] を選択し、 **[OWIN Startup Class]** を選択します。

1. クラスに*スタートアップ*の名前を指定し、プロジェクトに追加します。

1. *Startup*クラスの既定のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **HTML ページ**の**追加**] を選択します。

1. 新しいページの*インデックス*に名前を付け、[ **OK]** を選択します。

1. **ソリューションエクスプローラー**で、作成した HTML ページを右クリックし、 **[スタートページとして設定]** を選択します。

1. HTML ページの既定のコードを次のコードに置き換えます。

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. **ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。

    JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。

    > [!IMPORTANT]
    > パッケージマネージャーで、SignalR スクリプトの新しいバージョンがインストールされている可能性があります。

1. コードブロック内のスクリプト参照が、プロジェクト内のスクリプトファイルのバージョンに対応していることを確認します。

    元のコードブロックからのスクリプト参照:

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. 一致しない場合は、 *.html*ファイルを更新します。

1. メニューバーで **[ファイル]** 、 **[すべて保存]** の > を選択します。

## <a name="run-the-sample"></a>サンプルを実行する

1. ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、サンプルをデバッグモードで実行します。

    ![ユーザー名の入力](tutorial-getting-started-with-signalr/_static/image3.png)

1. ブラウザーが開いたら、チャット id の名前を入力します。

1. ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。

1. 各ブラウザーで、一意の名前を入力します。

1. ここで、コメントを追加し、 **[送信]** を選択します。 他のブラウザーでも同じ手順を繰り返します。 コメントはリアルタイムで表示されます。

    > [!NOTE]
    > この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。 ハブは、現在のすべてのユーザーにコメントをブロードキャストします。 後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。

    チャットアプリケーションを3つの異なるブラウザーで実行する方法について説明します。 Tom、Anand、およびスーザンがメッセージを送信すると、すべてのブラウザーがリアルタイムで更新されます。

    ![3つのブラウザーすべてに同じチャット履歴が表示されます](tutorial-getting-started-with-signalr/_static/image4.png)

1. **ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。 SignalR ライブラリによって実行時に生成される*ハブ*という名前のスクリプトファイルがあります。 このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。

    ![スクリプトドキュメントノードで自動生成されたハブスクリプト](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>コードを確認する

SignalRChat アプリケーションは、2つの基本的な SignalR 開発タスクを示しています。 ハブを作成する方法についても説明します。 サーバーは、そのハブをメイン調整オブジェクトとして使用します。 ハブは、SignalR jQuery ライブラリを使用してメッセージを送受信します。

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs の SignalR Hub

上記のコードサンプルでは、`ChatHub` クラスは `Microsoft.AspNet.SignalR.Hub` クラスから派生しています。 `Hub` クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。 ハブクラスにパブリックメソッドを作成し、web ページのスクリプトからそれらのメソッドを呼び出すことによって、これらのメソッドを使用できます。

チャットコードでは、クライアントは `ChatHub.Send` メソッドを呼び出して、新しいメッセージを送信します。 その後、ハブは `Clients.All.broadcastMessage`を呼び出すことによって、すべてのクライアントにメッセージを送信します。

`Send` メソッドは、いくつかのハブの概念を示しています。

* クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。

* このハブに接続されているすべてのクライアントと通信するには、`Microsoft.AspNet.SignalR.Hub.Clients` 動的プロパティを使用します。

* クライアントの関数 (`broadcastMessage` 関数など) を呼び出して、クライアントを更新します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>SignalR と jQuery の .html

コードサンプルの*SignalR ページは*、SignalR hub と通信するために、jQuery ライブラリを使用する方法を示しています。 このコードでは、多くの重要なタスクが実行されています。 このメソッドは、ハブを参照するプロキシを宣言し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言し、接続を開始してハブにメッセージを送信します。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> JavaScript では、サーバークラスとそのメンバーへの参照はキャメルケースである必要があります。 このコードサンプルではC# 、`chatHub`として JavaScript の*ChatHub*クラスを参照しています。

このコードブロックでは、スクリプトでコールバック関数を作成します。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。 コンテンツを表示する前に HTML エンコードする2行は省略可能であり、スクリプトインジェクションを防止するための適切な方法を示しています。

このコードは、ハブとの接続を開きます。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> この方法では、イベントハンドラーが実行される前に、コードによって接続が確立されます。

このコードは接続を開始し、HTML ページの **[送信]** ボタンでクリックイベントを処理する関数に渡します。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>その他の技術情報

SignalR の詳細については、次のリソースを参照してください。

* [SignalR プロジェクト](http://signalr.net)

* [SignalR Github とサンプル](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>次のステップ:

このチュートリアルでは、次のことを行います。

> [!div class="checklist"]
> * プロジェクトを設定する
> * サンプルを実行しました
> * コードを調べる

SignalR と MVC 5 の使用方法については、次の記事に進んでください。
> [!div class="nextstepaction"]
> [SignalR 2 と MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)