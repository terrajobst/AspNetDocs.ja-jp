---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリで EF を使用して非同期およびストアドプロシージャを使用する'
description: このチュートリアルでは、非同期プログラミングモデルを実装する方法と、ストアドプロシージャの使用方法について説明します。
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471388"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリで EF を使用して非同期およびストアドプロシージャを使用する

前のチュートリアルでは、同期プログラミングモデルを使用してデータの読み取りと更新を行う方法を学習しました。 このチュートリアルでは、非同期プログラミングモデルを実装する方法について説明します。 非同期コードを使用すると、アプリケーションのパフォーマンスを向上させることができます。これは、サーバーリソースをより効果的に使用するためです。

このチュートリアルでは、エンティティに対する挿入、更新、および削除の各操作にストアドプロシージャを使用する方法についても説明します。

最後に、アプリケーションを初めてデプロイした後に実装したすべてのデータベースの変更と共に、Azure に再デプロイします。

以下の図は、使用するページの一部を示しています。

![[部門] ページ](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![部署の作成](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 非同期コードの詳細
> * Department コントローラーを作成する
> * ストアドプロシージャを使用する
> * Deploy to Azure (Azure へのデプロイ)

## <a name="prerequisites"></a>前提条件

* [関連データの更新](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a>非同期コードを使用する理由

Web サーバーでは、利用できるスレッド数に限りがあります。負荷が高い状況では、利用できるスレッドが全部使われる可能性があります。 その場合、スレッドが解放されるまでサーバーは新しい要求を処理できません。 同期コードの場合、たくさんのスレッドが関連付けられていても、I/O の完了を待っているため、実際には何の作業も行っていないということがあります。 非同期コードの場合、あるプロセスが I/O の完了を待っているとき、そのスレッドは解放され、サーバーによって他の要求の処理に利用できます。 その結果、非同期コードによってサーバーリソースの使用効率が向上し、サーバーは遅延なしでより多くのトラフィックを処理できるようになります。

以前のバージョンの .NET では、非同期コードの記述とテストは複雑で、エラーが発生しやすく、デバッグが困難でした。 .NET 4.5 では、非同期コードの記述、テスト、およびデバッグが非常に簡単になりました。通常、そうでない場合を除き、非同期コードを記述することをお勧めします。 非同期コードでは少量のオーバーヘッドが発生しますが、トラフィックが少ない状況では、パフォーマンスの低下はほとんどありませんが、トラフィックの量が多い場合は、パフォーマンスが大幅に向上する可能性があります。

非同期プログラミングの詳細については、「 [.net 4.5 の非同期サポートを使用してブロック呼び出しを回避する](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)」を参照してください。

## <a name="create-department-controller"></a>Department コントローラーを作成する

以前のコントローラーと同じ方法で Department コントローラーを作成します。ただし、今回は **[非同期コントローラーアクションを使用する]** チェックボックスをオンにします。

次の点は、非同期にするために `Index` メソッドの同期コードに追加されたものを示しています。

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

Entity Framework データベースクエリを非同期に実行できるようにするために、次の4つの変更が適用されました。

- メソッドは `async` キーワードでマークされます。これにより、メソッド本体の一部に対するコールバックを生成し、返された `Task<ActionResult>` オブジェクトを自動的に作成するようにコンパイラに指示します。
- 戻り値の型が `ActionResult` から `Task<ActionResult>`に変更されました。 `Task<T>` 型は、`T`型の結果で進行中の作業を表します。
- `await` キーワードが web サービス呼び出しに適用されました。 コンパイラは、このキーワードを認識すると、メソッドを2つの部分に分割します。 最初の部分は、非同期的に開始される操作で終了します。 2番目の部分は、操作の完了時に呼び出されるコールバックメソッドに配置されます。
- `ToList` 拡張メソッドの非同期バージョンが呼び出されました。

`departments.ToList` ステートメントが変更されたが、`departments = db.Departments` ステートメントが変更されたのはなぜですか。 これは、クエリまたはコマンドをデータベースに送信するステートメントのみが非同期に実行されるためです。 `departments = db.Departments` ステートメントはクエリを設定しますが、クエリは `ToList` メソッドが呼び出されるまで実行されません。 したがって、`ToList` メソッドのみが非同期に実行されます。

`Details` メソッドと `HttpGet` `Edit` および `Delete` メソッドでは、`Find` メソッドを使用して、クエリがデータベースに送信されるようにします。これは、非同期的に実行されるメソッドです。

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

`Create`、`HttpPost Edit`、および `DeleteConfirmed` メソッドでは、これはコマンドを実行する `SaveChanges` メソッド呼び出しであり、メモリ内のエンティティが変更されるだけの `db.Departments.Add(department)` などのステートメントではありません。

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

*Views\Department\Index.cshtml*を開き、テンプレートコードを次のコードに置き換えます。

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

このコードでは、Index から department にタイトルを変更し、管理者名を右に移動して、管理者の完全な名前を指定します。

[作成]、[削除]、[詳細]、および [編集] ビューで、[`InstructorID`] フィールドのキャプションを「管理者」に変更します。これは、学科名フィールドをコースビューの "Department" に変更した場合と同じです。

[作成] ビューと [編集] ビューでは、次のコードを使用します。

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

[削除] ビューと [詳細] ビューでは、次のコードを使用します。

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

アプリケーションを実行し、 **[部門]** タブをクリックします。

すべての動作は他のコントローラーと同じですが、このコントローラーでは、すべての SQL クエリが非同期に実行されます。

Entity Framework で非同期プログラミングを使用する場合は、次の点に注意する必要があります。

- 非同期コードはスレッドセーフではありません。 言い換えると、同じコンテキストインスタンスを使用して複数の操作を並行して実行しないようにしてください。
- 非同期コードのパフォーマンス上の利点を最大限に活用する場合、(ページングなどのために) ライブラリ パッケージを利用しているのであれば、それがクエリをデータベースに送信させる Entity Framework メソッドを呼び出す場合、非同期を利用する必要があります。

## <a name="use-stored-procedures"></a>ストアドプロシージャを使用する

一部の開発者や Dba は、ストアドプロシージャを使用してデータベースにアクセスしたいと考えています。 以前のバージョンの Entity Framework では、[生の SQL クエリを実行](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)することで、ストアドプロシージャを使用してデータを取得できますが、update 操作にストアドプロシージャを使用するように EF に指示することはできません。 EF 6 では、ストアドプロシージャを使用するように Code First を簡単に構成できます。

1. *DAL\SchoolContext.cs*で、強調表示されているコードを `OnModelCreating` メソッドに追加します。

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    このコードは、`Department` エンティティに対する挿入、更新、および削除操作にストアドプロシージャを使用するように Entity Framework に指示します。
2. パッケージ管理コンソールで、次のコマンドを入力します。

    `add-migration DepartmentSP`

    *\\&lt;timestamp&gt;\_DepartmentSP.cs*を開いて、Insert、Update、Delete の各ストアドプロシージャを作成するコードを `Up` メソッドに表示します。

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. パッケージ管理コンソールで、次のコマンドを入力します。

     `update-database`
4. アプリケーションをデバッグモードで実行し、 **[部門]** タブをクリックして、 **[新規作成]** をクリックします。
5. 新しい部署のデータを入力し、 **[作成]** をクリックします。

6. Visual Studio で、 **[出力]** ウィンドウのログを見て、新しい部門の行を挿入するためにストアドプロシージャが使用されたことを確認します。

     ![Department の挿入 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Code First 既定のストアドプロシージャ名を作成します。 既存のデータベースを使用している場合は、データベースで既に定義されているストアドプロシージャを使用するために、ストアドプロシージャ名のカスタマイズが必要になることがあります。 その方法の詳細については、「 [Entity Framework Code First Insert/Update/Delete ストアドプロシージャ](https://msdn.microsoft.com/data/dn468673)」を参照してください。

生成されたストアドプロシージャをカスタマイズする場合は、スキャフォールディングコードを編集して、ストアドプロシージャを作成する移行 `Up` 方法を選択できます。 これにより、移行が実行されるたびに変更が反映され、展開後に運用環境で自動的に移行が実行されるときに、運用データベースに適用されます。

以前の移行で作成された既存のストアドプロシージャを変更する場合は、[追加-移行] コマンドを使用して空の移行を生成し、 [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx)メソッドを呼び出すコードを手動で記述します。

## <a name="deploy-to-azure"></a>Deploy to Azure (Azure へのデプロイ)

このセクションでは、このシリーズの[移行とデプロイ](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)に関するチュートリアルの「 **Azure へのアプリのデプロイ**」セクションを完了している必要があります。 ローカルプロジェクトでデータベースを削除することによって解決した移行エラーが発生した場合は、このセクションをスキップします。

1. Visual Studio の**ソリューション エクスプローラー**で、プロジェクトを右クリックし、コンテキスト メニューの **[発行]** をクリックします。
2. **[発行]** をクリックします。

    Visual Studio によってアプリケーションが Azure にデプロイされ、アプリケーションが既定のブラウザーで開き、Azure で実行されます。
3. アプリケーションをテストして、動作していることを確認します。

    データベースにアクセスするページを初めて実行する場合、Entity Framework は、現在のデータモデルを使用してデータベースを最新の状態にするために必要なすべての移行 `Up` 方法を実行します。 このチュートリアルで追加した Department ページを含め、最後にデプロイした後に追加したすべての web ページを使用できるようになりました。

## <a name="get-the-code"></a>コードの入手

[完成したプロジェクトをダウンロードする](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他のリソース

その他の Entity Framework リソースへのリンクについては、 [ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)を参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 非同期コードについて学習しました
> * Department コントローラーを作成しました
> * 使用されたストアドプロシージャ
> * Azure にデプロイ済み

複数のユーザーが同時に同じエンティティを更新した場合の競合の処理方法については、次の記事に進んでください。
> [!div class="nextstepaction"]
> [同時実行の処理](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
