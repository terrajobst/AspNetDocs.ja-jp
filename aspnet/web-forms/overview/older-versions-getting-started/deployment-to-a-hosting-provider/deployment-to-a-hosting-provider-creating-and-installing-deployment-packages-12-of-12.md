---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact での ASP.NET Web アプリケーションのデプロイ: トラブルシューティング (12 インチ) |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639874"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a><span data-ttu-id="0b17b-103">Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: トラブルシューティング (12 インチ)</span><span class="sxs-lookup"><span data-stu-id="0b17b-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Troubleshooting (12 of 12)</span></span>

<span data-ttu-id="0b17b-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0b17b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="0b17b-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="0b17b-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="0b17b-106">この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="0b17b-107">Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="0b17b-108">シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="0b17b-109">Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、および Windows Azure Web サイトへのデプロイ方法については、「 [ASP.NET Web deployment Using Visual studio](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

<span data-ttu-id="0b17b-110">このページでは、Visual Studio を使用して ASP.NET web アプリケーションを配置するときに発生する可能性のある一般的な問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-110">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="0b17b-111">それぞれについて、1つまたは複数の考えられる原因と、対応するソリューションが提供されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-111">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="0b17b-112">'/' アプリケーションのサーバーエラー-現在のカスタムエラー設定により、エラーの詳細をリモートで表示できません</span><span class="sxs-lookup"><span data-stu-id="0b17b-112">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-113">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-113">Scenario</span></span>

<span data-ttu-id="0b17b-114">リモートホストにサイトを展開した後、web.config ファイルの customErrors 設定を示すエラーメッセージが表示されますが、エラーの実際の原因は示されていません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-114">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-115">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-115">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-116">既定では、ASP.NET は、web アプリケーションがローカルコンピューター上で実行されている場合にのみ、詳細なエラー情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-116">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="0b17b-117">一般に、web アプリケーションがインターネット経由で公開されている場合は、詳細なエラー情報を表示しないようにします。ハッカーはこの情報を使用してアプリケーションの脆弱性を検出できるためです。</span><span class="sxs-lookup"><span data-stu-id="0b17b-117">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="0b17b-118">ただし、サイトまたは更新プログラムをサイトに展開するときに問題が発生し、実際のエラーメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-118">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="0b17b-119">リモートホストで実行されているときに、アプリケーションで詳細なエラーメッセージを表示できるようにするには、web.config ファイルを編集して `customErrors` モードをオフにし、アプリケーションを再デプロイして、アプリケーションを再度実行します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-119">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set `customErrors` mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="0b17b-120">アプリケーションの Web.config ファイルの `system.web` 要素に `customErrors` 要素がある場合は、`mode` 属性を "off" に変更します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-120">If the application Web.config file has a `customErrors` element in the `system.web` element, change the `mode` attribute to "off".</span></span> <span data-ttu-id="0b17b-121">それ以外の場合は、次の例に示すように、`mode` 属性を "off" に設定して、`system.web` 要素に `customErrors` 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-121">Otherwise add a `customErrors` element in the `system.web` element with the `mode` attribute set to "off", as shown in the following example:</span></span>

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. <span data-ttu-id="0b17b-122">アプリケーションを展開します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-122">Deploy the application.</span></span>
3. <span data-ttu-id="0b17b-123">アプリケーションを実行し、エラーが発生する原因となったものをすべて繰り返します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-123">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="0b17b-124">これで、実際のエラーメッセージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-124">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="0b17b-125">エラーを解決したら、元の `customErrors` 設定を復元し、アプリケーションを再展開します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-125">When you have resolved the error, restore the original `customErrors` setting and redeploy the application.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="0b17b-126">を使用する Web ページでアクセスが拒否される SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="0b17b-126">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-127">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-127">Scenario</span></span>

<span data-ttu-id="0b17b-128">SQL Server Compact を使用するサイトを展開し、データベースにアクセスする配置済みサイトでページを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-128">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-129">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-129">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-130">サーバー上のネットワークサービスアカウントは、 *bin\amd64*または*bin\x86*フォルダーにある SQL service Compact ネイティブバイナリを読み取ることができる必要がありますが、これらのフォルダーに対する読み取りアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-130">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="0b17b-131">*Bin*フォルダーで NETWORK SERVICE の読み取りアクセス許可を設定し、アクセス許可をサブフォルダーに拡張します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-131">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="0b17b-132">アクセス許可が不足しているため、構成ファイルを読み取れません</span><span class="sxs-lookup"><span data-stu-id="0b17b-132">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-133">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-133">Scenario</span></span>

