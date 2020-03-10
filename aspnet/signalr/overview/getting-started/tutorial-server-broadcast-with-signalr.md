---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'チュートリアル: SignalR 2 を使用したサーバーブロードキャスト |Microsoft Docs'
author: tdykstra
description: このチュートリアルでは、ASP.NET SignalR 2 を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431242"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>チュートリアル: SignalR 2 を使用したサーバーブロードキャスト

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

このチュートリアルでは、ASP.NET SignalR 2 を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。 サーバーブロードキャストとは、サーバーがクライアントに送信される通信を開始することを意味します。

このチュートリアルで作成するアプリケーションは、サーバーブロードキャスト機能の一般的なシナリオである株式ティッカーをシミュレートします。 サーバーは定期的に株価を更新し、接続されているすべてのクライアントに更新をブロードキャストします。 ブラウザーでは、サーバーからの通知に応じて、 **[変更]** 列と [ **%** ] 列の数値と記号が動的に変更されます。 同じ URL に対して追加のブラウザーを開くと、すべてのブラウザーで同じデータと同じデータの変更が同時に表示されます。

![Web の作成](tutorial-server-broadcast-with-signalr/_static/image1.png)

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * プロジェクトを作成する
> * サーバー コードを設定する
> * サーバーコードを確認する
> * クライアントコードの設定
> * クライアントコードを確認する
> * アプリケーションをテストする
> * ログの有効化

> [!IMPORTANT]
> アプリケーションをビルドする手順を実行しない場合は、新しい空の ASP.NET Web アプリケーションプロジェクトに SignalR パッケージをインストールできます。 このチュートリアルの手順を実行せずに NuGet パッケージをインストールする場合は、 *readme.txt*ファイルに記載されている手順に従う必要があります。 パッケージを実行するには、インストールされているパッケージの `ConfigureSignalR` メソッドを呼び出す OWIN startup クラスを追加する必要があります。 OWIN startup クラスを追加しないと、エラーが表示されます。 この記事の「 [StockTicker サンプルをインストール](#install-the-stockticker-sample)する」セクションを参照してください。

## <a name="prerequisites"></a>前提条件

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) と **ASP.NET および開発**ワークロード。

## <a name="create-the-project"></a>プロジェクトを作成する

このセクションでは、Visual Studio 2017 を使用して空の ASP.NET Web アプリケーションを作成する方法について説明します。

1. Visual Studio で、ASP.NET Web アプリケーションを作成します。

    ![Web の作成](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. **新しい ASP.NET Web アプリケーション-SignalR**ウィンドウで、**空**のままにして [ **OK]** を選択します。

## <a name="set-up-the-server-code"></a>サーバー コードを設定する

このセクションでは、サーバーで実行するコードを設定します。

### <a name="create-the-stock-class"></a>Stock クラスを作成する

まず、在庫に関する情報を格納して送信するために使用する*ストック*モデルクラスを作成します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **クラス**の**追加**] を選択します。

1. クラスに「 *Stock* 」という名前を指定し、プロジェクトに追加します。

1. *Stock.cs*ファイル内のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    株式の作成時に設定する2つのプロパティ (たとえば、Microsoft for Microsoft) と `Price`を `Symbol` します。 その他のプロパティは、`Price`を設定する方法とタイミングによって異なります。 初めて `Price`を設定すると、値が `DayOpen`に反映されます。 その後、`Price`を設定すると、アプリは `Price` と `DayOpen`の違いに基づいて `Change` と `PercentChange` のプロパティ値を計算します。

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>Stockhub および Stockティッカークラスを作成する

SignalR Hub API を使用して、サーバー間の対話を処理します。 SignalR `Hub` クラスから派生した `StockTickerHub` クラスは、クライアントからの接続とメソッド呼び出しの受信を処理します。 また、株価データを保持し、`Timer` オブジェクトを実行する必要もあります。 `Timer` オブジェクトは、クライアント接続に関係なく、定期的に価格の更新をトリガーします。 ハブは一時的なものであるため、これらの関数を `Hub` クラスに配置することはできません。 アプリは、接続やクライアントからサーバーへの呼び出しなど、ハブ上の各タスクの `Hub` クラスインスタンスを作成します。 そのため、株価データを保持するメカニズム、価格更新プログラムを別のクラスで実行する必要があります。 クラスに `StockTicker`という名前を指定します。

