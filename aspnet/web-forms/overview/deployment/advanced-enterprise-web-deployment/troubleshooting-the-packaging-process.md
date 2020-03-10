---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: パッケージ化プロセスのトラブルシューティング |Microsoft Docs
author: jrjlee
description: このトピックでは、M... で Enablepackageprocessの Andassert プロパティを使用して、パッケージ化プロセスに関する詳細情報を収集する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509752"
---
# <a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="2cab4-103">パッケージ化処理のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="2cab4-103">Troubleshooting the Packaging Process</span></span>

<span data-ttu-id="2cab4-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="2cab4-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="2cab4-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="2cab4-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="2cab4-106">このトピックでは、Microsoft Build Engine (MSBuild) で**Enablepackageprocessの Andassert**プロパティを使用して、パッケージ化プロセスに関する詳細情報を収集する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="2cab4-107">**Enablepackageprocessの Andassert**プロパティを**true**に設定すると、MSBuild は次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="2cab4-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="2cab4-108">ビルドログにパッケージ化プロセスに関する追加情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="2cab4-109">特定の条件下でエラーをログに記録します。たとえば、パッケージ化の一覧に重複するファイルがある場合などです。</span><span class="sxs-lookup"><span data-stu-id="2cab4-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="2cab4-110">*ProjectName*\_パッケージフォルダーにログディレクトリを作成し、パッケージ化するファイルに関する情報を記録するために使用します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="2cab4-111">パッケージ化処理が失敗した場合、または web 配置パッケージに予期したファイルが含まれていない場合は、この情報を使用してプロセスのトラブルシューティングを行い、問題が発生している場所を特定することができます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="2cab4-112">**Enablepackageprocessの Andassert**プロパティは、**デバッグ**構成を使用してプロジェクトをビルドする場合にのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="2cab4-113">他の構成では、プロパティは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-113">The property is ignored in other configurations.</span></span>

<span data-ttu-id="2cab4-114">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="2cab4-115">これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="2cab4-116">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="2cab4-117">Enablepackageprocessの Andassert プロパティについて</span><span class="sxs-lookup"><span data-stu-id="2cab4-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="2cab4-118">[Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)Web 発行パイプライン (WPP) が msbuild ターゲットのセットを提供する方法について説明します。これにより、msbuild の機能が拡張され、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) と統合できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2cab4-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="2cab4-119">Web アプリケーションプロジェクトをパッケージ化する場合は、WPP ターゲットを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="2cab4-120">これらの WPP ターゲットの多くには、 **Enablepackageprocesslogs Andassert**プロパティが**true**に設定されている場合に追加情報をログに記録する条件付きロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="2cab4-121">たとえば、**パッケージ**ターゲットを確認すると、追加のログディレクトリが作成され、 **enablepackageprocessの andassert**が**true**の場合は、ファイルの一覧がテキストファイルに書き込まれることがわかります。</span><span class="sxs-lookup"><span data-stu-id="2cab4-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="2cab4-122">WPP ターゲットは、% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web フォルダーの*Microsoft. Publishing. .targets*ファイルで定義されています。</span><span class="sxs-lookup"><span data-stu-id="2cab4-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="2cab4-123">このファイルを開き、Visual Studio 2010 または任意の XML エディターでターゲットを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="2cab4-124">ファイルの内容を変更しないように注意してください。</span><span class="sxs-lookup"><span data-stu-id="2cab4-124">Take care not to modify the contents of the file.</span></span>

## <a name="enabling-the-additional-logging"></a><span data-ttu-id="2cab4-125">追加のログ記録を有効にする</span><span class="sxs-lookup"><span data-stu-id="2cab4-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="2cab4-126">**Enablepackageprocessの Andassert**プロパティの値は、プロジェクトのビルド方法に応じてさまざまな方法で指定できます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="2cab4-127">コマンドラインからプロジェクトをビルドする場合は、コマンドライン引数として**Enablepackageprocessの Andassert**プロパティの値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

<span data-ttu-id="2cab4-128">カスタムプロジェクトファイルを使用してプロジェクトをビルドしている場合は、 **MSBuild**タスクの**Properties**属性に**Enablepackageprocessの andassert**値を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