<span data-ttu-id="0b17b-134">Visual Studio の [発行] ボタンをクリックしてローカルコンピューター上の IIS にアプリケーションを配置すると、発行が失敗し、次のようなエラーメッセージが**出力**ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-134">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-135">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-135">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-136">ローカルコンピューターでワンクリックで IIS に発行するには、管理者権限を使用して Visual Studio を実行している必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-136">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="0b17b-137">Visual Studio を閉じて、管理者権限で再起動します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-137">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="0b17b-138">対象のコンピューターに接続できませんでした...指定されたプロセスの使用</span><span class="sxs-lookup"><span data-stu-id="0b17b-138">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-139">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-139">Scenario</span></span>

<span data-ttu-id="0b17b-140">Visual Studio の [発行] ボタンをクリックしてアプリケーションを配置すると、発行が失敗し、**出力**ウィンドウに次のようなエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-140">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-141">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-141">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-142">プロキシサーバーは、移行先サーバーとの通信を中断しています。</span><span class="sxs-lookup"><span data-stu-id="0b17b-142">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="0b17b-143">Windows のコントロールパネルまたは Internet Explorer で、 **[インターネットオプション]** を選択し、 **[接続]** タブを選択します。 **[インターネットのプロパティ]** ダイアログボックスで、 **[LAN の設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-143">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="0b17b-144">**[ローカルエリアネットワーク (LAN) の設定]** ダイアログボックスで、 **[設定を自動的に検出]** する チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-144">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="0b17b-145">次に、[発行] ボタンをもう一度クリックします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-145">Then click the publish button again.</span></span>

<span data-ttu-id="0b17b-146">問題が解決しない場合は、システム管理者に問い合わせて、プロキシまたはファイアウォールの設定で実行できることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-146">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="0b17b-147">この問題が発生するのは、Web 配置が Web 管理サービスの展開 (8172) で非標準ポートを使用するためです。その他の接続の場合、Web 配置はポート80を使用します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-147">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="0b17b-148">サードパーティのホスティングプロバイダーにデプロイする場合、通常は Web 管理サービスを使用します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-148">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="0b17b-149">既定の .NET 4.0 アプリケーションプールが存在しません</span><span class="sxs-lookup"><span data-stu-id="0b17b-149">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-150">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-150">Scenario</span></span>

<span data-ttu-id="0b17b-151">.NET Framework 4 を必要とするアプリケーションを展開すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-151">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-152">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-152">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-153">ASP.NET 4 は IIS にインストールされていません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-153">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="0b17b-154">配置先のサーバーが開発用コンピューターで、Visual Studio 2010 がインストールされている場合、ASP.NET 4 はコンピューターにインストールされますが、IIS にインストールされていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-154">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="0b17b-155">デプロイ先のサーバーで、次のコマンドを実行して、管理者特権でのコマンドプロンプトを開き、ASP.NET 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-155">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

<span data-ttu-id="0b17b-156">また、既定のアプリケーションプールの .NET Framework バージョンを手動で設定することが必要になる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-156">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="0b17b-157">詳細については、「[テスト環境として IIS に配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)する」チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-157">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="0b17b-158">初期化文字列の形式は、インデックス0から始まる仕様に準拠していません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-158">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-159">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-159">Scenario</span></span>

<span data-ttu-id="0b17b-160">ワンクリック発行を使用してアプリケーションを配置した後、データベースにアクセスするページを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-160">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-161">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-161">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-162">配置したサイトの web.config ファイルを開き、次の例に示すように、接続*文字列の値*が `$(ReplaceableToken_`で始まるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-162">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplaceableToken_`, as in the following example:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

<span data-ttu-id="0b17b-163">接続文字列が次の例のようになっている場合は、プロジェクトファイルを編集し、次のプロパティを、すべてのビルド構成の `PropertyGroup` 要素に追加します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-163">If the connection strings look like this example, edit the project file and add the following property to the `PropertyGroup` element that is for all build configurations:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

<span data-ttu-id="0b17b-164">その後、アプリケーションを再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-164">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="0b17b-165">HTTP 500 内部サーバーエラー</span><span class="sxs-lookup"><span data-stu-id="0b17b-165">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-166">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-166">Scenario</span></span>

<span data-ttu-id="0b17b-167">展開されたサイトを実行すると、次のエラーメッセージが表示され、エラーの原因を示す特定の情報が表示されません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-167">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-168">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-168">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-169">500エラーには多くの原因がありますが、これらのチュートリアルに従うと、xml 変換ファイルの1つに XML 要素を間違った場所に配置することが考えられます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-169">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the XML transformation files.</span></span> <span data-ttu-id="0b17b-170">たとえば、`<configuration>`のすぐ下ではなく `<system.web>` の下に `<location>` 要素を挿入する変換を配置すると、このエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-170">For example, you would get this error if you put the transformation that inserts a `<location>` element under `<system.web>` instead of directly under `<configuration>`.</span></span> <span data-ttu-id="0b17b-171">この場合の解決策は、XML 変換ファイルを修正して再配置することです。</span><span class="sxs-lookup"><span data-stu-id="0b17b-171">The solution in that case is to correct the XML transformation file and redeploy.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="0b17b-172">HTTP 500.21 内部サーバーエラー</span><span class="sxs-lookup"><span data-stu-id="0b17b-172">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-173">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-173">Scenario</span></span>

<span data-ttu-id="0b17b-174">展開されたサイトを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-174">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-175">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-175">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-176">展開したサイトは ASP.NET 4 をターゲットにしていますが、ASP.NET 4 はサーバーの IIS に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-176">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="0b17b-177">サーバーで、管理者特権でのコマンドプロンプトを開き、次のコマンドを実行して ASP.NET 4 を登録します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-177">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

<span data-ttu-id="0b17b-178">また、既定のアプリケーションプールの .NET Framework バージョンを手動で設定することが必要になる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-178">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="0b17b-179">詳細については、「[テスト環境として IIS に配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)する」チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-179">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a><span data-ttu-id="0b17b-180">アプリ\_データ内の SQL Server Express データベースを開くことができませんでした</span><span class="sxs-lookup"><span data-stu-id="0b17b-180">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-181">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-181">Scenario</span></span>

<span data-ttu-id="0b17b-182">*Web.config ファイルの*接続文字列を更新して、 *App\_Data*フォルダー内の *.mdf*ファイルとして SQL Server Express データベースを指すようにしました。アプリケーションを初めて実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-182">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-183">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-183">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-184">*.Mdf*ファイルの名前は、以前に既存のデータベースの *.mdf*ファイルを削除した場合でも、コンピューター上に存在していた SQL Server Express データベースの名前と一致させることはできません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-184">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="0b17b-185">*.Mdf*ファイルの名前を、データベース名として使用されていない名前に変更し、新しい名前を使用するように*web.config ファイルを*変更します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-185">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="0b17b-186">別の方法として、 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)を使用して、以前に存在していた SQL Server Express データベースを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-186">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="0b17b-187">モデルの互換性を確認できません</span><span class="sxs-lookup"><span data-stu-id="0b17b-187">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-188">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-188">Scenario</span></span>

