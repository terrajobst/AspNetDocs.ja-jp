---
uid: web-pages/readme/overview
title: WebMatrix の Readme |Microsoft Docs
author: rick-anderson
description: WebMatrix および ASP.NET Web Pages (Razor) 1.0 リリースの Readme
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454270"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="79b47-103">WebMatrix Readme</span><span class="sxs-lookup"><span data-stu-id="79b47-103">WebMatrix Readme</span></span>

<span data-ttu-id="79b47-104">2011年1月13日</span><span class="sxs-lookup"><span data-stu-id="79b47-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="79b47-105">内容</span><span class="sxs-lookup"><span data-stu-id="79b47-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="79b47-106">この readme は、WebMatrix の1.0 リリースに適用されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="79b47-107">概要</span><span class="sxs-lookup"><span data-stu-id="79b47-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="79b47-108">インストール</span><span class="sxs-lookup"><span data-stu-id="79b47-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="79b47-109">アプリケーションを発行する方法</span><span class="sxs-lookup"><span data-stu-id="79b47-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="79b47-110">変更と懸案事項</span><span class="sxs-lookup"><span data-stu-id="79b47-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="79b47-111">WebMatrix 1.0 のインストール</span><span class="sxs-lookup"><span data-stu-id="79b47-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="79b47-112">ASP.NET Web ページ</span><span class="sxs-lookup"><span data-stu-id="79b47-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="79b47-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="79b47-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="79b47-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="79b47-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="79b47-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="79b47-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="79b47-116">アプリケーションのインストール</span><span class="sxs-lookup"><span data-stu-id="79b47-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="79b47-117">アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="79b47-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="79b47-118">参照項目</span><span class="sxs-lookup"><span data-stu-id="79b47-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="79b47-119">概要</span><span class="sxs-lookup"><span data-stu-id="79b47-119">Overview</span></span>

> <span data-ttu-id="79b47-120">WebMatrix は、わずか数分でインストール可能な無償の Web 開発ツールです。</span><span class="sxs-lookup"><span data-stu-id="79b47-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="79b47-121">データベースとプログラミングのフレームワークに Web サーバーを組み合わせることによって、1 つの統合的な環境を実現します。</span><span class="sxs-lookup"><span data-stu-id="79b47-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="79b47-122">WebMatrix では、独自の ASP.NET または PHP Web サイトを効率よくコーディング、テスト、発行することができるほか、広く普及しているオープン ソース アプリケーション (DotNetNuke、Umbraco、WordPress、Joomla など) をベースにして、新しい Web サイトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="79b47-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="79b47-123">WebMatrix には、インターネット上で Web サイトを実行するものと同じ強力な Web サーバー、データベース エンジン、フレームワークが使用されているため、開発環境から実稼働環境への円滑かつシームレスな移行が可能です。</span><span class="sxs-lookup"><span data-stu-id="79b47-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="79b47-124">インストール</span><span class="sxs-lookup"><span data-stu-id="79b47-124">Installation</span></span>

