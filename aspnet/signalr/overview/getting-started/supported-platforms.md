---
uid: signalr/overview/getting-started/supported-platforms
title: サポートされているプラットフォーム |Microsoft Docs
author: bradygaster
description: この記事では、SignalR でサポートされているクライアントとサーバーについて説明します。
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450124"
---
# <a name="supported-platforms"></a>サポートされているプラットフォーム

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、SignalR でサポートされているクライアントとサーバーについて説明します。 
> 
> ## <a name="questions-and-comments"></a>質問とコメント
> 
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

SignalR は、さまざまなサーバーおよびクライアント構成でサポートされています。 また、各トランスポートオプションには、独自の一連の要件があります。トランスポートのシステム要件が使用できない場合、SignalR は他のトランスポートへのフェールオーバーを正常に実行します。 SignalR がサポートするトランスポートの詳細については、「[トランスポートとフォールバック](introduction-to-signalr.md#transports)」を参照してください。

## <a name="server-system-requirements"></a>サーバー システムの要件

SignalR サーバーコンポーネントは、さまざまなサーバー構成でホストできます。 このセクションでは、サポートされているオペレーティングシステムのバージョン、.NET framework、インターネットインフォメーションサーバー、およびその他のコンポーネントについて説明します。

### <a name="supported-server-operating-systems"></a>サポート対象のサーバー オペレーティング システム

SignalR サーバーコンポーネントは、次のサーバーまたはクライアントオペレーティングシステムでホストできます。 SignalR が Websocket を使用するには、Windows Server 2012、Windows Server 2016、または Windows 8 が必要であることに注意してください (WebSocket は Windows Azure Websites で使用できます。サイトの .NET framework のバージョンが4.5 に設定されていて、Web ソケットがサイトで有効になっている必要があります)。[構成] ページ)。

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 r2
- Windows 10
- Windows 8
- Windows 7
- Windows Azure

### <a name="supported-server-net-framework-version"></a>サポートされているサーバー .NET Framework バージョン