<span data-ttu-id="0b17b-189">新しい SQL Server Express データベースを指すように*web.config ファイルの接続文字列を更新*し、アプリケーションを初めて実行したときに、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-189">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-190">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-190">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-191">Web.config ファイルに指定したデータベース名が、コンピューター上で以前に使用されていた場合は、データベースが既に存在している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-191">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="0b17b-192">前にコンピューターで使用されていない新しい名前を選択し、この新しいデータベース名を使用するように*web.config ファイルを変更します。*</span><span class="sxs-lookup"><span data-stu-id="0b17b-192">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="0b17b-193">別の方法として、 [SQL Server Express ユーティリティ](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)または[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)を使用して、既存のデータベースを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-193">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="0b17b-194">スクリプトがユーザーまたはロールを作成しようとしたときの SQL エラー</span><span class="sxs-lookup"><span data-stu-id="0b17b-194">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-195">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-195">Scenario</span></span>

<span data-ttu-id="0b17b-196">**[Sql のパッケージ化/発行]** タブで構成されたデータベース配置を使用している場合、配置中に実行される SQL スクリプトには create User または create Role コマンドがあり、これらのコマンドが実行されるとスクリプトの実行が失敗します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-196">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="0b17b-197">次のような詳細なメッセージが表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-197">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

