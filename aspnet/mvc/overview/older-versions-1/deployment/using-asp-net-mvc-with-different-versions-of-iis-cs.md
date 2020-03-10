---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: ASP.NET MVC を使用して、さまざまなバージョンの IIS (C#) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、さまざまなバージョンのインターネットインフォメーションサービスで ASP.NET MVC と URL ルーティングを使用する方法について説明します。 さまざまな戦略を学習できます...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 3b0a9509c0600f3598fd1218a7b383430548d4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486526"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a><span data-ttu-id="6c924-104">ASP.NET MVC を使用して、さまざまなバージョンの IIS (C#)</span><span class="sxs-lookup"><span data-stu-id="6c924-104">Using ASP.NET MVC with Different Versions of IIS (C#)</span></span>

<span data-ttu-id="6c924-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6c924-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6c924-106">このチュートリアルでは、さまざまなバージョンのインターネットインフォメーションサービスで ASP.NET MVC と URL ルーティングを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6c924-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="6c924-107">Iis 7.0 (クラシックモード)、IIS 6.0、およびそれより前のバージョンの IIS で ASP.NET MVC を使用するためのさまざまな方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6c924-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="6c924-108">ASP.NET MVC フレームワークは、ASP.NET ルーティングに依存して、ブラウザー要求をコントローラーアクションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="6c924-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="6c924-109">ASP.NET ルーティングを活用するために、web サーバーで追加の構成手順を実行することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="6c924-110">これはすべて、アプリケーションのバージョンインターネットインフォメーションサービス (IIS) と要求処理モードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="6c924-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="6c924-111">IIS のさまざまなバージョンの概要を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6c924-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="6c924-112">IIS 7.0 (統合モード)-ASP.NET ルーティングを使用するために特別な構成は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="6c924-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="6c924-113">IIS 7.0 (クラシックモード)-ASP.NET ルーティングを使用するには、特別な構成を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="6c924-114">IIS 6.0 以下-ASP.NET ルーティングを使用するには、特別な構成を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="6c924-115">IIS の最新バージョンは、バージョン 7.5 (Win7) です。</span><span class="sxs-lookup"><span data-stu-id="6c924-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="6c924-116">Iis 7 の iis 7 は、Windows Server 2008 および VISTA/SP1 以降に含まれています。</span><span class="sxs-lookup"><span data-stu-id="6c924-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="6c924-117">また、Home Basic 以外のすべてのバージョンの Vista オペレーティングシステムに IIS 7.0 をインストールすることもできます (「 [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="6c924-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="6c924-118">IIS 7.0 は、要求を処理する2つのモードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="6c924-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="6c924-119">統合モードまたはクラシックモードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="6c924-120">統合モードで IIS 7.0 を使用する場合は、特別な構成手順を実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6c924-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="6c924-121">ただし、クラシックモードで IIS 7.0 を使用する場合は、追加の構成を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="6c924-122">Microsoft Windows Server 2003 には、IIS 6.0 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6c924-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="6c924-123">Windows Server 2003 オペレーティングシステムを使用している場合は、iis 6.0 を IIS 7.0 にアップグレードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6c924-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="6c924-124">IIS 6.0 を使用する場合は、追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="6c924-125">Microsoft Windows XP Professional には IIS 5.1 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6c924-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="6c924-126">IIS 5.1 を使用する場合は、追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="6c924-127">最後に、Microsoft Windows 2000 および Microsoft Windows 2000 Professional には IIS 5.0 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6c924-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="6c924-128">IIS 5.0 を使用する場合は、追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="6c924-129">統合モードとクラシックモード</span><span class="sxs-lookup"><span data-stu-id="6c924-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="6c924-130">IIS 7.0 では、統合とクラシックの2つの異なる要求処理モードを使用して要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="6c924-131">統合モードでは、パフォーマンスが向上し、機能も強化されます。</span><span class="sxs-lookup"><span data-stu-id="6c924-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="6c924-132">クラシックモードは、以前のバージョンの IIS との下位互換性のために用意されています。</span><span class="sxs-lookup"><span data-stu-id="6c924-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="6c924-133">要求処理モードは、アプリケーションプールによって決定されます。</span><span class="sxs-lookup"><span data-stu-id="6c924-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="6c924-134">特定の web アプリケーションによって使用されている処理モードを特定するには、アプリケーションに関連付けられているアプリケーションプールを決定します。</span><span class="sxs-lookup"><span data-stu-id="6c924-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="6c924-135">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="6c924-135">Follow these steps:</span></span>

1. <span data-ttu-id="6c924-136">インターネットインフォメーションサービスマネージャーを起動する</span><span class="sxs-lookup"><span data-stu-id="6c924-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="6c924-137">[接続] ウィンドウで、アプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c924-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="6c924-138">アクション] ウィンドウで、 **[基本設定]** リンクをクリックして [アプリケーションの編集 ダイアログボックスを開きます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="6c924-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="6c924-139">選択したアプリケーションプールをメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="6c924-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="6c924-140">既定では、IIS は、 **DefaultAppPool**と**クラシック .net AppPool**という2つのアプリケーションプールをサポートするように構成されています。</span><span class="sxs-lookup"><span data-stu-id="6c924-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="6c924-141">DefaultAppPool が選択されている場合、アプリケーションは統合要求処理モードで実行されています。</span><span class="sxs-lookup"><span data-stu-id="6c924-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="6c924-142">クラシック .NET AppPool が選択されている場合は、アプリケーションがクラシック要求処理モードで実行されています。</span><span class="sxs-lookup"><span data-stu-id="6c924-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="6c924-143">[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6c924-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span></span>

<span data-ttu-id="6c924-144">**図 1**: 要求処理モードの検出 ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="6c924-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span></span>

<span data-ttu-id="6c924-145">[アプリケーションの編集] ダイアログボックスで要求処理モードを変更できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6c924-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="6c924-146">[選択] ボタンをクリックし、アプリケーションに関連付けられているアプリケーションプールを変更します。</span><span class="sxs-lookup"><span data-stu-id="6c924-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="6c924-147">ASP.NET アプリケーションをクラシックモードから統合モードに変更するときは、互換性の問題があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6c924-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="6c924-148">詳細については、次の記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6c924-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="6c924-149">Windows Vista および Windows Server 2008 で ASP.NET 1.1 を IIS 7.0 にアップグレードする-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="6c924-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>
- <span data-ttu-id="6c924-150">ASP.NET と IIS 7.0 の統合- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="6c924-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="6c924-151">ASP.NET アプリケーションで DefaultAppPool が使用されている場合、ASP.NET Routing (したがって ASP.NET MVC) を機能させるために追加の手順を実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6c924-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="6c924-152">ただし、ASP.NET アプリケーションが従来の .NET AppPool を使用するように構成されている場合は、次の作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="6c924-153">以前のバージョンの IIS での ASP.NET MVC の使用</span><span class="sxs-lookup"><span data-stu-id="6c924-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="6c924-154">Iis 7.0 よりも前のバージョンの IIS で ASP.NET MVC を使用する必要がある場合、またはクラシックモードで IIS 7.0 を使用する必要がある場合は、2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="6c924-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="6c924-155">まず、ファイル拡張子を使用するようにルートテーブルを変更できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="6c924-156">たとえば、/Store.aspx/Details. のような URL を要求するのではなく、URL を要求します。</span><span class="sxs-lookup"><span data-stu-id="6c924-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="6c924-157">2つ目の方法は、*ワイルドカードスクリプトマップ*と呼ばれるものを作成することです。</span><span class="sxs-lookup"><span data-stu-id="6c924-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="6c924-158">ワイルドカードスクリプトマップを使用すると、すべての要求を ASP.NET フレームワークにマップできます。</span><span class="sxs-lookup"><span data-stu-id="6c924-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="6c924-159">Web サーバーにアクセスできない場合 (たとえば、ASP.NET MVC アプリケーションがインターネットサービスプロバイダーによってホストされている場合) は、最初のオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="6c924-160">Url の外観を変更したくない場合に、web サーバーにアクセスできるようにするには、2番目のオプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="6c924-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="6c924-161">各オプションについては、次のセクションで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="6c924-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="6c924-162">ルートテーブルへの拡張機能の追加</span><span class="sxs-lookup"><span data-stu-id="6c924-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="6c924-163">以前のバージョンの IIS で動作するように ASP.NET ルーティングを取得する最も簡単な方法は、global.asax ファイルのルートテーブルを変更することです。</span><span class="sxs-lookup"><span data-stu-id="6c924-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="6c924-164">リスト1の既定および変更されていない global.asax ファイルは、既定のルートという名前のルートを1つ構成します。</span><span class="sxs-lookup"><span data-stu-id="6c924-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="6c924-165">**リスト 1-global.asax (変更なし)**</span><span class="sxs-lookup"><span data-stu-id="6c924-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

<span data-ttu-id="6c924-166">リスト1で構成された既定のルートでは、次のような Url をルーティングできます。</span><span class="sxs-lookup"><span data-stu-id="6c924-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="6c924-167">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="6c924-167">/Home/Index</span></span>

<span data-ttu-id="6c924-168">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="6c924-168">/Product/Details/3</span></span>

<span data-ttu-id="6c924-169">/Product</span><span class="sxs-lookup"><span data-stu-id="6c924-169">/Product</span></span>

<span data-ttu-id="6c924-170">残念ながら、以前のバージョンの IIS では、これらの要求を ASP.NET フレームワークに渡すことはできません。</span><span class="sxs-lookup"><span data-stu-id="6c924-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="6c924-171">そのため、これらの要求はコントローラーにルーティングされません。</span><span class="sxs-lookup"><span data-stu-id="6c924-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="6c924-172">たとえば、URL/Home/Index にブラウザーの要求を行うと、図2のエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c924-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="6c924-173">[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6c924-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span></span>

<span data-ttu-id="6c924-174">**図 2**: 404 が見つからないというエラーを受信[する (クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="6c924-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span></span>

<span data-ttu-id="6c924-175">以前のバージョンの IIS では、特定の要求が ASP.NET フレームワークにのみマップされています。</span><span class="sxs-lookup"><span data-stu-id="6c924-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="6c924-176">要求は、正しいファイル拡張子を持つ URL に対してである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="6c924-177">たとえば、/SomePage.aspx の要求は ASP.NET フレームワークにマップされます。</span><span class="sxs-lookup"><span data-stu-id="6c924-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="6c924-178">ただし、/SomePage.htm の要求ではありません。</span><span class="sxs-lookup"><span data-stu-id="6c924-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="6c924-179">そのため、ASP.NET ルーティングを機能させるには、ASP.NET フレームワークにマップされているファイル拡張子が含まれるように、既定のルートを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="6c924-180">これを行うには、`registermvc.wsf`という名前のスクリプトを使用します。</span><span class="sxs-lookup"><span data-stu-id="6c924-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="6c924-181">これは `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`の ASP.NET MVC 1 リリースに含まれていましたが、ASP.NET 2 の時点では、このスクリプトは ASP.NET フューチャに移動され、 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="6c924-182">このスクリプトを実行すると、IIS に新しい mvc 拡張機能が登録されます。</span><span class="sxs-lookup"><span data-stu-id="6c924-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="6c924-183">Mvc 拡張機能を登録した後で、グローバルな global.asax ファイル内のルートを変更して、ルートが mvc 拡張機能を使用するようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="6c924-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="6c924-184">リスト2の変更された global.asax ファイルは、以前のバージョンの IIS で動作します。</span><span class="sxs-lookup"><span data-stu-id="6c924-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="6c924-185">**リスト 2-global.asax (拡張機能を使用して変更)**</span><span class="sxs-lookup"><span data-stu-id="6c924-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

<span data-ttu-id="6c924-186">**重要**: global.asax ファイルを変更した後、ASP.NET MVC アプリケーションを再度ビルドしてください。</span><span class="sxs-lookup"><span data-stu-id="6c924-186">**Important**: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="6c924-187">リスト2の global.asax ファイルには、2つの重要な変更があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="6c924-188">Global.asax に2つのルートが定義されました。</span><span class="sxs-lookup"><span data-stu-id="6c924-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="6c924-189">既定のルートの URL パターン (最初のルート) は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6c924-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="6c924-190">{controller}.mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="6c924-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="6c924-191">Mvc 拡張機能を追加すると、ASP.NET ルーティングモジュールによってインターセプトされるファイルの種類が変更されます。</span><span class="sxs-lookup"><span data-stu-id="6c924-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="6c924-192">この変更により、ASP.NET MVC アプリケーションは次のような要求をルーティングするようになりました。</span><span class="sxs-lookup"><span data-stu-id="6c924-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="6c924-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="6c924-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="6c924-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="6c924-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="6c924-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="6c924-195">/Product.mvc/</span></span>

<span data-ttu-id="6c924-196">ルートルートの2番目のルートは [新規] です。</span><span class="sxs-lookup"><span data-stu-id="6c924-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="6c924-197">ルートルートのこの URL パターンは空の文字列です。</span><span class="sxs-lookup"><span data-stu-id="6c924-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="6c924-198">このルートは、アプリケーションのルートに対して行われた要求を照合するために必要です。</span><span class="sxs-lookup"><span data-stu-id="6c924-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="6c924-199">たとえば、ルートルートは次のような要求と一致します。</span><span class="sxs-lookup"><span data-stu-id="6c924-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="6c924-200">ルートテーブルにこれらの変更を加えた後、アプリケーション内のすべてのリンクがこれらの新しい URL パターンと互換性があることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="6c924-201">つまり、すべてのリンクに、mvc 拡張子が含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c924-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="6c924-202">Html.actionlink () ヘルパーメソッドを使用してリンクを生成する場合は、変更を加える必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6c924-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="6c924-203">Registermvc.wcf スクリプトを使用する代わりに IIS を手動で ASP.NET フレームワークにマップされている新しい拡張機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="6c924-204">新しい拡張機能を自分で追加する場合は、[**ファイルが存在することを確認**する] チェックボックスがオンになっていないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6c924-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="6c924-205">ホステッドサーバー</span><span class="sxs-lookup"><span data-stu-id="6c924-205">Hosted Server</span></span>

<span data-ttu-id="6c924-206">Web サーバーにアクセスすることは常に許可されていません。</span><span class="sxs-lookup"><span data-stu-id="6c924-206">You don't always have access to your web server.</span></span> <span data-ttu-id="6c924-207">たとえば、インターネットホスティングプロバイダーを使用して ASP.NET MVC アプリケーションをホストしている場合、必ずしも IIS にアクセスできるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="6c924-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="6c924-208">その場合は、ASP.NET フレームワークにマップされている既存のファイル拡張子の1つを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="6c924-209">ASP.NET にマップされたファイル拡張子の例としては、.aspx、axd、および .ashx 拡張子があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="6c924-210">たとえば、リスト3の変更された global.asax ファイルは、mvc 拡張機能ではなく .aspx 拡張子を使用します。</span><span class="sxs-lookup"><span data-stu-id="6c924-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="6c924-211">**リスト 3-global.asax (.aspx 拡張子を使用して変更)**</span><span class="sxs-lookup"><span data-stu-id="6c924-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

<span data-ttu-id="6c924-212">リスト3の global.asax ファイルは、以前の global.asax ファイルとまったく同じです。ただし、mvc 拡張機能ではなく .aspx 拡張子を使用する点が異なります。</span><span class="sxs-lookup"><span data-stu-id="6c924-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="6c924-213">.Aspx 拡張子を使用するために、リモート web サーバーでセットアップを実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6c924-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="6c924-214">ワイルドカードスクリプトマップの作成</span><span class="sxs-lookup"><span data-stu-id="6c924-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="6c924-215">ASP.NET MVC アプリケーションの Url を変更する必要がなく、web サーバーにアクセスできる場合は、追加のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="6c924-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="6c924-216">Web サーバーへのすべての要求を ASP.NET フレームワークにマップするワイルドカードスクリプトマップを作成できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="6c924-217">このようにして、既定の ASP.NET MVC ルートテーブルを IIS 7.0 (クラシックモード) または IIS 6.0 と共に使用できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="6c924-218">このオプションを使用すると、web サーバーに対して行われたすべての要求が IIS によってインターセプトされます。</span><span class="sxs-lookup"><span data-stu-id="6c924-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="6c924-219">これには、イメージ、従来の ASP ページ、HTML ページの要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6c924-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="6c924-220">このため、ASP.NET に対してワイルドカードスクリプトマップを有効にすると、パフォーマンスに影響があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="6c924-221">IIS 7.0 に対してワイルドカードスクリプトマップを有効にする方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6c924-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="6c924-222">[接続] ウィンドウでアプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c924-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="6c924-223">[**機能**ビュー] が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6c924-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="6c924-224">**[ハンドラーマッピング]** ボタンをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c924-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="6c924-225">**[ワイルドカードスクリプトマップの追加]** リンクをクリックします (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="6c924-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="6c924-226">Aspnet\_isapi .dll ファイルへのパスを入力します (このパスは Pageハンドラファクトリスクリプトマップからコピーできます)。</span><span class="sxs-lookup"><span data-stu-id="6c924-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="6c924-227">名前を「MVC」と入力します。</span><span class="sxs-lookup"><span data-stu-id="6c924-227">Enter the name MVC</span></span>
7. <span data-ttu-id="6c924-228">**[OK]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c924-228">Click the **OK** button</span></span>

<span data-ttu-id="6c924-229">[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="6c924-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span></span>

<span data-ttu-id="6c924-230">**図 3**: IIS 7.0 を使用したワイルドカードスクリプトマップの作成 ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png)される)</span><span class="sxs-lookup"><span data-stu-id="6c924-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span></span>

<span data-ttu-id="6c924-231">IIS 6.0 でワイルドカードスクリプトマップを作成するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="6c924-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="6c924-232">Web サイトを右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6c924-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="6c924-233">**[ホームディレクトリ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c924-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="6c924-234">**[構成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c924-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="6c924-235">**[マッピング]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="6c924-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="6c924-236">**[挿入]** ボタンをクリックします (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="6c924-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="6c924-237">Aspnet\_のパスを実行可能フィールドに貼り付けます (.aspx ファイルのスクリプトマップからこのパスをコピーできます)。</span><span class="sxs-lookup"><span data-stu-id="6c924-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="6c924-238">[**ファイルが存在することを確認**する] チェックボックスをオフにする</span><span class="sxs-lookup"><span data-stu-id="6c924-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="6c924-239">**[OK]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6c924-239">Click the **OK** button</span></span>

<span data-ttu-id="6c924-240">[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6c924-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span></span>

<span data-ttu-id="6c924-241">**図 4**: IIS 6.0 を使用したワイルドカードスクリプトマップの作成 ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png)される)</span><span class="sxs-lookup"><span data-stu-id="6c924-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span></span>

<span data-ttu-id="6c924-242">ワイルドカードスクリプトマップを有効にした後、グローバルな global.asax ファイル内のルートテーブルを変更してルートルートを含めるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="6c924-243">そうしないと、アプリケーションのルートページに対して要求を行ったときに、図5のエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6c924-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="6c924-244">リスト4で変更した global.asax ファイルを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="6c924-245">[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="6c924-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span></span>

<span data-ttu-id="6c924-246">**図 5**: ルートルートの不足エラー ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png)されます)</span><span class="sxs-lookup"><span data-stu-id="6c924-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span></span>

<span data-ttu-id="6c924-247">**リスト 4-global.asax (ルートルートで変更済み)**</span><span class="sxs-lookup"><span data-stu-id="6c924-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

<span data-ttu-id="6c924-248">IIS 7.0 または IIS 6.0 に対してワイルドカードスクリプトマップを有効にした後、次のような既定のルートテーブルを操作する要求を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="6c924-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="6c924-249">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="6c924-249">/Home/Index</span></span>

<span data-ttu-id="6c924-250">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="6c924-250">/Product/Details/3</span></span>

<span data-ttu-id="6c924-251">/Product</span><span class="sxs-lookup"><span data-stu-id="6c924-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="6c924-252">まとめ</span><span class="sxs-lookup"><span data-stu-id="6c924-252">Summary</span></span>

<span data-ttu-id="6c924-253">このチュートリアルの目的は、古いバージョンの IIS (またはクラシックモードでは IIS 7.0) を使用するときに ASP.NET MVC を使用する方法を説明することでした。</span><span class="sxs-lookup"><span data-stu-id="6c924-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="6c924-254">以前のバージョンの IIS で動作するように ASP.NET ルーティングを取得する2つの方法を説明しました。既定のルートテーブルを変更するか、ワイルドカードスクリプトマップを作成します。</span><span class="sxs-lookup"><span data-stu-id="6c924-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="6c924-255">最初のオプションでは、ASP.NET MVC アプリケーションで使用される Url を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6c924-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="6c924-256">この最初のオプションの非常に大きな利点の1つは、ルートテーブルを変更するために web サーバーにアクセスする必要がないことです。</span><span class="sxs-lookup"><span data-stu-id="6c924-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="6c924-257">つまり、インターネットホスティング会社で ASP.NET MVC アプリケーションをホストしている場合でも、この最初のオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6c924-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="6c924-258">2つ目の方法は、ワイルドカードスクリプトマップを作成することです。</span><span class="sxs-lookup"><span data-stu-id="6c924-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="6c924-259">この2つ目の方法の利点は、Url を変更する必要がないことです。</span><span class="sxs-lookup"><span data-stu-id="6c924-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="6c924-260">この2つ目のオプションの欠点は、ASP.NET MVC アプリケーションのパフォーマンスに影響を与える可能性があることです。</span><span class="sxs-lookup"><span data-stu-id="6c924-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6c924-261">Next</span><span class="sxs-lookup"><span data-stu-id="6c924-261">Next</span></span>](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
