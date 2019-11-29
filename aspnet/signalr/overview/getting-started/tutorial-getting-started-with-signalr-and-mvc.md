---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 'チュートリアル: SignalR 2 と MVC 5 を使用したリアルタイムチャット |Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR 2 を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。 MVC 5 アプリケーションに SignalR を追加します。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600486"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a>チュートリアル: SignalR 2 と MVC 5 を使用したリアルタイムチャット

このチュートリアルでは、ASP.NET SignalR 2 を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。 SignalR を MVC 5 アプリケーションに追加し、メッセージを送信して表示するためのチャットビューを作成します。

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * プロジェクトを設定する
> * サンプルの実行
> * コードを確認する

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>必要条件

* **ASP.NET と web 開発**ワークロードを含む[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 。

## <a name="set-up-the-project"></a>プロジェクトを設定する

このセクションでは、Visual Studio 2017 と SignalR 2 を使用して、空の ASP.NET MVC 5 アプリケーションを作成する方法、SignalR ライブラリを追加する方法、チャットアプリケーションを作成する方法について説明します。

1. Visual Studio で、.NET Framework 4.5 C#を対象とする ASP.NET アプリケーションを作成し、SignalRChat という名前を指定して、[OK] をクリックします。

    ![Web の作成](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. **New ASP.NET Web アプリケーション-SignalRMvcChat**で、 **[MVC]** を選択し、 **[認証の変更]** を選択します。

1. **[認証の変更]** で、 **[認証なし]** を選択し、 **[OK]** をクリックします。

    ![[認証なし] を選択する](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. **New ASP.NET Web アプリケーション-SignalRMvcChat**で、[ **OK]** を選択します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-signalrchat]** で、[**インストール済み** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。

1. クラスに*ChatHub*という名前を指定し、プロジェクトに追加します。

    この手順では、 *ChatHub.cs*クラスファイルを作成し、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。

1. 新しい*ChatHub.cs*クラスファイルのコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **クラス**の**追加**] を選択します。

1. 新しいクラスに「 *Startup* 」という名前を指定し、プロジェクトに追加します。

1. *Startup.cs*クラスファイル内のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. **ソリューションエクスプローラー**で、[**コントローラー** > **HomeController.cs**] を選択します。

1. このメソッドを*HomeController.cs*に追加します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    このメソッドは、後の手順で作成した**チャット**ビューを返します。

1. **ソリューションエクスプローラー**で、[**ビュー** > **ホーム**] を右クリックし、[ >  **ビュー**の**追加**] を選択します。

1. **[ビューの追加]** で、新しいビューに「**チャット**」という名前を指定し、 **[追加]** を選択します。

1. **Chat**の内容を次のコードに置き換えます。

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. **ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。

    JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。

    > [!IMPORTANT]
    > パッケージマネージャーで、SignalR スクリプトの新しいバージョンがインストールされている可能性があります。

1. コードブロック内のスクリプト参照が、プロジェクト内のスクリプトファイルのバージョンに対応していることを確認します。

    元のコードブロックからのスクリプト参照:

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. 一致しない場合は、 *cshtml*ファイルを更新します。

1. メニューバーで **[ファイル]** 、 **[すべて保存]** の > を選択します。

## <a name="run-the-sample"></a>サンプルを実行する

1. ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、サンプルをデバッグモードで実行します。

    ![ユーザー名の入力](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. ブラウザーが開いたら、チャット id の名前を入力します。

1. ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。

1. 各ブラウザーで、一意の名前を入力します。

1. ここで、コメントを追加し、 **[送信]** を選択します。 他のブラウザーでも同じ手順を繰り返します。 コメントはリアルタイムで表示されます。

    > [!NOTE]
    > この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。 ハブは、現在のすべてのユーザーにコメントをブロードキャストします。 後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。

    チャットアプリケーションを3つの異なるブラウザーで実行する方法について説明します。 Tom、Anand、およびスーザンがメッセージを送信すると、すべてのブラウザーがリアルタイムで更新されます。

    ![3つのブラウザーすべてに同じチャット履歴が表示されます](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. **ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。 SignalR ライブラリによって実行時に生成される*ハブ*という名前のスクリプトファイルがあります。 このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。

    ![スクリプトドキュメントノードで自動生成されたハブスクリプト](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a>コードを確認する

SignalR chat アプリケーションは、2つの基本的な SignalR 開発タスクを示しています。 ハブを作成する方法についても説明します。 サーバーは、そのハブをメイン調整オブジェクトとして使用します。 ハブは、SignalR jQuery ライブラリを使用してメッセージを送受信します。

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs の SignalR Hub

コードサンプルでは、`ChatHub` クラスは `Microsoft.AspNet.SignalR.Hub` クラスから派生します。 `Hub` クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。 ハブクラスにパブリックメソッドを作成し、web ページのスクリプトからそれらのメソッドにアクセスすることによって、これらのメソッドにアクセスできます。

チャットコードでは、クライアントは `ChatHub.Send` メソッドを呼び出して、新しいメッセージを送信します。 その後、ハブは `Clients.All.addNewMessageToPage`を呼び出すことによって、すべてのクライアントにメッセージを送信します。

`Send` メソッドは、いくつかのハブの概念を示しています。

* クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。

* このハブに接続されているすべてのクライアントと通信するには、`Microsoft.AspNet.SignalR.Hub.Clients` 動的プロパティを使用します。

* クライアントの関数 (`addNewMessageToPage` 関数など) を呼び出して、クライアントを更新します。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a>SignalR と jQuery Chat. cshtml

コードサンプルの*Chat. cshtml*ビューファイルは、SignalR jQuery ライブラリを使用して SignalR hub と通信する方法を示しています。  このコードでは、多くの重要なタスクが実行されています。 ハブ用に自動生成されたプロキシへの参照を作成し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言して、ハブにメッセージを送信するための接続を開始します。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> JavaScript では、サーバークラスとそのメンバーへの参照はキャメルケースにあります。 このコードサンプルではC# 、`chatHub`として JavaScript の `ChatHub` クラスを参照しています。

このコードブロックでは、スクリプトでコールバック関数を作成します。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。 `htmlEncode` 関数の省略可能な呼び出しは、メッセージをページに表示する前に HTML エンコードする方法を示しています。 スクリプトインジェクションを防ぐ方法です。

このコードは、ハブとの接続を開きます。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> この方法により、イベントハンドラーが実行される前に接続が確立されます。

このコードは接続を開始し、チャットページの **[送信]** ボタンでクリックイベントを処理する関数を渡します。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a>その他の技術情報

SignalR の詳細については、次のリソースを参照してください。

* [SignalR プロジェクト](http://signalr.net)

* [SignalR GitHub とサンプル](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>次のステップ:

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * プロジェクトを設定する
> * サンプルを実行しました
> * コードを調べる

次の記事に進み、ASP.NET SignalR 2 を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法を学習してください。
> [!div class="nextstepaction"]
> [高頻度のメッセージングを使用した Web アプリ](tutorial-high-frequency-realtime-with-signalr.md)