<span data-ttu-id="0b17b-198">**[SQL のパッケージ化/発行]** タブではなく、 **Web の発行**ウィザードでデータベースの配置を構成したときにこのエラーが発生した場合は、[[構成と配置](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)] フォーラムでスレッドを作成すると、このトラブルシューティングのページにソリューションが追加されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-198">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-199">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-199">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-200">配置の実行に使用しているユーザーアカウントに、ユーザーまたはロールを作成するためのアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-200">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="0b17b-201">たとえば、ホスティング会社は、`db_datareader`、`db_datawriter`、および `db_ddladmin` ロールを、ユーザーに対して設定されたユーザーアカウントに割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-201">For example, the hosting company might assign the `db_datareader`, `db_datawriter`, and `db_ddladmin` roles to the user account that it sets up for you.</span></span> <span data-ttu-id="0b17b-202">これらは、ほとんどのデータベースオブジェクトを作成するのに十分ですが、ユーザーまたはロールを作成するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-202">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="0b17b-203">このエラーを回避する方法の1つは、データベースの配置からユーザーとロールを除外することです。</span><span class="sxs-lookup"><span data-stu-id="0b17b-203">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="0b17b-204">これを行うには、データベースの自動的に生成されたスクリプトの `PreSource` 要素を編集して、次の属性が含まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-204">You can do this by editing the `PreSource` element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

