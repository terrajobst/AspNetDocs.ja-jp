---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリの EF で接続の回復性とコマンドインターセプトを使用する'
author: tdykstra
description: このチュートリアルでは、接続の回復性とコマンドインターセプトの使用方法について説明します。 Entity Framework 6 の2つの重要な機能です。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471400"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリの Entity Framework で接続の回復性とコマンドインターセプトを使用する

これまでは、アプリケーションは開発用コンピューターの IIS Express でローカルに実行されていました。 実際のアプリケーションを他のユーザーがインターネット経由で使用できるようにするには、それを web ホスティングプロバイダーに展開する必要があり、データベースをデータベースサーバーに配置する必要があります。

このチュートリアルでは、接続の回復性とコマンドインターセプトの使用方法について説明します。 これは Entity Framework 6 の2つの重要な機能であり、クラウド環境にデプロイするときに特に便利です。接続の回復性 (一時的なエラーの自動再試行) とコマンドインターセプト (データベースに送信されたすべての SQL クエリをキャッチする)をログに記録するか変更します)。

この接続の回復性とコマンドインターセプトのチュートリアルは省略可能です。 このチュートリアルをスキップする場合は、次のチュートリアルでいくつかの細かい調整を行う必要があります。

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 接続の回復性を有効にする
> * コマンドインターセプトを有効にする
> * 新しい構成をテストする

## <a name="prerequisites"></a>前提条件