![StockTicker からのブロードキャスト](tutorial-server-broadcast-with-signalr/_static/image3.png)

サーバー上で実行する `StockTicker` クラスのインスタンスは1つだけなので、各 `StockTickerHub` インスタンスからシングルトン `StockTicker` インスタンスへの参照を設定する必要があります。 `StockTicker` クラスは、在庫データを持ち、更新をトリガーするため、クライアントにブロードキャストする必要がありますが、`StockTicker` は `Hub` クラスではありません。 `StockTicker` クラスは、SignalR Hub 接続コンテキストオブジェクトへの参照を取得する必要があります。 その後、SignalR 接続コンテキストオブジェクトを使用して、クライアントにブロードキャストできます。

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs の作成

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-SignalR]** で、[**インストールされている** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。

1. クラスに「 *Stockhub* 」という名前を指定し、プロジェクトに追加します。

    この手順では、 *StockTickerHub.cs*クラスファイルを作成します。 同時に、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。

1. *StockTickerHub.cs*ファイル内のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. ファイルを保存します。

このアプリでは、[ハブ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)クラスを使用して、クライアントがサーバーで呼び出すことができるメソッドを定義します。 1つのメソッドを定義しています: `GetAllStocks()`。 クライアントは、最初にサーバーに接続するときに、このメソッドを呼び出して、すべての株式の一覧を現在の価格で取得します。 メソッドは、メモリからデータを返すため、同期的に実行して `IEnumerable<Stock>` を返すことができます。

データベースの検索や web サービスの呼び出しのように、待機時間がかかる処理を実行してデータを取得する必要がある場合は、`Task<IEnumerable<Stock>>` を戻り値として指定し、非同期処理を有効にします。 詳細については、「 [ASP.NET SignalR HUB API Guide-Server-非同期に実行するタイミング](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)」を参照してください。

`HubName` 属性は、アプリがクライアントの JavaScript コードでハブを参照する方法を指定します。 この属性を使用しない場合のクライアントの既定の名前は、キャメルケースバージョンのクラス名です。この場合、この例では `stockTickerHub`します。

後で説明するように、`StockTicker` クラスを作成すると、そのクラスのシングルトンインスタンスが、その静的 `Instance` プロパティに作成されます。 `StockTicker` のシングルトンインスタンスは、接続または切断するクライアントの数に関係なく、メモリ内にあります。 このインスタンスは、`GetAllStocks()` メソッドが現在の株価情報を返すために使用するものです。

#### <a name="create-stocktickercs"></a>StockTicker.cs の作成

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **クラス**の**追加**] を選択します。

1. クラスに「 *Stockticker* 」という名前を指定し、プロジェクトに追加します。

1. *StockTicker.cs*ファイル内のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

すべてのスレッドが同じ StockTicker コードのインスタンスを実行するため、StockTicker クラスはスレッドセーフである必要があります。

### <a name="examine-the-server-code"></a>サーバーコードを確認する

サーバーコードを調べると、アプリがどのように動作するかを理解するのに役立ちます。

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>静的フィールドへのシングルトンインスタンスの格納

このコードは、`Instance` プロパティをクラスのインスタンスにバックアップする静的 `_instance` フィールドを初期化します。 コンストラクターはプライベートであるため、アプリケーションが作成できるクラスの唯一のインスタンスです。 アプリでは、`_instance` フィールドの[遅延初期化](/dotnet/framework/performance/lazy-initialization)が使用されます。 パフォーマンス上の理由ではありません。 インスタンスの作成がスレッドセーフであることを確認する必要があります。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

クライアントがサーバーに接続するたびに、別のスレッドで実行されている Stockkerhub クラスの新しいインスタンスが、`StockTickerHub` クラスで既に説明したように、`StockTicker.Instance` 静的プロパティから Stockティッカーシングルトンインスタンスを取得します。

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary に株式データを格納する

