---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: キュー中心の作業パターン (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: 1177336b25479c06706227e5c8ff4d027cdaebb8
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456986"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>キュー中心の作業パターン (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

前述のように、複数のサービスを使用すると、アプリの有効な SLA が個々の Sla の*製品*である "複合" sla が得られる可能性があります。 たとえば、It アプリを修正するには、Web サイト、ストレージ、および SQL Database を使用します。 これらのサービスのいずれかが失敗した場合、アプリはユーザーにエラーを返します。

キャッシュは、読み取り専用コンテンツの一時的なエラーを処理するのに適した方法です。 しかし、アプリケーションが作業を行う必要がある場合はどうでしょうか。 たとえば、ユーザーが新しい Fix It タスクを送信した場合、アプリはタスクをキャッシュに配置するだけではありません。 アプリは、修正タスクを永続データストアに書き込み、処理できるようにする必要があります。

ここで、キュー中心の作業パターンが登場します。 このパターンは、web 層とバックエンドサービス間の疎結合を可能にします。

パターンのしくみを次に示します。 アプリケーションは、要求を取得すると、作業項目をキューに格納し、応答を直ちに返します。 次に、別のバックエンドプロセスがキューから作業項目を取得し、作業を行います。

キュー中心の作業パターンは、次の場合に役立ちます。

- 時間がかかる作業 (待機時間が長くなります)。
- 常に使用できるとは限りません。
- リソースを集中的に使用する作業 (高 CPU)。
- レート平準化によるメリットが得られる作業 (負荷の急激な増加による)。

## <a name="reduced-latency"></a>待機時間の短縮

キューは、時間のかかる作業を行うときに便利です。 タスクの実行に数秒以上かかる場合は、エンドユーザーをブロックするのではなく、作業項目をキューに配置します。 ユーザーに "私たちが作業しています" という指示を出し、キューリスナーを使用してバックグラウンドでタスクを処理します。

たとえば、オンライン小売業者で購入すると、web サイトはすぐに注文を確認します。 しかし、これは、既に送信されているトラックに含まれていることを意味するわけではありません。 タスクをキューに配置し、バックグラウンドでクレジット確認を行い、商品を発送するための準備を行います。

待機時間が短いシナリオでは、タスクを同期的に実行する場合と比較して、エンドツーエンドの合計時間がキューを使用していない可能性があります。 ただし、その他の利点は、その欠点を上回る可能性があります。

## <a name="increased-reliability"></a>信頼性の向上

これまでに見てきたバージョンの修正プログラムでは、web フロントエンドは SQL Database バックエンドと密接に結び付いています。 SQL database サービスが使用できない場合は、エラーが発生します。 再試行が機能しない場合 (つまり、エラーが一時的なものを超えている場合) は、エラーを表示し、後で再試行するようにユーザーに要求するだけです。

![SQL Database バックエンドで障害が発生した場合の web フロントエンドの失敗を示す図](queue-centric-work-pattern/_static/image1.png)

キューを使用すると、ユーザーが Fix It タスクを送信するときに、アプリがメッセージをキューに書き込みます。 メッセージペイロードは、タスクの[JSON](http://json.org/)表現です。 メッセージがキューに書き込まれるとすぐに、アプリはが返され、ユーザーに成功を示すメッセージが直ちに表示されます。

SQL データベースやキューリスナーなどのバックエンドサービスがオフラインになった場合でも、ユーザーは新しい Fix It タスクを送信できます。 バックエンドサービスが再び使用可能になるまで、メッセージはキューに入れられます。 その時点で、バックログがバックエンドサービスによって検出されます。

![SQL Database エラーが発生したときに web フロントエンドが引き続き機能することを示す図](queue-centric-work-pattern/_static/image2.png)

さらに、フロントエンドの回復性について心配することなく、より多くのバックエンドロジックを追加できます。 たとえば、新しい修正プログラムが割り当てられるたびに、その所有者に電子メールまたは SMS メッセージを送信することができます。 電子メールまたは SMS サービスが使用できなくなった場合は、他のすべてを処理し、電子メール/SMS メッセージを送信するための別のキューにメッセージを配置できます。

以前は、有効な SLA は Web Apps &times; ストレージ &times; SQL Database = 99.7% でした。 (「[エラーが](design-to-survive-failures.md)発生した場合の設計」を参照してください)。

キューを使用するようにアプリを変更すると、web フロントエンドは Web Apps とストレージのみに依存し、複合 SLA は99.8% になります。 (キューは Azure storage サービスの一部であるため、blob ストレージと同じ SLA に含まれています)。

99.8% よりもさらに高いパフォーマンスが必要な場合は、2つの異なるリージョンに2つのキューを作成できます。 一方をプライマリ、もう1つをセカンダリとして指定します。 プライマリキューが使用できない場合は、アプリでセカンダリキューにフェールオーバーします。 同時に使用できなくなる可能性は非常に小さいものです。

## <a name="rate-leveling-and-independent-scaling"></a>比率の平準化と独立したスケーリング

キューは、*レート*調整や*負荷平準化*と呼ばれるものにも役立ちます。

多くの場合、Web アプリはトラフィックの急激な増加の影響を受けやすくなります。 自動スケールを使用して web サーバーを自動的に追加して、増加した web トラフィックを処理できますが、負荷の急増に対応するのに十分な速さで自動スケールを処理できない場合があります。 Web サーバーが、キューにメッセージを書き込むことによって実行する必要のある作業の一部をオフロードできる場合は、より多くのトラフィックを処理できます。 バックエンドサービスは、キューからメッセージを読み取って処理することができます。 キューの深さは、受信負荷が変化するにつれて増加または縮小されます。

時間のかかる作業のほとんどがバックエンドサービスに読み込まれないため、web 層はトラフィックの急激な急増に簡単に対応できます。 また、特定の量のトラフィックを少数の web サーバーで処理できるため、コストを削減できます。

Web 層とバックエンドサービスは個別に拡張できます。 たとえば、3つの web サーバーが必要になる場合がありますが、キューメッセージを処理するサーバーは1つだけです。 また、多くのコンピューティング処理を要するタスクをバックグラウンドで実行している場合は、より多くのバックエンドサーバーが必要になることがあります。

![](queue-centric-work-pattern/_static/image3.png)

自動スケールは、web 層と同様に、バックエンドサービスでも機能します。 スケール アップするか、バックエンド VM の CPU 使用率に基づいて、キュー内のタスクを処理している VM の数をスケール ダウンします。 または、キューにあるアイテムの数に基づいて自動スケールできます。 たとえば、キュー内の項目数が10個を超えないように自動スケールに指示できます。 キューに 10 個を超える項目がある場合は、自動スケールは VM を追加します。 追いつくまで、自動スケールは、余分な VM を破棄します。

## <a name="adding-queues-to-the-fix-it-application"></a>It アプリケーションを修正するためのキューの追加

キューパターンを実装するには、Fix It アプリに2つの変更を加える必要があります。

- ユーザーが新しい Fix It タスクを送信するときに、タスクをデータベースに書き込むのではなく、キューに配置します。
- キュー内のメッセージを処理するバックエンドサービスを作成します。

キューについては、 [Azure Queue Storage サービス](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)を使用します。 別の方法として、 [Azure Service Bus](https://docs.microsoft.com/azure/service-bus/)を使用することもできます。

どのキューサービスを使用するかを決定するには、アプリがキュー内のメッセージを送受信する方法を検討します。

- 協調プロデューサーと競合コンシューマーがある場合は、Azure Queue Storage サービスの使用を検討してください。 "協調プロデューサー" とは、複数のプロセスがメッセージをキューに追加することを意味します。 "競合コンシューマー" とは、複数のプロセスがメッセージを処理するためにキューからメッセージをプルすることを意味しますが、特定のメッセージを処理できるのは1つの "コンシューマー" だけです。 1つのキューで取得できるスループットよりも高いスループットが必要な場合は、追加のキューや追加のストレージアカウントを使用します。
- [パブリッシュ/サブスクライブモデル](http://en.wikipedia.org/wiki/Publish/subscribe)が必要な場合は、Azure Service Bus キューを使用することを検討してください。

Fix It アプリは、協調するプロデューサーと競合コンシューマーモデルに適合しています。

もう1つの考慮事項は、アプリケーションの可用性です。 Queue Storage サービスは、blob Storage に使用しているものと同じサービスの一部であるため、SLA には影響しません。 Azure Service Bus は、独自の SLA を持つ独立したサービスです。 Service Bus キューを使用した場合は、追加の SLA の割合を考慮する必要があります。また、複合 SLA は低くなります。 Queue サービスを選択するときは、アプリケーションの可用性に与える影響について理解しておいてください。 詳細については、「 [resources](#resources) 」セクションを参照してください。

## <a name="creating-queue-messages"></a>キューメッセージの作成

このタスクをキューに配置するために、web フロントエンドは次の手順を実行します。

1. [Cloudqueueclient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx)インスタンスを作成します。 `CloudQueueClient` インスタンスは、Queue サービスに対して要求を実行するために使用されます。
2. キューを作成します (まだ存在しない場合)。
3. Fix It タスクをシリアル化します。
4. メッセージをキューに配置するには、 [Cloudqueue. AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx)を呼び出します。

この作業は、新しい `FixItQueueManager` クラスのコンストラクターと `SendMessageAsync` メソッドで行います。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

ここでは、 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json)ライブラリを使用して、FIXIT を Json 形式にシリアル化しています。 任意のシリアル化方法を使用できます。 JSON には人間が判読できるという利点がありますが、XML よりも詳細が少なくなっています。

実稼働品質のコードは、エラー処理ロジックを追加し、データベースが使用できなくなった場合は一時停止し、回復をより明確に処理し、アプリケーションの起動時にキューを作成し、"[有害な" メッセージ](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)を管理します。 (有害メッセージとは、何らかの理由で処理できないメッセージのことです。 有害なメッセージがキューに置かれないようにする必要があります。ワーカーロールは、そのメッセージを継続的に処理したり、失敗したり、再試行したり、失敗したりします)。

フロントエンド MVC アプリケーションでは、新しいタスクを作成するコードを更新する必要があります。 タスクをリポジトリに配置するのではなく、上に示した `SendMessageAsync` メソッドを呼び出します。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>キューメッセージの処理

キュー内のメッセージを処理するには、バックエンドサービスを作成します。 バックエンドサービスは、次の手順を実行する無限ループを実行します。

1. キューから次のメッセージを取得します。
2. メッセージを修正するタスクに逆シリアル化します。
3. 修正プログラムをデータベースに書き込みます。

バックエンドサービスをホストするために、*ワーカーロール*を含む Azure クラウドサービスを作成します。 ワーカー ロールは、バックエンド処理を実行できる 1 つまたは複数の VM で構成されます。 これらの VM で実行されるコードでは、利用可能になったキューからメッセージをプルします。 各メッセージについて、JSON ペイロードを逆シリアル化して、web 層で前に使用したのと同じリポジトリを使用して、Fix It Task エンティティのインスタンスをデータベースに書き込みます。

次の手順は、標準の web プロジェクトを持つソリューションにワーカーロールプロジェクトを追加する方法を示しています。 これらの手順は、ダウンロード可能な修正プログラムのプロジェクトで既に実行されています。

まず、Visual Studio ソリューションにクラウドサービスプロジェクトを追加します。 ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。 左側のウィンドウで、 **[ビジュアルC# ]** を展開し、 **[クラウド]** を選択します。

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

**[新しい Azure クラウドサービス]** ダイアログで、左側のウィンドウの **[ビジュアルC# ]** ノードを展開します。 **[Worker ロール]** を選択し、右矢印アイコンをクリックします。

![](queue-centric-work-pattern/_static/image6.png)

( *Web ロール*を追加することもできます。 Azure の Web サイトで実行するのではなく、同じクラウドサービスでフロントエンドを修正することができました。 これには、フロントエンドとバックエンド間の接続を簡単に調整できるという利点があります。 ただし、このデモを簡潔にするために、フロントエンドを Azure App Service Web アプリに保持し、クラウドサービスでバックエンドのみを実行しています)。

既定の名前は worker ロールに割り当てられます。 名前を変更するには、右側のウィンドウで worker ロールの上にマウスポインターを置き、鉛筆アイコンをクリックします。

![](queue-centric-work-pattern/_static/image7.png)

**[OK]** をクリックしてダイアログを完了します。 これにより、2つのプロジェクトが Visual Studio ソリューションに追加されます。

- 構成情報を含む、クラウドサービスを定義する Azure プロジェクト。
- ワーカーロールを定義するワーカーロールプロジェクト。

![](queue-centric-work-pattern/_static/image8.png)

詳細については、「 [Visual Studio を使用した Azure プロジェクトの作成](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)」を参照してください。

Worker ロール内では、前に見た `FixItQueueManager` クラスの `ProcessMessageAsync` メソッドを呼び出すことによってメッセージをポーリングします。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync` メソッドは、待機中のメッセージがあるかどうかを確認します。 存在する場合は、メッセージを `FixItTask` エンティティに逆シリアル化し、エンティティをデータベースに保存します。 キューが空になるまでループします。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

キューメッセージをポーリングすると、トランザクションの料金が小さいので、処理を待機しているメッセージがない場合、ワーカーロールの `RunAsync` メソッドは、`Task.Delay(1000)`を呼び出して、もう一度ポーリングする前に秒待機します。

Web プロジェクトで非同期コードを追加すると、IIS が制限されたスレッドプールを管理するため、パフォーマンスが自動的に向上します。 これは、ワーカーロールプロジェクトの場合には当てはまりません。 ワーカーロールのスケーラビリティを向上させるには、マルチスレッドコードを記述するか、非同期コードを使用して[並列プログラミング](https://msdn.microsoft.com/library/ff963553.aspx)を実装します。 このサンプルは並列プログラミングを実装していませんが、並列プログラミングを実装できるようにコードを非同期にする方法を示しています。

## <a name="summary"></a>要約

この章では、キュー中心の作業パターンを実装することによって、アプリケーションの応答性、信頼性、スケーラビリティを向上させる方法について説明しました。

これは、この電子書籍に記載されている13個のパターンの最後のパターンですが、成功したクラウドアプリの構築に役立つパターンとプラクティスは他にも多数あります。 [最後の章](more-patterns-and-guidance.md)では、これらの13のパターンで説明されていないトピックに関するリソースへのリンクを示します。

<a id="resources"></a>
## <a name="resources"></a>リソース

キューの詳細については、次のリソースを参照してください。

ドキュメント:

- [Microsoft Azure Storage キューパート 1: はじめに](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-storage-queues-part-1-getting-started/)。 Roman Schacherl の記事。
- [バックグラウンドタスクの実行](https://msdn.microsoft.com/library/ff803365.aspx)、クラウドへのアプリケーションの移動の第5章[、3エディション (](https://msdn.microsoft.com/library/ff728592.aspx) Microsoft のパターンとプラクティスを参照)。 (特に、「 [Azure Storage キューの使用」](https://msdn.microsoft.com/library/ff803365.aspx#sec7)を参照してください)。
- [Azure 上のキューベースのメッセージングソリューションのスケーラビリティとコスト効果を最大化するためのベストプラクティス](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx)です。 Valery のホワイトペーパー。
- [Azure キューと Service Bus キューを比較](https://msdn.microsoft.com/magazine/jj159884.aspx)します。 MSDN マガジンの記事では、使用するキューサービスを選択する際に役立つ追加情報を提供しています。 この記事では、Service Bus が認証用に ACS に依存していることを示しています。つまり、ACS を使用できない場合、SB キューは使用できなくなります。 ただし、記事が書かれたため、SB は ACS の代わりに[SAS トークン](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx)を使用できるように変更されました。
- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 「非同期メッセージングの概要」、「パイプとフィルターパターン」、「補正トランザクションパターン」、「競合コンシューマーパターン」、「CQRS パターン」を参照してください。
- [CQRS の旅](https://msdn.microsoft.com/library/jj554200)。 Microsoft のパターンとプラクティスによる CQRS に関する電子書籍。

ビデオ:

- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9部構成のビデオシリーズ。 高度な概念とアーキテクチャの原則を、非常にアクセスしやすく興味深い方法で紹介します。実際の顧客との Microsoft カスタマーアドバイザリチーム (CAT) エクスペリエンスによってストーリーが描画されます。 Azure Storage サービスとキューの概要については、35:13 以降のエピソード5を参照してください。

> [!div class="step-by-step"]
> [前へ](distributed-caching.md)
> [次へ](more-patterns-and-guidance.md)
