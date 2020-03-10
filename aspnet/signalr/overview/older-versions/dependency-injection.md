---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR 1.x での依存関係の注入 |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431542"
---
# <a name="dependency-injection-in-signalr-1x"></a>SignalR 1.x の依存関係挿入

[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

依存関係の挿入は、オブジェクト間のハードコーディングされた依存関係を削除する方法であり、テスト (モックオブジェクトを使用) または実行時の動作の変更のために、オブジェクトの依存関係を簡単に置き換えることができます。 このチュートリアルでは、SignalR hub で依存関係の挿入を実行する方法について説明します。 また、SignalR で IoC コンテナーを使用する方法も示します。 IoC コンテナーは、依存関係の挿入のための一般的なフレームワークです。

## <a name="what-is-dependency-injection"></a>依存関係の挿入とは

依存関係の挿入について既によく理解している場合は、このセクションをスキップしてください。

*依存関係の挿入*(DI) は、オブジェクトが独自の依存関係を作成することを担当しないパターンです。 DI を動機付けする簡単な例を次に示します。 メッセージをログに記録する必要があるオブジェクトがあるとします。 ログインターフェイスを定義することもできます。

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

オブジェクトでは、メッセージをログに記録するための `ILogger` を作成できます。

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

これは機能しますが、最適な設計ではありません。 `FileLogger` を別の `ILogger` 実装に置き換える場合は、`SomeComponent`を変更する必要があります。 他のオブジェクトの中には `FileLogger`を使用するものがあるため、すべてを変更する必要があります。 または、シングルトン `FileLogger` する場合は、アプリケーション全体で変更を行う必要があります。

より適切な方法は、コンストラクター引数を使用して、オブジェクトに `ILogger` を "挿入" することです。

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

これで、オブジェクトは、使用する `ILogger` を選択する責任を負いません。 `ILogger` の実装は、依存するオブジェクトを変更せずに切り替えることができます。

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

このパターンは、[コンストラクターの挿入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)と呼ばれます。 もう1つのパターンは setter インジェクションで、setter メソッドまたはプロパティを使用して依存関係を設定します。

## <a name="simple-dependency-injection-in-signalr"></a>SignalR での単純な依存関係の挿入

[SignalR を使用](../getting-started/tutorial-getting-started-with-signalr.md)したチュートリアルはじめにのチャットアプリケーションについて考えてみましょう。 そのアプリケーションのハブクラスを次に示します。

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

送信前にチャットメッセージをサーバーに保存するとします。 この機能を抽象化するインターフェイスを定義し、DI を使用して `ChatHub` クラスにインターフェイスを挿入することもできます。

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

唯一の問題は、SignalR アプリケーションが直接ハブを作成しないことです。SignalR によって作成されます。 既定では、SignalR はハブクラスにパラメーターなしのコンストラクターがあることを想定しています。 ただし、ハブインスタンスを作成する関数を簡単に登録し、この関数を使用して DI を実行できます。 **Globalhost. DependencyResolver. register**を呼び出して、関数を登録します。

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

これで、SignalR インスタンス `ChatHub` を作成する必要があるときに、はこの匿名関数を呼び出します。

## <a name="ioc-containers"></a>IoC コンテナー

前のコードは、単純なケースでは問題ありません。 しかし、次のように記述する必要がありました。

[!code-css[Main](dependency-injection/samples/sample8.css)]

多くの依存関係がある複雑なアプリケーションでは、この "配線" コードの多くを記述しなければならない場合があります。 特に依存関係が入れ子になっている場合は、このコードを維持することは困難です。 単体テストも困難です。

1つの解決策は、IoC コンテナーを使用することです。 IoC コンテナーは、依存関係の管理を担当するソフトウェアコンポーネントです。型をコンテナーに登録した後、コンテナーを使用してオブジェクトを作成します。 コンテナーは、依存関係の関係を自動的に判別します。 多くの IoC コンテナーでは、オブジェクトの有効期間やスコープなどを制御することもできます。

> [!NOTE]
> "IoC" は、フレームワークがアプリケーションコードを呼び出す一般的なパターンである "コントロールの反転" を表します。 IoC コンテナーによってオブジェクトが構築され、通常の制御フローが "反転" されます。

## <a name="using-ioc-containers-in-signalr"></a>SignalR での IoC コンテナーの使用

多くの場合、このチャットアプリケーションは、IoC コンテナーを活用するのには簡単ではありません。 では、 [Stockticker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)サンプルを見てみましょう。

StockTicker サンプルでは、次の2つの主要なクラスを定義します。

- `StockTickerHub`: クライアント接続を管理するハブクラス。
- `StockTicker`: 株価を保持し、定期的に更新するシングルトン。

`StockTickerHub` は `StockTicker` シングルトンへの参照を保持し、`StockTicker` は `StockTickerHub`の**IHubConnectionContext**への参照を保持します。 このインターフェイスを使用して、`StockTickerHub` インスタンスと通信します。 (詳細については、「 [ASP.NET SignalR でのサーバーブロードキャスト](index.md)」を参照してください)。

IoC コンテナーを使用して、これらの依存関係をビットに untangle ことができます。 まず、`StockTickerHub` クラスと `StockTicker` クラスを簡略化しましょう。 次のコードでは、必要のない部分をコメント化しています。

パラメーターなしのコンストラクターを `StockTicker`から削除します。 代わりに、常に DI を使用してハブを作成します。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

StockTicker の場合は、シングルトンインスタンスを削除します。 後で、IoC コンテナーを使用して StockTicker の有効期間を制御します。 また、コンストラクターをパブリックにします。

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

次に、`StockTicker`のインターフェイスを作成してコードをリファクターできます。 このインターフェイスを使用して、`StockTicker` クラスの `StockTickerHub` を分離します。

この種のリファクタリングは、Visual Studio によって簡単に行うことができます。 StockTicker.cs ファイルを開き、`StockTicker` クラスの宣言を右クリックして、[**リファクター** ...] を選択します。**インターフェイスを抽出**します。

![](dependency-injection/_static/image1.png)

**[インターフェイスの抽出]** ダイアログで、 **[すべて選択]** をクリックします。 他の既定値はそのままにします。 **[OK]** をクリックします。

![](dependency-injection/_static/image2.png)

Visual Studio によって `IStockTicker`という名前の新しいインターフェイスが作成され、`IStockTicker`から派生する `StockTicker` も変更されます。

IStockTicker.cs ファイルを開き、インターフェイスを**public**に変更します。

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

`StockTickerHub` クラスで、`StockTicker` の2つのインスタンスを `IStockTicker`に変更します。

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

`IStockTicker` インターフェイスの作成は、厳密には必要ありませんが、アプリケーション内のコンポーネント間の結合を減らすために DI がどのように役立つかを説明したいと考えました。

## <a name="add-the-ninject-library"></a>Ninject ライブラリを追加する

.NET 用に多数のオープンソースの IoC コンテナーがあります。 このチュートリアルでは、 [Ninject](http://www.ninject.org/)を使用します。 (他の一般的なライブラリには、[城主の Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)、および構造体の[マップ](http://docs.structuremap.net)が含まれています)。

NuGet パッケージマネージャーを使用して、 [Ninject ライブラリ](https://nuget.org/packages/Ninject/3.0.1.10)をインストールします。 Visual Studio で、 **[ツール]** メニューの [ **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>SignalR Dependency Resolver を置き換える

SignalR 内で Ninject を使用するには、 **Defaultdependencyresolver**から派生するクラスを作成します。

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

このクラスは、 **Defaultdependencyresolver**の**GetService**メソッドと**getservices**メソッドをオーバーライドします。 SignalR は、これらのメソッドを呼び出して、ハブインスタンスを含む、実行時にさまざまなオブジェクトを作成します。また、SignalR によって内部的に使用されるさまざまなサービスを作成します。

- **GetService**メソッドは、型の1つのインスタンスを作成します。 Ninject カーネルの**Tryget**メソッドを呼び出すには、このメソッドをオーバーライドします。 このメソッドが null を返す場合は、既定の競合回避モジュールに戻ります。
- **Getservices**メソッドは、指定された型のオブジェクトのコレクションを作成します。 このメソッドをオーバーライドして、Ninject の結果と既定の競合回避モジュールの結果を連結します。

## <a name="configure-ninject-bindings"></a>Ninject バインドを構成する

ここで、Ninject を使用して型バインドを宣言します。

RegisterHubs.cs ファイルを開きます。 `RegisterHubs.Start` メソッドで、ninject コンテナーを作成します。 Ninject は*カーネル*を呼び出します。

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

カスタム依存関係競合回避モジュールのインスタンスを作成します。

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

次のように `IStockTicker` のバインドを作成します。

[!code-html[Main](dependency-injection/samples/sample17.html)]

このコードは2つのことを言います。 まず、アプリケーションに `IStockTicker`が必要な場合は常に、カーネルが `StockTicker`のインスタンスを作成する必要があります。 次に、`StockTicker` クラスをシングルトンオブジェクトとして作成する必要があります。 Ninject は、オブジェクトのインスタンスを1つ作成し、要求ごとに同じインスタンスを返します。

次のように、 **IHubConnectionContext**のバインドを作成します。

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

このコードは、 **IHubConnection**を返す匿名関数を作成します。 **WhenInjectedInto**メソッドは、`IStockTicker` のインスタンスを作成するときにのみ、この関数を使用するように ninject を指示します。 その理由は、SignalR が**IHubConnectionContext**インスタンスを内部で作成し、SignalR がそれらを作成する方法をオーバーライドしないためです。 この関数は、`StockTicker` クラスにのみ適用されます。

**Maphubs**メソッドに依存関係競合回避モジュールを渡します。

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

SignalR では、既定の競合回避モジュールではなく、 **Maphubs**に指定されている競合回避モジュールが使用されるようになりました。

`RegisterHubs.Start`の完全なコードリストを次に示します。

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

Visual Studio で StockTicker アプリケーションを実行するには、F5 キーを押します。 ブラウザーウィンドウで、`http://localhost:*port*/SignalR.Sample/StockTicker.html`に移動します。

![](dependency-injection/_static/image3.png)

アプリケーションの機能は以前とまったく同じです。 (説明については、「 [ASP.NET SignalR でのサーバーブロードキャスト](index.md)」を参照してください)。動作は変更されていません。コードを簡単にテスト、保守、および進化させることができました。
