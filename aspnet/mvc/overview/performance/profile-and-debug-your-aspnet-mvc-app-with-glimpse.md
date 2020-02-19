---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: ASP.NET MVC アプリのプロファイルとデバッグMicrosoft Docs
author: Rick-Anderson
description: 活発は、ASP.NET の詳細なパフォーマンス、デバッグ、診断情報を提供するオープンソースの NuGet パッケージのファミリです。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457662"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="078a2-103">Glimpse を使用して ASP.NET MVC アプリをプロファイルおよびデバッグする</span><span class="sxs-lookup"><span data-stu-id="078a2-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="078a2-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="078a2-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="078a2-105">活発は、ASP.NET アプリのパフォーマンス、デバッグ、診断に関する詳細な情報を提供するオープンソースの NuGet パッケージのファミリです。</span><span class="sxs-lookup"><span data-stu-id="078a2-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="078a2-106">すべてのページの下部に、インストール、軽量、超高速の主要なパフォーマンスメトリックが表示されるのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="078a2-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="078a2-107">これにより、サーバーで何が起こっているかを調べる必要がある場合に、アプリにドリルダウンできます。</span><span class="sxs-lookup"><span data-stu-id="078a2-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="078a2-108">この情報は、Azure テスト環境など、開発サイクル全体で使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="078a2-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="078a2-109">[Fiddler](http://www.telerik.com/fiddler)および[F-12 開発ツール](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)にはクライアント側のビューが用意されていますが、サーバーから詳細なビューを提供しています。</span><span class="sxs-lookup"><span data-stu-id="078a2-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="078a2-110">このチュートリアルでは、ASP.NET MVC パッケージと EF パッケージを使用する方法に焦点を当てていますが、他にも多くのパッケージが用意されています。</span><span class="sxs-lookup"><span data-stu-id="078a2-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="078a2-111">可能な限り、管理に役立つ適切な[ドキュメント](http://getglimpse.com/Docs/)にリンクします。</span><span class="sxs-lookup"><span data-stu-id="078a2-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="078a2-112">ここでは、オープンソースプロジェクトです。ソースコードやドキュメントに投稿することもできます。</span><span class="sxs-lookup"><span data-stu-id="078a2-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="078a2-113">インストールの方法</span><span class="sxs-lookup"><span data-stu-id="078a2-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="078a2-114">Localhost のすべてを有効にする</span><span class="sxs-lookup"><span data-stu-id="078a2-114">Enable Glimpse for localhost</span></span>](#eg)
- <span data-ttu-id="078a2-115">[[タイムライン] タブ](#Time)</span><span class="sxs-lookup"><span data-stu-id="078a2-115">[The Timeline tab](#Time)</span></span>
- [<span data-ttu-id="078a2-116">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="078a2-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="078a2-117">ルート</span><span class="sxs-lookup"><span data-stu-id="078a2-117">Routes</span></span>](#route)
- [<span data-ttu-id="078a2-118">Azure での使用</span><span class="sxs-lookup"><span data-stu-id="078a2-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="078a2-119">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="078a2-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="078a2-120">インストールの方法</span><span class="sxs-lookup"><span data-stu-id="078a2-120">Installing Glimpse</span></span>

<span data-ttu-id="078a2-121">NuGet パッケージマネージャーコンソールからインストールするか、 **Nuget パッケージの管理**コンソールからインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="078a2-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="078a2-122">このデモでは、Mvc5 パッケージと EF6 パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="078a2-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![NuGet Dlg からのインストール](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="078a2-124">「 *. EF. EF」を検索します。*</span><span class="sxs-lookup"><span data-stu-id="078a2-124">Search for *Glimpse.EF*</span></span>

![NuGet install dlg からの、EF. EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="078a2-126">**[インストール済みのパッケージ]** を選択すると、インストールされている依存モジュールを確認できます。</span><span class="sxs-lookup"><span data-stu-id="078a2-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![インストールされたパッケージのインストール (DLg)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="078a2-128">次のコマンドは、パッケージマネージャーコンソールから、MVC5 モジュールと EF6 モジュールをインストールします。</span><span class="sxs-lookup"><span data-stu-id="078a2-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="078a2-129">Localhost のすべてを有効にする</span><span class="sxs-lookup"><span data-stu-id="078a2-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="078a2-130">http://localhost:&lt;p ort #&gt;/glimpse.axd に移動し、[を<strong>オン</strong>にする] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="078a2-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![[すべての axd] ページ](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="078a2-132">お気に入りバーが表示されている場合は、そのボタンをドラッグアンドドロップして、bookmarklets として追加することができます。</span><span class="sxs-lookup"><span data-stu-id="078a2-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![Bookmarklets を使用した IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="078a2-134">これでアプリに移動できるようになり、ページの下部に [**ヘッドアップディスプレイ**(HUD)] が表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![HUD がある連絡先マネージャーページ](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="078a2-136">この[ページ](http://getglimpse.com/Docs/Heads-up-Display)には、上に示したタイミング情報の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="078a2-137">HUD に表示される控えめなパフォーマンスデータにより、テストサイクルに到達する前に問題をすぐに通知できます。</span><span class="sxs-lookup"><span data-stu-id="078a2-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="078a2-138">右下隅にある &quot;g&quot; をクリックすると、[表示] パネルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![すべてのパネル](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="078a2-140">上の図では、[[実行] タブ](http://getglimpse.com/Docs/Execution-Tab)が選択されており、パイプライン内のアクションとフィルターのタイミングの詳細が示されています。</span><span class="sxs-lookup"><span data-stu-id="078a2-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="078a2-141">パイプラインのステージ6で、[ストップウォッチフィルタータイマー](http://www.nuget.org/packages/StopWatch/)の開始を確認できます。</span><span class="sxs-lookup"><span data-stu-id="078a2-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="078a2-142">ライトウェイトタイマーは便利なプロファイル/タイミングデータを提供できますが、承認とビューの表示に費やされた時間はすべてミスになります。</span><span class="sxs-lookup"><span data-stu-id="078a2-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="078a2-143">[ASP.NET MVC アプリのプロファイルと時間については、「Azure に対するすべての方法」を](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)参照してください。</span><span class="sxs-lookup"><span data-stu-id="078a2-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="078a2-144">[[タブ](http://getglimpse.com/Docs/Tabs)] ページには、各タブの詳細情報へのリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="078a2-145">[タイムライン] タブ</span><span class="sxs-lookup"><span data-stu-id="078a2-145">The Timeline tab</span></span>

<span data-ttu-id="078a2-146">次のコードを講師コントローラーに変更することで、Tom Dykstra の未解決の[EF 6/MVC 5 チュートリアル](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を変更しました。</span><span class="sxs-lookup"><span data-stu-id="078a2-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="078a2-147">上記のコードでは、クエリ文字列 (`eager`) を渡して、データの一括または明示的な読み込みを制御できます。</span><span class="sxs-lookup"><span data-stu-id="078a2-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="078a2-148">次の図では、明示的な読み込みが使用されており、タイミングページには `Index` アクションメソッドに読み込まれた各登録が示されています。</span><span class="sxs-lookup"><span data-stu-id="078a2-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![明示的な読み込み (explicit loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="078a2-150">次のコードでは、一括実行が指定されており、`Index` ビューが呼び出された後に各登録がフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="078a2-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![集中指定](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="078a2-152">時間セグメントをポイントすると、詳細なタイミング情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="078a2-152">You can hover over a time segment to get detailed timing information:</span></span>

![ホバーして詳細なタイミングを確認する](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="078a2-154">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="078a2-154">Model Binding</span></span>

<span data-ttu-id="078a2-155">[[モデルのバインド] タブ](http://getglimpse.com/Docs/Model-Binding-Tab)には、フォーム変数がどのようにバインドされているか、また、一部が期待どおりにバインドされていない理由を理解するのに役立つ豊富な情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="078a2-156">次の画像が表示され**ます。**</span><span class="sxs-lookup"><span data-stu-id="078a2-156">The image below shows the **?**</span></span> <span data-ttu-id="078a2-157">アイコンをクリックすると、その機能の [表示] ヘルプページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![モデルバインドビューを表示します](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="078a2-159">ルート</span><span class="sxs-lookup"><span data-stu-id="078a2-159">Routes</span></span>

 <span data-ttu-id="078a2-160">[ルートの表示] タブは、ルーティングをデバッグして理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="078a2-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="078a2-161">次の図では、製品ルートが選択されています (緑で示されています)。</span><span class="sxs-lookup"><span data-stu-id="078a2-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="078a2-162">ルートの制約、区分、データトークン](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 選択されている ![製品名も表示されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="078a2-163">詳細については、「 [ASP.NET MVC 5 で](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)の[ルート](http://getglimpse.com/Docs/Routes-Tab)と属性のルーティング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="078a2-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="078a2-164">Azure での使用</span><span class="sxs-lookup"><span data-stu-id="078a2-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="078a2-165">既定のセキュリティポリシーの設定では、ローカルホストからのデータの表示のみが許可されます。</span><span class="sxs-lookup"><span data-stu-id="078a2-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="078a2-166">このセキュリティポリシーを変更して、リモートサーバー (Azure 上の web アプリなど) でこのデータを表示できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="078a2-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="078a2-167">Azure 上のテスト環境の場合は、次のように、web.config ファイルの一番下まで強調表示されているマークを追加して、一目で確認できるよう*にします*。</span><span class="sxs-lookup"><span data-stu-id="078a2-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="078a2-168">この変更だけで、リモートサイトでユーザーが自分のデータを見ることができます。</span><span class="sxs-lookup"><span data-stu-id="078a2-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="078a2-169">上記のマークアップを発行プロファイルに追加することを検討してください。これにより、発行プロファイル (Azure テストプロファイルなど) を使用する場合にのみ適用されるがデプロイされます。データを制限するために、`canViewGlimpseData` ロールを追加し、このロールのユーザーのみが表示データを表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="078a2-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="078a2-170">*GlimpseSecurityPolicy.cs*ファイルからコメントを削除し、`Administrator` から `canViewGlimpseData` ロールに、 [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)呼び出しを変更します。</span><span class="sxs-lookup"><span data-stu-id="078a2-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="078a2-171">セキュリティ-ユーザーによって提供される豊富なデータによって、アプリのセキュリティが公開される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="078a2-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="078a2-172">Microsoft では、生産アプリでの使用については、セキュリティ監査を実行していません。</span><span class="sxs-lookup"><span data-stu-id="078a2-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="078a2-173">ロールの追加の詳細については、「my [Deploy a Secure ASP.NET MVC 5 web app With Membership, OAuth, and SQL Database To Azure」を](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)参照してください。</span><span class="sxs-lookup"><span data-stu-id="078a2-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="078a2-174">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="078a2-174">Additional Resources</span></span>

- [<span data-ttu-id="078a2-175">メンバーシップ、OAuth、SQL Database がある Secure ASP.NET MVC 5 アプリを Azure にデプロイする</span><span class="sxs-lookup"><span data-stu-id="078a2-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="078a2-176">[[設定](http://getglimpse.com/Docs/Configuration)]-タブ、ランタイムポリシー、ログ記録などの構成に関するドキュメントページ。</span><span class="sxs-lookup"><span data-stu-id="078a2-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
