---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: Project Katana | の概要Microsoft Docs
author: howarddierking
description: ASP.NET Framework は10年以上にわたっています。プラットフォームでは、さまざまな Web サイトとサービスの開発が可能になりました。 Web アプリケーションとして...
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 1f28db822930cdfd2ebf4cf9bb27d173f4aa4201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500344"
---
# <a name="an-overview-of-project-katana"></a>プロジェクト Katana の概要

[Howard Dierking](https://github.com/howarddierking)

> ASP.NET Framework は10年以上にわたっています。プラットフォームでは、さまざまな Web サイトとサービスの開発が可能になりました。 Web アプリケーションの開発戦略が進化するにつれて、ASP.NET MVC や ASP.NET Web API などのテクノロジを使用して、フレームワークを段階的に進化させることができました。 Web アプリケーションの開発では、クラウドコンピューティングの世界における次の革新的な手順を実行します。そのため、プロジェクト[Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)は、アプリケーションを ASP.NET するためのコンポーネントの基盤となるセットを提供します。これにより、プロジェクトの[Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) cloud は ASP.NET アプリケーションを最適化します。

## <a name="why-katana--why-now"></a>Katana の理由-なぜですか。

 開発者のフレームワークまたはエンドユーザーの製品について説明しているかどうかにかかわらず、製品作成の根底にある動機を理解することが重要です。これには、製品の作成者を知ることが含まれます。 ASP.NET は、最初は2つの顧客を念頭に置いて作成されました。   
  
**最初の顧客グループは、従来の ASP 開発者でした。** この時点で、ASP は interweaving マークアップとサーバー側スクリプトによって動的なデータドリブン Web サイトおよびアプリケーションを作成するための主要なテクノロジの1つでした。 ASP ランタイムによって提供されるサーバー側スクリプトには、基になる HTTP プロトコルと Web サーバーの主要な側面を抽象化し、セッションやアプリケーションの状態管理やキャッシュなどの追加サービスへのアクセスを提供する、オブジェクトのセットが用意されています。強力な従来の ASP アプリケーションは、サイズと複雑さが増大しているため、管理が困難になっていました。 これは、ほとんどの場合、スクリプト環境では、コードとマークアップのインターリーブによって生成されるコードの重複と組み合わせた構造がないことが原因でした。 いくつかの課題に対処しながら従来の ASP の長所を活用するために、ASP.NET は、サーバー側のプログラミングモデルも保持しながら、.NET Framework のオブジェクト指向言語によって提供されるコード編成を利用してきました。従来の ASP 開発者が使い慣れたものです。

**ASP.NET の対象となる顧客の2番目のグループは、Windows ビジネスアプリケーションの開発者でした。** HTML マークアップを記述することに慣れている従来の ASP 開発者や、より多くの HTML マークアップを生成するコードは、キャンバスと豊富なユーザーセットを含むデザイン時のエクスペリエンスに慣れていました。インターフェイスコントロール。 最初のバージョンの ASP.NET ("Web フォーム" とも呼ばれます) は、ユーザーインターフェイスコンポーネントのサーバー側のイベントモデルと、シームレスな開発者エクスペリエンスを実現する一連のインフラストラクチャ機能 (ViewState など) と同様のデザイン時のエクスペリエンスを提供していました。クライアント側プログラミングとサーバー側プログラミングの間 Web フォームは、WinForms 開発者にとってなじみのあるステートフルなイベントモデルで、Web のステートレスな性質を効果的に hid します。

### <a name="challenges-raised-by-the-historical-model"></a>履歴モデルによって発生した課題

**最終的な結果は、成熟した機能豊富なランタイムと開発者向けプログラミングモデルでした。** しかし、その機能を使用すると、豊富な課題が発生しました。 まず、フレームワークは**モノリシック**であり、論理的には異なる機能の単位が同じ system.servicemodel アセンブリ (たとえば、web フォームフレームワークを持つコア HTTP オブジェクト) に密に結合されていました。 第2に、ASP.NET が大きな .NET Framework の一部として含まれていました。これは、**リリース間の時間が年の順に**なったことを意味します。 これにより、急速に進化する Web 開発で発生するすべての変更に ASP.NET が対応することが困難になりました。 最後に、system.web は、特定の Web ホスティングオプションに対していくつかの異なる方法で結合されています: インターネットインフォメーションサービス (IIS)。

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>進化した手順: ASP.NET MVC と ASP.NET Web API

また、Web 開発で多くの変更が行われています。 Web アプリケーションは、大規模なフレームワークではなく、小規模で焦点を絞った一連のコンポーネントとして開発されてきました。 コンポーネントの数、およびそれらがリリースされた頻度は、より高速に増加しています。 Web にペースを置くことで、より大規模で特徴が豊富ではなく、より小さな、分離された、さらに焦点を絞ったフレームワークが必要になることが明らかになったので、 **ASP.NET チームは、1つのフレームワークではなく、プラグ可能な Web コンポーネントのファミリとして ASP.NET を有効にするために、いくつか**の

初期の変更点の1つは、Ruby on Rails のような Web 開発フレームワークにより、よく知られているモデルビューコントローラー (MVC) デザインパターンの普及が高まったことでした。 このスタイルの Web アプリケーションを構築することで、開発者はアプリケーションのマークアップをより細かく制御できるようになり、ASP.NET の最初の販売ポイントの1つであるマークアップとビジネスロジックの分離が維持されます。 このスタイルの Web アプリケーション開発の需要を満たすために、Microsoft では、 **ASP.NET MVC を帯域外で開発**することによって、将来的により適切に配置する機会を獲得しました (.NET Framework には含まれません)。 ASP.NET MVC は、独立したダウンロードとしてリリースされました。 これにより、エンジニアリングチームは、以前よりもはるかに頻繁に更新を提供できるようになりました。

Web アプリケーション開発のもう1つの大きなシフトは、サーバーで生成された動的な Web ページから、 **AJAX 要求を通じてバックエンド Web api と**通信するクライアント側スクリプトから生成されたページの動的セクションを使用した静的初期マークアップへのシフトです。 このアーキテクチャシフトは、Web Api の増加と ASP.NET Web API framework の開発に役立ちました。 ASP.NET MVC の場合と同様に、ASP.NET Web API のリリースでは、さらにモジュール式のフレームワークとして ASP.NET をさらに進化させる機会が提供されています。 エンジニアリングチームは、この機会とビルドされた ASP.NET Web API を利用して、 **system.web で見つかったコアフレームワーク型に依存しないようにしました**。 これにより、2つのことが可能になりました。つまり、ASP.NET Web API は完全に自己完結した方法で進化する可能性がありました (また、NuGet を介して配信されるため、すぐに反復処理を継続できます)。 2つ目は、System.web に外部依存関係がなく、IIS への依存関係がないため、カスタムホスト (たとえば、コンソールアプリケーション、Windows サービスなど) で実行する機能が含まれている ASP.NET Web API です。

### <a name="the-future-a-nimble-framework"></a>将来: 機敏なフレームワーク

フレームワークのコンポーネントを相互に分離してから NuGet でリリースすることで、フレームワークが**個別に、より迅速に反復処理**できるようになりました。 さらに、Web API の自己ホスト機能の能力と柔軟性は、サービスに対して**小規模で軽量なホスト**を必要とする開発者にとって非常に魅力的です。 実際には、他のフレームワークもこの機能を必要としていました。そのため、各フレームワークは独自のホストプロセスで独自のベースアドレスを使用して実行され、個別に管理 (開始、停止など) する必要がありました。 最新の Web アプリケーションでは、一般に、静的ファイルサービス、動的ページ生成、Web API、および最近のリアルタイム/プッシュ通知をサポートしています。 これらの各サービスを個別に実行して管理する必要があるということは、単に現実的ではありませんでした。

必要とされるのは、開発者がさまざまなコンポーネントやフレームワークからアプリケーションを作成し、そのアプリケーションをサポートするホストで実行できるようにする、単一のホストの抽象化でした。

## <a name="the-open-web-interface-for-net-owin"></a>Open Web Interface for .NET (OWIN)

 Ruby コミュニティの[ラック](http://rack.github.io/)によって実現される利点により、Web サーバーとフレームワークコンポーネントの間の抽象化を作成するために、.net コミュニティのいくつかのメンバーが設定されています。 OWIN 抽象化の2つの設計目標は、単純であり、他の種類のフレームワークで考えられる依存関係を最小限に抑えたことでした。 これらの2つの目標は、次のことを保証します。

- 新しいコンポーネントは、より簡単に開発および使用できます。
- アプリケーションは、ホストと、場合によってはプラットフォームやオペレーティングシステム全体にわたって簡単に移植できます。

生成される抽象化は、2つのコア要素で構成されます。 1つ目は環境ディクショナリです。 このデータ構造は、HTTP 要求と応答の処理に必要なすべての状態と、関連するサーバーの状態を格納する役割を担います。 環境ディクショナリは次のように定義されます。

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

OWIN と互換性のある Web サーバーは、HTTP 要求と応答のボディストリームやヘッダーコレクションなどのデータを環境ディクショナリに設定する役割を担います。 次に、追加の値を使用してディクショナリを設定または更新し、応答本文ストリームに書き込むのは、アプリケーションまたはフレームワークコンポーネントの役割です。

OWIN 仕様では、環境ディクショナリの種類を指定するだけでなく、コアディクショナリのキーと値のペアの一覧を定義します。 たとえば、次の表は、HTTP 要求に必要なディクショナリキーを示しています。

| キーの名前 | 値の説明 |
| --- | --- |
| `"owin.RequestBody"` | 要求本文を含むストリーム (存在する場合)。 ストリーム。要求本文がない場合は、プレースホルダーとして使用できます。 [要求本文](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)を参照してください。 |
| `"owin.RequestHeaders"` | 要求ヘッダーの `IDictionary<string, string[]>`。 「[ヘッダー](http://owin.org/html/owin.html#3-3-headers)」を参照してください。 |
| `"owin.RequestMethod"` | 要求の HTTP 要求メソッド (`"GET"`、`"POST"`など) を格納している `string`。 |
| `"owin.RequestPath"` | 要求パスを格納している `string`。 パスは、アプリケーションデリゲートの "ルート" に対する相対パスである必要があります。「[パス](http://owin.org/html/owin.html#5-3-paths)」を参照してください。 |
| `"owin.RequestPathBase"` | アプリケーションデリゲートの "ルート" に対応する要求パスの部分を含む `string`。「[パス](http://owin.org/html/owin.html#5-3-paths)」を参照してください。 |
| `"owin.RequestProtocol"` | プロトコルの名前とバージョン (`"HTTP/1.0"` や `"HTTP/1.1"`など) を含む `string`。 |
| `"owin.RequestQueryString"` | HTTP 要求 URI のクエリ文字列コンポーネントを含む `string`。先頭に "?" は使用できません。(例: `"foo=bar&baz=quux"`)。 値は空の文字列でもかまいません。 |
| `"owin.RequestScheme"` | 要求に使用される URI スキームを含む `string` (例: `"http"`、`"https"`)。「 [URI スキーム](http://owin.org/html/owin.html#5-1-uri-scheme)」を参照してください。 |

OWIN の2番目のキー要素はアプリケーションデリゲートです。 これは、OWIN アプリケーションのすべてのコンポーネント間のプライマリインターフェイスとして機能する関数シグネチャです。 アプリケーションデリゲートの定義は次のとおりです。

`Func<IDictionary<string, object>, Task>;`

次に、アプリケーションデリゲートは、関数が環境ディクショナリを入力として受け取り、タスクを返す、Func デリゲート型の実装にすぎません。 この設計には、開発者にとっていくつかの影響があります。

- OWIN コンポーネントを記述するために必要な型の依存関係の数は非常に少なくなっています。 これにより、開発者にとって OWIN のアクセシビリティが大幅に向上します。
- 非同期デザインを使用すると、特に i/o 負荷の高い操作で、抽象化をコンピューティングリソースの処理に効率的に行うことができます。
- アプリケーションデリゲートはアトミック実行の単位であり、環境ディクショナリはデリゲートのパラメーターとして渡されるため、OWIN コンポーネントを簡単に連結して、複雑な HTTP 処理パイプラインを作成できます。

実装の観点から見ると、OWIN は仕様 ([http://owin.org/html/owin.html](http://owin.org/html/owin.html)) です。 その目的は、次の Web フレームワークではなく、Web フレームワークと Web サーバーがどのように対話するかを指定することです。

[OWIN](http://owin.org/)または[Katana](https://github.com/aspnet/AspNetKatana/wiki)を調査している場合は、 [OWIN NuGet パッケージ](http://nuget.org/packages/Owin)と OWIN にもご気になるかもしれません。 このライブラリには、 [Iappbuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)という1つのインターフェイスが含まれています。このインターフェイスは、OWIN 仕様の[セクション 4](http://owin.org/html/owin.html#4-application-startup)で説明されているスタートアップシーケンスを形式化して体系化します。 OWIN サーバーを構築するために必要ではありませんが、 [Iappbuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)インターフェイスは具体的な参照ポイントを提供し、Katana プロジェクトコンポーネントによって使用されます。

## <a name="project-katana"></a>プロジェクト Katana

[OWIN](http://owin.org/html/owin.html)の仕様と*OWIN*はどちらもコミュニティ所有であり、コミュニティはオープンソースの取り組みを実行しますが、 [Katana](https://github.com/aspnet/AspNetKatana/wiki)プロジェクトは、オープンソースである一方で Microsoft によってリリースされる OWIN コンポーネントのセットを表します。 これらのコンポーネントには、ホストとサーバーなどのインフラストラクチャコンポーネントと、 [SignalR](../../../signalr/index.md)や[ASP.NET Web API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)などのフレームワークへの認証コンポーネントやバインドなどの機能コンポーネントの両方が含まれます。 このプロジェクトには、次の3つの高レベルの目標があります。 

- **ポータブル**–新しいコンポーネントが使用可能になったときに、コンポーネントを簡単に置き換えることができる必要があります。 これには、フレームワークからサーバーおよびホストへのすべての種類のコンポーネントが含まれます。 この目標は、サードパーティのフレームワークがサードパーティのサーバーやホストで実行される可能性がありますが、Microsoft のサーバーでは、サードパーティのフレームワークをシームレスに実行できることを意味します。
- **モジュール型/柔軟性**-既定でオンになっている多くの機能を含む多数のフレームワークとは異なり、Katana プロジェクトコンポーネントは小規模であり、アプリケーションで使用するコンポーネントを決定するためにアプリケーション開発者に制御する必要があります。
- **軽量/パフォーマンス/スケーラブル**–フレームワークの従来の概念を、アプリケーション開発者によって明示的に追加される小さなフォーカスのあるコンポーネントのセットに分割することによって、Katana アプリケーションが使用するコンピューティングリソースが少なくなり、その結果、他の種類のサーバーやフレームワークと比べて負荷が増加します。 アプリケーションの要件によって、基盤となるインフラストラクチャからさらに多くの機能が必要になるため、OWIN パイプラインに追加することができますが、これはアプリケーション開発者の責任において明示的に決定する必要があります。 さらに、下位レベルのコンポーネントの態は、使用可能になったときに、新しい高パフォーマンスのサーバーをシームレスに導入することで、OWIN アプリケーションのパフォーマンスを向上させることができます。

## <a name="getting-started-with-katana-components"></a>Katana コンポーネントを使用したはじめに

初めて導入された[node.js](http://nodejs.org/)フレームワークの1つの側面は、簡単に言えば、Web サーバーを作成して実行できるというシンプルなものでした。 Katana の目標が[node.js](http://nodejs.org/)で囲まれている場合は、ASP.NET Web アプリケーションの開発について知っているすべてのことを開発者に強制することなく、 [node.js](http://nodejs.org/) (およびそのようなフレームワーク) の多くの利点を Katana が提供することによって、それらをまとめることができます。 このステートメントが true を保持するためには、Katana プロジェクトの作業の開始が、 [node.js](http://nodejs.org/)の場合と同様に単純である必要があります。

## <a name="creating-hello-world"></a>"Hello World!" を作成しています

JavaScript と .NET 開発の重要な違いの1つは、コンパイラの存在 (または欠如) です。 そのため、単純な Katana サーバーの開始点は、Visual Studio プロジェクトです。 ただし、空の ASP.NET Web アプリケーションであるプロジェクトの種類のうち、最も少ないものから始めることができます。

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

次に、 [Owin](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)という NuGet パッケージをプロジェクトにインストールします。 このパッケージは、ASP.NET request パイプラインで実行される OWIN サーバーを提供します。 このファイルは[NuGet ギャラリー](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)にあり、次のコマンドを使用して、Visual Studio の [パッケージマネージャー] ダイアログまたはパッケージマネージャーコンソールを使用してインストールできます。

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

`Microsoft.Owin.Host.SystemWeb` パッケージをインストールすると、いくつかの追加パッケージが依存関係としてインストールされます。 これらの依存関係の1つは `Microsoft.Owin`です。これは、OWIN アプリケーションを開発するためのいくつかのヘルパー型とメソッドを提供するライブラリです。 これらの型を使用して、次の "hello world" サーバーをすばやく記述できます。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

この非常に単純な Web サーバーは、Visual Studio の**F5**コマンドを使用して実行できるようになりました。また、デバッグを完全にサポートしています。

## <a name="switching-hosts"></a>ホストの切り替え

既定では、前の "hello world" の例は ASP.NET request パイプラインで実行され、IIS のコンテキストでは System.web が使用されます。 これにより、IIS の管理機能と全体的な成熟度を使用して OWIN パイプラインの柔軟性と省かを向上させることができるため、非常に大きな価値をもたらすことができます。 ただし、IIS で提供される利点が必要ではなく、より小規模で軽量なホストを使用する場合もあります。 IIS と System.web の外部で単純な Web サーバーを実行するために必要なことは何でしょうか。

移植性の目標を示すために、Web サーバーホストからコマンドラインホストに移動するには、新しいサーバーとホストの依存関係をプロジェクトの出力フォルダーに追加してから、ホストを起動するだけです。 この例では、Web サーバーを `OwinHost.exe` という名前の Katana ホストでホストし、Katana HttpListener ベースのサーバーを使用します。 他の Katana コンポーネントと同様に、これらは次のコマンドを使用して NuGet から取得されます。

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

次に、コマンドラインからプロジェクトルートフォルダーに移動して、(それぞれの NuGet パッケージの tools フォルダーにインストールされていた) `OwinHost.exe` を実行するだけです。 既定では、`OwinHost.exe` は HttpListener ベースのサーバーを検索するように構成されているため、追加の構成は必要ありません。 `http://localhost:5000/` するために Web ブラウザーで移動すると、コンソールを使用して現在実行中のアプリケーションが表示されます。

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana アーキテクチャ

 Katana コンポーネントアーキテクチャは、*ホスト、サーバー、ミドルウェア、* *アプリケーション*のように、アプリケーションを4つの論理層に分割します。 コンポーネントアーキテクチャは、多くの場合、アプリケーションの再コンパイルを必要とせずに、これらのレイヤーの実装を簡単に置き換えることができるように考慮されています。   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>Host

 ホストは次の役割を担います。

- 基になるプロセスを管理します。
- サーバーの選択と、要求の処理に使用される OWIN パイプラインの構築を実行するワークフローを調整します。

  現時点では、Katana ベースのアプリケーションには、次の3つの主要なホスティングオプションがあります。  
  
**Iis/ASP. NET**: 標準の HttpModule 型と HttpHandler 型を使用して、OWIN パイプラインを ASP.NET 要求フローの一部として iis で実行できます。 ASP.NET ホスティングのサポートは、Web アプリケーションプロジェクトに NuGet パッケージをインストールすることによって有効になります。 また、IIS はホストとサーバーの両方として機能するため、この NuGet パッケージでは OWIN サーバー/ホストの区別が行われます。つまり、SystemWeb ホストを使用している場合、開発者は代替サーバーの実装を置き換えることはできません。  
  
**カスタムホスト**: Katana component suite を使用すると、開発者は独自のカスタムプロセスでアプリケーションをホストできるようになります。これは、コンソールアプリケーション、Windows サービスなどになります。この機能は、Web API によって提供される自己ホスト機能に似ています。 次の例は、Web API コードのカスタムホストを示しています。  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana アプリケーションの自己ホストセットアップは次のようになります。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API と Katana の自己ホストの例の大きな違いの1つは、Web API 構成コードが Katana 自己ホストの例にないことです。 移植性と省かの両方を有効にするために、Katana は、サーバーを起動するコードを、要求処理パイプラインを構成するコードから分離します。 Web API を構成するコードは、クラス Startup に含まれています。これはさらに、WebApplication. Start の型パラメーターとして指定されています。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

Startup クラスの詳細については、この記事の後半で詳しく説明します。 ただし、Katana の自己ホストプロセスを開始するために必要なコードは、ASP.NET Web API 自己ホストアプリケーションで現在使用しているコードに似ています。

**Owinhost .exe**: Katana Web アプリケーションを実行するカスタムプロセスを記述する必要がありますが、多くの場合は、サーバーを起動してアプリケーションを実行できる、ビルド済みの実行可能ファイルを起動することをお勧めします。 このシナリオでは、Katana component suite に `OwinHost.exe`が含まれています。 プロジェクトのルートディレクトリ内から実行すると、この実行可能ファイルはサーバーを起動し (既定では HttpListener サーバーを使用します)、規約を使用してユーザーのスタートアップクラスを検索して実行します。 より詳細な制御を行うために、実行可能ファイルには多数の追加のコマンドラインパラメーターが用意されています。

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>サーバー

 ホストは、アプリケーションを実行するプロセスの開始と管理を担当しますが、サーバーの役割は、ネットワークソケットを開き、要求をリッスンし、ユーザーが指定した OWIN コンポーネントのパイプラインを通じて送信することです (既にお気付きかもしれませんが、このパイプラインはアプリケーション開発者のスタートアップクラスに指定されています。 現在、Katana プロジェクトには、次の2つのサーバー実装が含まれています。 

- **Owin**: 前述のように、ASP.NET パイプラインと連携する IIS は、ホストとサーバーの両方として機能します。 このため、このホストオプションを選択すると、IIS は、プロセスのアクティブ化や HTTP 要求のリッスンなどのホストレベルの問題を管理します。 ASP.NET Web アプリケーションの場合は、ASP.NET パイプラインに要求を送信します。 Katana SystemWeb ホストは、ASP.NET HttpModule と HttpHandler を登録して、HTTP パイプラインを通過し、ユーザーが指定した OWIN パイプラインを介して要求を送信するときに、要求をインターセプトします。
- **Owin HttpListener**: 名前が示すように、この Katana server は、.NET Framework の HttpListener クラスを使用してソケットを開き、要求を開発者が指定した Owin パイプラインに送信します。 これは現在、Katana セルフホスト API と OwinHost .exe の両方に対する既定のサーバー選択です。

## <a name="middlewareframework"></a>ミドルウェア/フレームワーク

 既に説明したように、サーバーはクライアントからの要求を受け入れるときに、開発者のスタートアップコードによって指定される OWIN コンポーネントのパイプラインを介してそれを渡す役割を担います。 これらのパイプラインコンポーネントはミドルウェアと呼ばれます。  
 非常に基本的なレベルでは、OWIN ミドルウェアコンポーネントは、呼び出し可能になるように OWIN アプリケーションデリゲートを実装するだけで済みます。

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

ただし、ミドルウェアコンポーネントの開発と構成を簡略化するために、Katana はミドルウェアコンポーネントのいくつかの規則とヘルパーの種類をサポートしています。 最も一般的なのは、`OwinMiddleware` クラスです。 このクラスを使用して構築されたカスタムミドルウェアコンポーネントは、次のようになります。 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 このクラスは `OwinMiddleware`から派生し、パイプライン内の次のミドルウェアのインスタンスをその引数の1つとして受け取り、それを基本コンストラクターに渡すコンストラクターを実装します。 ミドルウェアの構成に使用される追加の引数は、次のミドルウェアパラメーターの後にコンストラクターパラメーターとしても宣言されます。   
  
実行時には、オーバーライドされた `Invoke` メソッドを使用してミドルウェアが実行されます。 このメソッドは、型 `OwinContext`の1つの引数を受け取ります。 このコンテキストオブジェクトは、前に説明した `Microsoft.Owin` NuGet パッケージによって提供され、要求、応答、および環境ディクショナリへの厳密に型指定されたアクセスを提供し、いくつかの追加のヘルパー型を提供します。   
  
ミドルウェアクラスは、次のように、アプリケーションのスタートアップコードの OWIN パイプラインに簡単に追加できます。   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

Katana インフラストラクチャは、単純に OWIN ミドルウェアコンポーネントのパイプラインを構築するだけなので、コンポーネントはパイプラインに参加するためにアプリケーションデリゲートをサポートするだけで済むため、ミドルウェアコンポーネントは、単純な logger から ASP.NET、Web API、 [SignalR](../../../signalr/index.md)などのフレームワーク全体まで多岐にわたります。 たとえば、前の OWIN パイプラインに ASP.NET Web API を追加するには、次のスタートアップコードを追加する必要があります。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana インフラストラクチャは、構成メソッドの IAppBuilder オブジェクトに追加された順序に基づいて、ミドルウェアコンポーネントのパイプラインを構築します。 この例では、LoggerMiddleware は、これらの要求が最終的にどのように処理されるかに関係なく、パイプラインを通過するすべての要求を処理できます。 これにより、ミドルウェアコンポーネント (認証コンポーネントなど) が複数のコンポーネントとフレームワーク (ASP.NET Web API、SignalR、静的ファイルサーバーなど) を含むパイプラインの要求を処理できるという強力なシナリオが可能になります。
 
## <a name="applications"></a>[アプリケーション]

前の例で示したように、OWIN および Katana プロジェクトは、新しいアプリケーションプログラミングモデルと考えることはできません。また、アプリケーションのプログラミングモデルとフレームワークをサーバーおよびホストインフラストラクチャから分離するための抽象化として考える必要があります。 たとえば、Web API アプリケーションをビルドする場合、開発者フレームワークは、Katana プロジェクトのコンポーネントを使用する OWIN パイプラインでアプリケーションが実行されているかどうかに関係なく、引き続き ASP.NET Web API framework を使用します。 OWIN 関連のコードがアプリケーション開発者に表示される場所の1つは、開発者が OWIN パイプラインを作成するアプリケーションスタートアップコードです。 スタートアップコードでは、開発者は一連の UseXx ステートメントを登録します。通常は、受信要求を処理する各ミドルウェアコンポーネントに対して1つのステートメントを使用します。 このエクスペリエンスは、現在の System.web world に HTTP モジュールを登録するのと同じ効果があります。 通常は、ASP.NET Web API や[SignalR](../../../signalr/index.md)など、より大きなフレームワークミドルウェアがパイプラインの最後に登録されます。 認証やキャッシュなどの横断的なミドルウェアコンポーネントは、通常、パイプラインの先頭に登録されます。これにより、パイプラインの後半で登録されるすべてのフレームワークおよびコンポーネントに対する要求が処理されます。 このミドルウェアコンポーネントを相互に分離し、基盤となるインフラストラクチャコンポーネントから分離することにより、システム全体が安定した状態を維持しながら、さまざまな速度でコンポーネントを進化させることができます。

## <a name="components--nuget-packages"></a>コンポーネント– NuGet パッケージ

現在の多くのライブラリやフレームワークと同様に、Katana プロジェクトコンポーネントは一連の NuGet パッケージとして提供されます。 今後のバージョン2.0 では、Katana package 依存関係グラフは次のようになります。 (大きいビューの場合は画像をクリックします)。

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana プロジェクト内のほぼすべてのパッケージは、Owin パッケージで直接的または間接的に依存しています。 これは IAppBuilder インターフェイスを含むパッケージであることに注意してください。これは、OWIN 仕様のセクション4で説明されているアプリケーションの起動シーケンスの具象実装を提供します。 さらに、パッケージの多くは Owin に依存しています。これは、HTTP 要求と応答を処理するための一連のヘルパー型を提供します。 パッケージの残りの部分は、ホスティングインフラストラクチャパッケージ (サーバーまたはホスト) またはミドルウェアのいずれかとして分類できます。 Katana プロジェクトの外部にあるパッケージと依存関係はオレンジ色で表示されます。

Katana 2.0 のホスティングインフラストラクチャには、SystemWeb と HttpListener ベースのサーバー、OwinHost .exe を使用して OWIN アプリケーションを実行するための OwinHost パッケージ、および自己ホスト型の OWIN アプリケーションの Owin パッケージが含まれます。カスタムホスト (例: コンソールアプリケーション、Windows サービスなど)

Katana 2.0 では、ミドルウェアコンポーネントは主にさまざまな認証手段を提供することに重点を置いています。 診断用の追加のミドルウェアコンポーネントが1つ用意されています。これにより、開始ページとエラーページのサポートが有効になります。 OWIN が事実上ホストの抽象化に成長するにつれて、Microsoft とサードパーティによって開発されたミドルウェアコンポーネントのエコシステムも数が増加します。

## <a name="conclusion"></a>まとめ

 最初から、Katana プロジェクトの目標はまだ作成されていないため、開発者は他の Web フレームワークを学習できます。 代わりに、以前よりも多くの選択肢を .NET Web アプリケーション開発者に提供するための抽象化を作成することになりました。 一般的な Web アプリケーションスタックの論理層を交換可能なコンポーネントのセットに分割することにより、Katana プロジェクトでは、スタック全体のコンポーネントが、これらのコンポーネントにとって適切な速度で改善されるようになります。 単純な OWIN 抽象化に関連するすべてのコンポーネントを構築することにより、Katana は、フレームワークとその上に構築されたアプリケーションを、さまざまなサーバーやホストで移植できるようにします。 開発者がスタックを管理するようにすることで、Katana は、開発者が軽量の方法や機能豊富な Web スタックのしくみについて究極の選択を行うことができるようになります。  

## <a name="for-more-information-about-katana"></a>Katana の詳細については、

- GitHub の Katana プロジェクト: [https://github.com/aspnet/AspNetKatana/](https://github.com/aspnet/AspNetKatana/)。
- ビデオ: [KATANA OWIN for ASP.NET](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)、Howard Dierking。

## <a name="acknowledgements"></a>謝辞

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) Rick は、Azure と MVC に重点を置いた Microsoft のシニアプログラミングライターです。
- [Scott マン Selman](http://www.hanselman.com/blog/): (twitter [@shanselman](https://twitter.com/shanselman) )
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (twitter [@jongalloway](https://twitter.com/jongalloway) )
