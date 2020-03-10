---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 | の機能強化Microsoft Docs
author: microsoft
description: Visual Studio 2005 では、web アプリケーション開発者は、Web プロジェクトの機能強化と機能強化の長い一覧を提供しています。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464650"
---
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="06a0c-103">Visual Studio 2005 の機能強化</span><span class="sxs-lookup"><span data-stu-id="06a0c-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="06a0c-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="06a0c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="06a0c-105">Visual Studio 2005 では、web アプリケーション開発者は、Web プロジェクトの機能強化と機能強化の長い一覧を提供しています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="06a0c-106">Visual Studio 2005 では、web アプリケーション開発者は、Web プロジェクトの機能強化と機能強化の長い一覧を提供しています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="06a0c-107">Visual Studio .NET 2002 や2003のように、Web プロジェクトの処理方法には多くの不満がありました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="06a0c-108">Visual Studio 2005 では、このような苦情に対処するために、多くの新機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="06a0c-109">Visual Studio .NET 2003 で Web アプリケーションのコンパイルを処理する方法を好む方は、「 [Web アプリケーションプロジェクト](https://go.microsoft.com/fwlink/?LinkId=57870)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06a0c-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="06a0c-110">このモジュールでは、Web プロジェクトの作成、管理、および開発の機能強化について説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="06a0c-111">後のモジュールでは、Web プロジェクトのビルドと配置の機能強化についても説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="06a0c-112">FrontPage サーバー拡張</span><span class="sxs-lookup"><span data-stu-id="06a0c-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="06a0c-113">Web プロジェクトを作成またはビルドするには、Visual Studio .NET 2002 および2003が必要 FrontPage Server Extensions です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="06a0c-114">開発者は、2つの異なるアクセスモード (FrontPage Server Extensions またはファイルアクセスモード) のいずれかを選択でき、IIS でのアプリケーションルートの設定などのタスクを実行するために FrontPage Server Extensions 使用されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="06a0c-115">Visual Studio 2005 では、ローカルプロジェクトの FrontPage Server Extensions への依存が削除されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="06a0c-116">Visual Studio 2005 では、FrontPage Server Extensions を使用する代わりに、IIS メタベースに直接アクセスできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="06a0c-117">また、Visual Studio 2005 では、リモートプロジェクトへのアクセスを可能にする、FrontPage Server Extensions を必要としない FTP のサポートも追加されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="06a0c-118">プロジェクトで FrontPage Server Extensions を使用する開発者にとって、このオプションは引き続き使用できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="06a0c-119">しかし、ASP.NET 開発者コミュニティからの強いフィードバックに基づいて、必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-120">FrontPage Server Extensions は、リモートプロジェクトの作成や開くなどにも必要です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="06a0c-121">ASP.NET 開発サーバー</span><span class="sxs-lookup"><span data-stu-id="06a0c-121">ASP.NET Development Server</span></span>

<span data-ttu-id="06a0c-122">Visual Studio 2005 には、ASP.NET 開発サーバーという名前の新しい Web サーバーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="06a0c-123">(この Web サーバーは以前は Cassini と呼ばれていました)。</span><span class="sxs-lookup"><span data-stu-id="06a0c-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="06a0c-124">ASP.NET 開発サーバーにはいくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="06a0c-125">管理者以外の管理者が Web サーバーに対して開発およびデバッグを行うことができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="06a0c-126">ASP.NET 開発サーバーは、柔軟なプロジェクトの場所を実現するために、仮想ディレクトリをファイルシステム内の任意の場所に動的にマップします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="06a0c-127">既に IIS を使用している Windows XP Professional のユーザーは、IIS の既定の Web サイトのファイルまたはフォルダー構造に影響を与えない新しい Web アプリケーションを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="06a0c-128">ASP.NET 開発サーバーを利用するために特別な構成は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="06a0c-129">ファイルシステムでホストされている Web プロジェクトがデバッグまたは参照されると、Visual Studio 2005 は、要求を処理するために ASP.NET 開発サーバーのインスタンスをランダムポートで自動的に開始します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="06a0c-130">詳細については、このモジュールの後の ASP.NET 開発サーバーで説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="06a0c-131">強化されたファイル管理</span><span class="sxs-lookup"><span data-stu-id="06a0c-131">Improved File Management</span></span>

<span data-ttu-id="06a0c-132">Visual Studio 2002 および2003では、Web アプリケーション内のすべてのファイルについて、 C#プロジェクトファイル (VB.NET と .csproj の場合は .vbproj) が格納されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="06a0c-133">ソリューションエクスプローラー表示は、プロジェクトファイルのファイル情報に基づいています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="06a0c-134">このため、外部エディターが使用されている場合、ソリューションエクスプローラーによって、誤った情報が表示されることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="06a0c-135">Visual Studio 2002 および2003では、ファイルの変更が上書きされることや、最新バージョンのファイルが表示されないことがよくあります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="06a0c-136">Visual Studio 2005 では、プロジェクトファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="06a0c-137">代わりに、ファイルとフォルダーの情報をディスクから直接読み取ります。これにより、プロジェクト内のファイルが正確に表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="06a0c-138">Visual Studio 2002 および2003の References フォルダーは Web アプリケーションの実際のフォルダーを表していないため、Visual Studio 2005 ではソリューションエクスプローラーから References フォルダーも削除されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="06a0c-139">Visual Studio 2005 でプロジェクトの参照にアクセスするには、プロジェクトのプロパティページを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="06a0c-140">Web プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="06a0c-140">Creating Web Projects</span></span>

