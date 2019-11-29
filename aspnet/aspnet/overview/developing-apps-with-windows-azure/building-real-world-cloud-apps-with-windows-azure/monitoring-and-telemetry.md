---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 監視とテレメトリ (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: 44941c9fd0dcd3223604fc4a4f2836f587578acb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585605"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>監視とテレメトリ (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson]((https://twitter.com/RickAndMSFT))、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

多くのユーザーは、アプリケーションがダウンしたことを知らせるために、顧客に依存しています。 これは、特にクラウドではなく、どこでもベストプラクティスではありません。 クイック通知の保証はありません。通知を受け取ると、多くの場合、何が起こったかについてのデータが最小限または誤解されます。 優れたテレメトリとログ記録システムにより、アプリで何が起こっているかを認識できます。問題が発生した場合は、すぐに見つけて、トラブルシューティングに役立つ情報を得ることができます。

## <a name="buy-or-rent-a-telemetry-solution"></a>テレメトリソリューションを購入またはレンタルする

> [!NOTE]
> この記事は[Application Insights](/azure/application-insights/app-insights-overview)がリリースされる前に作成されました。 Application Insights は、Azure でテレメトリソリューションを使用する場合に推奨される方法です。 詳細については[、ASP.NET web サイトの「セットアップ Application Insights](/azure/application-insights/app-insights-asp-net) 」を参照してください。

クラウド環境にとって優れた点の1つは、お客様の勝利を簡単に購入またはレンタルできることです。 テレメトリは一例です。 多くの労力を費やすことなく、非常に優れたテレメトリシステムを稼働させることができ、コスト効率に優れています。 Azure と統合される優れたパートナーが多数あり、その中には free レベルがあるものもあります。これにより、何の基本テレメトリも取得できます。 Azure で現在使用できるもののほんの一部を次に示します。

- [新しい聖箱](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#)には、監視機能も含まれています。

製品利用統計情報システムを簡単に使用できるように、新しい聖箱を設定する手順を簡単に説明します。

Azure 管理ポータルで、サービスにサインアップします。 **[新規]** をクリックし、 **[ストア]** をクリックします。 **[アドオンの選択]** ダイアログボックスが表示されます。 下にスクロールし、 **[新しい聖箱]** をクリックします。

![アドオンの選択](monitoring-and-telemetry/_static/image1.png)

右矢印をクリックし、目的のサービスレベルを選択します。 このデモでは、free レベルを使用します。

![アドオンの個人用設定](monitoring-and-telemetry/_static/image2.png)

右矢印をクリックし、[購入] を確認します。新しい聖箱がポータルにアドオンとして表示されるようになりました。

![購入の確認](monitoring-and-telemetry/_static/image3.png)

![管理ポータルの新しい聖なるアドオン](monitoring-and-telemetry/_static/image4.png)

**[接続情報]** をクリックし、ライセンスキーをコピーします。

![接続情報](monitoring-and-telemetry/_static/image5.png)

ポータルで web アプリの **[構成]** タブに移動し、 **[パフォーマンスの監視]** を**アドオン**に設定して、 **[アドオンの選択]** ドロップダウンリストを **[新しい聖箱]** に設定します。 **[保存]** をクリックします。

![[構成] タブの新しい聖箱](monitoring-and-telemetry/_static/image6.png)

Visual Studio で、新しい聖なる NuGet パッケージをアプリにインストールします。

![[構成] タブの開発者分析](monitoring-and-telemetry/_static/image7.png)

アプリを Azure にデプロイし、使用を開始します。 いくつかの修正プログラムを作成して、新しい箱が監視するための活動を提供します。

次に、ポータルの **[アドオン] タブに**ある**新しい聖**金のページに戻り、 **[管理]** をクリックします。 認証にシングルサインオンを使用して、資格情報を再度入力する必要がないように、ポータルから新しい聖管理ポータルに送信されます。 [概要] ページには、さまざまなパフォーマンス統計情報が表示されます。 (画像をクリックすると、[概要] ページの最大サイズが表示されます)。

[![新しい聖箱の監視 タブ](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

表示できる統計情報の一部を次に示します。

- 1日の異なる時刻の平均応答時間。

    ![応答時間](monitoring-and-telemetry/_static/image10.png)
- 1日の異なる時間におけるスループット率 (1 分あたりの要求数)。

    ![スループット](monitoring-and-telemetry/_static/image11.png)
- 異なる HTTP 要求の処理に費やされたサーバーの CPU 時間。

    ![Web トランザクション時間](monitoring-and-telemetry/_static/image12.png)
- アプリケーションコードのさまざまな部分で費やされた CPU 時間:

    ![トレースの詳細](monitoring-and-telemetry/_static/image13.png)
- 履歴パフォーマンスの統計情報。

    ![パフォーマンス履歴](monitoring-and-telemetry/_static/image14.png)
- Blob service などの外部サービスへの呼び出し、およびサービスの信頼性と応答性に関する統計情報。

    ![外部サービス](monitoring-and-telemetry/_static/image15.png)

    ![外部サービス](monitoring-and-telemetry/_static/image16.png)

    ![外部サービス](monitoring-and-telemetry/_static/image17.png)
- 世界中のどこにあるか、または米国 web アプリのトラフィックのどこにあるかに関する情報。

    ![Geography](monitoring-and-telemetry/_static/image18.png)

また、レポートとイベントを設定することもできます。 たとえば、エラーが発生し始めるたびに、アラートサポートスタッフに電子メールを送信して問題を報告することができます。

![レポート](monitoring-and-telemetry/_static/image19.png)

新しい聖箱は、テレメトリシステムの一例にすぎません。これは、他のサービスからも取得できます。 クラウドの利点は、コードを記述しなくても、最小限またはまったく費用をかけることなく、アプリケーションの使用状況や顧客の実際の使用状況について、さらに多くの情報を得ることができることです。

<a id="log"></a>
## <a name="log-for-insight"></a>詳細情報のログ

テレメトリパッケージは最初の手順として適していますが、独自のコードをインストルメント化する必要もあります。 テレメトリサービスでは、問題が発生したことが通知され、顧客がどのような状況を抱えているかがわかりますが、コード内で何が起こっているかについての洞察が得られない場合があります。

アプリの動作を確認するために、実稼働サーバーにリモートである必要はありません。 1台のサーバーを使用していても、何百ものサーバーに拡張した場合はどうすればよいでしょうか。 ログには、問題を分析してデバッグするために実稼働サーバーにリモートで必要とされない十分な情報が提供される必要があります。 ログを使用して問題を特定できるように、十分な情報をログに記録しておく必要があります。

### <a name="log-in-production"></a>運用環境のログイン

多くのユーザーは、問題があり、デバッグする必要がある場合にのみ、運用環境でのトレースを有効にします。 これにより、問題が発生してから、その問題に関するトラブルシューティング情報が得られるまでに、かなりの遅延が生じる可能性があります。 また、断続的なエラーについては役に立たないことがあります。

ストレージが安価なクラウド環境では、常に運用環境にログオンしたままにしておくことをお勧めします。 このようにすると、エラーが発生した場合は、既にログに記録されています。履歴データを使用すると、時間の経過と共に、または定期的に発生する問題を分析するのに役立ちます。 パージプロセスを自動化して古いログを削除することもできますが、ログを保持するよりも、このようなプロセスを設定する方がコストがかかる場合があります。

ログ記録の費用は、トラブルシューティングにかかる時間と、問題が発生したときに必要なすべての情報を取得することによって節約できるコストと比較して簡単です。 その後、だれかが、最後夜8:00 前後にランダムなエラーが発生したことを知らせても、エラーを覚えていないので、問題の原因をすぐに把握できます。

1か月あたり $4 未満の場合、ログは 50 gb まで保持できます。また、パフォーマンスのボトルネックを回避するために、ログ記録のパフォーマンスへの影響はごくわずかです。パフォーマンスのボトルネックを回避するには、ログライブラリが非同期であることを確認してください。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>アクションを必要とするログから通知されるログを区別する

ログは、(何かを知りたい)、または行動 (何かを行います) を通知するためのものです。 ACT ログは、純粋がユーザーまたは自動化されたプロセスを実行する必要がある問題に対してのみ記述するように注意してください。 ACT ログの数が多すぎると、ノイズが発生し、正規の問題を検出するためにすべてを処理するのに多くの作業が必要になります。 また、ACT ログで、サポートスタッフに電子メールを送信するなどのアクションが自動的にトリガーされる場合は、1つの問題によって何千ものアクションがトリガーされないようにしてください。

.NET システムの診断トレースでは、ログにエラー、警告、情報、デバッグ/詳細レベルを割り当てることができます。 Act ログのエラーレベルを予約し、ログ記録のために低いレベルを使用することで、ACT ログから ACT を区別できます。

![ログ レベル](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>実行時にログ記録レベルを構成する

運用環境でログを常にオンにすることは非常に便利ですが、もう1つのベストプラクティスは、ログ記録フレームワークを実装することです。これにより、アプリケーションを再デプロイしたり再起動したりすることなく、ログ記録する詳細レベルの実行時に調整できます。 たとえば、`System.Diagnostics` のトレース機能を使用すると、エラー、警告、情報、およびデバッグ/詳細ログを作成できます。 常にエラー、警告、および情報のログを運用環境に記録することをお勧めします。また、トラブルシューティングのためにデバッグ/詳細ログを動的に追加することもできます。

Azure App Service の Web Apps には、ファイルシステム、テーブルストレージ、または Blob ストレージに `System.Diagnostics` ログを書き込むためのサポートが組み込まれています。 ストレージの宛先ごとに異なるログ記録レベルを選択できます。また、アプリケーションを再起動しなくてもログ記録レベルを変更できます。 Blob storage のサポートにより[、hdinsight の分析ジョブ](https://docs.microsoft.com/azure/hdinsight/)をアプリケーションログで簡単に実行できるようになります。これは、Hdinsight が blob ストレージを直接操作する方法を認識しているためです。

### <a name="log-exceptions"></a>例外をログに記録する

例外を挿入しないで*ください。* ログコード内の ToString ()。 これにより、コンテキスト情報が残されます。 SQL エラーの場合は、SQL エラー番号は残されます。 すべての例外について、トラブルシューティングに必要なすべてのものを確実に提供するために、コンテキスト情報、例外自体、および内部例外を含めてください。 たとえば、コンテキスト情報には、サーバー名、トランザクション識別子、およびユーザー名を含めることができます (ただし、パスワードやシークレットは使用できません)。

各開発者が例外ログを使用して適切な作業を行う場合、その一部は実行されません。 毎回適切に実行されるようにするには、logger インターフェイスに例外処理を直接作成します。この場合、例外オブジェクト自体を logger クラスに渡し、logger クラスで例外データを適切にログに記録します。

### <a name="log-calls-to-services"></a>サービスへの呼び出しをログに記録する

アプリケーションがサービスを呼び出すたびに、データベース、REST API、または外部のサービスのいずれであるかにかかわらず、ログを作成することを強くお勧めします。 ログには、成功または失敗を示すだけでなく、各要求の所要時間も示されます。 クラウド環境では、完全な停止ではなく、低速ダウンに関連する問題が頻繁に発生します。 通常、10ミリ秒かかることがあります。 アプリの速度が低下していることを知らせる場合は、新しい聖を見たり、お客様の経験を持っている製品利用統計情報サービスを確認したり、自分のログを調べて、それが遅い理由の詳細を確認したりできるようにする必要があります。

### <a name="use-an-ilogger-interface"></a>ILogger インターフェイスを使用する

実稼働アプリケーションを作成する際には、単純な*ILogger*インターフェイスを作成し、メソッドをいくつか使用することをお勧めします。 これにより、後でログの実装を変更することが容易になり、コードを実行する必要がなくなります。 `System.Diagnostics.Trace` クラスを修正することもできますが、その代わりに、 *ILogger*を実装するログ記録クラスの内部で使用しているので、アプリ全体で*ILogger*メソッド呼び出しを行います。

このようにして、ログ記録を充実させたい場合は、 [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs)を任意のログメカニズムに置き換えることができます。 たとえば、アプリのサイズが大きくなると、 [Nlog](http://nlog-project.org/)や[エンタープライズライブラリのログ記録アプリケーションブロック](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)などのより包括的なログパッケージを使用することになります。 ([Log4Net](http://logging.apache.org/log4net/)はもう1つの一般的なログ記録フレームワークですが、非同期ログ記録は行われません)。

NLog などのフレームワークを使用することの考えられる理由の1つは、ログ出力を複数の大きなデータストアに分割しやすくすることです。 この機能を使用すると、大量の通知データを効率的に保存しながら、高速なクエリを実行する必要がなく、ACT データへのすばやいアクセスを維持することができます。

### <a name="semantic-logging"></a>セマンティックログ記録

より有用な診断情報を生成する可能性のある、比較的新しいログ記録を行う方法については、「[エンタープライズライブラリのセマンティックログアプリケーションブロック (スラブ)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)」を参照してください。 スラブでは、.NET 4.5 の[Windows イベントトレーシング](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)(ETW) と[EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)サポートを使用して、より構造化されたクエリ可能なログを作成できます。 記録するイベントの種類ごとに異なる方法を定義することで、記述する情報をカスタマイズできます。 たとえば、SQL Database エラーをログに記録するには、`LogSQLDatabaseError` メソッドを呼び出すことがあります。 この種の例外については、重要な情報がエラー番号であることがわかっているので、エラー番号パラメーターをメソッドシグネチャに含めて、記述したログレコードの別のフィールドとしてエラー番号を記録することができます。 この数値は別のフィールドにあるため、エラー番号をメッセージ文字列に連結しただけの場合よりも、SQL エラー番号に基づいてより簡単かつ確実にレポートを取得できます。

## <a name="logging-in-the-fix-it-app"></a>It アプリを修正する

### <a name="the-ilogger-interface"></a>ILogger インターフェイス

Fix It アプリの*ILogger*インターフェイスを次に示します。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

これらのメソッドを使用すると、*システム診断*でサポートされているのと同じ4つのレベルでログを書き込むことができます。 TraceApi メソッドは、待機時間に関する情報と共に外部サービス呼び出しをログに記録するためのメソッドです。 デバッグ/詳細レベルのメソッドのセットを追加することもできます。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger インターフェイスの Logger 実装

インターフェイスの実装は非常に単純です。 基本的には、標準の*システム診断*メソッドを呼び出すだけです。 次のスニペットは、3つの情報メソッドとそのそれぞれを示しています。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger メソッドの呼び出し

Fix It アプリ内のコードが例外をキャッチするたびに、 *ILogger*メソッドを呼び出して例外の詳細をログに記録します。 また、データベース、Blob service、または REST API の呼び出しが行われるたびに、呼び出しの前にストップウォッチが開始され、サービスが戻ったときにストップウォッチが停止され、成功または失敗に関する情報と共に経過時間が記録されます。

ログメッセージにクラス名とメソッド名が含まれていることに注意してください。 ログメッセージによって、アプリケーションコードのどの部分が記述されているかを特定することをお勧めします。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

この時点で、修正プログラムのアプリが SQL Database を呼び出すたびに、呼び出し、呼び出したメソッド、およびどれだけの時間がかかったかを確認できます。

![ログでのクエリの SQL Database](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

ログを参照すると、データベース呼び出しの時間が変動することがわかります。 この情報は役に立つ可能性があります。これは、アプリがすべてをログに記録するため、データベースサービスが時間の経過と共にどのように実行されているかの履歴傾向を分析できます。 たとえば、サービスは最も時間がかかる場合がありますが、要求が失敗したり、特定の時間帯に応答が遅くなったりすることがあります。

Blob service に対しても同じことを行うことができます。アプリが新しいファイルをアップロードするたびにログが記録され、各ファイルのアップロードにかかった時間を正確に確認できます。

![Blob アップロードログ](monitoring-and-telemetry/_static/image23.png)

これは、サービスを呼び出すたびに記述する数行のコード行にすぎません。問題が発生した場合は、問題の内容、エラーかどうか、または実行速度が低下しているかどうかを正確に知ることができます。 問題の原因を特定するには、サーバーにリモートでいる必要はありません。エラーが発生した後にログ記録をオンにして、再作成することをお勧めします。

## <a name="dependency-injection-in-the-fix-it-app"></a>It アプリを修正するための依存関係の挿入

上の例のリポジトリコンストラクターが logger インターフェイスの実装を取得する方法については、次のようになります。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

インターフェイスを実装に接続するために、アプリは[AutoFac](http://autofac.org/)を使用して[依存関係の挿入](http://en.wikipedia.org/wiki/Dependency_injection)(DI) を使用します。 DI を使用すると、コード内のさまざまな場所でインターフェイスに基づくオブジェクトを使用できます。また、インターフェイスがインスタンス化されるときに使用される実装を1つの場所で指定するだけで済みます。 これにより、実装の変更が簡単になります。たとえば、システム診断 logger を NLog logger に置き換えることができます。 または、自動化されたテストでは、logger のモックバージョンに置き換えることができます。

Fix It アプリケーションは、すべてのリポジトリとすべてのコントローラーで DI を使用します。 コントローラークラスのコンストラクターは、リポジトリが logger インターフェイスを取得するのと同じ方法で*ITaskRepository*インターフェイスを取得します。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

アプリは、AutoFac DI ライブラリを使用して、これらのコンストラクターに*Taskrepository*と*Logger*インスタンスを自動的に提供します。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

このコードは基本的に、コンストラクターが*ILogger*インターフェイスを必要とし、 *Logger*クラスのインスタンスを渡す場合、および*ifixittaskrepository*インターフェイスが必要な場合は、 *fixittaskrepository*クラスのインスタンスを渡すことを意味します。

[AutoFac](http://autofac.org/)は、使用できる多くの依存関係挿入フレームワークの1つです。 また、Microsoft のパターンとプラクティスで推奨およびサポートされている[Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)もあります。

## <a name="built-in-logging-support-in-azure"></a>Azure での組み込みのログ記録のサポート

Azure では、Azure App Service の[Web Apps に対して](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)次の種類のログ記録をサポートしています。

- システム診断トレース (サイトを再起動しなくても、オンとオフを切り替えることができ、レベルを設定できます)。
- Windows イベント。
- IIS ログ (HTTP/FREB)。

Azure では、Cloud Services で次の種類の[ログ記録](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)をサポートしています。

- システム診断のトレース。
- パフォーマンス カウンター。
- Windows イベント。
- IIS ログ (HTTP/FREB)。
- カスタムディレクトリ監視。

Fix It アプリは、Diagnostics トレースを使用します。 Web アプリでの診断ログの記録を有効にするために必要な作業は、ポータルでスイッチを反転させるか、REST API を呼び出すことだけです。 ポータルで、サイトの **[構成]** タブをクリックし、下にスクロールして **[アプリケーション診断]** セクションを表示します。 ログ記録をオンまたはオフにして、目的のログ記録レベルを選択することができます。 Azure では、ファイルシステムまたはストレージアカウントにログを書き込むことができます。

![[構成] タブのアプリ診断とサイト診断](monitoring-and-telemetry/_static/image24.png)

Azure でのログ記録を有効にすると、Visual Studio の [出力] ウィンドウにログが表示されます。

![ストリーミングログメニュー](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![ストリーミングログメニュー](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

また、ログをストレージアカウントに書き込んで、Visual Studio や[Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/)の**サーバーエクスプローラー**などの Azure Storage Table service にアクセスできる任意のツールでログを表示することもできます。

![サーバーエクスプローラーのログイン](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>要約

すぐに使えるテレメトリシステムを実装し、独自のコードでログ記録を行い、Azure でのログ記録を構成するのは非常に簡単です。 また、運用上の問題がある場合は、テレメトリシステムとカスタムログを組み合わせて使用することで、顧客にとって大きな問題になる前に問題を迅速に解決できるようになります。

次の[章](transient-fault-handling.md)では、調査する必要がある運用上の問題にならないように、一時的なエラーを処理する方法について説明します。

## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

製品利用統計情報に関するドキュメント:

- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 「インストルメンテーションとテレメトリに関するガイダンス」、「サービスメータリングのガイダンス」、「正常性エンドポイントの監視パターン」、および「ランタイム再構成パターン」を参照してください。
- [クラウドでの小額ピンチ: Azure Websites での新しい聖なるパフォーマンス監視を有効に](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)します。
- [Azure Cloud Services で大規模なサービスを設計するためのベストプラクティス](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 マーク Simm と Michael Thomassy によるホワイトペーパー。 「テレメトリと診断」セクションを参照してください。
- [Application Insights を使用した次世代の開発](https://msdn.microsoft.com/magazine/dn683794.aspx)。 MSDN マガジンの記事です。

ログ記録に関するドキュメント:

- [セマンティックログアプリケーションブロック (スラブ)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 Neil Mackenzie は、スラブを使用したセマンティックログ記録のケースを示しています。
- [セマンティックログを使用して、構造化された意味のあるログを作成](https://channel9.msdn.com/Events/Build/2013/3-336)します。 Videoユリウス Dominguez は、スラブを使用したセマンティックログ記録のケースを示しています。
- [EF6 SQL のログ記録–パート 1: 単純なログ記録](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur ヴィッカースは、EF 6 の Entity Framework によって実行されるクエリをログに記録する方法を示しています。
- [ASP.NET MVC アプリケーションでの Entity Framework を使用した接続の回復性とコマンドのインターセプト](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 9部構成のチュートリアルシリーズの第4部では、EF 6 のコマンドインターセプト機能を使用して、Entity Framework によってデータベースに送信された SQL コマンドをログに記録する方法を示します。
- [5.0 呼び出し元C#情報の属性を使用してログ記録を強化](http://www.dotnetcurry.com/showarticle.aspx?ID=972)します。 呼び出し元のメソッドの名前を、リテラルにハードコーディングしたり、リフレクションを使用して手動で取得したりせずに、簡単にログに記録する方法。

ドキュメント: 主にトラブルシューティングについて説明します。

- [Azure のトラブルシューティング &amp; デバッグに関するブログ](https://blogs.msdn.com/b/kwill/)
- [Azuretools – Azure Developer サポートチームによって使用される診断ユーティリティ](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)です。 では、さまざまな診断ツールと監視ツールをダウンロードして実行するために Azure VM で使用できるツールのダウンロードリンクが導入されています。 特定の VM の問題を診断する必要がある場合に便利です。
- [Visual Studio を使用して Azure App Service の web アプリのトラブルシューティングを](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)行います。 このチュートリアルでは、システム診断のトレースとリモートデバッグの概要について説明します。

ビデオ:

- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9パートシリーズ。 高度な概念とアーキテクチャの原則を、非常にアクセスしやすく興味深い方法で紹介します。実際の顧客との Microsoft カスタマーアドバイザリチーム (CAT) エクスペリエンスによってストーリーが描画されます。 エピソード4と9は、監視とテレメトリに関するものです。 エピソード9には、監視サービス MetricsHub、AppDynamics、新しい聖数、および PagerDuty の概要が含まれています。
- [大規模な構築: Azure のお客様から学んだ教訓-パート II](https://channel9.msdn.com/Events/Build/2012/3-030)。 Simm マークは、エラーの設計とすべてのインストルメント化について話します。 フェイルセーフシリーズに似ていますが、さらに詳細な方法について説明します。

コードサンプル:

- [Azure のクラウドサービスの基礎](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 Microsoft Azure Customer アドバイザリチームによって作成されたサンプルアプリケーション。 次の記事で説明されているように、テレメトリとログ記録の両方のプラクティスを示します。 このサンプルでは、 [Nlog](http://nlog-project.org/)を使用してアプリケーションのログ記録を実装します。 関連ドキュメントについては、[テレメトリとログに関する4つの TechNet wiki 記事](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)を参照してください。

> [!div class="step-by-step"]
> [前へ](design-to-survive-failures.md)
> [次へ](transient-fault-handling.md)
