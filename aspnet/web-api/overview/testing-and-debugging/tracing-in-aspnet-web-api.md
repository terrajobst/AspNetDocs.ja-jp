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
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="ab37d-103">ASP.NET Web API 2 でのトレース</span><span class="sxs-lookup"><span data-stu-id="ab37d-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="ab37d-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ab37d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="ab37d-105">Web ベースのアプリケーションをデバッグしようとする場合、適切なトレースログのセットに代わるものはありません。</span><span class="sxs-lookup"><span data-stu-id="ab37d-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="ab37d-106">このチュートリアルでは、ASP.NET Web API でトレースを有効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="ab37d-107">この機能を使用すると、コントローラーを呼び出す前と後の Web API フレームワークの動作をトレースできます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="ab37d-108">また、独自のコードをトレースするために使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ab37d-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="ab37d-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="ab37d-110">[Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (visual studio 2015 でも動作)</span><span class="sxs-lookup"><span data-stu-id="ab37d-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="ab37d-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="ab37d-111">Web API 2</span></span>
> - [<span data-ttu-id="ab37d-112">WebApi のトレース</span><span class="sxs-lookup"><span data-stu-id="ab37d-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="ab37d-113">Web API でのシステム診断のトレースの有効化</span><span class="sxs-lookup"><span data-stu-id="ab37d-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="ab37d-114">まず、新しい ASP.NET Web アプリケーションプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="ab37d-115">Visual Studio で、 **[ファイル]** メニューの [**新しい** > **プロジェクト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ab37d-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="ab37d-116">**[テンプレート]** の **[web]** で、 **[ASP.NET Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="ab37d-117">[Web API プロジェクト] テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="ab37d-118">**[ツール]** メニューの **[NuGet パッケージマネージャー]** 、 **[パッケージ管理コンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="ab37d-119">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="ab37d-120">最初のコマンドは、最新の Web API トレースパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ab37d-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="ab37d-121">また、コア Web API パッケージも更新されます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="ab37d-122">2番目のコマンドは、WebApi パッケージを最新バージョンに更新します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="ab37d-123">特定のバージョンの Web API を対象にする場合は、トレースパッケージをインストールするときに-Version フラグを使用します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="ab37d-124">アプリ\_の [開始] フォルダーで WebApiConfig.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="ab37d-125">**Register**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="ab37d-126">このコードは、Web API パイプラインに[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="ab37d-127">**SystemDiagnosticsTraceWriter**クラスはトレースを[トレース](https://msdn.microsoft.com/library/system.diagnostics.trace)に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="ab37d-128">トレースを表示するには、デバッガーでアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="ab37d-129">ブラウザーで `/api/values` にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="ab37d-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="ab37d-130">トレースステートメントは、Visual Studio の出力ウィンドウに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="ab37d-131">( **[表示]** メニューの **[出力]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="ab37d-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="ab37d-132">**SystemDiagnosticsTraceWriter**はトレースをトレースに書き込むため、**追加のトレース**リスナーを登録できます。たとえば、トレースをログファイルに書き込むことができます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="ab37d-133">トレースライターの詳細については、MSDN の「[トレースリスナー](https://msdn.microsoft.com/library/4y5y10s7.aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ab37d-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="ab37d-134">SystemDiagnosticsTraceWriter の構成</span><span class="sxs-lookup"><span data-stu-id="ab37d-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="ab37d-135">次のコードは、トレースライターを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ab37d-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="ab37d-136">次の2つの設定を制御できます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="ab37d-137">IsVerbose: false の場合、各トレースには最小限の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="ab37d-138">True の場合、トレースには詳細情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-138">If true, traces include more information.</span></span>
- <span data-ttu-id="ab37d-139">MinimumLevel: 最小トレースレベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="ab37d-140">トレースレベルは、デバッグ、情報、警告、エラー、および致命的です。</span><span class="sxs-lookup"><span data-stu-id="ab37d-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="ab37d-141">Web API アプリケーションにトレースを追加する</span><span class="sxs-lookup"><span data-stu-id="ab37d-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="ab37d-142">トレースライターを追加すると、Web API パイプラインによって作成されたトレースにすぐにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="ab37d-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="ab37d-143">トレースライターを使用して、独自のコードをトレースすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="ab37d-144">トレースライターを取得するには、 **Httpconfiguration. service. GetTraceWriter**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="ab37d-145">コントローラーから、このメソッドには**ApiController**プロパティを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="ab37d-146">トレースを書き込むには、 **ITraceWriter**メソッドを直接呼び出すことができますが、 [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)クラスは、よりわかりやすいいくつかの拡張メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="ab37d-147">たとえば、上に示した**info**メソッドでは、トレースレベル**情報**を含むトレースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="ab37d-148">Web API トレースインフラストラクチャ</span><span class="sxs-lookup"><span data-stu-id="ab37d-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="ab37d-149">このセクションでは、Web API のカスタムトレースライターを記述する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="ab37d-150">WebApi パッケージは、Web API のより一般的なトレースインフラストラクチャの上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="ab37d-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="ab37d-151">WebApi を使用する代わりに、 [Nlog](http://nlog-project.org/)や[log4net](http://logging.apache.org/log4net/)など、他のトレース/ログライブラリをプラグインすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="ab37d-152">トレースを収集するには、 **ITraceWriter**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="ab37d-153">次に、簡単な例を示します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="ab37d-154">**ITraceWriter**メソッドは、トレースを作成します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="ab37d-155">呼び出し元は、カテゴリとトレースレベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="ab37d-156">カテゴリには、任意のユーザー定義文字列を指定できます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-156">The category can be any user-defined string.</span></span> <span data-ttu-id="ab37d-157">**トレース**の実装では、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab37d-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="ab37d-158">新しい**TraceRecord**を作成します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="ab37d-159">以下に示すように、要求、カテゴリ、およびトレースレベルで初期化します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="ab37d-160">これらの値は、呼び出し元によって提供されます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="ab37d-161">*Traceaction*デリゲートを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="ab37d-162">このデリゲートの内部では、呼び出し元は**TraceRecord**の残りの部分を埋める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab37d-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="ab37d-163">任意のログ記録技法を使用して、 **TraceRecord**を記述します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="ab37d-164">次に示す例では、単に**system.string を呼び出します。**</span><span class="sxs-lookup"><span data-stu-id="ab37d-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="ab37d-165">トレースライターの設定</span><span class="sxs-lookup"><span data-stu-id="ab37d-165">Setting the Trace Writer</span></span>

<span data-ttu-id="ab37d-166">トレースを有効にするには、 **ITraceWriter**の実装を使用するように Web API を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab37d-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="ab37d-167">これを行うには、次のコードに示すように、 **Httpconfiguration**オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="ab37d-168">アクティブにできるトレースライターは1つだけです。</span><span class="sxs-lookup"><span data-stu-id="ab37d-168">Only one trace writer can be active.</span></span> <span data-ttu-id="ab37d-169">既定では、Web API は、何も実行しない &quot;no op&quot; トレーサーを設定します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="ab37d-170">(トレースを書き込む前にトレースライターが**null**であるかどうかをトレースコードで確認する必要がないように、&quot;no op&quot; トレーサーが存在します)。</span><span class="sxs-lookup"><span data-stu-id="ab37d-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="ab37d-171">Web API トレースのしくみ</span><span class="sxs-lookup"><span data-stu-id="ab37d-171">How Web API Tracing Works</span></span>

<span data-ttu-id="ab37d-172">Web API でのトレースは、*ファサード*パターンを使用します。トレースが有効になっている場合、web api は、要求パイプラインのさまざまな部分を、トレース呼び出しを実行するクラスとラップします。</span><span class="sxs-lookup"><span data-stu-id="ab37d-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="ab37d-173">たとえば、コントローラーを選択すると、パイプラインでは**IHttpControllerSelector**インターフェイスが使用されます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="ab37d-174">トレースを有効にすると、パイプラインは**IHttpControllerSelector**を実装するクラスを挿入しますが、実際の実装に対してを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API トレースでは、ファサードパターンを使用します。](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="ab37d-176">この設計の利点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ab37d-176">The benefits of this design include:</span></span>

- <span data-ttu-id="ab37d-177">トレースライターを追加しない場合、トレースコンポーネントはインスタンス化されず、パフォーマンスに影響しません。</span><span class="sxs-lookup"><span data-stu-id="ab37d-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="ab37d-178">**IHttpControllerSelector**などの既定のサービスを独自のカスタム実装に置き換える場合、トレースはラッパーオブジェクトによって実行されるため、トレースは影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="ab37d-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="ab37d-179">既定の**Itracemanager**サービスを置き換えることで、Web API トレースフレームワーク全体を独自のカスタムフレームワークに置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="ab37d-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="ab37d-180">トレースシステムを初期化するには、 **Itracemanager. initialize**を実装します。</span><span class="sxs-lookup"><span data-stu-id="ab37d-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="ab37d-181">これにより、Web API に組み込まれているすべてのトレースコードを含め、トレースフレームワーク*全体*が置換されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ab37d-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
