---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: ASP.NET MVC 4 での非同期メソッドの使用 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Web 用の Visual Studio Express 2012 (無料) を使用して、非同期の ASP.NET MVC Web アプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 15692b18fc112c4c6cce4d50a243a0e8d5fb52a4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457753"
---
# <a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>ASP.NET MVC 4 での非同期メソッドの使用

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである[web 用 Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11)を使用して、非同期 ASP.NET MVC Web アプリケーションを構築する方法の基本について説明します。 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)を使用することもできます。
> 
> このチュートリアルの完全なサンプルについては、github を[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)

[.Net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx)を組み合わせた ASP.NET MVC 4[コントローラー](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx)クラスを使用すると、 [Task&lt;actionresult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx)型のオブジェクトを返す非同期アクションメソッドを記述できます。 .NET Framework 4 では、[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)として参照される非同期プログラミングの概念が導入され、ASP.NET MVC 4[がサポートされています](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)。 タスクは **、タスクの種類と**、[システム](https://msdn.microsoft.com/library/system.threading.tasks.aspx)の名前空間の関連する型によって表されます。 .NET Framework 4.5 は、前の非同期手法よりもはるかに複雑な[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)オブジェクトの操作を行う[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)および[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードを使用したこの非同期サポートに基づいています。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードは、コードの一部を非同期に待機する必要があることを示す構文の省略形です。 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードは、メソッドをタスクベースの非同期メソッドとしてマークするために使用できるヒントを表します。 **Await**、 **async**、 **Task**オブジェクトを組み合わせることにより、.net 4.5 で非同期コードを簡単に記述できるようになります。 非同期メソッドの新しいモデルは、*タスクベースの非同期パターン*(**TAP**) と呼ばれます。 このチュートリアルでは、 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)および[Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードと[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)名前空間を使用した非同期プログラミングについて、いくつかの知識があることを前提としています。

[Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードと[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワード、および[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)名前空間の使用の詳細については、次の参照情報を参照してください。

- [ホワイトペーパー: 非同期性 in .NET](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await に関する FAQ](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio の非同期プログラミング](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>スレッドプールによる要求の処理方法

Web サーバーでは、.NET Framework は ASP.NET 要求を処理するために使用されるスレッドのプールを保持します。 要求が到着すると、その要求を処理するためにプールのスレッドがディスパッチされます。 要求が同期的に処理される場合、要求の処理中に要求を処理するスレッドがビジー状態になり、そのスレッドは別の要求にサービスを実行できません。   
  
スレッドプールは多くのビジー状態のスレッドに対応できる大きさになる可能性があるため、これは問題にはなりません。 ただし、スレッドプール内のスレッドの数は制限されています (.NET 4.5 の既定の最大値は 5000)。 実行時間の長い要求の同時実行性が高い大規模なアプリケーションでは、使用可能なすべてのスレッドがビジー状態になる可能性があります。 この状態をスレッドの不足と呼びます。 この条件に達すると、web サーバーが要求をキューに置いています。 要求キューがいっぱいになると、web サーバーは HTTP 503 状態 (サーバーがビジー状態) の要求を拒否します。 CLR スレッドプールには、新しいスレッドインジェクションに関する制限があります。 同時実行がバースト (web サイトで大量の要求が発生する可能性があります)、待機時間の長いバックエンド呼び出しによって使用可能なすべての要求スレッドがビジー状態である場合、スレッドの挿入率が制限されると、アプリケーションの応答が非常に悪くなります。 さらに、スレッドプールに追加された各新しいスレッドには、オーバーヘッド (1 MB のスタックメモリなど) があります。 同期メソッドを使用して待機時間の長い呼び出しを処理する web アプリケーションで、スレッドプールが .NET 4.5 の既定の最大値である5に達すると、アプリケーションでは、サービスが同じ要求を使用する場合よりも約 5 GB のメモリを消費します。非同期メソッドと50スレッドのみ。 非同期処理を実行している場合は、常にスレッドを使用するとは限りません。 たとえば、非同期 web サービス要求を行う場合、ASP.NET は、**非同期**のメソッド呼び出しと**await**の間でスレッドを使用しません。 待機時間の長い要求を処理するためにスレッドプールを使用すると、メモリフットプリントが大きくなり、サーバーハードウェアの使用率が低下する可能性があります。

## <a name="processing-asynchronous-requests"></a>非同期要求の処理

起動時に大量の要求が同時に表示されたり、バースト負荷がある web アプリでは、web サービス呼び出しを非同期にすると、アプリの応答性が向上します。 非同期要求の処理にかかる時間は同期要求の場合と同じです。 要求によって web サービスの呼び出しが完了するまでに2秒かかる場合、同期または非同期のどちらで実行されるかにかかわらず、要求は2秒かかります。 ただし、非同期呼び出しでは、最初の要求が完了するまで待機している間、スレッドは他の要求への応答をブロックされません。 そのため、長時間実行される操作を呼び出す多数の同時要求がある場合、非同期要求によって要求キューとスレッドプールの拡張を防ぐことができます。

## <a id="ChoosingSyncVasync"></a>同期または非同期のアクションメソッドの選択

ここでは、同期と非同期のアクション メソッドの使い分けに関するガイドラインを示します。 これはガイドラインです。各アプリケーションを個別に調べて、非同期メソッドがパフォーマンスにどのように役立つかを判断します。

一般に、次の条件に同期メソッドを使用します。

- 操作が単純であるか短時間で完了する。
- 効率よりも単純化の方が重要である。
- 操作が、膨大なディスクを使用する、またはネットワーク オーバーヘッドが生じる操作ではなく、主に CPU 操作である。 CPU バインド操作で非同期アクション メソッドを使用しても利点はなく、オーバーヘッドが大きくなります。

一般に、次のような状況では非同期メソッドを使用します。

- 非同期メソッドで使用できるサービスを呼び出していますが、.NET 4.5 以上を使用しています。
- 操作が CPU バインドではなくネットワーク バインドまたは I/O バインドである。
- コードの単純化よりも並列化の方が重要である。
- ユーザーが実行に時間のかかる要求を取り消すことができる機構を用意する必要がある。
- スレッドを切り替える利点がコンテキストスイッチのコストを上回る場合。 通常、同期メソッドが処理を行わずに ASP.NET request スレッドで待機する場合は、メソッドを非同期にする必要があります。 呼び出しを非同期にすると、web サービス要求の完了を待機している間に、ASP.NET request スレッドが処理を停止することはありません。
- テストでは、ブロッキング操作がサイトのパフォーマンスのボトルネックになっていること、および IIS がこれらのブロッキング呼び出しの非同期メソッドを使用してより多くの要求を処理できることが示されています。

ダウンロード可能なサンプルに、非同期アクション メソッドを効果的に使用する方法を示します。 このサンプルは、.NET 4.5 を使用して、ASP.NET MVC 4 での非同期プログラミングの簡単なデモを提供するように設計されています。 このサンプルは、ASP.NET MVC で非同期プログラミングを行うための参照アーキテクチャではありません。 サンプルプログラムは、 [ASP.NET Web API](../../../web-api/index.md)メソッドを呼び出します。このメソッドは、実行時間の長い Web サービス呼び出しをシミュレートします[。](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) ほとんどの運用アプリケーションでは、非同期アクションメソッドを使用するという明らかな利点はありません。   
  
すべてのアクション メソッドを非同期にする必要があるアプリケーションはほとんどありません。 多くの場合、少数の同期アクション メソッドを非同期メソッドに変換すると、必要な作業量に最適な効率向上が実現します。

## <a id="SampleApp"></a>サンプルアプリケーション

サンプルアプリケーションは、 [GitHub](https://github.com/)サイトの[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET)からダウンロードできます。 リポジトリは、次の3つのプロジェクトで構成されます。

- *Mvc4Async*: このチュートリアルで使用されているコードを含む ASP.NET MVC 4 プロジェクト。 これにより、Web API 呼び出しが**Webapipgw**サービスに対して行われます。
- *Webapipgw*: `Products, Gizmos and Widgets` コントローラーを実装する ASP.NET MVC 4 Web API プロジェクト。 *WebAppAsync*プロジェクトと*Mvc4Async*プロジェクトのデータを提供します。
- *WebAppAsync*: 別のチュートリアルで使用されている ASP.NET Web フォームプロジェクト。

## <a id="GizmosSynch"></a>ギズモ同期アクションメソッド

 次のコードは、ギズモの一覧を表示するために使用される `Gizmos` 同期アクションメソッドを示しています。 (この記事では、gizmo は架空の機械デバイスです)。 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

次のコードは、gizmo サービスの `GetGizmos` メソッドを示しています。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos` メソッドは、ギズモデータの一覧を返す ASP.NET Web API HTTP サービスに URI を渡します。 *Webapipgw*プロジェクトには、Web API `gizmos, widget` および `product` コントローラーの実装が含まれています。  
次の図は、サンプルプロジェクトのギズモビューを示しています。

![ギズモ](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>非同期ギズモアクションメソッドの作成

このサンプルでは、新しい[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードと[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワード (.Net 4.5 および Visual Studio 2012 で利用可能) を使用して、非同期プログラミングに必要な複雑な変換をコンパイラが管理できるようにします。 コンパイラでは、 C#同期制御フロー構造を使用してコードを記述できます。また、コンパイラは、ブロックしているスレッドを回避するために、コールバックを使用するために必要な変換を自動的に適用します。

次のコードは、`Gizmos` 同期メソッドと `GizmosAsync` 非同期メソッドを示しています。 ブラウザーが[HTML 5 の `<mark>` 要素](http://www.w3.org/wiki/HTML/Elements/mark)をサポートしている場合は、`GizmosAsync` の変更が黄色の強調表示で表示されます。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 `GizmosAsync` を非同期にできるようにするために、次の変更が適用されました。

- メソッドは[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードでマークされます。これは、本文の一部に対するコールバックを生成し、返される `Task<ActionResult>` を自動的に作成するようにコンパイラに指示します。
- &quot;Async&quot; がメソッド名に追加されました。 "Async" を追加する必要はありませんが、非同期メソッドを記述する場合の規則です。
- 戻り値の型が `ActionResult` から `Task<ActionResult>`に変更されました。 `Task<ActionResult>` の戻り値の型は、進行中の作業を表し、メソッドの呼び出し元に、非同期操作の完了を待機するハンドルを提供します。 この場合、呼び出し元は web サービスです。 `Task<ActionResult>` は、の結果で進行中の作業を表し `ActionResult.`
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードが web サービス呼び出しに適用されました。
- 非同期 web サービス API が呼び出されました (`GetGizmosAsync`)。

`GetGizmosAsync` メソッドの本体内部では、別の非同期メソッド `GetGizmosAsync` が呼び出されます。 `GetGizmosAsync` は、データが使用可能になったときに最終的に完了する `Task<List<Gizmo>>` を直ちに返します。 Gizmo データが取得されるまで他の操作を行わないようにするため、コードは ( **await**キーワードを使用して) タスクを待機します。 **Await**キーワードは、 **async**キーワードで注釈が付けられたメソッドでのみ使用できます。

**Await**キーワードは、タスクが完了するまでスレッドをブロックしません。 メソッドの残りの部分をタスクのコールバックとして登録し、すぐに制御を戻します。 待機中のタスクが最終的に完了すると、そのコールバックが呼び出され、中断した場所からメソッドの実行が再開されます。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードと[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワード、および[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)名前空間の使用の詳細については、「[非同期参照](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)」を参照してください。

次のコードは、`GetGizmos` メソッドと `GetGizmosAsync` メソッドを示します。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 非同期の変更は、上記の**GizmosAsync**に対して行われた変更に似ています。 

- メソッドシグネチャに[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードで注釈が付けられ、戻り値の型が `Task<List<Gizmo>>`に変更され、 *async*がメソッド名に追加されました。
- [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx)クラスの代わりに、非同期の[httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)クラスが使用されます。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードが[httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)非同期メソッドに適用されました。

次の図は、非同期 gizmo ビューを示しています。

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

ギズモデータのブラウザーの表示は、同期呼び出しによって作成されたビューと同じです。 唯一の違いは、高い負荷では、非同期バージョンの方がパフォーマンスが向上することです。

## <a id="Parallel"></a>複数の操作を並行して実行する

非同期アクションメソッドは、アクションが複数の独立した操作を実行する必要がある場合に、同期メソッドよりも大きな利点があります。 提供されているサンプルでは、同期メソッド `PWG`(Products、ウィジェット、およびギズモ) が、製品、ウィジェット、およびギズモの一覧を取得するために、3つの web サービス呼び出しの結果を表示します。 これらのサービスを提供する[ASP.NET Web API](../../../web-api/index.md)プロジェクトでは、遅延または低速のネットワーク呼び出しをシミュレートするためにタスクを使用[します。](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 遅延が500ミリ秒に設定されている場合、同期 `PWG` のバージョンは1500ミリ秒を超えているのに対して、非同期の `PWGasync` メソッドの完了には、約500ミリ秒かかります。 同期 `PWG` メソッドを次のコードに示します。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

非同期 `PWGasync` メソッドを次のコードに示します。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

次の図は、 **PWGasync**メソッドから返されるビューを示しています。

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>キャンセルトークンの使用

`Task<ActionResult>`を返す非同期アクションメソッドはキャンセル可能です。これは、 [Asynctimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx)属性が指定されている場合に[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)パラメーターを受け取ります。 次のコードは、タイムアウトが150ミリ秒の `GizmosCancelAsync` メソッドを示しています。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

次のコードは、 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)パラメーターを受け取る GetGizmosAsync オーバーロードを示しています。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

提供されているサンプルアプリケーションで、[*キャンセルトークンのデモ*] リンクを選択すると、`GizmosCancelAsync` メソッドが呼び出され、非同期呼び出しのキャンセルが示されます。

## <a id="ServerConfig"></a>高い同時実行性と高待機時間の Web サービス呼び出しのためのサーバー構成

非同期 web アプリケーションの利点を実現するには、既定のサーバー構成にいくつかの変更を加える必要がある場合があります。 非同期 web アプリケーションを構成し、ストレステストを行う場合は、次の点に注意してください。

- Windows 7、Windows Vista、およびすべての Windows クライアントオペレーティングシステムには、最大10個の同時要求があります。 高負荷の下で非同期メソッドの利点を確認するには、Windows Server オペレーティングシステムが必要です。
- 管理者特権のコマンドプロンプトから .NET 4.5 を IIS に登録します。  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_iis 登録ツール  
  「 [ASP.NET IIS Registration Tool (Aspnet\_iis 登録ツール)](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 」を参照してください。
- [Http.sys キューの](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)制限を既定値の1000から5000に増やすことが必要になる場合があります。 設定が低すぎる場合は、http 503 状態の[http.sys 拒否要求](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)が表示されることがあります。 Http.sys キューの制限を変更するには、次のようにします。

    - IIS マネージャーを開き、[アプリケーションプール] ウィンドウに移動します。
    - ターゲットアプリケーションプールを右クリックし、 **[詳細設定]** を選択します。  
        ![詳細](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - **[詳細設定**] ダイアログボックスで、*キューの長さ*を1000から5000に変更します。  
        ![キューの長さ](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  上の図では、アプリケーションプールで .NET 4.5 を使用している場合でも、.NET framework は v4.0 として表示されています。 この違いを理解するには、次を参照してください。

    - [.Net のバージョン管理とマルチターゲット化-.net 4.5 は、.NET 4.0 へのインプレースアップグレードです。](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [IIS アプリケーションまたは AppPool が2.0 ではなく ASP.NET 3.5 を使用するように設定する方法](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework のバージョンおよび依存関係](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- アプリケーションが web サービスまたは System.NET を使用して HTTP 経由でバックエンドと通信している場合は、 [Connectionmanagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx)要素を増やす必要がある場合があります。 ASP.NET アプリケーションでは、これは自動 autoConfig 機能によって Cpu の12倍の数に制限されています。 つまり、クワッドプロセスでは、最大 12 \* 4 = 48 の IP エンドポイントへの同時接続を持つことができます。 これは[autoConfig](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)に関連付けられているため、ASP.NET アプリケーションで `maxconnection` を増やす最も簡単な方法は、 *global.asax*ファイルの from `Application_Start` メソッドで、プログラムによって[System .net. servicepointmanager](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx)を設定することです。 例については、サンプルダウンロードを参照してください。
- .NET 4.5 では、 [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)の既定値である5000が正常である必要があります。