<span data-ttu-id="06a0c-141">Web 開発者には、Visual Studio 2005 でプロジェクトを作成するための多くの新しいオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="06a0c-142">Web サイトは、ファイルシステム内の任意の場所に作成できるようになりました。その後、新しい ASP.NET 開発サーバーを使用してデバッグまたは参照することができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="06a0c-143">開発者は、FTP を使用して新しい Web サイトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="06a0c-144">Visual Studio 2005 で Web プロジェクトを作成するためのビデオチュートリアルを表示するには、ここをクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="06a0c-145">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="06a0c-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="06a0c-146">ファイルシステムプロジェクト</span><span class="sxs-lookup"><span data-stu-id="06a0c-146">File System Projects</span></span>

<span data-ttu-id="06a0c-147">ビデオのチュートリアルで説明したように、ファイルシステム上の Web サイトをローカルコンピューター上に作成するか、ファイル共有を介してリモートの場所に作成するかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="06a0c-148">ファイルシステム上に作成された Web サイトは、ASP.NET 開発サーバーを使用して参照およびデバッグされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-149">ASP.NET 開発サーバーによって、お客様に混乱を招く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="06a0c-150">Web プロジェクトが IISs ディレクトリ構造のファイルシステムに作成された場合 (つまり、c:/inetpub/wwwroot)、Visual Studio 2005 内から起動された場合でも、Web サイトは ASP.NET 開発サーバーを通じて参照されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="06a0c-151">そのため、すべての IIS 構成 (つまり認証方法) は適用されません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="06a0c-152">既定の web プロジェクトでは、既定の .aspx ページ、default.cs ファイル、およびアプリ/_Data フォルダーのみが含まれるため、大量のオーバーヘッドも解消されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="06a0c-153">Web.config と特別なフォルダー (つまり、app/_code) は必要に応じて追加されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="06a0c-154">Web プロジェクトには、必要なファイルとフォルダーだけが含まれています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="06a0c-155">HTTP プロジェクト</span><span class="sxs-lookup"><span data-stu-id="06a0c-155">HTTP Projects</span></span>

<span data-ttu-id="06a0c-156">HTTP プロジェクトは、ローカルの IIS Web サイトまたはリモート Web サイトで作成されたプロジェクトのどちらでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="06a0c-157">既定のプロジェクトの場所は `http://localhost`です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="06a0c-158">参照ボタンをクリックした場合、[ローカル IIS] と [リモートサイト] の2つの HTTP オプションがあります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="06a0c-159">この2つのオプションの主な違いは、web サイトの情報を [場所の選択] ダイアログボックスに表示する方法と、ファイルを Web サーバーにコピーする方法です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="06a0c-160">ローカル IIS オプションは、ローカルコンピューター上のメタベースからサイト情報を読み取ります。ファイルは、ファイルシステムを使用してコピーされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="06a0c-161">リモートサイトオプションは FrontPage Server Extensions を使用し、サイト情報とファイルは HTTP と FrontPage Server Extensions の RPC 呼び出しを使用してコピーされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-162">Vs # # #/_tmp .htm ファイルと get/_aspx/_ver .aspx は、バージョン情報の決定には使用されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="06a0c-163">既定の HTTP オプションは Local IIS です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="06a0c-164">このオプションでは、IIS メタベースを読み取り、利用可能なサイトとコンテンツを作成する場所を特定します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="06a0c-165">別のフォルダーまたは仮想ディレクトリを選択するには、ツリービューでそれを選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="06a0c-166">また、新しい仮想ディレクトリを作成したり、フォルダーをアプリケーションとしてマークしたり、このダイアログボックスから既存の仮想ディレクトリを削除したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