<span data-ttu-id="0b17b-205">プロジェクトファイルの `PreSource` 要素を編集する方法の詳細については、「[方法: プロジェクトファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-205">For information about how to edit the `PreSource` element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="0b17b-206">開発用データベースのユーザーまたはロールが転送先データベースに存在する必要がある場合は、ホスティングプロバイダーに問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-206">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="0b17b-207">配置時にカスタムスクリプトを実行すると SQL Server タイムアウトエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="0b17b-207">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-208">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-208">Scenario</span></span>

<span data-ttu-id="0b17b-209">配置時に実行するカスタム SQL スクリプトを指定し、Web 配置実行するとタイムアウトになります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-209">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-210">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-210">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-211">トランザクションモードが異なる複数のスクリプトを実行すると、タイムアウトエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-211">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="0b17b-212">既定では、自動的に生成されたスクリプトはトランザクション内で実行されますが、カスタムスクリプトでは実行されません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-212">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="0b17b-213">**[Sql のパッケージ化/発行]** タブで **[既存のデータベースからデータまたはスキーマをプル]** する オプションを選択し、カスタムの sql スクリプトを追加する場合は、すべてのスクリプトで同じトランザクション設定が使用されるように、一部のスクリプトのトランザクション設定を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-213">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="0b17b-214">詳細については、「[方法: Web アプリケーションプロジェクトを使用してデータベースを配置](https://msdn.microsoft.com/library/dd465343.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-214">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="0b17b-215">すべてが同じでもこのエラーが発生するようにトランザクション設定を構成した場合は、スクリプトを個別に実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-215">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="0b17b-216">SQL の **[パッケージ化/発行]** タブの **[データベーススクリプト]** グリッドで、タイムアウトエラーを発生させるスクリプトの **[含める]** チェックボックスをオフにし、プロジェクトを発行します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-216">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="0b17b-217">次に、 **[データベーススクリプト]** グリッドに戻り、そのスクリプトの **[インクルード]** チェックボックスをオンにして、他のスクリプトの **[含める]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-217">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="0b17b-218">その後、プロジェクトを再度発行します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-218">Then publish the project again.</span></span> <span data-ttu-id="0b17b-219">今回は、発行時に、選択したカスタムスクリプトのみが実行されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-219">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="0b17b-220">サイトマニフェストのストリームデータはまだ使用できません</span><span class="sxs-lookup"><span data-stu-id="0b17b-220">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-221">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-221">Scenario</span></span>

<span data-ttu-id="0b17b-222">`t` (テスト) オプションを指定して *.deploy*ファイルを使用してパッケージをインストールすると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-222">When you are installing a package using the *deploy.cmd* file with the `t` (test) option, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-223">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-223">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-224">エラーメッセージは、コマンドがテストレポートを生成できないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-224">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="0b17b-225">ただし、`y` (実際のインストール) オプションを使用すると、コマンドが実行される場合があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-225">However, the command might run if you use the `y` (actual installation) option.</span></span> <span data-ttu-id="0b17b-226">このメッセージは、テストモードでのコマンドの実行に問題があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="0b17b-226">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="0b17b-227">このアプリケーションには ManagedRuntimeVersion v4.0 が必要です</span><span class="sxs-lookup"><span data-stu-id="0b17b-227">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-228">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-228">Scenario</span></span>

<span data-ttu-id="0b17b-229">を展開しようとすると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-229">When you attempt to deploy, you see the following error message:</span></span>

 <span data-ttu-id="0b17b-230">エラー: ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlscript ' のストリームデータはまだ使用できません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-230">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span> <span data-ttu-id="0b17b-231">使用しようとしているアプリケーションプールの ' managedRuntimeVersion ' プロパティが ' v2.0 ' に設定されています。</span><span class="sxs-lookup"><span data-stu-id="0b17b-231">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="0b17b-232">このアプリケーションには ' v4.0 ' が必要です。</span><span class="sxs-lookup"><span data-stu-id="0b17b-232">This application requires 'v4.0'.</span></span> 

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-233">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-233">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-234">ASP.NET 4 は IIS にインストールされていません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-234">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="0b17b-235">配置先のサーバーが開発用コンピューターで、Visual Studio 2010 がインストールされている場合、ASP.NET 4 はコンピューターにインストールされますが、IIS にインストールされていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-235">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="0b17b-236">デプロイ先のサーバーで、次のコマンドを実行して、管理者特権でのコマンドプロンプトを開き、ASP.NET 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-236">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="0b17b-237">Microsoft. Deployment. DeploymentProviderOptions をキャストできません</span><span class="sxs-lookup"><span data-stu-id="0b17b-237">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-238">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-238">Scenario</span></span>

<span data-ttu-id="0b17b-239">パッケージを展開すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-239">When you are deploying a package, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-240">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-240">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-241">Web 配置 1.1 UI を使用して、Web 配置2.0 がインストールされているサーバーに IIS マネージャーから展開しようとしています。</span><span class="sxs-lookup"><span data-stu-id="0b17b-241">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="0b17b-242">IIS リモート管理ツールを使用してパッケージをインポートして展開する場合は、接続を確立するときに **[利用可能な新機能]** ダイアログボックスを確認します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-242">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="0b17b-243">(このダイアログボックスは、接続が最初に確立されたときに1回だけ表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-243">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="0b17b-244">接続をクリアして最初からやり直すには、IIS マネージャーを終了し、コマンドプロンプトで `inetmgr /reset` を入力して再度起動します)。一覧に表示されている機能の1つが**WEB 配置 UI**で、バージョン番号が8よりも低い場合、展開先のサーバーに1.1 と2.0 の両方のバージョンの Web 配置がインストールされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-244">To clear the connection and start over, close IIS Manager and start it up again by entering `inetmgr /reset` at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="0b17b-245">2\.0 がインストールされているクライアントから展開するには、サーバーに Web 配置2.0 のみがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-245">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="0b17b-246">この問題を解決するには、ホスティングプロバイダーに連絡する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-246">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="0b17b-247">SQL Server Compact のネイティブコンポーネントを読み込むことができません</span><span class="sxs-lookup"><span data-stu-id="0b17b-247">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-248">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-248">Scenario</span></span>