コンストラクターは、いくつかのサンプル株価データを使用して `_stocks` コレクションを初期化し、株式を `GetAllStocks` 返します。 既に説明したように、この株式のコレクションは `StockTickerHub.GetAllStocks`によって返されます。これは、クライアントが呼び出すことができる `Hub` クラスのサーバーメソッドです。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

株式コレクションは、スレッドセーフの[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)型として定義されています。 別の方法として、 [dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)オブジェクトを使用して、変更を行うときに明示的にディクショナリをロックすることもできます。

このサンプルアプリケーションでは、アプリケーションデータをメモリに格納し、アプリが `StockTicker` インスタンスを破棄するときにデータを失うことは問題ありません。 実際のアプリケーションでは、データベースのようなバックエンドデータストアを操作します。

#### <a name="periodically-updating-stock-prices"></a>株価を定期的に更新する

コンストラクターは、在庫価格をランダムに更新するメソッドを定期的に呼び出す `Timer` オブジェクトを開始します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer` は、state パラメーターに null を渡す `UpdateStockPrices`を呼び出します。 価格を更新する前に、アプリは `_updateStockPricesLock` オブジェクトのロックを取得します。 このコードでは、別のスレッドが既に価格を更新しているかどうかを確認し、一覧の各株式に対して `TryUpdateStockPrice` を呼び出します。 `TryUpdateStockPrice` 方法では、株価を変更するかどうか、および変更する量を決定します。 株価が変化した場合、アプリは `BroadcastStockPrice` を呼び出して、接続されているすべてのクライアントに株価の変更をブロードキャストします。

スレッドセーフであることを[確認するため](https://msdn.microsoft.com/library/x13ttww7.aspx)に指定された `_updatingStockPrices` フラグ。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

実際のアプリケーションでは、`TryUpdateStockPrice` メソッドによって web サービスが呼び出され、価格が検索されます。 このコードでは、アプリはランダムな数値ジェネレーターを使用して、変更をランダムに行います。

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>SignalR コンテキストを取得して、StockTicker クラスがクライアントにブロードキャストできるようにする

価格の変更は、`StockTicker` オブジェクトで行われるため、接続されているすべてのクライアントで `updateStockPrice` メソッドを呼び出す必要があります。 `Hub` クラスでは、クライアントメソッドを呼び出すための API がありますが、`StockTicker` は `Hub` クラスから派生しておらず、`Hub` オブジェクトへの参照を持っていません。 接続されたクライアントにブロードキャストするには、`StockTicker` クラスが `StockTickerHub` クラスの SignalR context インスタンスを取得し、それを使用してクライアントのメソッドを呼び出す必要があります。

このコードは、シングルトンクラスのインスタンスを作成するときに SignalR コンテキストへの参照を取得し、その参照をコンストラクターに渡し、コンストラクターがそれを `Clients` プロパティに格納します。

コンテキストを1回だけ取得する理由は2つあります。コンテキストの取得はコストのかかるタスクであり、一度取得すると、クライアントに送信されるメッセージの順序がアプリによって保持されます。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

コンテキストの `Clients` プロパティを取得し、それを `StockTickerClient` プロパティに配置すると、`Hub` クラスと同じように見えるクライアントメソッドを呼び出すためのコードを記述できます。 たとえば、すべてのクライアントにブロードキャストするには、`Clients.All.updateStockPrice(stock)`を記述します。

`BroadcastStockPrice` で呼び出されている `updateStockPrice` メソッドはまだ存在しません。 クライアントで実行されるコードを記述するときに、後で追加します。 `Clients.All` は動的なので、ここで `updateStockPrice` を参照できます。これは、アプリが実行時に式を評価することを意味します。 このメソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。また、クライアントに `updateStockPrice`という名前のメソッドがある場合、アプリはそのメソッドを呼び出し、パラメーター値をそのメソッドに渡します。

`Clients.All` は、すべてのクライアントに送信することを意味します。 SignalR には、に送信するクライアントまたはクライアントのグループを指定するための他のオプションが用意されています。 詳細については、「 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)」を参照してください。

### <a name="register-the-signalr-route"></a>SignalR ルートを登録する

サーバーは、インターセプトする URL と SignalR に送信する URL を認識している必要があります。 これを行うには、OWIN startup クラスを追加します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。

1. **[新しい項目の追加-SignalR]** で、[**インストールされている** > **Visual C#**  > **Web** ] を選択し、 **[OWIN Startup Class]** を選択します。

1. クラスに「 *Startup* 」という名前を指定し、[ **OK]** を選択します。

1. *Startup.cs*ファイルの既定のコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

これで、サーバーコードの設定が完了しました。 次のセクションでは、クライアントを設定します。

## <a name="set-up-the-client-code"></a>クライアントコードの設定

このセクションでは、クライアントで実行するコードを設定します。

### <a name="create-the-html-page-and-javascript-file"></a>HTML ページと JavaScript ファイルを作成する

HTML ページにデータが表示され、JavaScript ファイルによってデータが整理されます。

#### <a name="create-stocktickerhtml"></a>StockTicker .html を作成する

まず、HTML クライアントを追加します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **HTML ページ**の**追加**] を選択します。

1. ファイルに「 *Stockticker* 」という名前を指定し、[ **OK]** を選択します。

1. *Stockticker .html*ファイルの既定のコードを次のコードに置き換えます。

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML では、5つの列、ヘッダー行、および5つのすべての列にまたがる1つのセルを持つデータ行を含むテーブルが作成されます。 データ行に "読み込み中..." と表示されます。アプリが開始されるとすぐに。 JavaScript コードは、その行を削除し、サーバーから取得した在庫データを使用してその行の位置を追加します。

    スクリプトタグでは、次のものを指定します。

    * JQuery スクリプトファイル。

    * SignalR コアスクリプトファイル。

    * SignalR プロキシスクリプトファイル。

    * 後で作成する StockTicker スクリプトファイル。

    アプリによって、SignalR プロキシスクリプトファイルが動的に生成されます。 "/Signalr/hubs" URL を指定し、ハブクラス (この場合は `StockTickerHub.GetAllStocks`) のメソッドのプロキシメソッドを定義します。 必要に応じて、 [SignalR ユーティリティ](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)を使用して、この JavaScript ファイルを手動で生成できます。 `MapHubs` メソッドの呼び出しでは、動的なファイルの作成を無効にすることを忘れないでください。

1. **ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。

    JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。

    > [!IMPORTANT]
    > パッケージマネージャーにより、SignalR スクリプトの新しいバージョンがインストールされます。

1. コードブロック内のスクリプト参照を、プロジェクト内のスクリプトファイルのバージョンに対応するように更新します。

1. **ソリューションエクスプローラー**で、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** を選択します。

#### <a name="create-stocktickerjs"></a>StockTicker を作成する

次に、JavaScript ファイルを作成します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **JavaScript ファイル**の**追加**] を選択します。

1. ファイルに「 *Stockticker* 」という名前を指定し、[ **OK]** を選択します。

1. 次のコードを*Stockticker*ファイルに追加します。

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>クライアントコードを確認する

クライアントコードを確認すると、クライアントコードがサーバーコードと対話してアプリを動作させる方法を理解するのに役立ちます。

#### <a name="starting-the-connection"></a>接続を開始しています

`$.connection` は、SignalR プロキシを参照します。 このコードは、`StockTickerHub` クラスのプロキシへの参照を取得し、それを `ticker` 変数に格納します。 プロキシ名は、`HubName` 属性によって設定された名前です。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

すべての変数と関数を定義した後、ファイルの最後のコード行では、SignalR `start` 関数を呼び出して SignalR 接続を初期化します。 `start` 関数は非同期に実行され、 [JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。 Done 関数を呼び出して、アプリが非同期アクションを終了したときに呼び出す関数を指定できます。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>すべての株式を取得する

`init` 関数は、サーバーで `getAllStocks` 関数を呼び出し、サーバーから返された情報を使用して、stock テーブルを更新します。 既定では、サーバーでメソッド名が pascal 形式であっても、クライアントでキャメルを使用する必要があることに注意してください。 キャメル規則は、オブジェクトではなく、メソッドにのみ適用されます。 たとえば、`stock.symbol` や `stock.price`ではなく、`stock.Symbol` と `stock.Price`を参照しているとします。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

`init` メソッドでは、アプリは、`formatStock` を呼び出して `stock` オブジェクトのプロパティを書式設定し、`supplant` を呼び出して `rowTemplate` 変数内のプレースホルダーを `stock` オブジェクトのプロパティ値に置き換えることによって、サーバーから受け取った各 stock オブジェクトのテーブル行に対して HTML を作成します。 その後、結果として得られる HTML は、stock テーブルに追加されます。

> [!NOTE]
> 非同期 `start` 関数が終了した後に実行される `callback` 関数として渡すことによって、`init` を呼び出します。 `start`を呼び出した後に別の JavaScript ステートメントとして `init` を呼び出すと、関数は失敗します。これは、start 関数が接続の確立を完了するまで待機することなく、すぐに実行されるためです。 この場合、`init` 関数は、アプリがサーバー接続を確立する前に `getAllStocks` 関数の呼び出しを試みます。

#### <a name="getting-updated-stock-prices"></a>更新された株価の取得

サーバーが株価の価格を変更すると、接続されたクライアントで `updateStockPrice` が呼び出されます。 アプリケーションは、関数を `stockTicker` プロキシのクライアントプロパティに追加して、サーバーからの呼び出しで使用できるようにします。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

`updateStockPrice` 関数は、サーバーから受け取った stock オブジェクトを、`init` 関数と同じようにテーブル行に書式設定します。 テーブルに行を追加する代わりに、テーブル内の株価の現在の行を検索し、その行を新しい行に置き換えます。

## <a name="test-the-application"></a>アプリケーションをテストする

アプリをテストして、動作しているかどうかを確認できます。 すべてのブラウザーウィンドウに、在庫価格が変動するライブ株価テーブルが表示されます。

1. ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、アプリをデバッグモードで実行します。

    ![デバッグモードをオンにして [再生] を選択したユーザーのスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    ブラウザーウィンドウが開き、**ライブ株価テーブル**が表示されます。 最初は、stock テーブルに "読み込み中..." と表示されます。行を入力すると、アプリによって最初の株価データが表示され、株価が変化します。

1. ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。

    最初の株価表示は最初のブラウザーと同じであり、同時に変更が行われます。

1. すべてのブラウザーを閉じ、新しいブラウザーを開いて、同じ URL にアクセスします。

    StockTicker シングルトンオブジェクトは引き続きサーバーで実行されます。 **ライブ株価テーブル**には、株式の変化が続いていることが示されています。 最初のテーブルにゼロ変更の数値が表示されません。

1. ブラウザーを閉じます。

## <a name="enable-logging"></a>ログの有効化

SignalR には、クライアントで有効にできる組み込みのログ関数があり、トラブルシューティングに役立ちます。 このセクションでは、ログ記録を有効にし、SignalR が使用している次のトランスポートメソッドのうち、どれがログに記録されるかを示す例を参照してください。

* [Websocket](http://en.wikipedia.org/wiki/WebSocket)。 IIS 8 と現在のブラウザーでサポートされています。

* [サーバーが送信](http://en.wikipedia.org/wiki/Server-sent_events)したイベント (Internet Explorer 以外のブラウザーでサポートされています)。

* [永続的フレーム](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。 Internet Explorer でサポートされています。

* [Ajax の長いポーリング](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)(すべてのブラウザーでサポートされます)。

SignalR は、特定の接続について、サーバーとクライアントの両方でサポートされる最適なトランスポート方法を選択します。

1. *Stockticker*を開きます。

1. 次の強調表示されたコード行を追加して、ファイルの末尾で接続を初期化するコードの直前にログ記録を有効にします。

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. **F5** キーを押してプロジェクトを実行します。

1. ブラウザーの [開発者ツール] ウィンドウを開き、コンソールを選択してログを表示します。 新しい接続のトランスポートメソッドをネゴシエートする SignalR のログを表示するには、ページの更新が必要になる場合があります。

    * Internet Explorer 10 を Windows 8 (IIS 8) で実行している場合、転送方法は**websocket**になります。

    * Internet Explorer 10 を Windows 7 (IIS 7.5) で実行している場合、トランスポート方法は**iframe**です。

    * Windows 8 (IIS 8) で Firefox 19 を実行している場合、転送方法は**websocket**です。

        > [!TIP]
        > Firefox では、コンソールウィンドウを取得するために、消火バグアドインをインストールします。

    * Windows 7 (IIS 7.5) で Firefox 19 を実行している場合、トランスポート方式は**サーバー側で送信**されたイベントです。

## <a name="install-the-stockticker-sample"></a>StockTicker サンプルをインストールする

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample)は、stockticker アプリケーションをインストールします。 NuGet パッケージには、最初から作成した簡易バージョンよりも多くの機能が含まれています。 チュートリアルのこのセクションでは、NuGet パッケージをインストールし、新しい機能とそれらを実装するコードを確認します。

> [!IMPORTANT]
> このチュートリアルの前の手順を実行せずにパッケージをインストールする場合は、プロジェクトに OWIN startup クラスを追加する必要があります。 この手順については、NuGet パッケージ用のこの readme.txt ファイルで説明されています。

### <a name="install-the-signalrsample-nuget-package"></a>SignalR NuGet パッケージをインストールする

1. **ソリューション エクスプローラー**でプロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選びます。

1. **[NuGet パッケージマネージャー: SignalR]** で、 **[参照]** を選択します。

1. **[パッケージソース]** で、 **[nuget.org]** を選択します。

1. 検索ボックスに「 *SignalR* 」と入力し、[ **SignalR** > **インストール**] を選択します。

1. **ソリューションエクスプローラー**で、 *SignalR*フォルダーを展開します。

    SignalR パッケージをインストールすると、フォルダーとその内容が作成されます。

1. *SignalR*フォルダーで、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** を選択します。

    > [!NOTE]
    > SignalR NuGet パッケージをインストールすると、 *Scripts*フォルダーにある jQuery のバージョンが変更される可能性があります。 パッケージによって*SignalR*フォルダーにインストールされる新しい*stockticker .html*ファイルは、パッケージがインストールする jquery バージョンと同期されますが、元の*stockticker*ファイルを再度実行する場合は、最初にスクリプトタグの jquery 参照を更新する必要があります。

### <a name="run-the-application"></a>アプリケーションの実行

 最初のアプリに表示されたテーブルには便利な機能があります。 完全な株式ティッカーアプリケーションでは、新しい機能が表示されます。水平方向のスクロールウィンドウで、色が変化したときに色が変化する株価を表示します。

1. **F5** キーを押して、アプリを実行します。

     アプリを初めて実行すると、"マーケット" が "閉じています" と表示され、静的テーブルと、スクロールしていないティッカーウィンドウが表示されます。

1. **[Open Market]** を選択します。

    ![ライブティッカーのスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **[Live Stock ティッカー]** ボックスが水平にスクロールすると、サーバーは定期的に株価の変化を定期的にブロードキャストし始めます。

    * 株価が変化するたびに、アプリは**Live Stock テーブル**と**live stock ティッカー**の両方を更新します。

    * 株価の変化が正の場合、アプリでは背景が緑色で表示されます。

    * 変更が負の場合、アプリは、赤の背景で株価を表示します。

1. **[マーケットを閉じる]** を選択します。

    * テーブルの更新を停止します。

    * ティッカーはスクロールを停止します。

1. **[リセット]** を選択します。

    * すべての株式データがリセットされます。

    * アプリは、価格の変更が開始される前に初期状態を復元します。

1. ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。

1. 各ブラウザーで同じデータが同時に動的に更新されていることがわかります。

1. いずれかのコントロールを選択すると、すべてのブラウザーが同時に同じように応答します。

### <a name="live-stock-ticker-display"></a>Live Stock ティッカーの表示

**Live Stock ティッカー**の表示は、CSS スタイルによって1行に書式設定された `<div>` 要素内の順序付けられていないリストです。 このアプリでは、テーブルと同じ方法で、`<li>` テンプレート文字列内のプレースホルダーを置き換え、`<li>` 要素を `<ul>` 要素に動的に追加することによって、ティッカーを初期化して更新します。 アプリには、jQuery `animate` 関数を使用したスクロール機能が含まれており、`<div>`内の順序付けられていないリストの左余白を変更します。

#### <a name="signalrsample-stocktickerhtml"></a>SignalR のサンプル

Stock ティッカー HTML コードは次のとおりです。

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR のサンプル

Stock ティッカー CSS コードは次のとおりです。

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR SignalR (サンプルの場合)

スクロールを行う jQuery コードを次に示します。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>クライアントが呼び出すことができるサーバー上の追加のメソッド

アプリに柔軟性を追加するには、アプリが呼び出すことができる追加のメソッドがあります。

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR StockTickerHub.cs

`StockTickerHub` クラスは、クライアントが呼び出すことができる4つの追加のメソッドを定義します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

アプリは、ページの上部にあるボタンに応答して、`OpenMarket`、`CloseMarket`、および `Reset` を呼び出します。 これらは、すべてのクライアントに直ちに反映された状態の変更をトリガーする1つのクライアントのパターンを示しています。 これらの各メソッドは、`StockTicker` クラスのメソッドを呼び出して、市場状態の変化を引き起こし、新しい状態をブロードキャストします。

#### <a name="signalrsample-stocktickercs"></a>SignalR StockTicker.cs

`StockTicker` クラスでは、アプリは `MarketState` 列挙値を返す `MarketState` プロパティを使用して、市場の状態を維持します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

`StockTicker` クラスはスレッドセーフである必要があるため、市場の状態を変更する各メソッドは、ロックブロック内で実行します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

このコードがスレッドセーフであることを確認するには、`volatile`指定された `MarketState` プロパティをバックアップする `_marketState` フィールドを使用します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange` メソッドと `BroadcastMarketReset` メソッドは、既に説明した BroadcastStockPrice メソッドに似ていますが、クライアントで定義されているさまざまなメソッドを呼び出す場合を除きます。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上の追加の関数