![[場所の選択] ダイアログ](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="06a0c-168">**図 1**: [場所の選択] ダイアログ</span><span class="sxs-lookup"><span data-stu-id="06a0c-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="06a0c-169">以前のバージョンの Visual Studio とは異なり、[ **Secure Sockets Layer を使用**する] チェックボックスをオンにし、SSL 証明書が参照している URL と一致しない場合は、続行するかどうかを確認するセキュリティ警告ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="06a0c-170">Visual Studio .NET 2003 を使用すると、証明書が一致しない場合、プロジェクトの作成は失敗します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![SSL 証明書に関するセキュリティの警告](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="06a0c-172">**図 2**: SSL 証明書に関するセキュリティの警告</span><span class="sxs-lookup"><span data-stu-id="06a0c-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="06a0c-173">ホストヘッダーに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="06a0c-173">Note on Host Headers</span></span>

<span data-ttu-id="06a0c-174">特定の IP にバインドされたサイトで Web アプリケーションを作成する場合は、ホストヘッダーが構成されていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="06a0c-175">そうしないと、Visual Studio によって `http://localhost`にサイトが作成されますが、サイトが IDE 内から参照またはデバッグされている場合、IP アドレスは正しく解決されません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="06a0c-176">[リモートサイト] オプションを選択すると、ダイアログボックスが表示され、新しい Web サイトの送信先 URL を入力できるようになります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="06a0c-177">この URL は、FrontPage Server Extensions が有効になっているサーバー上にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="06a0c-178">FrontPage Server Extensions を使用してローカル Web サーバーを操作する場合は、[リモートサイト] オプションを使用してローカル URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![リモートサーバーでの Web サイトの作成](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="06a0c-180">**図 3**: リモートサーバーに Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="06a0c-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="06a0c-181">SSL を使用してリモートサイトにアプリケーションを作成する場合、SSL 証明書が一致しない場合、確認ダイアログは、ローカル IIS オプションを使用したときに表示されるダイアログと若干異なります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![リモートサイトのセキュリティアラート](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="06a0c-183">**図 4**: リモートサイトのセキュリティの警告</span><span class="sxs-lookup"><span data-stu-id="06a0c-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="06a0c-184">FTP</span><span class="sxs-lookup"><span data-stu-id="06a0c-184">FTP</span></span>

<span data-ttu-id="06a0c-185">Visual Studio 2005 では、FTP 経由で Web サイトを作成するためのオプションが導入されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="06a0c-186">このオプションを使用すると、IDE は users temp フォルダーにローカルでファイルを作成し、FTP を使用してファイルを FTP の場所に移動します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-187">Temp フォルダーの場所は、c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;アプリケーション名&gt;</span><span class="sxs-lookup"><span data-stu-id="06a0c-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="06a0c-188">FTP オプションを使用すると、[場所の選択] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="06a0c-189">次に示すように、必要な FTP 接続情報をこのダイアログボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP の [場所の選択] ダイアログ](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="06a0c-191">**図 5**: FTP の [場所の選択] ダイアログ</span><span class="sxs-lookup"><span data-stu-id="06a0c-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="06a0c-192">ラボ: FTP サイトのセットアップとプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="06a0c-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="06a0c-193">次の手順では、ftp サイトを構成して、ユーザーが FTP 経由でのみアップロードできる場所を持つようにします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="06a0c-194">FTP サービスをインストールする</span><span class="sxs-lookup"><span data-stu-id="06a0c-194">Install the FTP Service</span></span>

1. <span data-ttu-id="06a0c-195">[プログラムの追加と削除] を開き、[Windows コンポーネントの追加と削除] を選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="06a0c-196">インターネットインフォメーションサービス (Windows 2003 の場合はアプリケーションサーバー) を選択し、 **[詳細]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="06a0c-197">**ファイル転送プロトコル (FTP) サービス**を確認し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="06a0c-198">**[次へ]** をクリックして、FTP サービスをインストールします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="06a0c-199">コンテンツ用の新しいフォルダーを作成する</span><span class="sxs-lookup"><span data-stu-id="06a0c-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="06a0c-200">Windows エクスプローラーで、c:/inetpub/wwwroot 内に**User1**という名前の新しいフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="06a0c-201">フォルダーおよびフォルダーに対するアクセス許可を構成します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="06a0c-202">[管理ツール] からインターネットインフォメーションサービススナップインを開きます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="06a0c-203">これで、[コンピューター名] ノードの下に [FTP サイト] フォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="06a0c-204">**[FTP サイト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="06a0c-205">**既定の FTP サイト**を右クリックし、 **[新規**]、 **[仮想ディレクトリ]** の順に選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="06a0c-206">仮想ディレクトリ名として「 **User1** 」と入力し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="06a0c-207">パスとして **「c:/inetpub/wwwroot/User1** 」と入力し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="06a0c-208">**[次へ]** をクリックし、 **[完了]** をクリックしてウィザードを完了します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="06a0c-209">[既定の FTP サイト] で**User1**仮想ディレクトリを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="06a0c-210">**[書き込み]** チェックボックスをオンにし、 **[OK]** をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="06a0c-211">既定の **[FTP サイト]** を右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="06a0c-212">**[セキュリティアカウント]** タブで、 **[匿名接続を許可する]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="06a0c-213">続行するかどうかを確認するダイアログで **[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="06a0c-214">**[OK]** をクリックしてダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="06a0c-215">**[Web サイト]** ノードの下の **[既定の web サイト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="06a0c-216">**User1**ディレクトリを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="06a0c-217">**[アプリケーションの設定]** セクションで、 **[作成]** をクリックして、フォルダーをアプリケーションとしてマークします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="06a0c-218">**[OK]** をクリックしてダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="06a0c-219">インターネットインフォメーションサービススナップインを閉じます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="06a0c-220">Web プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="06a0c-220">Create web project</span></span>

1. <span data-ttu-id="06a0c-221">Visual Studio 2005 を開きます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="06a0c-222">**[ファイル]** メニューの **[新しい Web サイト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="06a0c-223">**[場所]** ドロップダウンで、 **[FTP]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="06a0c-224">**[参照]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-224">Click **Browse**.</span></span>
5. <span data-ttu-id="06a0c-225">**[サーバー]** テキストボックスに「 **localhost** 」と入力します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="06a0c-226">[ディレクトリ] ボックスに「 **User1** 」と入力します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="06a0c-227">**[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-227">Click **Open**.</span></span> <span data-ttu-id="06a0c-228">FTP の場所は、[新しい Web サイト] ダイアログに入力されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="06a0c-229">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-229">Click **OK**.</span></span>
9. <span data-ttu-id="06a0c-230">FTP ログオン ダイアログで **匿名ログオン** チェックボックスをオフにし、資格情報を入力して、**OK** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="06a0c-231">プロジェクトの URL は何ですか?</span><span class="sxs-lookup"><span data-stu-id="06a0c-231">What is the URL for the project?</span></span> <span data-ttu-id="06a0c-232">(プロジェクトの URL はソリューションエクスプローラーに表示されます)。</span><span class="sxs-lookup"><span data-stu-id="06a0c-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="06a0c-233">**[ビルド]** メニューの **[Web サイトのビルド]** または **[ソリューションのビルド]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="06a0c-234">ソリューションエクスプローラーで default.aspx を右クリックし、 **[ブラウザーで表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="06a0c-235">[Web サイトの URL が必要] ダイアログボックスで、URL として「`http://localhost/user1`」と入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-236">型/_Default を読み込むことができないことを示すエラーが表示された場合は、以前のバージョンではなく、Web サイトで ASP.NET 2.0 を実行していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="06a0c-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="06a0c-237">これはインターネットインフォメーションサービスの [ASP.NET] タブから行うことができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="06a0c-238">Web プロジェクトを開く</span><span class="sxs-lookup"><span data-stu-id="06a0c-238">Opening Web Projects</span></span>

<span data-ttu-id="06a0c-239">Web プロジェクトを開くことは、プロジェクトの作成と似ています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="06a0c-240">次のセクションでは、IDE 内での作業中に使用する領域について説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="06a0c-241">また、HTTP および FTP を使用した Web プロジェクトの操作についても説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="06a0c-242">Web プロジェクトを開くには、[ファイル] メニューの [Web サイトを開く] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="06a0c-243">前に説明したのと同じ [場所を選択] ダイアログボックスが表示され、ファイルシステム、ローカル IIS、FTP、リモートサイトの4つのオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="06a0c-244">ファイル システム</span><span class="sxs-lookup"><span data-stu-id="06a0c-244">File System</span></span>

<span data-ttu-id="06a0c-245">このモジュールで既に説明したように、Visual Studio はプロジェクトファイルを使用しなくなりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="06a0c-246">したがって、ファイルシステムから Web サイトを開くことを選択した場合、実際には、選択したフォルダーが Visual Studio で最初に Web プロジェクトとして作成されていない場合でも、必要なフォルダーを選択できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="06a0c-247">たとえば、[マイドキュメント] フォルダーを Web サイトとして開くことを選択すると、次のように Visual Studio によってファイルが開き、ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![Web サイトとして開かれたマイドキュメント](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="06a0c-249">**図 6**: Web サイトとして開いている*ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="06a0c-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="06a0c-250">Visual Studio は必要に応じて追加のファイルとフォルダーのみを作成するため、開いている場所に追加のファイルやフォルダーは追加されません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="06a0c-251">このアーキテクチャの副作用は、ファイルシステムに Web サイトを入れ子にできないことです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="06a0c-252">たとえば、次のディレクトリ構造について考えてみます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="06a0c-253">C:/MyWebSite サイトの Web プロジェクト</span><span class="sxs-lookup"><span data-stu-id="06a0c-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="06a0c-254">C:/MyWebSite/Nested の別の web プロジェクト</span><span class="sxs-lookup"><span data-stu-id="06a0c-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="06a0c-255">C:/MyWebSite サイトで Web サイトを開くと、入れ子になったフォルダーがそのアプリケーションのサブフォルダーとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="06a0c-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="06a0c-256">HTTP</span></span>

<span data-ttu-id="06a0c-257">HTTP 経由で Web サイトを開くと、IIS メタベース (ローカル IIS) または FrontPage Server Extensions (リモートサイト) のいずれかを使用して、設定が読み取られます。入れ子になった web アプリケーションがある場合は、それらをアプリケーションとして識別するアイコンと共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="06a0c-258">FrontPage での web アプリケーションの操作に慣れている場合は、Visual Studio 2005 の動作も似ています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="06a0c-259">現在 IDE 内で開かれているアプリケーションの下に入れ子になっているアプリケーションのアイコンが Visual Studio に表示される場合でも、コンテンツを表示するために拡張することはできません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="06a0c-260">ただし、それらをダブルクリックして開くことはできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="06a0c-261">この操作を行うと、web アプリケーションを開く (または現在開いているソリューションを置き換える) か、現在のソリューションに Web アプリケーションを追加するかを確認するダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![入れ子になったアプリケーションアイコンをダブルクリックすると、このダイアログが表示されます。](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="06a0c-263">**図 7**: 入れ子になったアプリケーションアイコンをダブルクリックすると、このダイアログが表示される</span><span class="sxs-lookup"><span data-stu-id="06a0c-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="06a0c-264">FTP サイト</span><span class="sxs-lookup"><span data-stu-id="06a0c-264">FTP Site</span></span>

<span data-ttu-id="06a0c-265">FTP 経由でサイトを開くと、ファイルはすべてローカルの temp フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="06a0c-266">ローカルストレージの場所の完全なパスは、プロジェクトの [プロパティ] ウィンドウに表示され、次の形式で作成されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="06a0c-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;アプリケーション名&gt;</span><span class="sxs-lookup"><span data-stu-id="06a0c-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="06a0c-268">FTP を使用する場合、Visual Studio ではプロジェクトのベース URL を指定する必要があるため、次のように参照できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="06a0c-269">ベース URL を指定しなかった場合は、Web サイト内のページを初めて参照しようとしたときに、そのことを求めるメッセージが Visual Studio によって表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![FTP サイトのベース URL の指定](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="06a0c-271">**図 8**: FTP サイトのベース URL を指定する</span><span class="sxs-lookup"><span data-stu-id="06a0c-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="06a0c-272">コンパイルの機能強化</span><span class="sxs-lookup"><span data-stu-id="06a0c-272">Improvements in Compilation</span></span>

<span data-ttu-id="06a0c-273">Visual Studio 2005 で Web アプリケーションを操作すると、以前のバージョンよりもかなり高速に処理できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="06a0c-274">これは、コンパイルアーキテクチャの変更に小さな部分がないためです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="06a0c-275">Visual Studio 2002 および2003では、Web アプリケーションは、/bin フォルダーに存在する1つのプライマリアセンブリにコンパイルされました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="06a0c-276">Visual Studio 2005 で、アプリ/_Code フォルダーが追加されました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="06a0c-277">クラスとその他の UI 以外のコードは、アプリ/_Code フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="06a0c-278">Visual Studio によってプロジェクトがビルドされると、アプリ/_Code フォルダー内のすべてのファイルが1つのアプリ/_Code .dll ファイルにコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="06a0c-279">この変更の結果、後続のビルドは以前のバージョンよりもはるかに高速になります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-280">MSBuild コマンドラインユーティリティを使用して、ASP.NET Web アプリケーションを構築することもできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="06a0c-281">このツールについては、モジュール9で説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="06a0c-282">もう1つのコンパイル拡張機能は、[ビルド] メニューの [新しいビルドページ] オプションです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="06a0c-283">この機能を使用すると、開発者は現在のページのみを (もちろん、依存関係と共に) 再構築できるので、変更をより迅速にコンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="06a0c-284">でC#は intellisense を更新するためのバックグラウンドコンパイルが提供されないため、この機能を使用すると、単一ページを単に再構築するだけで intellisense をすばやく更新できるため、この機能を非常できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="06a0c-285">プロジェクトのビルドプロパティを使用すると、スタートアップページが実行される前に発生するビルドの種類を構成できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="06a0c-286">開発者は、現在のページのみをビルドして、Visual Studio がコードの変更後により迅速にアプリケーションのデバッグを開始できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

![ビルドページの開始アクション](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="06a0c-288">**図 9**: ビルドページの開始アクション</span><span class="sxs-lookup"><span data-stu-id="06a0c-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="06a0c-289">Visual Studio と ASP.NET アーキテクチャのもう1つの優れた機能強化は、エディットコンティニュの領域にあります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="06a0c-290">Visual Studio 2005 では、開発者はプロジェクトのデバッグを開始し、デバッガーをデタッチせずにプロジェクトでコードを変更できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="06a0c-291">実際には、プロジェクトのデバッグを開始し、新しいクラスを追加し、そのクラスにコードを追加し、そのクラスの新しいインスタンスを作成してクラスのメソッドを実行するコードをページに追加します。デバッガーはデタッチされません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="06a0c-292">新しいコードを実行すると、ブラウザーを更新するだけで簡単に実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="06a0c-293">Visual Studio 2005 のエディットコンティニュ機能のビデオチュートリアルを参照するには、ここをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="06a0c-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="06a0c-294">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="06a0c-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="06a0c-295">ASP.NET 2.0 と Visual Studio 2005 の堅牢なエディットコンティニュ機能は、ASP.NET アプリケーションのアーキテクチャの変更によるものです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="06a0c-296">ASP.NET 1.x では、Visual Studio 2002/2003 で作成されたアプリケーションは、/bin フォルダーに格納されていたプライマリアセンブリにコンパイルされています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="06a0c-297">アプリケーションのすべてのクラスやページなどが、その1つの DLL にコンパイルされました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="06a0c-298">次に、実行時に、ASP.NET はページ内のすべてのコントロール、マークアップ、および ASP.NET コードをコンパイルし、それらの Dll を ASP.NET 一時フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="06a0c-299">ASP.NET 2.0 を使用する Visual Studio 2005 では、上に示した2つのコンパイルモデル (Visual Studio 用と実行時の ASP.NET 用) が1つの共通コンパイルモデルにマージされています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="06a0c-300">つまり、コンパイルのすべての問題は、実行時ではなく、開発段階でキャッチされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="06a0c-301">また、デザイナーと IntelliSense で、ユーザーコントロールやマスターページなどの機能をサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="06a0c-302">ここをクリックして、ユーザーコントロールのデザイナーサポートのビデオチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="06a0c-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="06a0c-303">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="06a0c-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="06a0c-304">ユーザーコントロールがページから削除された場合、@Register ディレクティブはマークアップに残り、ユーザーコントロールが Web サイトから削除された場合にパーサーエラーを回避するために、手動で削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="06a0c-305">Visual Studio のコンパイルモデルのもう1つの改良点は、Web サイトの発行機能です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="06a0c-306">発行機能によって Web サイトがプリコンパイルされるため、開発者は、必要に応じて何もコンパイルしなくても、パフォーマンスを向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="06a0c-307">また、ソースコードをデプロイする必要がないように、App/_Code フォルダー内のすべてのソースコードを DLL にプリコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

![[Web サイトの発行] ダイアログ](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="06a0c-309">**図 10**: [Web サイトの発行] ダイアログ</span><span class="sxs-lookup"><span data-stu-id="06a0c-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-310">Aspnet/_compile ユーティリティを使用して、ASP.NET Web アプリケーションを事前にコンパイルすることもできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="06a0c-311">このツールについては、モジュール9で説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="06a0c-312">Web サイトを発行すると、次に示すように、プリコンパイルされたファイルが一時 ASP.NET Files フォルダーに格納されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="06a0c-313">ファイル拡張子が*コンパイル*されたファイルは、特定の dll の依存関係を定義する XML ファイルです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="06a0c-314">Web フォームまたはユーザーコントロールは、 *App/_Web/_* で始まるランダムな dll にコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="06a0c-315">[*このプリコンパイル済みサイトを更新可能に*する] チェックボックスをオンにしたままにした場合、Webforms およびユーザーコントロール内のマークアップは DLL に事前コンパイルされないため、デプロイ後に変更を加えることができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="06a0c-316">展開されたコンテンツの変更が許可されないようにマークアップをロックする場合は、このチェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="06a0c-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="06a0c-317">[*固定名およびシングルページアセンブリを使用*する] チェックボックスを使用すると、各ページが固定の名前付きアセンブリにコンパイルされるようにバッチコンパイルを無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="06a0c-318">このチェックボックスをオフのままにすると、バッチコンパイルを利用できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="06a0c-319">[*プリコンパイル済みアセンブリで厳密な*名前を付ける] チェックボックスを使用すると、プリコンパイル済みアセンブリに厳密な名前を付けることができます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-320">ASP.NET 1.x では、厳密な名前付きのアセンブリをグローバルアセンブリキャッシュ (GAC) にインストールする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="06a0c-321">ASP.NET 2.0 では、厳密な名前付きアセンブリを GAC にインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NET アプリケーションのプリコンパイル済みファイル](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="06a0c-323">**図 11**: ASP.NET アプリケーションのプリコンパイル済みファイル</span><span class="sxs-lookup"><span data-stu-id="06a0c-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-324">上記のアプリケーションでは、web.config ファイルがありませんでした。</span><span class="sxs-lookup"><span data-stu-id="06a0c-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="06a0c-325">既に存在していた場合は、Web サイトの発行プロセスの後に*PrecompiledApp*という名前が付いています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="06a0c-326">展開の機能強化</span><span class="sxs-lookup"><span data-stu-id="06a0c-326">Improvements in Deployment</span></span>

<span data-ttu-id="06a0c-327">Visual Studio 2002 および2003と同様に、Visual Studio 2005 にはプロジェクトのコピー機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="06a0c-328">ただし、この機能は Visual Studio 2005 で強化されており、現在は "Web サイトのコピー" と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="06a0c-329">[Web サイトのコピー] ダイアログは、左フレームと右フレームに分割されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="06a0c-330">左フレームはソース Web サイトと呼ばれ、右フレームはリモート Web サイトと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="06a0c-331">開発者によっては、右側のフレームに表示されるサイトが必ずしもリモートサイトであるとは限らないということがあります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="06a0c-332">ローカルファイルシステムまたは IIS のローカルインスタンスのサイトの場合もあります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="06a0c-333">また、ダイアログボックスを使用すると、リモート Web サイトからソース Web サイト*に*発行することができるため、左側のフレームに表示されるサイトは必ずしもソース web サイトであるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="06a0c-334">プロジェクトをリモート Web サイトにコピーする場合は、そのサイトに FrontPage Server Extensions がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="06a0c-335">そうでない場合は、FTP を使用して接続する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="06a0c-336">一方、ローカルの IIS インスタンスにプロジェクトをコピーする場合、FrontPage Server Extensions は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-337">ローカル IIS インスタンスに新しい Web サイトを作成しようとしたときに、FrontPage 2002 サーバー拡張機能がインストールされている場合は、SharePoint サーバーで Web サイトの作成がサポートされていないことを示すエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="06a0c-338">この場合、FrontPage 2000 のサーバー拡張機能をインストールするか、FrontPage Server Extensions を削除するかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="06a0c-339">Web サイトのコピー機能のビデオチュートリアルについては、こちらをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="06a0c-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="06a0c-340">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="06a0c-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="06a0c-341">デバッグの機能強化</span><span class="sxs-lookup"><span data-stu-id="06a0c-341">Improvements in Debugging</span></span>

<span data-ttu-id="06a0c-342">Visual Studio 2005 でのデバッグでは、主に4つの機能強化が行われています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="06a0c-343">管理者以外のローカルでのデバッグは、すぐに使用できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="06a0c-344">既定では、コンパイル要素の Debug 属性は false になりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="06a0c-345">リモートデバッグのセットアップと構成は、以前よりも簡単です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="06a0c-346">FTP の場所を介して開いている Web サイトをデバッグできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="06a0c-347">非管理者としてのデバッグ</span><span class="sxs-lookup"><span data-stu-id="06a0c-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="06a0c-348">ASP.NET 開発サーバーの追加により、管理者以外の管理者はすぐに ASP.NET アプリケーションを簡単にデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="06a0c-349">ローカルファイルシステムで実行されている ASP.NET アプリケーションがデバッグされると、Visual Studio は、ログオンしているユーザーのコンテキストで ASP.NET 開発サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="06a0c-350">そのユーザーは、追加の構成なしでそのアプリケーションをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="06a0c-351">既定ではデバッグは False です</span><span class="sxs-lookup"><span data-stu-id="06a0c-351">Debug is False by Default</span></span>

<span data-ttu-id="06a0c-352">ASP.NET 1.x では、web.config ファイルの*コンパイル*要素の*debug*属性が既定で*true*に設定されていました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="06a0c-353">アプリケーションを実稼働環境に配置する前に、開発者がこの属性を*false*に設定することを常に推奨していましたが、ほとんどの開発者はデバッグ属性を true に設定したままにした場合の結果を十分に理解していないので、単純にそのままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="06a0c-354">Debug 属性が true に設定されている場合の最も重大な問題は、ASP.NET コンパイルモデルを無効にすることです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="06a0c-355">したがって、各ページは個別の DLL にコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="06a0c-356">Web アプリケーションが数千のページで構成されている場合 (どのような方法でも前例ではありません)、そのアプリケーションによって数千の小さな Dll が作成されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="06a0c-357">これらの Dll はサイズが小さいのに対して、メモリ内の特定の場所に読み込まれません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="06a0c-358">そのため、システムメモリの断片化が発生し、OutOfMemoryException オカレンスに寄与する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="06a0c-359">ASP.NET 2.0 では、debug 属性は既定で false に設定されています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="06a0c-360">既に説明したように、開発者が Visual Studio 2005 で ASP.NET アプリケーションをデバッグすると、デバッグが有効になっている web.config ファイルを追加するように求められます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="06a0c-361">これを行うと、ASP.NET 1.x に存在するのと同じ欠点が発生しますが、開発者は、アプリケーションを運用環境に移行する前に、属性を false にリセットする必要があるという警告が表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="06a0c-362">リモートデバッグのセットアップと構成</span><span class="sxs-lookup"><span data-stu-id="06a0c-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="06a0c-363">Visual Studio 2002/2003 では、リモートデバッグはコンピューターデバッグマネージャー (mdm.exe) と vs7jit プロセスに依存していました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="06a0c-364">このため、リモートデバッグの問題のトラブルシューティングは、多くの場合、お客様のためのブラックボックスであり、PSS にとってはあまり良くありませんでした。</span><span class="sxs-lookup"><span data-stu-id="06a0c-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="06a0c-365">Visual Studio 2005 では、mdm.exe プロセスと vs7jit プロセスに依存することがなくなります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="06a0c-366">代わりに、リモートデバッグモニターサービス (msvsmon) を使用するようになりました。</span><span class="sxs-lookup"><span data-stu-id="06a0c-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="06a0c-367">Visual Studio 2005 でのリモートデバッグの要件は非常に単純です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="06a0c-368">デバッグする前に、リモートサーバーで msvsmon を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="06a0c-369">リモートデバッグモニターは、Visual Studio CD からインストールできます。または、Web サーバーに何もインストールせずに、共有から msvsmon を実行するだけでかまいません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="06a0c-370">Msvsmon を実行すると、リモートデバッグのためにブロックされているポートについての通知が表示される可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="06a0c-371">幸いにも、次に示すように、警告ダイアログボックスでポートのブロックを簡単に解除できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![Windows ファイアウォールがリモートデバッグをブロックしていることを示す通知](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="06a0c-373">**図 12**: Windows ファイアウォールがリモートデバッグをブロックしていることを示す通知</span><span class="sxs-lookup"><span data-stu-id="06a0c-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="06a0c-374">デバッグに必要なポートのブロックを解除すると、次に示すようにリモートデバッグモニターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="06a0c-375">このインターフェイスから、接続を監視し、デバッグのアクセス許可を簡単に変更できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![リモートデバッグモニター](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="06a0c-377">**図 13**: リモートデバッグモニター</span><span class="sxs-lookup"><span data-stu-id="06a0c-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="06a0c-378">FTP 経由で開かれた Web アプリケーションをリモートでデバッグすることもできます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="06a0c-379">手順は、前に説明した手順と同じです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="06a0c-380">ただし、このモジュールで既に説明したように、FTP プロジェクトを参照するためのベース URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="06a0c-381">ラボ2</span><span class="sxs-lookup"><span data-stu-id="06a0c-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="06a0c-382">Visual Studio 2005 を使用したリモートデバッグ</span><span class="sxs-lookup"><span data-stu-id="06a0c-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="06a0c-383">このラボでは、Visual Studio 2005 を使用したリモートデバッグについて説明します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="06a0c-384">このラボのビデオチュートリアルについては、ここをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="06a0c-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="06a0c-385">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="06a0c-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="06a0c-386">このラボでは2台のコンピューターが必要です。1つは Visual Studio 2005 を実行し、もう1つは IIS 5 以上を実行します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="06a0c-387">Visual Studio 2005 を開き、リモートサーバー上に新しい Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-388">Web サイトは、リモートの IIS インスタンスまたは FTP を使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="06a0c-389">リモート Web サーバーから、開発用コンピューターで、UNC パスを使用して msvsmon を見つけて実行します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="06a0c-390">Msvsmon の既定の場所は、server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/リモートデバッガー/x86 です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="06a0c-391">リモートデバッグ用にポートのブロックを解除するよう求められた場合は、それを実行します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="06a0c-392">開発用コンピューターから default.aspx の分離コードを開き、ページ/_Load メソッドにブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="06a0c-393">開発用コンピューターからデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="06a0c-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="06a0c-394">ブレークポイントを予想どおりにヒットさせる必要があります。</span><span class="sxs-lookup"><span data-stu-id="06a0c-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="06a0c-395">ASP.NET 開発サーバー</span><span class="sxs-lookup"><span data-stu-id="06a0c-395">ASP.NET Development Server</span></span>

<span data-ttu-id="06a0c-396">既に説明したように、Visual Studio 2005 には ASP.NET 開発サーバーという名前の Web サーバーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="06a0c-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="06a0c-397">(ASP.NET 開発サーバーは、Cassini と呼ばれることもあります)。この Web サーバーは、ファイルシステムで実行されている Web アプリケーションを参照およびデバッグするための便利な手段です。</span><span class="sxs-lookup"><span data-stu-id="06a0c-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="06a0c-398">ASP.NET 開発サーバーは制限された Web サーバーです。</span><span class="sxs-lookup"><span data-stu-id="06a0c-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="06a0c-399">リモート接続は許可されません。 Web サーバーを起動したユーザー以外のユーザーからの要求は許可されません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="06a0c-400">また、ASP ページにサービスを提供する機能はありません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="06a0c-401">ASP.NET のリソースと HTML リソース (画像、CSS ファイルなどを含む) のみが提供されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="06a0c-402">ASP.NET 開発サーバーは、c:/Windows/Microsoft .NET/Framework/v2.0./ */* / */* /\* にある webdev. WebServer ファイルを実行することで、コマンドラインから起動できます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="06a0c-403">次のダイアログには、使用可能なパラメーターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06a0c-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="06a0c-404">**図14**</span><span class="sxs-lookup"><span data-stu-id="06a0c-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="06a0c-405">ASP.NET 開発サーバーは、コマンドラインを使用して明示的に起動した場合はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="06a0c-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
