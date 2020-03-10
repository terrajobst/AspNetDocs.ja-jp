---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: SignalR 1.x を使用した高頻度のリアルタイム |Microsoft Docs
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。 高頻度のメッセージング...
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505714"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a>SignalR 1.x による高頻度リアルタイム

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このチュートリアルでは、ASP.NET SignalR を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。 この場合、高頻度のメッセージングでは、一定のレートで送信された更新を意味します。このアプリケーションの場合、1秒あたり最大10個のメッセージが送信されます。
> 
> このチュートリアルで作成するアプリケーションは、ユーザーがドラッグできる図形を表示します。 その他のすべての接続されたブラウザーでの図形の位置は、時間指定の更新を使用して、ドラッグした図形の位置と一致するように更新されます。
> 
> このチュートリアルで導入された概念には、リアルタイムゲームやその他のシミュレーションアプリケーションのアプリケーションがあります。
> 
> このチュートリアルのコメントは歓迎しています。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com)に投稿できます。

## <a name="overview"></a>概要

このチュートリアルでは、リアルタイムで他のブラウザーとオブジェクトの状態を共有するアプリケーションを作成する方法について説明します。 作成するアプリケーションは MoveShape と呼ばれます。 MoveShape ページには、ユーザーがドラッグできる HTML Div 要素が表示されます。ユーザーが Div をドラッグすると、その新しい位置がサーバーに送信されます。その後、接続されている他のすべてのクライアントに対して、一致するように図形の位置を更新するように指示します。

