---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web フォーム接続の回復性とコマンドインターセプト |Microsoft Docs
author: Erikre
description: このチュートリアルでは、接続の回復性とコマンドインターセプトをサポートするようにサンプルアプリケーションを変更する方法について説明します。
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 95f0b5635c12d5ef88622e5766c1278c6570dd4d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484234"
---
# <a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web フォームの接続回復性とコマンド傍受

[Erik Reitan](https://github.com/Erikre)

このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、接続の回復性とコマンドのインターセプトをサポートします。 接続の回復性を有効にすることで、Wingtip Toys サンプルアプリケーションは、クラウド環境の典型的な一時的なエラーが発生したときに、自動的にデータ呼び出しを再試行します。 また、コマンドインターセプトを実装することにより、Wingtip Toys サンプルアプリケーションは、データベースに送信されたすべての SQL クエリをログに記録または変更するためにキャッチします。

> [!NOTE] 
> 
> この Web フォームチュートリアルは、Tom Dykstra の次の MVC チュートリアルに基づいています。  
> [ASP.NET MVC アプリケーションでの Entity Framework を使用した接続の回復性とコマンドのインターセプト](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="what-youll-learn"></a>ここでは、次の内容について学習します。

- 接続の回復性を提供する方法。
- コマンドインターセプトを実装する方法。

## <a name="prerequisites"></a>前提条件

開始する前に、次のソフトウェアがコンピューターにインストールされていることを確認してください。

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)または[Web 用 Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 .NET Framework は自動的にインストールされます。
- Wingtip toys のサンプルプロジェクト。 Wingtip Toys プロジェクト内のこのチュートリアルで説明されている機能を実装できます。 ダウンロードの詳細については、次のリンクを使用してください。

    - [ASP.NET 4.5.1 Web フォーム (Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) ) (C#) でのはじめに
- このチュートリアルを完了する前に、関連するチュートリアルシリーズ[はじめに (ASP.NET 4.5 Web フォームおよび Visual Studio 2013](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)) を確認することを検討してください。 チュートリアルシリーズでは、**ウィング・ toys 社**のプロジェクトとコードについて理解を深めることができます。

## <a name="connection-resiliency"></a>接続の回復性

アプリケーションを Windows Azure に展開する場合、考慮する必要がある1つのオプションは、データベースをクラウドデータベースサービスである**windows** **Azure SQL Database**に展開することです。 通常、一時的な接続エラーは、web サーバーとデータベースサーバーが同じデータセンターに直接接続されている場合よりも、クラウドデータベースサービスに接続すると、より頻繁に発生します。 クラウド web サーバーとクラウドデータベースサービスが同じデータセンターでホストされている場合でも、ロードバランサーなど、問題が発生する可能性のあるネットワーク接続が増加します。

また、クラウドサービスは通常、他のユーザーによって共有されます。これは、そのサービスの応答性が影響を受ける可能性があることを意味します。 また、データベースへのアクセスが制限される可能性があります。 調整とは、データベースサービスが、*サービスレベルアグリーメント*(SLA) で許可されているよりも頻繁にアクセスしようとした場合に、例外をスローすることを意味します。

クラウドサービスにアクセスするときに発生する接続の問題の多くは、一時的なものです。つまり、短時間に解決されます。 そのため、データベース操作を試行して、通常は一時的なエラーの種類を取得した場合は、しばらく待ってから操作を再試行することができ、操作は成功する可能性があります。 一時的なエラーを自動的に再試行することによって、ユーザーにとってより良いエクスペリエンスを提供できます。そのほとんどは、顧客に対して非表示になります。 Entity Framework 6 の接続の復元機能では、失敗した SQL クエリを再試行するプロセスを自動化できます。

接続の回復性機能は、特定のデータベースサービスに対して適切に構成されている必要があります。

1. どの例外が一時的なものである可能性があるかを把握しておく必要があります。 たとえば、プログラムのバグによるエラーではなく、ネットワーク接続が一時的に失われたことによって発生したエラーを再試行します。
2. 失敗した操作が再試行されるまでの間、適切な時間を待機する必要があります。 バッチ処理の再試行の間隔は、ユーザーが応答を待機しているオンライン web ページの場合よりも長くなる可能性があります。
3. この場合は、適切な回数の再試行を行う必要があります。 バッチ処理では、オンラインアプリケーションの場合と同じように再試行することができます。

これらの設定は、Entity Framework プロバイダーでサポートされている任意のデータベース環境に対して手動で構成できます。

接続の回復性を有効にするために必要なのは、`DbConfiguration` クラスから派生したクラスをアセンブリに作成することだけです。このクラスでは、SQL Database 実行戦略を設定します。これは Entity Framework の再試行ポリシーに関するもう1つの用語です。

### <a name="implementing-connection-resiliency"></a>接続の回復性の実装

1. Visual Studio で、[ウィングヒント toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409)のサンプル Web フォームアプリケーションをダウンロードして開きます。
2. **ウィング? toys**アプリケーションの*Logic*フォルダーで、 *WingtipToysConfiguration.cs*という名前のクラスファイルを追加します。
3. 既存のコードを次のコードに置き換えます。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

Entity Framework は、`DbConfiguration`から派生したクラスで検出されたコードを自動的に実行します。 `DbConfiguration` クラスを使用する*と、web.config ファイルで*実行するコードで構成タスクを実行できます。 詳細については、「 [Entityframework コードベースの構成](https://msdn.microsoft.com/data/jj680699)」を参照してください。

1. *Logic*フォルダーで、 *AddProducts.cs*ファイルを開きます。
2. 黄色で強調表示されているように、`System.Data.Entity.Infrastructure` の `using` ステートメントを追加します。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. `AddProduct` メソッドに `catch` ブロックを追加して、`RetryLimitExceededException` が黄色で強調表示された状態で記録されるようにします。   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

`RetryLimitExceededException` 例外を追加することで、より適切なログ記録を提供したり、ユーザーがプロセスの再試行を選択できるエラーメッセージを表示したりすることができます。 `RetryLimitExceededException` 例外をキャッチすることにより、一時的なエラーだけが既に試行されており、何度も失敗しています。 返される実際の例外は、`RetryLimitExceededException` 例外でラップされます。 さらに、一般的な catch ブロックも追加しました。 `RetryLimitExceededException` 例外の詳細については、「 [Entity Framework 接続の回復性/再試行ロジック](https://msdn.microsoft.com/data/dn456835)」を参照してください。

## <a name="command-interception"></a>コマンドのインターセプト

再試行ポリシーを有効にしたので、正常に動作しているかどうかをテストするにはどうすればよいでしょうか。 特にローカルで実行している場合は、一時的なエラーを強制的に実行するのは簡単ではなく、実際の一時的なエラーを自動化された単体テストに統合することは特に困難です。 接続の回復性機能をテストするには、SQL Server に送信 Entity Framework するクエリをインターセプトし、通常は一時的な例外の種類に SQL Server 応答を置き換える方法が必要です。

また、クエリインターセプトを使用して、クラウドアプリケーションのベストプラクティスを実装することもできます。データベースサービスなど、外部サービスへのすべての呼び出しの待機時間と成功または失敗をログに記録します。

チュートリアルのこのセクションでは、ログ記録と一時的なエラーのシミュレートの両方に、Entity Framework の[*インターセプト機能*](https://msdn.microsoft.com/data/dn469464)を使用します。

### <a name="create-a-logging-interface-and-class"></a>ログインターフェイスとクラスを作成する

ログ記録のベストプラクティスは、`System.Diagnostics.Trace` またはログ記録クラスへのハードコーディングではなく、 [`interface`](https://msdn.microsoft.com/library/ms173156.aspx)を使用することです。 これにより、後で必要になったときにログ記録メカニズムを簡単に変更できるようになります。 このセクションでは、ログインターフェイスとクラスを作成して実装します。

上記の手順に基づいて、Visual Studio でウィング? **toys**サンプルアプリケーションをダウンロードして開きました。

1. **ウィングヒントの toys**プロジェクトにフォルダーを作成し、*ログ*に名前を指定します。
2. *Logging*フォルダーで、 *ILogger.cs*という名前のクラスファイルを作成し、既定のコードを次のコードに置き換えます。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   インターフェイスには、ログの相対的な重要度を示す3つのトレースレベルが用意されています。また、データベースクエリなどの外部サービスの呼び出しの待機時間情報を提供するように設計されています。 ログ記録メソッドには、例外を渡すことができるオーバーロードがあります。 これは、スタックトレースや内部例外などの例外情報が、インターフェイスを実装するクラスによって確実にログに記録されるようにするためです。これは、アプリケーション全体での各ログ記録メソッドの呼び出しで実行されることに依存するものではありません。  
  
   `TraceApi` メソッドを使用すると、SQL Database などの外部サービスに対する各呼び出しの待機時間を追跡できます。
3. *Logging*フォルダーで、 *Logger.cs*という名前のクラスファイルを作成し、既定のコードを次のコードに置き換えます。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

の実装では、`System.Diagnostics` を使用してトレースを実行します。 これは .NET の組み込み機能で、トレース情報の生成と使用が簡単になります。 `System.Diagnostics` トレースと共に使用したり、ファイルにログを書き込んだり、Windows Azure の blob ストレージに書き込んだりするために、多くの &quot;リスナー&quot; 使用できます。 詳細については、「 [Visual Studio での Windows Azure Web サイトのトラブルシューティング](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)」のいくつかのオプションとその他のリソースへのリンクを参照してください。 このチュートリアルでは、Visual Studio の **[出力]** ウィンドウのログのみを確認します。

実稼働アプリケーションでは、`System.Diagnostics`以外のトレースフレームワークの使用を検討する必要があります。また、`ILogger` インターフェイスを使用すると、別のトレースメカニズムに簡単に切り替えることができます。

### <a name="create-interceptor-classes"></a>インターセプタークラスの作成

次に、クエリをデータベースに送信するたびに Entity Framework が呼び出すクラスを作成します。1つは一時的なエラーをシミュレートし、もう1つはログ記録を行います。 これらのインターセプタークラスは、`DbCommandInterceptor` クラスから派生する必要があります。 これらのメソッドは、クエリが実行されるときに自動的に呼び出されるメソッドオーバーライドを記述します。 これらの方法では、データベースに送信されているクエリを確認またはログに記録できます。また、クエリをデータベースに渡す前にクエリを変更したり、クエリをデータベースに渡したりしなくても Entity Framework に返すことができます。

1. データベースに送信される前にすべての SQL クエリをログに記録するインターセプタークラスを作成するには、 *Logic*フォルダーに*InterceptorLogging.cs*という名前のクラスファイルを作成し、既定のコードを次のコードに置き換えます。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   クエリまたはコマンドが成功した場合、このコードは待機時間情報を含む情報ログを書き込みます。 例外の場合は、エラーログが作成されます。
2. *Adminpage*という名前のページの **[名前]** ボックスに &quot;Throw&quot; を入力したときにダミーの一時的なエラーを生成するインターセプタークラスを作成するには、 *Logic*フォルダーに*InterceptorTransientErrors.cs*という名前のクラスファイルを作成し、既定のコードを次のコードに置き換えます。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    このコードは、`ReaderExecuting` メソッドをオーバーライドするだけです。このメソッドは、複数行のデータを返すことができるクエリに対して呼び出されます。 他の種類のクエリの接続の回復性を確認する場合は、ログインターセプターと同様に `NonQueryExecuting` および `ScalarExecuting` メソッドをオーバーライドすることもできます。  
  
   後で、"管理者" としてログインし、上部のナビゲーションバーで **[管理者]** リンクを選択します。 次に、 *adminpage*ページで、&quot;Throw&quot;という名前の製品を追加します。 このコードでは、エラー番号20のダミー SQL Database 例外が作成されます。これは通常、一時的な型です。 現在 transient として認識されている他のエラー番号は、64、233、10053、10054、10060、10928、10929、40197、40501、40613ですが、これらは SQL Database の新しいバージョンで変更される可能性があります。 製品の名前は " *InterceptorTransientErrors.cs* " に変更されます。これは、このファイルのコードで実行できます。  
  
   このコードは、クエリを実行し、結果を返すのではなく、Entity Framework に例外を返します。 一時的な例外が*4*回返された後、コードは、クエリをデータベースに渡す通常の手順に戻ります。

    すべてのログが記録されるので、Entity Framework がクエリの実行を4回試行してから最後に成功することを確認できます。アプリケーションの唯一の違いは、クエリ結果を含むページのレンダリングに時間がかかることです。  
  
   Entity Framework が再試行される回数は構成可能です。このコードでは、SQL Database 実行ポリシーの既定値であるため、4回指定されています。 実行ポリシーを変更した場合は、一時的なエラーが生成される回数を指定するコードも変更します。 さらに、Entity Framework が `RetryLimitExceededException` 例外をスローするように、より多くの例外を生成するようにコードを変更することもできます。
3. *Global.asax*で、次の using ステートメントを追加します。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 次に、強調表示された行を `Application_Start` メソッドに追加します。  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

これらのコード行により、Entity Framework がデータベースにクエリを送信するときにインターセプターコードが実行されます。 一時的なエラーのシミュレーションとログ記録用に個別のインターセプタークラスを作成したので、個別に有効または無効にすることができます。   
  
 コード内の任意の場所で `DbInterception.Add` メソッドを使用して、インターセプターを追加できます。`Application_Start` メソッド内に存在する必要はありません。 `Application_Start` メソッドにインターセプターを追加していない場合は、もう1つのオプションとして、 *WingtipToysConfiguration.cs*という名前のクラスを更新または追加し、上記のコードを `WingtipToysConfiguration` クラスのコンストラクターの最後に配置します。

このコードをどこに置いても、同じインターセプターの `DbInterception.Add` を複数回実行しないように注意する必要があります。または、追加のインターセプターインスタンスを取得します。 たとえば、ログインターセプターを2回追加すると、すべての SQL クエリに対して2つのログが表示されます。

インターセプターは、登録の順序 (`DbInterception.Add` メソッドが呼び出される順序) で実行されます。 この順序は、インターセプターで行っていることによっては重要です。 たとえば、インターセプターでは、`CommandText` プロパティで取得した SQL コマンドが変更される場合があります。 SQL コマンドを変更した場合、次のインターセプターでは、元の SQL コマンドではなく、変更された SQL コマンドが取得されます。

一時的なエラーのシミュレーションコードを記述しました。これにより、UI に別の値を入力して一時的なエラーを発生させることができます。 別の方法として、特定のパラメーター値を確認せずに、一時的な例外のシーケンスを常に生成するようにインターセプターコードを記述することもできます。 その後、一時的なエラーを生成する場合にのみ、インターセプターを追加できます。 ただし、これを行う場合は、データベースの初期化が完了するまでインターセプターを追加しないでください。 つまり、一時的なエラーの生成を開始する前に、いずれかのエンティティセットに対してクエリなどのデータベース操作を少なくとも1つ実行します。 Entity Framework は、データベースの初期化中に複数のクエリを実行し、トランザクションでは実行されないため、初期化中にエラーが発生するとコンテキストが不整合な状態になる可能性があります。

## <a name="test-logging-and-connection-resiliency"></a>テストログと接続の回復性

1. Visual Studio で**F5**キーを押してアプリケーションをデバッグモードで実行し、パスワードとして "Pa $ $word" を使用して "Admin" としてログインします。
2. 上部のナビゲーションバーから **[管理者]** を選択します。
3. 適切な説明、価格、および画像ファイルを使用して、"Throw" という名前の新しい製品を入力します。
4. **[製品の追加]** ボタンをクリックします。  
   Entity Framework がクエリを何度か再試行している間に、ブラウザーが数秒間ハングしているように見えます。 最初の再試行は非常に短時間で行われます。その後、再試行のたびに待機時間が長くなります。 各再試行の前に待機するこのプロセスは、*指数バックオフ*と呼ばれます。
5. ページが読み込まれなくなるまで待ちます。
6. プロジェクトを停止し、Visual Studio の **[出力]** ウィンドウでトレース出力を確認します。 [**デバッグ** -&gt; **Windows** -&gt;**出力**] を選択すると、**出力**ウィンドウが表示されます。 ロガーによって書き込まれた他のいくつかのログを過去にスクロールすることが必要になる場合があります。  
  
   実際の SQL クエリがデータベースに送信されていることがわかります。 最初のクエリとコマンドがいくつか表示されます。開始するには、データベースのバージョンと移行履歴テーブルを確認して Entity Framework ます。   
    ![出力ウィンドウ](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   アプリケーションを停止して再起動しない限り、このテストを繰り返すことはできないことに注意してください。 アプリケーションの1回の実行で接続の回復性を複数回テストできるようにするには、`InterceptorTransientErrors` でエラーカウンターをリセットするコードを記述します。
7. 実行戦略 (再試行ポリシー) の違いを確認するには、 *Logic*フォルダー内の*WingtipToysConfiguration.cs*ファイル内の `SetExecutionStrategy` 行をコメントアウトし、 **[管理者]** ページをデバッグモードでもう一度実行して、&quot;Throw という名前の製品を再び&quot; に追加します。  
  
   今回は、最初に生成された例外でデバッガーが最初にクエリを実行しようとすると直ちに停止します。  
    ![デバッグ-詳細の表示](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. *WingtipToysConfiguration.cs*ファイル内の `SetExecutionStrategy` 行のコメントを解除します。

## <a name="summary"></a>まとめ

このチュートリアルでは、接続の回復性とコマンドインターセプトをサポートするように Web フォームサンプルアプリケーションを変更する方法を説明しました。

## <a name="next-steps"></a>次の手順

ASP.NET Web フォームで接続の回復性とコマンドインターセプトを確認した後、 [ASP.NET 4.5 の](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)ASP.NET web forms トピック「非同期メソッド」を参照してください。 このトピックでは、Visual Studio を使用して非同期の ASP.NET Web フォームアプリケーションを構築する方法の基本について説明します。
