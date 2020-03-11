---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 および Visual Studio 2010 Web 開発の概要 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、the.NET Framework 4 および Visual Studio 2010 に含まれる ASP.NET の新機能の多くの概要について説明します。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: ecde48f6bd88ee5f569bfeb8b70c26a50bc869c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511432"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 と Visual Studio 2010 Web 開発の概要

> このドキュメントでは、the.NET Framework 4 および Visual Studio 2010 に含まれる ASP.NET の新機能の多くの概要について説明します。
> 
> [このホワイトペーパーをダウンロードする](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

**目次**

**[コアサービス](#0.2__Toc253429238 "_Toc253429238")**  
[Web.config ファイルのリファクタリング](#0.2__Toc253429239 "_Toc253429239")  
[拡張可能な出力キャッシュ](#0.2__Toc253429240 "_Toc253429240")  
[Web アプリケーションの自動起動](#0.2__Toc253429241 "_Toc253429241")  
[ページを永続的にリダイレクトする](#0.2__Toc253429242 "_Toc253429242")  
[セッション状態の圧縮](#0.2__Toc253429243 "_Toc253429243")  
[許容される Url の範囲を拡張する](#0.2__Toc253429244 "_Toc253429244")  
[拡張可能な要求の検証](#0.2__Toc253429245 "_Toc253429245")  
[オブジェクトキャッシュとオブジェクトキャッシュの拡張性](#0.2__Toc253429246 "_Toc253429246")  
[Extensible HTML、URL、および HTTP ヘッダーエンコード](#0.2__Toc253429247 "_Toc253429247")  
[1つのワーカープロセスにおける個々のアプリケーションのパフォーマンス監視](#0.2__Toc253429248 "_Toc253429248")  
[複数のターゲット設定](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web フォームと MVC に含まれる jQuery](#0.2__Toc253429251 "_Toc253429251")  
[Content Delivery Network サポート](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager の明示的なスクリプト](#0.2__Toc253429253 "_Toc253429253")

**[Web フォーム](#0.2__Toc253429256 "_Toc253429256")**  
[メタタグを MetaDescription プロパティとページに設定します。](#0.2__Toc253429257 "_Toc253429257")  
[個々のコントロールのビューステートを有効にする](#0.2__Toc253429258 "_Toc253429258")  
[ブラウザー機能の変更点](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4 でのルーティング](#0.2__Toc253429260 "_Toc253429260")  
[クライアント Id の設定](#0.2__Toc253429261 "_Toc253429261")  
[データコントロールでの行選択の保持](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET Chart コントロール](#0.2__Toc253429263 "_Toc253429263")  
[QueryExtender コントロールを使用したデータのフィルター処理](#0.2__Toc253429264 "_Toc253429264")  
[Html エンコードされたコード式](#0.2__Toc253429265 "_Toc253429265")  
[プロジェクトテンプレートの変更](#0.2__Toc253429266 "_Toc253429266")  
[CSS の機能強化](#0.2__Toc253429267 "_Toc253429267")  
[非表示フィールドの周囲の div 要素の非表示](#0.2__Toc253429268 "_Toc253429268")  
[テンプレートコントロール用の外部テーブルのレンダリング](#0.2__Toc253429269 "_Toc253429269")  
[ListView コントロールの機能強化](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList と RadioButtonList のコントロールの機能強化](#0.2__Toc253429271 "_Toc253429271")  
[メニューコントロールの機能強化](#0.2__Toc253429272 "_Toc253429272")  
[Wizard および CreateUserWizard コントロール56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[区分のサポート](#0.2__Toc253429275 "_Toc253429275")  
[データ注釈属性の検証のサポート](#0.2__Toc253429276 "_Toc253429276")  
[テンプレートヘルパー](#0.2__Toc253429277 "_Toc253429277")

**[動的データ](#0.2__Toc253429278 "_Toc253429278")**  
[既存のプロジェクトの動的データを有効にする](#0.2__Toc253429279 "_Toc253429279")  
[宣言型の DynamicDataManager コントロール構文](#0.2__Toc253429280 "_Toc253429280")  
[エンティティテンプレート](#0.2__Toc253429281 "_Toc253429281")  
[Url と電子メールアドレスの新しいフィールドテンプレート](#0.2__Toc253429282 "_Toc253429282")  
[DynamicHyperLink コントロールを使用したリンクの作成](#0.2__Toc253429283 "_Toc253429283")  
[データモデルでの継承のサポート](#0.2__Toc253429284 "_Toc253429284")  
[多対多リレーションシップのサポート (Entity Framework のみ)](#0.2__Toc253429285 "_Toc253429285")  
[表示およびサポートの列挙型を制御する新しい属性](#0.2__Toc253429286 "_Toc253429286")  
[フィルターの強化されたサポート](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 の Web 開発の機能強化](#0.2__Toc253429288 "_Toc253429288")**  
[CSS 互換性の向上](#0.2__Toc253429289 "_Toc253429289")  
[HTML および JavaScript のスニペット](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense の機能強化](#0.2__Toc253429291 "_Toc253429291")

**[Visual Studio 2010 を使用した Web アプリケーションのデプロイ](#0.2__Toc253429292 "_Toc253429292")**  
[Web パッケージ](#0.2__Toc253429293 "_Toc253429293")  
[Web.config 変換](#0.2__Toc253429294 "_Toc253429294")  
[データベースの配置](#0.2__Toc253429295 "_Toc253429295")  
[ワンクリックによる Web アプリケーションの発行](#0.2__Toc253429296 "_Toc253429296")  
[リソース](#0.2__Toc253429297 "_Toc253429297")

**[免責事項](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>コアサービス

ASP.NET 4 では、出力キャッシュやセッション状態ストレージなどのコア ASP.NET サービスを向上させる多くの機能が導入されています。

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>Web.config ファイルのリファクタリング

Ajax、ルーティング、IIS 7 との統合などの新機能が追加されたため、Web アプリケーションの構成が含まれている `Web.config` ファイルは、.NET Framework の過去数回のリリースで大幅に増加しています。 これにより、Visual Studio のようなツールを使用せずに、新しい Web アプリケーションを構成したり、起動したりすることが難しくなりました。 .NET Framework 4 では、主要な構成要素が `machine.config` ファイルに移動され、アプリケーションはこれらの設定を継承するようになりました。 これにより、ASP.NET 4 アプリケーションの `Web.config` ファイルを空にするか、次の行だけを含めることができます。これは、アプリケーションが対象とするフレームワークのバージョンを Visual Studio に対して指定します。

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>拡張可能な出力キャッシュ

ASP.NET 1.0 がリリースされてから、出力キャッシュによって、生成されたページ、コントロール、および HTTP 応答の出力をメモリに格納できるようになりました。 後続の Web 要求では、ASP.NET は、出力をゼロから再生成するのではなく、メモリから生成された出力を取得することで、コンテンツをより迅速に提供できます。 ただし、この方法には制限があります。生成されたコンテンツは常にメモリに格納される必要があり、大量のトラフィックが発生しているサーバーでは、出力キャッシュによって消費されるメモリが Web アプリケーションの他の部分からのメモリ要求と競合する可能性があります。

ASP.NET 4 では、出力キャッシュに拡張ポイントを追加して、1つまたは複数のカスタム出力キャッシュプロバイダーを構成することができます。 出力キャッシュプロバイダーは、任意のストレージ機構を使用して HTML コンテンツを永続化できます。 これにより、ローカルまたはリモートのディスク、クラウドストレージ、および分散キャッシュエンジンを含むさまざまな永続化メカニズムに対して、カスタムの出力キャッシュプロバイダーを作成できます。

カスタム出力キャッシュプロバイダーは、新しい system.servicemodel*プロバイダー*型から派生したクラスとして作成します。 次の例に示すように、 *outputCache*要素の新しい*providers*サブセクションを使用して、`Web.config` ファイルにプロバイダーを構成できます。

[!code-xml[Main](overview/samples/sample2.xml)]

ASP.NET 4 の既定では、すべての HTTP 応答、表示ページ、およびコントロールは、前の例で示したように、メモリ内の出力キャッシュを使用します。前の例では、 *defaultprovider を*属性が AspNetInternalProvider に設定されています。 *Defaultprovider を*に別のプロバイダー名を指定することで、Web アプリケーションに使用される既定の出力キャッシュプロバイダーを変更できます。

さらに、1つのコントロールと要求ごとに異なる出力キャッシュプロバイダーを選択できます。 さまざまな Web ユーザーコントロールに対して別の出力キャッシュプロバイダーを選択する最も簡単な方法は、次の例に示すように、コントロールディレクティブで新しい*providerName*属性を使用して宣言的に実行することです。

[!code-aspx[Main](overview/samples/sample3.aspx)]

HTTP 要求に別の出力キャッシュプロバイダーを指定する場合は、もう少し作業が必要です。 プロバイダーを宣言的に指定する代わりに、`Global.asax` ファイルの新しい*Getouputcacheprovidername*メソッドをオーバーライドして、特定の要求に対して使用するプロバイダーをプログラムで指定します。 その方法を次の例に示します。

[!code-csharp[Main](overview/samples/sample4.cs)]

ASP.NET 4 に対する出力キャッシュプロバイダーの拡張機能が追加されたため、Web サイトに対してより積極的でインテリジェントな出力キャッシュ戦略を推進できるようになりました。 たとえば、サイトの "上位 10" ページをメモリにキャッシュし、ディスク上のトラフィックを減らすページをキャッシュできるようになりました。 または、表示されたページのさまざまな組み合わせをキャッシュできますが、分散キャッシュを使用して、フロントエンド Web サーバーからメモリ消費がオフロードされるようにします。

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>Web アプリケーションの自動起動

一部の Web アプリケーションでは、最初の要求を提供する前に、大量のデータを読み込んだり、高負荷の初期化処理を実行したりする必要があります。 以前のバージョンの ASP.NET では、このような状況については、ASP.NET アプリケーションを "ウェイクアップ" するカスタムアプローチを考案し、`Global.asax` ファイルの*Load メソッド\_アプリケーション*の実行中に初期化コードを実行する必要がありました。

Windows Server 2008 R2 の IIS 7.5 で ASP.NET 4 が実行されている場合、このシナリオに直接対処する*自動開始*という新しいスケーラビリティ機能を利用できます。 自動開始機能は、アプリケーションプールを起動し、ASP.NET アプリケーションを初期化して、HTTP 要求を受け入れるための制御されたアプローチを提供します。

> [!NOTE] 
> 
> Iis 7.5 用の IIS アプリケーションのウォームアップモジュール
> 
> IIS チームは、IIS 7.5 用のアプリケーションのウォームアップモジュールの最初のベータテストバージョンをリリースしました。 これにより、前に説明したよりも簡単にアプリケーションを準備できます。 カスタムコードを記述する代わりに、Web アプリケーションがネットワークからの要求を受け入れる前に実行するリソースの Url を指定します。 このウォームアップは、iis サービスの開始時に発生します (IIS アプリケーションプールを*Always running*として構成した場合)。また、iis ワーカープロセスがリサイクルされるときにも発生します。 リサイクル中、古い IIS ワーカープロセスは、新たに起動されたワーカープロセスが完全に動作するようになってから、アプリケーションで中断やその他の問題が発生しないようにします。 このモジュールは、バージョン2.0 以降の任意のバージョンの ASP.NET で動作することに注意してください。
> 
> 詳細については、IIS.net Web サイトの「[アプリケーションのウォームアップ](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)」を参照してください。 ウォームアップ機能の使用方法を示すチュートリアルについては、IIS.net Web サイトの「 [IIS 7.5 アプリケーションのウォームアップモジュールでのはじめに](https://www.iis.net/learn/manage)」を参照してください。

自動開始機能を使用するには、iis 管理者が、`applicationHost.config` ファイルの次の構成を使用して、IIS 7.5 のアプリケーションプールを自動的に開始するように設定します。

[!code-xml[Main](overview/samples/sample5.xml)]

1つのアプリケーションプールに複数のアプリケーションを含めることができるため、`applicationHost.config` ファイルの次の構成を使用して、個々のアプリケーションを自動的に開始するように指定します。

[!code-xml[Main](overview/samples/sample6.xml)]

IIS 7.5 サーバーがコールドスタートされるか、個々のアプリケーションプールがリサイクルされるときに、IIS 7.5 は `applicationHost.config` ファイルの情報を使用して、どの Web アプリケーションを自動的に開始する必要があるかを判断します。 自動開始用にマークされているアプリケーションごとに、IIS 7.5 は ASP.NET 4 に要求を送信して、アプリケーションが一時的に HTTP 要求を受け付けない状態でアプリケーションを起動します。 この状態になると、ASP.NET は*Serviceautostartprovider*属性で定義されている型 (前の例で示したように) をインスタンス化し、そのパブリックエントリポイントを呼び出します。

次の例に示すように、 *IProcessHostPreloadClient*インターフェイスを実装することによって、必要なエントリポイントでマネージ自動開始型を作成します。

[!code-csharp[Main](overview/samples/sample7.cs)]

*プリロード*メソッドで初期化コードを実行し、メソッドから制御が戻った後、ASP.NET アプリケーションは要求を処理する準備ができています。

IIS .5 と ASP.NET 4 に自動開始する機能が追加されたため、最初の HTTP 要求を処理する前に、コストの高いアプリケーションの初期化を実行するための明確なアプローチができました。 たとえば、新しい自動開始機能を使用してアプリケーションを初期化し、アプリケーションが初期化され、HTTP トラフィックを受け入れる準備ができたことをロードバランサーに通知することができます。

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>ページを永続的にリダイレクトする

Web アプリケーションでは、時間の経過と共にページやその他のコンテンツを移動するのが一般的です。これにより、検索エンジンに古いリンクが蓄積される可能性があります。 ASP.NET では、開発者は、要求を新しい URL に転送するために、を使用して以前の Url への要求を処理しました *。* ただし、*リダイレクト*メソッドは Http 302 Found (一時的なリダイレクト) 応答を発行します。これにより、ユーザーが古い url にアクセスしようとしたときに http ラウンドトリップが追加されます。

ASP.NET 4 は、次の例に示すように、永続的に移動された HTTP 301 を簡単に発行できるようにする新しい*Redirectpermanent*ヘルパーメソッドを追加します。

[!code-csharp[Main](overview/samples/sample8.cs)]

永続的なリダイレクトを認識する検索エンジンとその他のユーザーエージェントは、コンテンツに関連付けられている新しい URL を格納します。これにより、一時的なリダイレクトのためにブラウザーによって行われる不要なラウンドトリップが不要になります。

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>セッション状態の圧縮

ASP.NET には、Web ファーム全体にセッション状態を格納するための既定のオプションが2つ用意されています。アウトプロセスセッション状態サーバーを呼び出すセッション状態プロバイダーと、データを Microsoft SQL Server データベースに格納するセッション状態プロバイダーです。 どちらのオプションでも、Web アプリケーションのワーカープロセスの外部に状態情報が格納されるため、リモートストレージに送信する前にセッション状態をシリアル化する必要があります。 開発者がセッション状態で保存する情報の量によっては、シリアル化されたデータのサイズが非常に大きくなることがあります。

ASP.NET 4 では、両方の種類のアウトプロセスセッション状態プロバイダーに新しい圧縮オプションが導入されています。 次の例に示されている*compressionEnabled*構成オプションが*true*に設定されている場合、ASP.NET は、.NET Framework *GZipStream*クラスを使用して、シリアル化されたセッション状態を圧縮 (および圧縮解除) します。

[!code-xml[Main](overview/samples/sample9.xml)]

`Web.config` ファイルに新しい属性を簡単に追加することで、Web サーバー上に予備の CPU サイクルがあるアプリケーションでは、シリアル化されたセッション状態データのサイズを大幅に削減することができます。

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>許容される Url の範囲を拡張する

ASP.NET 4 では、アプリケーションの Url のサイズを拡張するための新しいオプションが導入されています。 以前のバージョンのでは、NTFS ファイルパスの制限に基づいて、制約された URL パスの長さを260文字に ASP.NET していました。 ASP.NET 4 では、2つの新しい*httpRuntime*構成属性を使用して、アプリケーションに合わせてこの制限を増やす (または減らす) ことができます。 次の例では、これらの新しい属性を示します。

[!code-xml[Main](overview/samples/sample10.xml)]

長いまたは短いパス (プロトコル、サーバー名、クエリ文字列を含まない URL の部分) を許可するには、 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 属性を変更します。 より長いまたは短いクエリ文字列を許可するには、 *[Maxquerystringlength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 属性の値を変更します。

ASP.NET 4 では、URL 文字チェックで使用される文字を構成することもできます。 ASP.NET が URL のパス部分で無効な文字を検出すると、要求が拒否され、HTTP 400 エラーが発行されます。 以前のバージョンの ASP.NET では、URL 文字のチェックは固定された文字セットに限定されていました。 ASP.NET 4 では、次の例に示すように、 *httpRuntime* configuration 要素の新しい*Requestpathinvalidcharacters*属性を使用して、有効な文字のセットをカスタマイズできます。

[!code-xml[Main](overview/samples/sample11.xml)]

既定では、 *Requestpathinvalidcharacters*属性は8文字を無効として定義します。 (既定で*Requestpathinvalidcharacters*に割り当てられている文字列では、`Web.config` ファイルは XML ファイルであるため、より小さい (&lt;)、より大きい (&gt;)、アンパサンド (&amp;) の各文字がエンコードされます。必要に応じて、無効な文字のセットをカスタマイズできます。

> [!NOTE]
> 注 ASP.NET 4 は、IETF から0x1F への ASCII 範囲の文字を含む URL パスを常に拒否します。これは、IETF の RFC 2396 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)) で定義されている無効な url 文字であるためです。 IIS 6 以降を実行する Windows Server のバージョンでは、http.sys プロトコルデバイスドライバーは、これらの文字で Url を自動的に拒否します。

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>拡張可能な要求の検証

ASP.NET 要求の検証では、クロスサイトスクリプティング (XSS) 攻撃で一般的に使用される文字列について、受信 HTTP 要求データを検索します。 潜在的な XSS 文字列が検出された場合、要求の検証は疑わしい文字列にフラグを指定し、エラーを返します。 組み込みの要求検証では、XSS 攻撃で使用される最も一般的な文字列を検出した場合にのみ、エラーが返されます。 以前に XSS 検証をより積極的に実行しようとすると、誤検知が多くなりました。 ただし、顧客は、より積極的な要求の検証や、特定のページまたは特定の種類の要求に対して XSS チェックを意図的に緩和する必要がある場合があります。

ASP.NET 4 では、要求検証機能が拡張され、カスタムの要求検証ロジックを使用できるようになりました。 要求の検証を拡張するには *、新しい httpRuntime*型から派生するクラスを作成し、カスタム型を使用するように (`Web.config` ファイルのセクションで) アプリケーションを構成します。 次の例は、カスタムの要求検証クラスを構成する方法を示しています。

[!code-xml[Main](overview/samples/sample12.xml)]

新しい*Requestvalidationtype*属性には、カスタム要求の検証を提供するクラスを指定する標準 .NET Framework 型識別子文字列が必要です。 各要求に対して、ASP.NET はカスタム型を呼び出して、受信 HTTP 要求データの各部分を処理します。 受信 URL、すべての HTTP ヘッダー (cookie とカスタムヘッダーの両方)、およびエンティティ本体は、次の例に示すようなカスタム要求検証クラスによってすべて検査できます。

[!code-csharp[Main](overview/samples/sample13.cs)]

受信 HTTP データの一部を検査しない場合は、要求検証クラスをフォールバックして、ASP.NET の既定の要求の検証を実行するだけで base を呼び出すことができます *。IsValidRequestString。*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>オブジェクトキャッシュとオブジェクトキャッシュの拡張性

最初のリリース以降、ASP.NET には強力なメモリ内オブジェクトキャッシュ () が含まれて*いました*。 キャッシュの実装は、非 Web アプリケーションで使用されていることがよくありました。 ただし、ASP.NET オブジェクトキャッシュを使用できるようにするために、Windows フォームまたは WPF アプリケーションが `System.Web.dll` への参照を含めるのは厄介です。

すべてのアプリケーションでキャッシュを使用できるようにするために、.NET Framework 4 では新しいアセンブリ、新しい名前空間、いくつかの基本型、および具体的なキャッシュ実装が導入されています。 新しい `System.Runtime.Caching.dll` アセンブリに*は、system.string 名前空間*の新しいキャッシュ API が含まれています。 名前空間には、クラスの2つのコアセットが含まれています。

- 任意の種類のカスタムキャッシュ実装を構築するための基盤を提供する抽象型。
- 具体的なメモリ内オブジェクトキャッシュの実装 (system.string*キャッシュ*クラス) を実行します。

新しい*Memorycache*クラスは ASP.NET キャッシュに密接に基づいてモデル化されており、内部キャッシュエンジンのロジックの多くを ASP.NET と共有しています。 カスタムキャッシュの開発をサポートするために、ASP.NET のパブリックキャッシュ Api が更新されまし*たが、* この*キャッシュ*オブジェクトを使用している場合は、新しい api での使い慣れた概念がわかります。

新しい*Memorycache*クラスとサポートする基本 api の詳細については、ドキュメント全体が必要になります。 ただし、次の例は、新しいキャッシュ API のしくみを示しています。 この例は、`System.Web.dll`に依存せずに Windows フォームアプリケーション用に記述されています。

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>Extensible HTML、URL、および HTTP ヘッダーエンコード

ASP.NET 4 では、次の一般的なテキストエンコードタスク用のカスタムエンコードルーチンを作成できます。

- HTML エンコード。
- URL エンコード。
- HTML 属性のエンコード。
- 送信 HTTP ヘッダーをエンコードしています。

カスタムエンコーダーを作成するには、次の例に示すように *、新しい ASP.NET*型から派生し、次の例に示すように、`Web.config` ファイルの*httpRuntime*セクションでカスタム型を使用するように構成します。

[!code-xml[Main](overview/samples/sample15.xml)]

カスタムエンコーダーが構成されると、 *ASP.NET クラスまた*は*HttpUtility*クラスのパブリックエンコードメソッドが呼び出されるたびに、カスタムエンコード実装が自動的に呼び出されます。 これにより、Web 開発チームの1つの部分で、アグレッシブな文字エンコーディングを実装するカスタムエンコーダーを作成できます。一方、Web 開発チームの残りの部分では、引き続きパブリック ASP.NET encoding Api を使用します。 *HttpRuntime*要素でカスタムエンコーダーを一元的に構成することで、パブリック ASP.NET encoding api からのすべてのテキストエンコード呼び出しがカスタムエンコーダー経由でルーティングされることが保証されます。

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>1つのワーカープロセスにおける個々のアプリケーションのパフォーマンス監視

1台のサーバーでホストできる Web サイトの数を増やすために、多くのホスト側は、1つのワーカープロセスで複数の ASP.NET アプリケーションを実行します。 ただし、複数のアプリケーションが1つの共有ワーカープロセスを使用している場合、サーバー管理者は、問題が発生している個々のアプリケーションを特定するのが困難です。

ASP.NET 4 は、CLR によって導入された新しいリソース監視機能を活用しています。 この機能を有効にするには、次の XML 構成スニペットを `aspnet.config` 構成ファイルに追加します。

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> .NET Framework がインストールされているディレクトリに `aspnet.config` ファイルがあることに注意してください。 これは `Web.config` ファイルではありません。

*AppDomainResourceMonitoring*機能が有効になっている場合、"ASP.NET Applications" パフォーマンスカテゴリには、[ *% マネージプロセッサ時間*] と [*使用されたマネージメモリ*] の2つの新しいパフォーマンスカウンターが用意されています。 これらのパフォーマンスカウンターはどちらも、新しい CLR アプリケーションドメインリソース管理機能を使用して、個々の ASP.NET アプリケーションの推定 CPU 時間とマネージメモリ使用率を追跡します。 その結果、ASP.NET 4 では、管理者は1つのワーカープロセスで実行されている個々のアプリケーションのリソース消費量をより詳細に表示できるようになりました。

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>マルチ ターゲット

.NET Framework の特定のバージョンを対象とするアプリケーションを作成できます。 ASP.NET 4 では、`Web.config` ファイルの*コンパイル*要素に新しい属性を使用して、.NET Framework 4 以降を対象にすることができます。 .NET Framework 4 を明示的に対象としており、オプションの要素を `Web.config` ファイルに含める場合 (たとえば、 *system.string のエントリ*など)、これらの要素は .NET Framework 4 に対して適切である必要があります。 (.NET Framework 4 を明示的に対象にしていない場合、ターゲットフレームワークは、`Web.config` ファイル内のエントリがないことから推測されます)。

次の例は、`Web.config` ファイルの*コンパイル*要素での*targetframework*属性の使用方法を示しています。

[!code-xml[Main](overview/samples/sample17.xml)]

.NET Framework の特定のバージョンを対象とする場合は、次の点に注意してください。

- .NET Framework 4 アプリケーションプールでは、`Web.config` ファイルに*Targetframework*属性が含まれていない場合、または `Web.config` ファイルが見つからない場合、ASP.NET ビルドシステムはターゲットとして .NET Framework 4 を想定します。 (.NET Framework 4 で実行されるように、アプリケーションのコーディングを変更することが必要になる場合があります)。
- *Targetframework*属性を含め、`Web.config` ファイルで*システムの codeDom*要素が定義されている場合、このファイルには .NET Framework 4 の正しいエントリが含まれている必要があります。
- *Aspnet\_コンパイラ*コマンドを使用してアプリケーション (ビルド環境など) をプリコンパイルする場合は、ターゲットフレームワークに対して、正しいバージョンの*aspnet\_コンパイラ*コマンドを使用する必要があります。 .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) に同梱されているコンパイラを使用して、.NET Framework 3.5 以前のバージョン用にコンパイルします。 .NET Framework 4 に付属するコンパイラを使用して、そのフレームワークを使用して、またはそれ以降のバージョンを使用して作成されたアプリケーションをコンパイルします。
- 実行時に、コンパイラはコンピューターにインストールされている最新のフレームワークアセンブリ (したがって GAC 内) を使用します。 後でフレームワークに対して更新が行われた場合 (たとえば、仮定のバージョン4.1 がインストールされている場合)、 *targetframework*属性が下位バージョン (4.0 など) を対象としていても、新しいバージョンのフレームワークの機能を使用できます。 (ただし、Visual Studio 2010 のデザイン時、または*aspnet\_コンパイラ*コマンドを使用すると、フレームワークの新しい機能を使用するとコンパイラエラーが発生します)。

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>Web フォームと MVC に含まれる jQuery

Web フォームと MVC の両方に対応した Visual Studio テンプレートには、オープンソースの jQuery ライブラリが含まれています。 新しい web サイトまたはプロジェクトを作成すると、次の3つのファイルを含む Scripts フォルダーが作成されます。

- jQuery-1.4.1 –ユーザーが判読できる、わかりやすいバージョンの jQuery ライブラリ。
- jQuery-14.1:、jQuery ライブラリの縮小版です。
- jQuery-は、jQuery ライブラリの Intellisense ドキュメントファイルを対象としています。

アプリケーションの開発中に、指定されていないバージョンの jQuery を含めます。 運用アプリケーション用の jQuery の縮小版を含めます。

たとえば、次の Web フォームページでは、jQuery を使用して、フォーカスがあるときに ASP.NET TextBox コントロールの背景色を黄色に変更する方法を示しています。

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>Content Delivery Network サポート

Microsoft Ajax Content Delivery Network (CDN) を使用すると、ASP.NET Ajax および jQuery スクリプトを Web アプリケーションに簡単に追加できます。 たとえば、次のように Ajax.microsoft.com を指す `<script>` タグをページに追加するだけで、jQuery ライブラリの使用を開始できます。

[!code-html[Main](overview/samples/sample19.html)]

Microsoft Ajax CDN を利用すると、Ajax アプリケーションのパフォーマンスを大幅に向上させることができます。 Microsoft Ajax CDN の内容は、世界中のサーバーにキャッシュされます。 また、Microsoft Ajax CDN を使用すると、異なるドメインにある Web サイト用に、キャッシュ内の JavaScript ファイルをブラウザーで再利用できます。

Microsoft Ajax Content Delivery Network は、Secure Sockets Layer を使用して web ページを提供する必要がある場合に、SSL (HTTPS) をサポートします。

CDN が使用できない場合は、フォールバックを実装します。 フォールバックをテストします。

Microsoft Ajax CDN の詳細については、次の web サイトを参照してください。

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager は、Microsoft Ajax CDN をサポートしています。 1つのプロパティ (EnableCdn プロパティ) を設定するだけで、CDN からすべての ASP.NET framework JavaScript ファイルを取得できます。

[!code-aspx[Main](overview/samples/sample20.aspx)]

EnableCdn プロパティを true に設定すると、ASP.NET フレームワークは、検証および UpdatePanel に使用されるすべての JavaScript ファイルを含むすべての ASP.NET framework JavaScript ファイルを CDN から取得します。 この1つのプロパティを設定すると、web アプリケーションのパフォーマンスに大きな影響を与える可能性があります。

Webresource.axd 属性を使用して、独自の JavaScript ファイルの CDN パスを設定できます。 新しい CdnPath プロパティは、EnableCdn プロパティを true に設定したときに使用される CDN へのパスを指定します。

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager の明示的なスクリプト

以前は、ASP.NET ScriptManger を使用した場合、モノリシック ASP.NET Ajax ライブラリ全体を読み込む必要がありました。 AjaxFrameworkMode の新しいプロパティを利用することで、ASP.NET Ajax ライブラリのどのコンポーネントが読み込まれるかを厳密に制御し、必要な ASP.NET Ajax ライブラリのコンポーネントのみを読み込むことができます。

AjaxFrameworkMode プロパティには、次の値を設定できます。

- 有効-ScriptManager コントロールに Microsoftajax.js スクリプトファイルが自動的に含まれることを指定します。これは、すべてのコアフレームワークスクリプト (レガシ動作) の結合されたスクリプトファイルです。
- Disabled-Microsoft Ajax スクリプトのすべての機能が無効になっていること、および ScriptManager コントロールがスクリプトを自動的に参照していないことを指定します。
- Explicit--ページに必要な個別のフレームワークコアスクリプトファイルへのスクリプト参照を明示的に含めること、および各スクリプトファイルに必要な依存関係への参照を含めることを指定します。

たとえば、AjaxFrameworkMode プロパティを明示的な値に設定した場合は、必要な特定の ASP.NET Ajax コンポーネントスクリプトを指定できます。

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web フォーム

ASP.NET 1.0 のリリース以降、Web フォームは ASP.NET のコア機能になっています。 ASP.NET 4 のこの領域には、次のような多くの機能強化が行われています。

- *メタ*タグを設定する機能。
- ビューステートをより詳細に制御できます。
- ブラウザー機能を簡単に操作できるようになりました。
- Web フォームでの ASP.NET ルーティングの使用のサポート。
- 生成された Id をより詳細に制御できます。
- 選択された行をデータコントロールで永続化する機能。
- *FormView*コントロールと*ListView*コントロールでのレンダリングされた HTML の詳細な制御。
- データソースコントロールのフィルター処理のサポート。

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>メタタグを MetaDescription プロパティとページに設定します。

ASP.NET 4 は、*ページ*クラスに*メタキーワード*と*MetaDescription*の2つのプロパティを追加します。 これら2つのプロパティは、次の例に示すように、ページ内の対応する*メタ*タグを表します。

[!code-aspx[Main](overview/samples/sample23.aspx)]

これら2つのプロパティは、ページの*Title*プロパティと同じように動作します。 次の規則に従います。

1. *Head*要素に、プロパティ名に一致する*メタ*タグがない場合 (つまり、 *MetaDescription*の場合は name = "keywords"、*これらのプロパティ*が設定されていないことを意味します)、 *meta*タグは表示されるときにページに追加されます。
2. これらの名前を持つ*メタ*タグが既に存在する場合、これらのプロパティは既存のタグの内容の get および set メソッドとして機能します。

これらのプロパティは実行時に設定できます。これにより、データベースまたは他のソースからコンテンツを取得できます。また、タグを動的に設定して、特定のページの内容を示すことができます。

次の例のように、Web フォームページのマークアップの上部にある *@ Page*ディレクティブで*Keywords*および*Description*プロパティを設定することもできます。

[!code-aspx[Main](overview/samples/sample24.aspx)]

これにより、ページで既に宣言されている*メタ*タグの内容がオーバーライドされます。

Description *meta*タグの内容は、Google での検索リストのプレビューを改善するために使用されます。 (詳細については、Google 作り直し Central ブログの「 [meta description を使用したスニペットの改善](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html)」を参照してください)。Google と Windows Live Search では、キーワードの内容を何も使用しませんが、他の検索エンジンでは使用できます。 詳細については、検索エンジンガイド Web サイトの「 [Meta Keywords アドバイス](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)」を参照してください。

これらの新しいプロパティは単純な機能ですが、これらのプロパティを手動で追加したり、独自のコードを記述して*meta*タグを作成したりする必要はありません。

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>個々のコントロールのビューステートを有効にする

既定では、ページに対してビューステートが有効になっています。これにより、ページ上の各コントロールは、アプリケーションで必要でない場合でも、ビューステートを保存する可能性があります。 ビューステートデータは、ページによって生成されるマークアップに含まれ、クライアントへのページの送信とポストバックにかかる時間が長くなります。 必要以上に多くのビューステートを格納すると、パフォーマンスが大幅に低下する可能性があります。 以前のバージョンの ASP.NET では、開発者はページサイズを減らすために個々のコントロールのビューステートを無効にすることができましたが、個別のコントロールに対して明示的に行う必要がありました。 ASP.NET 4 では、Web サーバーコントロールに*Viewstatemode*プロパティが含まれています。このプロパティを使用すると、ビューステートを既定で無効にして、ページに必要なコントロールに対してのみ有効にすることができます。

*Viewstatemode*プロパティは、次の3つの値を持つ列挙を受け取ります。*Enabled*、 *Disabled*、および*Inherit*。 *Enabled*は、そのコントロールおよび*継承*するように設定されている子コントロール、または何も設定されていない子コントロールのビューステートを有効にします。 *Disabled*はビューステートを無効にし、*継承*はコントロールが親コントロールから*viewstatemode*設定を使用することを指定します。

*Viewstatemode*プロパティがどのように機能するかを次の例に示します。 次のページのコントロールのマークアップとコードには、 *Viewstatemode*プロパティの値が含まれています。

[!code-aspx[Main](overview/samples/sample25.aspx)]

ご覧のように、このコードは PlaceHolder1 コントロールのビューステートを無効にします。 子 label1 コントロールは、このプロパティ値を継承します (コントロールの*Viewstatemode*の既定値は*Inherit*です)。したがって、ビューステートは保存されません。 PlaceHolder2 コントロールでは、 *Viewstatemode*が Enabled に設定されて*いる*ため、label2 はこのプロパティを継承し、ビューステートを保存します。 ページが最初に読み込まれるときに、両方の*ラベル*コントロールの*Text*プロパティが文字列 "[DynamicValue]" に設定されます。

これらの設定の効果は、ページが初めて読み込まれるときに、ブラウザーに次の出力が表示されることです。

無効 `: [DynamicValue]`

有効:`[DynamicValue]`

ただし、ポストバック後、次の出力が表示されます。

無効 `: [DeclaredValue]`

有効:`[DynamicValue]`

Label1 コントロール ( *Viewstatemode*値が*Disabled*に設定されている) は、コードで設定された値を保持していません。 ただし、label2 コントロール ( *Viewstatemode*値が Enabled に設定され*て*いる) は、その状態を保持しています。

次の例のように、 *@ Page*ディレクティブで*viewstatemode*を設定することもできます。

[!code-aspx[Main](overview/samples/sample26.aspx)]

*Page*クラスは、別のコントロールです。これは、ページ内の他のすべてのコントロールの親コントロールとして機能します。 *Page*のインスタンスに対して*viewstatemode*の既定値が*有効になっ*ています。 コントロールが既定で*継承*するため、 *viewstatemode*を page レベルまたは control level に設定しない限り、コントロールは*Enabled*プロパティ値を継承します。

*Viewstatemode*プロパティの値は、 *enableviewstate*プロパティが*true*に設定されている場合にのみビューステートを維持するかどうかを決定します。 *Enableviewstate*プロパティが*false*に設定されている場合、 *viewstatemode*が*有効*に設定されていても、ビューステートは維持されません。

この機能を使用するには、マスターページの*ContentPlaceHolder*コントロールを使用することをお勧めします。この場合、マスターページの*viewstatemode*を*無効*に設定し、ビューステートを必要とするコントロールを含む*ContentPlaceHolder*コントロールに対して個別に有効にすることができます。

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>ブラウザー機能の変更点

ASP.NET は、*ブラウザー機能*と呼ばれる機能を使用してサイトを参照するためにユーザーが使用しているブラウザーの機能を決定します。 ブラウザーの機能は、 *Httpbrowsercapabilities*オブジェクト (*要求*によって公開されます) によって表されます。 たとえば、 *Httpbrowsercapabilities*オブジェクトを使用して、現在のブラウザーの型とバージョンが JavaScript の特定のバージョンをサポートしているかどうかを判断できます。 または、 *Httpbrowsercapabilities*オブジェクトを使用して、要求がモバイルデバイスから送信されたものかどうかを判断することもできます。

*Httpbrowsercapabilities*オブジェクトは、一連のブラウザー定義ファイルによって駆動されます。 これらのファイルには、特定のブラウザーの機能に関する情報が含まれています。 ASP.NET 4 では、これらのブラウザー定義ファイルが更新され、最近導入されたブラウザーとデバイス (Google Chrome、モーション BlackBerry スマートフォン、Apple iPhone など) に関する情報が含まれるようになりました。

次の一覧に、新しいブラウザー定義ファイルを示します。

- *blackberry.browser*
- *chrome.browser*
- *Default.browser*
- *firefox.browser*
- *gateway.browser*
- *generic.browser*
- *ie.browser*
- *iemobile.browser*
- *iphone.browser*
- *opera.browser*
- *safari.browser*

#### <a name="using-browser-capabilities-providers"></a>ブラウザー機能プロバイダーの使用

ASP.NET バージョン 3.5 Service Pack 1 では、次の方法でブラウザーに用意されている機能を定義できます。

- コンピューターレベルでは、次のフォルダーに `.browser` XML ファイルを作成または更新します。

- [!code-console[Main](overview/samples/sample27.cmd)]

- ブラウザー機能を定義したら、Visual Studio コマンドプロンプトから次のコマンドを実行して、ブラウザー機能アセンブリをリビルドし、GAC に追加します。

- [!code-console[Main](overview/samples/sample28.cmd)]

- 個々のアプリケーションについては、アプリケーションの `App_Browsers` フォルダーに `.browser` ファイルを作成します。

これらの方法では、XML ファイルを変更する必要があります。また、コンピューターレベルの変更の場合は、aspnet\_regbrowsers プロセスを実行した後でアプリケーションを再起動する必要があります。

ASP.NET 4 には、*ブラウザー機能プロバイダー*と呼ばれる機能が含まれています。 名前が示すように、これによってプロバイダーを作成し、独自のコードを使用してブラウザーの機能を決定することができます。

実際には、開発者がカスタムブラウザー機能を定義していないことがよくあります。 ブラウザーファイルを更新するのは困難ですが、更新プロセスはかなり複雑であり、`.browser` ファイルの XML 構文は、使用や定義が複雑になることがあります。 一般的なブラウザー定義の構文、または最新のブラウザー定義が含まれているデータベース、またはこのようなデータベースの Web サービスでも、この処理がはるかに簡単になります。 新しいブラウザー機能プロバイダーの機能により、これらのシナリオが可能になり、サードパーティの開発者にとって実用的になります。

新しい ASP.NET 4 ブラウザー機能プロバイダー機能を使用するには、2つの主な方法があります。 ASP.NET browser 機能定義機能を拡張するか、全体を置き換えます。 以下のセクションでは、最初に機能を置き換える方法と、その機能を拡張する方法について説明します。

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>ASP.NET Browser 機能の置き換え

ASP.NET browser 機能の定義機能を完全に置き換えるには、次の手順を実行します。

1. 次の例のように、 *HttpCapabilitiesProvider*から派生し、 *getbrowsercapabilities*メソッドをオーバーライドするプロバイダークラスを作成します。 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    この例のコードでは、ブラウザーという名前の機能だけを指定し、その機能を MyCustomBrowser に設定する新しい*Httpbrowsercapabilities*オブジェクトを作成します。
2. プロバイダーをアプリケーションに登録します。 

    アプリケーションでプロバイダーを使用するには、`Web.config` または `Machine.config` ファイルの*Browsercaps*セクションに*provider*属性を追加する必要があります。 (特定のモバイルデバイスのフォルダーなど、アプリケーション内の特定のディレクトリの*場所*要素にプロバイダー属性を定義することもできます)。次の例は、構成ファイルで*provider*属性を設定する方法を示しています。

    [!code-xml[Main](overview/samples/sample30.xml)]

    新しいブラウザー機能の定義を登録するもう1つの方法は、次の例に示すようにコードを使用することです。

    [!code-csharp[Main](overview/samples/sample31.cs)]

    このコードは、`Global.asax` ファイルの*Application\_Start*イベントで実行する必要があります。 *BrowserCapabilitiesProvider*クラスの変更は、アプリケーション内のコードを実行する前に行う必要があります。これにより、キャッシュが解決済みの*使用*オブジェクトに対して有効な状態のままになるようにします。

#### <a name="caching-the-httpbrowsercapabilities-object"></a>HttpBrowserCapabilities オブジェクトをキャッシュしています

前の例には1つの問題があります。これは、 *Httpbrowsercapabilities*オブジェクトを取得するために、カスタムプロバイダーが呼び出されるたびにコードが実行されることを示しています。 これは、要求のたびに複数回発生する可能性があります。 この例では、プロバイダーのコードはそれほど多くありません。 ただし、 *Httpbrowsercapabilities*オブジェクトを取得するためにカスタムプロバイダーのコードが大きな作業を実行する場合は、パフォーマンスに影響する可能性があります。 これが行われないようにするには、 *Httpbrowsercapabilities*オブジェクトをキャッシュします。 次の手順に従います。

1. 次の例のように、 *HttpCapabilitiesProvider*から派生するクラスを作成します。 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    この例では、コードはカスタム BuildCacheKey メソッドを呼び出すことによってキャッシュキーを生成し、カスタム GetCacheTime メソッドを呼び出すことによってキャッシュの時間を取得します。 次に、解決された*Httpbrowsercapabilities*オブジェクトをキャッシュに追加します。 オブジェクトはキャッシュから取得して、カスタムプロバイダーを使用する後続の要求で再利用できます。
2. 前の手順の説明に従って、プロバイダーをアプリケーションに登録します。

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>ASP.NET Browser 機能の拡張機能

前のセクションでは、ASP.NET 4 で新しい*Httpbrowsercapabilities*オブジェクトを作成する方法について説明しています。 また、ASP.NET に既に存在するものに新しいブラウザー機能の定義を追加して、ASP.NET ブラウザー機能の機能を拡張することもできます。 これは、XML ブラウザー定義を使用せずに行うことができます。 次の手順では、その方法を示します。

1. 次の例に示すように、 *HttpCapabilitiesEvaluator*から派生し、 *getbrowsercapabilities*メソッドをオーバーライドするクラスを作成します。 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    このコードでは、まず、ASP.NET ブラウザーの機能を使用してブラウザーを識別します。 ただし、要求で定義されている情報に基づいてブラウザーが識別されない場合 (つまり、 *Httpbrowsercapabilities*オブジェクトの*browser*プロパティが "Unknown" という文字列の場合)、コードはカスタムプロバイダー (MyBrowserCapabilitiesEvaluator) を呼び出してブラウザーを識別します。
2. 前の例で説明したように、プロバイダーをアプリケーションに登録します。

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>既存の機能の定義に新しい機能を追加してブラウザー機能の機能を拡張する

カスタムブラウザー定義プロバイダーを作成し、新しいブラウザー定義を動的に作成するだけでなく、既存のブラウザー定義を拡張して機能を追加することもできます。 これにより、必要なものに近い定義を使用できますが、いくつかの機能がありません。 そのためには、次の手順に従います。

1. 次の例に示すように、 *HttpCapabilitiesEvaluator*から派生し、 *getbrowsercapabilities*メソッドをオーバーライドするクラスを作成します。 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    このコード例では、既存の ASP.NET *HttpCapabilitiesEvaluator*クラスを拡張し、次のコードを使用して、現在の要求定義と一致する*httpbrowsercapabilities*オブジェクトを取得します。

    [!code-csharp[Main](overview/samples/sample35.cs)]

    このコードでは、このブラウザーの機能を追加または変更できます。 新しいブラウザー機能を指定するには、次の2つの方法があります。

    - *使用*オブジェクトの*Capabilities*プロパティによって公開される*IDictionary*オブジェクトに、キーと値のペアを追加します。 前の例では、コードによってマルチタッチという名前の機能が追加され、値が*true*になります。
    - *使用*オブジェクトの既存のプロパティを設定します。 前の例では、コードによって*Frames*プロパティが*true*に設定されています。 このプロパティは、 *Capabilities*プロパティによって公開される*IDictionary*オブジェクトのアクセサーにすぎません。 

        > [!NOTE]
        > 注このモデルは、コントロールアダプターを含む*Httpbrowsercapabilities*の任意のプロパティに適用されます。
2. 前の手順で説明したように、プロバイダーをアプリケーションに登録します。

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4 でのルーティング

ASP.NET 4 では、Web フォームでのルーティングを使用するための組み込みサポートが追加されています。 ルーティングを使用すると、物理ファイルにマップされていない要求 Url を受け入れるようにアプリケーションを構成できます。 代わりに、ルーティングを使用して、ユーザーにとって意味のある Url を定義し、アプリケーションの検索エンジン最適化 (SEO) に役立てることができます。 たとえば、既存のアプリケーションに製品カテゴリを表示するページの URL は、次の例のようになります。

[!code-console[Main](overview/samples/sample36.cmd)]

ルーティングを使用すると、次の URL を使用して同じ情報を表示するようにアプリケーションを構成できます。

[!code-console[Main](overview/samples/sample37.cmd)]

ルーティングは、ASP.NET 3.5 SP1 以降で利用できます。 (ASP.NET 3.5 SP1 でルーティングを使用する方法の例については、Phil Haack のブログの「 [Routing With WebForms」を参照して](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "このエントリのタイトル。")ください)。ただし、ASP.NET 4 には、ルーティングを使用しやすくするための機能がいくつか含まれています。次に例を示します。

- *PageRouteHandler*クラス。ルートを定義するときに使用する単純な HTTP ハンドラーです。 クラスは、要求のルーティング先のページにデータを渡します。
- 新しいプロパティは、 *httprequest*と*ページの routedata*です。これは、 *httprequest データ*オブジェクトのプロキシです。 これらのプロパティを使用すると、ルートから渡された情報に簡単にアクセスできるようになります。
- 次の新しい式ビルダーは、次の新しい式ビルダーで定義されてい*ます。このビルダーおよび* *system.web..* .
- *Routeurl*。 ASP.NET サーバーコントロール内のルート url に対応する url を作成する簡単な方法を提供します。
- *Routevalue*。 *RouteContext*オブジェクトから情報を抽出する簡単な方法を提供します。
- *Routeparameter*クラスを使用すると、 *RouteContext*オブジェクトに含まれるデータをデータソースコントロールのクエリに簡単に渡すことができます ( [*formparameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)に似ています)。

#### <a name="routing-for-web-forms-pages"></a>Web フォームページのルーティング

次の例は、 *route*クラスの new *MapPageRoute*メソッドを使用して、Web フォームのルートを定義する方法を示しています。

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4 では、 *MapPageRoute*メソッドが導入されています。 次の例は、前の例で示した SearchRoute 定義に相当しますが、 *PageRouteHandler*クラスを使用します。

[!code-csharp[Main](overview/samples/sample39.cs)]

この例のコードでは、ルートを物理ページ (最初のルートの場合は `~/search.aspx`) にマップします。 また、最初のルート定義では、searchterm という名前のパラメーターを URL から抽出し、ページに渡す必要があることも指定しています。

*MapPageRoute*メソッドでは、次のメソッドオーバーロードがサポートされています。

- *MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*
- *MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*
- *MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*

*Checkphysicalurlaccess*パラメーターは、ルーティング先の物理ページ (この場合は default.aspx) のセキュリティアクセス許可、および受信 URL (この場合は search/{searchterm}) に対するアクセス許可をルートがチェックするかどうかを指定します。 *Checkphysicalurlaccess*の値が*false*の場合は、受信 URL のアクセス許可だけがチェックされます。 これらのアクセス許可は、次のような設定を使用して、`Web.config` ファイルで定義されます。

[!code-xml[Main](overview/samples/sample40.xml)]

この例の構成では、管理者ロールに属しているユーザーを除くすべてのユーザーに対して、物理的なページ `search.aspx` へのアクセスが拒否されます。 *Checkphysicalurlaccess*パラメーターが*true* (既定値) に設定されている場合、物理ページの検索はそのロールのユーザーに制限されているので、管理者ユーザーのみが URL にアクセスできます。 *Checkphysicalurlaccess*が*false*に設定されていて、サイトが前の例のように構成されている場合、認証されたすべてのユーザーは URL にアクセスできます。

#### <a name="reading-routing-information-in-a-web-forms-page"></a>Web フォームページでのルーティング情報の読み取り

Web フォームの物理ページのコードでは、次の2つの新しいプロパティを使用して、ルーティングによって URL から抽出された情報 (または別のオブジェクトによって*Routedata*オブジェクトに追加されたその他の情報) にアクセスできます。*HttpRequest*および*ページの routedata*。 (*ページの RouteData*は、 *HttpRequest. routedata routedata*をラップします)。次の例では、*ページの RouteData*を使用する方法を示します。

[!code-csharp[Main](overview/samples/sample41.cs)]

このコードは、前の例のルートで定義されているように、searchterm パラメーターに渡された値を抽出します。 次の要求 URL について考えてみましょう。

[!code-console[Main](overview/samples/sample42.cmd)]

この要求が行われると、"scott" という単語が `search.aspx` ページに表示されます。

#### <a name="accessing-routing-information-in-markup"></a>マークアップでのルーティング情報へのアクセス

前のセクションで説明したメソッドは、Web フォームページのコードでルートデータを取得する方法を示しています。 また、同じ情報にアクセスできるように、マークアップで式を使用することもできます。 式ビルダーは、宣言型コードを操作するための強力で洗練された方法です。 (詳細については、Phil Haack のブログの「[カスタム式ビルダーを使用した Express](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)の入力」を参照してください)。

ASP.NET 4 には、Web フォームルーティング用の2つの新しい式ビルダーが含まれています。 次の例は、これらの使用方法を示しています。

[!code-aspx[Main](overview/samples/sample43.aspx)]

この例では、 *routeurl*式を使用して、ルートパラメーターに基づく URL を定義しています。 これにより、完全な URL をマークアップにハードコーディングする必要がなくなり、後で URL 構造を変更しても、このリンクを変更する必要がなくなります。

このマークアップでは、前に定義したルートに基づいて、次の URL が生成されます。

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET は、入力パラメーターに基づいて、正しいルートを自動的に処理します (つまり、正しい URL を生成します)。 また、式にルート名を含めることもできます。これにより、使用するルートを指定できます。

*Routevalue*式を使用する方法を次の例に示します。

[!code-aspx[Main](overview/samples/sample45.aspx)]

このコントロールを含むページを実行すると、ラベルに "scott" という値が表示されます。

*Routevalue*式を使用すると、マークアップでルートデータを簡単に使用できるようになります。また、マークアップでは、より複雑なページの routevalue ["x"] 構文を使用する必要がなくなります。

#### <a name="using-route-data-for-data-source-control-parameters"></a>データソース管理パラメーターにルートデータを使用する

*Routeparameter*クラスを使用すると、データソースコントロール内のクエリのパラメーター値としてルートデータを指定できます。 これは、次の例に示すように、クラスと[よく似](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)ています。

[!code-aspx[Main](overview/samples/sample46.aspx)]

ルート パラメーターの searchterm の値が使用しての例では、@companynameパラメーター、 *選択* ステートメント。

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>クライアント Id の設定

新しい*Clientidmode*プロパティは、ASP.NET の長期間の問題に対処します。つまり、コントロールがレンダリングする要素の*id*属性を作成する方法を説明します。 アプリケーションにこれらの要素を参照するクライアントスクリプトが含まれている場合は、表示される要素の*id*属性を知っておくことが重要です。

Web サーバーコントロール用に表示される HTML の*id*属性は、コントロールの*ClientID*プロパティに基づいて生成されます。 ASP.NET 4 までは、 *ClientID*プロパティから*id*属性を生成するアルゴリズムは、名前付けコンテナー (存在する場合) と id を連結し、(データコントロールと同様に) 繰り返し制御する場合にプレフィックスと連番を追加します。 これは、ページ内のコントロールの Id が一意であることが常に保証されていますが、アルゴリズムによって、予測不可能な制御 Id が生成されたため、クライアントスクリプトでの参照が困難になっていました。

新しい*Clientidmode*プロパティを使用すると、コントロールに対してクライアント ID を生成する方法をより正確に指定できます。 ページなど、任意のコントロールに対して*Clientidmode*プロパティを設定できます。 設定できる設定は次のとおりです。

- *Autoid* –これは、以前のバージョンの ASP.NET で使用されていた*ClientID*プロパティ値を生成するためのアルゴリズムに相当します。
- *Static* – *ClientID*値が親名前付けコンテナーの id を連結せずに id と同じになるように指定します。 これは、Web ユーザーコントロールで役に立ちます。 Web ユーザーコントロールはさまざまなページに配置でき、異なるコンテナーコントロールに配置される可能性があるため、ID 値がどのようになるかを予測できないため、 *Autoid*アルゴリズムを使用するコントロールのクライアントスクリプトを記述するのが困難な場合があります。
- *予測可能*-このオプションは、主にテンプレートの繰り返しを使用するデータコントロールで使用されます。 コントロールの名前付けコンテナーの ID プロパティを連結しますが、生成される*ClientID*値には、"ctlxxx" のような文字列は含まれません。 この設定は、コントロールの*ClientIDRowSuffix*プロパティと組み合わせて使用できます。 *ClientIDRowSuffix*プロパティをデータフィールドの名前に設定し、そのフィールドの値を、生成された*ClientID*値のサフィックスとして使用します。 通常は、データレコードの主キーを*ClientIDRowSuffix*値として使用します。
- *継承*–この設定は、コントロールの既定の動作です。これは、コントロールの ID 生成が親と同じであることを指定します。

*Clientidmode*プロパティは、ページレベルで設定できます。 これにより、現在のページ内のすべてのコントロールの既定の*Clientidmode*値が定義されます。

ページレベルの既定の*Clientidmode*値は*autoid*で、コントロールレベルの既定の*Clientidmode*値は*Inherit*です。 その結果、コードのどこでもこのプロパティを設定しなかった場合、すべてのコントロールが既定で*Autoid*アルゴリズムになります。

次の例に示すように、 *@ page*ディレクティブでページレベルの値を設定します。

[!code-aspx[Main](overview/samples/sample47.aspx)]

また、構成ファイルで、コンピューター (コンピューター) レベルまたはアプリケーションレベルのいずれかで、 *Clientidmode*値を設定することもできます。 これにより、アプリケーション内のすべてのページのすべてのコントロールに対する既定の*Clientidmode*設定が定義されます。 コンピューターレベルで値を設定すると、そのコンピューター上のすべての Web サイトの既定の*Clientidmode*設定が定義されます。 次の例は、構成ファイルの*Clientidmode*設定を示しています。

[!code-xml[Main](overview/samples/sample48.xml)]

前述のように、 *ClientID*プロパティの値は、コントロールの親の名前付けコンテナーから派生します。 マスターページを使用している場合など、一部のシナリオでは、コントロールは次のレンダリングされた HTML のような Id で終了することがあります。

[!code-html[Main](overview/samples/sample49.html)]

場合でも、*入力*マークアップに示される要素 (から、 *テキスト ボックス*コントロール) 2 つの名前付けコンテナーは、ページの深さ (入れ子になった*ContentPlaceholder*コントロール)、マスター ページが処理されるため、最終結果は、次のようにコントロール ID です。

[!code-console[Main](overview/samples/sample50.cmd)]

この ID はページ内で一意であることが保証されていますが、ほとんどの場合、この ID は不必要に長くなります。 レンダリングされた ID の長さを減らし、ID の生成方法をより細かく制御できるようにするとします。 (たとえば、"ctlxxx" プレフィックスを削除する場合など)。これを実現する最も簡単な方法は、次の例に示すように、 *Clientidmode*プロパティを設定することです。

[!code-aspx[Main](overview/samples/sample51.aspx)]

このサンプルでは、最も外側の*Namingpanel*要素に対して*Clientidmode*プロパティが*Static*に設定され、内側の*Namingpanel*要素に対して*予測可能*に設定されています。 これらの設定により、次のマークアップが生成されます (ページの残りの部分とマスターページは、前の例と同じであると見なされます)。

[!code-html[Main](overview/samples/sample52.html)]

*静的*な設定では、最も外側の*namingpanel*要素内の任意のコントロールの名前付け階層をリセットし、生成された ID から ContentPlaceHolder id と *id を除去*する効果があります。 (レンダリングされた要素の*name*属性は影響を受けないため、通常の ASP.NET 機能はイベントやビューステートなどのために保持されます)。名前付け階層をリセットする副作用として、 *Namingpanel*要素のマークアップを別の*ContentPlaceholder*コントロールに移動したとしても、レンダリングされたクライアント id は変わりません。

> [!NOTE]
> 表示されるコントロール Id が一意であることを確認してください。 そうでない場合は、 *document.getelementbyid*関数など、個々の HTML 要素に対して一意の id を必要とする機能を中断できます。

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>データバインドコントロールでの予測可能なクライアント Id の作成

レガシアルゴリズムによってデータバインドリストコントロールに生成される*ClientID*値は、長くなる可能性があり、実際には予測できません。 *Clientidmode*機能は、これらの id の生成方法をより細かく制御するのに役立ちます。

次の例のマークアップには、 *ListView*コントロールが含まれています。

[!code-aspx[Main](overview/samples/sample53.aspx)]

前の例では、 *Clientidmode*プロパティと*RowClientIDRowSuffix*プロパティがマークアップで設定されています。 *ClientIDRowSuffix*プロパティはデータバインドコントロールでのみ使用でき、その動作は使用しているコントロールによって異なります。 違いは次のとおりです。

- *GridView*コントロール—データソース内の1つまたは複数の列の名前を指定できます。この名前は実行時に組み合わされ、クライアント id が作成されます。 たとえば、 *RowClientIDRowSuffix*を "ProductName, ProductId" に設定した場合、レンダリングされた要素のコントロール id の形式は次のようになります。

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView*コントロール—クライアント ID に追加されるデータソース内の1つの列を指定できます。 たとえば、 *ClientIDRowSuffix*を "ProductName" に設定した場合、レンダリングされるコントロール id の形式は次のようになります。

- [!code-console[Main](overview/samples/sample55.cmd)]

- この場合、後続の1は、現在のデータ項目の製品 ID から派生します。

- *Repeater*コントロール: このコントロールは、 *ClientIDRowSuffix*プロパティをサポートしていません。 *Repeater*コントロールでは、現在の行のインデックスが使用されます。 *Repeater*コントロールで ClientIDMode = "予測可能" を使用すると、次の形式のクライアント id が生成されます。

- [!code-console[Main](overview/samples/sample56.cmd)]

- 末尾の0は、現在の行のインデックスです。

*FormView*コントロールと*DetailsView*コントロールには複数の行が表示されないため、 *ClientIDRowSuffix*プロパティをサポートしていません。

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>データコントロールでの行選択の保持

*GridView*コントロールと*ListView*コントロールを使用して、ユーザーが行を選択できるようにすることができます。 以前のバージョンの ASP.NET では、ページの行インデックスに基づいて選択が行われていました。 たとえば、ページ1の3番目の項目を選択し、ページ2に移動すると、そのページの3番目の項目が選択されます。

永続化の選択は、最初は .NET Framework 3.5 SP1 の動的データプロジェクトでのみサポートされていました。 この機能が有効になっている場合、現在選択されている項目は項目のデータキーに基づきます。 これは、ページ1の3番目の行を選択し、ページ2に移動した場合、ページ2で何も選択されていないことを意味します。 ページ1に戻ると、3番目の行が選択されたままになります。 次の例に示すように、 *EnablePersistedSelection*プロパティを使用すると、すべてのプロジェクトの*GridView*コントロールと*ListView*コントロールで、永続化された選択がサポートされるようになりました。

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET Chart コントロール

ASP.NET *Chart*コントロールは、.NET Framework 内のデータ可視化オファリングを拡張します。 *グラフ*コントロールを使用すると、複雑な統計分析や財務分析のための直感的で視覚的に説得力のあるグラフを持つ ASP.NET ページを作成できます。 ASP.NET *Chart*コントロールは .NET Framework バージョン 3.5 SP1 リリースのアドオンとして導入され、.NET Framework 4 リリースの一部になっています。

コントロールには、次の機能があります。

- 35 種類のグラフ
- グラフ領域、タイトル、凡例、および注釈の数に制限はありません。
- すべてのグラフ要素のさまざまな外観設定。
- ほとんどの種類のグラフでは、3-d がサポートしています。
- データポイントを自動的に収めることができるスマートデータラベル。
- ストリップライン、スケール区切り、および対数目盛り。
- データの分析と変換に使用できる 50 を超える財務式および統計式。
- グラフデータの単純なバインドと操作。
- 日付、時刻、通貨などの一般的なデータ形式のサポート。
- Ajax を使用したクライアントクリックイベントなど、対話機能とイベントドリブンカスタマイズのサポート。
- 状態管理。
- バイナリ ストリーム転送。

次の図は、ASP.NET Chart コントロールによって生成される財務グラフの例を示しています。

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

図 2: ASP.NET Chart コントロールの例

ASP.NET Chart コントロールの使用方法の例については、MSDN Web サイトの「 [Microsoft Chart コントロールのサンプル環境](https://go.microsoft.com/fwlink/?LinkId=128300)」ページでサンプルコードをダウンロードしてください。 コミュニティコンテンツのその他のサンプルについては、[グラフコントロールフォーラム](https://go.microsoft.com/fwlink/?LinkId=128713)を参照してください。

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>ASP.NET ページへのグラフコントロールの追加

次の例は、マークアップを使用して ASP.NET ページに*グラフ*コントロールを追加する方法を示しています。 この例では、*グラフ*コントロールによって、静的なデータポイントの縦棒グラフが生成されます。

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>3-d グラフの使用

*グラフ*コントロールには、グラフ領域の特性を定義する*ChartArea*オブジェクトを含むことができる、 *chartareas*コレクションが含まれています。 たとえば、グラフ領域に3-d を使用するには、次の例のように*Area3DStyle*プロパティを使用します。

[!code-aspx[Main](overview/samples/sample59.aspx)]

次の図は、*横棒*グラフの4つの系列を含む3-d グラフを示しています。

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

図 3:3-d 横棒グラフ

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>スケール区切りと対数スケールの使用

スケール区切りと対数スケールは、グラフに洗練を追加するための2つの追加方法です。 これらの機能は、グラフ領域の各軸に固有です。 たとえば、グラフ領域の主軸の Y 軸でこれらの機能を使用するには、 *ChartArea*オブジェクトで*AxisY*プロパティと*scalebreakstyle*プロパティを使用します。 次のスニペットは、主軸の Y 軸でスケール区切りを使用する方法を示しています。

[!code-aspx[Main](overview/samples/sample60.aspx)]

次の図は、スケール区切りが有効になっている Y 軸を示しています。

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

図 4: スケール区切り

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>QueryExtender コントロールを使用したデータのフィルター処理

データドリブン Web ページを作成する開発者にとって非常に一般的なタスクは、データをフィルター処理することです。 これは従来、データソースコントロールで*Where*句を構築することによって行われていました。 この方法は複雑になる場合があります。場合によっては、 *Where*構文を使用しても、基になるデータベースのすべての機能を利用できないことがあります。

フィルター処理を容易にするために、ASP.NET 4 に新しい*Queryextender*コントロールが追加されました。 これらのコントロールによって返されるデータをフィルター処理するために、このコントロールを*EntityDataSource*または*LinqDataSource*コントロールに追加できます。 *Queryextender*コントロールは LINQ に依存しているため、データがページに送信される前にデータベースサーバーにフィルターが適用されるため、非常に効率的な操作になります。

*Queryextender*コントロールでは、さまざまなフィルターオプションがサポートされています。 以下のセクションでは、これらのオプションについて説明し、それらの使用方法の例を示します。

#### <a name="search"></a>検索

検索オプションの場合、 *Queryextender*コントロールは、指定されたフィールド内で検索を実行します。 次の例では、コントロールは TextBoxSearch コントロールに入力されたテキストを使用し、`ProductName` の内容を検索し、 *LinqDataSource*コントロールから返されるデータの列を `Supplier.CompanyName` します。

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>範囲

Range オプションは検索オプションに似ていますが、範囲を定義する値のペアを指定します。 次の例では、 *Queryextender*コントロールは、 *LinqDataSource*コントロールから返されたデータの `UnitPrice` 列を検索します。 範囲は、ページ上の TextBoxFrom コントロールと TextBoxTo コントロールから読み取られます。

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

[プロパティ式] オプションを使用すると、プロパティ値の比較を定義できます。 式が*true*に評価された場合、検査対象のデータが返されます。 次の例では、 *Queryextender*コントロールは、`Discontinued` 列のデータをページ上の CheckBoxDiscontinued コントロールの値と比較することによって、データをフィルター処理します。

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

最後に、 *Queryextender*コントロールで使用するカスタム式を指定できます。 このオプションを使用すると、カスタムフィルターロジックを定義するページ内の関数を呼び出すことができます。 次の例は、 *Queryextender*コントロールでカスタム式を宣言によって指定する方法を示しています。

[!code-aspx[Main](overview/samples/sample64.aspx)]

次の例は、 *Queryextender*コントロールによって呼び出されるカスタム関数を示しています。 この場合、 *Where*句を含むデータベースクエリを使用する代わりに、コードは LINQ クエリを使用してデータをフィルター処理します。

[!code-csharp[Main](overview/samples/sample65.cs)]

これらの例では、一度に*Queryextender*コントロールで使用されている式が1つだけ表示されます。 ただし、 *Queryextender*コントロール内には複数の式を含めることができます。

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html エンコードされたコード式

一部の ASP.NET サイト (特に ASP.NET MVC) は、`<%`= `expression %>` 構文 (多くの場合 "code ナゲット" と呼ばれます) を使用して応答にテキストを書き込むことに大きく依存しています。 コード式を使用する場合、テキストを HTML エンコードするのは簡単ではありません。テキストがユーザー入力からのものである場合、ページは XSS (クロスサイトスクリプティング) 攻撃に対して開いたままにすることができます。

ASP.NET 4 では、コード式の次の新しい構文が導入されています。

[!code-aspx[Main](overview/samples/sample66.aspx)]

この構文では、応答への書き込み時に既定で HTML エンコーディングが使用されます。 この新しい式は、実質的に次のように変換されます。

[!code-aspx[Main](overview/samples/sample67.aspx)]

たとえば、&lt;%:要求 ["UserInput"]%&gt;*要求 ["userinput"]* の値に対して HTML エンコードを実行します。

この機能の目的は、古い構文のすべてのインスタンスを新しい構文に置き換えることができるようにすることです。これにより、使用するすべての手順を強制的に決定する必要がなくなります。 ただし、出力されるテキストが HTML または既にエンコードされている場合もあります。この場合、エンコードが2倍になる可能性があります。

このような場合、ASP.NET 4 では、具象実装である*Htmlstring*と共に、新しいインターフェイス*ihtmlstring*が導入されています。 これらの型のインスタンスを使用すると、戻り値が既に HTML として表示されるように適切にエンコード (または検証) されることを示すことができます。したがって、値は HTML エンコードされないようにする必要があります。 たとえば、次のは HTML エンコードされていてはなりません。

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 ヘルパーメソッドは、この新しい構文で動作するように更新され、ASP.NET 4 を実行している場合にのみ、二重にエンコードされないようになっています。 ASP.NET 3.5 SP1 を使用してアプリケーションを実行する場合、この新しい構文は機能しません。

これによって、XSS 攻撃からの保護が保証されないことに注意してください。 たとえば、引用符で囲まれていない属性値を使用する HTML には、依然として脆弱なユーザー入力を含めることができます。 ASP.NET controls と ASP.NET MVC のヘルパーの出力には、常に引用符で囲んだ属性値が含まれていることに注意してください。これは推奨される方法です。

同様に、この構文では、ユーザー入力に基づいて JavaScript 文字列を作成する場合など、JavaScript のエンコードは実行されません。

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>プロジェクトテンプレートの変更

以前のバージョンの ASP.NET では、Visual Studio を使用して新しい Web サイトプロジェクトまたは Web アプリケーションプロジェクトを作成すると、次の図に示すように、結果として得られるプロジェクトには default.aspx ページ、既定の `Web.config` ファイル、および `App_Data` フォルダーだけが含まれます。

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio では、次の図に示すように、まったくファイルが含まれていない空の Web サイトプロジェクトタイプもサポートされています。

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

その結果、初級者にとって、実稼働 Web アプリケーションを構築する方法についてのガイダンスはほとんどありません。 このため、ASP.NET 4 では、空の Web アプリケーションプロジェクト用に1つ、Web アプリケーションと Web サイトプロジェクト用にそれぞれ1つずつ、3つの新しいテンプレートが導入されています。

#### <a name="empty-web-application-template"></a>空の Web アプリケーションテンプレート

名前が示すように、空の Web アプリケーションテンプレートは、ダウンダウンされた Web アプリケーションプロジェクトです。 このプロジェクトテンプレートは、次の図に示すように、Visual Studio の [新しいプロジェクト] ダイアログボックスから選択します。

[![](overview/_static/image7.png)](overview/_static/image6.png)

([クリックすると、フルサイズの画像が表示](overview/_static/image8.png)される)

空の ASP.NET Web アプリケーションを作成すると、Visual Studio によって次のフォルダーレイアウトが作成されます。

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

これは、以前のバージョンの ASP.NET の空の Web サイトレイアウトに似ていますが、例外が1つあります。 Visual Studio 2010 では、空の Web アプリケーションと空の Web サイトプロジェクトには、プロジェクトが対象としているフレームワークを識別するために Visual Studio で使用される情報を含む、次の最小限の `Web.config` ファイルが含まれています。

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

この*Targetframework*プロパティがない場合、Visual Studio では、古いアプリケーションを開くときに互換性を維持するために、既定で .NET Framework 2.0 を対象とします。

#### <a name="web-application-and-web-site-project-templates"></a>Web アプリケーションと Web サイトプロジェクトのテンプレート

Visual Studio 2010 に付属するその他の2つの新しいプロジェクトテンプレートには、大幅な変更が含まれています。 次の図は、新しい Web アプリケーションプロジェクトを作成するときに作成されるプロジェクトのレイアウトを示しています。 (Web サイトプロジェクトのレイアウトは実質的には同じです)。

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

プロジェクトには、以前のバージョンでは作成されなかった多数のファイルが含まれています。 また、新しい Web アプリケーションプロジェクトは、基本メンバーシップ機能を使用して構成されます。これにより、新しいアプリケーションへのアクセスのセキュリティ保護をすぐに開始できます。 この追加のため、新しいプロジェクトの `Web.config` ファイルには、メンバーシップ、ロール、およびプロファイルの構成に使用されるエントリが含まれています。 次の例は、新しい Web アプリケーションプロジェクトの `Web.config` ファイルを示しています。 (この例では、 *roleManager*は無効になっています)。

[![](overview/_static/image13.png)](overview/_static/image12.png)

([クリックすると、フルサイズの画像が表示](overview/_static/image14.png)される)

このプロジェクトには、`Account` ディレクトリ内の2つ目の `Web.config` ファイルも含まれています。 2番目の構成ファイルは、ログインしていないユーザーの ChangePassword ページへのアクセスをセキュリティで保護する方法を提供します。 次の例は、2番目の `Web.config` ファイルの内容を示しています。

![](overview/_static/image15.png)

新しいプロジェクトテンプレートに既定で作成されるページには、以前のバージョンよりも多くのコンテンツが含まれています。 プロジェクトには既定のマスターページと CSS ファイルが含まれており、既定のページ (default.aspx) は既定でマスターページを使用するように構成されています。 その結果、Web アプリケーションまたは Web サイトを初めて実行するときに、既定の (ホーム) ページが既に機能していることになります。 実際には、新しい MVC アプリケーションを起動するときに表示される既定のページに似ています。

[![](overview/_static/image17.png)](overview/_static/image16.png)

([クリックすると、フルサイズの画像が表示](overview/_static/image18.png)される)

プロジェクトテンプレートに対するこれらの変更の目的は、新しい Web アプリケーションの構築を開始する方法に関するガイダンスを提供することです。 意味的に正しい、厳密な XHTML 1.0 準拠のマークアップ、および CSS を使用して指定されたレイアウトでは、テンプレートのページは ASP.NET 4 Web アプリケーションを構築するためのベストプラクティスを表します。 既定のページには、簡単にカスタマイズできる2列のレイアウトもあります。

たとえば、新しい Web アプリケーションでは、一部の色を変更し、My ASP.NET アプリケーションロゴの代わりに会社のロゴを挿入するとします。 これを行うには、`Content` の下に新しいディレクトリを作成し、ロゴイメージを格納します。

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

ページにイメージを追加するには、次の例のように、`Site.Master` ファイルを開き、My ASP.NET Application のテキストが定義されている場所を見つけて、 *src*属性が新しいロゴイメージに設定されている*イメージ*要素で置き換えます。

[![](overview/_static/image21.png)](overview/_static/image20.png)

([クリックすると、フルサイズの画像が表示](overview/_static/image22.png)される)

その後、サイトの .css ファイルに移動し、CSS クラス定義を変更して、ページの背景色やヘッダーの背景色を変更できます。

これらの変更の結果として、カスタマイズされたホームページをごくわずかな労力で表示できるようになります。

[![](overview/_static/image24.png)](overview/_static/image23.png)

([クリックすると、フルサイズの画像が表示](overview/_static/image25.png)される)

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS の機能強化

ASP.NET 4 の主要な作業領域の1つは、最新の HTML 標準に準拠した HTML のレンダリングに役立ちました。 これには、ASP.NET Web サーバーコントロールが CSS スタイルを使用する方法の変更が含まれます。

#### <a name="compatibility-setting-for-rendering"></a>レンダリングの互換性設定

既定では、Web アプリケーションまたは Web サイトが .NET Framework 4 を対象とする場合、 *pages*要素の*controlRenderingCompatibilityVersion*属性は "4.0" に設定されます。 この要素はコンピューターレベルの `Web.config` ファイルで定義され、既定ではすべての ASP.NET 4 アプリケーションに適用されます。

[!code-xml[Main](overview/samples/sample69.xml)]

*ControlRenderingCompatibility*の値は文字列であり、今後のリリースで新しいバージョンの定義が可能になります。 現在のリリースでは、このプロパティで次の値がサポートされています。

- "3.5". この設定は、従来の表示とマークアップを示します。 コントロールによってレンダリングされるマークアップは100% 後方互換性があり、 *xhtmlConformance*プロパティの設定が受け入れられます。
- "4.0". プロパティにこの設定が含まれている場合、ASP.NET Web サーバーコントロールは次の操作を実行します。
- *XhtmlConformance*プロパティは、常に "Strict" として扱われます。 その結果、コントロールは XHTML 1.0 Strict マークアップをレンダリングします。
- 非入力コントロールを無効にすると、無効なスタイルが表示できなくなります。
- 非表示フィールドの周囲の*div*要素には、ユーザーが作成した CSS 規則に干渉しないようにスタイルが適用されるようになりました。
- メニューコントロールは、意味的に正しい、アクセシビリティガイドラインに準拠しているマークアップをレンダリングします。
- 検証コントロールは、インラインスタイルをレンダリングしません。
- 以前に表示された border = "0" (ASP.NET *Table*コントロールから派生したコントロールと ASP.NET *Image*コントロール) がこの属性をレンダリングしないコントロール。

#### <a name="disabling-controls"></a>無効化 (コントロールを)

ASP.NET 3.5 SP1 以前のバージョンでは、*有効になっている*プロパティが*false*に設定されているコントロールに対して、フレームワークによって、*無効になっ*た属性が HTML マークアップでレンダリングされます。 ただし、HTML 4.01 仕様によれば、*入力*要素のみがこの属性を持つ必要があります。

ASP.NET 4 では、次の例に示すように、 *controlRenderingCompatibilityVersion*プロパティを "3.5" に設定できます。

[!code-xml[Main](overview/samples/sample70.xml)]

次のような*ラベル*コントロールのマークアップを作成すると、コントロールが無効になります。

[!code-aspx[Main](overview/samples/sample71.aspx)]

*ラベル*コントロールでは、次の HTML が表示されます。

[!code-html[Main](overview/samples/sample72.html)]

ASP.NET 4 では、 *controlRenderingCompatibilityVersion*を "4.0" に設定できます。 その場合、コントロールの*Enabled*プロパティが*false*に設定されていると、*入力*要素を表示するコントロールのみが、*無効*な属性をレンダリングします。 代わりに HTML*入力*要素をレンダリングしないコントロールでは、コントロールの無効な検索を定義するために使用できる CSS クラスを参照する*クラス*属性がレンダリングされます。 たとえば、前の例で示した*ラベル*コントロールでは、次のマークアップが生成されます。

[!code-html[Main](overview/samples/sample73.html)]

このコントロールに対して指定されたクラスの既定値は "aspNetDisabled" です。 ただし、 *WebControl*クラスの static *DisabledCssClass*静的プロパティを設定することによって、この既定値を変更できます。 コントロールの開発者にとって、特定のコントロールに使用する動作は、 *SupportsDisabledAttribute*プロパティを使用して定義することもできます。

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>非表示フィールドの周囲の div 要素の非表示

ASP.NET 2.0 以降のバージョンでは、XHTML 標準に準拠するために、 *div*要素内にシステム固有の非表示フィールド (ビューステート情報を格納するために使用される*非表示*の要素など) が表示されます。 ただし、これにより、CSS ルールがページ上の*div*要素に影響を与える場合に問題が発生する可能性があります。 たとえば、非表示の*div*要素に関するページに1ピクセルの線が表示されることがあります。 ASP.NET 4 では、ASP.NET によって生成された隠しフィールドを囲む*div*要素は、次の例のように CSS クラス参照を追加します。

[!code-html[Main](overview/samples/sample74.html)]

その後、次の例のように、ASP.NET によって生成された*非表示*の要素にのみ適用される CSS クラスを定義できます。

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>テンプレートコントロール用の外部テーブルのレンダリング

既定では、テンプレートをサポートする次の ASP.NET Web サーバーコントロールは、インラインスタイルを適用するために使用される外部テーブルに自動的にラップされます。

- *FormView*
- *Login*
- *PasswordRecovery*
- *ChangePassword*
- *ウィザード*
- *CreateUserWizard*

*Renderoutertable*という名前の新しいプロパティがこれらのコントロールに追加され、外部テーブルをマークアップから削除できるようになりました。 たとえば、次の*FormView*コントロールの例を考えてみます。

[!code-aspx[Main](overview/samples/sample76.aspx)]

このマークアップは、HTML テーブルを含むページに次の出力をレンダリングします。

[!code-html[Main](overview/samples/sample77.html)]

テーブルが表示されないようにするには、次の例に示すように、 *FormView*コントロールの*renderoutertable*プロパティを設定します。

[!code-aspx[Main](overview/samples/sample78.aspx)]

前の例では、 *table*、 *tr*、および*td*要素を使用せずに、次の出力が表示されます。

> Content

この拡張機能を使用すると、コントロールによって予期しないタグがレンダリングされないため、コントロールのコンテンツのスタイルを CSS で簡単に設定できます。

> [!NOTE]
> この変更により、Visual Studio 2010 デザイナーのオートフォーマット関数のサポートが無効になります。これは、オートフォーマットオプションによって生成されるスタイル属性をホストできる*table*要素がなくなったためです。

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView コントロールの機能強化

*ListView*コントロールは、ASP.NET 4 で使いやすくなっています。 以前のバージョンのコントロールでは、既知の ID を持つサーバーコントロールを含むレイアウトテンプレートを指定する必要があります。 次のマークアップは、ASP.NET 3.5 で*ListView*コントロールを使用する一般的な例を示しています。

[!code-aspx[Main](overview/samples/sample79.aspx)]

ASP.NET 4 では、 *ListView*コントロールにレイアウトテンプレートは必要ありません。 前の例で示したマークアップは、次のマークアップに置き換えることができます。

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList と RadioButtonList のコントロールの機能強化

ASP.NET 3.5 では、次の2つの設定を使用して、 *CheckBoxList*と*RadioButtonList*のレイアウトを指定できます。

- *Flow*。 コントロールは、コンテンツを格納するために*スパン*要素をレンダリングします。
- *テーブル*。 コントロールは、その内容を格納する*table*要素をレンダリングします。

次の例では、これらの各コントロールのマークアップを示します。

[!code-aspx[Main](overview/samples/sample81.aspx)]

既定では、コントロールは次のような HTML を表示します。

[!code-html[Main](overview/samples/sample82.html)]

これらのコントロールには項目のリストが含まれているので、意味のある正しい HTML を表示するには、HTML リスト (*li*) 要素を使用して内容をレンダリングする必要があります。 これにより、ユーザーは補助的なテクノロジを使用して Web ページを読みやすくなり、CSS を使用してコントロールのスタイルを簡単にすることができます。

ASP.NET 4 では、 *CheckBoxList*および*RadioButtonList*コントロールで、 *RepeatLayout*プロパティの次の新しい値がサポートされています。

- *OrderedList* –コンテンツは*ol*要素内の*li*要素としてレンダリングされます。
- *Unorderedlist レイアウト*–コンテンツは、 *ul*要素内の*li*要素としてレンダリングされます。

これらの新しい値を使用する方法を次の例に示します。

[!code-aspx[Main](overview/samples/sample83.aspx)]

上記のマークアップでは、次の HTML が生成されます。

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 注*RepeatLayout*を*OrderedList*または*unorderedlist レイアウト*に設定すると、 *repeatdirection*プロパティを使用できなくなります。また、マークアップまたはコード内でプロパティが設定されている場合は、実行時に例外がスローされます。 これらのコントロールのビジュアルレイアウトは、代わりに CSS を使用して定義されているため、プロパティには値がありません。

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>メニューコントロールの機能強化

ASP.NET 4 より前の*メニュー*コントロールでは、一連の HTML テーブルが表示されていました。 これにより、インラインプロパティの設定以外で CSS スタイルを適用することが難しくなりました。また、アクセシビリティ標準に準拠していませんでした。

ASP.NET 4 では、コントロールは、順序付けられていないリストとリストの要素で構成されるセマンティックマークアップを使用して HTML をレンダリングするようになりました。 次の例は、*メニュー*コントロールの ASP.NET ページのマークアップを示しています。

[!code-aspx[Main](overview/samples/sample85.aspx)]

ページがレンダリングされると、コントロールは次の HTML を生成します (わかりやすくするために*onclick*コードは省略されています)。

[!code-html[Main](overview/samples/sample86.html)]

レンダリングの機能強化に加えて、フォーカス管理を使用してメニューのキーボードナビゲーションが改善されました。 *メニュー*コントロールがフォーカスを取得すると、方向キーを使用して要素を移動できます。 また、*メニュー*コントロールは、アクセシビリティを向上させるために[、](http://www.w3.org/TR/wai-aria-practices/#menu "メニューの ARIA のガイドライン")アクセス可能なリッチインターネットアプリケーション (ARIA) ロールおよび属性をアタッチするようになりました。

メニューコントロールのスタイルは、表示されている HTML 要素を含む行ではなく、ページの上部にあるスタイルブロックで表示されます。 コントロールのスタイルを完全に制御する場合は、新しい*Includeスタイルブロック*プロパティを*false*に設定できます。この場合、スタイルブロックは出力されません。 このプロパティを使用する方法の1つは、Visual Studio デザイナーのオートフォーマット機能を使用してメニューの外観を設定することです。 その後、ページを実行してページソースを開き、レンダリングされたスタイルブロックを外部 CSS ファイルにコピーできます。 Visual Studio で、スタイルを元に戻し、 *Includeスタイルブロック*を*false*に設定します。 その結果、メニューの外観は、外部スタイルシートのスタイルを使用して定義されます。

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>ウィザードと CreateUserWizard のコントロール

ASP.NET *Wizard*および*CreateUserWizard*コントロールは、レンダリングする HTML を定義できるテンプレートをサポートしています。 (*CreateUserWizard*は*ウィザード*から派生します。)完全にテンプレート化された*CreateUserWizard*コントロールのマークアップの例を次に示します。

[!code-aspx[Main](overview/samples/sample87.aspx)]

コントロールは、次のような HTML をレンダリングします。

[!code-html[Main](overview/samples/sample88.html)]

ASP.NET 3.5 SP1 では、テンプレートの内容を変更することはできますが、*ウィザード*コントロールの出力の制御は制限されています。 ASP.NET 4 では、 *LayoutTemplate*テンプレートを作成し、(予約された名前を使用して)*プレースホルダー*コントロールを挿入して、*ウィザードコントロール*のレンダリング方法を指定できます。 次の例はこのことを示します。

[!code-aspx[Main](overview/samples/sample89.aspx)]

この例では、 *LayoutTemplate*要素に次の名前付きプレースホルダーが含まれています。

- *Headerplaceholder* –実行時に、 *system.windows.controls.headereditemscontrol.headertemplate*要素の内容に置き換えられます。
- *Sidebarplaceholder* –実行時に、これは*sidebarplaceholder*要素の内容に置き換えられます。
- *Wizardstepplaceholder* –実行時に、これは*wizardstepplaceholder*要素の内容に置き換えられます。
- *Navigationplaceholder* –実行時に、定義したナビゲーションテンプレートに置き換えられます。

プレースホルダーを使用する例のマークアップでは、次の HTML が表示されます (テンプレートで実際に定義されていないコンテンツは含まれません)。

[!code-html[Main](overview/samples/sample90.html)]

現在ユーザー定義されていない HTML は*span*要素だけです。 (今後のリリースでは、 *span*要素がレンダリングされないことを想定しています)。これにより、*ウィザード*コントロールによって生成されるすべてのコンテンツを完全に制御できるようになりました。

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC は、3.5 年 3 2009 月に ASP.NET SP1 のアドオンフレームワークとして導入されました。 Visual Studio 2010 には、新しい機能を含む ASP.NET MVC 2 が含まれています。

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>区分のサポート

区分を使用すると、他のセクションからの相対分離で、コントローラーとビューを大規模なアプリケーションのセクションにグループ化できます。 各領域は、メインアプリケーションで参照できる個別の ASP.NET MVC プロジェクトとして実装できます。 これにより、大規模なアプリケーションを構築する際の複雑さを管理し、複数のチームが1つのアプリケーションで共同作業を簡単に行えるようになります。

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>データ注釈属性の検証のサポート

*Dataannotations*属性を使用すると、メタデータ属性を使用して、検証ロジックをモデルにアタッチできます。 *Dataannotations*属性は、ASP.NET 3.5 SP1 の ASP.NET 動的データで導入されました。 これらの属性は、既定のモデルバインダーに統合されており、ユーザー入力を検証するためのメタデータドリブンの手段を提供しています。

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>テンプレートヘルパー

テンプレートヘルパーを使用すると、編集および表示テンプレートをデータ型に自動的に関連付けることができます。 たとえば、テンプレートヘルパーを使用して、日付の選択 UI 要素が*システムの DateTime*値に対して自動的に表示されるように指定できます。 これは、ASP.NET 動的データのフィールドテンプレートに似ています。

ヘルパーメソッドの*html. editorfor*および*html. displayfor*は、標準データ型を表示するための組み込みのサポートと、複数のプロパティを持つ複雑なオブジェクトが含まれています。 また、 *DisplayName*や*ScaffoldColumn*などのデータ注釈属性を*ビューモデル*オブジェクトに適用できるようにすることで、レンダリングをカスタマイズします。

多くの場合、UI ヘルパーからの出力をさらにカスタマイズし、生成される内容を完全に制御する必要があります。 ヘルパーメソッドの*html. Editorfor* *.html*は、テンプレート機構を使用してこれをサポートしています。これにより、表示される出力をオーバーライドおよび制御できる外部テンプレートを定義できます。 テンプレートは、クラスごとに個別にレンダリングできます。

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>動的データ

動的データは、2008 .NET Framework 3.5 SP1 リリースで導入されました。 この機能には、次のようなデータドリブンアプリケーションを作成するための多くの拡張機能が用意されています。

- データドリブンの Web サイトをすばやく構築するための RAD エクスペリエンス。
- データモデルで定義されている制約に基づく自動検証。
- 動的データプロジェクトの一部であるフィールドテンプレートを使用して、 *GridView*コントロールおよび*DetailsView*コントロールのフィールドに対して生成されたマークアップを簡単に変更する機能。

> [!NOTE]
> 注詳細については、MSDN ライブラリの[動的データのドキュメント](https://msdn.microsoft.com/library/cc488545.aspx)を参照してください。

ASP.NET 4 では、開発者がデータ主導の Web サイトをすばやく構築できるように、動的データが強化されています。

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>既存のプロジェクトの動的データを有効にする

.NET Framework 3.5 SP1 に同梱されている動的データ機能には、次のような新機能があります。

- フィールドテンプレート–データバインドコントロール用のデータ型ベースのテンプレートを提供します。 フィールドテンプレートを使用すると、各フィールドのテンプレートフィールドを使用する場合よりも、データコントロールの外観を簡単にカスタマイズできます。
- 検証–動的データを使用すると、データクラスの属性を使用して、必須フィールド、範囲チェック、型チェック、正規表現を使用したパターン一致、カスタム検証などの一般的なシナリオの検証を指定できます。 検証は、データコントロールによって適用されます。

ただし、これらの機能には次の要件があります。

- データアクセス層は Entity Framework または LINQ to SQL に基づいている必要がありました。
- これらの機能でサポートされているデータソースコントロールは、 *EntityDataSource*コントロールまたは*LinqDataSource*コントロールのみです。
- 機能には、動的データまたは動的データエンティティテンプレートを使用して作成された Web プロジェクトが必要でした。この機能をサポートするために必要なすべてのファイルが含まれています。

ASP.NET 4 での動的データサポートの主な目的は、ASP.NET アプリケーションに対して動的データの新しい機能を有効にすることです。 次の例は、既存のページで動的データ機能を利用できるコントロールのマークアップを示しています。

[!code-aspx[Main](overview/samples/sample91.aspx)]

ページのコードでは、これらのコントロールの動的データサポートを有効にするために、次のコードを追加する必要があります。

[!code-csharp[Main](overview/samples/sample92.cs)]

*GridView*コントロールが編集モードの場合、動的データ入力されたデータが適切な形式であるかどうかが自動的に検証されます。 そうでない場合は、エラーメッセージが表示されます。

この機能には、挿入モードの既定値を指定できるなど、他の利点もあります。 動的データない場合は、フィールドの既定値を実装するには、イベントにアタッチし、( *FindControl*を使用して) コントロールを見つけて、その値を設定する必要があります。 ASP.NET 4 では、 *EnableDynamicData*呼び出しで、次の例に示すように、オブジェクトの任意のフィールドに既定値を渡すことができる2番目のパラメーターがサポートされています。

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>宣言型の DynamicDataManager コントロール構文

*DynamicDataManager*コントロールが拡張され、コードだけではなく、ASP.NET のほとんどのコントロールと同様に、宣言によって構成できるようになりました。 *DynamicDataManager*コントロールのマークアップは、次の例のようになります。

[!code-aspx[Main](overview/samples/sample94.aspx)]

このマークアップにより、 *DynamicDataManager*コントロールの*DataControls*セクションで参照されている GridView1 コントロールの動的データ動作が有効になります。

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>エンティティテンプレート

エンティティテンプレートを使用すると、カスタムページを作成しなくても、データのレイアウトをカスタマイズすることができます。 ページテンプレートは、 *FormView*コントロール (以前のバージョンの動的データのページテンプレートで使用される*DetailsView*コントロールではなく) と、エンティティテンプレートをレンダリングするための*DynamicEntity*コントロールを使用します。 これにより、動的データによって表示されるマークアップをより詳細に制御できます。

次の一覧は、エンティティテンプレートを含む新しいプロジェクトディレクトリレイアウトを示しています。

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate` ディレクトリには、データモデルオブジェクトを表示する方法のテンプレートが含まれています。 既定では、オブジェクトは `Default.ascx` テンプレートを使用してレンダリングされます。これにより、ASP.NET 3.5 SP1 の動的データで使用される*DetailsView*コントロールによって作成されたマークアップと同様のマークアップが提供されます。 次の例は、`Default.ascx` コントロールのマークアップを示しています。

[!code-aspx[Main](overview/samples/sample96.aspx)]

既定のテンプレートを編集して、サイト全体のルックアンドフィールを変更することができます。 表示、編集、および挿入操作のためのテンプレートがあります。 オブジェクトの外観を変更するために、データオブジェクトの名前に基づいて新しいテンプレートを追加することができます。 たとえば、次のテンプレートを追加できます。

[!code-console[Main](overview/samples/sample97.cmd)]

テンプレートには、次のマークアップが含まれる場合があります。

[!code-aspx[Main](overview/samples/sample98.aspx)]

新しいエンティティテンプレートは、新しい*DynamicEntity*コントロールを使用してページに表示されます。 実行時に、このコントロールはエンティティテンプレートの内容に置き換えられます。 次のマークアップは、エンティティテンプレートを使用する `Detail.aspx` ページテンプレートの*FormView*コントロールを示しています。 マークアップの*DynamicEntity*要素に注目してください。

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>Url と電子メールアドレスの新しいフィールドテンプレート

ASP.NET 4 には、`EmailAddress.ascx` と `Url.ascx`という2つの新しい組み込みフィールドテンプレートが導入されています。 これらのテンプレートは、 *DataType*属性を使用して*EmailAddress*または*Url*としてマークされているフィールドに使用されます。 *EmailAddress*オブジェクトの場合、フィールドは*mailto:* プロトコルを使用して作成されるハイパーリンクとして表示されます。 ユーザーがリンクをクリックすると、ユーザーの電子メールクライアントが開き、スケルトンメッセージが作成されます。 *Url*として型指定されたオブジェクトは、通常のハイパーリンクとして表示されます。

次の例は、フィールドをマークする方法を示しています。

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>DynamicHyperLink コントロールを使用したリンクの作成

動的データでは、.NET Framework 3.5 SP1 で追加された新しいルーティング機能を使用して、エンドユーザーが Web サイトにアクセスしたときに表示される Url を制御します。 新しい*DynamicHyperLink*コントロールを使用すると、動的データサイト内のページへのリンクを簡単に作成できます。 次の例は、 *DynamicHyperLink*コントロールの使用方法を示しています。

[!code-aspx[Main](overview/samples/sample101.aspx)]

このマークアップは、`Global.asax` ファイルで定義されているルートに基づいて、`Products` テーブルのリストページを指すリンクを作成します。 コントロールは、動的データページの基になっている既定のテーブル名を自動的に使用します。

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>データモデルでの継承のサポート

Entity Framework と LINQ to SQL はどちらも、データモデルの継承をサポートしています。 この例として、`InsurancePolicy` テーブルを持つデータベースが挙げられます。 また、`InsurancePolicy` と同じフィールドを持つ `CarPolicy` テーブルと `HousePolicy` テーブルが含まれている場合もあります。その後、フィールドを追加します。 動的データは、データモデル内の継承されたオブジェクトを理解し、継承されたテーブルのスキャフォールディングをサポートするように変更されました。

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>多対多リレーションシップのサポート (Entity Framework のみ)

Entity Framework には、テーブル間の多対多リレーションシップの豊富なサポートがあります。これは、*エンティティ*オブジェクトのコレクションとしてリレーションシップを公開することによって実装されます。 新しい `ManyToMany.ascx` および `ManyToMany_Edit.ascx` のフィールドテンプレートが追加され、多対多リレーションシップに関係するデータを表示および編集できるようになりました。

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>表示およびサポートの列挙型を制御する新しい属性

*Displayattribute*が追加され、フィールドの表示方法をさらに制御できるようになりました。 以前のバージョンの動的データの*DisplayName*属性では、フィールドのキャプションとして使用される名前を変更できました。 新しい*Displayattribute*クラスを使用すると、フィールドを表示する順序や、フィールドをフィルターとして使用するかどうかなど、フィールドを表示するためのオプションをさらに指定できます。 また、この属性は、 *GridView*コントロールのラベル、 *DetailsView*コントロールで使用される名前、フィールドのヘルプテキスト、フィールドに使用される透かし (フィールドがテキスト入力を受け入れる場合) に使用される名前を個別に制御します。

*EnumDataTypeAttribute*クラスが追加され、フィールドを列挙型にマップできるようになりました。 この属性をフィールドに適用する場合は、列挙型を指定します。 動的データでは、新しい `Enumeration.ascx` フィールドテンプレートを使用して、列挙値を表示および編集するための UI を作成します。 このテンプレートでは、データベースの値が列挙体の名前にマップされます。

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>フィルターの強化されたサポート

動的データ1.0 には、ブール型の列と外部キー列の組み込みフィルターが付属しています。 フィルターでは、表示されているかどうかを指定することはできませんでした。 新しい*displayattribute*属性では、列をフィルターとして表示するかどうかを制御できるようにすることで、これらの問題の両方に対処します。

さらに拡張機能として、Web フォームの[新機能を使用するために、](#0.2__QueryExtender "_QueryExtender")フィルター処理のサポートが再記述されています。 これにより、フィルターを作成する際に、フィルターを使用するデータソースコントロールに関する知識を必要としません。 これらの拡張機能と共に、フィルターもテンプレートコントロールに設定されています。これにより、新しいフィルターを追加することができます。 最後に、前に説明した*Displayattribute*クラスを使用すると、既定のフィルターを上書きできます。これと同じように、 *UIHint*では、列の既定のフィールドテンプレートをオーバーライドできます。

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 の Web 開発の機能強化

Visual Studio 2010 での Web 開発が強化され、CSS 互換性が向上し、HTML および ASP.NET マークアップスニペットと新しい動的 IntelliSense JavaScript による生産性が向上しました。

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>CSS 互換性の向上

Visual Studio 2010 の Visual Web Developer designer が更新され、CSS 2.1 標準準拠が向上しました。 デザイナーでは、HTML ソースの整合性が維持され、以前のバージョンの Visual Studio よりも堅牢になります。 内部的には、レンダリング、レイアウト、および保守性における将来の機能強化を向上させるために、アーキテクチャが改善されました。

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML および JavaScript のスニペット

HTML エディターでは、IntelliSense によってタグ名がオートコンプリートされます。 IntelliSense のスニペット機能は、タグ全体を自動的に補完します。 Visual Studio 2010 では、JavaScript で IntelliSense スニペットがサポートさC#れており、以前のバージョンの visual studio でサポートされていた Visual Basic とともにサポートされていました。

Visual Studio 2010 には、一般的な ASP.NET と HTML タグ (runat = "server" など) とタグに固有の共通属性 ( *ID*、 *DataSourceID*、 *ControlToValidate*、*テキスト*など) を含むオートコンプリートを実行するための、200を超えるスニペットが含まれています。

追加のスニペットをダウンロードすることも、ユーザー自身またはチームが一般的なタスクに使用するマークアップのブロックをカプセル化する独自のスニペットを作成することもできます。

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense の機能強化

Visual 2010 では、より充実した編集エクスペリエンスを提供するために、JavaScript IntelliSense が再設計されました。 IntelliSense は、 *Registernamespace*などのメソッドによって動的に生成されたオブジェクト、および他の JavaScript フレームワークで使用される同様の手法を認識するようになりました。 スクリプトの大規模なライブラリを分析し、処理の遅延がほとんどまたはまったくない IntelliSense を表示するようにパフォーマンスが向上しました。 ほとんどすべてのサードパーティライブラリをサポートし、さまざまなコーディングスタイルをサポートするために、互換性が飛躍的に向上しています。 ドキュメントコメントは入力時に解析されるようになり、IntelliSense によってすぐに利用できるようになりました。

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>Visual Studio 2010 を使用した Web アプリケーションのデプロイ

ASP.NET 開発者は、Web アプリケーションをデプロイするときに、次のような問題が発生していることがよくわかります。

- 共有ホスティングサイトに配置するには、FTP などのテクノロジが必要ですが、これは低速になる可能性があります。 また、データベースを構成するための SQL スクリプトの実行などのタスクを手動で実行する必要があります。また、仮想ディレクトリフォルダーをアプリケーションとして構成するなど、IIS 設定を変更する必要があります。
- エンタープライズ環境では、管理者は Web アプリケーションファイルの展開に加えて、ASP.NET 構成ファイルと IIS 設定を頻繁に変更する必要があります。 データベース管理者は、アプリケーションデータベースを実行するために、一連の SQL スクリプトを実行する必要があります。 このようなインストールには手間がかかり、多くの場合、完了までに数時間かかるため、慎重に文書化する必要があります。

Visual Studio 2010 には、これらの問題に対処し、Web アプリケーションをシームレスにデプロイできるテクノロジが含まれています。 これらのテクノロジの1つは、IIS Web 配置ツール (Msdeploy.exe) です。

Visual Studio 2010 の Web 配置機能には、次の主な領域があります。

- Web パッケージ
- Web.config 変換
- データベースの配置
- ワンクリックによる Web アプリケーションの発行

以下のセクションでは、これらの機能について詳しく説明します。

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>Web パッケージ

Visual Studio 2010 では、Msdeploy.exe ツールを使用して、アプリケーションの圧縮 (.zip) ファイルを作成します。このファイルを*Web パッケージ*と呼びます。 パッケージファイルには、アプリケーションに関するメタデータに加え、次のコンテンツが含まれています。

- IIS 設定。アプリケーションプールの設定、エラーページの設定などが含まれます。
- 実際の Web コンテンツ。 Web ページ、ユーザーコントロール、静的コンテンツ (画像と HTML ファイル) などが含まれます。
- データベーススキーマとデータを SQL Server します。
- セキュリティ証明書、GAC にインストールするコンポーネント、レジストリ設定など。

Web パッケージは任意のサーバーにコピーし、IIS マネージャーを使用して手動でインストールすることができます。 また、自動展開の場合は、コマンドラインコマンドまたはデプロイ Api を使用してパッケージをインストールすることもできます。

Visual Studio 2010 には、Web パッケージを作成するための組み込みの MSBuild タスクとターゲットが用意されています。 詳細については、MSDN Web サイトの「 [ASP.NET Web Application Project Deployment の概要](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)」および「Vishal Joshi のブログで[web パッケージを作成する必要がある 10 + 20 の理由](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)」を参照してください。

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 変換

Web アプリケーションの配置の場合、Visual Studio 2010 では[XML ドキュメント変換 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)が導入されています。これは、`Web.config` ファイルを開発設定から運用設定に変換できる機能です。 変換の設定は、`web.debug.config`、`web.release.config`などという名前の変換ファイルで指定されます。 (これらのファイルの名前は MSBuild の構成と一致します)。変換ファイルには、配置された `Web.config` ファイルに対して行う必要がある変更のみが含まれています。 変更は、単純な構文を使用して指定します。

次の例は、リリース構成の配置用に生成される `web.release.config` ファイルの一部を示しています。 この例の Replace キーワードは、デプロイ時に、`Web.config` ファイルの*connectionString*ノードが、例に示されている値に置き換えられることを指定します。

[!code-xml[Main](overview/samples/sample102.xml)]

詳細については、MSDN <a id="0.2_a"></a> web サイトの「Web[アプリケーションプロジェクトの配置の web.config 変換構文](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)」と[web 配置に関するページを参照してください。Vishal Joshi のブログの web.config 変換](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) ます。

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>データベースの配置

Visual Studio 2010 配置パッケージには SQL Server データベースへの依存関係を含めることができます。 パッケージ定義の一部として、ソースデータベースの接続文字列を指定します。 Web パッケージを作成すると、Visual Studio 2010 はデータベーススキーマの SQL スクリプトと、必要に応じてデータを作成してから、パッケージに追加します。 また、カスタムの SQL スクリプトを提供し、サーバーで実行する順序を指定することもできます。 デプロイ時には、対象サーバーに適した接続文字列を指定します。配置プロセスでは、この接続文字列を使用して、データベーススキーマを作成するスクリプトを実行し、データを追加します。

また、ワンクリック発行を使用して、アプリケーションがリモート共有ホスティングサイトに発行されたときに、データベースを直接発行するように配置を構成することもできます。 詳細については、[Vishal Joshi のブログで、Web アプリケーションプロジェクトを使用してデータベースをデプロイします。このためには、MSDN Web サイトおよび[データベース配置 (VS 2010 を含む](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html))](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) ます。

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>ワンクリックによる Web アプリケーションの発行

また、Visual Studio 2010 では、IIS リモート管理サービスを使用して、Web アプリケーションをリモートサーバーに発行することもできます。 ホスティングアカウントまたはテストサーバーまたはステージングサーバーの発行プロファイルを作成できます。 各プロファイルは、適切な資格情報を安全に保存できます。 その後、Web ワンクリック発行ツールバーを使用して、1回のクリックで任意の対象サーバーに配置できます。 Visual Studio 2010 では、MSBuild コマンドラインを使用して発行することもできます。 これにより、チームビルド環境を構成して、継続的インテグレーションモデルに発行を含めることができます。

詳細については、[1回のクリックで発行して Web 配置](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) を使用して Web アプリケーションプロジェクトをデプロイします。 MSDN Web サイトと Web 1 で、Vishal Joshi のブログにある[[VS 2010 を使用して発行] をクリック](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)します。 Visual Studio 2010 で Web アプリケーションのデプロイに関するビデオプレゼンテーションを表示するには、Vishal Joshi のブログの[Web Developer preview の VS 2010](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html)を参照してください。

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>リソース

次の Web サイトでは、ASP.NET 4 および Visual Studio 2010 に関する追加情報を提供しています。

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN Web サイトの ASP.NET 4 に関する公式ドキュメント。
- [https://www.asp.net/](https://www.asp.net/) — ASP.NET チームの独自の Web サイト。
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx)と[ASP.NET 動的データコンテンツマップ](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)-ASP.NET チームサイトのオンラインリソースと ASP.NET 動的データの公式ドキュメントを参照してください。
- [https://www.asp.net/ajax/](../../ajax/index.md) — ASP.NET Ajax 開発の主要な Web リソースです。
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) -Visual Web Developer チームのブログ。 visual Studio 2010 の機能に関する情報が含まれています。
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET のプレビューリリースのメイン Web リソースです。

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>免責情報

このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。

このドキュメントに記載されている情報は、説明されている問題に関する Microsoft Corporation の発行日時点における最新の見解を表します。 マイクロソフトは変化する市場の状況に対応する必要があるため、本ドキュメントをマイクロソフトの確約と解釈することはできず、発行日以降は、提示されている情報の正確性を保証できません。

このホワイト ペーパーは、情報提供のみを目的としています。 マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。

お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。 このドキュメントのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。ただしこれは、著作権法上のお客様の権利を制限するものではありません。

マイクロソフトは、このドキュメントに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。 別途マイクロソフトのライセンス契約上に明示の規定のない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。

特に明記されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人名、場所、およびイベントは架空のものであり、実在する企業、組織、製品、ドメイン名、電子メールとは一切関係ありません。アドレス、ロゴ、人物、場所、またはイベントが想定されているか、または推測する必要があります。

© 2009 Microsoft Corporation. All rights reserved.

Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。

本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。
