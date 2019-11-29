---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 'チュートリアル: SignalR 2 | を使用した高頻度のリアルタイムアプリの作成Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600454"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>チュートリアル: SignalR 2 を使用した高頻度のリアルタイムアプリの作成

このチュートリアルでは、ASP.NET SignalR 2 を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。 この場合、"高頻度のメッセージング" とは、サーバーが更新を一定の速度で送信することを意味します。 1秒あたり最大10個のメッセージを送信します。

作成したアプリケーションには、ユーザーがドラッグできる図形が表示されます。 サーバーは、接続されているすべてのブラウザー内の図形の位置を更新し、時間指定の更新を使用して、ドラッグした図形の位置と一致します。

このチュートリアルで導入された概念には、リアルタイムゲームやその他のシミュレーションアプリケーションのアプリケーションがあります。

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * プロジェクトを設定する
> * 基本アプリケーションを作成する
> * アプリの起動時にハブにマップする
> * クライアントを追加する
> * アプリを実行する
> * クライアントループを追加する
> * サーバーループの追加
> * スムーズなアニメーションの追加

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>必要条件

* **ASP.NET と web 開発**ワークロードを含む[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 。

## <a name="set-up-the-project"></a>プロジェクトを設定する

このセクションでは、Visual Studio 2017 でプロジェクトを作成します。

このセクションでは、Visual Studio 2017 を使用して空の ASP.NET Web アプリケーションを作成し、SignalR と jQuery のライブラリを追加する方法について説明します。

1. Visual Studio で、ASP.NET Web アプリケーションを作成します。

    ![Web の作成](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. **[New ASP.NET Web Application-MoveShapeDemo]** ウィンドウで、 **[Empty]** を選択したままにして、[ **OK]** を選択します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-MoveShapeDemo]** で、[**インストールされている** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。

1. クラスに*MoveShapeHub*という名前を指定し、プロジェクトに追加します。

    この手順では、 *MoveShapeHub.cs*クラスファイルを作成します。 同時に、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。

1. [**ツール** > **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] を選択します。

1. **パッケージマネージャーコンソール**で、次のコマンドを実行します。

    ```console
    Install-Package jQuery.UI.Combined
    ```

    コマンドを実行すると、jQuery UI ライブラリがインストールされます。 図形をアニメーション化するために使用します。

1. **ソリューションエクスプローラー**で、[スクリプト] ノードを展開します。

    ![スクリプトライブラリの参照](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    JQuery、jQueryUI、SignalR のスクリプトライブラリは、プロジェクトに表示されます。

## <a name="create-the-base-application"></a>基本アプリケーションを作成する

このセクションでは、ブラウザーアプリケーションを作成します。 アプリは、各マウス移動イベントの発生時に、図形の場所をサーバーに送信します。 サーバーは、この情報を、接続されている他のすべてのクライアントにリアルタイムでブロードキャストします。 このアプリケーションの詳細については、後のセクションで説明します。

1. *MoveShapeHub.cs*ファイルを開きます。

1. *MoveShapeHub.cs*ファイル内のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. ファイルを保存します。

`MoveShapeHub` クラスは、SignalR hub の実装です。 [SignalR でのはじめに](tutorial-getting-started-with-signalr.md)チュートリアルと同様、ハブにはクライアントが直接呼び出すメソッドがあります。 この場合、クライアントは図形の新しい X 座標と Y 座標を使用してオブジェクトをサーバーに送信します。 これらの座標は、接続されている他のすべてのクライアントにブロードキャストされます。 SignalR は、このオブジェクトを JSON を使用して自動的にシリアル化します。

アプリは `ShapeModel` オブジェクトをクライアントに送信します。 図形の位置を格納するメンバーがあります。 サーバー上のオブジェクトのバージョンには、どのクライアントのデータが格納されているかを追跡するメンバーもあります。 このオブジェクトは、サーバーがクライアントのデータをそれ自体に送信しないようにします。 このメンバーは、`JsonIgnore` 属性を使用して、アプリケーションがデータをシリアル化してクライアントに送り返すことを防止します。

## <a name="map-to-the-hub-when-app-starts"></a>アプリの起動時にハブにマップする

次に、アプリケーションの起動時に、ハブへのマッピングを設定します。 SignalR 2 では、OWIN startup クラスを追加するとマッピングが作成されます。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-MoveShapeDemo]** で、[**インストールされている** > **Visual C#**  > **Web** ] を選択し、 **[OWIN Startup Class]** を選択します。

1. クラスに「 *Startup* 」という名前を指定し、[ **OK]** を選択します。

1. *Startup.cs*ファイルの既定のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

OWIN startup クラスは、アプリが `Configuration` メソッドを実行するときに `MapSignalR` を呼び出します。 このアプリは、`OwinStartup` assembly 属性を使用して OWIN のスタートアッププロセスにクラスを追加します。

## <a name="add-the-client"></a>クライアントを追加する

クライアントの HTML ページを追加します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **HTML ページ**の**追加**] を選択します。

1. ページの**既定**の名前を指定し、[ **OK]** を選択します。

1. **ソリューションエクスプローラー**で、[ *Default .html* ] を右クリックし、 **[スタートページとして設定]** を選択します。

1. *既定の .html*ファイルの既定のコードを次のコードに置き換えます。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. **ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。

    JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。

    > [!IMPORTANT]
    > パッケージマネージャーでは、SignalR スクリプトの新しいバージョンがインストールされます。

1. コードブロック内のスクリプト参照を、プロジェクト内のスクリプトファイルのバージョンに対応するように更新します。

この HTML および JavaScript コードでは、`shape`と呼ばれる赤色の `div` が作成されます。 JQuery ライブラリを使用して図形のドラッグ動作を有効にし、`drag` イベントを使用して、図形の位置をサーバーに送信します。

## <a name="run-the-app"></a>アプリを実行する

アプリを実行して、作業することができます。 図形をブラウザーウィンドウの周りにドラッグすると、他のブラウザーでも図形は移動します。

1. ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、アプリケーションをデバッグモードで実行します。

    ![デバッグモードをオンにして [再生] を選択したユーザーのスクリーンショット。](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    ブラウザーウィンドウが開き、右上隅に赤色の図形が表示されます。

1. ページの URL をコピーします。

1. 別のブラウザーを開き、アドレスバーに URL を貼り付けます。

1. いずれかのブラウザーウィンドウで図形をドラッグします。 他のブラウザーウィンドウの図形は次のようになります。

アプリケーションはこのメソッドを使用して機能しますが、推奨されるプログラミングモデルではありません。 送信されるメッセージの数に上限はありません。 その結果、クライアントとサーバーはメッセージを処理できないため、パフォーマンスが低下します。 また、アプリによって、クライアントに不整合なアニメーションが表示されます。 この不自然なアニメーションは、図形が各メソッドによって瞬時に移動するために発生します。 図形を新しい場所に滑らかに移動させる方が適切です。 次に、これらの問題を解決する方法を学習します。

## <a name="add-the-client-loop"></a>クライアントループを追加する

マウスの移動イベントごとに図形の場所を送信すると、不必要な量のネットワークトラフィックが発生します。 アプリでは、クライアントからのメッセージを調整する必要があります。

Javascript `setInterval` 関数を使用して、固定レートでサーバーに新しい位置情報を送信するループを設定します。 このループは、"ゲームループ" の基本的な表現です。 これは、ゲームのすべての機能を駆動する、繰り返し呼び出される関数です。

1. *既定の .html*ファイルのクライアントコードを次のコードに置き換えます。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > スクリプト参照を再置換する必要があります。 プロジェクト内のスクリプトのバージョンと一致している必要があります。

    この新しいコードでは、`updateServerModel` 関数を追加します。 固定頻度で呼び出されます。 関数は、`moved` フラグによって、送信する新しい位置データがあることが示されたときに、その位置データをサーバーに送信します。

1. [再生] ボタンを選択してアプリケーションを起動します

1. ページの URL をコピーします。

1. 別のブラウザーを開き、アドレスバーに URL を貼り付けます。

1. いずれかのブラウザーウィンドウで図形をドラッグします。 他のブラウザーウィンドウの図形は次のようになります。

アプリはサーバーに送信されるメッセージの数を調整するため、アニメーションは最初に smooth did として表示されません。

## <a name="add-the-server-loop"></a>サーバーループの追加

現在のアプリケーションでは、サーバーからクライアントに送信されたメッセージは、受信した頻度で送信されます。 クライアントに表示されるように、このネットワークトラフィックにも同様の問題があります。

アプリは、必要以上に頻繁にメッセージを送信できます。 その結果、接続があふれてしまう可能性があります。 このセクションでは、送信メッセージの速度を調整するタイマーを追加するようにサーバーを更新する方法について説明します。

1. `MoveShapeHub.cs` の内容を次のコードに置き換えます。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. [Play] \ (再生 \) ボタンを選択して、アプリケーションを開始します。

1. ページの URL をコピーします。

1. 別のブラウザーを開き、アドレスバーに URL を貼り付けます。

1. いずれかのブラウザーウィンドウで図形をドラッグします。

このコードは、クライアントを拡張して `Broadcaster` クラスを追加します。 新しいクラスは、.NET framework の `Timer` クラスを使用して、送信メッセージを調整します。

ハブ自体が一時的なものであることを理解することをお勧めします。 これは、必要になるたびに作成されます。 そのため、アプリはシングルトンとして `Broadcaster` を作成します。 遅延初期化を使用して、必要になるまで `Broadcaster`の作成を延期します。 これにより、タイマーを開始する前に、アプリが最初のハブインスタンスを完全に作成することが保証されます。

次に、クライアントの `UpdateShape` 関数の呼び出しが、ハブの `UpdateModel` メソッドから移動されます。 アプリが受信メッセージを受信するたびに、すぐには呼び出されなくなりました。 代わりに、アプリは1秒あたり25回の呼び出しでクライアントにメッセージを送信します。 プロセスは、`Broadcaster` クラス内の `_broadcastLoop` タイマーによって管理されます。

最後に、ハブからクライアントメソッドを直接呼び出すのではなく、`Broadcaster` クラスが現在のオペレーティング `_hubContext` ハブへの参照を取得する必要があります。 `GlobalHost`で参照を取得します。

## <a name="add-smooth-animation"></a>スムーズなアニメーションの追加

アプリケーションはほぼ完成していますが、さらに改善することもできます。 アプリは、サーバーメッセージに応答してクライアント上の図形を移動します。 図形の位置をサーバーによって指定された新しい場所に設定するのではなく、JQuery UI ライブラリの `animate` 関数を使用します。 現在と新しい位置の間で図形を滑らかに移動できます。

1. *既定の .html*ファイルのクライアントの `updateShape` メソッドを、強調表示されているコードのように更新します。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. [Play] \ (再生 \) ボタンを選択して、アプリケーションを開始します。

1. ページの URL をコピーします。

1. 別のブラウザーを開き、アドレスバーに URL を貼り付けます。

1. いずれかのブラウザーウィンドウで図形をドラッグします。

他のウィンドウでの図形の動きは、不自然に見えます。 アプリは、着信メッセージごとに1回設定するのではなく、時間の経過と共にその動きを補間します。

このコードは、図形を古い位置から新しい位置に移動します。 サーバーは、アニメーションの間隔の間に図形の位置を示します。 この場合、これは100ミリ秒です。 新しいアニメーションが開始される前に、その図形で実行されていた前のアニメーションがアプリによってクリアされます。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>その他の技術情報

ここで学習した通信パラダイムは、 [SignalR で作成された ShootR ゲーム](https://shootr.azurewebsites.net/)と同様に、オンラインゲームやその他のシミュレーションの開発に役立ちます。

SignalR の詳細については、次のリソースを参照してください。

* [SignalR プロジェクト](http://signalr.net)

* [SignalR GitHub とサンプル](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>次のステップ:

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * プロジェクトを設定する
> * 基本アプリケーションを作成しました
> * アプリの起動時にハブにマップされます
> * クライアントを追加しました
> * アプリを実行しました
> * クライアントループを追加しました
> * サーバーループを追加しました
> * スムーズなアニメーションの追加

次の記事に進み、ASP.NET SignalR 2 を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。
> [!div class="nextstepaction"]
> [SignalR 2 とサーバーブロードキャスト](tutorial-server-broadcast-with-signalr.md)