> <span data-ttu-id="79b47-125">WebMatrix 1.0 をインストールするには、最初に[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="79b47-126">まず Web Platform Installer のインストールし、それを使用して WebMatrix をインストールすることになります。</span><span class="sxs-lookup"><span data-stu-id="79b47-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="79b47-127">インストール中に問題が発生した場合は、「 [Microsoft Web Platform Installer に関する問題のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=196212)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="79b47-128">アプリケーションの発行方法</span><span class="sxs-lookup"><span data-stu-id="79b47-128">How to Publish Applications</span></span>

> <span data-ttu-id="79b47-129">[アプリケーションを公開するための詳細な手順を確認する](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="79b47-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="79b47-130">変更点と問題</span><span class="sxs-lookup"><span data-stu-id="79b47-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="79b47-131">WebMatrix 1.0 のインストールの問題</span><span class="sxs-lookup"><span data-stu-id="79b47-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="79b47-132">問題: Microsoft .NET Framework 4 をサポートするプラットフォームでしか WebMatrix 1.0 は使用できない</span><span class="sxs-lookup"><span data-stu-id="79b47-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="79b47-133">WebMatrix には .NET Framework Version 4 が必須です。</span><span class="sxs-lookup"><span data-stu-id="79b47-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="79b47-134">特定の条件が揃うと、サポートされたプラットフォーム構成でないにもかかわらず、WebMatrix 1.0 インストーラーが先に進む場合があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="79b47-135">たとえば、SP1 更新プログラムが適用されていない Windows Vista では、WebMatrix のインストールが正常に開始されますが、.NET Framework 4 コンポーネントでエラーが発生し、インストールはブロックされます。</span><span class="sxs-lookup"><span data-stu-id="79b47-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="79b47-136">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-136">**Workaround**</span></span>  
> <span data-ttu-id="79b47-137">サポートされているプラットフォームにインストールします。サポート対象のプラットフォームは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="79b47-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="79b47-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="79b47-138">Windows 7</span></span>
> - <span data-ttu-id="79b47-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="79b47-139">Windows Server 2008</span></span>
> - <span data-ttu-id="79b47-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="79b47-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="79b47-141">Windows Vista SP1 以降</span><span class="sxs-lookup"><span data-stu-id="79b47-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="79b47-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="79b47-142">Windows XP SP3</span></span>
> - <span data-ttu-id="79b47-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="79b47-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="79b47-144">問題: Microsoft Visual Studio 2008 が SP1 未適用の状態でインストールされていると WebMatrix 1.0 をインストールできない</span><span class="sxs-lookup"><span data-stu-id="79b47-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="79b47-145">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-145">**Workaround**</span></span>  
> <span data-ttu-id="79b47-146">Microsoft ダウンロードセンターから[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="79b47-147">問題: SQL Server Compact 4.0 のアセンブリの一部が GAC にインストールされない</span><span class="sxs-lookup"><span data-stu-id="79b47-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="79b47-148">SQL Server Compact 4.0 を 64 ビット コンピューターにインストールする際、そのコンピューターに .NET Framework 3.5 SP1 Client Profile しかインストールされていないと、SQL Server Compact 4.0 のマネージド アセンブリがグローバル アセンブリ キャッシュ (GAC) に配置されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="79b47-149">GAC にインストールされないマネージド アセンブリは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="79b47-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="79b47-150">*System.data.sqlserverce* (ADO.NET provider) (システムプロバイダー)</span><span class="sxs-lookup"><span data-stu-id="79b47-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="79b47-151">*System.data.sqlserverce* (ADO.NET) (Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="79b47-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="79b47-152">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-152">**Workaround**</span></span>  
> <span data-ttu-id="79b47-153">SQL Server Compact 4.0 をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="79b47-154">次の場所から完全バージョンの .NET Framework 3.5 SP1 をダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="79b47-155">Microsoft .NET Framework 3.5 Service pack 1 (フルパッケージ)</span><span class="sxs-lookup"><span data-stu-id="79b47-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="79b47-156">そのうえで SQL Server Compact 4.0 を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="79b47-157">問題: コマンド ラインを使用して SQL Server Compact をアンインストールすることはできない</span><span class="sxs-lookup"><span data-stu-id="79b47-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="79b47-158">このリリースでは、コマンド ライン オプションを使用して SQL Server Compact をアンインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="79b47-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="79b47-159">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-159">**Workaround**</span></span>  
> <span data-ttu-id="79b47-160">Windows のコントロールパネルの [*プログラムと機能*] を使用して、Microsoft SQL Server Compact 4.0 をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="79b47-161">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="79b47-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="79b47-162">ここでは、Razor 構文を使用した ASP.NET Web Pages 1.0 リリースの新機能、変更点、および既知の問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="79b47-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="79b47-163">新機能</span><span class="sxs-lookup"><span data-stu-id="79b47-163">New features</span></span>](#NewFeatures)
- <span data-ttu-id="79b47-164">[[変更点]](#Changes)</span><span class="sxs-lookup"><span data-stu-id="79b47-164">[Changes](#Changes)</span></span>
- [<span data-ttu-id="79b47-165">問題</span><span class="sxs-lookup"><span data-stu-id="79b47-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a><span data-ttu-id="79b47-166">新機能</span><span class="sxs-lookup"><span data-stu-id="79b47-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="79b47-167">新機能: パッケージ マネージャーを無効にするための構成設定を追加</span><span class="sxs-lookup"><span data-stu-id="79b47-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="79b47-168">*Web.config ファイルの*`<appSettings>` 要素に新しい `asp:AdminManagerEnabled` キーを使用できます。これにより、パッケージマネージャーを完全に無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="79b47-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="79b47-169">この要素の既定値は true です。これは、 *web.config ファイルに*含まれていない場合、パッケージマネージャーが有効になっていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="79b47-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="79b47-170">パッケージマネージャーを無効にするには、 *web*サイトのルートにある web.config ファイルに次の要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="79b47-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a><span data-ttu-id="79b47-171">変化</span><span class="sxs-lookup"><span data-stu-id="79b47-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="79b47-172">変更点: "webPages:AdminFolderVirtualPath" キーの名前を "asp:AdminFolderVirtualPath" に変更</span><span class="sxs-lookup"><span data-stu-id="79b47-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="79b47-173">パッケージマネージャーの場所を指定するために*web.config ファイルに*追加できる `webPages:AdminFolderVirtualPath` キーは、`webPages` 名前空間ではなく `asp:` 名前空間を使用するように名前が変更されました。</span><span class="sxs-lookup"><span data-stu-id="79b47-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="79b47-174">この要素を使用している場合は、構成ファイルで名前を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a> <span data-ttu-id="79b47-175">既知の問題</span><span class="sxs-lookup"><span data-stu-id="79b47-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="79b47-176">問題: メンバーシップ ユーザーのパスワードが認識されなくなった</span><span class="sxs-lookup"><span data-stu-id="79b47-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="79b47-177">セキュリティを強化するため、メンバーシップ (ログイン) パスワードの作成と保存のアルゴリズムが変更されました。</span><span class="sxs-lookup"><span data-stu-id="79b47-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="79b47-178">その結果、ASP.NET Razor のベータ版で作成されたメンバー (ユーザー) 用に保存されたパスワードは認識されなくなります。</span><span class="sxs-lookup"><span data-stu-id="79b47-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="79b47-179">**回避策**サイトがまだ運用環境に配置されていない場合は、メンバーシップデータベースからユーザーレコードを削除します。</span><span class="sxs-lookup"><span data-stu-id="79b47-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="79b47-180">データベースが有効な場合は、プログラムによってメンバーシップデータベース内の既存のパスワードを再生成します。</span><span class="sxs-lookup"><span data-stu-id="79b47-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="79b47-181">問題: メンバーシップ用のカスタム ユーザー テーブルを使用しているときに予期しない動作が生じる</span><span class="sxs-lookup"><span data-stu-id="79b47-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="79b47-182">ASP.NET Razor web サイトのメンバーシッププロバイダーを初期化するには、`WebSecurity.InitializeDatabaseConnection` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="79b47-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="79b47-183">(WebMatrix では、スターターサイトテンプレートには、 *\_該当*ファイルにこのメソッドの呼び出しが含まれています)。このメソッドの `autoCreateTables` パラメーターが true に設定されている場合 (既定では、スタートサイトテンプレートで true に設定されています)、認識できないテーブル名がメソッドに渡された場合 (2 番目のパラメーター)、メソッドはエラーをスローしません。</span><span class="sxs-lookup"><span data-stu-id="79b47-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="79b47-184">エラーがスローされずに、自動的にテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="79b47-185">メンバーシップにカスタムユーザーテーブルを使用するが、間違ったテーブル名を `WebSecurity.InitializeDatabaseConnection` メソッドに渡す場合は、この問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="79b47-186">指定したテーブルが存在しなかったとしても、既定ではメソッドからエラーが生成されません。新しいテーブルが作成されるため、アプリケーションは一見、正常に機能しているように見えます。</span><span class="sxs-lookup"><span data-stu-id="79b47-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="79b47-187">しかし、最終的には、カスタム ユーザー テーブル (とそのテーブル内のフィールド) に依存しているアプリケーション コードで予期しないエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="79b47-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="79b47-188">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-188">**Workaround**</span></span>  
> <span data-ttu-id="79b47-189">`InitializeDatabaseConnection` メソッドで渡された名前がメンバーシップデータベースのユーザープロファイルテーブルと一致していることを確認するか、`autoCreateTables` パラメーターが false に設定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a><span data-ttu-id="79b47-190">問題: "管理者モジュールは、~/アプリの\_データへのアクセスが必要です" というエラーメッセージが表示される</span><span class="sxs-lookup"><span data-stu-id="79b47-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="79b47-191">状況によっては、ユーザーを作成しようとしたり、ASP.NET メンバーシップシステムを使用しようとしたりすると、ページには、*管理モジュールからアプリケーション\_データへのアクセスが必要に*なるというエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="79b47-192">これは、IIS または IIS Express が実行されているアカウントに、web サイトのルートにある*アプリ\_Data*フォルダーに対して作成および書き込みを行うためのアクセス許可がない場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="79b47-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="79b47-193">**回避策**Web サイトの*アプリ\_データ*フォルダーを手動で作成します。</span><span class="sxs-lookup"><span data-stu-id="79b47-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="79b47-194">次に、アプリケーションを実行する Windows アカウント (通常は NETWORK SERVICE) に、アプリケーションのルートフォルダーと、アプリの\_データなどのサブフォルダーに対する読み取り/書き込みアクセス許可が付与されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="79b47-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="79b47-195">詳細については、サポート技術情報の記事「 [SQL Server Express ユーザーインスタンスと ASP.net Web アプリケーションプロジェクトに関する問題](https://support.microsoft.com/kb/2002980)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="79b47-196">問題: "SQL Server のユーザー インスタンスを生成できませんでした" というエラーが表示される</span><span class="sxs-lookup"><span data-stu-id="79b47-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="79b47-197">WebMatrix Web アプリケーションに SQL Server Express が使用されており、Windows 7 または Windows Server 2008 R2 で IIS 7.5 が実行されている場合、ユーザーのローカル アプリケーション パスを SQL Server が実行時に取得できないことを示すエラーが表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="79b47-198">**回避策**アプリケーションが実行されている Windows アカウント (通常は NETWORK SERVICE) に、アプリケーションのルートフォルダーと、*アプリの\_データ*などのサブフォルダーに対する読み取り/書き込みアクセス許可があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="79b47-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="79b47-199">詳細については、サポート技術情報の記事「 [SQL Server Express ユーザーインスタンスと ASP.net Web アプリケーションプロジェクトに関する問題](https://support.microsoft.com/kb/2002980)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="79b47-200">問題: IIS 6.0 以前の環境でパッケージ マネージャーのリソースまたはパスワードを含んだファイルが返される</span><span class="sxs-lookup"><span data-stu-id="79b47-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="79b47-201">RC2 リリースを使用してビルドされた ASP.NET Web ページ (Razor) アプリケーションを配置する場合、アプリケーションの packagesources に、 */App\_Data/admin*の下に*パスワード .txt*またはファイルが含まれていると、IIS 6.0 は要求された場合にファイルを提供し、パッケージマネージャーインスタンスのパスワードを公開する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="79b47-202">\**回避策\*\*\*パスワード .txt*または*packagesources*ファイルの名前を packagesources または*に変更*します。既定では、IIS 6.0 は *.config*拡張子を持つファイルを提供しません。</span><span class="sxs-lookup"><span data-stu-id="79b47-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="79b47-203">(IIS 7 では、 *App\_Data*フォルダー内のファイルは提供されないため、ファイルの名前を変更する必要はありません)。</span><span class="sxs-lookup"><span data-stu-id="79b47-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="79b47-204">問題: Beta 3 リリースを使用してインストールしたパッケージをアンインストールしても、パッケージのコンポーネントが完全には削除されない</span><span class="sxs-lookup"><span data-stu-id="79b47-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="79b47-205">Beta 3 リリースのパッケージ マネージャーを使用してインストールされたパッケージを、現在のリリースを使用してアンインストールしようとすると、完全にはパッケージがアンインストールされません。</span><span class="sxs-lookup"><span data-stu-id="79b47-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="79b47-206">パッケージマネージャーの **[アンインストール]** ボタンを使用すると、一部のコンポーネントが削除されますが、パッケージのライブラリコードは残され、*パッケージの .config*ファイルは更新されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="79b47-207">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-207">**Workaround** </span></span>  
> <span data-ttu-id="79b47-208">次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="79b47-209">*アプリ\_Data\packages*フォルダーを削除します。</span><span class="sxs-lookup"><span data-stu-id="79b47-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="79b47-210">これにより、すべてのパッケージが削除されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="79b47-211">Web サイトのルートにある*パッケージの .config*ファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="79b47-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="79b47-212">問題: Visual Studio で Web ベースのパッケージ マネージャーを呼び出すとアプリケーションがオフラインになる</span><span class="sxs-lookup"><span data-stu-id="79b47-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="79b47-213">(WebMatrix ではなく) Visual Studio で作業していて、 *\_管理*機能を使用してパッケージマネージャーを起動している場合、visual studio はアプリケーションをオフラインにし、web サイトルートに*アプリ\_* を送信します。これにより、パッケージマネージャーを使用する機能が中断されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="79b47-214">ほとんどの場合、web ベースのパッケージマネージャーインターフェイスを使用しているときにこの動作が表示されますが、 *App\_Data*フォルダー内のファイルを追加、削除、または変更すると、同じ動作が発生します。</span><span class="sxs-lookup"><span data-stu-id="79b47-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="79b47-215">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-215">**Workaround** </span></span>  
> <span data-ttu-id="79b47-216">Visual Studio でパッケージを扱う場合は、Web ベースのパッケージ マネージャーではなく、NuGet 拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="79b47-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="79b47-217">詳細については、 [NuGet のドキュメント](https://docs.microsoft.com/nuget/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="79b47-218">*App\_Data*フォルダー内の他のファイルを操作する場合は、この問題を回避するためにファイルを他の場所に保持することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="79b47-219">これが現実的でない場合は、*アプリ\_オフライン .htm*ファイルを手動で削除するか、サイトが自動的にオンラインに戻るまで待機します (既定では30秒後)。</span><span class="sxs-lookup"><span data-stu-id="79b47-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="79b47-220">問題: Visual Studio IntelliSense およびプロジェクト テンプレートは ASP.NET MVC Version 3 でしか利用できない</span><span class="sxs-lookup"><span data-stu-id="79b47-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="79b47-221">ASP.NET Web Pages をインストールしても Visual Studio 用のツール (ASP.NET Web Pages アプリケーション用のプロジェクト テンプレート、IntelliSense など) はインストールされません。</span><span class="sxs-lookup"><span data-stu-id="79b47-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="79b47-222">**回避策**Visual Studio で ASP.NET Web ページアプリケーションの IntelliSense とプロジェクトテンプレートを使用するには、Web Platform Installer または[スタンドアロンインストーラー](https://go.microsoft.com/fwlink/?LinkID=191797)を使用して ASP.NET MVC 3 RC をインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="79b47-223">問題: フィードなどの外部データをプロキシ サーバーから読み取る</span><span class="sxs-lookup"><span data-stu-id="79b47-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="79b47-224">サイトを実行しているサーバーがプロキシサーバーの背後にある場合は、サイトの外部からの情報を読み取ることができるよう*に、web.config ファイルに*プロキシ情報を構成することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="79b47-225">たとえば、`ReCaptcha` ヘルパーを使用する場合、ヘルパーは reCAPTCHA サービスと通信しますが、プロキシサーバーによってブロックされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="79b47-226">同様に、ASP.NET Web Pages で使用されているフィード (パッケージ マネージャーによって使用されているフィードなど) にもプロキシ構成が必要となることがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="79b47-227">外部サービスの操作中またはパッケージフィードの操作で問題が発生した場合は、アプリケーションのルート*web.config*ファイルに次の要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="79b47-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="79b47-228">プロキシサーバーの構成の詳細については、MSDN Web サイトの「 [&lt;proxy&gt; 要素 (ネットワーク設定)](https://msdn.microsoft.com/library/sa91de1e.aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="79b47-229">問題: .NET Framework  Version 4 をアンインストールすると Razor 構文を使用する ASP.NET Web Pages が無効になる</span><span class="sxs-lookup"><span data-stu-id="79b47-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="79b47-230">.NET Framework  Version 4 をアンインストールして再インストールした場合、Razor 構文を使用する ASP.NET Web Pages は無効になります。</span><span class="sxs-lookup"><span data-stu-id="79b47-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="79b47-231">拡張子が*cshtml*のページは正しく動作しません。</span><span class="sxs-lookup"><span data-stu-id="79b47-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="79b47-232">ASP.NET Web ページは、アセンブリをコンピューターのルート*web.config*ファイルに登録し、.NET Framework を削除するとそのファイルが削除されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="79b47-233">.NET Framework を再インストールすると、新しいバージョンの構成ファイルがインストールされますが、ASP.NET Web Pages アセンブリに対する参照は追加されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="79b47-234">**回避策**.NET Framework を再インストールした後、Razor 構文で ASP.NET Web ページを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="79b47-235">これにより、コンピュータールートの*web.config ファイルに*次の要素が追加されます。通常は次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="79b47-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="79b47-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="79b47-237">IIS 7 または IIS 7.5 では、次のような URL の要求は、拡張子が*cshtml*または*vbhtml*のページを見つけることができません。</span><span class="sxs-lookup"><span data-stu-id="79b47-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="79b47-238">IIS 7 または IIS 7.5 では URL の書き換えが既定で有効になっていないため、この問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="79b47-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="79b47-239">Likeliest シナリオでは、IIS Express を使用してローカルでテストするときに問題が発生することはありませんが、web サイトをホストする web サイトにデプロイするときにこの問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="79b47-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="79b47-240">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="79b47-241">サーバーコンピューターを制御している場合は、サーバーコンピューターで、更新プログラムに記載されている更新プログラムをインストールします。この更新プログラムは[、特定の iis 7.0 または iis 7.5 ハンドラーが、url の末尾がピリオドではない要求を処理](https://support.microsoft.com/kb/980368)できるようにします。</span><span class="sxs-lookup"><span data-stu-id="79b47-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="79b47-242">サーバーコンピューターを制御できない場合は (たとえば、ホスティング web サイトに配置する場合)、 *web*サイトの web.config ファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="79b47-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="79b47-243">問題: SQL Server Compact がインストールされていないコンピューターにアプリケーションを展開する</span><span class="sxs-lookup"><span data-stu-id="79b47-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="79b47-244">SQL Server Compact データベースを含むアプリケーションは、SQL Server Compact がインストールされていないコンピューターで実行できます。</span><span class="sxs-lookup"><span data-stu-id="79b47-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="79b47-245">Microsoft WebMatrix 1.0 は、これらのバイナリを自動的にコピーし *、適切な web.config ファイル*変換を実行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="79b47-246">**回避策**これらのファイルをコピーし*て、web.config ファイルを*手動で変更する必要がある場合は、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="79b47-247">データベースエンジンアセンブリを、ターゲットコンピューター上のアプリケーションの*Bin*フォルダー (およびサブフォルダー) にコピーします。</span><span class="sxs-lookup"><span data-stu-id="79b47-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="79b47-248">*SQL Server C:\Program Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*をコピー </span><span class="sxs-lookup"><span data-stu-id="79b47-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="79b47-249">**to** *\bin*</span><span class="sxs-lookup"><span data-stu-id="79b47-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="79b47-250">*SQL Server Compact C:\Program Edition\v4.0\Private\x86\\* **を** *\Bin\x86*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="79b47-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="79b47-251">*SQL Server Compact C:\Program Edition\v4.0\Private\amd64\\* \* を \Bin\amd64**にコピーし**ます。</span><span class="sxs-lookup"><span data-stu-id="79b47-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="79b47-252">*Web*サイトのルートフォルダーで、web.config ファイルを作成するか、開きます。</span><span class="sxs-lookup"><span data-stu-id="79b47-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="79b47-253">(WebMatrix 1.0 では、 **[ファイルの種類の選択]** ダイアログボックスで **[すべて]** をクリックすると、このファイルの種類が使用可能になります)。</span><span class="sxs-lookup"><span data-stu-id="79b47-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="79b47-254">次の要素を `<configuration>` 要素の子として追加します (`<system.web>` 要素内ではありません)。</span><span class="sxs-lookup"><span data-stu-id="79b47-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="79b47-255">問題点: "Database" および "WebGrid" のヘルパーは、Visual Basic の中程度の信頼では機能しません</span><span class="sxs-lookup"><span data-stu-id="79b47-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="79b47-256">Visual Basic ( *vbhtml*ファイルの作成) を使用している場合、アプリケーションが中程度の信頼を使用するように設定されていると、`Database` と `WebGrid` のヘルパーは機能しません。</span><span class="sxs-lookup"><span data-stu-id="79b47-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="79b47-257">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-257">**Workaround**</span></span>  
> <span data-ttu-id="79b47-258">Visual Studio 2010 を使用している場合は、Service Pack 1 のリリースをインストールすることで、この問題を解決できます。</span><span class="sxs-lookup"><span data-stu-id="79b47-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="79b47-259">SP1 リリースの最終版が利用可能になるまでは、Microsoft ダウンロードセンターの[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en)のページからベータ版の sp1 をダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="79b47-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="79b47-260">これが現実的でない場合、または Visual Studio 2010 を使用していない場合は、アプリケーションを一時的に完全信頼を使用するように設定できます。</span><span class="sxs-lookup"><span data-stu-id="79b47-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="79b47-261">問題: "ApplicationPart" リソースに外部からアクセスできる</span><span class="sxs-lookup"><span data-stu-id="79b47-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="79b47-262">アセンブリに `ApplicationPart` クラスから派生したオブジェクトが含まれている場合、そのアセンブリのリソースは `ResourceRouteHandler` クラスによって公開されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="79b47-263">たとえば、次のような URL があるとします。</span><span class="sxs-lookup"><span data-stu-id="79b47-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="79b47-264">この要求は、すべてのリソース文字列を*system.web. Web ページの管理*アセンブリにダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="79b47-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="79b47-265">すべての埋め込みリソース (静的コンテンツとして提供される予定ではないものも含む) がダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="79b47-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="79b47-266">埋め込みリソースに機密情報が含まれている場合は、セキュリティ上のリスクが生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="79b47-267">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-267">**Workaround** </span></span>  
> <span data-ttu-id="79b47-268">**Applicationpart**オブジェクトを作成する場合は、その**applicationpart**オブジェクトのアセンブリに関連付けられている埋め込みリソースに機密情報が含まれていないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="79b47-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="79b47-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="79b47-270">WebMatrix のインストールに関する問題の詳細については、このドキュメントの「 [webmatrix のインストールに関する問題](#Known_Issues_Installation)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="79b47-271">ドキュメントのこのセクションでは、WebMatrix 開発環境に関する既知の問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="79b47-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="79b47-272">問題点: web.config ファイルのデータベース接続文字列のユーザー名またはパスワードの変更は、[データベース] ワークスペースに反映されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="79b47-273">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="79b47-274">*Web.config ファイルで*、接続文字列のデータベース名を変更します (たとえば、"1" を追加します)。</span><span class="sxs-lookup"><span data-stu-id="79b47-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="79b47-275">*Web.config ファイルを*保存します。</span><span class="sxs-lookup"><span data-stu-id="79b47-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="79b47-276">[**データベース**と更新] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="79b47-277">*Web.config*ファイルの接続文字列でデータベース名を元のデータベース名に変更します。</span><span class="sxs-lookup"><span data-stu-id="79b47-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="79b47-278">*Web.config ファイルを*保存します。</span><span class="sxs-lookup"><span data-stu-id="79b47-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="79b47-279">[**データベース**と更新] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="79b47-280">問題: WebMatrix によって作成されたフォルダーを削除することはできません</span><span class="sxs-lookup"><span data-stu-id="79b47-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="79b47-281">高度なアクセス許可を使用して WebMatrix が実行されている場合 (つまり、Windows の **[管理者として実行]** オプションを使用して webmatrix を開始した場合)、webmatrix によって作成されたフォルダーをエクスプローラーを使用して削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="79b47-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="79b47-282">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-282">**Workaround**</span></span>  
> <span data-ttu-id="79b47-283">昇格されたアクセス許可を使用してエクスプローラーを実行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="79b47-284">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="79b47-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="79b47-285">Windows で、 **[開始]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="79b47-286">「Windows Explorer」と入力し、**エクスプローラー**のエントリを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="79b47-287">**[管理者として実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="79b47-288">その後、フォルダーを削除できます。</span><span class="sxs-lookup"><span data-stu-id="79b47-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="79b47-289">問題: WebMatrix 1.0 は、昇格が必要な特定のタスクを実行できない</span><span class="sxs-lookup"><span data-stu-id="79b47-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="79b47-290">WebMatrix 1.0 は、次の状況での追加コンポーネントのインストールなど、昇格が必要な特定のタスクを実行できません。</span><span class="sxs-lookup"><span data-stu-id="79b47-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="79b47-291">Windows Vista または Windows 7 では、管理者特権を持たないアカウントを使用してログインし、ユーザーアカウント制御 (UAC) が無効になっています。</span><span class="sxs-lookup"><span data-stu-id="79b47-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="79b47-292">Microsoft Windows XP または Microsoft Windows Server 2003 を使用している。</span><span class="sxs-lookup"><span data-stu-id="79b47-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="79b47-293">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-293">**Workaround**</span></span>  
> <span data-ttu-id="79b47-294">WebMatrix 1.0 のほとんどのタスクには、管理者権限は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="79b47-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="79b47-295">そのためには、管理者として操作を実行するか、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="79b47-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="79b47-296">Windows Vista または Windows 7 では、UAC を有効にします。</span><span class="sxs-lookup"><span data-stu-id="79b47-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="79b47-297">Windows XP では、ユーザーを管理者セキュリティグループに追加します。</span><span class="sxs-lookup"><span data-stu-id="79b47-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="79b47-298">問題: "Web ギャラリーからのサイト" が無効になっています</span><span class="sxs-lookup"><span data-stu-id="79b47-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="79b47-299">Web Platform Installer 3.0 がインストールされていない場合、 **[Web ギャラリーからのサイト]** オプションは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="79b47-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="79b47-300">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-300">**Workaround**</span></span>  
> <span data-ttu-id="79b47-301">[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="79b47-302">問題: Google Chrome は Run オプションとして使用できません</span><span class="sxs-lookup"><span data-stu-id="79b47-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="79b47-303">Google Chrome は、 **[ホーム]** タブの **[実行]** にあるブラウザーの一覧に表示されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="79b47-304">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-304">**Workaround**</span></span>  
> <span data-ttu-id="79b47-305">Google Chrome の一部のバージョンは、Windows の既定のプログラム機能に正しく登録されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="79b47-306">回避策として、Google Chrome を起動し、[ *Google chrome* ] メニューをクリックして、[*オプション*] をクリックし、[ *google chrome の既定のブラウザーを作成*する] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="79b47-307">問題点: [外部キー] ダイアログボックスで主キーを入力できない</span><span class="sxs-lookup"><span data-stu-id="79b47-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="79b47-308">**[外部キー]** ダイアログボックスでは、主キーテーブルの主キーの名前を入力することはできません。</span><span class="sxs-lookup"><span data-stu-id="79b47-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="79b47-309">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-309">**Workaround**</span></span>  
> <span data-ttu-id="79b47-310">これは意図的なものであり、</span><span class="sxs-lookup"><span data-stu-id="79b47-310">This is intentional.</span></span> <span data-ttu-id="79b47-311">主キーテーブルの主キーの名前を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="79b47-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="79b47-312">問題: Razor 構文、、またはの WebMatrix ではC#、IntelliSense を使用できません Visual Basic</span><span class="sxs-lookup"><span data-stu-id="79b47-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="79b47-313">HTML および CSS では、IntelliSense が WebMatrix でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="79b47-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="79b47-314">ただし、他の言語では使用できません。</span><span class="sxs-lookup"><span data-stu-id="79b47-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="79b47-315">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-315">**Workaround** </span></span>  
> <span data-ttu-id="79b47-316">[なし] :</span><span class="sxs-lookup"><span data-stu-id="79b47-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="79b47-317">問題点: HTML および CSS 用の IntelliSense は、文脈に適していない要素を提案します。</span><span class="sxs-lookup"><span data-stu-id="79b47-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="79b47-318">WebMatrix のマークアップ用の IntelliSense では、 [css 2.1 スキーマ](http://www.w3.org/TR/CSS2/)を使用した[XHTML 1.0 移行スキーマ](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)と css を使用した HTML がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="79b47-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="79b47-319">IntelliSense はこれらの特定のスキーマに基づいているため、特定のタグ、属性、またはプロパティが、現在のページまたはスタイル定義に適していない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="79b47-320">HTML の場合は、不適切な形式の XHTML として解釈される可能性があるコンテンツ (タグが閉じられていない場合など) に予期しない候補が表示されることもあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="79b47-321">挿入ポイントが不完全なタグ内にある場合、この問題はさらに顕著になる可能性があります。その場合は、IntelliSense によって新しい開始タグが提示されるか、またはその他の不適切な候補が提示されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="79b47-322">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-322">**Workaround** </span></span>  
> <span data-ttu-id="79b47-323">HTML の場合は、整形式の完全な XHTML ページ内で作業していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="79b47-324">CSS の場合、回避策はありません。</span><span class="sxs-lookup"><span data-stu-id="79b47-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="79b47-325">問題: 入力中に IntelliSense が呼び出されない</span><span class="sxs-lookup"><span data-stu-id="79b47-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="79b47-326">場合によっては、エディターに HTML または CSS が入力されているときに IntelliSense が呼び出されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="79b47-327">特に、挿入ポイントが別の要素の横、またはファイルの末尾にある場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="79b47-328">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-328">**Workaround** </span></span>  
> <span data-ttu-id="79b47-329">挿入ポイントの周囲に空白があること、および挿入ポイントがファイルの末尾にないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="79b47-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="79b47-330">Ctrl キーを押しながら Space キーを押すと、IntelliSense を手動で呼び出すこともできます。</span><span class="sxs-lookup"><span data-stu-id="79b47-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="79b47-331">問題: IntelliSense を無効にするための UI が使用できない</span><span class="sxs-lookup"><span data-stu-id="79b47-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="79b47-332">WebMatrix 1.0 では、IntelliSense を無効にするための UI やジェスチャは提供されません。</span><span class="sxs-lookup"><span data-stu-id="79b47-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="79b47-333">**回避策** </span><span class="sxs-lookup"><span data-stu-id="79b47-333">**Workaround** </span></span>  
> <span data-ttu-id="79b47-334">次のコマンドを使用して WebMatrix を開始します。これには、IntelliSense を無効にするスイッチが含まれています。</span><span class="sxs-lookup"><span data-stu-id="79b47-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="79b47-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="79b47-335">IIS Express</span></span>

<span data-ttu-id="79b47-336">IIS Express には、次の URL から入手できる独自の readme ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="79b47-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x411</span><span class="sxs-lookup"><span data-stu-id="79b47-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="79b47-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="79b47-338">SQL Server Compact</span></span>

<span data-ttu-id="79b47-339">SQL Server Compact には、次の URL から入手できる独自の readme ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="79b47-340">WebMatrix の一部として SQL Server Compact をインストールする場合の問題の詳細については、このドキュメントの「 [webmatrix のインストールに関する問題](#Known_Issues_Installation)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a><span data-ttu-id="79b47-341">アプリケーションのインストール</span><span class="sxs-lookup"><span data-stu-id="79b47-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="79b47-342">問題: ユーザーの [マイドキュメント] フォルダーがネットワーク共有にリダイレクトされると、アプリケーションのインストールに時間がかかることがある</span><span class="sxs-lookup"><span data-stu-id="79b47-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="79b47-343">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-343">**Workaround**</span></span>  
> <span data-ttu-id="79b47-344">[なし] :</span><span class="sxs-lookup"><span data-stu-id="79b47-344">None.</span></span> <span data-ttu-id="79b47-345">アプリケーションのインストールには時間がかかる場合がありますが、正しくインストールされます。</span><span class="sxs-lookup"><span data-stu-id="79b47-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a><span data-ttu-id="79b47-346">アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="79b47-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="79b47-347">問題: SQL Compact データベースを公開すると、"必要なアクセス許可を取得できません" というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="79b47-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="79b47-348">WebMatrix では、中程度の信頼の構成で .NET Framework バージョン3.5 を実行しているサーバーに、SQL Server Compact のサポートバイナリを展開することは完全にサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="79b47-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="79b47-349">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-349">**Workaround**</span></span>  
> <span data-ttu-id="79b47-350">推奨される回避策は、サーバーに .NET Framework 4 をインストールすることです。</span><span class="sxs-lookup"><span data-stu-id="79b47-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="79b47-351">または、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="79b47-352">*Web\_MediumTrust*ファイルの `SecurityClasses` セクションに次の要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="79b47-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="79b47-353">次の必要なアクセス許可を使用して、 *Web\_MediumTrust*ファイルに新しいアクセス許可セットを作成します。</span><span class="sxs-lookup"><span data-stu-id="79b47-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="79b47-354">*Web\_MediumTrust*ファイルに次の要素を配置して、アクセス許可セットを SQL Server Compact に適用します。</span><span class="sxs-lookup"><span data-stu-id="79b47-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="79b47-355">問題: ギャラリーおよび PhpBB web アプリケーションで、発行後に "サービスを利用できません" というエラーが表示される</span><span class="sxs-lookup"><span data-stu-id="79b47-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="79b47-356">状況によっては、アプリケーションの発行によって "サービスを利用できません" というエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="79b47-357">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-357">**Workaround**</span></span>  
> <span data-ttu-id="79b47-358">WebMatrix で、 **[発行の設定]** ウィンドウでサーバー名の末尾に円記号 (\) を追加し、もう一度アプリケーションを発行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="79b47-359">問題: 発行後に Moodle web サイトのレイアウトとリンクが壊れている</span><span class="sxs-lookup"><span data-stu-id="79b47-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="79b47-360">Moodle アプリケーションを発行すると、アプリケーションが正常に動作しなくなります。</span><span class="sxs-lookup"><span data-stu-id="79b47-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="79b47-361">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-361">**Workaround**</span></span>  
> <span data-ttu-id="79b47-362">WebMatrix で、 **[発行の設定]** ウィンドウの **[サイト名]** フィールドの末尾にスラッシュ (/) を追加し、アプリケーションを再度発行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="79b47-363">問題: nopCommerce のパブリッシングがデータベースエラーで失敗する</span><span class="sxs-lookup"><span data-stu-id="79b47-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="79b47-364">NopCommerce の発行に失敗し、"nop\_ログテーブルに挿入できませんでした。" などのデータベースエラーが報告されます。</span><span class="sxs-lookup"><span data-stu-id="79b47-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="79b47-365">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="79b47-366">WebMatrix で、 **[実行]** をクリックして nopCommerce をローカルで起動します。</span><span class="sxs-lookup"><span data-stu-id="79b47-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="79b47-367">[管理] ページにログインします。</span><span class="sxs-lookup"><span data-stu-id="79b47-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="79b47-368">**[システム]** メニューをクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="79b47-369">**[ログ]** オプションをクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="79b47-370">**[ログの消去]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="79b47-371">NopCommerce をもう一度公開します。</span><span class="sxs-lookup"><span data-stu-id="79b47-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="79b47-372">問題: 発行されたサイトをダウンロードすると、Silverstripe CMS に "HTTP 500 PHP FCGI エラー" が表示される</span><span class="sxs-lookup"><span data-stu-id="79b47-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="79b47-373">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-373">**Workaround**</span></span>  
> <span data-ttu-id="79b47-374">[発行**済みサイトのダウンロード**] をクリックした後、**発行プレビュー**で `silverstripe-cache/manifest_main` をスキップします。</span><span class="sxs-lookup"><span data-stu-id="79b47-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="79b47-375">このファイルはキャッシュの目的で使用され、各コンピューターに固有です。</span><span class="sxs-lookup"><span data-stu-id="79b47-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="79b47-376">問題: 発行されたサイトをダウンロードすると、Subtext に "/' アプリケーションでのサーバーエラーが表示される</span><span class="sxs-lookup"><span data-stu-id="79b47-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="79b47-377">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-377">**Workaround**</span></span>  
> <span data-ttu-id="79b47-378">サイトの*web.config*ファイルを開き、データベース接続文字列のユーザー ID とパスワードを SQL Server 管理者の資格情報 ("sa" の資格情報) に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="79b47-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="79b47-379">または、次の手順に従って、ログインしているユーザーアカウントに `db_owner` アクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="79b47-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="79b47-380">Web Platform Installer を使用して SQL Server Management Studio をインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="79b47-381">ローカル SQL Server Express インスタンス (既定では `.\SQLEXPRESS`) に接続します。</span><span class="sxs-lookup"><span data-stu-id="79b47-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="79b47-382">[**データベース**&gt; *[Localsubtextdatabase]* をクリックし &gt;**セキュリティ**&gt; **Users** &gt; *[localsubtextdatabase*] (既定値は `subtextuser`]、右クリックして、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="79b47-383">[ロールメンバーシップ] セクションで [ **db\_所有者**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b47-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="79b47-384">問題: [宛先 URL] フィールドに http://または https://のプレフィックスが付いていないと、発行後にサイトが機能しない場合がある</span><span class="sxs-lookup"><span data-stu-id="79b47-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="79b47-385">**[発行の設定]** ダイアログボックスで、インストール先の URL が `http://` または `https://`で始まらない場合は、展開後にサイトが動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="79b47-386">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-386">**Workaround**</span></span>  
> <span data-ttu-id="79b47-387">サイトを発行する前に、 **[発行の設定]** ダイアログボックスの目的の URL が `http://` または `https://`で始まることを確認します。</span><span class="sxs-lookup"><span data-stu-id="79b47-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="79b47-388">問題点: MySQL データベースの公開が失敗し、"データベースをパブリッシュできませんでした。</span><span class="sxs-lookup"><span data-stu-id="79b47-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="79b47-389">これは、リモートデータベースがスクリプトを実行できない場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="79b47-390">このエラーは、さまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="79b47-391">このエラーが表示される理由の1つは、データベーススクリプトに単一引用符 (') が含まれていて、MySQL データベースの既定の文字セットが UTF-8 に設定されていない場合です。</span><span class="sxs-lookup"><span data-stu-id="79b47-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="79b47-392">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-392">**Workaround**</span></span>  
> <span data-ttu-id="79b47-393">リモート MySQL データベースの既定の文字セットを UTF-8 に設定します。</span><span class="sxs-lookup"><span data-stu-id="79b47-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="79b47-394">問題: サイトを公開またはダウンロードした後に、DotNetNuke に一部のリンクが表示されない</span><span class="sxs-lookup"><span data-stu-id="79b47-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="79b47-395">DotNetNuke サイトを発行またはダウンロードする場合は、キャッシュをクリアして、サイトに新しいリンクが表示されるようにすることが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="79b47-396">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="79b47-397">"Host" としてログインします。</span><span class="sxs-lookup"><span data-stu-id="79b47-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="79b47-398">ホスト メニューにアクセスし、**ホストの設定** を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b47-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="79b47-399">下にスクロールし、 **[詳細設定]** の **[パフォーマンスの設定]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="79b47-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="79b47-400">ページの **[キャッシュのクリア]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="79b47-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="79b47-401">ページの下部にアクセスし、アプリケーションを再起動します。</span><span class="sxs-lookup"><span data-stu-id="79b47-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="79b47-402">問題: 発行されたサイトをダウンロードした後、AtomSite の一部のリンクが壊れている</span><span class="sxs-lookup"><span data-stu-id="79b47-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="79b47-403">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-403">**Workaround**</span></span>  
> <span data-ttu-id="79b47-404">*App.config*ファイル、*ユーザー .config*ファイル、およびすべての *.xml*ファイルで、URL 文字列 (たとえば、`http://myhost.com/atomsite`) をローカルの文字列 (たとえば、`http://localhost:1239`) に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="79b47-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="79b47-405">問題: WordPress などの MySQL ベースのアプリケーションがデータベースエラーを発行して報告できない</span><span class="sxs-lookup"><span data-stu-id="79b47-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="79b47-406">既定では、WebMatrix は、UTF-8 文字セットを使用して MySQL をインストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="79b47-407">独自のに MySQL をインストールし、文字セットが UTF-8 ではない場合 (たとえば、Latin1)、データベースの発行プロセスが失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="79b47-408">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="79b47-409">MySQL の文字セットを UTF-8 に変更します。</span><span class="sxs-lookup"><span data-stu-id="79b47-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="79b47-410">(詳細については、MySQL の web サイトの「[サーバー文字セットと照合順序](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="79b47-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="79b47-411">アプリケーションを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="79b47-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="79b47-412">アプリケーションを再発行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="79b47-413">問題: ブラウザーベースのセットアップを実行しているアプリケーションで、"発行済みサイトのダウンロード" に失敗する</span><span class="sxs-lookup"><span data-stu-id="79b47-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="79b47-414">一部のアプリケーション (たとえば、Kentico CMS) では、データベースの作成などのインストール後のセットアップを実行するために、それらのアプリケーションをブラウザーで起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79b47-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="79b47-415">ブラウザーベースのセットアップを完了せずにこのようなアプリケーションを発行した場合、リモートサーバーから同じサイトをダウンロードしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="79b47-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="79b47-416">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-416">**Workaround**</span></span>  
> <span data-ttu-id="79b47-417">サイトを公開する前に、ブラウザーベースのセットアップを完了します。</span><span class="sxs-lookup"><span data-stu-id="79b47-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="79b47-418">問題: "公開されたサイトのダウンロード" が DotNetNuke および Kooboo CMS のデータベースエラーで失敗する</span><span class="sxs-lookup"><span data-stu-id="79b47-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="79b47-419">サーバーからアプリケーションをダウンロードしようとしたときに、 **[発行の設定]** ダイアログボックスのデータベース接続文字列に管理者の資格情報がある場合、発行ログに次のエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="79b47-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="79b47-420">**回避策**</span><span class="sxs-lookup"><span data-stu-id="79b47-420">**Workaround**</span></span>  
> <span data-ttu-id="79b47-421">実際には、データベースの管理者以外の資格情報を使用して、サイトを (または公開している) 再発行します。</span><span class="sxs-lookup"><span data-stu-id="79b47-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="79b47-422">詳細情報</span><span class="sxs-lookup"><span data-stu-id="79b47-422">For More Information</span></span>

<span data-ttu-id="79b47-423">WebMatrix 1.0 の詳細については、次の web サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="79b47-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="79b47-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="79b47-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="79b47-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="79b47-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="79b47-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="79b47-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="79b47-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="79b47-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="79b47-428">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="79b47-428">All Rights Reserved.</span></span> <span data-ttu-id="79b47-429">[使用条件](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="79b47-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
