---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 'チュートリアル: ASP.NET SignalR 1.x を使用したサーバーブロードキャスト |Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。 サーバーブロードキャストは、communic...
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467932"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>チュートリアル: ASP.NET SignalR 1.x を使用したサーバーブロードキャスト

[Fletcher](https://github.com/pfletcher)、 [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このチュートリアルでは、ASP.NET SignalR を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。 サーバーブロードキャストとは、クライアントに送信される通信がサーバーによって開始されることを意味します。 このシナリオでは、クライアントに送信される通信が1つまたは複数のクライアントによって開始される、チャットアプリケーションなどのピアツーピアシナリオとは異なるプログラミングアプローチが必要です。
> 
> このチュートリアルで作成するアプリケーションは、サーバーブロードキャスト機能の一般的なシナリオである株式ティッカーをシミュレートします。
> 
> このチュートリアルのコメントは歓迎しています。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com)に投稿できます。

## <a name="overview"></a>概要

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet パッケージは、サンプルのシミュレートされた株式ティッカーアプリケーションを Visual Studio プロジェクトにインストールします。 このチュートリアルの最初の部分では、そのアプリケーションの簡略化されたバージョンをゼロから作成します。 このチュートリアルの残りの部分では、NuGet パッケージをインストールし、作成する追加機能とコードを確認します。

Stock ティッカーアプリケーションは、サーバーからすべての接続されたクライアントへの通知を定期的に "プッシュ" またはブロードキャストする、一種のリアルタイムアプリケーションの代表です。

このチュートリアルの最初の部分で作成するアプリケーションには、在庫データを含むグリッドが表示されます。