<span data-ttu-id="0b17b-249">展開されたサイトを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-249">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-250">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-250">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-251">配置されたサイトには、ネイティブアセンブリをアプリケーションの*bin*フォルダーの下に持つ*amd64*および*x86*サブフォルダーがありません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-251">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="0b17b-252">SQL Server Compact がインストールされているコンピューターでは、ネイティブアセンブリは*C:\Program are SQL Server Compact Edition\v4.0\Private*に配置されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-252">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="0b17b-253">Visual Studio プロジェクトの正しいフォルダーに正しいファイルを取り込むには、NuGet SqlServerCompact パッケージをインストールするのが最善の方法です。</span><span class="sxs-lookup"><span data-stu-id="0b17b-253">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="0b17b-254">パッケージのインストールでは、ネイティブアセンブリを*amd64*および*x86*にコピーするビルド後スクリプトが追加されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-254">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="0b17b-255">ただし、これらを展開するためには、プロジェクトに手動で含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-255">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="0b17b-256">詳細については、 [SQL Server Compact のデプロイ](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)に関するチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-256">For more information, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="0b17b-257">Entity Framework Code First アプリケーションを展開した後の "パスが有効ではありません" エラーが発生する</span><span class="sxs-lookup"><span data-stu-id="0b17b-257">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-258">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-258">Scenario</span></span>

<span data-ttu-id="0b17b-259">Entity Framework Code First Migrations を使用するアプリケーションと DBMS (SQL Server Compact など) をデプロイして、そのデータベースをアプリの\_データフォルダー内のファイルに格納します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-259">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="0b17b-260">最初の配置後にデータベースを作成するように構成された Code First Migrations。</span><span class="sxs-lookup"><span data-stu-id="0b17b-260">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="0b17b-261">アプリケーションを実行すると、次の例のようなエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-261">When you run the application you get an error message like the following example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-262">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-262">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-263">データベースを作成しようとしていますが、アプリ\_データフォルダーが存在しません Code First。</span><span class="sxs-lookup"><span data-stu-id="0b17b-263">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="0b17b-264">をデプロイしたときに*app\_data*フォルダーにファイルがないか、**プロジェクトのプロパティ**ウィンドウの **[パッケージ/発行 Web]** タブで [**アプリ\_データを除外**する] を選択しました。</span><span class="sxs-lookup"><span data-stu-id="0b17b-264">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the **Project Properties** window.</span></span> <span data-ttu-id="0b17b-265">サーバーにコピーするファイルがフォルダーに存在しない場合、配置プロセスではサーバーにフォルダーが作成されません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-265">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="0b17b-266">サイトにデータベースが既にセットアップされている場合は、[発行プロファイル] で [**宛先にある追加のファイルを削除**する] を選択した場合、配置プロセスによってファイルと*アプリ\_データ*フォルダー自体が削除されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-266">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="0b17b-267">この問題を解決するには、*アプリの\_データ*フォルダーに .txt ファイルなどのプレースホルダーファイルを配置し、[**アプリ\_データを除外**する] を選択して再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-267">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span> 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="0b17b-268">"基になる RCW から分離された COM オブジェクトは使用できません。"</span><span class="sxs-lookup"><span data-stu-id="0b17b-268">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-269">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-269">Scenario</span></span>

<span data-ttu-id="0b17b-270">これで、ワンクリック発行を使用してアプリケーションをデプロイした後、次のエラーが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0b17b-270">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-271">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-271">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-272">通常、このエラーを解決するには、Visual Studio の終了と再起動が必要です。</span><span class="sxs-lookup"><span data-stu-id="0b17b-272">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="0b17b-273">発行に使用されるユーザーの資格情報に setACL 機関がないため、展開が失敗する</span><span class="sxs-lookup"><span data-stu-id="0b17b-273">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-274">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-274">Scenario</span></span>

<span data-ttu-id="0b17b-275">フォルダーのアクセス許可を設定する権限がないことを示すエラーが表示され、発行が失敗します (使用しているユーザーアカウントには setACL 機関がありません)。</span><span class="sxs-lookup"><span data-stu-id="0b17b-275">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-276">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-276">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-277">既定では、Visual Studio はサイトのルートフォルダーに対する読み取りアクセス許可を設定し、App\_Data フォルダーに対する書き込みアクセス許可を設定します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-277">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="0b17b-278">サイトフォルダーの既定のアクセス許可が正しいことがわかっていて、設定する必要がない場合は、この動作を無効にします。そのためには、発行プロファイルファイル (単一のプロファイルに影響を与える場合) または (すべてのプロファイルに影響を与える場合は) .targets ファイルに **&lt;includesetaclprovideron ondestination&lt;&gt;** を追加します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-278">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="0b17b-279">これらのファイルを編集する方法の詳細については、「[方法: プロファイル (pubxml) ファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-279">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="0b17b-280">アプリケーションがアプリケーションフォルダーに書き込もうとしたときにアクセス拒否エラーが発生する</span><span class="sxs-lookup"><span data-stu-id="0b17b-280">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-281">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-281">Scenario</span></span>

