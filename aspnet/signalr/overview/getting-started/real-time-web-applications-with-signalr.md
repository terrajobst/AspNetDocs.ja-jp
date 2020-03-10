---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 'ハンズオンラボ: SignalR を使用したリアルタイム Web アプリケーション |Microsoft Docs'
author: bradygaster
description: リアルタイム Web アプリケーションは、接続されているクライアントに対して、リアルタイムでサーバー側のコンテンツをプッシュする機能を備えています。 ASP.NET 開発者向けの ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431668"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a>ハンズオンラボ: SignalR を使用したリアルタイム Web アプリケーション

[Web キャンプチーム](https://twitter.com/webcamps)別

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[Web キャンプトレーニングキットのダウンロード (2015 年10月リリース)](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> リアルタイム Web アプリケーションは、接続されているクライアントに対して、リアルタイムでサーバー側のコンテンツをプッシュする機能を備えています。 ASP.NET 開発者にとって、 **ASP.NET SignalR**は、リアルタイム web 機能をアプリケーションに追加するためのライブラリです。 複数のトランスポートを利用し、クライアントおよびサーバーの最適なトランスポートを指定して、最適なトランスポートを自動的に選択します。 これは、ブラウザーとサーバー間の双方向通信を可能にする HTML5 API である**WebSocket**を利用します。
> 
> また、 **SignalR**は、ASP.NET アプリケーションでサーバーとクライアントの RPC を実行するための単純な高レベルの API (サーバー側の .net コードからクライアントのブラウザーで JavaScript 関数を呼び出す) を提供するだけでなく、接続/切断イベント、グループ化接続、承認など、接続管理のための便利なフックを追加します。
> 
> **SignalR**は、クライアントとサーバー間でリアルタイムの作業を行うために必要なトランスポートの一部を抽象化したものです。 **SignalR**接続は HTTP として起動し、使用可能な場合は**WebSocket**接続に昇格されます。 **Websocket**は**SignalR**に最適なトランスポートです。これは、サーバーのメモリを最も効率的に使用し、待機時間が最も短く、最も基本的な機能 (クライアントとサーバー間の完全な双方向通信など) を備えているためです。 **websocket**では、サーバーが**windows server 2012**または**windows 8**を使用している必要がありますが、 **.NET Framework 4.5**。 これらの要件が満たされていない場合、 **SignalR**は他のトランスポートを使用して接続しようとします ( *Ajax 長時間ポーリング*など)。
> 
> **SignalR** API には、クライアントとサーバー間の通信用に、**永続的な接続**と**ハブ**の2つのモデルが含まれています。 **接続**は、単一受信者、グループ化、またはブロードキャストメッセージを送信するための単純なエンドポイントを表します。 **ハブ**は、接続 API に基づいて構築されたより高度なパイプラインで、クライアントとサーバーが互いにメソッドを直接呼び出すことができます。
> 
> ![SignalR アーキテクチャ](real-time-web-applications-with-signalr/_static/image1.png)
> 
> すべてのサンプルコードとスニペットは、 [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)で提供される2015年10月リリースの Web キャンプトレーニングキットに含まれています。  このページのインストーラーのリンクは機能しなくなっていることに注意してください。代わりに、Assets セクションの下にあるいずれかのリンクを使用してください。

<a id="Overview"></a>
## <a name="overview"></a>概要

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- SignalR を使用して、サーバーからクライアントに通知を送信します。
- **SQL Server**を使用して SignalR アプリケーションを Scale Out します。

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このハンズオンラボを完了するには、次のものが必要です。

- [Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。

1. Windows エクスプローラーウィンドウを開き、ラボの**ソース**フォルダーを参照します。
2. **[Setup.exe]** を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。
3. ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。

> [!NOTE]
> セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>コードスニペットの使用

ラボドキュメント全体で、コードブロックを挿入するように指示されます。 便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。

> [!NOTE]
> 各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。 演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。 演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。 このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。

---

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [SignalR を使用したリアルタイムデータの操作](#Exercise1)
2. [SQL Server を使用したスケールアウト](#Exercise2)

このラボの推定所要時間: **60 分**

> [!NOTE]
> Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。 定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。 このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。 開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>演習 1: SignalR を使用したリアルタイムデータの操作

チャットは例としてよく使用されますが、リアルタイムの Web 機能を使用して、さらに多くのことを行うことができます。 ユーザーが web ページを更新して新しいデータを表示したり、新しいデータを取得するために Ajax 長いポーリングを実装するたびに、SignalR を使用することができます。

SignalR は**サーバープッシュ**または**ブロードキャスト**機能をサポートしています。接続管理は自動的に処理されます。 クライアントとサーバー間の通信に対する従来の HTTP 接続では、要求ごとに接続が再確立されますが、SignalR はクライアントとサーバー間の永続的な接続を提供します。 SignalR では、サーバーコードは、現在知られている要求-応答モデルではなく、リモートプロシージャコール (RPC) を使用してブラウザーでクライアントコードを呼び出します。

この演習では、SignalR を使用して統計ダッシュボードと更新されたメトリックを表示するように**マニアクイズ**アプリケーションを構成します。ページ全体を更新する必要はありません。

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>タスク1–マニアクイズ統計ページを調べる

このタスクでは、アプリケーションを実行し、統計ページがどのように表示されるか、および情報の更新方法を改善する方法を確認します。

1. **Web 用 Visual Studio Express 2013**を開き、 **Source\Ex1-WorkingWithRealTimeData\Begin**フォルダーにある**GeekQuiz**ソリューションを開きます。
2. F5 キーを押して、ソリューションを実行します。 ブラウザーに**ログイン**ページが表示されます。

    ![ソリューションの実行](real-time-web-applications-with-signalr/_static/image2.png "ソリューションの実行")

    *ソリューションの実行*
3. ページの右上隅にある **[登録]** をクリックして、アプリケーションに新しいユーザーを作成します。

    ![リンクの登録](real-time-web-applications-with-signalr/_static/image3.png "リンクの登録")

    *リンクの登録*
4. **[登録]** ページで、**ユーザー名**と**パスワード**を入力し、 **[登録]** をクリックします。

    ![ユーザーの登録](real-time-web-applications-with-signalr/_static/image4.png "ユーザーの登録")

    *ユーザーの登録*
5. アプリケーションは新しいアカウントを登録し、ユーザーは認証されて、最初のクイズの質問を示すホームページにリダイレクトされます。
6. 新しいウィンドウで **[統計]** ページを開き、[**ホーム**ページと**統計情報**] ページを横に並べて表示します。

    ![サイドバイサイドウィンドウ](real-time-web-applications-with-signalr/_static/image5.png "サイドバイサイドウィンドウ")

    *サイドバイサイドウィンドウ*
7. **ホーム**ページで、いずれかのオプションをクリックして質問に回答します。

    ![質問への回答](real-time-web-applications-with-signalr/_static/image6.png "質問への回答")

    *質問への回答*
8. いずれかのボタンをクリックすると、回答が表示されます。

    ![回答が正しい質問](real-time-web-applications-with-signalr/_static/image7.png "回答が正しい質問")

    *質問に正しく回答*
9. [統計] ページに表示される情報が古くなっていることに注意してください。 更新された結果を表示するためにページを更新します。

    ![[統計] ページ](real-time-web-applications-with-signalr/_static/image8.png "[統計] ページ")

    *[統計] ページ*
10. Visual Studio に戻り、デバッグを停止します。

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>タスク2–マニアクイズに SignalR を追加してオンライングラフを表示する

このタスクでは、SignalR をソリューションに追加し、新しい回答がサーバーに送信されたときにクライアントに自動的に更新を送信します。

1. Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** をクリックします。
2. **[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを実行します。

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR パッケージのインストール](real-time-web-applications-with-signalr/_static/image9.png "SignalR パッケージのインストール")

    *SignalR パッケージのインストール*

   > [!NOTE]
   > 新しい MVC 5 アプリケーションから**SignalR** NuGet パッケージバージョン2.0.2 をインストールする場合は、SignalR をインストールする前に**OWIN**パッケージをバージョン 2.0.1 (またはそれ以降) に手動で更新する必要があります。 これを行うには、**パッケージマネージャーコンソール**で次のスクリプトを実行します。
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > SignalR の今後のリリースでは、OWIN の依存関係が自動的に更新されます。
3. **ソリューションエクスプローラー**で、 **Scripts**フォルダーを展開し、SignalR *js*ファイルがソリューションに追加されたことを確認します。

    ![SignalR JavaScript の参照](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript の参照")

    *SignalR JavaScript の参照*
4. **ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトを右クリックし、 **[追加]** [ | **新しいフォルダー**] の順に選択して、**ハブ**に名前を指定します。
5. **ハブ** フォルダーを右クリックし、追加 を選択します。 **新しい項目**。

    ![新しい項目の追加](real-time-web-applications-with-signalr/_static/image11.png "新しい項目の追加")

    *新しい項目の追加*
6. **[新しい項目の追加]** ダイアログボックスで、 **[ C# Visual |] を選択します。Web |SignalR**ノード左側のウィンドウで、中央のウィンドウから **[SignalR Hub クラス (v2)]** を選択し、ファイルに**StatisticsHub.cs**という名前を指定して、 **[追加]** をクリックします。

    ![[新しい項目の追加] ダイアログボックス](real-time-web-applications-with-signalr/_static/image12.png "[新しい項目の追加] ダイアログボックス")

    *[新しい項目の追加] ダイアログボックス*
7. **StatisticsHub**クラスのコードを次のコードに置き換えます。

    (コードスニペット- *Realtimesignalr-Ex1-StatisticsHubClass*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. **Startup.cs**を開き、**構成**メソッドの末尾に次の行を追加します。

    (コードスニペット- *Realtimesignalr-Ex1-MapSignalR*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. **Services**フォルダー内の**StatisticsService.cs**ページを開き、次の using ディレクティブを追加します。

    (コードスニペット- *Realtimesignalr-Ex1 ディレクティブ*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. 接続しているクライアントに更新プログラムを通知するには、最初に現在の接続の**コンテキスト**オブジェクトを取得します。 **ハブ**オブジェクトには、1つのクライアントにメッセージを送信したり、接続されているすべてのクライアントにブロードキャストしたりするメソッドが含まれています。 次のメソッドを**StatisticsService**クラスに追加して、統計データをブロードキャストします。

    (コードスニペット- *Realtimesignalr-Ex1-NotifyUpdatesMethod*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > 上記のコードでは、任意のメソッド名を使用してクライアント上の関数を呼び出しています (つまり、 *updateStatistics*)。 指定したメソッド名は動的オブジェクトとして解釈されます。つまり、IntelliSense やコンパイル時の検証は行われません。 式は実行時に評価されます。 メソッドの呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。 クライアントに名前と一致するメソッドがある場合、そのメソッドが呼び出され、パラメーター値が渡されます。 一致するメソッドがクライアントに見つからない場合、エラーは発生しません。 詳細については、 [ASP.NET SignalR HUB API ガイド](../guide-to-the-api/hubs-api-guide-server.md)を参照してください。
11. **Controllers**フォルダー内の**TriviaController.cs**ページを開き、次の using ディレクティブを追加します。

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. 次の強調表示されたコードを**Post**アクションメソッドに追加します。

    (コードスニペット- *Realtimesignalr-Ex1-Notifyアップデートの呼び出し*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. ビュー内の Statistics ページを開きます **。** **ホーム**フォルダー。 **Scripts**セクションを見つけて、セクションの先頭に次のスクリプト参照を追加します。

    (コードスニペット- *Realtimesignalr-Ex1-SignalRScriptReferences*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > SignalR およびその他のスクリプトライブラリを Visual Studio プロジェクトに追加すると、パッケージマネージャーによって、このトピックに示されているバージョンよりも新しいバージョンの SignalR スクリプトファイルがインストールされる場合があります。 コード内のスクリプト参照が、プロジェクトにインストールされているスクリプトライブラリのバージョンと一致していることを確認します。
14. クライアントを SignalR hub に接続し、ハブから新しいメッセージを受信したときに統計データを更新するために、次の強調表示されたコードを追加します。

    (コードスニペット- *Realtimesignalr-Ex1-SignalRClientCode*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    このコードでは、ハブプロキシを作成し、サーバーから送信されたメッセージをリッスンするイベントハンドラーを登録します。 この場合は、 *updateStatistics*メソッドを介して送信されたメッセージをリッスンします。

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>タスク3–ソリューションを実行する

このタスクでは、ソリューションを実行して、新しい質問に回答した後、SignalR を使用して統計ビューが自動的に更新されていることを確認します。

1. F5 キーを押して、ソリューションを実行します。

    > [!NOTE]
    > まだアプリケーションにログインしていない場合は、タスク1で作成したユーザーでログインします。
2. 新しいウィンドウで **[統計]** ページを開き、タスク1で行ったように**ホーム**ページと**統計情報**のページを並べて表示します。
3. **ホーム**ページで、いずれかのオプションをクリックして質問に回答します。

    ![別の質問への回答](real-time-web-applications-with-signalr/_static/image13.png "別の質問への回答")

    *別の質問への回答*
4. いずれかのボタンをクリックすると、回答が表示されます。 ページ全体を更新する必要なく、更新された情報で質問に回答した後、ページの統計情報が自動的に更新されることに注意してください。

    ![回答後に更新された統計ページ](real-time-web-applications-with-signalr/_static/image14.png "回答後に更新された統計ページ")

    *回答後に更新された統計ページ*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>演習 2: SQL Server を使用したスケールアウト

Web アプリケーションをスケーリングする場合は、通常、*スケールアップ*と*スケールアウト*のオプションのいずれかを選択できます。 スケール*アップ*とは、より大きなサーバーを使用して、より多くのリソース (CPU、RAM など) を使用することです。*スケールアウト*とは、負荷を処理するためにサーバーを追加することを意味します。 後者の問題は、クライアントが異なるサーバーにルーティングされる可能性があることです。 1つのサーバーに接続されているクライアントは、別のサーバーから送信されたメッセージを受信しません。

*バックプレーン*と呼ばれるコンポーネントを使用して、サーバー間でメッセージを転送することで、これらの問題を解決できます。 バックプレーンが有効になっている場合、各アプリケーションインスタンスはバックプレーンにメッセージを送信し、バックプレーンはそれらを他のアプリケーションインスタンスに転送します。

現在、SignalR には3種類の背面があります。

- **Windows Azure Service Bus**。 Service Bus は、コンポーネントが疎結合されたメッセージを送信できるようにするメッセージングインフラストラクチャです。
- **SQL Server**。 SQL Server バックプレーンは、SQL テーブルにメッセージを書き込みます。 バックプレーンは、効率的なメッセージングのために Service Broker を使用します。 ただし、Service Broker が有効になっていない場合にも機能します。
- **Redis**。 Redis は、メモリ内のキーと値のストアです。 Redis は、メッセージを送信するためのパブリッシュ/サブスクライブ ("pub/sub") パターンをサポートしています。

すべてのメッセージは、メッセージバスを介して送信されます。 メッセージバスは、パブリッシュ/サブスクライブの抽象化を提供する[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)インターフェイスを実装します。 背面は、既定の**IMessageBus**をそのバックプレーン用に設計されたバスに置き換えることによって機能します。

各サーバーインスタンスは、バスを介してバックプレーンに接続します。 メッセージが送信されると、バックプレーンに送られ、バックプレーンがすべてのサーバーに送信します。 サーバーは、バックプレーンからメッセージを受信すると、メッセージをローカルキャッシュに格納します。 サーバーは、ローカルキャッシュからクライアントにメッセージを配信します。

SignalR バックプレーンの動作の詳細については、こちらの[記事](../performance/scaleout-in-signalr.md)を参照してください。

> [!NOTE]
> バックプレーンがボトルネックになる可能性があるシナリオがいくつかあります。 一般的な SignalR シナリオをいくつか次に示します。
> 
> - [サーバーブロードキャスト](tutorial-server-broadcast-with-signalr.md)(stock ティッカーなど): 背面は、このシナリオに適しています。これは、サーバーがメッセージの送信速度を制御するためです。
> - [クライアント対クライアント](tutorial-getting-started-with-signalr.md)(チャットなど): このシナリオでは、メッセージの数がクライアントの数に合わせてスケーリングされる場合、バックプレーンはボトルネックになる可能性があります。これは、より多くのクライアントが参加したときにメッセージの割合が増加した場合に発生します。
> - [高頻度リアル](tutorial-high-frequency-realtime-with-signalr.md)タイム (リアルタイムゲームなど): このシナリオでは、バックプレーンはお勧めできません。

この演習では、 **SQL Server**を使用して、**マニアクイズ**アプリケーション間でメッセージを配布します。 これらのタスクを1つのテストコンピューターで実行して、構成を設定する方法を学習しますが、完全な効果を得るためには、SignalR アプリケーションを複数のサーバーに配置する必要があります。 また、いずれかのサーバーまたは別の専用サーバーに SQL Server をインストールする必要があります。

![SQL Server ダイアグラムを使用した Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>タスク 1-シナリオについて

このタスクでは、ローカルコンピューターで複数の IIS インスタンスをシミュレートする**マニアクイズ**の2つのインスタンスを実行します。 このシナリオでは、1つのアプリケーションでトリビアの質問に回答するときに、2番目のインスタンスの統計ページで更新プログラムに通知されません。 このシミュレーションは、アプリケーションが複数のインスタンスに配置され、ロードバランサーを使用してアプリケーションと通信する環境に似ています。

1. **Source/Ex2-スケール Ingoutwithsqlserver/begin**フォルダーにある**begin. .sln**ソリューションを開きます。 読み込みが完了すると、**サーバーエクスプローラー**が表示されます。このソリューションには、構造が同じで名前が異なる2つのプロジェクトがあることがわかります。 これにより、ローカルコンピューター上で同じアプリケーションの2つのインスタンスの実行がシミュレートされます。

    ![マニアクイズの2つのインスタンスをシミュレートするソリューションを開始する](real-time-web-applications-with-signalr/_static/image16.png "マニアクイズの2つのインスタンスをシミュレートするソリューションを開始する")

    *マニアクイズの2つのインスタンスをシミュレートするソリューションを開始する*
2. ソリューションの プロパティ ページを開くには、ソリューションノードを右クリックし、**プロパティ** を選択します。 **[スタートアッププロジェクト]** で、 **[マルチスタートアッププロジェクト]** を選択し、両方のプロジェクトの**アクション**値を [*開始*] に変更します。

    ![複数のプロジェクトの開始](real-time-web-applications-with-signalr/_static/image17.png "複数のプロジェクトの開始")

    *複数のプロジェクトの開始*
3. F5 キーを押して、ソリューションを実行します。 このアプリケーションでは、異なるポートで**マニアクイズ**の2つのインスタンスを起動し、同じアプリケーションの複数のインスタンスをシミュレートします。 左側のブラウザーのいずれかを画面の右側にピン留めします。 資格情報を使用してログインするか、新しいユーザーを登録します。 ログインしたら、左側にある トリビア ページを保持し、右側のブラウザーの **統計情報** ページに移動します。

    ![マニアクイズをサイドバイサイドで](real-time-web-applications-with-signalr/_static/image18.png)

    *マニアクイズをサイドバイサイドで*

    ![さまざまなポートでのマニアクイズ](real-time-web-applications-with-signalr/_static/image19.png)

    *さまざまなポートでのマニアクイズ*
4. 左側のブラウザーで質問への回答を開始すると、右側のブラウザーの **[統計]** ページが更新されていないことがわかります。 これは、 **SignalR**がローカルキャッシュを使用してクライアント間でメッセージを分散するためです。このシナリオでは複数のインスタンスがシミュレートされるため、キャッシュはそれらの間で共有されません。 **SignalR**が機能していることを確認するには、同じ手順を1つのアプリを使用してテストします。 次のタスクでは、インスタンス間でメッセージをレプリケートするようにバックプレーンを構成します。
5. Visual Studio に戻り、デバッグを停止します。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>タスク2– SQL Server バックプレーンの作成

このタスクでは、**マニアクイズ**アプリケーションのバックプレーンとして機能するデータベースを作成します。 **SQL Server オブジェクトエクスプローラー**を使用してサーバーを参照し、データベースを初期化します。 さらに、 **Service Broker**を有効にします。

1. **Visual Studio**で、メニュー**ビュー**を開き、 **[SQL Server オブジェクトエクスプローラー]** を選択します。
2. LocalDB インスタンスに接続するには、 **[SQL Server]** ノードを右クリックし、 **[SQL Server の追加]** オプションを選択します。

    ![SQL Server インスタンスの追加](real-time-web-applications-with-signalr/_static/image20.png "SQL Server インスタンスの追加")

    *SQL Server オブジェクトエクスプローラーへの SQL Server インスタンスの追加*
3. **サーバー名**を *(localdb) \ v11.0*に設定し、認証モードとして**Windows 認証**をそのまま使用します。 **[接続]** をクリックして続行します。

    ![LocalDB に接続しています](real-time-web-applications-with-signalr/_static/image21.png "LocalDB に接続しています")

    *LocalDB に接続しています*
4. LocalDB インスタンスに接続したので、SignalR のバックプレーン SQL Server を表すデータベースを作成する必要があります。 これを行うには、 **[データベース]** ノードを右クリックし、 **[新しいデータベースの追加]** をクリックします。

    ![新しいデータベースの追加](real-time-web-applications-with-signalr/_static/image22.png "新しいデータベースの追加")

    *新しいデータベースの追加*
5. データベース名を*SignalR*に設定し、 **[OK]** をクリックして作成します。

    ![SignalR データベースの作成](real-time-web-applications-with-signalr/_static/image23.png "SignalR データベースの作成")

    *SignalR データベースの作成*

    > [!NOTE]
    > データベースの任意の名前を選択できます。
6. バックプレーンから更新をより効率的に受け取るには、データベースに対して Service Broker を有効にすることをお勧めします。 Service Broker は、SQL Server でのメッセージングとキューのネイティブサポートを提供します。 バックプレーンは、Service Broker なしでも動作します。 データベースを右クリックし、 **[新しいクエリ]** をクリックして、新しいクエリを開きます。

    ![新しいクエリを開く](real-time-web-applications-with-signalr/_static/image24.png "新しいクエリを開く")

    *新しいクエリを開く*
7. Service Broker が有効になっているかどうかを確認するには、**データベース**カタログビューの **\_Broker\_enabled**列に対してクエリを実行します。 最近開いたクエリウィンドウで、次のスクリプトを実行します。

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![Service Broker の状態のクエリ](real-time-web-applications-with-signalr/_static/image25.png "Service Broker の状態のクエリ")

    *Service Broker の状態のクエリ*
8. の値**が\_broker\_有効になっ**ているデータベースの列が 0&quot;&quot;場合は、次のコマンドを使用して有効にします。 **&lt;データベース&gt;** を、データベースの作成時に設定した名前に置き換えます (例: SignalR)。

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![Service Broker の有効化](real-time-web-applications-with-signalr/_static/image26.png "Service Broker の有効化")

    *Service Broker の有効化*

    > [!NOTE]
    > このクエリでデッドロックが発生した場合は、データベースに接続されているアプリケーションがないことを確認してください。

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>タスク3– SignalR アプリケーションを構成する

このタスクでは、SQL Server バックプレーンに接続するように**マニアクイズ**を構成します。 最初に**SignalR** NuGet パッケージを追加し、接続文字列をバックプレーンデータベースに設定します。

1. [**ツール** > **NuGet パッケージマネージャー**] から**パッケージマネージャーコンソール**を開きます。 **[既定のプロジェクト]** ドロップダウンリストで **[GeekQuiz]** プロジェクト が選択されていることを確認します。 次のコマンドを入力して、 **SignalR** NuGet パッケージをインストールします。

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. 前の手順を繰り返しますが、今度は project **GeekQuiz2**を実行します。
3. SQL Server バックプレーンを構成するには、 **GeekQuiz**プロジェクトの**Startup.cs**ファイルを開き、次のコードを**configure**メソッドに追加します。 **&lt;データベース&gt;** を、SQL Server バックプレーンの作成時に使用したデータベース名に置き換えます。 **GeekQuiz2**プロジェクトに対してこの手順を繰り返します。

    (コードスニペット- *Realtimesignalr-Ex2-StartupConfiguration*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. 両方のプロジェクトが SQL Server バックプレーンを使用するように構成されたので、 **F5**キーを押してそれらを同時に実行します。
5. ここでも、 **Visual Studio**は異なるポートで**マニアクイズ**の2つのインスタンスを起動します。 画面の右側にあるいずれかのブラウザーをピン留めし、資格情報でログインします。 左側の [トリビア] ページをそのままにして、適切なブラウザーの**Statistics**ページインに移動します。
6. 左側のブラウザーで質問への回答を開始します。 今回は、バックプレーンによって**統計**ページが更新されます。 アプリケーションを切り替えます (**統計**は左側にあり、**トリビア**が右側にあります)。テストを繰り返して、両方のインスタンスで動作していることを検証します。 バックプレーンは、接続されている各サーバーのメッセージの*共有キャッシュ*として機能し、各サーバーは、接続されたクライアントに配布するために独自のローカルキャッシュにメッセージを格納します。
7. Visual Studio に戻り、デバッグを停止します。
8. SQL Server バックプレーンコンポーネントは、指定されたデータベースに必要なテーブルを自動的に生成します。 **SQL Server オブジェクトエクスプローラー**パネルで、バックプレーン用に作成したデータベース (例: SignalR) を開き、そのテーブルを展開します。 次のテーブルが表示されます。

    ![バックプレーンが生成したテーブル](real-time-web-applications-with-signalr/_static/image27.png)

    *バックプレーンが生成したテーブル*
9. **SignalR\_0**テーブルを右クリックし、[データの**表示**] を選択します。

    ![SignalR バックプレーンメッセージテーブルの表示](real-time-web-applications-with-signalr/_static/image28.png)

    *SignalR バックプレーンメッセージテーブルの表示*
10. トリビアの質問に答えると、**ハブ**に送信されたさまざまなメッセージが表示されます。 バックプレーンは、これらのメッセージを接続されている任意のインスタンスに配布します。

    ![バックプレーンメッセージテーブル](real-time-web-applications-with-signalr/_static/image29.png)

    *バックプレーンメッセージテーブル*

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、 **SignalR**をアプリケーションに追加し、**ハブ**を使用して接続されているクライアントにサーバーから通知を送信する方法を学習しました。 また、アプリケーションが複数の IIS インスタンスに配置されている場合に、*バックプレーン*コンポーネントを使用してアプリケーションをスケールアウトする方法についても学習しました。
