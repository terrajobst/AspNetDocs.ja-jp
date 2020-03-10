---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1.0 と 1.1 | のサイドバイサイド実行Microsoft Docs
author: rick-anderson
description: このホワイトペーパーでは、.NET 1.0 と .NET 1.1 の両方をコンピューターにインストールする方法について説明します。これにより、ASP.NET Web アプリケーションをいずれかのバージョンの fram で実行できるようになります。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513832"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="ea799-103">ASP.NET で .NET Framework 1.0 と 1.1 を並行して実行する</span><span class="sxs-lookup"><span data-stu-id="ea799-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="ea799-104">このホワイトペーパーでは、.NET 1.0 と .NET 1.1 の両方をコンピューターにインストールする方法について説明します。これにより、ASP.NET Web アプリケーションをいずれかのバージョンのフレームワークで実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ea799-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="ea799-105">ASP.NET 1.0 と ASP.NET 1.1 に適用されます。</span><span class="sxs-lookup"><span data-stu-id="ea799-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="ea799-106">ASP.NET では、アプリケーションは同じコンピューターにインストールされているときにサイドバイサイドで実行されますが、異なるバージョンの .NET Framework を使用します。</span><span class="sxs-lookup"><span data-stu-id="ea799-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="ea799-107">次のトピックでは、ASP.NET アプリケーションを side-by-side 実行用に構成する方法について説明し、詳細な手順を示します。</span><span class="sxs-lookup"><span data-stu-id="ea799-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="ea799-108">インストール中に .NET Framework バージョン1.0 への Web アプリケーションのマッピングを維持する</span><span class="sxs-lookup"><span data-stu-id="ea799-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="ea799-109">Web アプリケーションを特定のバージョンの .NET Framework にマップする</span><span class="sxs-lookup"><span data-stu-id="ea799-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="ea799-110">Web サイトが使用している .NET Framework のバージョンを確認する</span><span class="sxs-lookup"><span data-stu-id="ea799-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="ea799-111">従来、コンピューターでコンポーネントまたはアプリケーションが更新されると、古いバージョンが削除され、新しいバージョンに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="ea799-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="ea799-112">新しいバージョンが以前のバージョンと互換性がない場合は、通常、コンポーネントまたはアプリケーションを使用する他のアプリケーションが中断されます。</span><span class="sxs-lookup"><span data-stu-id="ea799-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="ea799-113">.NET Framework は、side-by-side 実行のサポートを提供します。これにより、複数のバージョンのアセンブリまたはアプリケーションを同じコンピューターに同時にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="ea799-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="ea799-114">複数のバージョンを同時にインストールできるため、マネージアプリケーションでは、別のバージョンを使用するアプリケーションに影響を与えずに、使用するバージョンを選択できます。</span><span class="sxs-lookup"><span data-stu-id="ea799-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="ea799-115">既定では .NET Framework バージョン1.1 のインストール時に、.NET Framework の最新バージョンを使用するように既存のすべての ASP.NET アプリケーションが自動的に再構成されます。</span><span class="sxs-lookup"><span data-stu-id="ea799-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="ea799-116">ASP.NET アプリケーションで既定 .NET Framework 1.1 に設定しない場合は、[ここ](#1)をクリックして、インストール中にこれを回避する方法を確認してください。</span><span class="sxs-lookup"><span data-stu-id="ea799-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="ea799-117">Web サーバーを .NET Framework 1.1 に更新し、1つまたは複数の Web アプリケーションで .NET Framework 1.0 を実行する場合は、インターネットインフォメーションサービス (IIS) スクリプトマップを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea799-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="ea799-118">スクリプトマッピングは、特定の Web アプリケーションの .aspx ファイル拡張子を .NET Framework のバージョンにマップするメカニズムです。</span><span class="sxs-lookup"><span data-stu-id="ea799-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="ea799-119">[ここ](#2)をクリックして、Web アプリケーションを特定のバージョンの .NET Framework にマップする方法を確認してください。</span><span class="sxs-lookup"><span data-stu-id="ea799-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="ea799-120">インターネットインフォメーションマネージャーまたは ASP.NET IIS 登録ツール (Aspnet\_iis 登録ツール) を使用して、特定の Web アプリケーションを実行している .NET Framework バージョンを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="ea799-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="ea799-121">Web サイトが使用している .NET Framework のバージョンを確認するには、[ここ](#3)をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="ea799-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="ea799-122">.NET Framework 1.1 に移行する際の1つのインポートの考慮事項は、.NET Framework の各バージョンが独自の machine.config ファイルを使用することです。</span><span class="sxs-lookup"><span data-stu-id="ea799-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="ea799-123">このため、Web 管理者が machine.config ファイルに変更を加えた場合は、それらの変更を .NET Framework 1.1 の machine.config ファイルに移行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea799-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="ea799-124">インストール中に .NET Framework 1.0 への Web アプリケーションのマッピングを維持する</span><span class="sxs-lookup"><span data-stu-id="ea799-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="ea799-125">既定では、既存のすべての ASP.NET アプリケーションは、新しいバージョンの .NET Framework を使用するために、インストール時に自動的に再構成されます。</span><span class="sxs-lookup"><span data-stu-id="ea799-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="ea799-126">新しいバージョンの .NET Framework を使用すると、アプリケーションは、新しいリリースに含まれる機能強化や新機能を最大限に活用できます。</span><span class="sxs-lookup"><span data-stu-id="ea799-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="ea799-127">同時に、更新するアプリケーションをきめ細かく制御する必要がある Web 管理者は、.NET Framework のインストール中に、既存のすべての ASP.NET アプリケーションの自動再マップを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="ea799-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="ea799-128">ASP.NET アプリケーション全体を新しいバージョンの .NET Framework に自動的に再マップしないようにするために、Web 管理者は Dotnetfx.exe セットアッププログラムと共に/noaspupgrade コマンドラインオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ea799-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="ea799-129">**ASP.NET アプリケーションの新しいバージョンへの再マップの合計を回避するには**</span><span class="sxs-lookup"><span data-stu-id="ea799-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="ea799-130">**[スタート]** に移動します。</span><span class="sxs-lookup"><span data-stu-id="ea799-130">Go to **Start**.</span></span>
2. <span data-ttu-id="ea799-131">**[実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea799-131">Click on **run**.</span></span>
3. <span data-ttu-id="ea799-132">「**cmd**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="ea799-132">Type **cmd**.</span></span>
4. <span data-ttu-id="ea799-133">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea799-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="ea799-134">コマンドプロンプトで、次の行を入力して .NET Framework のインストールを開始します: **dotnetfx.exe/c: "install/noaspupgrade?** .</span><span class="sxs-lookup"><span data-stu-id="ea799-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="ea799-135">Microsoft .NET Framework 1.1 セットアップで [**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea799-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="ea799-136">.NET Framework 1.1 のセットアッププロセスが開始されます。</span><span class="sxs-lookup"><span data-stu-id="ea799-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="ea799-137">Web アプリケーションを特定のバージョンの .NET Framework にマップする</span><span class="sxs-lookup"><span data-stu-id="ea799-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="ea799-138">.NET Framework の各バージョンには、ASP.NET IIS Registration Tool (Aspnet\_iis 登録ツール) のバージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ea799-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="ea799-139">このツールを使用すると、管理者は、.NET Framework の特定のバージョンで Web アプリケーションを実行するように指定できます。</span><span class="sxs-lookup"><span data-stu-id="ea799-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="ea799-140">これは、Web アプリケーションを .NET Framework のバージョンにマッピングすることと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="ea799-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="ea799-141">管理者は、Web アプリケーションに関連付けられる .NET Framework のバージョンに対応する Aspnet\_iis 登録ツールを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea799-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="ea799-142">たとえば、Web サイトで .NET Framework 1.1 を使用することを指定する管理者は、.NET Framework 1.1 に付属する Aspnet\_iis 登録ツールを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea799-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="ea799-143">バージョン1.0 の Aspnet\_iis 登録ツールは次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="ea799-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="ea799-144">C:\windows\ microsoft.net \framework\\**v v1.0.3705**iis 登録ツール\_</span><span class="sxs-lookup"><span data-stu-id="ea799-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="ea799-145">Aspnet\_iis 登録ツールのバージョン1、1は次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="ea799-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="ea799-146">C:\windows\ microsoft.net \framework\\**v 1.1.4322**iis 登録ツール\_</span><span class="sxs-lookup"><span data-stu-id="ea799-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="ea799-147">Aspnet\_iis 登録ツールには、Web アプリケーションをマッピングするスクリプトの2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="ea799-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="ea799-148">**-s**は、パスとその子ディレクトリ内のスクリプトマップを設定します。</span><span class="sxs-lookup"><span data-stu-id="ea799-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="ea799-149">**-sn**パス内のスクリプトマップのみを設定します。</span><span class="sxs-lookup"><span data-stu-id="ea799-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="ea799-150">パスは、Web アプリケーションの IIS メタデータパスを定義します。これは、W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} の形式で定義されています。</span><span class="sxs-lookup"><span data-stu-id="ea799-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="ea799-151">たとえば、既定の Web サイトの下にあるポータルと呼ばれる Web アプリケーションの場合、メタベースのパスは W3SVC/1/ROOT/Portal です。</span><span class="sxs-lookup"><span data-stu-id="ea799-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="ea799-152">また、メタベースエディターというツールを使用して、メタベースパスを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="ea799-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="ea799-153">このツールは、Microsoft サポートサイトの[https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="ea799-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="ea799-154">Aspnet\_iis 登録ツール-s W3SVC/1/ROOT/Portal を実行して、ポータルの IIS スクリプトマップとそのサブアプリケーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="ea799-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="ea799-155">Aspnet\_iis 登録ツール-sn W3SVC/1/ROOT/Portal を実行して、ポータルのサブディレクトリ内のアプリケーションに影響を与えずに、ポータルの IIS スクリプトマップを更新します。</span><span class="sxs-lookup"><span data-stu-id="ea799-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="ea799-156">Web アプリケーションで使用している .NET Framework のバージョンを確認する</span><span class="sxs-lookup"><span data-stu-id="ea799-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="ea799-157">管理者は、インターネット Service Manager を使用して、Web サイトを実行している .NET Framework のバージョンを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="ea799-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="ea799-158">オペレーティングシステムのバージョンが異なると、インターネット Service Manager が異なる方法で起動します。</span><span class="sxs-lookup"><span data-stu-id="ea799-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="ea799-159">Service manager を起動するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="ea799-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="ea799-160">**インターネット Service Manager を開始するには**</span><span class="sxs-lookup"><span data-stu-id="ea799-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="ea799-161">**[スタート]** に移動します。</span><span class="sxs-lookup"><span data-stu-id="ea799-161">Go to **Start**.</span></span>
2. <span data-ttu-id="ea799-162">**[実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea799-162">Click on **run**.</span></span>
3. <span data-ttu-id="ea799-163">「 **Inetmgr.exe**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="ea799-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="ea799-164">インターネット Service Manager から、確認する .NET Framework のバージョンを持つ Web アプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ea799-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="ea799-165">Web アプリケーションを右クリックし、[プロパティ] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="ea799-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="ea799-166">[プロパティ] ウィンドウで、[構成] を選択し**ます。**</span><span class="sxs-lookup"><span data-stu-id="ea799-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="ea799-167">アプリケーションマッピングテーブルから **.aspx**を選択し、 **[編集]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea799-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="ea799-168">**[実行可能ファイル]** テキストボックスで、スクロールしてバージョンディレクトリを確認します。</span><span class="sxs-lookup"><span data-stu-id="ea799-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="ea799-169">バージョンディレクトリが1.1.4322 の場合、アプリケーションは .NET Framework 1.1 にマップされます。</span><span class="sxs-lookup"><span data-stu-id="ea799-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="ea799-170">反対に、バージョンディレクトリが v v1.0.3705 の場合、アプリケーションは .NET Framework 1.0 にマップされます。</span><span class="sxs-lookup"><span data-stu-id="ea799-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
