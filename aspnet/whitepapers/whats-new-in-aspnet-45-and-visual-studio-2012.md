---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 と Visual Studio 2012 における新機能 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、ASP.NET 4.5 で導入される新機能と強化された機能について説明します。 また、web 開発に加えられた機能強化についても説明します。
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422734"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 と Visual Studio 2012 における新機能

> このドキュメントでは、ASP.NET 4.5 で導入される新機能と強化された機能について説明します。 また、Visual Studio 2012 で web 開発を行う際の改善点についても説明します。 このドキュメントは、当初、2012年2月29日に発行されました。

- [ASP.NET Core ランタイムとフレームワーク](#_Toc318097372)

    - [HTTP 要求と応答の非同期的な読み取りと書き込み](#_Toc318097373)
    - [HttpRequest の処理の機能強化](#_Toc318097374)
    - [応答を非同期的にフラッシュする](#_Toc318097375)
    - [*Await*および*タスク*ベースの非同期モジュールとハンドラーのサポート](#_Toc318097376)
    - [非同期 HTTP モジュール](#_Toc318097377)
    - [非同期 HTTP ハンドラー](#_Toc318097378)
    - [新しい ASP.NET 要求の検証機能](#_Toc318097379)
    - [遅延 ("lazy") 要求の検証](#_Toc318097380)
    - [未検証要求のサポート](#_Toc318097381)
    - [アンチ Xss ライブラリ](#_Toc318097382)
    - [Websocket プロトコルのサポート](#_Toc318097383)
    - [バンドルと縮小](#_Toc318097384)
    - [Web ホスティングのパフォーマンスの向上](#_Toc_perf)

        - [主要なパフォーマンス要因](#_Toc_perf_1)
        - [新しいパフォーマンス機能の要件](#_Toc_perf_2)
        - [共通アセンブリの共有](#_Toc_perf_3)
        - [高速起動のためのマルチコア JIT コンパイルの使用](#_Toc_perf_4)
        - [メモリ用に最適化するためのガベージコレクションのチューニング](#_Toc_perf_5)
        - [Web アプリケーションのプリフェッチ](#_Toc_perf_6)
- [ASP.NET Web フォーム](#_Toc318097385)

    - [厳密に型指定されたデータ コントロール](#_Toc318097386)
    - [モデル バインド](#_Toc318097387)

        - [データの選択](#_Toc318097388)
        - [値プロバイダー](#_Toc318097389)
        - [コントロールの値によるフィルター処理](#_Toc318097390)
    - [HTML エンコードされたデータバインディング式](#_Toc318097391)
    - [控えめに検証](#_Toc318097392)
    - [HTML5 の更新プログラム](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET Web ページ2](#_Toc318097395)
- [Visual Studio 2012 リリース候補](#_Toc318097396)

    - [Visual Studio 2010 と Visual Studio 2012 リリース候補間のプロジェクト共有 (プロジェクト互換性)](#project-compatibility)
    - [ASP.NET 4.5 Web サイトテンプレートの構成の変更](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [ASP.NET ルーティング用の IIS 7 でのネイティブサポート](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML エディター](#_Toc318097397)

        - [スマートタスク](#_Toc318097398)
        - [WAI-ARIA のサポート](#_Toc318097399)
        - [新しい HTML5 スニペット](#_Toc318097400)
        - [ユーザーコントロールに抽出](#_Toc318097401)
        - [属性のコードナゲットの IntelliSense](#_Toc318097402)
        - [開始タグまたは終了タグの名前を変更するときに、一致するタグの名前を自動的に変更する](#_Toc318097403)
        - [イベントハンドラーの生成](#_Toc318097404)
        - [スマートインデント](#_Toc318097405)
        - [ステートメント入力候補を自動的に減らす](#_Toc318097406)
    - [JavaScript エディター](#_Toc318097407)

        - [コードのアウトライン](#_Toc318097408)
        - [中かっこの一致](#_Toc318097409)
        - [定義に移動](#_Toc318097410)
        - [ECMAScript5 のサポート](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC 署名のオーバーロード](#_Toc318097413)
        - [暗黙の参照](#_Toc318097414)
    - [CSS エディター](#_Toc318097415)

        - [ステートメント入力候補を自動的に減らす](#_Toc318097416)
        - [階層インデント。](#_Toc318097417)
        - [CSS ハックのサポート](#_Toc318097418)
        - [ベンダー固有のスキーマ (-moz-,-webkit)](#_Toc318097419)
        - [コメントとコメント解除のサポート](#_Toc318097420)
        - [カラーピッカー](#_Toc318097421)
        - [スニペット](#_Toc318097422)
        - [カスタム領域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [発行](#_Toc318097425)

        - [発行プロファイル](#_Toc318097426)
        - [ASP.NET のプリコンパイルとマージ](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免責事項](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core ランタイムとフレームワーク

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>HTTP 要求と応答の非同期的な読み取りと書き込み

ASP.NET 4 では、 *GetBufferlessInputStream*メソッドを使用して HTTP 要求エンティティをストリームとして読み取る機能が導入されました。 このメソッドは、要求エンティティへのストリームアクセスを提供しました。 ただし、同期的に実行され、要求の間、スレッドに関連付けられます。

ASP.NET 4.5 では、HTTP 要求エンティティでストリームを非同期的に読み取る機能、および非同期的にフラッシュする機能がサポートされています。 また、ASP.NET 4.5 には、HTTP 要求エンティティをダブルバッファーする機能があります。これにより、.aspx ページハンドラーや ASP.NET MVC コントローラーなどの下流の HTTP ハンドラーとの統合が容易になります。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest の処理の機能強化

*GetBufferlessInputStream*から ASP.NET 4.5 によって返されるストリーム参照は、同期と非同期の両方の読み取りメソッドをサポートします。 *GetBufferlessInputStream*から返された*ストリーム*オブジェクトは、system.io.stream.beginread メソッドと EndRead メソッドの両方を実装するようになりました。 非同期*ストリーム*メソッドを使用すると、要求エンティティをチャンク単位で非同期に読み取ることができ、ASP.NET では非同期読み取りループの各反復処理の間で現在のスレッドが解放されます。

また、ASP.NET 4.5 には、要求エンティティを読み取るためのコンパニオンメソッドも追加されています。 *httprequest.getbufferedinputstream*です。 この新しいオーバーロードは、同期読み取りと非同期読み取りの両方をサポートする*GetBufferlessInputStream*のように動作します。 ただし、読み取り時には、 *httprequest.getbufferedinputstream*もエンティティバイトを ASP.NET 内部バッファーにコピーして、下流のモジュールとハンドラーが引き続き要求エンティティにアクセスできるようにします。 たとえば、パイプライン内の上流コードによって、 *httprequest.getbufferedinputstream*を使用して要求エンティティが既に読み取られている場合でも、 *Httprequest*または*httprequest*を使用できます。 これにより、要求に対して非同期処理を実行することができます (たとえば、データベースへの大きなファイルのアップロードをストリーミングする) が、後で .aspx ページと MVC ASP.NET コントローラーを引き続き実行できます。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>応答を非同期的にフラッシュする

HTTP クライアントに応答を送信すると、クライアントが遠く離れたり、低帯域幅で接続したりすると、かなりの時間がかかることがあります。 通常、ASP.NET は、アプリケーションによって作成された応答バイトをバッファーします。 次に、ASP.NET は、要求処理の最後に、未収バッファーの1回の送信操作を実行します。

バッファーされた応答が大きい場合 (たとえば、大きなファイルをクライアントにストリーミングする場合) は、 *httpresponse.cache*を定期的に呼び出して、バッファリングされた出力をクライアントに送信し、メモリ使用量を制御したままにしておく必要があります。 ただし、 *flush*は同期呼び出しであるため、*フラッシュ*を繰り返し呼び出すと、長時間実行される可能性のある要求の間、スレッドが引き続き使用されます。

ASP.NET 4.5 では、 *httpresponse.cache*クラスの*Beginflush*および*endflush*メソッドを使用して非同期的にフラッシュを実行するためのサポートが追加されています。 これらのメソッドを使用すると、オペレーティングシステムのスレッドを使用せずにクライアントにデータを段階的に送信する非同期モジュールと非同期ハンドラーを作成できます。 *Beginflush*呼び出しと*endflush*呼び出しの間で、ASP.NET は現在のスレッドを解放します。 これにより、実行時間の長い HTTP ダウンロードをサポートするために必要なアクティブなスレッドの合計数が大幅に削減されます。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>*Await*および*タスク*ベースの非同期モジュールとハンドラーのサポート

.NET Framework 4 では、*タスク*と呼ばれる非同期プログラミングの概念が導入されました。 タスクは *、タスクの種類と*、*システム*の名前空間の関連する型によって表されます。 .NET Framework 4.5 は、*タスク*オブジェクトの操作を単純にするコンパイラの機能強化により、この点に基づいています。 .NET Framework 4.5 では、コンパイラは*await*と*async*という2つの新しいキーワードをサポートしています。 *Await*キーワードは、コードの一部を非同期に待機する必要があることを示す構文の省略形です。 *Async*キーワードは、メソッドをタスクベースの非同期メソッドとしてマークするために使用できるヒントを表します。

*Await*、 *async*、 *Task*オブジェクトを組み合わせることにより、.net 4.5 で非同期コードを簡単に記述できるようになります。 ASP.NET 4.5 では、新しいコンパイラの機能強化を使用して非同期 HTTP モジュールと非同期 HTTP ハンドラーを記述できる新しい Api により、これらの簡素化がサポートされています。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>非同期 HTTP モジュール

*タスク*オブジェクトを返すメソッド内で非同期処理を実行するとします。 次のコード例では、非同期呼び出しを行って Microsoft ホームページをダウンロードする非同期メソッドを定義します。 メソッドシグネチャで*async*キーワードが使用されていること、および*Downloadstringtaskasync*への*await*呼び出しが使用されていることに注意してください。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

ここで .NET Framework 記述する必要があるのは、ダウンロードの完了を待機している間、呼び出し履歴のアンワインドが自動的に処理され、ダウンロードが完了した後に自動的にコールスタックが復元されることだけです。

ここで、非同期の ASP.NET HTTP モジュールでこの非同期メソッドを使用するとします。 ASP.NET 4.5 には、ASP.NET HTTP パイプラインによって公開されている古い非同期プログラミングモデルとタスクベースの非同期メソッドを統合するために使用できるヘルパーメソッド (*EventHandlerTaskAsyncHelper*) と新しいデリゲート型 (*TaskEventHandler*) が含まれています。 この例では、次の方法を示します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>非同期 HTTP ハンドラー

ASP.NET で非同期ハンドラーを記述する従来のアプローチは、 *IHttpAsyncHandler*インターフェイスを実装することです。 ASP.NET 4.5 では、から派生できる*HttpTaskAsyncHandler*非同期基本型が導入されています。これにより、非同期ハンドラーの記述が非常に簡単になります。

*HttpTaskAsyncHandler*型は abstract であり、 *processrequestasync*メソッドをオーバーライドする必要があります。 内部的には、ASP.NET は、ASP.NET パイプラインによって使用される古い非同期プログラミングモデルと*Processrequestasync*の戻り値の署名 ( *Task*オブジェクト) を統合します。

次の例は、非同期 HTTP ハンドラーの実装の一部として*タスク*と*await*を使用する方法を示しています。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新しい ASP.NET 要求の検証機能

既定では、ASP.NET は要求の検証を実行し、フィールド、ヘッダー、cookie などのマークアップまたはスクリプトを検索する要求を調べます。 いずれかが検出されると、ASP.NET は例外をスローします。 これは、潜在的なクロスサイトスクリプティング攻撃に対する防御の1行目として機能します。

ASP.NET 4.5 を使用すると、未検証要求データを選択的に簡単に読み取ることができます。 また、ASP.NET 4.5 では、従来は外部ライブラリであった一般的なアンチ Xss ライブラリも統合されています。

開発者は、アプリケーションの要求の検証を選択的にオフにすることを頻繁に要求されています。 たとえば、アプリケーションがフォーラムソフトウェアの場合、HTML 形式のフォーラムの投稿とコメントをユーザーが送信できるようにする必要がありますが、それでも、要求の検証では他のすべてが確認されていることを確認してください。

ASP.NET 4.5 では、未検証入力を選択して簡単に操作できるようにする2つの機能が導入されています: 遅延 ("lazy") 要求の検証と未検証要求データへのアクセス。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>遅延 ("lazy") 要求の検証

ASP.NET 4.5 では、既定ですべての要求データが要求の検証の対象となります。 ただし、要求データに実際にアクセスするまで、要求の検証を遅延するようにアプリケーションを構成することができます。 (これは、特定のデータシナリオの遅延読み込みのような用語に基づいて、レイジー要求の検証と呼ばれることもあります)。次の例に示すように、 *httpRUntime*要素で*requestvalidationmode*属性を4.5 に設定することにより、web.config ファイルで遅延検証を使用するようにアプリケーションを構成できます。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

要求の検証モードが4.5 に設定されている場合、要求の検証は特定の要求値に対してのみトリガーされ、コードがその値にアクセスしたときにのみトリガーされます。 たとえば、コードが要求の値を取得した場合は、form コレクション内のその要素に対してのみ、要求の検証が呼び出されます。フォーム ["フォーラム\_post"]。 *フォーム*コレクション内の他の要素は検証されません。 以前のバージョンの ASP.NET では、コレクション内のいずれかの要素にアクセスしたときに、要求コレクション全体に対して要求の検証がトリガーされました。 新しい動作により、さまざまなアプリケーションコンポーネントが、他の部分で要求の検証をトリガーすることなく、さまざまな要求データを簡単に確認できるようになります。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>未検証要求のサポート

遅延要求の検証だけでは、要求の検証を選択的にバイパスする問題は解決されません。 Request. Form ["フォーラム\_post"] の呼び出しでは、その特定の要求値に対して要求の検証がトリガーされます。 ただし、そのフィールドでマークアップを許可する必要があるため、検証をトリガーせずにこのフィールドにアクセスすることもできます。

これを可能にするために、ASP.NET 4.5 では、要求データへの未検証アクセスがサポートされるようになりました。 ASP.NET 4.5 には、 *HttpRequest*クラスの新しい*未検証*collection プロパティが含まれています。 このコレクションは、*フォーム*、 *QueryString*、 *cookie*、 *Url*など、要求データのすべての共通値へのアクセスを提供します。

フォーラムの例を使用して、未検証 request データを読み取ることができるようにするには、まず、新しい要求の検証モードを使用するようにアプリケーションを構成する必要があります。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

次に、*未検証*プロパティを使用して、未検証 form 値を読み取ることができます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> セキュリティ-*未検証の要求データを慎重に使用します。* ASP.NET 4.5 では、未検証要求のプロパティとコレクションが追加され、非常に特殊な未検証要求データに簡単にアクセスできるようになりました。 ただし、危険なテキストがユーザーに表示されないようにするには、未加工の要求データに対してカスタム検証を実行する必要があります。

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>アンチ Xss ライブラリ

Microsoft のアンチ Xss ライブラリが普及しているため、ASP.NET 4.5 には、そのライブラリのバージョン4.0 からのコアエンコードルーチンが組み込まれました。

エンコーディングルーチンは、新しい*system.web. web.config*名前空間の*アンチ Xssenプログラマ*の型によって実装されます。 型で実装されている任意の静的エンコードメソッドを呼び出すことによって、*アンチ Xssenプログラマ*型を直接使用できます。 ただし、新しいアンチ XSS ルーチンを使用するための最も簡単な方法は、既定では、ASP.NET アプリケーションが*アンチ Xssenプログラマ*クラスを使用するように構成することです。 これを行うには、次の属性を web.config ファイルに追加します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

*EncoderType*属性が*アンチ Xssenプログラマ*型を使用するように設定されている場合、ASP.NET のすべての出力エンコードは、新しいエンコードルーチンを自動的に使用します。

これらは、ASP.NET 4.5 に組み込まれている外部アンチ Xss ライブラリの部分です。

- *HtmlEncode*、 *HtmlFormUrlEncode*、 *htmlattributeencode*
- *Xmlattributeencode*と*xmlencode*
- *UrlEncode*と*urlpathencode* (new)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Websocket プロトコルのサポート

Websocket プロトコルは、標準ベースのネットワークプロトコルで、クライアントとサーバーの間で HTTP 経由のセキュリティで保護されたリアルタイムの双方向通信を確立する方法を定義します。 マイクロソフトは、IETF と W3C 標準の両方の本文を使用して、プロトコルの定義を支援してきました。 Websocket プロトコルは、ブラウザーだけでなく、すべてのクライアントでサポートされており、Microsoft は、クライアントとモバイルの両方のオペレーティングシステムで Websocket プロトコルをサポートする多くのリソースに投資しています。

Websocket プロトコルを使用すると、クライアントとサーバーの間で実行時間の長いデータ転送を簡単に作成できます。 たとえば、チャットアプリケーションを作成する方がはるかに簡単です。クライアントとサーバーの間で実行時間の長い接続を確立できるからです。 ソケットの動作をシミュレートするために、定期的なポーリングや HTTP の長いポーリングなどの回避策を使用する必要はありません。

ASP.NET 4.5 と IIS 8 には、低レベルの Websocket サポートが含まれており、ASP.NET 開発者は、Websocket オブジェクトで文字列とバイナリデータの両方を非同期的に読み取り、書き込みを行うために、マネージ Api を使用できます。 ASP.NET 4.5 には、Websocket プロトコルを操作するための型を含む新しい名前空間が*あります。*

ブラウザークライアントは、次の例に示すように、ASP.NET アプリケーションの URL を指す DOM *WebSocket*オブジェクトを作成することによって、websocket 接続を確立します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

任意の種類のモジュールまたはハンドラーを使用して、ASP.NET に Websocket エンドポイントを作成できます。 前の例では、.ashx ファイルを使用してハンドラーを簡単に作成できるため、.ashx ファイルが使用されていました。

Websocket プロトコルによれば、ASP.NET アプリケーションは、要求を HTTP GET 要求から Websocket 要求にアップグレードすることを示すことによって、クライアントの Websocket 要求を受け入れます。 次に例を示します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest*メソッドは、ASP.NET が現在の HTTP 要求をアンワインドしてから、関数デリゲートに制御を転送するため、関数デリゲートを受け取ります。 概念的には、この方法は、バックグラウンド処理を実行するスレッド開始デリゲートを定義する、 *thread*の使用方法と似ています。

ASP.NET が完了し、クライアントが Websocket ハンドシェイクを正常に完了すると、ASP.NET はデリゲートを呼び出し、Websocket アプリケーションは実行を開始します。 次のコード例は、ASP.NET で組み込みの Websocket サポートを使用する単純な echo アプリケーションを示しています。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

*Await*キーワードと非同期タスクベースの操作に対する .net 4.5 のサポートは、websocket アプリケーションの作成に適しています。 このコード例は、Websocket 要求が ASP.NET 内で完全に非同期に実行されることを示しています。 アプリケーションは、await ソケットを呼び出すことによって、メッセージがクライアントから送信されるのを非同期に待機し*ます。ReceiveAsync*。 同様に、await ソケットを呼び出すことによって、クライアントに非同期メッセージを送信することもでき*ます。SendAsync*。

ブラウザーでは、アプリケーションは*onmessage*関数を介して websocket メッセージを受信します。 ブラウザーからメッセージを送信するには、次の例に示すように、 *WebSocket* DOM 型の*send*メソッドを呼び出します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

今後、この機能の更新プログラムがリリースされる可能性があります。これにより、Websocket アプリケーションのこのリリースで必要な低レベルのコーディングの一部が抽象化されます。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>バンドル化と縮小

バンドルを使用すると、個々の JavaScript ファイルと CSS ファイルを1つのファイルとして扱うことができるバンドルにまとめることができます。 不要な空白文字やその他の文字を削除することによって、では、JavaScript ファイルと CSS ファイルを縮小します。 これらの機能は、Web フォーム、ASP.NET MVC、および Web ページで動作します。

バンドルは、バンドルクラスまたはその子クラスである ScriptBundle とスタイルバンドルを使用して作成されます。 バンドルのインスタンスを構成すると、そのバンドルをグローバル BundleCollection インスタンスに追加するだけで、受信要求で使用できるようになります。 既定のテンプレートでは、バンドルの構成は BundleConfig ファイルで実行されます。 この既定の構成では、テンプレートで使用されるすべてのコアスクリプトと css ファイルのバンドルが作成されます。

バンドルは、考えられるいくつかのヘルパーメソッドのいずれかを使用して、ビュー内から参照されます。 デバッグモードとリリースモードでのバンドルのさまざまなマークアップのレンダリングをサポートするために、ScriptBundle クラスとスタイルバンドルクラスには、ヘルパーメソッドである Render が用意されています。 デバッグモードの場合、Render はバンドル内の各リソースのマークアップを生成します。 リリースモードでは、Render はバンドル全体に対して1つのマークアップ要素を生成します。 デバッグモードとリリースモードを切り替えるには、次のように web.config でコンパイル要素の debug 属性を変更します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

また、最適化を有効または無効にするには、Bundletable.enableoptimization ときプロパティを使用して直接設定することもできます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

ファイルがバンドルされている場合は、最初にアルファベット順 (**ソリューションエクスプローラー**に表示されます) に並べ替えられます。 次に、既知のライブラリとそのカスタム拡張 (jQuery、MooTools、Dojo など) が最初に読み込まれるように整理されます。 たとえば、上記のスクリプトフォルダーのバンドルの最終的な順序は次のようになります。

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. .js

また、CSS ファイルはアルファベット順に並べ替えられた後、再構成され、.css とノーマライズが他のファイルよりも前に来るようになります。 上に示したスタイルフォルダーのバンドルの最終的な並べ替えは、次のようになります。

1. reset.css
2. content.css
3. forms.css
4. globals.css
5. menu .css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web ホスティングのパフォーマンスの向上

.NET Framework 4.5 と Windows 8 では、web サーバーワークロードのパフォーマンスを大幅に向上させるのに役立つ機能が導入されています。 これには、減少 (最大35%) が含まれます。ASP.NET を使用する web ホスティングサイトの起動時間とメモリフットプリントの両方。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>主要なパフォーマンス要因

理想的には、すべての web サイトがアクティブでメモリ内にあり、次の要求にすばやく応答できるようにする必要があります。 サイトの応答性に影響する要因は次のとおりです。

- アプリケーションプールがリサイクルされた後にサイトが再起動するまでにかかる時間。 これは、サイトアセンブリがメモリ内に存在しなくなったときに、サイトの web サーバープロセスを起動するためにかかる時間です。 (プラットフォームアセンブリは、他のサイトで使用されているため、まだメモリ内にあります)。このような状況は、"コールドサイト、ウォームフレームワークスタートアップ"、または "コールドサイトスタートアップ" と呼ばれます。
- サイトがどの程度のメモリを占有しているか。 この用語は、"サイトごとのメモリ消費" または "非共有の作業セット" です。

これらの要因の両方に重点を置いた新しいパフォーマンスの向上。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>新しいパフォーマンス機能の要件

新しい機能の要件は、次のカテゴリに分けることができます。

- .NET Framework 4 で実行される機能強化。
- .NET Framework 4.5 が必要であるが、Windows の任意のバージョンで実行できる機能強化。
- Windows 8 で実行されている .NET Framework 4.5 でのみ利用できる機能強化。

パフォーマンスは、有効にできる改善レベルごとに増加します。

.NET Framework 4.5 の機能強化の一部では、他のシナリオにも適用される、より広範なパフォーマンス機能を利用しています。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共通アセンブリの共有

**要件**: .NET Framework 4 および Visual Studio 11 DEVELOPER Preview SDK

サーバー上の異なるサイトでは、多くの場合、同じヘルパーアセンブリ (たとえば、スタートキットやサンプルアプリケーションのアセンブリ) を使用します。 各サイトには、Bin ディレクトリ内にこれらのアセンブリの独自のコピーがあります。 アセンブリのオブジェクトコードは同一ですが、物理的には独立したアセンブリなので、各アセンブリはコールドサイトの起動中に個別に読み取られ、メモリ内に個別に保持される必要があります。

新しいインターン機能によって、このような非効率性が解決され、RAM の要件と読み込み時間が短縮されます。 インターンを使用すると、Windows はファイルシステム内の各アセンブリのコピーを1つ保持できます。また、サイトの Bin フォルダー内の個々のアセンブリは、単一のコピーへのシンボリックリンクに置き換えられます。 個々のサイトに個別のバージョンのアセンブリが必要な場合は、シンボリックリンクがアセンブリの新しいバージョンに置き換えられ、そのサイトのみが影響を受けます。

シンボリックリンクを使用してアセンブリを共有するには、aspnet\_という名前の新しいツールが必要です。これにより、インターンアセンブリのストアを作成して管理できます。 これは、Visual Studio 11 Developer Preview SDK の一部として提供されています。 (ただし、最新の[更新プログラム](https://support.microsoft.com/kb/2468871)がインストールされていることを前提として、.NET Framework 4 のみがインストールされているシステムで動作します)。

対象となるすべてのアセンブリがインターン化されていることを確認するには、aspnet\_を定期的に実行します (たとえば、定期的なタスクとして1週間に1回)。 一般的な用途は次のとおりです。

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

すべてのオプションを表示するには、引数を指定せずにツールを実行します。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>高速起動のためのマルチコア JIT コンパイルの使用

**要件**: .NET Framework 4.5

コールドサイトを起動する場合、アセンブリをディスクから読み取る必要があるだけでなく、サイトを JIT コンパイルする必要があります。 複雑なサイトの場合、これによって大幅な遅延が発生する可能性があります。 .NET Framework 4.5 の新しい汎用手法により、使用可能なプロセッサコア全体に JIT コンパイルを分散することで、これらの遅延が軽減されます。 これは、以前にサイトを起動したときに収集された情報を使用して、可能な限り早く実行されます。 この[機能は、](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) system.string メソッドによって実装されています。

ASP.NET では、複数のコアを使用した JIT コンパイルが既定で有効になっているため、この機能を利用するために何もする必要はありません。 この機能を無効にする場合は、web.config ファイルで次の設定を行います。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>メモリ用に最適化するためのガベージコレクションのチューニング

**要件**: .NET Framework 4.5

サイトが実行されると、ガベージコレクター (GC) ヒープの使用は、メモリの消費に大きな影響をもたらす可能性があります。 .NET Framework GC では、ガベージコレクターと同様に、CPU 時間 (コレクションの頻度と意味) とメモリ使用量 (新しいオブジェクト、解放されたオブジェクト、または解放可能なオブジェクトに使用される追加の領域) との間でトレードオフを行います。 以前のリリースでは、適切なバランスを実現するために GC を構成する方法についてのガイダンスを提供しています (たとえば、「 [ASP.NET 2.0/3.5 共有ホスティング構成](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)」を参照してください)。

.NET Framework 4.5 では、複数のスタンドアロン設定ではなく、以前に推奨されていたすべての GC 設定と、サイトごとのパフォーマンスを向上する新しいチューニングを有効にする、ワークロード定義の構成設定を使用できます。ワーキングセット。

GC メモリのチューニングを有効にするには、Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config ファイルに次の設定を追加します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(Aspnet の変更に関する前のガイダンスに慣れている場合は、この設定が古い設定に置き換わることに注意してください。たとえば、gcServer や gcConcurrent などを設定する必要はありません。古い設定を削除する必要はありません)。

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Web アプリケーションのプリフェッチ

**要件**: Windows 8 で実行されている .NET Framework 4.5

いくつかのリリースでは、Windows には、アプリケーションの起動に伴うディスク読み取りコストを削減する[prefetcher](http://en.wikipedia.org/wiki/Prefetcher)と呼ばれるテクノロジが組み込まれています。 コールドスタートはクライアントアプリケーションの主な問題であるため、このテクノロジは、サーバーにとって不可欠なコンポーネントのみを含む Windows Server には含まれていません。 プリフェッチは、Windows Server の最新バージョンで使用できるようになりました。これにより、個々の web サイトの起動を最適化できます。

Windows Server の場合、prefetcher は既定では有効になっていません。 高密度 web ホスティング用に prefetcher を有効にして構成するには、コマンドラインで次のコマンドセットを実行します。

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

次に、prefetcher と ASP.NET アプリケーションを統合するために、web.config ファイルに次のを追加します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>厳密に型指定されたデータ コントロール

ASP.NET 4.5 では、Web フォームにデータを操作するための機能強化が含まれています。 1つ目の改善点は、厳密に型指定されたデータコントロールです。 以前のバージョンの ASP.NET の Web フォームコントロールでは、 *Eval*とデータバインディング式を使用してデータバインド値を表示します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

双方向のデータバインディングの場合は、 *Bind*を使用します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

実行時に、これらの呼び出しは、リフレクションを使用して指定されたメンバーの値を読み取り、結果をマークアップに表示します。 この方法を使用すると、任意の整形されていないデータに対して簡単にデータをバインドできます。

ただし、このようなデータバインディング式では、メンバー名の IntelliSense、ナビゲーション (定義への移動など)、またはこれらの名前のコンパイル時チェックなどの機能をサポートしていません。

この問題に対処するために、ASP.NET 4.5 では、コントロールがバインドされているデータのデータ型を宣言する機能が追加されています。 これは、新しい*ItemType*プロパティを使用して行います。 このプロパティを設定すると、 *Item*と*BindItem*の2つの新しい型指定された変数が、データバインド式のスコープで使用できるようになります。 変数は厳密に型指定されているため、Visual Studio の開発エクスペリエンスのすべての利点が得られます。

双方向のデータバインディング式の場合は、 *BindItem*変数を使用します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

データバインディングをサポートする ASP.NET Web フォームフレームワークのほとんどのコントロールは、 *ItemType*プロパティをサポートするように更新されています。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>モデル バインド

モデルバインドは、コード中心のデータアクセスを操作するために、ASP.NET Web フォームコントロールのデータバインディングを拡張します。 *ObjectDataSource*コントロールの概念と、ASP.NET MVC のモデルバインドの概念が組み込まれています。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>データの選択

モデルバインドを使用してデータを選択するようにデータコントロールを構成するには、コントロールの*SelectMethod*プロパティを、ページのコード内のメソッドの名前に設定します。 データコントロールは、ページライフサイクルの適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。 *DataBind*メソッドを明示的に呼び出す必要はありません。

次の例では、 *GridView*コントロールは*GetCategories*という名前のメソッドを使用するように構成されています。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

*GetCategories*メソッドは、ページのコードで作成します。 単純な select 操作の場合、メソッドはパラメーターを必要とせず、 *IEnumerable*または*IQueryable*オブジェクトを返します。 新しい*ItemType*プロパティが設定されている場合 (前述の厳密に型指定された[データコントロール](#_Toc318097386)で説明されているように、厳密に型指定されたデータバインディング式を有効にする)、これらのインターフェイスのジェネリックバージョンを *&gt;&lt;* *&gt;&lt;* 返す必要があります。これは、 *itemtype*プロパティの型 ( *iqueryable&lt;Category&gt;* など) と一致する*t*パラメーターを

次の例は、 *GetCategories*メソッドのコードを示しています。 この例では、Northwind サンプルデータベースで Entity Framework Code First モデルを使用します。 このコードにより、 *Include*メソッドを使用して各カテゴリの関連製品の詳細が返されるようになります。 (これにより、マークアップ内の*TemplateField*要素に、各カテゴリの製品数が表示されます。 [n + 1 を選択](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)する必要はありません)。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

ページを実行すると、 *GridView*コントロールは*GetCategories*メソッドを自動的に呼び出し、構成されたフィールドを使用して返されたデータをレンダリングします。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Select メソッドは*IQueryable*オブジェクトを返すため、 *GridView*コントロールはクエリを実行する前にさらに操作できます。 たとえば、 *GridView*コントロールでは、返された*IQueryable*オブジェクトを実行する前に、並べ替えとページングを行うためのクエリ式を追加できます。これにより、基になる LINQ プロバイダーによってこれらの操作が実行されます。 この場合、Entity Framework によって、これらの操作がデータベースで確実に実行されます。

次の例は、並べ替えとページングを可能にするために変更された*GridView*コントロールを示しています。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

これで、ページの実行時に、コントロールは現在のデータページだけが表示され、選択された列によって並べ替えられていることを確認できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

返されたデータをフィルター処理するには、select メソッドにパラメーターを追加する必要があります。 これらのパラメーターは、実行時にモデルバインディングによって設定されます。また、これらのパラメーターを使用して、データを返す前にクエリを変更できます。

たとえば、クエリ文字列にキーワードを入力して、ユーザーが製品をフィルター処理できるようにするとします。 パラメーターをメソッドに追加し、パラメーター値を使用するようにコードを更新することができます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

このコードには、*キーワード*に値が指定されている場合は*Where*式が含まれ、その後クエリ結果が返されます。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>値プロバイダー

前の例は、*キーワード*パラメーターの値の取得元の場所に固有のものではありませんでした。 この情報を示すために、パラメーター属性を使用できます。 この例では、 *System.web binding*名前空間にある*querystringattribute*クラスを使用できます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

これにより、モデルバインドは、クエリ文字列から実行時に*キーワード*パラメーターに値をバインドしようとするように指示します。 (この場合、型変換の実行が必要になることがありますが、この場合はそうではありません)。値を指定できず、型が null 非許容である場合は、例外がスローされます。

これらのメソッドの値のソースは、値プロバイダーと呼ばれ、使用する値プロバイダーを示すパラメーター属性は、値プロバイダー属性と呼ばれます。 Web フォームには、Web フォームアプリケーションでのユーザー入力のすべての一般的なソース (クエリ文字列、cookie、フォーム値、コントロール、ビューステート、セッション状態、プロファイルプロパティなど) に関する値プロバイダーと対応する属性が含まれます。 カスタム値プロバイダーを作成することもできます。

既定では、値プロバイダーコレクション内の値を検索するためのキーとしてパラメーター名が使用されます。 この例のコードでは、キーワードという名前のクエリ文字列値が検索されます (たとえば、~/default.aspx? keyword = chef)。 パラメーター属性に引数として渡すことによって、カスタムキーを指定できます。 たとえば、q という名前のクエリ文字列変数の値を使用するには、次のようにします。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

このメソッドがページのコード内にある場合、ユーザーはクエリ文字列を使用してキーワードを渡すことによって結果をフィルター処理できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

モデルバインドでは、値の読み取り、null 値のチェック、適切な型への変換の試行、変換が成功したかどうかの確認、最後にの値の使用など、手作業でコーディングする必要がある多くのタスクが実行されます。照会. モデルバインドを使用すると、コードがはるかに少なくなり、アプリケーション全体で機能を再利用することができます。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>コントロールの値によるフィルター処理

例を拡張して、ユーザーがドロップダウンリストからフィルター値を選択できるようにするとします。 次のドロップダウンリストをマークアップに追加し、 *SelectMethod*プロパティを使用して別のメソッドからデータを取得するように構成します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

通常は、 *EmptyDataTemplate*要素を*GridView*コントロールに追加して、一致する製品が見つからない場合にコントロールがメッセージを表示するようにします。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

ページコードで、ドロップダウンリストの新しい select メソッドを追加します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最後に、 *Getproducts* select メソッドを更新して、選択したカテゴリの ID を含む新しいパラメーターをドロップダウンリストから取得します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

ページが実行されると、ユーザーはドロップダウンリストからカテゴリを選択できるようになり、フィルター処理されたデータを表示するために*GridView*コントロールが自動的に再バインドされます。 これが可能なのは、モデルバインドが select メソッドのパラメーターの値を追跡し、ポストバック後にパラメーター値が変更されたかどうかを検出するためです。 その場合、モデルバインドによって、関連付けられたデータコントロールが強制的にデータに再バインドされます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML エンコードされたデータバインディング式

データバインディング式の結果を HTML エンコードできるようになりました。 コロン (:) を追加します。データバインディング式をマークする &lt;% # プレフィックスの末尾。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>控えめに検証

クライアント側の検証ロジックに控えめな JavaScript を使用するように、組み込みの検証コントロールを構成できるようになりました。 これにより、ページマークアップでインラインでレンダリングされる JavaScript の量が大幅に減少し、ページ全体のサイズが縮小されます。 次のいずれかの方法で、控えめな JavaScript をバリデーターコントロール用に構成できます。

- 次の設定を Web.config ファイルの *&lt;appSettings&gt;* 要素に追加することでグローバルに行うことができます。 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 静的な*UnobtrusiveValidationMode*プロパティを*UnobtrusiveValidationMode*に設定することによってグローバルに実行します (通常は、*アプリケーション\_* 、global.asax ファイルの Start メソッド)。
- *ページクラスの*new *UnobtrusiveValidationMode*プロパティを*UnobtrusiveValidationMode*に設定して、ページに対して個別に設定します。

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 の更新プログラム

HTML5 の新機能を利用するために、Web フォームサーバーコントロールにいくつかの機能強化が行われています。

- *TextBox*コントロールの*TextMode*プロパティが更新され、 *email*や*datetime*などの新しい HTML5 入力型がサポートされるようになりました。
- *FileUpload*コントロールで、この HTML5 機能をサポートするブラウザーからの複数のファイルアップロードがサポートされるようになりました。
- 検証コントロールは、HTML5 入力要素の検証をサポートするようになりました。
- URL を表す属性を持つ新しい HTML5 要素では、runat = "server" がサポートされるようになりました。 その結果、URL パスで ASP.NET 規則を使用できます。たとえば、~ 演算子を使用すると、アプリケーションルートを表すことができます (&lt;video runat = "server" src = "~/myvideo"/&gt;)。
- *UpdatePanel*コントロールは、HTML5 入力フィールドの投稿をサポートするように修正されました。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta が Visual Studio 11 Beta に含まれるようになりました。 ASP.NET MVC は、モデルビューコントローラー (MVC) パターンを利用することで、高度なテストが可能な、保守しやすい Web アプリケーションを開発するためのフレームワークです。 ASP.NET MVC 4 を使用すると、モバイル Web 用のアプリケーションの構築が容易になり、ASP.NET Web API が含まれます。これにより、任意のデバイスに接続できる HTTP サービスを構築できます。 詳細については、 [ASP.NET MVC 4 リリースノート](mvc4-release-notes.md)を参照してください。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web ページ 2

次のような新機能があります。

- 新規および更新されたサイトテンプレート。
- *検証*ヘルパーを使用して、サーバー側およびクライアント側の検証を追加します。
- アセットマネージャーを使用してスクリプトを登録する機能。
- OAuth および OpenID を使用した Facebook およびその他のサイトからのログインの有効化。
- *Maps*ヘルパーを使用してマップを追加します。
- Web ページアプリケーションをサイドバイサイドで実行する。
- モバイルデバイスのレンダリングページ。

これらの機能とページ全体のコード例の詳細については、 [Web ページ 2 Beta のトップ機能](https://go.microsoft.com/fwlink/?LinkID=227824)に関するページを参照してください。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

このセクションでは、Visual Web Developer 11 Beta および Visual Studio 2012 リリース候補での web 開発の機能強化について説明します。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 と Visual Studio 2012 リリース候補間のプロジェクト共有 (プロジェクト互換性)

Visual Studio 2012 リリース候補が表示されるまで、新しいバージョンの Visual Studio で既存のプロジェクトを開くと、変換ウィザードが起動します。 これにより、プロジェクトとソリューションのコンテンツ (アセット) を旧バージョンと互換性のない新しい形式にアップグレードすることが強制されました。 そのため、変換後に、以前のバージョンの Visual Studio でプロジェクトを開くことができませんでした。

多くのお客様は、これが適切なアプローチではなかったことを伝えてきました。 Visual Studio 11 Beta では、Visual Studio 2010 SP1 でのプロジェクトとソリューションの共有がサポートされるようになりました。 これは、Visual Studio 2012 リリース候補で2010プロジェクトを開いた場合でも、Visual Studio 2010 SP1 でプロジェクトを開くことができることを意味します。

> [!NOTE]
> いくつかの種類のプロジェクトは、Visual Studio 2010 SP1 と Visual Studio 2012 リリース候補間で共有することはできません。 これには、いくつかの古いプロジェクト (ASP.NET MVC 2 プロジェクトなど) や特別な目的 (セットアッププロジェクトなど) のプロジェクトが含まれます。

Visual studio 11 Beta で Visual Studio 2010 SP1 Web プロジェクトを初めて開くと、次のプロパティがプロジェクトファイルに追加されます。

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags、UpgradeBackupLocation、および OldToolsVersion は、プロジェクトファイルをアップグレードするプロセスによって使用されます。 Visual Studio 2010 では、プロジェクトの操作には影響しません。

VisualStudioVersion は、現在のプロジェクトの Visual Studio のバージョンを示す MSBuild 4.5 で使用される新しいプロパティです。 このプロパティは、MSBuild 4.0 (Visual Studio 2010 SP1 で使用される MSBuild のバージョン) には存在しないため、既定値をプロジェクトファイルに挿入します。

VSToolsPath プロパティは、MSBuildExtensionsPath32 設定で表されるパスからインポートする正しい .targets ファイルを決定するために使用されます。

Import 要素に関連するいくつかの変更もあります。 これらの変更は、両方のバージョンの Visual Studio 間の互換性をサポートするために必要です。

> [!NOTE]
> 2つの異なるコンピューター上の Visual Studio 2010 SP1 と Visual Studio 11 Beta の間でプロジェクトを共有する場合、およびプロジェクトに App\_Data フォルダー内のローカルデータベースが含まれている場合は、データベースで使用される SQL Server のバージョンが両方のコンピューターにインストールされていることを確認する必要があります。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 Web サイトテンプレートの構成の変更

Visual Studio 2012 リリース候補の web サイトテンプレートを使用して作成されたサイト*の既定の web.config ファイル*には、次のような変更が加えられました。

- `<httpRuntime>` 要素で、`encoderType` 属性が既定で設定され、ASP.NET に追加されたアンチ Xss 型が使用されるようになりました。 詳細については、「 [xss」ライブラリ](#_Toc318097382)を参照してください。
- また `<httpRuntime>` 要素では、`requestValidationMode` 属性は "4.5" に設定されています。 つまり、既定では、要求の検証は、遅延 ("レイジー") 検証を使用するように構成されます。 詳細については、「 [New ASP.NET Request Validation Features](#_Toc318097379)」を参照してください。
- `<system.webServer>` セクションの `<modules>` 要素には、`runAllManagedModulesForAllRequests` 属性が含まれていません。 (既定値は false です)。これは、SP1 に更新されていないバージョンの IIS 7 を使用している場合、新しいサイトでのルーティングに問題がある可能性があることを意味します。 詳細については、「 [ASP.NET Routing の IIS 7 のネイティブサポート](#Native_Support_In_IIS7_For_ASPNET_Routine)」を参照してください。

これらの変更は、既存のアプリケーションには影響しません。 ただし、新しいテンプレートを使用して ASP.NET 4.5 用に作成した既存の web サイトと新しい web サイトの動作の違いを表している可能性があります。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>ASP.NET ルーティング用の IIS 7 でのネイティブサポート

このように ASP.NET を変更することはできませんが、SP1 更新プログラムが適用されていないバージョンの IIS 7 を使用している場合に影響を与える可能性がある新しい web サイトプロジェクトのテンプレートが変更されました。

ASP.NET では、ルーティングをサポートするために、次の構成設定をアプリケーションに追加できます。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

**RunallmanagedASP.NET Forallrequests**が true の場合、url に *.aspx*、 *mvc*、または同様の拡張子がない場合でも、`http://mysite/myapp/home` のような url はに移動します。

IIS 7 に対して行われた更新により、 **Runallmanagedモジュール Forallrequests**が不要になり、ASP.NET ルーティングがネイティブでサポートされます。 (更新プログラムの詳細については、Microsoft サポートの記事で、[特定の iis 7.0 または iis 7.5 ハンドラーが、url の末尾がピリオドではない要求を処理](https://support.microsoft.com/kb/980368)できるようにする更新プログラムについて説明しています)。

Web サイトが IIS 7 で実行されており、IIS が更新されている場合は、 **Runallmanagedモジュール Forallrequests**を true に設定する必要はありません。 実際には、要求に不要な処理オーバーヘッドが追加されるため、true に設定することは推奨されません。 この設定が true の場合、 *.htm*、 *.jpg*、およびその他の静的ファイルの要求も含め、すべての要求が ASP.NET 要求パイプラインを経由します。

Visual Studio 2012 RC に用意されているテンプレートを使用して新しい ASP.NET 4.5 web サイトを作成した場合、web サイトの構成に**Runallmanagedモジュール Forallrequests**設定は含まれません。 これは、既定では false に設定されていることを意味します。

SP1 がインストールされていない状態で Windows 7 で web サイトを実行すると、IIS 7 には必要な更新プログラムが含まれません。 その結果、ルーティングは機能しなくなり、エラーが表示されます。 ルーティングが機能しない問題が発生した場合は、次のいずれかの操作を実行できます。

- Windows 7 を SP1 に更新します。これにより、IIS 7 に更新プログラムが追加されます。
- 前述の Microsoft サポートの記事で説明されている更新プログラムをインストールします。
- その web サイトの Web.config ファイルで**Runallmanagedモジュール Forallrequests**を true に設定します。 これにより、要求にオーバーヘッドがいくつか追加されることに注意してください。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML エディター

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>スマートタスク

デザインビューでは、多くの場合、サーバーコントロールの複雑なプロパティを設定するためのダイアログボックスとウィザードが関連付けられています。 たとえば、特別なダイアログボックスを使用して、 *Repeater*コントロールにデータソースを追加したり、 *GridView*コントロールに列を追加したりできます。

ただし、複合プロパティのこの種の UI ヘルプは、ソースビューでは使用できません。 そのため、Visual Studio 11 では、ソースビューのスマートタスクが導入されています。 スマートタスクは、および Visual Basic エディターで一般的に使用されるC#機能のコンテキストに対応したショートカットです。

ASP.NET Web フォームコントロールでは、挿入ポイントが要素内にある場合、スマートタスクは、サーバータグに小さいグリフとして表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

グリフをクリックするか、CTRL +. キーを押すとスマートタスクが拡張されます。 (ドット)。コードエディターと同様です。 次に、デザインビューのスマートタスクに似たショートカットが表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

たとえば、前の図のスマートタスクは、GridView タスクのオプションを示しています。 [列の編集] を選択すると、次のダイアログボックスが表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

ダイアログボックスに入力すると、デザインビューで設定できるものと同じプロパティが設定されます。 [OK] をクリックすると、コントロールのマークアップが新しい設定で更新されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA のサポート

アクセス可能な web サイトの作成がますます重要になっています。 [WAI アクセシビリティ標準](http://www.w3.org/WAI/intro/aria)では、開発者がアクセス可能な web サイトを作成する方法を定義します。 この standard は、Visual Studio で完全にサポートされるようになりました。

たとえば、 *role*属性には IntelliSense が完全に含まれるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

また、WAI 標準では、 *aria*というプレフィックスが付いた属性も導入されています。これにより、HTML5 ドキュメントにセマンティクスを追加できるようになります。 Visual Studio*では、* 次の aria 属性も完全にサポートされています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新しい HTML5 スニペット

一般的に使用される HTML5 マークアップをより迅速かつ簡単に記述できるように、Visual Studio には多くのスニペットが含まれています。 ビデオスニペットの例を次に示します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

スニペットを呼び出すには、IntelliSense で要素が選択されたときに Tab キーを2回押します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

これにより、カスタマイズできるスニペットが生成されます。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>ユーザーコントロールに抽出

大規模な web ページでは、個々の部分をユーザーコントロールに移動することをお勧めします。 このリファクタリング形式を使用すると、ページの読みやすさを向上させることができ、ページの構造を簡略化できます。

これを簡単にするために、ソースビューで Web フォームページを編集するときに、ページ内のテキストを選択して右クリックし、[ユーザーコントロールに抽出] を選択できるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>属性のコードナゲットの IntelliSense

Visual Studio では、すべてのページまたはコントロールにサーバー側のコードナゲットの IntelliSense が常に用意されています。 Visual Studio には、HTML 属性でコードナゲットの IntelliSense も含まれるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

これにより、データバインディング式を簡単に作成できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>開始タグまたは終了タグの名前を変更するときに、一致するタグの名前を自動的に変更する

HTML 要素の名前を変更すると (たとえば、 *div*タグが*ヘッダー*タグになるように変更した場合)、対応する開始タグまたは終了タグもリアルタイムで変更されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

これにより、終了タグの変更や間違ったタグの変更を忘れた場合に、エラーを回避できます。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>イベントハンドラーの生成

Visual Studio にソースビューの機能が追加され、イベントハンドラーを作成して手動でバインドできるようになりました。 ソースビューでイベント名を編集している場合は、IntelliSense によって &lt;新しいイベント&gt;が表示されます。これにより、正しいシグネチャを持つページのコードにイベントハンドラーが作成されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

既定では、イベントハンドラーは、イベント処理メソッドの名前としてコントロールの ID を使用します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

結果のイベントハンドラーは次のようになります (この例C#では)。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>スマートインデント

空の HTML 要素内で Enter キーを押すと、エディターによって、カーソル位置が右側に配置されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

この場所で Enter キーを押すと、終了タグが下へ移動して、開始タグと一致するようにインデントされます。 挿入ポイントもインデントされます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>ステートメント入力候補を自動的に減らす

Visual Studio の IntelliSense の一覧が、関連するオプションのみを表示するように入力した内容に基づいてフィルター処理されるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense では、IntelliSense の一覧内の個々の単語のタイトルケースに基づいてフィルター処理も行います。 たとえば、「dl」と入力すると、dl と asp: DataList の両方が表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

この機能により、既知の要素に対してステートメントの入力候補が高速になります。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript エディター

Visual Studio 2012 リリース候補の JavaScript エディターはまったく新しいものであり、Visual Studio での JavaScript の操作エクスペリエンスが大幅に向上しています。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>コードのアウトライン表示

すべての関数に対してアウトライン領域が自動的に作成されるようになりました。これにより、現在のフォーカスに関連しないファイルの一部を折りたたむことができます。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>かっこの一致

左中かっこまたは右中かっこに挿入ポイントを配置すると、エディターによって一致するものが強調表示されます。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>定義に移動

[定義へ移動] コマンドを使用すると、関数または変数のソースに移動できます。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 のサポート

このエディターは、JavaScript 言語を記述する最新バージョンである ECMAScript5 の新しい構文と Api をサポートしています。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

DOM Api 用の IntelliSense が改善され、 *Queryselector*、DOM Storage、クロスドキュメントメッセージング、 *canvas*などの多くの新しい HTML5 api がサポートされるようになりました。 DOM IntelliSense は、ネイティブタイプライブラリ定義ではなく、単一の単純な JavaScript ファイルによって駆動されるようになりました。 これにより、拡張や置換を簡単に行うことができます。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 署名のオーバーロード

次の例に示すように、新しい *&lt;signature&gt;* 要素を使用して、JavaScript 関数の個別のオーバーロードに対して詳細な IntelliSense コメントを宣言できるようになりました。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>暗黙の参照

特定の JavaScript ファイルまたはブロックが参照するファイルの一覧に暗黙的に含まれる JavaScript ファイルを中央のリストに追加できるようになりました。つまり、そのコンテンツに対して IntelliSense を利用できます。 たとえば、ファイルの中央のリストに jQuery ファイルを追加することができます。また、明示的に参照しているかどうかにかかわらず、ファイルの JavaScript ブロックで jQuery 関数の IntelliSense を利用できます (///&lt;reference/&gt;を使用します)。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS エディター

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>ステートメント入力候補を自動的に減らす

CSS の IntelliSense の一覧は、選択したスキーマでサポートされている CSS プロパティと値に基づいてフィルター処理されるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense では、case 検索のタイトルもサポートされています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>階層インデント

CSS エディターは、階層的なルールを表示するためにインデントを使用します。これにより、カスケードルールが論理的に編成される方法の概要が示されます。 次の例では、セレクター #list がリストのカスケード子であるため、インデントされます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

次の例は、より複雑な継承を示しています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

ルールのインデントは、親ルールによって決定されます。 階層インデントは既定で有効になっていますが、[オプション] ダイアログボックス (メニューバーの [ツール]、[オプション]) を無効にすることができます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS ハックのサポート

何百もの実世界の CSS ファイルを分析することで、CSS ハッキングが非常に一般的であることがわかります。また、Visual Studio で最も広く使用されているものがサポートされるようになりました。 このサポートには、IntelliSense と、star (\*) プロパティとアンダースコア (\_) プロパティのハッキングの検証が含まれます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

一般的なセレクターハックもサポートされているので、適用された場合でも階層インデントが維持されます。 Internet Explorer 7 のターゲットとして使用される一般的なセレクターハックは、セレクターを*先頭に子と html で\** します。 この規則を使用すると、階層的なインデントが維持されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>ベンダー固有のスキーマ (-moz-,-webkit)

CSS3 には、異なるタイミングで異なるブラウザーによって実装された多数のプロパティが導入されています。 これまで、開発者は、ベンダー固有の構文を使用して特定のブラウザーをコーディングしていました。 これらのブラウザー固有のプロパティは、IntelliSense に含まれるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>コメントとコメント解除のサポート

コードエディターで使用するのと同じショートカットを使用して、CSS ルールのコメント化とコメント解除を行うことができるようになりました (Ctrl + K、C からコメント、Ctrl + K、コメントを解除します)。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Color picker

以前のバージョンの Visual Studio では、色に関連する属性の IntelliSense は、名前付きの色の値のドロップダウンリストで設定されていました。 この一覧は、フル機能のカラーピッカーに置き換えられました。

色の値を入力すると、カラーピッカーが自動的に表示され、以前に使用した色の一覧が表示され、その後に既定のカラーパレットが表示されます。 マウスまたはキーボードを使用して色を選択できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

一覧は、完全なカラーピッカーに展開できます。 ピッカーを使用すると、不透明度スライダーを移動したときに任意の色を RGBA に自動的に変換することで、アルファチャネルを制御できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>スニペット

CSS エディターのスニペットを使用すると、クロスブラウザースタイルを簡単かつ迅速に作成できます。 ブラウザー固有の設定を必要とする多くの CSS3 プロパティがスニペットにロールアウトされました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS スニペットでは、IntelliSense の一覧を示すアットマーク (@) を入力することによって、(CSS3 メディアクエリなどの) 高度なシナリオをサポートしています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

@media 値を選択して Tab キーを押すと、CSS エディターによって次のスニペットが挿入されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

コードのスニペットと同様に、独自の CSS スニペットを作成することもできます。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>カスタム領域

コードエディターで既に使用可能な名前付きコード領域を CSS 編集に使用できるようになりました。 これにより、関連するスタイルブロックを簡単にグループ化できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

領域が折りたたまれると、リージョンの名前が表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

Page Inspector は、Visual Studio IDE で web ページ (HTML、Web フォーム、ASP.NET MVC、または Web ページ) をレンダリングするツールであり、ソースコードと結果の出力の両方を調べることができます。 ASP.NET ページでは、Page Inspector を使用して、ブラウザーに表示される HTML マークアップを生成したサーバー側コードを確認できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Page Inspector の詳細については、次のチュートリアルを参照してください。

- [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)での Page Inspector の使用
- [ASP.NET Web フォーム](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)での Page Inspector の使用

<a id="_Toc318097425"></a>
### <a name="publishing"></a>発行

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>発行プロファイル

Visual Studio 2010 では、Web アプリケーションプロジェクトの公開情報はバージョン管理に保存されず、他のユーザーと共有するように設計されていません。 Visual Studio 2012 リリース候補では、発行プロファイルの形式が変更されています。 これにより、チームの成果物が作成され、MSBuild に基づくビルドから簡単に利用できるようになりました。 ビルド構成情報は [発行] ダイアログボックスに表示されるので、発行前にビルド構成を簡単に切り替えることができます。

発行プロファイルは、PublishProfiles フォルダーに格納されます。 フォルダーの場所は、使用しているプログラミング言語によって異なります。

- C#: Properties\PublishProfiles
- Visual Basic: マイプロジェクト \ 発行プロファイル

各プロファイルは MSBuild ファイルです。 発行時に、このファイルはプロジェクトの MSBuild ファイルにインポートされます。 Visual Studio 2010 では、発行またはパッケージプロセスを変更する場合、カスタマイズを**ProjectName**. wpp. .targets という名前のファイルに配置する必要があります。 これはまだサポートされていますが、カスタマイズを発行プロファイル自体に配置できるようになりました。 このようにして、カスタマイズはそのプロファイルに対してのみ使用されます。

MSBuild から発行プロファイルを利用することもできるようになりました。 これを行うには、プロジェクトをビルドするときに次のコマンドを使用します。

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

プロジェクトの .csproj 値はプロジェクトのパスであり、ProfileName は発行するプロファイルの名前です。 または、 *publishprofile*プロパティのプロファイル名を渡す代わりに、発行プロファイルへの完全パスを渡すこともできます。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET のプリコンパイルとマージ

Web アプリケーションプロジェクトの場合、Visual Studio 2012 リリース候補では、プロジェクトの発行時またはパッケージ化時にサイトのコンテンツをプリコンパイルおよびマージできる [Web のパッケージ化/発行] ページにオプションが追加されます。 これらのオプションを表示するには、ソリューションエクスプローラーでプロジェクトを右クリックし、[プロパティ] をクリックします。次に、[Web のパッケージ化/発行] プロパティページをクリックします。 次の図は、[公開前にこのアプリケーションをプリコンパイルする] オプションを示しています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

このオプションを選択すると、web アプリケーションを発行またはパッケージ化するたびに、Visual Studio によってアプリケーションがプリコンパイルされます。 サイトのプリコンパイル方法またはアセンブリのマージ方法を制御する場合は、[詳細設定] ボタンをクリックして、これらのオプションを構成します。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Visual Studio で web プロジェクトをテストするための既定の web サーバーが IIS Express されるようになりました。 Visual Studio 開発サーバーは、開発時にローカル web サーバーに対してもオプションですが、IIS Express が推奨されるサーバーになりました。 Visual Studio 11 Beta での IIS Express の使用経験は、Visual Studio 2010 SP1 での使用方法と非常によく似ています。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免責事項

このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。

このドキュメントに含まれる情報は、取り上げている問題についての、公開時点における Microsoft Corporation の見解を表します。 Microsoft は変化する市場状況に対応する必要があるため、これを Microsoft による確約と解釈しないでください。Microsoft は、記載されている情報の公開後の正確さを保証できません。

このホワイト ペーパーは、情報提供のみを目的としています。 マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。

お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。 このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。

Microsoft は、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。 別途マイクロソフトのライセンス契約上に明示の規定がない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。

特に明記されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人名、場所、およびイベントは架空のものであり、実在する企業、組織、製品、ドメイン名、電子メールとは一切関係ありません。アドレス、ロゴ、人物、場所、またはイベントが想定されているか、または推測する必要があります。

(C) 2012 Microsoft Corporation. All rights reserved.

Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。

本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。
