---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: ASP.NET 4.5 | での非同期メソッドの使用Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Web 用 Visual Studio Express 2012 を使用して非同期の ASP.NET Web フォームアプリケーションを構築する方法の基本について説明します。これは無料です...
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 7abc3d7acc60d7d868958f2a313bc408f96c95a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507166"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>ASP.NET 4.5 での非同期メソッドの使用

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである[web 用 Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11)を使用して、非同期の ASP.NET Web フォームアプリケーションを構築する方法の基本について説明します。 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)を使用することもできます。 このチュートリアルでは、次のセクションについて説明します。
> 
> - [スレッドプールによる要求の処理方法](#HowRequestsProcessedByTP)
> - [同期メソッドまたは非同期メソッドの選択](#ChoosingSyncVasync)
> - [サンプルアプリケーション](#SampleApp)
> - [ギズモ同期ページ](#GizmosSynch)
> - [非同期のギズモページの作成](#CreatingAsynchGizmos)
> - [複数の操作を並行して実行する](#Parallel)
> - [キャンセルトークンの使用](#CancelToken)
> - [高い同時実行性と高待機時間の Web サービス呼び出しのためのサーバー構成](#ServerConfig)
> 
> このチュートリアルの完全なサンプルについては、「」をご覧ください。  
> [GitHub](https://github.com/)サイトで[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)します。

[.Net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx)を組み合わせた ASP.NET 4.5 Web ページを使用すると、 [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)型のオブジェクトを返す非同期メソッドを登録できます。 .NET Framework 4 では、[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)として参照される非同期プログラミングの概念が導入され、ASP.NET 4.5 では[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)がサポートされています。 タスクは **、タスクの種類と**、[システム](https://msdn.microsoft.com/library/system.threading.tasks.aspx)の名前空間の関連する型によって表されます。 .NET Framework 4.5 は、前の非同期手法よりもはるかに複雑な[タスク](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)オブジェクトの操作を行う[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)および[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードを使用したこの非同期サポートに基づいています。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードは、コードの一部を非同期に待機する必要があることを示す構文の省略形です。 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードは、メソッドをタスクベースの非同期メソッドとしてマークするために使用できるヒントを表します。 **Await**、 **async**、 **Task**オブジェクトを組み合わせることにより、.net 4.5 で非同期コードを簡単に記述できるようになります。 非同期メソッドの新しいモデルは、*タスクベースの非同期パターン*(**TAP**) と呼ばれます。 このチュートリアルでは、 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)および[Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードと[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)名前空間を使用した非同期プログラミングについて、いくつかの知識があることを前提としています。

[Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードと[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワード、および[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)名前空間の使用の詳細については、次の参照情報を参照してください。

- [ホワイトペーパー: 非同期性 in .NET](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await に関する FAQ](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio の非同期プログラミング](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>スレッドプールによる要求の処理方法

Web サーバーでは、.NET Framework は ASP.NET 要求を処理するために使用されるスレッドのプールを保持します。 要求が到着すると、その要求を処理するためにプールのスレッドがディスパッチされます。 要求が同期的に処理される場合、要求の処理中に要求を処理するスレッドがビジー状態になり、そのスレッドは別の要求にサービスを実行できません。   
  
スレッドプールは多くのビジー状態のスレッドに対応できる大きさになる可能性があるため、これは問題にはなりません。 ただし、スレッドプール内のスレッドの数は制限されています (.NET 4.5 の既定の最大値は 5000)。 実行時間の長い要求の同時実行性が高い大規模なアプリケーションでは、使用可能なすべてのスレッドがビジー状態になる可能性があります。 この状態をスレッドの不足と呼びます。 この条件に達すると、web サーバーが要求をキューに置いています。 要求キューがいっぱいになると、web サーバーは HTTP 503 状態 (サーバーがビジー状態) の要求を拒否します。 CLR スレッドプールには、新しいスレッドインジェクションに関する制限があります。 同時実行がバースト (web サイトで大量の要求が発生する可能性があります)、待機時間の長いバックエンド呼び出しによって使用可能なすべての要求スレッドがビジー状態である場合、スレッドの挿入率が制限されると、アプリケーションの応答が非常に悪くなります。 さらに、スレッドプールに追加された各新しいスレッドには、オーバーヘッド (1 MB のスタックメモリなど) があります。 同期メソッドを使用して待機時間の長い呼び出しを処理する web アプリケーションで、スレッドプールが .NET 4.5 の既定の最大値である5に達すると、アプリケーションでは、サービスが同じ要求を使用する場合よりも約 5 GB のメモリを消費します。非同期メソッドと50スレッドのみ。 非同期処理を実行している場合は、常にスレッドを使用するとは限りません。 たとえば、非同期 web サービス要求を行う場合、ASP.NET は、**非同期**のメソッド呼び出しと**await**の間でスレッドを使用しません。 待機時間の長い要求を処理するためにスレッドプールを使用すると、メモリフットプリントが大きくなり、サーバーハードウェアの使用率が低下する可能性があります。

## <a name="processing-asynchronous-requests"></a>非同期要求の処理

起動時に大量の要求が同時に表示されたり、バースト負荷が発生したりする web アプリケーションでは、web サービスの呼び出しが非同期になるため、アプリケーションの応答性が向上します。 非同期要求の処理にかかる時間は同期要求の場合と同じです。 たとえば、要求によって web サービス呼び出しの完了に2秒を要する場合、同期または非同期のどちらで実行されるかにかかわらず、要求は2秒かかります。 ただし、非同期呼び出しでは、最初の要求が完了するまで待機している間、スレッドは他の要求への応答をブロックされません。 そのため、長時間実行される操作を呼び出す多数の同時要求がある場合、非同期要求によって要求キューとスレッドプールの拡張を防ぐことができます。

## <a id="ChoosingSyncVasync"></a>同期メソッドまたは非同期メソッドの選択

ここでは、同期または非同期のメソッドを使用する場合のガイドラインを示します。 これはガイドラインです。各アプリケーションを個別に調べて、非同期メソッドがパフォーマンスにどのように役立つかを判断します。

一般に、次の条件に同期メソッドを使用します。

- 操作が単純であるか短時間で完了する。
- 効率よりも単純化の方が重要である。
- 操作が、膨大なディスクを使用する、またはネットワーク オーバーヘッドが生じる操作ではなく、主に CPU 操作である。 CPU バインド操作で非同期メソッドを使用すると、利点はなく、オーバーヘッドが大きくなります。

一般に、次のような状況では非同期メソッドを使用します。

- 非同期メソッドで使用できるサービスを呼び出していますが、.NET 4.5 以上を使用しています。
- 操作が CPU バインドではなくネットワーク バインドまたは I/O バインドである。
- コードの単純化よりも並列化の方が重要である。
- ユーザーが実行に時間のかかる要求を取り消すことができる機構を用意する必要がある。
- スレッドを切り替える利点がコンテキストスイッチのコストを上回る場合。 一般に、同期メソッドが作業を行わずに ASP.NET request スレッドをブロックする場合は、メソッドを非同期にする必要があります。 呼び出しを非同期にすると、web サービス要求の完了を待機している間、ASP.NET request スレッドは動作しなくなります。
- テストでは、ブロッキング操作がサイトのパフォーマンスのボトルネックになっていること、および IIS がこれらのブロッキング呼び出しの非同期メソッドを使用してより多くの要求を処理できることが示されています。

  ダウンロード可能なサンプルは、非同期メソッドを効果的に使用する方法を示しています。 このサンプルは、ASP.NET 4.5 での非同期プログラミングの簡単なデモを提供するように設計されています。 このサンプルは、ASP.NET で非同期プログラミングを行うための参照アーキテクチャではありません。 サンプルプログラムは、 [ASP.NET Web API](../../../web-api/index.md)メソッドを呼び出します。このメソッドは、実行時間の長い Web サービス呼び出しをシミュレートします[。](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) ほとんどの運用アプリケーションでは、非同期メソッドを使用するための明らかな利点は示されません。   
  
一部のアプリケーションでは、すべてのメソッドを非同期にする必要があります。 多くの場合、いくつかの同期メソッドを非同期メソッドに変換することで、必要な作業量の効率を最大限に高めることができます。

## <a id="SampleApp"></a>サンプルアプリケーション

サンプルアプリケーションは、 [GitHub](https://github.com/)サイトの[https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET)からダウンロードできます。 リポジトリは、次の3つのプロジェクトで構成されます。

- *WebAppAsync*: Web API **WebAPIpwg**サービスを使用する ASP.NET web フォームプロジェクト。 このチュートリアルのコードの大部分は、このプロジェクトからのものです。
- *Webapipgw*: `Products, Gizmos and Widgets` コントローラーを実装する ASP.NET MVC 4 Web API プロジェクト。 *WebAppAsync*プロジェクトと*Mvc4Async*プロジェクトのデータを提供します。
- *Mvc4Async*: 別のチュートリアルで使用されているコードを含む ASP.NET MVC 4 プロジェクト。 これにより、 **WebAPIpwg**サービスに対する Web API 呼び出しが行われます。

## <a id="GizmosSynch"></a>ギズモ同期ページ

 次のコードは、ギズモの一覧を表示するために使用される `Page_Load` 同期メソッドを示しています。 (この記事では、gizmo は架空の機械デバイスです)。 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

次のコードは、gizmo サービスの `GetGizmos` メソッドを示しています。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

`GizmoService GetGizmos` メソッドは、ギズモデータの一覧を返す ASP.NET Web API HTTP サービスに URI を渡します。 *Webapipgw*プロジェクトには、Web API `gizmos, widget` および `product` コントローラーの実装が含まれています。  
次の図は、サンプルプロジェクトのギズモページを示しています。

![ギズモ](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>非同期のギズモページの作成

このサンプルでは、新しい[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードと[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワード (.Net 4.5 および Visual Studio 2012 で利用可能) を使用して、非同期プログラミングに必要な複雑な変換をコンパイラが管理できるようにします。 コンパイラでは、 C#同期制御フロー構造を使用してコードを記述できます。また、コンパイラは、ブロックしているスレッドを回避するために、コールバックを使用するために必要な変換を自動的に適用します。

ASP.NET 非同期ページには、`Async` 属性が "true" に設定された[ページ](https://msdn.microsoft.com/library/ydy4x04a.aspx)ディレクティブが含まれている必要があります。 次のコードは、 *GizmosAsync*ページの `Async` 属性が "true" に設定された[Page](https://msdn.microsoft.com/library/ydy4x04a.aspx)ディレクティブを示しています。

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

次のコードは、同期 `Page_Load` メソッド `Gizmos` と `GizmosAsync` 非同期ページを示しています。 ブラウザーが[HTML 5 &lt;mark&gt; 要素](http://www.w3.org/wiki/HTML/Elements/mark)をサポートしている場合は、黄色の強調表示で `GizmosAsync` に変更が表示されます。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

非同期バージョン:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 `GizmosAsync` ページを非同期にできるように、次の変更が適用されました。

- [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx)ディレクティブには、`Async` 属性を "true" に設定する必要があります。
- `RegisterAsyncTask` メソッドは、非同期的に実行されるコードを含む非同期タスクを登録するために使用されます。
- 新しい `GetGizmosSvcAsync` メソッドは[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードでマークされます。これにより、コンパイラは、本文の一部に対するコールバックを生成し、返された `Task` を自動的に作成するように指示します。
- 非同期&quot; &quot;非同期メソッド名に追加されました。 "Async" を追加する必要はありませんが、非同期メソッドを記述する場合の規則です。
- 新しい `GetGizmosSvcAsync` メソッドの戻り値の型は `Task`です。 `Task` の戻り値の型は、進行中の作業を表し、メソッドの呼び出し元に、非同期操作の完了を待機するハンドルを提供します。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードが web サービス呼び出しに適用されました。
- 非同期 web サービス API が呼び出されました (`GetGizmosAsync`)。

`GetGizmosSvcAsync` メソッドの本体内部では、別の非同期メソッド `GetGizmosAsync` が呼び出されます。 `GetGizmosAsync` は、データが使用可能になったときに最終的に完了する `Task<List<Gizmo>>` を直ちに返します。 Gizmo データが取得されるまで他の操作を行わないようにするため、コードは ( **await**キーワードを使用して) タスクを待機します。 **Await**キーワードは、 **async**キーワードで注釈が付けられたメソッドでのみ使用できます。

**Await**キーワードは、タスクが完了するまでスレッドをブロックしません。 メソッドの残りの部分をタスクのコールバックとして登録し、すぐに制御を戻します。 待機中のタスクが最終的に完了すると、そのコールバックが呼び出され、中断した場所からメソッドの実行が再開されます。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードと[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワード、および[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)名前空間の使用の詳細については、「[非同期参照](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)」を参照してください。

次のコードは、`GetGizmos` メソッドと `GetGizmosAsync` メソッドを示します。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 非同期の変更は、上記の**GizmosAsync**に対して行われた変更に似ています。 

- メソッドシグネチャに[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)キーワードで注釈が付けられ、戻り値の型が `Task<List<Gizmo>>`に変更され、 *async*がメソッド名に追加されました。
- 非同期[Httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)クラスは、同期[WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx)クラスの代わりに使用されます。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)キーワードが[httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx)の非同期メソッドに適用されました。

次の図は、非同期 gizmo ビューを示しています。

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

ギズモデータのブラウザーの表示は、同期呼び出しによって作成されたビューと同じです。 唯一の違いは、高い負荷では、非同期バージョンの方がパフォーマンスが向上することです。

## <a name="registerasynctask-notes"></a>RegisterAsyncTask メモ

`RegisterAsyncTask` とフックされたメソッドは、 [PreRender](https://msdn.microsoft.com/library/ms178472.aspx)の直後に実行されます。 次のコードに示すように、非同期の void ページイベントを直接使用することもできます。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

非同期 void イベントの欠点は、イベントの実行時に開発者が完全に制御できなくなることです。 たとえば、.aspx との両方の場合です。マスター定義 `Page_Load` イベントと、それらの一方または両方が非同期であるため、実行の順序を保証できません。 非イベントハンドラー (`async void Button_Click` など) に対して同じ indeterminiate 順序が適用されます。 ほとんどの開発者にとって、これは許容されますが、実行順序を完全に制御する必要があるユーザーは、タスクオブジェクトを返すメソッドを使用する `RegisterAsyncTask` のような Api のみを使用する必要があります。

## <a id="Parallel"></a>複数の操作を並行して実行する

非同期メソッドは、アクションが複数の独立した操作を実行する必要がある場合に、同期メソッドよりも大きな利点があります。 提供されているサンプルでは、同期ページ*PWG*(Products、ウィジェット、およびギズモの場合) は、3つの web サービス呼び出しの結果を表示して、製品、ウィジェット、およびギズモの一覧を取得します。 これらのサービスを提供する[ASP.NET Web API](../../../web-api/index.md)プロジェクトでは、遅延または低速のネットワーク呼び出しをシミュレートするためにタスクを使用[します。](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 遅延が500ミリ秒に設定されている場合、非同期の*PWGasync*ページは完了するまでに約500ミリ秒かかりますが、同期 `PWG` バージョンには1500ミリ秒かかります。 同期*PWG*ページを次のコードに示します。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

非同期 `PWGasync` コードを次に示します。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

次の図は、非同期の*PWGasync*ページから返されるビューを示しています。

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a id="CancelToken"></a>キャンセルトークンの使用

`Task`を返す非同期メソッドはキャンセル可能です。これは、 [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx)ディレクティブの `AsyncTimeout` 属性が指定されている場合に、 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)パラメーターを受け取ります。 次のコードは、タイムアウトが秒の*GizmosCancelAsync*ページを示しています。

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

次のコードは、 *GizmosCancelAsync.aspx.cs*ファイルを示しています。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

提供されているサンプルアプリケーションで、 *GizmosCancelAsync*リンクを選択すると、 *GizmosCancelAsync*ページが呼び出され、非同期呼び出しのキャンセル (タイムアウトによる) が示されます。 遅延時間はランダムな範囲内であるため、タイムアウトエラーメッセージを表示するには、2回ページを更新する必要がある場合があります。

## <a id="ServerConfig"></a>高い同時実行性と高待機時間の Web サービス呼び出しのためのサーバー構成

非同期 web アプリケーションの利点を実現するには、既定のサーバー構成にいくつかの変更を加える必要がある場合があります。 非同期 web アプリケーションを構成し、ストレステストを行う場合は、次の点に注意してください。

- Windows 7、Windows Vista、ウィンドウ8、およびすべての Windows クライアントオペレーティングシステムには、最大10個の同時要求があります。 高負荷の下で非同期メソッドの利点を確認するには、Windows Server オペレーティングシステムが必要です。
- 次のコマンドを使用して、管理者特権でのコマンドプロンプトから .NET 4.5 を IIS に登録します。  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet\_iis 登録ツール-i  
  「 [ASP.NET IIS Registration Tool (Aspnet\_iis 登録ツール)](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 」を参照してください。
- [Http.sys キューの](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)制限を既定値の1000から5000に増やすことが必要になる場合があります。 設定が低すぎる場合は、http 503 状態の[http.sys 拒否要求](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)が表示されることがあります。 Http.sys キューの制限を変更するには、次のようにします。

    - IIS マネージャーを開き、[アプリケーションプール] ウィンドウに移動します。
    - ターゲットアプリケーションプールを右クリックし、 **[詳細設定]** を選択します。  
        ![詳細](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - **[詳細設定**] ダイアログボックスで、*キューの長さ*を1000から5000に変更します。  
        ![キューの長さ](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  上の図では、アプリケーションプールで .NET 4.5 を使用している場合でも、.NET framework は v4.0 として表示されています。 この違いを理解するには、次を参照してください。

- [.Net のバージョン管理とマルチターゲット化-.net 4.5 は、.NET 4.0 へのインプレースアップグレードです。](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [IIS アプリケーションまたは AppPool が2.0 ではなく ASP.NET 3.5 を使用するように設定する方法](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [.NET Framework のバージョンおよび依存関係](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- アプリケーションが web サービスまたは System.NET を使用して HTTP 経由でバックエンドと通信している場合は、 [Connectionmanagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx)要素を増やす必要がある場合があります。 ASP.NET アプリケーションでは、これは自動 autoConfig 機能によって Cpu の12倍の数に制限されています。 つまり、クワッドプロセスでは、最大 12 \* 4 = 48 の IP エンドポイントへの同時接続を持つことができます。 これは[autoConfig](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)に関連付けられているため、ASP.NET アプリケーションで `maxconnection` を増やす最も簡単な方法は、 *global.asax*ファイルの from `Application_Start` メソッドで、プログラムによって[System .net. servicepointmanager](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx)を設定することです。 例については、サンプルダウンロードを参照してください。
- .NET 4.5 では、 [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)の既定値である5000が正常である必要があります。

## <a name="contributors"></a>共同作成者

- [Levi Broderick](http://stackoverflow.com/users/59641/levi)
- [Tom Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Brad Wilson](http://bradwilson.typepad.com/)
- [HongMei Ge](https://blogs.msdn.com/b/hongmeig/)
