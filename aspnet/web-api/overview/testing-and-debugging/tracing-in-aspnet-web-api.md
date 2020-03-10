---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2 | のトレースMicrosoft Docs
author: MikeWasson
description: ASP.NET Web API でトレースを有効にする方法について説明します。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484342"
---
# <a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 でのトレース

[Mike Wasson](https://github.com/MikeWasson)

> Web ベースのアプリケーションをデバッグしようとする場合、適切なトレースログのセットに代わるものはありません。 このチュートリアルでは、ASP.NET Web API でトレースを有効にする方法について説明します。 この機能を使用すると、コントローラーを呼び出す前と後の Web API フレームワークの動作をトレースできます。 また、独自のコードをトレースするために使用することもできます。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - [Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (visual studio 2015 でも動作)
> - Web API 2
> - [WebApi のトレース](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>Web API でのシステム診断のトレースの有効化

まず、新しい ASP.NET Web アプリケーションプロジェクトを作成します。 Visual Studio で、 **[ファイル]** メニューの [**新しい** > **プロジェクト**] をクリックします。 **[テンプレート]** の **[web]** で、 **[ASP.NET Web アプリケーション]** を選択します。

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

[Web API プロジェクト] テンプレートを選択します。

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

**[ツール]** メニューの **[NuGet パッケージマネージャー]** 、 **[パッケージ管理コンソール]** の順に選択します。

[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

最初のコマンドは、最新の Web API トレースパッケージをインストールします。 また、コア Web API パッケージも更新されます。 2番目のコマンドは、WebApi パッケージを最新バージョンに更新します。

> [!NOTE]
> 特定のバージョンの Web API を対象にする場合は、トレースパッケージをインストールするときに-Version フラグを使用します。

アプリ\_の [開始] フォルダーで WebApiConfig.cs ファイルを開きます。 **Register**メソッドに次のコードを追加します。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

このコードは、Web API パイプラインに[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)クラスを追加します。 **SystemDiagnosticsTraceWriter**クラスはトレースを[トレース](https://msdn.microsoft.com/library/system.diagnostics.trace)に書き込みます。

トレースを表示するには、デバッガーでアプリケーションを実行します。 ブラウザーで `/api/values` にアクセスします。

![](tracing-in-aspnet-web-api/_static/image5.png)

トレースステートメントは、Visual Studio の出力ウィンドウに書き込まれます。 ( **[表示]** メニューの **[出力]** を選択します)。

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

**SystemDiagnosticsTraceWriter**はトレースをトレースに書き込むため、**追加のトレース**リスナーを登録できます。たとえば、トレースをログファイルに書き込むことができます。 トレースライターの詳細については、MSDN の「[トレースリスナー](https://msdn.microsoft.com/library/4y5y10s7.aspx) 」を参照してください。

### <a name="configuring-systemdiagnosticstracewriter"></a>SystemDiagnosticsTraceWriter の構成

次のコードは、トレースライターを構成する方法を示しています。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

次の2つの設定を制御できます。

- IsVerbose: false の場合、各トレースには最小限の情報が含まれます。 True の場合、トレースには詳細情報が含まれます。
- MinimumLevel: 最小トレースレベルを設定します。 トレースレベルは、デバッグ、情報、警告、エラー、および致命的です。

## <a name="adding-traces-to-your-web-api-application"></a>Web API アプリケーションにトレースを追加する

トレースライターを追加すると、Web API パイプラインによって作成されたトレースにすぐにアクセスできるようになります。 トレースライターを使用して、独自のコードをトレースすることもできます。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

トレースライターを取得するには、 **Httpconfiguration. service. GetTraceWriter**を呼び出します。 コントローラーから、このメソッドには**ApiController**プロパティを使用してアクセスできます。

トレースを書き込むには、 **ITraceWriter**メソッドを直接呼び出すことができますが、 [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)クラスは、よりわかりやすいいくつかの拡張メソッドを定義します。 たとえば、上に示した**info**メソッドでは、トレースレベル**情報**を含むトレースが作成されます。

## <a name="web-api-tracing-infrastructure"></a>Web API トレースインフラストラクチャ

このセクションでは、Web API のカスタムトレースライターを記述する方法について説明します。

WebApi パッケージは、Web API のより一般的なトレースインフラストラクチャの上に構築されています。 WebApi を使用する代わりに、 [Nlog](http://nlog-project.org/)や[log4net](http://logging.apache.org/log4net/)など、他のトレース/ログライブラリをプラグインすることもできます。

トレースを収集するには、 **ITraceWriter**インターフェイスを実装します。 次に、簡単な例を示します。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**ITraceWriter**メソッドは、トレースを作成します。 呼び出し元は、カテゴリとトレースレベルを指定します。 カテゴリには、任意のユーザー定義文字列を指定できます。 **トレース**の実装では、次の操作を行う必要があります。

1. 新しい**TraceRecord**を作成します。 以下に示すように、要求、カテゴリ、およびトレースレベルで初期化します。 これらの値は、呼び出し元によって提供されます。
2. *Traceaction*デリゲートを呼び出します。 このデリゲートの内部では、呼び出し元は**TraceRecord**の残りの部分を埋める必要があります。
3. 任意のログ記録技法を使用して、 **TraceRecord**を記述します。 次に示す例では、単に**system.string を呼び出します。**

## <a name="setting-the-trace-writer"></a>トレースライターの設定

トレースを有効にするには、 **ITraceWriter**の実装を使用するように Web API を構成する必要があります。 これを行うには、次のコードに示すように、 **Httpconfiguration**オブジェクトを使用します。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

アクティブにできるトレースライターは1つだけです。 既定では、Web API は、何も実行しない &quot;no op&quot; トレーサーを設定します。 (トレースを書き込む前にトレースライターが**null**であるかどうかをトレースコードで確認する必要がないように、&quot;no op&quot; トレーサーが存在します)。

## <a name="how-web-api-tracing-works"></a>Web API トレースのしくみ

Web API でのトレースは、*ファサード*パターンを使用します。トレースが有効になっている場合、web api は、要求パイプラインのさまざまな部分を、トレース呼び出しを実行するクラスとラップします。

たとえば、コントローラーを選択すると、パイプラインでは**IHttpControllerSelector**インターフェイスが使用されます。 トレースを有効にすると、パイプラインは**IHttpControllerSelector**を実装するクラスを挿入しますが、実際の実装に対してを呼び出します。

![Web API トレースでは、ファサードパターンを使用します。](tracing-in-aspnet-web-api/_static/image8.png)

この設計の利点は次のとおりです。

- トレースライターを追加しない場合、トレースコンポーネントはインスタンス化されず、パフォーマンスに影響しません。
- **IHttpControllerSelector**などの既定のサービスを独自のカスタム実装に置き換える場合、トレースはラッパーオブジェクトによって実行されるため、トレースは影響を受けません。

既定の**Itracemanager**サービスを置き換えることで、Web API トレースフレームワーク全体を独自のカスタムフレームワークに置き換えることもできます。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

トレースシステムを初期化するには、 **Itracemanager. initialize**を実装します。 これにより、Web API に組み込まれているすべてのトレースコードを含め、トレースフレームワーク*全体*が置換されることに注意してください。
