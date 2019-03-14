---
title: Razor コンポーネントのホスティング モデル
author: guardrex
description: クライアント側 Blazor とサーバー側の ASP.NET Core で Razor コンポーネント ホスティング モデルを理解します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042439"
---
# <a name="razor-components-hosting-models"></a>Razor コンポーネントのホスティング モデル

によって[Daniel Roth](https://github.com/danroth27)

Razor のコンポーネントは、クライアント側で実行するように設計 web フレームワーク WebAssembly ベースの .NET ランタイム上のブラウザーで (*Blazor*) または ASP.NET Core でのサーバー側 (*ASP.NET Core の Razor コンポーネント*)。 ホスティング モデルでは、アプリおよびコンポーネントのモデルに関係なく*は同じまま*します。 この記事では、使用可能なホスティング モデルについて説明します。

## <a name="client-side-hosting-model"></a>クライアント側のホスティング モデル

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Blazor のプリンシパルのホスティング モデルは、ブラウザーで実行されているクライアント側です。 このモデルで Blazor アプリ、その依存関係、および .NET ランタイムがブラウザーにダウンロードされます。 アプリがブラウザー UI スレッド上で直接実行されます。 すべての UI の更新とイベントの処理は、同じプロセス内で発生します。 アプリの資産をどのような web サーバーが推奨を使用して静的ファイルとしてデプロイできます (を参照してください[ホストを展開および](xref:host-and-deploy/razor-components/index))。

![Blazor クライアント側:Blazor アプリは、ブラウザー内での UI スレッドで実行されます。](hosting-models/_static/client-side.png)

クライアント側のホスティング モデルを使用して Blazor アプリを作成するには、使用、 **Blazor**または **(ASP.NET Core のホストされる) Blazor**プロジェクト テンプレート (`blazor`または`blazorhosted`テンプレート、を使用する場合[新しい dotnet](/dotnet/core/tools/dotnet-new)コマンド プロンプトでコマンド)。 含まれる*blazor.webassembly.js*ハンドルのスクリプトを作成します。

* .NET ランタイムで、アプリとその依存関係をダウンロードしています。
* アプリを実行するランタイムを初期化します。

クライアント側のホスティング モデルでは、いくつかの利点を提供します。 クライアント側 Blazor:

* .NET サーバー側の依存関係がありません。
* リッチな対話型の UI があります。
* クライアント リソースと機能を完全に活用します。
* オフロードは、サーバーからクライアントに機能します。
* オフライン シナリオをサポートしています。

クライアント側のホストには欠点があります。 クライアント側 Blazor:

* アプリをブラウザーの機能に制限されます。
* 対応クライアントのハードウェアとソフトウェア (たとえば、WebAssembly サポート) が必要です。
* より大きなダウンロード サイズと読み込み時間長くアプリ。
* .NET ランタイムおよびツールのサポート (たとえば、.NET Standard のサポートとデバッグに制限あり) を成熟させる必要があります。

Visual Studio が含まれています、 **Blazor (ホストされる ASP.NET Core)** WebAssembly で実行し、ASP.NET Core サーバーでホストされている Blazor アプリを作成するためのプロジェクト テンプレート。 ASP.NET Core アプリは Blazor アプリをクライアントに機能しますが、別のプロセスは、それ以外の場合。 クライアント側の Blazor アプリは、Web API の呼び出しまたは SignalR 接続を使用してネットワーク経由でサーバーと対話できます。

> [!IMPORTANT]
> クライアント側の Blazor アプリは、IIS サブ アプリとしてホストされる ASP.NET Core アプリによって処理されますが、ASP.NET Core モジュールの継承されたハンドラーを無効にします。 Blazor アプリのアプリ ベース パスを設定*index.html*サブアプリを IIS で構成するときに使用される IIS エイリアスをファイル。
>
> 詳細については、次を参照してください。[アプリ ベース パス](xref:host-and-deploy/razor-components/index#app-base-path)します。

## <a name="server-side-hosting-model"></a>サーバー側のホスティング モデル

ASP.NET Core の Razor コンポーネント サーバー側のホスティング モデルでは、アプリは、ASP.NET Core アプリ内からサーバーで実行されます。 UI の更新、イベント処理、JavaScript の呼び出しは、SignalR 接続経由で処理されます。

![ASP.NET Core Razor コンポーネント サーバー側:ブラウザーでは、SignalR 接続経由でサーバー (ASP.NET Core アプリの内部でホストされている) アプリと対話します。](hosting-models/_static/server-side.png)

サーバー側のホスティング モデルを使用して Razor コンポーネント アプリを作成するには、使用、 **Blazor (ASP.NET Core ではサーバー側)** テンプレート (`blazorserver`を使用する場合[新しい dotnet](/dotnet/core/tools/dotnet-new)コマンド プロンプトで)。 ASP.NET Core アプリは、Razor コンポーネント サーバー側のアプリをホストし、クライアントが接続する SignalR エンドポイントを設定します。 ASP.NET Core アプリを参照して、アプリの`Startup`クラスを追加します。

* サーバー側コンポーネントの Razor サービス。
* 要求パイプラインを処理するアプリです。

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

*Blazor.server.js*スクリプト&dagger;クライアント接続を確立します。 永続化および (たとえば、失われたネットワーク接続の場合は) 発生時に必要なアプリの状態を復元するアプリの役目です。

サーバー側のホスティング モデルには、いくつかの利点があります。

* .NET を使用して、全体のアプリを作成することができますとC#コンポーネント モデルを使用します。
* により、機能豊富な対話型実現し、不要なページ更新を回避できます。
* クライアント側の Blazor アプリよりもアプリのサイズが大幅に小さくなりますがあり、非常に高速に読み込みます。
* コンポーネント ロジックは、.NET Core の互換性のある Api の使用など、サーバーの機能のフル活用できます。
* 既存の .NET tooling、デバッグなどが期待どおりに動作するため、サーバー上で .NET Core で実行します。
* シン クライアントと連動 (たとえば、WebAssembly とリソースをサポートしないブラウザーがデバイスを制限する)。

サーバー側のホストには欠点があります。

* 待機時間があります。すべてのユーザー操作には、ネットワーク ホップが必要があります。
* オフライン サポートにはありません。クライアント接続に失敗した場合、アプリは稼働を停止します。
* スケーラビリティに少なくなっています。サーバーは、複数のクライアント接続を管理し、クライアントの状態を処理する必要があります。
* アプリを処理するために、ASP.NET Core サーバーが必要です。 (たとえば、CDN) からサーバーなしの展開は、ことはできません。

&dagger;*Blazor.server.js*スクリプトは、次のパスに発行: *bin/{デバッグ |リリース}/{ターゲット フレームワーク}/publish/{アプリケーション名}。アプリ/dist/フレームワーク (_f)* します。