![StockTicker の初期バージョン](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

定期的にサーバーは株価をランダムに更新し、接続されているすべてのクライアントに更新をプッシュします。 ブラウザーでは、サーバーからの通知に応じて、 **[変更]** 列と [ **%** ] 列の数値と記号が動的に変更されます。 同じ URL に対して追加のブラウザーを開くと、すべてのブラウザーで同じデータと同じデータの変更が同時に表示されます。

このチュートリアルは、次のセクションで構成されています。

- [前提条件](#prerequisites)
- [プロジェクトを作成する](#createproject)
- [SignalR NuGet パッケージを追加する](#nugetpackages)
- [サーバーコードの設定](#server)
- [クライアントコードの設定](#client)
- [アプリケーションをテストする](#test)
- [ログ記録を有効化する](#enablelogging)
- [完全な StockTicker サンプルをインストールして確認する](#fullsample)
- [次の手順](#nextsteps)

> [!NOTE]
> アプリケーションをビルドする手順を実行しない場合は、新しい**空の ASP.NET Web アプリケーション**プロジェクトに SignalR パッケージをインストールし、これらの手順を読んでコードの説明を取得することができます。 このチュートリアルの最初の部分では、SignalR コードのサブセットについて説明します。2番目の部分では、SignalR パッケージの追加機能の主な機能について説明します。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>前提条件

開始する前に、コンピューターに Visual Studio 2012 または 2010 SP1 がインストールされていることを確認してください。 Visual Studio をお持ちでない場合は、無料の Visual Studio 2012 Express for Web を入手するには、 [ASP.NET のダウンロード](https://www.asp.net/downloads)を参照してください。

Visual Studio 2010 を使用している場合は、 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)がインストールされていることを確認します。

<a id="createproject"></a>

## <a name="create-the-project"></a>プロジェクトを作成する

1. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。
2. **[新しいプロジェクト]** ダイアログボックスの [ **C#** **テンプレート**] で展開し、 **[Web]** を選択します。
3. **[ASP.NET 空の Web アプリケーション]** テンプレートを選択し、プロジェクトに*SignalR*という名前を指定して、[ **OK]** をクリックします。

    ![New Project dialog box](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>SignalR NuGet パッケージを追加する

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>SignalR および JQuery NuGet パッケージを追加する

NuGet パッケージをインストールすることによって、SignalR 機能をプロジェクトに追加できます。

1. [ツール] をクリックします。 **NuGet パッケージマネージャー |パッケージマネージャーコンソール**。
2. パッケージマネージャーで、次のコマンドを入力します。

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    SignalR パッケージは、他のいくつかの NuGet パッケージを依存関係としてインストールします。 インストールが完了すると、ASP.NET アプリケーションで SignalR を使用するために必要なすべてのサーバーおよびクライアントコンポーネントが作成されます。

<a id="server"></a>

## <a name="set-up-the-server-code"></a>サーバー コードを設定する

このセクションでは、サーバーで実行するコードを設定します。

### <a name="create-the-stock-class"></a>Stock クラスを作成する

まず、在庫に関する情報を格納して送信するために使用するストックモデルクラスを作成します。

1. プロジェクトフォルダーに新しいクラスファイルを作成し、 *Stock.cs*という名前を付けて、テンプレートコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    株式の作成時に設定する2つのプロパティは、記号 (たとえば、Microsoft の場合は MSFT) と価格です。 その他のプロパティは、価格を設定する方法とタイミングによって異なります。 価格を初めて設定すると、値は DayOpen に反映されます。 Price を設定した後に、Change プロパティと PercentChange プロパティの値は、Price と DayOpen の差に基づいて計算されます。

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>StockTicker および Stockticker クラスを作成する

SignalR Hub API を使用して、サーバー間の対話を処理します。 SignalR Hub クラスから派生する StockTickerHub クラスは、クライアントからの接続の受信とメソッドの呼び出しを処理します。 また、在庫データを保持し、タイマーオブジェクトを実行して、クライアント接続とは関係なく、定期的に価格更新をトリガーする必要があります。 ハブインスタンスは一時的なものであるため、これらの関数をハブクラスに配置することはできません。 ハブクラスのインスタンスは、接続や、クライアントからサーバーへの呼び出しなど、ハブ上の各操作に対して作成されます。 そのため、株価データを保持するメカニズム、価格の更新、価格更新のブロードキャストは、別のクラスで実行する必要があります。このクラスには、StockTicker という名前を指定します。

![StockTicker からのブロードキャスト](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

サーバー上で実行される StockTicker クラスのインスタンスは1つだけなので、各 Stockticker インスタンスからシングルトン StockTicker インスタンスへの参照を設定する必要があります。 StockTicker クラスは、在庫データを持ち、更新をトリガーするため、クライアントにブロードキャストできる必要がありますが、StockTicker はハブクラスではありません。 そのため、StockTicker クラスは、SignalR Hub 接続コンテキストオブジェクトへの参照を取得する必要があります。 その後、SignalR 接続コンテキストオブジェクトを使用して、クライアントにブロードキャストできます。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[新しい項目の追加]** をクリックします。
2. [ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=279941)がインストールされた visual Studio 2012 を使用している場合は、 **[ビジュアルC# ]** の下にある **[Web]** をクリックし、 **SignalR Hub クラス**項目テンプレートを選択します。 それ以外の場合は、 **[クラス]** テンプレートを選択します。
3. 新しいクラスに*StockTickerHub.cs*という名前を指定し、 **[追加]** をクリックします。

    ![StockTickerHub.cs の追加](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. テンプレート コードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [ハブ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)クラスは、クライアントがサーバーで呼び出すことができるメソッドを定義するために使用されます。 1つのメソッドを定義しています: `GetAllStocks()`。 クライアントは、最初にサーバーに接続するときに、このメソッドを呼び出して、すべての株式の一覧を現在の価格で取得します。 メソッドは、メモリからデータを返すため、同期的に実行し、`IEnumerable<Stock>` を返すことができます。 データベース参照や web サービス呼び出しなど、待機する必要のある処理を実行してデータを取得する必要がある場合は、`Task<IEnumerable<Stock>>` を戻り値として指定して、非同期処理を有効にします。 詳細については、「 [ASP.NET SignalR HUB API Guide-Server-非同期に実行するタイミング](index.md)」を参照してください。

    HubName 属性は、クライアントの JavaScript コードでハブを参照する方法を指定します。 この属性を使用しない場合のクライアントの既定の名前は、camel 形式のクラス名です。この場合、この例では、"Stock" になります。

    後で説明するように、StockTicker クラスを作成すると、そのクラスのシングルトンインスタンスが静的インスタンスプロパティに作成されます。 接続または切断するクライアントの数に関係なく、StockTicker のシングルトンインスタンスはメモリに残ります。そのインスタンスは、GetAllStocks メソッドが現在の株価情報を返すために使用するものです。
5. プロジェクトフォルダーに新しいクラスファイルを作成し、 *StockTicker.cs*という名前を付けて、テンプレートコードを次のコードに置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    複数のスレッドが同じ StockTicker コードのインスタンスを実行するため、StockTicker クラスを threadsafe する必要があります。

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>静的フィールドへのシングルトンインスタンスの格納

    このコードは、インスタンスプロパティをクラスのインスタンスとバックする静的 \_インスタンスフィールドを初期化します。これは、コンストラクターがプライベートとしてマークされているため、作成可能なクラスの唯一のインスタンスです。 [遅延初期化](https://msdn.microsoft.com/library/dd997286.aspx)は、パフォーマンス上の理由ではなく、\_インスタンスフィールドに使用されますが、インスタンスの作成が threadsafe されていることを確認します。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    クライアントがサーバーに接続するたびに、別のスレッドで実行されている StockTickerHub クラスの新しいインスタンスが、StockTickerHub クラスで既に説明したように、stockティッカーシングルトンインスタンスを取得します。

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary に株式データを格納する

    コンストラクターは、いくつかのサンプル株式データを使用して \_の株式コレクションを初期化し、GetAllStocks は株式を返します。 既に説明したように、この株式のコレクションは、クライアントが呼び出すことのできるハブクラスのサーバーメソッドである GetAllStocks によって返されます。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    株式コレクションは、スレッドセーフの[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)型として定義されています。 別の方法として、 [dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)オブジェクトを使用して、変更を行うときに明示的にディクショナリをロックすることもできます。

    このサンプルアプリケーションでは、アプリケーションデータをメモリに格納し、StockTicker インスタンスが破棄されたときにデータを失わせることができます。 実際のアプリケーションでは、データベースなどのバックエンドデータストアを使用します。

    ### <a name="periodically-updating-stock-prices"></a>株価を定期的に更新する

    コンストラクターは、在庫価格をランダムに更新するメソッドを定期的に呼び出すタイマーオブジェクトを開始します。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices は、state パラメーターに null を渡すタイマーによって呼び出されます。 価格を更新する前に、\_updateStockPricesLock オブジェクトに対してロックが取得されます。 このコードでは、別のスレッドが既に価格を更新しているかどうかを確認し、一覧の各株式で TryUpdateStockPrice を呼び出します。 TryUpdateStockPrice メソッドは、株価を変更するかどうか、および変更する量を決定します。 株価が変更された場合、BroadcastStockPrice が呼び出され、すべての接続されたクライアントに株価の変更がブロードキャストされます。

    \_updatingStockPrices フラグは、threadsafe にアクセスできるように、 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)としてマークされています。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    実際のアプリケーションでは、TryUpdateStockPrice メソッドは web サービスを呼び出して価格を検索します。このコードでは、ランダムな数値ジェネレーターを使用して、変更をランダムに行います。

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>SignalR コンテキストを取得して、StockTicker クラスがクライアントにブロードキャストできるようにする

    ここでは、価格の変更は StockTicker オブジェクトで行われるため、接続されているすべてのクライアントで updateStockPrice メソッドを呼び出す必要があります。 ハブクラスでは、クライアントメソッドを呼び出すための API がありますが、StockTicker はハブクラスから派生しておらず、どのハブオブジェクトへの参照も持っていません。 したがって、接続されたクライアントにブロードキャストするために、StockTicker クラスは、Stockticker クラスの SignalR context インスタンスを取得し、それを使用してクライアントでメソッドを呼び出す必要があります。

    このコードは、シングルトンクラスのインスタンスを作成するときに SignalR コンテキストへの参照を取得し、その参照をコンストラクターに渡し、コンストラクターがそれをクライアントプロパティに格納します。

    コンテキストを一度だけ取得する理由は2つあります。コンテキストの取得は負荷の高い操作であるため、一度取得すると、クライアントに送信されるメッセージの順序が確実に維持されます。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    コンテキストのクライアントプロパティを取得し、それを Stockclients クライアントプロパティに格納すると、ハブクラスと同じように見えるクライアントメソッドを呼び出すためのコードを記述できます。 たとえば、すべてのクライアントにブロードキャストするには、クライアントを作成します。すべての updateStockPrice (stock).

    BroadcastStockPrice で呼び出されている updateStockPrice メソッドはまだ存在しません。クライアントで実行されるコードを記述するときに、後で追加します。 クライアントが動的であるため、ここでは updateStockPrice を参照できます。これは、実行時に式が評価されることを意味します。 このメソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。クライアントに updateStockPrice という名前のメソッドがある場合は、そのメソッドが呼び出され、パラメーター値が渡されます。

    クライアント。 All はすべてのクライアントに送信することを意味します。 SignalR には、に送信するクライアントまたはクライアントのグループを指定するための他のオプションが用意されています。 詳細については、「 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)」を参照してください。

### <a name="register-the-signalr-route"></a>SignalR ルートを登録する

サーバーは、インターセプトする URL と SignalR に送信する URL を認識している必要があります。 そのためには、 *global.asax*ファイルにいくつかのコードを追加します。

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[新しい項目の追加]** をクリックします。
2. **グローバルアプリケーションクラス**項目テンプレートを選択し、 **[追加]** をクリックします。

    ![Global.asax の追加](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. SignalR route 登録コードをアプリケーション\_の開始メソッドに追加します。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    既定では、すべての SignalR トラフィックのベース URL は "/signalr" で、"/signalr/hubs" は、アプリケーション内のすべてのハブのプロキシを定義する動的に生成された JavaScript ファイルを取得するために使用されます。 MapHubs メソッドには、 [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx)クラスのインスタンスで別のベース URL と特定の SignalR オプションを指定できるオーバーロードが含まれています。
4. ファイルの先頭に using ステートメントを追加します。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. *Global.asax*ファイルを保存して閉じ、プロジェクトをビルドします。

これで、サーバーコードの設定が完了しました。 次のセクションでは、クライアントを設定します。

<a id="client"></a>

## <a name="set-up-the-client-code"></a>クライアントコードの設定

1. プロジェクトフォルダーに新しい HTML ファイルを作成し、「 *Stockticker .html*」という名前を指定します。
2. テンプレート コードを次のコードに置き換えます。

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML では、5つの列、ヘッダー行、および5つのすべての列にまたがる1つのセルを持つデータ行を含むテーブルが作成されます。 データ行に "読み込み中..." と表示されます。とは、アプリケーションの起動時にすぐに表示されます。 JavaScript コードは、その行を削除し、サーバーから取得した在庫データを使用してその行の位置を追加します。

    スクリプトタグは、jQuery スクリプトファイル、SignalR コアスクリプトファイル、SignalR プロキシスクリプトファイル、および後で作成する StockTicker スクリプトファイルを指定します。 "/Signalr/hubs" URL を指定する SignalR proxy スクリプトファイルが動的に生成され、ハブクラス (この場合は GetAllStocks) のメソッドのプロキシメソッドを定義します。 必要に応じて、 [SignalR ユーティリティ](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)を使用してこの JavaScript ファイルを手動で生成し、maphubs メソッド呼び出しでの動的ファイル作成を無効にすることができます。
3. > [!IMPORTANT]
   > *Stockticker .html*の JavaScript ファイル参照が正しいことを確認します。 つまり、スクリプトタグの jQuery バージョン (例では 1.8.2) がプロジェクトの*scripts*フォルダー内の jquery バージョンと同じであることを確認し、スクリプトタグの SignalR バージョンがプロジェクトの*Scripts*フォルダーの SignalR バージョンと同じであることを確認します。 必要に応じて、スクリプトタグ内のファイル名を変更します。
4. **ソリューションエクスプローラー**で、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** をクリックします。
5. プロジェクトフォルダーに新しい JavaScript ファイルを作成し、*という名前*を指定します。
6. テンプレート コードを次のコードに置き換えます。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $. connection は、SignalR プロキシを参照します。 このコードは、Stockhub クラスのプロキシへの参照を取得し、それをティッカー変数に格納します。 プロキシ名は、[HubName] 属性によって設定された名前です。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    すべての変数と関数が定義された後、ファイル内の最後のコード行は、SignalR start 関数を呼び出すことによって SignalR 接続を初期化します。 Start 関数は非同期に実行され、 [JQuery 遅延オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。つまり、done 関数を呼び出して、非同期操作の完了時に呼び出す関数を指定できます。「」をご覧ください。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Init 関数は、サーバー上で getAllStocks 関数を呼び出し、サーバーから返された情報を使用して、stock テーブルを更新します。 既定では、クライアントで camel 形式の文字種を使用する必要があることに注意してください。ただし、サーバーでは、メソッド名は pascal 形式です。 Camel 形式の規則は、オブジェクトではなく、メソッドにのみ適用されます。 たとえば、stock を参照します。シンボルと株価。株価、証券、株価はありません。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    クライアントで pascal 形式の表記を使用する場合、またはまったく異なる方法名を使用する場合は、HubName 属性を使用してハブクラス自体を修飾するのと同じ方法で、ハブメソッドを HubMethodName 属性で修飾できます。

    Init メソッドでは、formatStock を呼び出して stock オブジェクトのプロパティを書式設定することによって、サーバーから受信した各 stock オブジェクトに対してテーブル行の HTML が作成されます。次に、代わりを呼び出して ( *Stockticker*の先頭で定義されている)、stock オブジェクトのプロパティ値で行テンプレート変数のプレースホルダーを置き換えます。 その後、結果として得られる HTML は、stock テーブルに追加されます。

    Init を呼び出すには、非同期の開始関数が完了した後に実行されるコールバック関数としてを渡します。 Start を呼び出した後に別の JavaScript ステートメントとして init を呼び出した場合、関数は失敗します。これは、start 関数が接続の確立を完了するまで待機することなく、すぐに実行されるためです。 その場合、init 関数は、サーバー接続が確立される前に、getAllStocks 関数を呼び出そうとします。

    サーバーが株価の価格を変更すると、接続されているクライアントで updateStockPrice が呼び出されます。 関数は、サーバーからの呼び出しで使用できるようにするために、stockTicker プロキシのクライアントプロパティに追加されます。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    UpdateStockPrice 関数は、サーバーから受け取った stock オブジェクトを、init 関数と同じようにテーブルの行に書式設定します。 ただし、テーブルに行を追加するのではなく、テーブル内の株価の現在の行を検索し、その行を新しい行に置き換えます。

<a id="test"></a>

## <a name="test-the-application"></a>アプリケーションをテストする

1. F5 キーを押してデバッグ モードでアプリケーションを実行します。

    Stock テーブルでは、最初に "読み込み中..." と表示されます。行を入力すると、最初の株式データが表示されます。その後、株価が変化します。

    ![読み込み](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![最初のストックテーブル](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![サーバーから変更を受信する株価テーブル](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. ブラウザーのアドレスバーから URL をコピーして、1つまたは複数の新しいブラウザーウィンドウに貼り付けます。

    最初の株価表示は最初のブラウザーと同じであり、同時に変更が行われます。
3. すべてのブラウザーを閉じて新しいブラウザーを開き、同じ URL にアクセスします。

    StockTicker シングルトンオブジェクトは引き続きサーバーで実行されているので、stock テーブルの表示では、株式の変更が継続されていることが示されています。 (最初のテーブルにゼロ変更の数値が表示されません)。
4. ブラウザーを閉じます。

<a id="enablelogging"></a>

## <a name="enable-logging"></a>ログの有効化

SignalR には、クライアントで有効にできる組み込みのログ関数があり、トラブルシューティングに役立ちます。 このセクションでは、ログ記録を有効にし、SignalR が使用している次のトランスポートメソッドのうち、どれがログによってどのように表示されるかを示す例を参照してください。

- [Websocket](http://en.wikipedia.org/wiki/WebSocket)。 IIS 8 と現在のブラウザーでサポートされています。
- [サーバーが送信](http://en.wikipedia.org/wiki/Server-sent_events)したイベント (Internet Explorer 以外のブラウザーでサポートされています)。
- [永続的フレーム](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。 Internet Explorer でサポートされています。
- [Ajax の長いポーリング](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)(すべてのブラウザーでサポートされます)。

SignalR は、特定の接続について、サーバーとクライアントの両方でサポートされる最適なトランスポート方法を選択します。

1. *Stockticker js*を開き、ファイルの末尾で接続を初期化するコードの直前にログ記録を有効にするコード行を追加します。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. F5 キーを押してプロジェクトを実行します。
3. ブラウザーの [開発者ツール] ウィンドウを開き、コンソールを選択してログを表示します。 新しい接続のトランスポートメソッドをネゴシエートする Signalr のログを表示するには、ページの更新が必要になる場合があります。

    Internet Explorer 10 を Windows 8 (IIS 8) で実行している場合、転送方法は Websocket になります。

    ![IE 10 IIS 8 コンソール](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    Internet Explorer 10 を Windows 7 (IIS 7.5) で実行している場合、トランスポート方法は iframe です。

    ![IE 10 コンソール、IIS 7.5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    Firefox では、コンソールウィンドウを取得するために、消火バグアドインをインストールします。 Windows 8 (IIS 8) で Firefox 19 を実行している場合、転送方法は Websocket です。

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    Windows 7 (IIS 7.5) で Firefox 19 を実行している場合、トランスポート方法はサーバーから送信されたイベントです。

    ![Firefox 19 IIS 7.5 コンソール](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>完全な StockTicker サンプルをインストールして確認する

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet パッケージによってインストールされる stockticker アプリケーションには、最初から作成した簡易バージョンよりも多くの機能が含まれています。 チュートリアルのこのセクションでは、NuGet パッケージをインストールし、新しい機能とそれらを実装するコードを確認します。

### <a name="install-the-signalrsample-nuget-package"></a>SignalR NuGet パッケージをインストールする

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[NuGet パッケージの管理]** をクリックします。
2. **[NuGet パッケージの管理]** ダイアログボックスで、 **[オンライン]** をクリックし、 **[オンライン検索]** ボックスに「 *SignalR* 」と入力して、 **SignalR**パッケージの **[インストール]** をクリックします。

    ![SignalR パッケージをインストールします。](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. *Global.asax*ファイルで、Routetable. ルート. maphubs (); をコメントアウトします。アプリケーション\_の開始メソッドで前に追加した行。

    SignalR パッケージは、 *\_アプリ*に SignalR ルートを登録するため、 *global.asax*のコードは不要になりました。これは、ファイルを起動します。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    アセンブリ属性によって参照される WebActivator クラスは、SignalR パッケージの依存関係としてインストールされる WebActivatorEx NuGet パッケージに含まれています。
4. **ソリューションエクスプローラー**で、SignalR パッケージをインストールすることによって作成された*SignalR*フォルダーを展開します。
5. *SignalR*フォルダーで、[ *stockticker .html*] を右クリックし、 **[スタートページとして設定]** をクリックします。

    > [!NOTE]
    > SignalR NuGet パッケージをインストールすると、 *Scripts*フォルダーにある jQuery のバージョンが変更される可能性があります。 パッケージによって*SignalR*フォルダーにインストールされる新しい*stockticker .html*ファイルは、パッケージがインストールする jquery バージョンと同期されますが、元の*stockticker*ファイルを再度実行する場合は、最初にスクリプトタグの jquery 参照を更新する必要があります。

### <a name="run-the-application"></a>アプリケーションの実行

1. F5 キーを押してアプリケーションを実行します。

    先ほど見たグリッドに加えて、完全な株式ティッカーアプリケーションでは、同じ在庫データを表示する水平スクロールウィンドウが表示されます。 アプリケーションを初めて実行すると、"market" が "closed" になり、静的グリッドと、スクロールしていないティッカーウィンドウが表示されます。

    ![StockTicker 画面の開始](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    **[Open Market]** をクリックすると、 **[Live stock ティッカー]** ボックスが水平方向にスクロールし、サーバーが定期的に株価の変更を定期的にブロードキャストするようになります。 株価が変化するたびに、 **Live Stock テーブル**グリッドと**live stock ティッカー**ボックスの両方が更新されます。 株価の変化が正の場合は、株価が緑で表示され、変更が負の場合は、株価が赤の背景で表示されます。

    ![StockTicker アプリ, マーケットオープン](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    **[マーケットを閉じる]** ボタンをクリックすると、変更が停止し、ティッカースクロールが停止します。 **[リセット]** ボタンをクリックすると、価格の変更が開始される前に、すべての株式データが初期状態にリセットされます ブラウザーウィンドウをさらに開いて同じ URL にアクセスすると、各ブラウザーで同じデータが同時に動的に更新されます。 いずれかのボタンをクリックすると、すべてのブラウザーが同時に同じように応答します。

### <a name="live-stock-ticker-display"></a>Live Stock ティッカーの表示

**Live Stock ティッカー**の表示は、div 要素内の順序付けられていないリストで、CSS スタイルによって1行に書式設定されます。 このティッカーは、テーブルと同じ方法で初期化および更新されます。 &lt;li&gt; テンプレート文字列のプレースホルダーを置換し、&lt;li&gt; 要素を &lt;ul&gt; 要素に動的に追加します。 スクロールは、div 内の順序付けられていないリストの左余白を変更する jQuery アニメーション関数を使用して実行されます。

Stock ティッカー HTML:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

Stock ティッカー CSS:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

スクロールを行う jQuery コードを次に示します。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>クライアントが呼び出すことができるサーバー上の追加のメソッド

Stockhub クラスは、クライアントが呼び出すことのできる4つの追加のメソッドを定義します。

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

OpenMarket、CloseMarket、Reset は、ページの上部にあるボタンへの応答として呼び出されます。 この例では、1つのクライアントが、すべてのクライアントに直ちに伝達される状態の変更をトリガーするパターンを示します。 これらの各メソッドは、市場の状態の変化に影響を与える StockTicker クラスのメソッドを呼び出し、新しい状態をブロードキャストします。

StockTicker クラスでは、MarketState 列挙値を返す MarketState プロパティによって、市場の状態が維持されます。

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

StockTicker クラスは threadsafe する必要があるため、次のようにして、市場の状態を変更する各メソッドがロックブロック内で実行されます。

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

このコードが threadsafe であることを確認するために、MarketState プロパティをバックする \_marketState フィールドは volatile としてマークされています。

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

BroadcastMarketStateChange メソッドと BroadcastMarketReset メソッドは、既に説明した BroadcastStockPrice メソッドに似ていますが、クライアントで定義されているさまざまなメソッドを呼び出す点が異なります。

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上の追加の関数

UpdateStockPrice 関数は、グリッドとティッカーの両方の表示を処理するようになりました。また、jQuery 色を使用して赤と緑の色をフラッシュします。

*SignalR*の新しい関数では、市場の状態に基づいてボタンを有効または無効にし、ティッカーウィンドウの水平スクロールを停止または開始します。 複数の関数がティッカー. client に追加されるため、 [jQuery 拡張関数](http://api.jquery.com/jQuery.extend/)を使用して追加します。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>接続を確立した後の追加のクライアントセットアップ

クライアントが接続を確立した後、適切な marketOpened または marketClosed 関数を呼び出すために市場が開いているか閉じられたかを確認し、サーバーメソッドの呼び出しをボタンにアタッチします。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

サーバーメソッドは、接続が確立されるまで、ボタンには接続されません。そのため、コードは、使用可能になる前にサーバーメソッドを呼び出すことができません。

<a id="nextsteps"></a>

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、定期的に、または任意のクライアントからの通知に応答して、サーバーからすべての接続されたクライアントにメッセージをブロードキャストする SignalR アプリケーションをプログラミングする方法を学習しました。 マルチスレッドシングルトンインスタンスを使用してサーバーの状態を維持するパターンは、マルチプレーヤーのオンラインゲームのシナリオでも使用できます。 例について[は、SignalR に基づく ShootR ゲーム](https://github.com/NTaylorMullen/ShootR)を参照してください。

ピアツーピア通信のシナリオを示すチュートリアルについては、「[はじめに](index.md)と[SignalR を使用したリアルタイム更新](index.md)」を参照してください。

より高度な SignalR 開発の概念については、次のサイトで SignalR ソースコードとリソースを参照してください。

- [ASP.NET SignalR](https://asp.net/signalr/)
- [SignalR プロジェクト](http://signalr.net/)
- [SignalR Github とサンプル](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