<span data-ttu-id="2cab4-129">Team Foundation Server (TFS) のビルド定義を使用してプロジェクトをビルドしている場合は、 **MSBuild の Arguments**行で**enablepackageprocessの andassert**プロパティの値を指定できます。![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2cab4-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="2cab4-130">ビルド定義の作成と構成の詳細については、「[配置をサポートするビルド定義の作成](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cab4-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>

<span data-ttu-id="2cab4-131">または、すべてのビルドにパッケージを含める場合は、web アプリケーションプロジェクトのプロジェクトファイルを変更して、 **Enablepackageprocessの Andassert**プロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="2cab4-132">.Csproj ファイルまたは .vbproj ファイル内の最初の**PropertyGroup**要素にプロパティを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cab4-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a><span data-ttu-id="2cab4-133">ログファイルの確認</span><span class="sxs-lookup"><span data-stu-id="2cab4-133">Reviewing the Log Files</span></span>

<span data-ttu-id="2cab4-134">**Enablepackageprocessの Andassert**が**true**に設定された web アプリケーションプロジェクトをビルドしてパッケージ化すると、MSBuild は*ProjectName*\_package フォルダーに Log という名前の追加のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="2cab4-135">ログフォルダーには、さまざまなファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2cab4-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="2cab4-136">表示されるファイルの一覧は、プロジェクトの内容とビルドプロセスによって異なります。</span><span class="sxs-lookup"><span data-stu-id="2cab4-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="2cab4-137">ただし、通常、これらのファイルは、処理のさまざまな段階で、パッケージ化のために WPP が収集しているファイルの一覧を記録するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="2cab4-138">*PreExcludePipelineCollectFilesPhaseFileList*ファイルには、除外対象として指定されたファイルがすべて削除される前に、MSBuild によってパッケージ化のために収集されるファイルが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="2cab4-139">*AfterExcludeFilesFilesList*ファイルには、除外対象として指定されたファイルがすべて削除された後に、変更されたファイルの一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2cab4-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2cab4-140">パッケージ化プロセスからファイルとフォルダーを除外する方法の詳細については、「[展開からのファイルとフォルダーの除外](excluding-files-and-folders-from-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cab4-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="2cab4-141">*Aftertransformwebconfig .txt*ファイルには *、任意の web.config 変換*が実行された後にパッケージ化のために収集されたファイルが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="2cab4-142">この一覧では、構成固有の*web.config 変換ファイル*( *web.config や web.config など)* *は、パッケージ*化のためにファイルの一覧から除外されます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="2cab4-143">変換された1つの*web.config*がその場所に含まれています。</span><span class="sxs-lookup"><span data-stu-id="2cab4-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="2cab4-144">*PostAutoParameterizationWebConfigConnectionStrings*ファイルには、 *web.config ファイル内*の接続文字列がパラメーター化された後のファイルの一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2cab4-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="2cab4-145">これは、パッケージを配置するときに、接続文字列をターゲット環境の適切な設定に置き換えることができるプロセスです。</span><span class="sxs-lookup"><span data-stu-id="2cab4-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="2cab4-146">*Prepackage .txt*ファイルには、パッケージに含めるファイルの完成したビルド前の一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2cab4-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="2cab4-147">追加のログファイルの名前は、通常、WPP ターゲットに対応します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="2cab4-148">これらのターゲットを確認するには *、%* PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web フォルダー内のファイルを調べます。</span><span class="sxs-lookup"><span data-stu-id="2cab4-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>

<span data-ttu-id="2cab4-149">Web パッケージの内容が期待どおりでない場合は、これらのファイルを確認することで、プロセスがどの時点で問題になったかを特定するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="2cab4-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2cab4-150">まとめ</span><span class="sxs-lookup"><span data-stu-id="2cab4-150">Conclusion</span></span>

<span data-ttu-id="2cab4-151">このトピックでは、MSBuild で**Enablepackageprocessの Andassert**プロパティを使用して、パッケージ化プロセスのトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2cab4-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="2cab4-152">この記事では、ビルドプロセスにプロパティ値を提供するさまざまな方法について説明し、プロパティを**true**に設定した場合に記録される追加情報について説明しました。</span><span class="sxs-lookup"><span data-stu-id="2cab4-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="2cab4-153">参考資料</span><span class="sxs-lookup"><span data-stu-id="2cab4-153">Further Reading</span></span>

<span data-ttu-id="2cab4-154">カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cab4-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="2cab4-155">WPP と、それがパッケージ化プロセスを管理する方法の詳細については、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cab4-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="2cab4-156">Web 配置パッケージから特定のファイルとフォルダーを除外する方法のガイダンスについては、「[展開からのファイルとフォルダーの除外](excluding-files-and-folders-from-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cab4-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2cab4-157">[[戻る]](running-windows-powershell-scripts-from-msbuild-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="2cab4-157">[Previous](running-windows-powershell-scripts-from-msbuild-project-files.md)</span></span>
