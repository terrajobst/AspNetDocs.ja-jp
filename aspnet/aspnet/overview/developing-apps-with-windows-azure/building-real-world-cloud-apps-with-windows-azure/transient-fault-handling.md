---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: 一時的なエラー処理 (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: e798cb83cfb97db63fef6dc38c8f62804461d01b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456856"
---
# <a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>一時的なエラー処理 (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

実際のクラウドアプリを設計する場合は、一時的なサービス中断を処理する方法について検討する必要があります。 クラウドアプリでは、ネットワーク接続と外部サービスに依存しているため、この問題は一意です。 通常は自己復旧を行うことはほとんどありません。また、それらをインテリジェントに処理する準備ができていない場合は、顧客のエクスペリエンスが悪くなります。

## <a name="causes-of-transient-failures"></a>一時的なエラーの原因

クラウド環境では、失敗したデータベース接続と削除されたデータベース接続が定期的に発生していることがわかります。 これは、web サーバーとデータベースサーバーが直接物理的に接続しているオンプレミス環境と比較して、ロードバランサーが多くなるためです。 また、マルチテナントサービスに依存している場合は、サービスの呼び出しが遅いか、タイムアウトになることがあります。これは、サービスを使用する他のユーザーが頻繁にヒットするためです。 その他のケースとしては、サービスに頻繁にアクセスしているユーザーが、サービスによって意図的にスロットルされ、サービスの他のテナントに悪影響を与えないようにすることが考えられます。

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>スマートな再試行/バックオフロジックを使用して、一時的な障害の影響を軽減する

例外をスローして、使用できない、またはエラーページを顧客に表示するのではなく、通常は一時的なエラーを認識し、エラーの原因となった操作を自動的に再試行します。これは、それが成功するまでの時間です。 ほとんどの場合、2回目の試行では操作が成功し、問題が発生したことをユーザーが認識していない状態でエラーから復旧します。

スマートな再試行ロジックを実装するには、いくつかの方法があります。

- Microsoft Patterns &amp; プラクティスグループには、[一時的なエラー処理アプリケーションブロック](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx)があります。これは、(Entity Framework ではなく) SQL Database アクセスに ADO.NET を使用している場合にすべての処理を実行します。 再試行のポリシーを設定するのは、クエリまたはコマンドを再試行する回数と、試行間の待機時間を設定し、*使用している*ブロックで SQL コードをラップするだけです。

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    また、TFH は[Azure In-Role Cache](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx)と[Service Bus](https://azure.microsoft.com/services/service-bus/)もサポートしています。
- Entity Framework を使用する場合、通常は SQL 接続を直接操作しないので、このパターンおよびプラクティスパッケージを使用することはできませんが、Entity Framework 6 では、この種の再試行ロジックをフレームワークに直接作成します。 再試行戦略を指定するのと同様の方法で、EF はデータベースにアクセスするたびにその方法を使用します。

    この機能を Fix It アプリで使用するには、 *Dbconfiguration*から派生したクラスを追加し、再試行ロジックを有効にするだけです。

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    通常は一時的なエラーとして示されている例外 SQL Database については、表示されるコードは EF に対して最大3回の操作を再試行するように指示します。再試行の間隔は指数バックオフで、最大遅延時間は5秒です。 指数バックオフとは、再試行が再試行されるたびに、もう一度試す前に長時間待機することを意味します。 行の試行が3回失敗した場合、例外がスローされます。 サーキットブレーカーに関する次のセクションでは、指数バックオフと再試行回数が制限される理由について説明します。

    Azure Storage サービスを使用しているときに、Blob 用の修正プログラムと同様の問題が発生する可能性があります。また、.NET ストレージクライアント API は同じ種類のロジックを既に実装しています。 再試行ポリシーを指定するだけでかまいません。既定の設定に満足できる場合は、それを行う必要もありません。

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>サーキットブレーカー

何回も再試行しない場合は、次のようないくつかの理由があります。

- 失敗した要求を永続的に再試行するユーザーが多すぎると、他のユーザーのエクスペリエンスが低下する可能性があります。 数百万のユーザーがすべての再試行要求を繰り返し行っている場合、IIS ディスパッチキューを使用して、アプリが要求を処理できないようにすることができます。
- サービスの障害によってすべてのユーザーが再試行している場合は、サービスが復旧を開始するときに大量の要求をキューに入れている可能性があります。
- 調整によってエラーが発生した場合、サービスが調整に使用する時間帯があると、続行の再試行によってそのウィンドウが移動され、調整が続行される可能性があります。
- Web ページが表示されるのを待機しているユーザーがいる可能性があります。 ユーザーの待機時間が長すぎると、後でもう一度試してみるのが困難になる可能性があります。

指数バックオフは、サービスがアプリケーションから取得できる再試行の頻度を制限することで、これらの問題の一部に対処します。 ただし、*サーキットブレーカー*も必要です。これは、特定の再試行しきい値でアプリの再試行を停止し、次のような何らかのアクションを実行することを意味します。

- カスタムフォールバック。 Reuters から株価を得られない場合は、ブルームバーグから入手できるかもしれません。または、データベースからデータを取得できない場合は、キャッシュからデータを取得できます。
- サイレントモードで失敗します。 サービスから必要なものが、アプリのすべてまたは何でもない場合は、データを取得できない場合は null を返します。 修正プログラムのタスクを表示していて Blob service が応答していない場合は、イメージを使用せずにタスクの詳細を表示できます。
- フェールファースト。 他のユーザーがサービスを中断したり、調整期間を延長したりする可能性がある再試行要求でサービスがいっぱいになるのを防ぐために、ユーザーにエラーを送信します。 "後でもう一度お試しください" というメッセージが表示できます。

1つのサイズに適合する再試行ポリシーはありません。 ユーザーが応答を待機している同期 web アプリの場合よりも、再試行回数を増やして非同期のバックグラウンドワーカープロセスで待機することができます。 リレーショナルデータベースサービスの再試行の間隔は、キャッシュサービスの場合よりも長くなる可能性があります。 ここでは、数値がどのように変化するかを理解できるように、推奨される再試行ポリシーの例をいくつか紹介します。 ("Fast First" は、最初の再試行の前に遅延がないことを意味します。

![再試行ポリシーの例](transient-fault-handling/_static/image1.png)

SQL Database 再試行ポリシーのガイダンスについては、「SQL Database の一時的なエラー[と接続エラーのトラブルシューティング](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)」を参照してください。

## <a name="summary"></a>要約

再試行/バックオフ戦略を使用すると、一時的なエラーをお客様のほとんどの時間に非表示にすることができます。また、Microsoft は、ADO.NET、Entity Framework、Azure Storage サービスのいずれを使用しているかにかかわらず、作業を最小限に抑えるために使用できるフレームワークを提供します。

次の[章](distributed-caching.md)では、分散キャッシュを使用してパフォーマンスと信頼性を向上させる方法について説明します。

## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

ドキュメント

- [Azure Cloud Services で大規模なサービスを設計するためのベストプラクティス](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 マーク Simm と Michael Thomassy によるホワイトペーパー。 フェイルセーフシリーズに似ていますが、さらに詳細な方法について説明します。 「テレメトリと診断」セクションを参照してください。
- [フェイルセーフ: 回復力のあるクラウドアーキテクチャに関するガイダンス](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 ホワイトペーパー (Marc Mercuri、Ulrich Homann、Andrew Townhill)。 フェールセーフビデオシリーズの Web ページバージョン。
- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 「再試行パターン、スケジューラエージェントのスーパーバイザーパターン」を参照してください。
- [Azure SQL Database のフォールトトレランス](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)。 Tony Petrossian によるブログ投稿。
- [Entity Framework 接続の回復性/再試行ロジック](https://msdn.microsoft.com/data/dn456835)。 Entity Framework 6 の一時的なエラー処理機能を使用およびカスタマイズする方法について説明します。
- [ASP.NET MVC アプリケーションでの Entity Framework を使用した接続の回復性とコマンドのインターセプト](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 9部構成のチュートリアルシリーズの第4部では、SQL Database の EF 6 の接続復元機能を設定する方法について説明します。

Videos

- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9パートシリーズ。 高度な概念とアーキテクチャの原則を、非常にアクセスしやすく興味深い方法で紹介します。実際の顧客との Microsoft カスタマーアドバイザリチーム (CAT) エクスペリエンスによってストーリーが描画されます。 40:55 で始まるエピソード3のサーキットブレーカーについて説明します。
- [大規模な構築: Azure のお客様から学んだ教訓-パート II](https://channel9.msdn.com/Events/Build/2012/3-030)。 Simm をマークすると、エラーの設計、一時的なエラー処理、すべてのインストルメント化について話します。

コード サンプル

- [Azure のクラウドサービスの基礎](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 [エンタープライズライブラリの一時的なエラー処理ブロック](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)(tfh) を使用する方法を示す Microsoft Azure カスタマーアドバイザリチームによって作成されたサンプルアプリケーション。 詳細については、「[Cloud Service Fundamentals Data Access Layer – Transient Fault Handling (クラウド サービスの基本データ アクセス層 – 一時的エラー処理)](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)」を参照してください。 ADO.NET を直接使用して (Entity Framework を使用せずに) データベースにアクセスする場合は、TFH を使用することをお勧めします。

> [!div class="step-by-step"]
> [前へ](monitoring-and-telemetry.md)
> [次へ](distributed-caching.md)
