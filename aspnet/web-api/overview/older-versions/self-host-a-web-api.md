---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自己ホスト ASP.NET Web API 1 (C#)-ASP.NET 4.x
author: MikeWasson
description: コードを使用したチュートリアルでは、コンソールアプリケーション内で web API をホストする方法を示します。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421372"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="4b773-103">自己ホスト ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="4b773-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="4b773-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4b773-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="4b773-105">このチュートリアルでは、コンソールアプリケーション内で web API をホストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4b773-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="4b773-106">ASP.NET Web API には IIS は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="4b773-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="4b773-107">独自のホストプロセスで web API を自己ホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="4b773-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="4b773-108">**新しいアプリケーションでは、OWIN を使用して Web API をセルフホストする必要があります。**</span><span class="sxs-lookup"><span data-stu-id="4b773-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="4b773-109">「 [USE OWIN To Self Host ASP.NET Web API 2」を](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="4b773-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4b773-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="4b773-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4b773-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="4b773-111">Web API 1</span></span>
> - <span data-ttu-id="4b773-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4b773-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="4b773-113">コンソールアプリケーションプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="4b773-113">Create the Console Application Project</span></span>

<span data-ttu-id="4b773-114">Visual Studio を起動し、**スタート**ページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="4b773-115">または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="4b773-116">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="4b773-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="4b773-117">**[ビジュアルC# ]** で、 **[Windows]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="4b773-118">プロジェクトテンプレートの一覧で、 **[コンソールアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="4b773-119">プロジェクトに SelfHost Host &quot;という名前を指定し、[ **OK]** をクリックします。&quot;</span><span class="sxs-lookup"><span data-stu-id="4b773-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="4b773-120">ターゲットフレームワークを設定する (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="4b773-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="4b773-121">Visual Studio 2010 を使用している場合は、ターゲットフレームワークを .NET Framework 4.0 に変更します。</span><span class="sxs-lookup"><span data-stu-id="4b773-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="4b773-122">(既定では、プロジェクトテンプレートは[.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)を対象としています)。</span><span class="sxs-lookup"><span data-stu-id="4b773-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="4b773-123">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="4b773-124">**ターゲットフレームワーク** ドロップダウンリストで、ターゲットフレームワーク を .NET Framework 4.0 に変更します。</span><span class="sxs-lookup"><span data-stu-id="4b773-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="4b773-125">変更を適用するように求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="4b773-126">NuGet パッケージマネージャーのインストール</span><span class="sxs-lookup"><span data-stu-id="4b773-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="4b773-127">NuGet パッケージマネージャーは、non-ASP.NET プロジェクトに Web API アセンブリを追加する最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="4b773-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="4b773-128">NuGet パッケージマネージャーがインストールされているかどうかを確認するには、Visual Studio の **[ツール]** メニューをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="4b773-129">**Nuget パッケージマネージャー**というメニュー項目が表示された場合は、Nuget パッケージマネージャーがあります。</span><span class="sxs-lookup"><span data-stu-id="4b773-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="4b773-130">NuGet パッケージマネージャーをインストールするには:</span><span class="sxs-lookup"><span data-stu-id="4b773-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="4b773-131">Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="4b773-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="4b773-132">**[ツール]** メニューの **[拡張機能と更新プログラム]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="4b773-133">**[拡張機能と更新プログラム]** ダイアログで、 **[オンライン]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="4b773-134">"NuGet パッケージマネージャー" が表示されない場合は、検索ボックスに「nuget package manager」と入力します。</span><span class="sxs-lookup"><span data-stu-id="4b773-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="4b773-135">NuGet パッケージマネージャーを選択し、 **[ダウンロード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="4b773-136">ダウンロードが完了すると、をインストールするように求められます。</span><span class="sxs-lookup"><span data-stu-id="4b773-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="4b773-137">インストールが完了すると、Visual Studio を再起動するように求められる場合があります。</span><span class="sxs-lookup"><span data-stu-id="4b773-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="4b773-138">Web API NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="4b773-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="4b773-139">NuGet パッケージマネージャーがインストールされたら、Web API の自己ホストパッケージをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="4b773-140">**[ツール]** メニューの **[NuGet パッケージマネージャー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="4b773-141">*注*: このメニュー項目が表示されない場合は、NuGet パッケージマネージャーが正しくインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="4b773-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="4b773-142">**[ソリューションの NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="4b773-143">**[NugGet パッケージの管理]** ダイアログボックスで、 **[オンライン]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="4b773-144">検索ボックスに、「&quot;WebApi&quot;」と入力します。</span><span class="sxs-lookup"><span data-stu-id="4b773-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="4b773-145">ASP.NET Web API セルフホストパッケージを選択し、 **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="4b773-146">パッケージがインストールされたら、 **[閉じる]** をクリックしてダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="4b773-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="4b773-147">AspNetWebApi ではなく、WebApi という名前のパッケージを必ずインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="4b773-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="4b773-148">モデルとコントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="4b773-148">Create the Model and Controller</span></span>

<span data-ttu-id="4b773-149">このチュートリアルでは、[はじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)チュートリアルと同じモデルとコントローラークラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="4b773-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="4b773-150">`Product`という名前のパブリッククラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="4b773-151">`ProductsController`という名前のパブリッククラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="4b773-152">このクラスを**ApiController**から派生させます。</span><span class="sxs-lookup"><span data-stu-id="4b773-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="4b773-153">このコントローラーのコードの詳細については、[はじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4b773-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="4b773-154">このコントローラーは、次の3つの GET アクションを定義します。</span><span class="sxs-lookup"><span data-stu-id="4b773-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="4b773-155">URI</span><span class="sxs-lookup"><span data-stu-id="4b773-155">URI</span></span> | <span data-ttu-id="4b773-156">Description</span><span class="sxs-lookup"><span data-stu-id="4b773-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b773-157">/api/products</span><span class="sxs-lookup"><span data-stu-id="4b773-157">/api/products</span></span> | <span data-ttu-id="4b773-158">すべての製品の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="4b773-158">Get a list of all products.</span></span> |
| <span data-ttu-id="4b773-159">/api/*id*</span><span class="sxs-lookup"><span data-stu-id="4b773-159">/api/products/*id*</span></span> | <span data-ttu-id="4b773-160">ID で製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="4b773-160">Get a product by ID.</span></span> |
| <span data-ttu-id="4b773-161">//カテゴリ =*カテゴリ*</span><span class="sxs-lookup"><span data-stu-id="4b773-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="4b773-162">カテゴリ別に製品の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="4b773-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="4b773-163">Web API をホストする</span><span class="sxs-lookup"><span data-stu-id="4b773-163">Host the Web API</span></span>

<span data-ttu-id="4b773-164">Program.cs ファイルを開き、次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="4b773-165">**Program**クラスに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="4b773-166">OptionalHTTP URL 名前空間の予約を追加する</span><span class="sxs-lookup"><span data-stu-id="4b773-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="4b773-167">このアプリケーションは `http://localhost:8080/`をリッスンします。</span><span class="sxs-lookup"><span data-stu-id="4b773-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="4b773-168">既定では、特定の HTTP アドレスでリッスンするには、管理者特権が必要です。</span><span class="sxs-lookup"><span data-stu-id="4b773-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="4b773-169">このチュートリアルを実行すると、次のエラーが表示されることがあります。 "HTTP は URL http://+:8080/を登録できませんでした。このエラーを回避する方法は2つあります。</span><span class="sxs-lookup"><span data-stu-id="4b773-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="4b773-170">管理者特権で Visual Studio を実行します。または、</span><span class="sxs-lookup"><span data-stu-id="4b773-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="4b773-171">Netsh.exe を使用して、アカウントに URL を予約するアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="4b773-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="4b773-172">Netsh.exe を使用するには、管理者特権でコマンドプロンプトを開き、次のコマンドを入力します。コマンド:</span><span class="sxs-lookup"><span data-stu-id="4b773-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="4b773-173">ここで、 *machine\username など*はユーザーアカウントです。</span><span class="sxs-lookup"><span data-stu-id="4b773-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="4b773-174">自己ホストを完了したら、予約を削除してください。</span><span class="sxs-lookup"><span data-stu-id="4b773-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="4b773-175">クライアントアプリケーションから Web API を呼び出す (C#)</span><span class="sxs-lookup"><span data-stu-id="4b773-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="4b773-176">ここでは、web API を呼び出す簡単なコンソールアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="4b773-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="4b773-177">新しいコンソールアプリケーションプロジェクトをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="4b773-178">ソリューションエクスプローラーで、ソリューションを右クリックし、 **[新しいプロジェクトの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="4b773-179">&quot;ClientApp&quot;という名前の新しいコンソールアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="4b773-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="4b773-180">NuGet パッケージマネージャーを使用して ASP.NET Web API コアライブラリパッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="4b773-181">ツール メニューの  **NuGet パッケージマネージャー** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="4b773-182">**[ソリューションの NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="4b773-183">**[NuGet パッケージの管理]** ダイアログで、 **[オンライン]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="4b773-184">検索ボックスに、「&quot;WebApi&quot;」と入力します。</span><span class="sxs-lookup"><span data-stu-id="4b773-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="4b773-185">Microsoft ASP.NET Web API クライアントライブラリパッケージを選択し、 **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="4b773-186">ClientApp に参照を SelfHost プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="4b773-187">ソリューションエクスプローラーで、ClientApp プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="4b773-188">**[参照の追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="4b773-189">**[参照マネージャー]** ダイアログボックスの **[ソリューション]** で、 **[プロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="4b773-190">SelfHost プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="4b773-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="4b773-191">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4b773-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="4b773-192">クライアント/プログラム .cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="4b773-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="4b773-193">次の **using** ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="4b773-194">静的**Httpclient**インスタンスを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="4b773-195">すべての製品を一覧表示し、ID で製品を一覧表示し、カテゴリ別に製品を一覧表示するには、次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="4b773-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="4b773-196">これらの各メソッドは、同じパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="4b773-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="4b773-197">GET 要求を適切な URI に送信するには、 **Httpclient**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4b773-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="4b773-198">**HttpResponseMessage EnsureSuccessStatusCode**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4b773-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="4b773-199">このメソッドは、HTTP 応答の状態がエラーコードの場合に例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="4b773-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="4b773-200">**Readasasync&lt;t&gt;** を呼び出して、HTTP 応答から CLR 型を逆シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="4b773-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="4b773-201">このメソッドは、**システムの .net. HttpContentExtensions**で定義されている拡張メソッドです。</span><span class="sxs-lookup"><span data-stu-id="4b773-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="4b773-202">**GetAsync**メソッドと**readasasync**メソッドは両方とも非同期です。</span><span class="sxs-lookup"><span data-stu-id="4b773-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="4b773-203">これらは、非同期操作を表す**タスク**オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="4b773-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="4b773-204">**Result**プロパティを取得すると、操作が完了するまでスレッドがブロックされます。</span><span class="sxs-lookup"><span data-stu-id="4b773-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="4b773-205">非ブロッキング呼び出しを行う方法など、HttpClient の使用方法の詳細については、「 [.Net クライアントからの WEB API の呼び出し](../advanced/calling-a-web-api-from-a-net-client.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4b773-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="4b773-206">これらのメソッドを呼び出す前に、HttpClient インスタンスの BaseAddress プロパティを "`http://localhost:8080`" に設定します。</span><span class="sxs-lookup"><span data-stu-id="4b773-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="4b773-207">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="4b773-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="4b773-208">これにより、次のように出力されます。</span><span class="sxs-lookup"><span data-stu-id="4b773-208">This should output the following.</span></span> <span data-ttu-id="4b773-209">(最初に SelfHost アプリケーションを実行してください)。</span><span class="sxs-lookup"><span data-stu-id="4b773-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