`updateStockPrice` 関数はテーブルとティッカーの両方の表示を処理し、`jQuery.Color` を使用して赤と緑の色をフラッシュするようになりました。

*SignalR*の新機能では、マーケットの状態に基づいてボタンを有効または無効にします。 また、 **Live Stock ティッカー**の水平スクロールも停止または開始します。 `ticker.client`には多くの関数が追加されるため、アプリは[jQuery 拡張関数](http://api.jquery.com/jQuery.extend/)を使用して追加します。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>接続を確立した後の追加のクライアントセットアップ

クライアントが接続を確立した後、次のような作業を行う必要があります。

* 市場がオープンまたは閉鎖されているかどうかを調べて、適切な `marketOpened` または `marketClosed` 関数を呼び出します。

* サーバーメソッドの呼び出しをボタンにアタッチします。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

サーバーメソッドは、アプリによって接続が確立されるまで、ボタンには接続されません。 このため、使用可能になる前に、コードがサーバーメソッドを呼び出すことはできません。

## <a name="additional-resources"></a>その他のリソース

このチュートリアルでは、サーバーから接続されているすべてのクライアントにメッセージをブロードキャストする SignalR アプリケーションをプログラミングする方法について学習しました。 これで、定期的にメッセージをブロードキャストしたり、任意のクライアントからの通知に応答したりすることができます。 マルチスレッドシングルトンインスタンスの概念を使用すると、マルチプレーヤーのオンラインゲームシナリオでサーバーの状態を維持できます。 例については、 [SignalR に基づく ShootR ゲーム](https://github.com/NTaylorMullen/ShootR)を参照してください。

ピアツーピア通信のシナリオを示すチュートリアルについては、「[はじめに](introduction-to-signalr.md)と[SignalR を使用したリアルタイム更新](tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。

SignalR の詳細については、次のリソースを参照してください。

* [ASP.NET SignalR](../../index.md)
* [SignalR プロジェクト](http://signalr.net/)
* [SignalR GitHub とサンプル](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * プロジェクトが作成されました
> * サーバー コードを設定する
> * サーバーコードを調べています
> * クライアントコードの設定
> * クライアントコードを調べる
> * アプリケーションをテストする
> * 有効なログ記録

次の記事に進み、ASP.NET SignalR 2 を使用するリアルタイム web アプリケーションを作成する方法を学習してください。
> [!div class="nextstepaction"]
> [SignalR を使用してリアルタイム web アプリを作成する](real-time-web-applications-with-signalr.md)