<span data-ttu-id="0b17b-282">アプリケーションフォルダーのいずれかでファイルを作成または編集しようとすると、アプリケーションエラーが発生します。これは、そのフォルダーに対する書き込み権限がないためです。</span><span class="sxs-lookup"><span data-stu-id="0b17b-282">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-283">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-283">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-284">既定では、Visual Studio はサイトのルートフォルダーに対する読み取りアクセス許可を設定し、App\_Data フォルダーに対する書き込みアクセス許可を設定します。</span><span class="sxs-lookup"><span data-stu-id="0b17b-284">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="0b17b-285">アプリケーションにサブフォルダーへの書き込みアクセス権が必要な場合は、[フォルダーのアクセス許可の設定](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)と[運用環境への配置に](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)関するチュートリアルに従って、そのフォルダーのアクセス許可を設定できます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-285">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the [Setting Folder Permissions](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) and [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorials.</span></span> <span data-ttu-id="0b17b-286">アプリケーションにサイトのルートフォルダーへの書き込みアクセス権が必要な場合は、ルートフォルダーに対する読み取り専用アクセスを設定できないようにする必要があります。これを行うには、発行プロファイルファイル (単一のプロファイルに影響を与える場合) または (すべてのプロファイルに影響を与える場合) .targets ファイルに **&lt;includesetaclprovideron&lt;&gt;on**を追加します</span><span class="sxs-lookup"><span data-stu-id="0b17b-286">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="0b17b-287">これらのファイルを編集する方法の詳細については、「[方法: プロファイル (pubxml) ファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-287">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="0b17b-288">構成エラー-targetFramework 属性が、インストールされているバージョンより後のバージョンを参照してい .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0b17b-288">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="0b17b-289">通信の種類</span><span class="sxs-lookup"><span data-stu-id="0b17b-289">Scenario</span></span>

<span data-ttu-id="0b17b-290">ASP.NET 4.5 を対象とする web プロジェクトが正常に発行されましたが、アプリケーションを実行すると (web.config ファイルで `customErrors` モードが "off" に設定されている場合)、次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-290">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the `customErrors` mode set to "off" in the Web.config file) you get the following error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

<span data-ttu-id="0b17b-291">エラーページの [ソースエラー] ボックスには、web.config の次の行がエラーの原因として強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-291">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="0b17b-292">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="0b17b-292">Possible Cause and Solution</span></span>

<span data-ttu-id="0b17b-293">サーバーは ASP.NET 4.5 をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-293">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="0b17b-294">ASP.NET 4.5 のサポートを追加できるかどうかを判断するには、ホスティングプロバイダーに問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-294">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="0b17b-295">サーバーのアップグレードがオプションではない場合は、代わりに ASP.NET 4 以前を対象とする web プロジェクトをデプロイする必要があります。ASP.NET 4 以前の web プロジェクトを同じ宛先に配置する場合は、 **web の発行**ウィザードの **[設定]** タブにある **[変換先で追加のファイルを削除]** する チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="0b17b-295">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="0b17b-296">[**転送先で追加のファイルを削除**する] を選択しないと、構成エラーページが引き続き表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b17b-296">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="0b17b-297">[プロジェクトの**プロパティ**] ウィンドウには [ターゲットフレームワーク] ドロップダウンリストが含まれていますが、 **.NET Framework 4.5**から **.NET Framework 4**に変更するだけでこの問題を解決することはできません。</span><span class="sxs-lookup"><span data-stu-id="0b17b-297">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="0b17b-298">ターゲットフレームワークを以前のバージョンの framework に変更すると、プロジェクトはその後のフレームワークバージョンのアセンブリへの参照を保持し、実行されなくなります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-298">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="0b17b-299">これらの参照を手動で変更するか、.NET Framework 4 以前を対象とする新しいプロジェクトを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b17b-299">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="0b17b-300">詳細については、「 [Web サイトのターゲット設定 .NET Framework](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b17b-300">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0b17b-301">前へ</span><span class="sxs-lookup"><span data-stu-id="0b17b-301">Previous</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