![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

このチュートリアルで作成するアプリケーションは、Damian Edwards のデモに基づいています。 このデモを含むビデオについては、[こちら](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)をご覧ください。

このチュートリアルでは、最初に、図形のドラッグ時に発生する各イベントから SignalR メッセージを送信する方法を示します。 接続された各クライアントは、メッセージを受信するたびに、図形のローカルバージョンの位置を更新します。

アプリケーションはこの方法を使用して機能しますが、送信されるメッセージの数に上限がないため、クライアントとサーバーがメッセージを大量に使用し、パフォーマンスが低下する可能性があるため、これは推奨されるプログラミングモデルではありません. また、クライアントで表示されるアニメーションも不整合になります。これは、各メソッドによって図形が瞬時に移動されるのではなく、新しい場所に滑らかに移動するためです。 このチュートリアルの後のセクションでは、クライアントまたはサーバーによってメッセージが送信される最大速度を制限するタイマー関数を作成する方法と、図形を位置をスムーズに移動する方法について説明します。 このチュートリアルで作成したアプリケーションの最終バージョンは、[コードギャラリー](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)からダウンロードできます。

このチュートリアルは、次のセクションで構成されています。

- [前提条件](#prerequisites)
- [プロジェクトを作成する](#createtheproject)
- [ASP.NET SignalR と JQuery. UI NuGet パッケージを追加する](#nugetpackages)
- [基本アプリケーションを作成する](#baseapp)
- [クライアントループを追加する](#clientloop)
- [サーバーループの追加](#serverloop)
- [クライアントに smooth animation を追加する](#animation)
- [その他の手順](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>前提条件

このチュートリアルには、Visual Studio 2012 または Visual Studio 2010 が必要です。 Visual Studio 2010 が使用されている場合、プロジェクトは .NET Framework 4.5 ではなく .NET Framework 4 を使用します。

Visual Studio 2012 を使用している場合は、 [ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)をインストールすることをお勧めします。 この更新プログラムには、公開、新機能、新しいテンプレートなどの新機能が追加されています。

Visual Studio 2010 を使用している場合は、 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)がインストールされていることを確認します。

<a id="createtheproject"></a>

## <a name="create-the-project"></a>プロジェクトを作成する

このセクションでは、Visual Studio でプロジェクトを作成します。

1. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。
2. **[新しいプロジェクト]** ダイアログボックスの [ **C#** **テンプレート**] で展開し、 **[Web]** を選択します。
3. **[ASP.NET 空の Web アプリケーション]** テンプレートを選択し、プロジェクトに*MoveShapeDemo*という名前を指定して、[ **OK]** をクリックします。

    ![新しいプロジェクトの作成](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a>SignalR および JQuery. UI NuGet パッケージを追加する

NuGet パッケージをインストールすることによって、SignalR 機能をプロジェクトに追加できます。 また、このチュートリアルでは、図形をドラッグアンドアニメーション化できるようにするために、JQuery. UI パッケージも使用します。

1. [ツール] をクリックします。 **NuGet パッケージマネージャー |パッケージマネージャーコンソール**。
2. パッケージマネージャーで、次のコマンドを入力します。

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    SignalR パッケージは、他のいくつかの NuGet パッケージを依存関係としてインストールします。 インストールが完了すると、ASP.NET アプリケーションで SignalR を使用するために必要なすべてのサーバーおよびクライアントコンポーネントが作成されます。
3. 次のコマンドをパッケージマネージャーコンソールに入力して、JQuery および JQuery. UI パッケージをインストールします。

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>基本アプリケーションを作成する

このセクションでは、各マウス移動イベント時に図形の場所をサーバーに送信するブラウザーアプリケーションを作成します。 その後、サーバーは、受信時に、他のすべての接続されたクライアントにこの情報をブロードキャストします。 このアプリケーションの拡張については、後のセクションで説明します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[クラス.]** . の順に選択します。クラスに**MoveShapeHub**という名前を指定し、 **[追加]** をクリックします。
2. 新しい**MoveShapeHub**クラスのコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    上の `MoveShapeHub` クラスは、SignalR hub の実装です。 [SignalR でのはじめに](index.md)チュートリアルと同様、ハブにはクライアントが直接呼び出すメソッドがあります。 この場合、クライアントは図形の新しい X 座標と Y 座標を含むオブジェクトをサーバーに送信し、その後、接続されている他のすべてのクライアントにブロードキャストされます。 SignalR は、このオブジェクトを JSON を使用して自動的にシリアル化します。

    クライアントに送信されるオブジェクト (`ShapeModel`) には、図形の位置を格納するためのメンバーが含まれています。 サーバー上のオブジェクトのバージョンには、特定のクライアントに独自のデータが送信されないように、格納されているクライアントのデータを追跡するためのメンバーも含まれています。 このメンバーは、`JsonIgnore` 属性を使用して、シリアル化とクライアントへの送信を維持します。
3. 次に、アプリケーションの起動時にハブを設定します。 **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **グローバルアプリケーションクラス**。 *グローバル*の既定の名前をそのまま使用し、[ **OK]** をクリックします。

    ![グローバルアプリケーションクラスの追加](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. Global.asax.cs クラスの**using**ステートメントの後に、次の `using` ステートメントを追加します。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. SignalR の既定のルートを登録するには、グローバルクラスの `Application_Start` メソッドに次のコード行を追加します。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    Global.asax ファイルは次のようになります。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. 次に、クライアントを追加します。 **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **新しい項目**。 **[新しい項目の追加]** ダイアログで、 **[Html ページ]** を選択します。 ページに適切な名前 (既定の **.html**など) を付け、 **[追加]** をクリックします。
7. **ソリューションエクスプローラー**で、作成したページを右クリックし、 **[スタートページとして設定]** をクリックします。
8. HTML ページの既定のコードを次のコードスニペットに置き換えます。

    > [!NOTE]
    > 以下のスクリプト参照が、Scripts フォルダー内のプロジェクトに追加されたパッケージと一致していることを確認します。 Visual Studio 2010 では、プロジェクトに追加された JQuery と SignalR のバージョンが以下のバージョン番号と一致しない可能性があります。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    上記の HTML および JavaScript コードでは、Shape という名前の赤い Div を作成し、jQuery ライブラリを使用して図形のドラッグ動作を有効にし、図形の `drag` イベントを使用して、図形の位置をサーバーに送信します。
9. F5 キーを押してアプリケーションを起動します。 ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。 ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>クライアントループを追加する

すべてのマウス移動イベントに対して図形の場所を送信すると、不要なネットワークトラフィックが発生するため、クライアントからのメッセージを調整する必要があります。 Javascript `setInterval` 関数を使用して、固定レートでサーバーに新しい位置情報を送信するループを設定します。 このループは、ゲームまたはその他のシミュレーションのすべての機能を駆動する "ゲームループ" の非常に基本的な表現です。

1. 次のコードスニペットと一致するように、HTML ページのクライアントコードを更新します。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    上記の更新では、固定頻度で呼び出される `updateServerModel` 関数が追加されます。 この関数は、`moved` フラグによって、送信する新しい位置データがあることが示されたときに、その位置データをサーバーに送信します。
2. F5 キーを押してアプリケーションを起動します。 ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。 ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。 サーバーに送信されるメッセージの数は制限されるため、アニメーションは前のセクションと同様に smooth として表示されません。

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>サーバーループの追加

現在のアプリケーションでは、サーバーからクライアントに送信されたメッセージは、受信された頻度で送信されます。 これは、クライアントで見られたのと同様の問題を示しています。メッセージは必要以上に頻繁に送信され、その結果、接続があふれてしまう可能性があります。 このセクションでは、送信メッセージの速度を調整するタイマーを実装するようにサーバーを更新する方法について説明します。

1. `MoveShapeHub.cs` の内容を次のコードスニペットに置き換えます。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    上記のコードでは、クライアントを拡張して `Broadcaster` クラスを追加しています。これにより、.NET framework の `Timer` クラスを使用して送信メッセージが調整されます。

    ハブ自体は一時的なものであるため (必要になるたびに作成されます)、`Broadcaster` がシングルトンとして作成されます。 遅延初期化 (.NET 4 で導入) は、必要になるまで作成を延期するために使用されます。これにより、タイマーが開始される前に最初のハブインスタンスが完全に作成されます。

    次に、クライアントの `UpdateShape` 関数の呼び出しはハブの `UpdateModel` メソッドから移動され、受信メッセージが受信されるとすぐには呼び出されなくなります。 代わりに、クライアントへのメッセージは、`Broadcaster` クラス内から `_broadcastLoop` タイマーによって管理される、1秒あたり25回の呼び出しで送信されます。

    最後に、ハブからクライアントメソッドを直接呼び出すのではなく、`Broadcaster` クラスは `GlobalHost`を使用して現在の操作ハブ (`_hubContext`) への参照を取得する必要があります。
2. F5 キーを押してアプリケーションを起動します。 ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。 ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。 前のセクションのブラウザーには表示される違いはありませんが、クライアントに送信されるメッセージの数は制限されます。

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>クライアントに smooth animation を追加する

アプリケーションはほぼ完成していますが、サーバーメッセージに応答してクライアントが移動されるときに、クライアント上の図形の動きにおいて、改良が加えられています。 図形の位置をサーバーによって指定された新しい場所に設定するのではなく、JQuery UI ライブラリの `animate` 関数を使用して、現在と新しい位置の間で図形を滑らかに移動します。

1. 次の強調表示されているコードのように、クライアントの `updateShape` メソッドを更新します。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    上のコードでは、アニメーションの間隔 (この場合は100ミリ秒) で、前の場所からサーバーによって指定された新しい位置に図形を移動します。 図形で実行されている前のアニメーションは、新しいアニメーションが開始される前にクリアされます。
2. F5 キーを押してアプリケーションを起動します。 ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。 ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。 他のウィンドウでの図形の移動は、受信メッセージごとに1回設定されるのではなく、時間の経過と共に補間されるため、不自然に見えないようになります。

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>その他の手順

このチュートリアルでは、クライアントとサーバー間で頻度の高いメッセージを送信する SignalR アプリケーションをプログラミングする方法を学習しました。 この通信パラダイムは、オンラインゲームや、 [SignalR で作成された ShootR ゲーム](http://shootr.signalr.net)などの他のシミュレーションを開発する場合に便利です。

このチュートリアルで作成した完全なアプリケーションは、[コードギャラリー](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)からダウンロードできます。

SignalR development の概念の詳細については、SignalR のソースコードとリソースに関する次のサイトを参照してください。

- [SignalR プロジェクト](http://signalr.net)
- [SignalR Github とサンプル](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