SignalR 2 は .NET Framework 4.5 でのみサポートされています。 信頼性、互換性、安定性、およびパフォーマンスを向上させる更新プログラムについては、「推奨される[更新プログラム](#updates)」セクションを参照してください。

### <a name="supported-server-iis-versions"></a>サポートされているサーバー IIS のバージョン

SignalR が IIS でホストされている場合、次のバージョンがサポートされます。 開発用 (Windows 8 または Windows 7) のように、クライアントのオペレーティングシステムを使用する場合は、IIS または Cassini の完全バージョンを使用しないことをお勧めします。これは、接続数が10個に制限されているためです。一時的で、頻繁に再確立され、使用されなくなった直後に破棄されることはありません。 IIS Express は、クライアントオペレーティングシステムで使用する必要があります。

また、SignalR を使用するには、IIS 8 または IIS 8 Express を使用する必要があります。サーバーは、Windows 8、Windows Server 2012 以降を使用している必要があり、WebSocket は IIS で有効になっている必要があります。 IIS で WebSocket を有効にする方法の詳細については、「 [iis 8.0 Websocket プロトコルのサポート](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)」を参照してください。

- IIS 8 または IIS 8 Express。
- IIS 7 および7.5。 [拡張子 url](https://support.microsoft.com/kb/980368)のサポートが必要です。
- IIS は統合モードで実行されている必要があります。クラシックモードはサポートされていません。 サーバー送信イベントトランスポートを使用してクラシックモードで IIS を実行すると、最大30秒間のメッセージ遅延が発生する可能性があります。
- ホスティングアプリケーションは、完全信頼モードで実行されている必要があります。

## <a name="client-system-requirements"></a>クライアント システムの要件

SignalR は、さまざまなクライアントプラットフォームで使用できます。 ここでは、web ブラウザー、Windows デスクトップアプリケーション、Silverlight アプリケーション、およびモバイルデバイスで SignalR を使用するためのシステム要件について説明します。

### <a name="web-browsers"></a>Web ブラウザー

SignalR はさまざまな web ブラウザーで使用できますが、通常は最新の2つのバージョンのみがサポートされています。

ブラウザーで SignalR を使用するアプリケーションでは、jQuery バージョン1.6.4 または以降のメジャーバージョン (1.7.2、1.8.2、1.9.1 など) を使用する必要があります。

SignalR は、次のブラウザーで使用できます。

- Microsoft Internet Explorer のバージョン8、9、10、および11。 最新、デスクトップ、およびモバイルバージョンがサポートされています。
- Mozilla Firefox: 現在のバージョン-1、Windows と Mac の両方のバージョン。
- Google Chrome: 現在のバージョン-1、Windows と Mac の両方のバージョン。
- Safari: 現在のバージョン-1、Mac と iOS の両方のバージョン。
- Opera: 現在のバージョン-1、Windows のみ。
- Android ブラウザー

特定のブラウザーを必要とするだけでなく、SignalR が使用するさまざまなトランスポートにも独自の要件があります。 次のトランスポートは、次の構成でサポートされています。

<a id="browser"></a>

**Web ブラウザートランスポートの要件**

| トランスポート | Internet Explorer | Chrome (Windows または iOS) | Firefox | Safari (OSX または iOS) | Android |
| --- | --- | --- | --- | --- | --- |
| WebSocket | 10+ | 現在-1 | 現在-1 | 現在-1 | 該当なし |
| Server-Sent Events | 該当なし | 現在-1 | 現在-1 | 現在-1 | 該当なし |
| ForeverFrame | 8+ | 該当なし | 該当なし | 該当なし | 4.1 |
| 長いポーリング | 8+ | 現在-1 | 現在-1 | 現在-1 | 4.1 |

\*: 6 + すべての機能に必要です。

#### <a name="unsupported-browsers"></a>サポートされていないブラウザー

SignalR は、以前のバージョンのブラウザーでは重大な問題*が発生すること*なく実行できますが、SignalR では積極的にテストされないため、通常はバグを修正することはありません。

### <a name="windows-desktop-and-silverlight-applications"></a>Windows デスクトップアプリケーションと Silverlight アプリケーション

SignalR は、web ブラウザーでの実行に加えて、スタンドアロンの Windows クライアントアプリケーションまたは Silverlight アプリケーションでホストできます。 Windows デスクトップアプリケーションと Silverlight SignalR アプリケーションには、次のシステム要件があります。

- .NET 4 を使用するアプリケーションは、Windows XP SP3 以降でサポートされています。
- .NET Framework 4.5 を使用するアプリケーションは、Windows Vista 以降でサポートされています。

オペレーティングシステムと .NET framework の要件に加えて、SignalR で使用できるトランスポートには独自の要件があります。 次のトランスポートは、次の構成でサポートされています。

**Windows デスクトップと Silverlight トランスポートの要件**

| トランスポート | .NET アプリケーション | Silverlight |
| --- | --- | --- |
| Web ソケット | Windows 8 以降および .NET 4.5 以降 | 該当なし |
| 無期限フレーム | 該当なし | 該当なし |
| Server-Sent Events | .NET 4+ | 5+ |
| 長いポーリング | .NET 4+ | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Windows ストアアプリケーションと Windows Phone アプリケーション

SignalR は、Windows ストアアプリケーションと Windows Phone 8 アプリケーションで使用できます。 次のトランスポートは、次の構成でサポートされています。

**Windows ストアおよび Windows Phone トランスポートの要件**

| トランスポート | Windows ストア/.NET | Windows ストア/JavaScript | Windows Phone/IE | Windows Phone/ .NET |
| --- | --- | --- | --- | --- |
| WebSocket | 該当なし | Win8 + | 8+ | 該当なし |
| 無期限フレーム | 該当なし | Win8 + | 7.5+ | 該当なし |
| Server-Sent Events | Win8 + | 該当なし | 該当なし | 8+ |
| 長いポーリング | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>推奨される更新プログラム

SignalR サーバーには、次の更新プログラムをお勧めします。

- .NET Framework 4.5 の更新プログラムは、[こちらで](https://support.microsoft.com/kb/2750149)入手できます。
- Microsoft は、ASP.NET の Qfe を定期的にリリースします。 これらは、使用可能なものとして適用する必要があります。