* [並べ替え、フィルター処理、ページング](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>接続の回復性を有効にする

アプリケーションを Windows Azure にデプロイする場合は、データベースをクラウドデータベースサービスである Windows Azure SQL Database に配置します。 通常、一時的な接続エラーは、web サーバーとデータベースサーバーが同じデータセンターに直接接続されている場合よりも、クラウドデータベースサービスに接続すると、より頻繁に発生します。 クラウド web サーバーとクラウドデータベースサービスが同じデータセンターでホストされている場合でも、ロードバランサーなど、問題が発生する可能性のあるネットワーク接続が増加します。

また、クラウドサービスは通常、他のユーザーによって共有されます。これは、そのサービスの応答性が影響を受ける可能性があることを意味します。 また、データベースへのアクセスが制限される可能性があります。 調整とは、データベースサービスが、サービスレベルアグリーメント (SLA) で許可されているよりも頻繁にアクセスしようとした場合に、例外をスローすることを意味します。

クラウドサービスにアクセスするときの接続に関する多くの問題は、一時的なものです。つまり、短時間に解決されます。 そのため、データベース操作を試行して、通常は一時的なエラーの種類を取得した場合は、しばらく待ってから操作を再試行することができ、操作は成功する可能性があります。 一時的なエラーを自動的に再試行することによって、ユーザーにとってより良いエクスペリエンスを提供できます。そのほとんどは、顧客に対して非表示になります。 Entity Framework 6 の接続の復元機能では、失敗した SQL クエリを再試行するプロセスを自動化できます。

接続の回復性機能は、特定のデータベースサービスに対して適切に構成されている必要があります。

- どの例外が一時的なものである可能性があるかを把握しておく必要があります。 たとえば、プログラムのバグによるエラーではなく、ネットワーク接続が一時的に失われたことによって発生したエラーを再試行します。
- 失敗した操作が再試行されるまでの間、適切な時間を待機する必要があります。 バッチ処理の再試行の間隔は、ユーザーが応答を待機しているオンライン web ページの場合よりも長くなる可能性があります。
- この場合は、適切な回数の再試行を行う必要があります。 バッチ処理では、オンラインアプリケーションの場合と同じように再試行することができます。

これらの設定は、Entity Framework プロバイダーでサポートされている任意のデータベース環境に対して手動で構成できますが、通常は Windows Azure SQL Database を使用するオンラインアプリケーションに対して適切に機能する既定値は、既に構成されています。これらは、Contoso 大学アプリケーション用に実装する設定です。

接続の回復性を有効にするために必要なのは、 [Dbconfiguration](https://msdn.microsoft.com/data/jj680699.aspx)クラスから派生したクラスをアセンブリに作成することだけです。このクラスでは、EF では、*再試行ポリシー*のもう1つの用語として SQL Database*実行方法*を設定します。

1. DAL フォルダーで、 *SchoolConfiguration.cs*という名前のクラスファイルを追加します。
2. テンプレート コードを次のコードに置き換えます。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    Entity Framework は、`DbConfiguration`から派生したクラスで検出されたコードを自動的に実行します。 `DbConfiguration` クラスを使用する*と、web.config ファイルで*実行するコードで構成タスクを実行できます。 詳細については、「 [Entityframework コードベースの構成](https://msdn.microsoft.com/data/jj680699)」を参照してください。
3. *StudentController.cs*で、`System.Data.Entity.Infrastructure`の `using` ステートメントを追加します。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. `DataException` 例外をキャッチするすべての `catch` ブロックを、`RetryLimitExceededException` 例外をキャッチするように変更します。 次に例を示します。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    `DataException` を使用して、"もう一度やり直してください" というメッセージを表示するために、一時的なエラーを特定しようとしています。 ただし、再試行ポリシーを有効にしたので、一時的なエラーだけが既に試行されており、何度も失敗したため、返された実際の例外は `RetryLimitExceededException` 例外でラップされます。

詳細については、「 [Entity Framework 接続の回復性/再試行ロジック](https://msdn.microsoft.com/data/dn456835)」を参照してください。

## <a name="enable-command-interception"></a>コマンドインターセプトを有効にする

再試行ポリシーを有効にしたので、正常に動作しているかどうかをテストするにはどうすればよいでしょうか。 特にローカルで実行している場合は、一時的なエラーを強制的に実行するのは簡単ではなく、実際の一時的なエラーを自動化された単体テストに統合することは特に困難です。 接続の回復性機能をテストするには、SQL Server に送信 Entity Framework するクエリをインターセプトし、通常は一時的な例外の種類に SQL Server 応答を置き換える方法が必要です。

また、クエリインターセプトを使用して、クラウドアプリケーションのベストプラクティスを実装することもできます。データベースサービスなど[、外部サービスへのすべての呼び出しの待機時間と成功または失敗をログに記録](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)します。 EF6 にはログ記録を容易にする[専用のログ API](https://msdn.microsoft.com/data/dn469464)が用意されていますが、チュートリアルのこのセクションでは、ログ記録と一時的なエラーのシミュレートの両方で、Entity Framework の[傍受機能](https://msdn.microsoft.com/data/dn469464)を直接使用する方法について学習します。

### <a name="create-a-logging-interface-and-class"></a>ログインターフェイスとクラスを作成する

[ログ記録のベストプラクティス](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)としては、トレースまたはログ記録クラスのハードコーディングではなく、インターフェイスを使用します。 これにより、後で必要になったときにログ記録メカニズムを簡単に変更できるようになります。 このセクションでは、ログインターフェイスとそれを実装するクラスを作成します。/p >

1. プロジェクトにフォルダーを作成し、*ログ記録*という名前を指定します。
2. [ *Logging* ] フォルダーで、 *ILogger.cs*という名前のクラスファイルを作成し、テンプレートコードを次のコードに置き換えます。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    インターフェイスには、ログの相対的な重要度を示す3つのトレースレベルが用意されています。また、データベースクエリなどの外部サービスの呼び出しの待機時間情報を提供するように設計されています。 ログ記録メソッドには、例外を渡すことができるオーバーロードがあります。 これは、スタックトレースや内部例外などの例外情報が、インターフェイスを実装するクラスによって確実にログに記録されるようにするためです。これは、アプリケーション全体での各ログ記録メソッドの呼び出しで実行されることに依存するものではありません。

    TraceApi メソッドを使用すると、SQL Database などの外部サービスに対する各呼び出しの待機時間を追跡できます。
3. [ *Logging* ] フォルダーで、 *Logger.cs*という名前のクラスファイルを作成し、テンプレートコードを次のコードに置き換えます。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    の実装では、トレースを実行するためにシステム診断を使用します。 これは .NET の組み込み機能で、トレース情報の生成と使用が簡単になります。 システム診断トレースでは、ログをファイルに書き込む場合や、Azure の blob ストレージに書き込む場合など、多くの "リスナー" を使用できます。 詳細については、「 [Visual Studio での Azure websites のトラブルシューティング](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)」のオプションとその他のリソースへのリンクを参照してください。 このチュートリアルでは、Visual Studio の **[出力]** ウィンドウのログのみを確認します。

    実稼働アプリケーションでは、ILogger 以外のトレースパッケージを使用することを検討できます。また、そのような場合は、別のトレースメカニズムに簡単に切り替えることができます。

### <a name="create-interceptor-classes"></a>インターセプタークラスの作成

次に、クエリをデータベースに送信するたびに Entity Framework が呼び出すクラスを作成します。1つは一時的なエラーをシミュレートし、もう1つはログ記録を行います。 これらのインターセプタークラスは、`DbCommandInterceptor` クラスから派生する必要があります。 ここでは、クエリが実行されるときに自動的に呼び出されるメソッドオーバーライドを記述します。 これらの方法では、データベースに送信されているクエリを確認またはログに記録できます。また、クエリをデータベースに渡す前にクエリを変更したり、クエリをデータベースに渡したりしなくても Entity Framework に返すことができます。

1. データベースに送信されるすべての SQL クエリをログに記録するインターセプタークラスを作成するには、 *SchoolInterceptorLogging.cs*という名前のクラスファイルを*DAL*フォルダーに作成し、テンプレートコードを次のコードに置き換えます。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    クエリまたはコマンドが成功した場合、このコードは待機時間情報を含む情報ログを書き込みます。 例外の場合は、エラーログが作成されます。
2. **検索**ボックスに「Throw」と入力したときにダミーの一時的なエラーを生成するインターセプタークラスを作成するには、 *SchoolInterceptorTransientErrors.cs*という名前のクラスファイルを*DAL*フォルダーに作成し、テンプレートコードを次のコードに置き換えます。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    このコードは、`ReaderExecuting` メソッドをオーバーライドするだけです。このメソッドは、複数行のデータを返すことができるクエリに対して呼び出されます。 他の種類のクエリの接続の回復性を確認する場合は、ログインターセプターと同様に `NonQueryExecuting` および `ScalarExecuting` メソッドをオーバーライドすることもできます。

    学生ページを実行し、検索文字列として「Throw」と入力すると、このコードでは、通常は一時的なものであることが知られているエラー番号20のダミー SQL Database 例外が作成されます。 現在 transient として認識されている他のエラー番号は、64、233、10053、10054、10060、10928、10929、40197、40501、40613ですが、これらは SQL Database の新しいバージョンで変更される可能性があります。

    このコードは、クエリを実行してクエリ結果を返すのではなく、Entity Framework に例外を返します。 一時的な例外が4回返された後、コードは、クエリをデータベースに渡す通常の手順に戻ります。

    すべてのログが記録されるので、Entity Framework がクエリの実行を4回試行してから最後に成功することを確認できます。アプリケーションの唯一の違いは、クエリ結果を含むページのレンダリングに時間がかかることです。

    Entity Framework が再試行される回数は構成可能です。このコードでは、SQL Database 実行ポリシーの既定値であるため、4回指定されています。 実行ポリシーを変更した場合は、一時的なエラーが生成される回数を指定するコードも変更します。 さらに、Entity Framework が `RetryLimitExceededException` 例外をスローするように、より多くの例外を生成するようにコードを変更することもできます。

    検索ボックスに入力した値は `command.Parameters[0]` と `command.Parameters[1]` になります (1 つは名に使用され、姓は1になります)。 値 "% Throw%" が検出されると、これらのパラメーターの "Throw" が "a" に置き換えられるため、一部の学生が検索されて返されます。

    これは、アプリケーション UI への入力の変更に基づいて、接続の回復性をテストするための便利な方法です。 また、後の「 *Dbinterception. Add*メソッドに関するコメント」で説明されているように、すべてのクエリまたは更新の一時的なエラーを生成するコードを記述することもできます。
3. *Global.asax*で、次の `using` ステートメントを追加します。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. 強調表示された行を `Application_Start` メソッドに追加します。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    これらのコード行により、Entity Framework がデータベースにクエリを送信するときにインターセプターコードが実行されます。 一時的なエラーのシミュレーションとログ記録用に個別のインターセプタークラスを作成したので、個別に有効または無効にすることができます。

    コード内の任意の場所で `DbInterception.Add` メソッドを使用して、インターセプターを追加できます。`Application_Start` メソッド内に存在する必要はありません。 別の方法として、前の手順で作成した DbConfiguration クラスにこのコードを配置して、実行ポリシーを構成することもできます。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    このコードをどこに置いても、同じインターセプターの `DbInterception.Add` を複数回実行しないように注意する必要があります。または、追加のインターセプターインスタンスを取得します。 たとえば、ログインターセプターを2回追加すると、すべての SQL クエリに対して2つのログが表示されます。

    インターセプターは、登録の順序 (`DbInterception.Add` メソッドが呼び出される順序) で実行されます。 この順序は、インターセプターで行っていることによっては重要です。 たとえば、インターセプターでは、`CommandText` プロパティで取得した SQL コマンドが変更される場合があります。 SQL コマンドを変更した場合、次のインターセプターでは、元の SQL コマンドではなく、変更された SQL コマンドが取得されます。

    一時的なエラーのシミュレーションコードを記述しました。これにより、UI に別の値を入力して一時的なエラーを発生させることができます。 別の方法として、特定のパラメーター値を確認せずに、一時的な例外のシーケンスを常に生成するようにインターセプターコードを記述することもできます。 その後、一時的なエラーを生成する場合にのみ、インターセプターを追加できます。 ただし、これを行う場合は、データベースの初期化が完了するまでインターセプターを追加しないでください。 つまり、一時的なエラーの生成を開始する前に、いずれかのエンティティセットに対してクエリなどのデータベース操作を少なくとも1つ実行します。 Entity Framework は、データベースの初期化中に複数のクエリを実行し、トランザクションでは実行されないため、初期化中にエラーが発生するとコンテキストが不整合な状態になる可能性があります。

## <a name="test-the-new-configuration"></a>新しい構成をテストする

1. **F5**キーを押してデバッグモードでアプリケーションを実行し、 **[Students]** タブをクリックします。
2. Visual Studio の **[出力]** ウィンドウでトレース出力を確認します。 ロガーによって書き込まれたログを取得するために、いくつかの JavaScript エラーを前にスクロールすることが必要になる場合があります。

    実際の SQL クエリがデータベースに送信されていることがわかります。 最初のクエリと Entity Framework コマンドがいくつか表示されます。開始するには、データベースのバージョンと移行の履歴テーブルを確認します (次のチュートリアルでは、移行について学習します)。 また、ページングのクエリが表示され、学生の数がわかります。最後に、学生データを取得するクエリが表示されます。

    ![通常のクエリのログ記録](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. **[Students]** ページで、検索文字列として「Throw」と入力し、 **[検索]** をクリックします。

    ![検索文字列をスローする](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Entity Framework がクエリを何度か再試行している間に、ブラウザーが数秒間ハングしているように見えます。 最初の再試行は非常に短時間で行われます。その後、再試行のたびに、待機時間が長くなります。 各再試行の前に待機するこのプロセスは、*指数バックオフ*と呼ばれます。

    このページが表示されると、名前に "a" を持つ学生が表示され、[出力] ウィンドウを見ると、同じクエリが5回試行されたことがわかります。最初の4回は一時的な例外を返します。 一時的なエラーが発生するたびに、`SchoolInterceptorTransientErrors` クラス (「コマンドの一時エラーを返す」) で一時的なエラーを生成したときに記述したログが表示され、`SchoolInterceptorLogging` が例外を取得したときにログが書き込まれます。

    ![再試行を示すログ出力](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    検索文字列を入力したため、学生データを返すクエリがパラメーター化されます。

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    パラメーターの値はログに記録されませんが、これを行うことはできます。 パラメーター値を確認する場合は、インターセプターメソッドで取得した `DbCommand` オブジェクトの `Parameters` プロパティからパラメーター値を取得するためのログ記録コードを記述できます。

    アプリケーションを停止して再起動しない限り、このテストを繰り返すことはできないことに注意してください。 アプリケーションの1回の実行で接続の回復性を複数回テストできるようにするには、`SchoolInterceptorTransientErrors`でエラーカウンターをリセットするコードを記述します。
4. 実行戦略 (再試行ポリシー) の違いを確認するには、 *SchoolConfiguration.cs*の `SetExecutionStrategy` 行をコメントアウトし、[Students] ページをデバッグモードでもう一度実行して、もう一度 "Throw" を検索します。

    今回は、最初に生成された例外でデバッガーが最初にクエリを実行しようとすると直ちに停止します。

    ![ダミーの例外](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. *SchoolConfiguration.cs*で*setexecutionstrategy*行のコメントを解除します。

## <a name="get-the-code"></a>コードの入手

[完成したプロジェクトのダウンロード](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他のリソース

その他の Entity Framework リソースへのリンクについては[、「ASP.NET Data Access-推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 接続の回復性を有効にする
> * 有効なコマンドインターセプト
> * 新しい構成をテストした

次の記事に進み、Code First 移行と Azure デプロイについて学習してください。
> [!div class="nextstepaction"]
> [移行と Azure のデプロイの Code First](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
