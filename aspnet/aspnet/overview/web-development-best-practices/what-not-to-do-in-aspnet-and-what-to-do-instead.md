---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET では何が行われず、代わりに何をするかを説明します。Microsoft Docs
author: Rick-Anderson
description: このトピックでは、ASP.NET web プロジェクト内での複数のよくある間違いについて説明します。 ここでは、これらの処理を回避するための推奨事項について説明します。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500134"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>ASP.NET では行わないことと、その代わりに行うこと

> このトピックでは、ASP.NET web プロジェクト内での複数のよくある間違いについて説明します。 これらの一般的な誤りを回避するための推奨事項について説明します。 これは、ノルウェーの開発者のカンファレンスで**Damian Edwards**による[プレゼンテーション](http://vimeo.com/68390507)に基づいています。

## <a name="disclaimer"></a>免責事項

このトピックは、アプリケーションの安全性と効率性を確保するための完全なガイドではありません。 このトピックでは説明されていないセキュリティとパフォーマンスについては、ベストプラクティスに従う必要があります。 .NET のクラスとプロセスに関連する一般的な間違いを回避する方法についてのみ説明します。

## <a name="overview"></a>概要

このトピックには、次のセクションが含まれます。

- [標準への準拠](#standards)

    - [コントロールアダプター](#adapters)
    - [コントロールのスタイルプロパティ](#styleprop)
    - [ページとコントロールのコールバック](#callback)
    - [ブラウザー機能の検出](#browsercap)
- [セキュリティ](#security)

    - [要求の検証](#validation)
    - [Cookie なしのフォーム認証とセッション](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [中程度の信頼](#medium)
    - [appSettings&gt; の &lt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [信頼性とパフォーマンス](#performance)

    - [PreSendRequestHeaders と PreSendRequestContent](#presend)
    - [Web フォームを使用した非同期ページイベント](#asyncevents)
    - [起動と破棄の作業](#fire)
    - [要求エンティティ本体](#requestentity)
    - [応答。リダイレクトと応答終了](#redirect)
    - [EnableViewState と ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [実行時間の長い要求 (> 110 秒)](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>標準への準拠

<a id="adapters"></a>

### <a name="control-adapters"></a>コントロールアダプター

推奨事項: アダプティブレンダリングのためにコントロールアダプターの使用を停止し、代わりに CSS メディアクエリと標準準拠の HTML を使用します。

.NET 2.0 では、さまざまなデバイスや環境用にカスタマイズされたプレゼンテーションコードをレンダリングするために、コントロールアダプターが導入されました。 これで、このアダプティブレンダリングは CSS と HTML で実現できます。 コントロールアダプターの使用を停止し、既存のアダプターを CSS と HTML に変換する必要があります。

詳細については、「[メディアクエリ](http://www.w3.org/TR/css3-mediaqueries/)」と「[方法: モバイルページを ASP.NET WEB フォーム/MVC アプリケーションに追加](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)する」を参照してください。

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>コントロールのスタイルプロパティ

推奨事項: コントロールマークアップでのスタイル値の設定を停止します。代わりに、CSS スタイルシートで書式設定値を設定します。

Web サーバーコントロールには、インラインスタイルプロパティの設定に使用できる多数のプロパティが含まれています。 たとえば、ForeColor プロパティは、コントロールのテキストの色を設定します。 CSS スタイルシートを使用すると、これと同じ効果をより効率的に行うことができます。 スタイルシートを使用すると、スタイル値を一元化し、アプリケーション全体でこれらの値を設定しないようにすることができます。

次の例は、テキストを赤に設定する CSS クラスを示しています。

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

次の例では、CSS クラスを動的に適用する方法を示します。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>ページとコントロールのコールバック

推奨事項: ページとコントロールのコールバックの使用を停止し、代わりに、AJAX、UpdatePanel、MVC アクションメソッド、Web API、または SignalR のいずれかを使用します。

以前のバージョンの ASP.NET では、ページとコントロールのコールバックメソッドを使用して、ページ全体を更新せずに web ページの一部を更新できました。 [AJAX](../../../ajax/index.md)、 [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)、 [MVC](../../../mvc/index.md)、 [Web API](../../../web-api/index.md) 、または[SignalR](../../../signalr/index.md)を使用して部分ページ更新を実行できるようになりました。 わかりやすい Url とルーティングに関する問題が発生する可能性があるため、コールバックメソッドの使用を停止する必要があります。 既定では、コントロールはコールバックメソッドを有効にしませんが、コントロールでこの機能を有効にした場合は、無効にする必要があります。

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>ブラウザー機能の検出

推奨: 静的なブラウザー機能の検出の使用を停止し、代わりに動的な機能の検出を使用します。

以前のバージョンの ASP.NET では、各ブラウザーでサポートされている機能は、XML ファイルに格納されていました。 静的参照を使用した機能サポートの検出は、最適な方法ではありません。 これで、 [Modernizr](http://modernizr.com/)などの機能検出フレームワークを使用して、ブラウザーのサポートされている機能を動的に検出できます。 機能の検出では、メソッドまたはプロパティを使用して、ブラウザーが目的の結果を生成したかどうかを確認することによって、サポートが決定されます。 既定では、Modernizr は Web アプリケーションテンプレートに含まれています。

<a id="security"></a>

## <a name="security"></a>Security

<a id="validation"></a>

### <a name="request-validation"></a>要求の検証

推奨事項: ユーザー入力を検証し、ユーザーからの出力をエンコードします。

要求の検証は、ASP.NET の機能の1つであり、認識された脅威が見つかると、各要求を調べ、要求を停止します。 クロスサイトスクリプティング攻撃に対してアプリケーションをセキュリティで保護するための要求の検証に依存しないでください。 代わりに、ユーザーからのすべての入力を検証し、出力をエンコードします。 一部のケースでは、正規表現を使用して入力を検証できますが、より複雑なケースでは、値が許可された値と一致するかどうかを判断する .NET クラスを使用してユーザー入力を検証する必要があります。

次の例は、Uri クラスの静的メソッドを使用して、ユーザーが指定した Uri が有効かどうかを判断する方法を示しています。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

ただし、Uri を十分に検証するには、`http` または `https`が指定されていることを確認する必要もあります。 次の例では、インスタンスメソッドを使用して、Uri が有効であることを確認します。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

ユーザー入力を HTML として、または SQL クエリにユーザー入力を含めて表示する前に、その値をエンコードして、悪意のあるコードが含まれていないことを確認します。

次に示すように、&lt;%:%&gt; 構文を使用してマークアップの値を HTML エンコードできます。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

また、Razor 構文では、次に示すように、@ を使用して HTML エンコードできます。

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

次の例は、コードビハインドで値を HTML エンコードする方法を示しています。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

SQL コマンドの値を安全にエンコードするには、 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)などのコマンドパラメーターを使用します。 <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>Cookie なしのフォーム認証とセッション

推奨: cookie が必要です。

クエリ文字列で認証情報を渡すことは、セキュリティで保護されていません。 そのため、アプリケーションに認証が含まれている場合は、cookie が必要です。 Cookie に機密情報が格納されている場合は、cookie に SSL を要求することを検討してください。

次の例は、web.config ファイルでを指定する方法を示しています。フォーム認証では、SSL を使用して送信される cookie が必要です。

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

推奨: false に設定しないでください。

既定では、EnableViewStateMac は true に設定されています。 アプリケーションがビューステートを使用していない場合でも、EnableViewStateMac を false に設定しないでください。 この値を false に設定すると、アプリケーションはクロスサイトスクリプトに対して脆弱になります。

ASP.NET 4.5.2 以降では、ランタイムによって**EnableViewStateMac = true**が適用されます。 False に設定した場合でも、ランタイムはこの値を無視し、true に設定された値を使用して処理を続行します。 詳細については、「 [ASP.NET 4.5.2 And EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)」を参照してください。

次の例は、EnableViewStateMac を true に設定する方法を示しています。 この値は、既定で true に設定されているため、実際に true に設定する必要はありません。 ただし、アプリケーションの任意のページで false に設定した場合は、すぐにこの値を修正する必要があります。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>中程度の信頼

推奨: セキュリティ境界として中程度の信頼 (またはその他の信頼レベル) に依存しないでください。

部分信頼では、アプリケーションを適切に保護することはできないため、使用しないでください。 代わりに、完全信頼を使用して、信頼されていないアプリケーションを別のアプリケーションプールに分離します。 また、各アプリケーションプールを一意の id で実行します。 詳細については、「 [ASP.NET 部分信頼ではアプリケーションの分離が保証されない](https://support.microsoft.com/kb/2698981)」を参照してください。

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

推奨: &lt;appSettings&gt; 要素のセキュリティ設定を無効にしないでください。

AppSettings 要素には、セキュリティ更新プログラムに必要な多くの値が含まれています。 これらの値は変更したり無効にしたりしないでください。 更新プログラムを展開するときにこれらの値を無効にする必要がある場合は、展開の完了後すぐに再度有効にしてください。

詳細については、「 [ASP.NET AppSettings 要素](https://msdn.microsoft.com/library/hh975440.aspx)」を参照してください。

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

推奨: 代わりに[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)を使用してください。

UrlPathEncode メソッドが .NET Framework に追加され、特定のブラウザーの互換性の問題を解決します。 URL を適切にエンコードすることはできず、クロスサイトスクリプトからアプリケーションを保護することもありません。 アプリケーションでは使用しないでください。 代わりに、 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)を使用してください。

次の例は、エンコードされた URL をハイパーリンクコントロールのクエリ文字列パラメーターとして渡す方法を示しています。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>信頼性とパフォーマンス

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders と PreSendRequestContent

推奨: これらのイベントをマネージモジュールで使用しないでください。 代わりに、必要なタスクを実行するネイティブ IIS モジュールを記述します。 「[ネイティブコード HTTP モジュールの作成](https://msdn.microsoft.com/library/ms693629.aspx)」を参照してください。

ネイティブ IIS モジュールでは、 [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)および[Presendrequestcontent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)イベントを使用できます。
> [!WARNING]
> `IHttpModule`を実装するマネージモジュールで `PreSendRequestHeaders` および `PreSendRequestContent` を使用しないでください。 これらのプロパティを設定すると、非同期要求に関する問題が発生する可能性があります。 アプリケーションで要求されたルーティング (ARR) と websocket を組み合わせると、w3wp.exe がクラッシュする原因となるアクセス違反例外が発生する可能性があります。 たとえば、iiscore のようになります。Iiscore .dll の W3_CONTEXT_BASE:: GetIsLastNotification + 68 で、アクセス違反例外 (0xC0000005) が発生しました。

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>Web フォームを使用した非同期ページイベント

推奨事項: Web フォームでは、ページのライフサイクルイベントに対して非同期の void メソッドを記述しないでください。代わりに、非同期コード用に[RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)を使用します。

**Async**と**void**を使用してページイベントをマークすると、非同期コードがいつ終了したかを判断できません。 代わりに、Page. RegisterAsyncTask を使用して非同期コードを実行し、その完了を追跡できるようにします。

次の例は、非同期コードを含むボタンクリックハンドラーを示しています。 この例では、非同期タスクの簡略化された例としてのみ提供される文字列値を非同期に読み取り、推奨される方法としては使用しません。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

非同期タスクを使用している場合は、web.config ファイルで Http ランタイムターゲットフレームワークを 4.5 (またはそれ以降) に設定します。 ターゲットフレームワークを4.5 に設定すると、.NET 4.5 で追加された新しい同期コンテキストが有効になります。 この値は、Visual Studio の新しいプロジェクトで既定で設定されますが、既存のプロジェクトを操作している場合は設定されません。

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>起動と破棄の作業

推奨事項: ASP.NET 内で要求を処理する場合は、起動と破棄の作業 (QueueUserWorkItem メソッドの呼び出し、デリゲートを繰り返し呼び出すタイマーの作成など) を行わないようにしてください。

アプリケーションの ASP.NET 内で実行される作業を忘れることがある場合、アプリケーションは同期されない可能性があります。いつでも、アプリドメインを破棄できます。つまり、進行中のプロセスがアプリケーションの現在の状態と一致しなくなる可能性があります。

この種類の作業は、ASP.NET の外部で移動する必要があります。 Azure の Web ジョブ、Windows サービス、または Worker ロールを使用して、進行中の作業を実行し、別のプロセスからそのコードを実行できます。

ASP.NET 内でこの作業を実行する必要がある場合は、 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)という名前の Nuget パッケージを追加してコードを実行できます。

<a id="requestentity"></a>

### <a name="request-entity-body"></a>要求エンティティ本体

推奨事項: ハンドラーの execute イベントの前に、InputStream または要求を読み取らないようにします。

最初に、要求. フォームまたは InputStream から読み取る必要があります。 MVC では、コントローラーはハンドラーであり、アクションメソッドが実行されるときに execute イベントです。 Web フォームでは、ページはハンドラーであり、execute イベントは、ページの Init イベントが発生したときに発生します。 Execute イベントより前に要求エンティティ本体を読み取ると、要求の処理が妨げられます。

Execute イベントの前に要求エンティティ本体を読み取る必要がある場合は、 [GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)または[httprequest.getbufferedinputstream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)を使用します。 GetBufferlessInputStream を使用する場合は、要求から生のストリームを取得し、要求全体を処理する必要があると想定します。 GetBufferlessInputStream を呼び出した後、InputStream は ASP.NET によって設定されていないため、使用できません。 Httprequest.getbufferedinputstream を使用すると、要求からストリームのコピーが取得されます。 要求の形式と InputStream は、ASP.NET が他のコピーを設定するため、後で要求の中でも使用できます。

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>応答。リダイレクトと応答終了

推奨事項: Response を呼び出した後のスレッドの処理方法の違いに注意[してください。リダイレクト (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)。

[Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)メソッドは、Response. End メソッドを呼び出します。 同期プロセスでは、要求を呼び出します。リダイレクトを実行すると、現在のスレッドがすぐに中止されます。 ただし、非同期プロセスでは、Response を呼び出すと、現在のスレッドが中止されないため、要求に対してコードの実行が続行されます。 非同期プロセスでは、メソッドからタスクを返してコードの実行を停止する必要があります。

MVC プロジェクトでは、Response. Redirect を呼び出すことはできません。 代わりに、RedirectResult を返します。

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState と ViewStateMode

推奨事項: ビューステートを使用するコントロールをきめ細かく制御できるように、EnableViewState ではなく ViewStateMode を使用します。

Page ディレクティブで EnableViewState を false に設定すると、ページ内のすべてのコントロールに対してビューステートが無効になり、有効にすることはできません。 ページの特定のコントロールに対してのみビューステートを有効にする場合は、ページの ViewStateMode を Disabled に設定します。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

次に、ビューステートを実際に必要とするコントロールに対してのみ ViewStateMode を Enabled に設定します。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

必要なコントロールに対してのみビューステートを有効にすることで、web ページのビューステートのサイズを縮小できます。

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

推奨事項: ユニバーサルプロバイダーを使用します。

現在のプロジェクトテンプレートでは、SqlMembershipProvider が[ASP.NET ユニバーサルプロバイダー](http://www.nuget.org/packages/Microsoft.AspNet.Providers)に置き換えられました。これは NuGet パッケージとして利用できます。 以前のバージョンのテンプレートを使用してビルドされたプロジェクトで SqlMembershipProvider を使用している場合は、ユニバーサルプロバイダーに切り替える必要があります。 ユニバーサルプロバイダーは、Entity Framework によってサポートされているすべてのデータベースで動作します。

詳細については、「 [ASP.NET ユニバーサルプロバイダーの概要](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)」を参照してください。

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>実行時間の長い要求 (> 110 秒)

推奨事項: 接続されたクライアントに[websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)または[SignalR](../../../signalr/index.md)を使用し、非同期 i/o 操作を使用します。

実行時間の長い要求では、web アプリケーションで予期しない結果が発生し、パフォーマンスが低下する可能性があります。 要求の既定のタイムアウト設定は110秒です。 実行時間の長い要求でセッション状態を使用している場合、ASP.NET は110秒後にセッションオブジェクトのロックを解除します。 ただし、ロックが解除され、操作が正常に完了しない可能性がある場合、アプリケーションはセッションオブジェクトに対する操作の途中である可能性があります。 最初の要求の実行中にユーザーからの2番目の要求がブロックされた場合、2番目の要求では、不整合な状態にあるセッションオブジェクトにアクセスする可能性があります。

アプリケーションにブロッキング (または同期) i/o 操作が含まれている場合は、アプリケーションが応答しなくなります。

パフォーマンスを向上させるには、.NET Framework で非同期 i/o 操作を使用します。 また、Websocket または SignalR を使用して、クライアントをサーバーに接続します。 これらの機能は、実行時間の長い要求を効率的に処理するように設計されています。
