---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN と Katana | を使用したはじめにMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472444"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="ae563-102">OWIN と Katana の概要</span><span class="sxs-lookup"><span data-stu-id="ae563-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="ae563-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ae563-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ae563-104">[Open Web Interface for .net (OWIN)](http://owin.org/)は、.net web サーバーと web アプリケーションの間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="ae563-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="ae563-105">OWIN を使用すると、web サーバーをアプリケーションから分離することで、.NET web 開発用のミドルウェアを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="ae563-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="ae563-106">また、OWIN を使用すると、Windows サービスやその他&#8212;のプロセスでの自己ホストなど、web アプリケーションを他のホストに移植しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="ae563-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="ae563-107">OWIN は、実装ではなく、コミュニティ所有の仕様です。</span><span class="sxs-lookup"><span data-stu-id="ae563-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="ae563-108">Katana プロジェクトは、Microsoft によって開発されたオープンソースの OWIN コンポーネントのセットです。</span><span class="sxs-lookup"><span data-stu-id="ae563-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="ae563-109">OWIN と Katana の両方の概要については、「 [Project Katana の概要](an-overview-of-project-katana.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ae563-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="ae563-110">この記事では、作業を開始するためにコードにすぐに進みます。</span><span class="sxs-lookup"><span data-stu-id="ae563-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="ae563-111">このチュートリアルでは[Visual Studio 2013 リリース候補](https://go.microsoft.com/fwlink/?LinkId=306566)を使用しますが、Visual Studio 2012 を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="ae563-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="ae563-112">いくつかの手順は Visual Studio 2012 では異なりますが、以下の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="ae563-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="ae563-113">IIS でのホスト OWIN</span><span class="sxs-lookup"><span data-stu-id="ae563-113">Host OWIN in IIS</span></span>

<span data-ttu-id="ae563-114">このセクションでは、IIS で OWIN をホストします。</span><span class="sxs-lookup"><span data-stu-id="ae563-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="ae563-115">このオプションを使用すると、OWIN パイプラインの柔軟性と省かが、IIS の成熟した機能セットと共に得られます。</span><span class="sxs-lookup"><span data-stu-id="ae563-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="ae563-116">このオプションを使用すると、OWIN アプリケーションは ASP.NET request パイプラインで実行されます。</span><span class="sxs-lookup"><span data-stu-id="ae563-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="ae563-117">最初に、新しい ASP.NET Web アプリケーションプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="ae563-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="ae563-118">(Visual Studio 2012 では、ASP.NET 空の Web アプリケーションプロジェクトの種類を使用します。)</span><span class="sxs-lookup"><span data-stu-id="ae563-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="ae563-119">**[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="ae563-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="ae563-120">NuGet パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae563-120">Add NuGet Packages</span></span>

<span data-ttu-id="ae563-121">次に、必要な NuGet パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae563-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="ae563-122">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ae563-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ae563-123">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ae563-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="ae563-124">Startup クラスを追加する</span><span class="sxs-lookup"><span data-stu-id="ae563-124">Add a Startup Class</span></span>

<span data-ttu-id="ae563-125">次に、OWIN startup クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="ae563-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="ae563-126">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="ae563-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="ae563-127">**[新しい項目の追加]** ダイアログで、 **[Owin Startup class]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ae563-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="ae563-128">Startup クラスの構成の詳細については、「 [OWIN Startup Class Detection](owin-startup-class-detection.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ae563-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="ae563-129">次のコードを `Startup1.Configuration` メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="ae563-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="ae563-130">このコードは、OWIN パイプラインに単純なミドルウェアを追加し、 **OWIN**インスタンスを受け取る関数として実装します。</span><span class="sxs-lookup"><span data-stu-id="ae563-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="ae563-131">サーバーが HTTP 要求を受信すると、OWIN パイプラインはミドルウェアを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ae563-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="ae563-132">ミドルウェアは、応答のコンテンツタイプを設定し、応答本文を書き込みます。</span><span class="sxs-lookup"><span data-stu-id="ae563-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="ae563-133">OWIN Startup クラステンプレートは、Visual Studio 2013 で使用できます。</span><span class="sxs-lookup"><span data-stu-id="ae563-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="ae563-134">Visual Studio 2012 を使用している場合は、`Startup1`という名前の新しい空のクラスを追加し、次のコードを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ae563-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="ae563-135">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="ae563-135">Run the Application</span></span>

<span data-ttu-id="ae563-136">F5 キーを押してデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="ae563-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="ae563-137">Visual Studio によってブラウザーウィンドウが開き、`http://localhost:*port*/`します。</span><span class="sxs-lookup"><span data-stu-id="ae563-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="ae563-138">ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ae563-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="ae563-139">コンソールアプリケーションでの自己ホスト OWIN</span><span class="sxs-lookup"><span data-stu-id="ae563-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="ae563-140">カスタムプロセスでは、このアプリケーションを IIS ホスティングから自己ホスト型に簡単に変換できます。</span><span class="sxs-lookup"><span data-stu-id="ae563-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="ae563-141">Iis をホストすると、IIS は、サービスをホストするプロセスとして、HTTP サーバーとの両方として機能します。</span><span class="sxs-lookup"><span data-stu-id="ae563-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="ae563-142">自己ホストを使用すると、アプリケーションはプロセスを作成し、 **HttpListener**クラスを HTTP サーバーとして使用します。</span><span class="sxs-lookup"><span data-stu-id="ae563-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="ae563-143">Visual Studio で、新しいコンソール アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="ae563-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="ae563-144">[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ae563-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="ae563-145">このチュートリアルのパート1の `Startup1` クラスをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="ae563-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="ae563-146">このクラスを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="ae563-146">You don't need to modify this class.</span></span>

<span data-ttu-id="ae563-147">次のように、アプリケーションの `Main` メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="ae563-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="ae563-148">コンソールアプリケーションを実行すると、サーバーは `http://localhost:9000`のリッスンを開始します。</span><span class="sxs-lookup"><span data-stu-id="ae563-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="ae563-149">Web ブラウザーでこのアドレスに移動すると、"Hello world" というページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae563-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="ae563-150">OWIN 診断の追加</span><span class="sxs-lookup"><span data-stu-id="ae563-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="ae563-151">Owin パッケージには、未処理の例外をキャッチし、エラーの詳細を示す HTML ページを表示するミドルウェアが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ae563-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="ae563-152">このページは、"[黄色いスクリーン](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)(YSOD)" と呼ばれることがある ASP.NET エラーページとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="ae563-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="ae563-153">YSOD と同様、Katana エラーページは開発時に役立ちますが、運用モードで無効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ae563-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="ae563-154">プロジェクトに診断パッケージをインストールするには、パッケージマネージャーコンソールウィンドウで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ae563-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="ae563-155">`Startup1.Configuration` メソッドのコードを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="ae563-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="ae563-156">ここで、CTRL キーを押しながら F5 キーを押してデバッグなしでアプリケーションを実行し、Visual Studio が例外で中断しないようにします。</span><span class="sxs-lookup"><span data-stu-id="ae563-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="ae563-157">アプリケーションは前と同じように動作します。 `http://localhost/fail`に移動するまで、アプリケーションは例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="ae563-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="ae563-158">エラーページミドルウェアは、例外をキャッチし、エラーに関する情報を含む HTML ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="ae563-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="ae563-159">タブをクリックすると、スタック、クエリ文字列、cookie、要求ヘッダー、および OWIN 環境変数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae563-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="ae563-160">次の手順</span><span class="sxs-lookup"><span data-stu-id="ae563-160">Next Steps</span></span>

- [<span data-ttu-id="ae563-161">OWIN スタートアップ クラス検出</span><span class="sxs-lookup"><span data-stu-id="ae563-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="ae563-162">OWIN を使用して自己ホスト ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="ae563-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="ae563-163">OWIN を使用して SignalR をセルフホストする</span><span class="sxs-lookup"><span data-stu-id="ae563-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
