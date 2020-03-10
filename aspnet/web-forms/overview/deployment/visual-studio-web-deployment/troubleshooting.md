---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 'Visual Studio を使用した ASP.NET Web 配置: トラブルシューティング |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: b42476fca18b04f4557a216ee205cfd9220023e8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465094"
---
# <a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a><span data-ttu-id="20e86-103">Visual Studio を使用した ASP.NET Web 配置: トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="20e86-103">ASP.NET Web Deployment using Visual Studio: Troubleshooting</span></span>

<span data-ttu-id="20e86-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="20e86-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="20e86-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="20e86-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="20e86-106">このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20e86-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="20e86-107">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="20e86-108">このページでは、Visual Studio を使用して ASP.NET web アプリケーションを配置するときに発生する可能性のある一般的な問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="20e86-108">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="20e86-109">それぞれについて、1つまたは複数の考えられる原因と、対応するソリューションが提供されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-109">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

<span data-ttu-id="20e86-110">ここで紹介するシナリオは、Azure とサードパーティのホスティングプロバイダーの両方に適用されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-110">The scenarios shown apply to both Azure and third-party hosting providers.</span></span> <span data-ttu-id="20e86-111">Azure App Service の Web アプリのトラブルシューティングの詳細については、以下のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-111">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

- [<span data-ttu-id="20e86-112">Visual Studio を使用した Azure App Service での Web アプリのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="20e86-112">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [<span data-ttu-id="20e86-113">Azure App Service の Web Apps の監視</span><span class="sxs-lookup"><span data-stu-id="20e86-113">Monitor Web Apps in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- <span data-ttu-id="20e86-114">[Windows AZURE SDK 2.0 for .net のリリースの発表](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net)(ScottGu のブログ、Visual Studio で診断ログを取得する方法について説明します)</span><span class="sxs-lookup"><span data-stu-id="20e86-114">[Announcing the release of Windows Azure SDK 2.0 for .NET](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu's blog, shows how to get diagnostic logs in Visual Studio)</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="20e86-115">'/' アプリケーションのサーバーエラー-現在のカスタムエラー設定により、エラーの詳細をリモートで表示できません</span><span class="sxs-lookup"><span data-stu-id="20e86-115">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-116">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-116">Scenario</span></span>

<span data-ttu-id="20e86-117">リモートホストにサイトを展開した後、web.config ファイルの customErrors 設定を示すエラーメッセージが表示されますが、エラーの実際の原因は示されていません。</span><span class="sxs-lookup"><span data-stu-id="20e86-117">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-118">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-118">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-119">既定では、ASP.NET は、web アプリケーションがローカルコンピューター上で実行されている場合にのみ、詳細なエラー情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="20e86-119">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="20e86-120">一般に、web アプリケーションがインターネット経由で公開されている場合は、詳細なエラー情報を表示しないようにします。ハッカーはこの情報を使用してアプリケーションの脆弱性を検出できるためです。</span><span class="sxs-lookup"><span data-stu-id="20e86-120">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="20e86-121">ただし、サイトまたは更新プログラムをサイトに展開するときに問題が発生し、実際のエラーメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="20e86-121">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="20e86-122">リモートホストで実行されているときに、アプリケーションで詳細なエラーメッセージを表示できるようにするには、web.config ファイルを編集して customErrors モードをオフにし、アプリケーションを再デプロイして、アプリケーションを再度実行します。</span><span class="sxs-lookup"><span data-stu-id="20e86-122">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set customErrors mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="20e86-123">アプリケーションの Web.config ファイルに customErrors 要素の要素が含まれている場合は、mode 属性を "off" に変更します。</span><span class="sxs-lookup"><span data-stu-id="20e86-123">If the application Web.config file has a customErrors element in the system.web element, change the mode attribute to "off".</span></span> <span data-ttu-id="20e86-124">それ以外の場合は、次の例に示すように、mode 属性を "off" に設定して、system.web 要素に customErrors 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="20e86-124">Otherwise add a customErrors element in the system.web element with the mode attribute set to "off", as shown in the following example:</span></span> 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. <span data-ttu-id="20e86-125">アプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="20e86-125">Deploy the application.</span></span>
3. <span data-ttu-id="20e86-126">アプリケーションを実行し、エラーが発生する原因となったものをすべて繰り返します。</span><span class="sxs-lookup"><span data-stu-id="20e86-126">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="20e86-127">これで、実際のエラーメッセージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="20e86-127">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="20e86-128">エラーを解決したら、元の customErrors 設定を復元し、アプリケーションを再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="20e86-128">When you have resolved the error, restore the original customErrors setting and redeploy the application.</span></span>

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a><span data-ttu-id="20e86-129">このファイルが既に存在する場合は、' ContosoUniversity ' を作成/シャドウコピーできません。</span><span class="sxs-lookup"><span data-stu-id="20e86-129">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-130">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-130">Scenario</span></span>

<span data-ttu-id="20e86-131">Visual Studio でプロジェクトを実行しようとすると、次の例のようなエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-131">When you try to run a project in Visual Studio you get an error page with a message like the following example:</span></span>

<span data-ttu-id="20e86-132">Server Error in '/' Application.</span><span class="sxs-lookup"><span data-stu-id="20e86-132">Server Error in '/' Application.</span></span> <span data-ttu-id="20e86-133">このファイルが既に存在する場合は、' ContosoUniversity ' を作成/シャドウコピーできません。</span><span class="sxs-lookup"><span data-stu-id="20e86-133">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-134">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-134">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-135">しばらく待ってからブラウザーを更新するか、サイトを再コンパイルしてからもう一度実行してみてください。</span><span class="sxs-lookup"><span data-stu-id="20e86-135">Wait a minute and refresh the browser, or recompile the site and try running it again.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="20e86-136">を使用する Web ページでアクセスが拒否される SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="20e86-136">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-137">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-137">Scenario</span></span>

<span data-ttu-id="20e86-138">SQL Server Compact を使用するサイトを展開し、データベースにアクセスする配置済みサイトでページを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-138">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

<span data-ttu-id="20e86-139">アクセスが拒否されました。</span><span class="sxs-lookup"><span data-stu-id="20e86-139">Access is denied.</span></span> <span data-ttu-id="20e86-140">(HRESULT からの例外: 0x80070005 (E\_ACCESSDENIED))</span><span class="sxs-lookup"><span data-stu-id="20e86-140">(Exception from HRESULT: 0x80070005 (E\_ACCESSDENIED))</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-141">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-141">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-142">サーバー上のネットワークサービスアカウントは、 *bin\amd64*または*bin\x86*フォルダーにある SQL service Compact ネイティブバイナリを読み取ることができる必要がありますが、これらのフォルダーに対する読み取りアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="20e86-142">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="20e86-143">*Bin*フォルダーで NETWORK SERVICE の読み取りアクセス許可を設定し、アクセス許可をサブフォルダーに拡張します。</span><span class="sxs-lookup"><span data-stu-id="20e86-143">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="20e86-144">アクセス許可が不足しているため、構成ファイルを読み取れません</span><span class="sxs-lookup"><span data-stu-id="20e86-144">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-145">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-145">Scenario</span></span>

<span data-ttu-id="20e86-146">Visual Studio の [発行] ボタンをクリックしてローカルコンピューター上の IIS にアプリケーションを配置すると、発行が失敗し、次のようなエラーメッセージが**出力**ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-146">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

<span data-ttu-id="20e86-147">IIS 構成ファイル ' MACHINE/リダイレクション ' の読み取り中にエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="20e86-147">An error occurred when reading the IIS Configuration File 'MACHINE/REDIRECTION'.</span></span> <span data-ttu-id="20e86-148">この操作を実行している id は...エラー: アクセス許可が不十分であるため、構成ファイルを読み取ることができません。</span><span class="sxs-lookup"><span data-stu-id="20e86-148">The identity performing this operation was ... Error: Cannot read configuration file due to insufficient permissions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-149">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-149">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-150">ローカルコンピューターでワンクリックで IIS に発行するには、管理者権限を使用して Visual Studio を実行している必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-150">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="20e86-151">Visual Studio を閉じて、管理者権限で再起動します。</span><span class="sxs-lookup"><span data-stu-id="20e86-151">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="20e86-152">対象のコンピューターに接続できませんでした...指定されたプロセスの使用</span><span class="sxs-lookup"><span data-stu-id="20e86-152">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-153">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-153">Scenario</span></span>

<span data-ttu-id="20e86-154">Visual Studio の [発行] ボタンをクリックしてアプリケーションを配置すると、発行が失敗し、**出力**ウィンドウに次のようなエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-154">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-155">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-155">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-156">プロキシサーバーは、移行先サーバーとの通信を中断しています。</span><span class="sxs-lookup"><span data-stu-id="20e86-156">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="20e86-157">Windows のコントロールパネルまたは Internet Explorer で、 **[インターネットオプション]** を選択し、 **[接続]** タブを選択します。 **[インターネットのプロパティ]** ダイアログボックスで、 **[LAN の設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20e86-157">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="20e86-158">**[ローカルエリアネットワーク (LAN) の設定]** ダイアログボックスで、 **[設定を自動的に検出]** する チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="20e86-158">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="20e86-159">次に、[発行] ボタンをもう一度クリックします。</span><span class="sxs-lookup"><span data-stu-id="20e86-159">Then click the publish button again.</span></span>

<span data-ttu-id="20e86-160">問題が解決しない場合は、システム管理者に問い合わせて、プロキシまたはファイアウォールの設定で実行できることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-160">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="20e86-161">この問題が発生するのは、Web 配置が Web 管理サービスの展開 (8172) で非標準ポートを使用するためです。その他の接続の場合、Web 配置はポート80を使用します。</span><span class="sxs-lookup"><span data-stu-id="20e86-161">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="20e86-162">サードパーティのホスティングプロバイダーにデプロイする場合、通常は Web 管理サービスを使用します。</span><span class="sxs-lookup"><span data-stu-id="20e86-162">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="20e86-163">既定の .NET 4.0 アプリケーションプールが存在しません</span><span class="sxs-lookup"><span data-stu-id="20e86-163">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-164">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-164">Scenario</span></span>

<span data-ttu-id="20e86-165">.NET Framework 4 を必要とするアプリケーションを展開すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-165">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

<span data-ttu-id="20e86-166">既定の .NET 4.0 アプリケーションプールが存在しないか、アプリケーションを追加できませんでした。</span><span class="sxs-lookup"><span data-stu-id="20e86-166">The default .NET 4.0 application pool does not exist or the application could not be added.</span></span> <span data-ttu-id="20e86-167">ASP.NET 4.0 がこのコンピューターにインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-167">Please verify that ASP.NET 4.0 is installed on this machine.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-168">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-168">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-169">ASP.NET 4 は IIS にインストールされていません。</span><span class="sxs-lookup"><span data-stu-id="20e86-169">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="20e86-170">配置先のサーバーが開発用コンピューターで、Visual Studio 2010 がインストールされている場合、ASP.NET 4 はコンピューターにインストールされますが、IIS にインストールされていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-170">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="20e86-171">デプロイ先のサーバーで、次のコマンドを実行して、管理者特権でのコマンドプロンプトを開き、ASP.NET 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="20e86-171">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

<span data-ttu-id="20e86-172">また、既定のアプリケーションプールの .NET Framework バージョンを手動で設定することが必要になる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="20e86-172">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="20e86-173">詳細については、このシリーズの「テスト環境として IIS に展開する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-173">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="20e86-174">初期化文字列の形式は、インデックス0から始まる仕様に準拠していません。</span><span class="sxs-lookup"><span data-stu-id="20e86-174">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-175">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-175">Scenario</span></span>

<span data-ttu-id="20e86-176">ワンクリック発行を使用してアプリケーションを配置した後、データベースにアクセスするページを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-176">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

<span data-ttu-id="20e86-177">初期化文字列の形式は、インデックス0から始まる仕様に準拠していません。</span><span class="sxs-lookup"><span data-stu-id="20e86-177">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-178">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-178">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-179">配置したサイトの web.config ファイルを開き、次の例に示すように、接続*文字列の値*が `$(ReplaceableToken_`で始まるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="20e86-179">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplaceableToken_`, as in the following example:</span></span>

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

<span data-ttu-id="20e86-180">接続文字列が次の例のようになっている場合は、プロジェクトファイルを編集し、次のプロパティを、すべてのビルド構成の PropertyGroup 要素に追加します。</span><span class="sxs-lookup"><span data-stu-id="20e86-180">If the connection strings look like this example, edit the project file and add the following property to the PropertyGroup element that is for all build configurations:</span></span>

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

<span data-ttu-id="20e86-181">その後、アプリケーションを再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="20e86-181">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="20e86-182">HTTP 500 内部サーバーエラー</span><span class="sxs-lookup"><span data-stu-id="20e86-182">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-183">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-183">Scenario</span></span>

<span data-ttu-id="20e86-184">展開されたサイトを実行すると、次のエラーメッセージが表示され、エラーの原因を示す特定の情報が表示されません。</span><span class="sxs-lookup"><span data-stu-id="20e86-184">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

<span data-ttu-id="20e86-185">HTTP エラー 500-内部サーバーエラー。</span><span class="sxs-lookup"><span data-stu-id="20e86-185">HTTP Error 500 - Internal Server Error.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-186">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-186">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-187">500エラーには多くの原因がありますが、これらのチュートリアルに従うと、web.config 変換ファイルの1つに XML 要素を誤った場所に配置することが考えられます。</span><span class="sxs-lookup"><span data-stu-id="20e86-187">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the Web.config transformation files.</span></span> <span data-ttu-id="20e86-188">たとえば、&lt;の場所&gt; 要素を &lt;構成&gt;の直接ではなく &lt;system.web&gt; に挿入する変換を行うと、このエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="20e86-188">For example, you would get this error if you put the transformation that inserts a &lt;location&gt; element under &lt;system.web&gt; instead of directly under &lt;configuration&gt;.</span></span> <span data-ttu-id="20e86-189">Web.config 変換プレビュー機能を使用して、変換が意図したとおりに動作していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="20e86-189">You can use the Web.config transform preview feature to verify that transformations are working as intended.</span></span> <span data-ttu-id="20e86-190">正しくコード化されていない変換が見つかった場合の解決策は、変換ファイルを修正して再配置することです。</span><span class="sxs-lookup"><span data-stu-id="20e86-190">The solution if you find a transform that was coded incorrectly is to correct the transformation file and redeploy.</span></span> <span data-ttu-id="20e86-191">エラーが明確でない場合は、変換をコメントアウトして、500エラーの原因となっているものを確認してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-191">If an error isn't obvious, try commenting out transforms and redeploying to see which one is causing the 500 error.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="20e86-192">HTTP 500.21 内部サーバーエラー</span><span class="sxs-lookup"><span data-stu-id="20e86-192">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-193">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-193">Scenario</span></span>

<span data-ttu-id="20e86-194">展開されたサイトを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-194">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="20e86-195">HTTP エラー 500.21-内部サーバーエラー。</span><span class="sxs-lookup"><span data-stu-id="20e86-195">HTTP Error 500.21 - Internal Server Error.</span></span> <span data-ttu-id="20e86-196">ハンドラー "Pagehandler ファクトリ-Integrated" のモジュールリストに無効なモジュール "ManagedPipelineHandler" があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-196">Handler "PageHandlerFactory-Integrated" has a bad module "ManagedPipelineHandler" in its module list.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-197">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-197">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-198">展開したサイトは ASP.NET 4 をターゲットにしていますが、ASP.NET 4 はサーバーの IIS に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="20e86-198">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="20e86-199">サーバーで、管理者特権でのコマンドプロンプトを開き、次のコマンドを実行して ASP.NET 4 を登録します。</span><span class="sxs-lookup"><span data-stu-id="20e86-199">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

<span data-ttu-id="20e86-200">また、既定のアプリケーションプールの .NET Framework バージョンを手動で設定することが必要になる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="20e86-200">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="20e86-201">詳細については、このシリーズの「テスト環境として IIS に展開する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-201">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a><span data-ttu-id="20e86-202">アプリ\_データ内の SQL Server Express データベースを開くことができませんでした</span><span class="sxs-lookup"><span data-stu-id="20e86-202">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-203">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-203">Scenario</span></span>

<span data-ttu-id="20e86-204">*Web.config ファイルの*接続文字列を更新して、 *App\_Data*フォルダー内の *.mdf*ファイルとして SQL Server Express データベースを指すようにしました。アプリケーションを初めて実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-204">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="20e86-205">SqlException: ログインによって要求されたデータベース "DatabaseName" を開くことができません。</span><span class="sxs-lookup"><span data-stu-id="20e86-205">System.Data.SqlClient.SqlException: Cannot open database "DatabaseName" requested by the login.</span></span> <span data-ttu-id="20e86-206">ログインに失敗しました。</span><span class="sxs-lookup"><span data-stu-id="20e86-206">The login failed.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-207">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-207">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-208">*.Mdf*ファイルの名前は、以前に既存のデータベースの *.mdf*ファイルを削除した場合でも、コンピューター上に存在していた SQL Server Express データベースの名前と一致させることはできません。</span><span class="sxs-lookup"><span data-stu-id="20e86-208">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="20e86-209">*.Mdf*ファイルの名前を、データベース名として使用されていない名前に変更し、新しい名前を使用するように*web.config ファイルを*変更します。</span><span class="sxs-lookup"><span data-stu-id="20e86-209">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="20e86-210">別の方法として、 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)を使用して、以前に存在していた SQL Server Express データベースを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="20e86-210">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="20e86-211">モデルの互換性を確認できません</span><span class="sxs-lookup"><span data-stu-id="20e86-211">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-212">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-212">Scenario</span></span>

<span data-ttu-id="20e86-213">新しい SQL Server Express データベースを指すように*web.config ファイルの接続文字列を更新*し、アプリケーションを初めて実行したときに、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-213">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="20e86-214">データベースにモデルメタデータが含まれていないため、モデルの互換性を確認できません。</span><span class="sxs-lookup"><span data-stu-id="20e86-214">Model compatibility cannot be checked because the database does not contain model metadata.</span></span> <span data-ttu-id="20e86-215">DbModelBuilder の規則に IncludeMetadataConvention が追加されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="20e86-215">Ensure that IncludeMetadataConvention has been added to the DbModelBuilder conventions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-216">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-216">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-217">Web.config ファイルに指定したデータベース名が、コンピューター上で以前に使用されていた場合は、データベースが既に存在している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-217">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="20e86-218">前にコンピューターで使用されていない新しい名前を選択し、この新しいデータベース名を使用するように*web.config ファイルを変更します。*</span><span class="sxs-lookup"><span data-stu-id="20e86-218">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="20e86-219">別の方法として、 [SQL Server Express ユーティリティ](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)または[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)を使用して、既存のデータベースを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="20e86-219">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="20e86-220">スクリプトがユーザーまたはロールを作成しようとしたときの SQL エラー</span><span class="sxs-lookup"><span data-stu-id="20e86-220">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-221">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-221">Scenario</span></span>

<span data-ttu-id="20e86-222">**[Sql のパッケージ化/発行]** タブで構成されたデータベース配置を使用している場合、配置中に実行される SQL スクリプトには create User または create Role コマンドがあり、これらのコマンドが実行されるとスクリプトの実行が失敗します。</span><span class="sxs-lookup"><span data-stu-id="20e86-222">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="20e86-223">次のような詳細なメッセージが表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-223">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

<span data-ttu-id="20e86-224">**[SQL のパッケージ化/発行]** タブではなく、 **Web の発行**ウィザードでデータベースの配置を構成したときにこのエラーが発生した場合は、[[構成と配置](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)] フォーラムでスレッドを作成すると、このトラブルシューティングのページにソリューションが追加されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-224">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-225">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-225">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-226">配置の実行に使用しているユーザーアカウントに、ユーザーまたはロールを作成するためのアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="20e86-226">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="20e86-227">たとえば、ホスティング会社では、データベース\_datareader、db\_datawriter、および db\_ddladmin の各ロールが設定されているユーザーアカウントに割り当てられる場合があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-227">For example, the hosting company might assign the db\_datareader, db\_datawriter, and db\_ddladmin roles to the user account that it sets up for you.</span></span> <span data-ttu-id="20e86-228">これらは、ほとんどのデータベースオブジェクトを作成するのに十分ですが、ユーザーまたはロールを作成するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="20e86-228">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="20e86-229">このエラーを回避する方法の1つは、データベースの配置からユーザーとロールを除外することです。</span><span class="sxs-lookup"><span data-stu-id="20e86-229">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="20e86-230">これを行うには、データベースの自動的に生成されたスクリプトの PreSource 要素を編集して、次の属性が含まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="20e86-230">You can do this by editing the PreSource element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

<span data-ttu-id="20e86-231">プロジェクトファイルで PreSource 要素を編集する方法の詳細については、「[方法: プロジェクトファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-231">For information about how to edit the PreSource element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="20e86-232">開発用データベースのユーザーまたはロールが転送先データベースに存在する必要がある場合は、ホスティングプロバイダーに問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="20e86-232">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="20e86-233">配置時にカスタムスクリプトを実行すると SQL Server タイムアウトエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="20e86-233">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-234">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-234">Scenario</span></span>

<span data-ttu-id="20e86-235">配置時に実行するカスタム SQL スクリプトを指定し、Web 配置実行するとタイムアウトになります。</span><span class="sxs-lookup"><span data-stu-id="20e86-235">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-236">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-236">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-237">トランザクションモードが異なる複数のスクリプトを実行すると、タイムアウトエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-237">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="20e86-238">既定では、自動的に生成されたスクリプトはトランザクション内で実行されますが、カスタムスクリプトでは実行されません。</span><span class="sxs-lookup"><span data-stu-id="20e86-238">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="20e86-239">**[Sql のパッケージ化/発行]** タブで **[既存のデータベースからデータまたはスキーマをプル]** する オプションを選択し、カスタムの sql スクリプトを追加する場合は、すべてのスクリプトで同じトランザクション設定が使用されるように、一部のスクリプトのトランザクション設定を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-239">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="20e86-240">詳細については、「[方法: Web アプリケーションプロジェクトを使用してデータベースを配置](https://msdn.microsoft.com/library/dd465343.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-240">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="20e86-241">すべてが同じでもこのエラーが発生するようにトランザクション設定を構成した場合は、スクリプトを個別に実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="20e86-241">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="20e86-242">SQL の **[パッケージ化/発行]** タブの **[データベーススクリプト]** グリッドで、タイムアウトエラーを発生させるスクリプトの **[含める]** チェックボックスをオフにし、プロジェクトを発行します。</span><span class="sxs-lookup"><span data-stu-id="20e86-242">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="20e86-243">次に、 **[データベーススクリプト]** グリッドに戻り、そのスクリプトの **[インクルード]** チェックボックスをオンにして、他のスクリプトの **[含める]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="20e86-243">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="20e86-244">その後、プロジェクトを再度発行します。</span><span class="sxs-lookup"><span data-stu-id="20e86-244">Then publish the project again.</span></span> <span data-ttu-id="20e86-245">今回は、発行時に、選択したカスタムスクリプトのみが実行されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-245">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="20e86-246">サイトマニフェストのストリームデータはまだ使用できません</span><span class="sxs-lookup"><span data-stu-id="20e86-246">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-247">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-247">Scenario</span></span>

<span data-ttu-id="20e86-248">T (test) オプションを指定して *.deploy*ファイルを使用してパッケージをインストールすると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-248">When you are installing a package using the *deploy.cmd* file with the t (test) option, you see the following error message:</span></span>

<span data-ttu-id="20e86-249">エラー: ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlscript ' のストリームデータはまだ使用できません。</span><span class="sxs-lookup"><span data-stu-id="20e86-249">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-250">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-250">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-251">エラーメッセージは、コマンドがテストレポートを生成できないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="20e86-251">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="20e86-252">ただし、y (実際のインストール) オプションを使用すると、コマンドが実行される場合があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-252">However, the command might run if you use the y (actual installation) option.</span></span> <span data-ttu-id="20e86-253">このメッセージは、テストモードでのコマンドの実行に問題があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="20e86-253">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="20e86-254">このアプリケーションには ManagedRuntimeVersion v4.0 が必要です</span><span class="sxs-lookup"><span data-stu-id="20e86-254">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-255">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-255">Scenario</span></span>

<span data-ttu-id="20e86-256">を展開しようとすると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-256">When you attempt to deploy, you see the following error message:</span></span>

<span data-ttu-id="20e86-257">使用しようとしているアプリケーションプールの ' managedRuntimeVersion ' プロパティが ' v2.0 ' に設定されています。</span><span class="sxs-lookup"><span data-stu-id="20e86-257">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="20e86-258">このアプリケーションには ' v4.0 ' が必要です。</span><span class="sxs-lookup"><span data-stu-id="20e86-258">This application requires 'v4.0'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-259">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-259">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-260">ASP.NET 4 は IIS にインストールされていません。</span><span class="sxs-lookup"><span data-stu-id="20e86-260">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="20e86-261">配置先のサーバーが開発用コンピューターで、Visual Studio 2010 がインストールされている場合、ASP.NET 4 はコンピューターにインストールされますが、IIS にインストールされていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-261">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="20e86-262">デプロイ先のサーバーで、次のコマンドを実行して、管理者特権でのコマンドプロンプトを開き、ASP.NET 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="20e86-262">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="20e86-263">Microsoft. Deployment. DeploymentProviderOptions をキャストできません</span><span class="sxs-lookup"><span data-stu-id="20e86-263">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-264">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-264">Scenario</span></span>

<span data-ttu-id="20e86-265">パッケージを展開すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-265">When you are deploying a package, you see the following error message:</span></span>

<span data-ttu-id="20e86-266">型 ' Microsoft. Deployment. DeploymentProviderOptions ' のオブジェクトを ' Microsoft. Deployment. DeploymentProviderOptions ' にキャストできません。</span><span class="sxs-lookup"><span data-stu-id="20e86-266">Unable to cast object of type 'Microsoft.Web.Deployment.DeploymentProviderOptions' to 'Microsoft.Web.Deployment.DeploymentProviderOptions'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-267">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-267">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-268">Web 配置 1.1 UI を使用して、Web 配置2.0 がインストールされているサーバーに IIS マネージャーから展開しようとしています。</span><span class="sxs-lookup"><span data-stu-id="20e86-268">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="20e86-269">IIS リモート管理ツールを使用してパッケージをインポートして展開する場合は、接続を確立するときに **[利用可能な新機能]** ダイアログボックスを確認します。</span><span class="sxs-lookup"><span data-stu-id="20e86-269">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="20e86-270">(このダイアログボックスは、接続が最初に確立されたときに1回だけ表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-270">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="20e86-271">接続をクリアして最初からやり直すには、IIS マネージャーを終了し、コマンドプロンプトで「inetmgr.exe/reset」と入力して再度起動します)。一覧に表示されている機能の1つが**WEB 配置 UI**で、バージョン番号が8よりも低い場合、展開先のサーバーに1.1 と2.0 の両方のバージョンの Web 配置がインストールされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-271">To clear the connection and start over, close IIS Manager and start it up again by entering inetmgr /reset at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="20e86-272">2\.0 がインストールされているクライアントから展開するには、サーバーに Web 配置2.0 のみがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-272">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="20e86-273">この問題を解決するには、ホスティングプロバイダーに連絡する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-273">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="20e86-274">SQL Server Compact のネイティブコンポーネントを読み込むことができません</span><span class="sxs-lookup"><span data-stu-id="20e86-274">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-275">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-275">Scenario</span></span>

<span data-ttu-id="20e86-276">展開されたサイトを実行すると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-276">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="20e86-277">バージョン8482の ADO.NET プロバイダーに対応する SQL Server Compact のネイティブコンポーネントを読み込むことができません。</span><span class="sxs-lookup"><span data-stu-id="20e86-277">Unable to load the native components of SQL Server Compact corresponding to the ADO.NET provider of version 8482.</span></span> <span data-ttu-id="20e86-278">正しいバージョンの SQL Server Compact をインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="20e86-278">Install the correct version of SQL Server Compact.</span></span> <span data-ttu-id="20e86-279">詳細については、サポート技術情報の記事974247を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-279">Refer to KB article 974247 for more details.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-280">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-280">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-281">配置されたサイトには、ネイティブアセンブリをアプリケーションの*bin*フォルダーの下に持つ*amd64*および*x86*サブフォルダーがありません。</span><span class="sxs-lookup"><span data-stu-id="20e86-281">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="20e86-282">SQL Server Compact がインストールされているコンピューターでは、ネイティブアセンブリは*C:\Program are SQL Server Compact Edition\v4.0\Private*に配置されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-282">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="20e86-283">Visual Studio プロジェクトの正しいフォルダーに正しいファイルを取り込むには、NuGet SqlServerCompact パッケージをインストールするのが最善の方法です。</span><span class="sxs-lookup"><span data-stu-id="20e86-283">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="20e86-284">パッケージのインストールでは、ネイティブアセンブリを*amd64*および*x86*にコピーするビルド後スクリプトが追加されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-284">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="20e86-285">ただし、これらを展開するためには、プロジェクトに手動で含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-285">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="20e86-286">詳細については、 [SQL Server Compact のデプロイ](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)に関するチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-286">For more information, see the [Deploying SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="20e86-287">Entity Framework Code First アプリケーションを展開した後の "パスが有効ではありません" エラーが発生する</span><span class="sxs-lookup"><span data-stu-id="20e86-287">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-288">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-288">Scenario</span></span>

<span data-ttu-id="20e86-289">Entity Framework Code First Migrations を使用するアプリケーションと DBMS (SQL Server Compact など) をデプロイして、そのデータベースをアプリの\_データフォルダー内のファイルに格納します。</span><span class="sxs-lookup"><span data-stu-id="20e86-289">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="20e86-290">最初の配置後にデータベースを作成するように構成された Code First Migrations。</span><span class="sxs-lookup"><span data-stu-id="20e86-290">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="20e86-291">アプリケーションを実行すると、次の例のようなエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-291">When you run the application you get an error message like the following example:</span></span>

<span data-ttu-id="20e86-292">パスが無効です。</span><span class="sxs-lookup"><span data-stu-id="20e86-292">The path is not valid.</span></span> <span data-ttu-id="20e86-293">データベースのディレクトリを確認してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-293">Check the directory for the database.</span></span> <span data-ttu-id="20e86-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]</span><span class="sxs-lookup"><span data-stu-id="20e86-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-295">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-295">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-296">データベースを作成しようとしていますが、アプリ\_データフォルダーが存在しません Code First。</span><span class="sxs-lookup"><span data-stu-id="20e86-296">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="20e86-297">デプロイ時に*app\_data*フォルダーにファイルがないか、プロジェクトプロパティウィンドウの **[パッケージ/発行 Web]** タブで [**アプリ\_データを除外**する] を選択しました。</span><span class="sxs-lookup"><span data-stu-id="20e86-297">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the Project Properties window.</span></span> <span data-ttu-id="20e86-298">サーバーにコピーするファイルがフォルダーに存在しない場合、配置プロセスではサーバーにフォルダーが作成されません。</span><span class="sxs-lookup"><span data-stu-id="20e86-298">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="20e86-299">サイトにデータベースが既にセットアップされている場合は、[発行プロファイル] で [**宛先にある追加のファイルを削除**する] を選択した場合、配置プロセスによってファイルと*アプリ\_データ*フォルダー自体が削除されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-299">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="20e86-300">この問題を解決するには、*アプリの\_データ*フォルダーに .txt ファイルなどのプレースホルダーファイルを配置し、[**アプリ\_データを除外**する] を選択して再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="20e86-300">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span>

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="20e86-301">"基になる RCW から分離された COM オブジェクトは使用できません。"</span><span class="sxs-lookup"><span data-stu-id="20e86-301">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-302">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-302">Scenario</span></span>

<span data-ttu-id="20e86-303">これで、ワンクリック発行を使用してアプリケーションをデプロイした後、次のエラーが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="20e86-303">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

<span data-ttu-id="20e86-304">Web 配置タスクが失敗しました。</span><span class="sxs-lookup"><span data-stu-id="20e86-304">Web deployment task failed.</span></span> <span data-ttu-id="20e86-305">(リモートエージェント URL '<https://serverurl.com/msdeploy.axd?site=sitename>' への要求を完了できませんでした。)</span><span class="sxs-lookup"><span data-stu-id="20e86-305">(Could not complete the request to remote agent URL '<https://serverurl.com/msdeploy.axd?site=sitename>'.)</span></span>  
 <span data-ttu-id="20e86-306">リモートエージェント URL '<https://url/msdeploy.axd?site=sitename>' への要求を完了できませんでした。</span><span class="sxs-lookup"><span data-stu-id="20e86-306">Could not complete the request to remote agent URL '<https://url/msdeploy.axd?site=sitename>'.</span></span>  
<span data-ttu-id="20e86-307">要求が中止されました: 要求は取り消されました。</span><span class="sxs-lookup"><span data-stu-id="20e86-307">The request was aborted: The request was canceled.</span></span>  
<span data-ttu-id="20e86-308">基になる RCW から分離された COM オブジェクトは使用できません。</span><span class="sxs-lookup"><span data-stu-id="20e86-308">COM object that has been separated from its underlying RCW cannot be used.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-309">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-309">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-310">通常、このエラーを解決するには、Visual Studio の終了と再起動が必要です。</span><span class="sxs-lookup"><span data-stu-id="20e86-310">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="20e86-311">発行に使用されるユーザーの資格情報に setACL 機関がないため、展開が失敗する</span><span class="sxs-lookup"><span data-stu-id="20e86-311">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-312">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-312">Scenario</span></span>

<span data-ttu-id="20e86-313">フォルダーのアクセス許可を設定する権限がないことを示すエラーが表示され、発行が失敗します (使用しているユーザーアカウントには setACL 機関がありません)。</span><span class="sxs-lookup"><span data-stu-id="20e86-313">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-314">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-314">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-315">既定では、Visual Studio はサイトのルートフォルダーに対する読み取りアクセス許可を設定し、App\_Data フォルダーに対する書き込みアクセス許可を設定します。</span><span class="sxs-lookup"><span data-stu-id="20e86-315">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="20e86-316">サイトフォルダーの既定のアクセス許可が正しいことがわかっていて、設定する必要がない場合は、この動作を無効にします。そのためには、発行プロファイルファイル (単一のプロファイルに影響を与える場合) または (すべてのプロファイルに影響を与える場合は) .targets ファイルに **&lt;includesetaclprovideron ondestination&lt;&gt;** を追加します。&gt;</span><span class="sxs-lookup"><span data-stu-id="20e86-316">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="20e86-317">これらのファイルを編集する方法の詳細については、「[方法: プロファイル (pubxml) ファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-317">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="20e86-318">アプリケーションがアプリケーションフォルダーに書き込もうとしたときにアクセス拒否エラーが発生する</span><span class="sxs-lookup"><span data-stu-id="20e86-318">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-319">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-319">Scenario</span></span>

<span data-ttu-id="20e86-320">アプリケーションフォルダーのいずれかでファイルを作成または編集しようとすると、アプリケーションエラーが発生します。これは、そのフォルダーに対する書き込み権限がないためです。</span><span class="sxs-lookup"><span data-stu-id="20e86-320">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-321">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-321">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-322">既定では、Visual Studio はサイトのルートフォルダーに対する読み取りアクセス許可を設定し、App\_Data フォルダーに対する書き込みアクセス許可を設定します。</span><span class="sxs-lookup"><span data-stu-id="20e86-322">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="20e86-323">アプリケーションにサブフォルダーへの書き込みアクセス権が必要な場合は、このシリーズの「フォルダーのアクセス許可の設定」と「運用環境へのデプロイ」に示されているように、そのフォルダーのアクセス許可を設定できます。</span><span class="sxs-lookup"><span data-stu-id="20e86-323">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the Setting Folder Permissions and Deploying to the Production Environment tutorials in this series.</span></span> <span data-ttu-id="20e86-324">アプリケーションにサイトのルートフォルダーへの書き込みアクセス権が必要な場合は、ルートフォルダーに対する読み取り専用アクセスを設定できないようにする必要があります。これを行うには、発行プロファイルファイル (単一のプロファイルに影響を与える場合) または (すべてのプロファイルに影響を与える場合) .targets ファイルに **&lt;includesetaclprovideron&lt;&gt;on**を追加します&gt;</span><span class="sxs-lookup"><span data-stu-id="20e86-324">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="20e86-325">これらのファイルを編集する方法の詳細については、「[方法: プロファイル (pubxml) ファイルの配置設定を編集](https://msdn.microsoft.com/library/ff398069.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-325">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="20e86-326">構成エラー-targetFramework 属性が、インストールされているバージョンより後のバージョンを参照してい .NET Framework</span><span class="sxs-lookup"><span data-stu-id="20e86-326">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-327">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-327">Scenario</span></span>

<span data-ttu-id="20e86-328">ASP.NET 4.5 を対象とする web プロジェクトが正常に発行されましたが、アプリケーションを実行すると (web.config ファイルで customErrors モードが "off" に設定されている場合)、次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-328">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the customErrors mode set to "off" in the Web.config file) you get the following error:</span></span>

<span data-ttu-id="20e86-329">Web.config ファイルの &lt;のコンパイル&gt; 要素の ' targetFramework ' 属性は、バージョン4.0 以降の .NET Framework をターゲットとするためにのみ使用されます (たとえば、'&lt;コンパイル targetFramework = "4.0"&gt;')。</span><span class="sxs-lookup"><span data-stu-id="20e86-329">The 'targetFramework' attribute in the &lt;compilation&gt; element of the Web.config file is used only to target version 4.0 and later of the .NET Framework (for example, '&lt;compilation targetFramework="4.0"&gt;').</span></span> <span data-ttu-id="20e86-330">' TargetFramework ' 属性は、現在インストールされているバージョンの .NET Framework より新しいバージョンを参照しています。</span><span class="sxs-lookup"><span data-stu-id="20e86-330">The 'targetFramework' attribute currently references a version that is later than the installed version of the .NET Framework.</span></span> <span data-ttu-id="20e86-331">.NET Framework の有効なターゲットバージョンを指定するか、必要なバージョンの .NET Framework をインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="20e86-331">Specify a valid target version of the .NET Framework, or install the required version of the .NET Framework.</span></span>

<span data-ttu-id="20e86-332">エラーページの [ソースエラー] ボックスには、web.config の次の行がエラーの原因として強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-332">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

<span data-ttu-id="20e86-333">&lt;コンパイル targetFramework = "4.5"/&gt;</span><span class="sxs-lookup"><span data-stu-id="20e86-333">&lt;compilation targetFramework="4.5" /&gt;</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-334">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-334">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-335">サーバーは ASP.NET 4.5 をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="20e86-335">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="20e86-336">ASP.NET 4.5 のサポートを追加できるかどうかを判断するには、ホスティングプロバイダーに問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="20e86-336">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="20e86-337">サーバーのアップグレードがオプションではない場合は、代わりに ASP.NET 4 以前を対象とする web プロジェクトをデプロイする必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-337">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.</span></span>

<span data-ttu-id="20e86-338">ASP.NET 4 以前の web プロジェクトを同じ宛先に配置する場合は、 **web の発行**ウィザードの **[設定]** タブにある **[変換先で追加のファイルを削除]** する チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="20e86-338">If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="20e86-339">[**転送先で追加のファイルを削除**する] を選択しないと、構成エラーページが引き続き表示されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-339">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="20e86-340">[プロジェクトの**プロパティ**] ウィンドウには [ターゲットフレームワーク] ドロップダウンリストが含まれていますが、 **.NET Framework 4.5**から **.NET Framework 4**に変更するだけでこの問題を解決することはできません。</span><span class="sxs-lookup"><span data-stu-id="20e86-340">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="20e86-341">ターゲットフレームワークを以前のバージョンの framework に変更すると、プロジェクトはその後のフレームワークバージョンのアセンブリへの参照を保持し、実行されなくなります。</span><span class="sxs-lookup"><span data-stu-id="20e86-341">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="20e86-342">これらの参照を手動で変更するか、.NET Framework 4 以前を対象とする新しいプロジェクトを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-342">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="20e86-343">詳細については、「 [Web サイトのターゲット設定 .NET Framework](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-343">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

## <a name="medium-trust-errors"></a><span data-ttu-id="20e86-344">中程度の信頼エラー</span><span class="sxs-lookup"><span data-stu-id="20e86-344">Medium Trust Errors</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-345">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-345">Scenario</span></span>

<span data-ttu-id="20e86-346">運用環境でアプリケーションを実行すると、中程度の信頼に関連するエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="20e86-346">When you run your application in production, it gets an error related to medium trust.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-347">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-347">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-348">多くのサードパーティのホスティングプロバイダーは、web サイトを中程度の信頼で実行しています。これは、許可されていないものがあることを意味します。</span><span class="sxs-lookup"><span data-stu-id="20e86-348">Many third-party hosting providers run your web site in medium trust, which means that there are some things it isn't allowed to do.</span></span> <span data-ttu-id="20e86-349">たとえば、アプリケーションコードは Windows レジストリにアクセスできず、アプリケーションのフォルダー階層の外部にあるファイルの読み取りや書き込みもできません。</span><span class="sxs-lookup"><span data-stu-id="20e86-349">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="20e86-350">既定では、アプリケーションはローカルコンピューター上で*完全信頼*で実行されます。つまり、アプリケーションは、運用環境に配置するときに失敗する可能性がある処理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="20e86-350">By default your application runs in *full trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span>

<span data-ttu-id="20e86-351">トラブルシューティングを行うために、ローカル IIS 環境で中程度の信頼でアプリケーションを実行するように構成できます。</span><span class="sxs-lookup"><span data-stu-id="20e86-351">You can configure the application to run in medium trust in the local IIS environment in order to troubleshoot.</span></span> <span data-ttu-id="20e86-352">これを行うには、アプリケーションの*web.config*ファイルを開き、次の例に示すように、system.web 要素に**trust**要素を追加**します。**</span><span class="sxs-lookup"><span data-stu-id="20e86-352">To do that, open the application *Web.config* file, and add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

<span data-ttu-id="20e86-353">これで、アプリケーションはローカルコンピューター上でも IIS の中程度の信頼で実行されるようになります。</span><span class="sxs-lookup"><span data-stu-id="20e86-353">The application will now run in medium trust in IIS even on your local computer.</span></span>

<span data-ttu-id="20e86-354">Azure には中程度の信頼が必要ないため、Azure App Service にデプロイする場合は、この操作を行わないでください。</span><span class="sxs-lookup"><span data-stu-id="20e86-354">Don't do this if you are deploying to Azure App Service, because Azure does not require medium trust.</span></span> <span data-ttu-id="20e86-355">このチュートリアルが2012年2月に作成された時点で、この方法を使用してアプリケーションを中程度の信頼で実行すると、Azure でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="20e86-355">At the time this tutorial is being written in February, 2012, using this method to make your application run in medium trust will cause an error in Azure.</span></span>

<span data-ttu-id="20e86-356">Entity Framework Code First Migrations を使用していて、中程度の信頼でアプリケーションを実行するホスティングプロバイダーにデプロイする場合は、バージョン5.0 以降がインストールされていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-356">If you are using Entity Framework Code First Migrations and you are deploying to a hosting provider that runs your application in medium trust, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="20e86-357">Entity Framework バージョン4.3 では、データベーススキーマを更新するために、移行には完全な信頼が必要です。</span><span class="sxs-lookup"><span data-stu-id="20e86-357">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>

## <a name="http-40417-not-found-error"></a><span data-ttu-id="20e86-358">HTTP 404.17 が見つかりませんエラー</span><span class="sxs-lookup"><span data-stu-id="20e86-358">HTTP 404.17 Not Found Error</span></span>

### <a name="scenario"></a><span data-ttu-id="20e86-359">シナリオ</span><span class="sxs-lookup"><span data-stu-id="20e86-359">Scenario</span></span>

<span data-ttu-id="20e86-360">配置したサイトを IIS で開発用コンピューターで実行すると、次のエラーメッセージが表示され、サーバーが default.aspx を処理できないことが報告されます。</span><span class="sxs-lookup"><span data-stu-id="20e86-360">When you run the deployed site on your development computer in IIS, you see the following error message reporting that the server can't process Default.aspx:</span></span>

<span data-ttu-id="20e86-361">HTTP エラー 404.17-見つかりません</span><span class="sxs-lookup"><span data-stu-id="20e86-361">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="20e86-362">要求されたコンテンツはスクリプトであり、静的ファイルハンドラーによって処理されません。</span><span class="sxs-lookup"><span data-stu-id="20e86-362">The requested content appears to be script and will not be served by the static file handler.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="20e86-363">考えられる原因と解決策</span><span class="sxs-lookup"><span data-stu-id="20e86-363">Possible Cause and Solution</span></span>

<span data-ttu-id="20e86-364">コンピューターに ASP.NET 4.5 がインストールされていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20e86-364">ASP.NET 4.5 might not be installed on your computer.</span></span> <span data-ttu-id="20e86-365">ASP.NET 4.5 をインストールする方法については、このシリーズの「テスト環境として IIS に展開する」の手順を参照してください。</span><span class="sxs-lookup"><span data-stu-id="20e86-365">See the steps in the Deploying to IIS as a Test Environment tutorial in this series that explain how to install ASP.NET 4.5.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20e86-366">[[戻る]](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="20e86-366">[Previous](deploying-extra-files.md)</span></span>
