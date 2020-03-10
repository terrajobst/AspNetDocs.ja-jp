---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild プロジェクトファイルから Windows PowerShell スクリプトを実行する |Microsoft Docs
author: jrjlee
description: このトピックでは、ビルドおよび配置のプロセスの一部として Windows PowerShell スクリプトを実行する方法について説明します。 スクリプトはローカルで実行できます (つまり、b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441448"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a><span data-ttu-id="7ba61-104">MSBuild プロジェクト ファイルから Windows PowerShell スクリプトを実行する</span><span class="sxs-lookup"><span data-stu-id="7ba61-104">Running Windows PowerShell Scripts from MSBuild Project Files</span></span>

<span data-ttu-id="7ba61-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="7ba61-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="7ba61-106">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="7ba61-106">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="7ba61-107">このトピックでは、ビルドおよび配置のプロセスの一部として Windows PowerShell スクリプトを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-107">This topic describes how to run a Windows PowerShell script as part of a build and deployment process.</span></span> <span data-ttu-id="7ba61-108">スクリプトは、移行先の web サーバーやデータベースサーバーなど、ローカルで (つまり、ビルドサーバー上で) 実行することも、リモートで実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-108">You can run a script locally (in other words, on the build server) or remotely, like on a destination web server or database server.</span></span>
> 
> <span data-ttu-id="7ba61-109">配置後の Windows PowerShell スクリプトを実行する理由は多数あります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-109">There are lots of reasons why you might want to run a post-deployment Windows PowerShell script.</span></span> <span data-ttu-id="7ba61-110">たとえば、次の場合です。</span><span class="sxs-lookup"><span data-stu-id="7ba61-110">For example, you might want to:</span></span>
> 
> - <span data-ttu-id="7ba61-111">カスタムイベントソースをレジストリに追加します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-111">Add a custom event source to the registry.</span></span>
> - <span data-ttu-id="7ba61-112">アップロード用のファイルシステムディレクトリを生成します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-112">Generate a file system directory for uploads.</span></span>
> - <span data-ttu-id="7ba61-113">ビルドディレクトリをクリーンアップします。</span><span class="sxs-lookup"><span data-stu-id="7ba61-113">Clean up build directories.</span></span>
> - <span data-ttu-id="7ba61-114">カスタムログファイルにエントリを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-114">Write entries to a custom log file.</span></span>
> - <span data-ttu-id="7ba61-115">新しくプロビジョニングされた web アプリケーションにユーザーを招待する電子メールを送信します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-115">Send emails inviting users to a newly provisioned web application.</span></span>
> - <span data-ttu-id="7ba61-116">適切なアクセス許可を持つユーザーアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-116">Create user accounts with the appropriate permissions.</span></span>
> - <span data-ttu-id="7ba61-117">SQL Server インスタンス間のレプリケーションを構成します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-117">Configure replication between SQL Server instances.</span></span>
> 
> <span data-ttu-id="7ba61-118">このトピックでは、Microsoft Build Engine (MSBuild) プロジェクトファイルのカスタムターゲットから Windows PowerShell スクリプトをローカルとリモートの両方で実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-118">This topic will show you how to run Windows PowerShell scripts both locally and remotely from a custom target in a Microsoft Build Engine (MSBuild) project file.</span></span>

<span data-ttu-id="7ba61-119">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="7ba61-120">これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="7ba61-121">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="7ba61-122">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="7ba61-122">Task Overview</span></span>

<span data-ttu-id="7ba61-123">自動またはシングルステップのデプロイプロセスの一環として Windows PowerShell スクリプトを実行するには、次の高レベルのタスクを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-123">To run a Windows PowerShell script as part of an automated or single-step deployment process, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="7ba61-124">Windows PowerShell スクリプトをソリューションとソース管理に追加します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-124">Add the Windows PowerShell script to your solution and to source control.</span></span>
- <span data-ttu-id="7ba61-125">Windows PowerShell スクリプトを呼び出すコマンドを作成します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-125">Create a command that invokes your Windows PowerShell script.</span></span>
- <span data-ttu-id="7ba61-126">コマンドで予約済みの XML 文字をエスケープします。</span><span class="sxs-lookup"><span data-stu-id="7ba61-126">Escape any reserved XML characters in your command.</span></span>
- <span data-ttu-id="7ba61-127">カスタム MSBuild プロジェクトファイルにターゲットを作成し、 **Exec**タスクを使用してコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-127">Create a target in your custom MSBuild project file and use the **Exec** task to run your command.</span></span>

<span data-ttu-id="7ba61-128">このトピックでは、これらの手順を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-128">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="7ba61-129">このトピックのタスクとチュートリアルでは、MSBuild のターゲットとプロパティについて理解していること、およびカスタム MSBuild プロジェクトファイルを使用してビルドおよび配置プロセスを実行する方法について理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="7ba61-129">The tasks and walkthroughs in this topic assume that you're already familiar with MSBuild targets and properties, and that you understand how to use a custom MSBuild project file to drive a build and deployment process.</span></span> <span data-ttu-id="7ba61-130">詳細については、「[プロジェクトファイルに](../web-deployment-in-the-enterprise/understanding-the-project-file.md)ついて」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ba61-130">For more information, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

## <a name="creating-and-adding-windows-powershell-scripts"></a><span data-ttu-id="7ba61-131">Windows PowerShell スクリプトの作成と追加</span><span class="sxs-lookup"><span data-stu-id="7ba61-131">Creating and Adding Windows PowerShell Scripts</span></span>

<span data-ttu-id="7ba61-132">このトピックのタスクでは、「 **Logdeploy. ps1** 」という名前のサンプル Windows PowerShell スクリプトを使用して、MSBuild からスクリプトを実行する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-132">The tasks in this topic use a sample Windows PowerShell script named **LogDeploy.ps1** to illustrate how to run scripts from MSBuild.</span></span> <span data-ttu-id="7ba61-133">**Logdeploy. ps1**スクリプトには、1行のエントリをログファイルに書き込む単純な関数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7ba61-133">The **LogDeploy.ps1** script contains a simple function that writes a single-line entry to a log file:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

<span data-ttu-id="7ba61-134">**Logdeploy. ps1**スクリプトは2つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-134">The **LogDeploy.ps1** script accepts two parameters.</span></span> <span data-ttu-id="7ba61-135">最初のパラメーターは、エントリを追加するログファイルへの完全パスを表し、2番目のパラメーターは、ログファイルに記録する配置先を表します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-135">The first parameter represents the full path to the log file to which you want to add an entry, and the second parameter represents the deployment destination that you want to record in the log file.</span></span> <span data-ttu-id="7ba61-136">スクリプトを実行すると、次の形式でログファイルに行が追加されます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-136">When you run the script, it adds a line to the log file in this format:</span></span>

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

<span data-ttu-id="7ba61-137">MSBuild で**Logdeploy. ps1**スクリプトを使用できるようにするには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-137">To make the **LogDeploy.ps1** script available to MSBuild, you need to:</span></span>

- <span data-ttu-id="7ba61-138">スクリプトをソース管理に追加します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-138">Add the script to source control.</span></span>
- <span data-ttu-id="7ba61-139">Visual Studio 2010 で、スクリプトをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-139">Add the script to your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="7ba61-140">ビルドサーバーとリモートコンピューターのどちらでスクリプトを実行するかに関係なく、スクリプトをソリューションコンテンツと共に配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="7ba61-140">You don't need to deploy the script with your solution content, regardless of whether you plan to run the script on the build server or on a remote computer.</span></span> <span data-ttu-id="7ba61-141">1つの方法として、スクリプトをソリューションフォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-141">One option is to add the script to a solution folder.</span></span> <span data-ttu-id="7ba61-142">Contact Manager の例では、デプロイプロセスの一部として Windows PowerShell スクリプトを使用する必要があるため、[ソリューションの発行] フォルダーにスクリプトを追加するのが理にかなっています。</span><span class="sxs-lookup"><span data-stu-id="7ba61-142">In the Contact Manager example, because you want to use the Windows PowerShell script as part of the deployment process, it makes sense to add the script to the Publish solution folder.</span></span>

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

<span data-ttu-id="7ba61-143">ソリューションフォルダーの内容がソース資料としてビルドサーバーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-143">The contents of solution folders are copied to build servers as source material.</span></span> <span data-ttu-id="7ba61-144">ただし、これらはプロジェクトの出力の一部を形成しません。</span><span class="sxs-lookup"><span data-stu-id="7ba61-144">However, they form no part of any project output.</span></span>

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a><span data-ttu-id="7ba61-145">ビルドサーバーで Windows PowerShell スクリプトを実行する</span><span class="sxs-lookup"><span data-stu-id="7ba61-145">Executing a Windows PowerShell Script on the Build Server</span></span>

<span data-ttu-id="7ba61-146">場合によっては、プロジェクトをビルドするコンピューターで Windows PowerShell スクリプトを実行することが必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-146">In some scenarios, you may want to run Windows PowerShell scripts on the computer that builds your projects.</span></span> <span data-ttu-id="7ba61-147">たとえば、Windows PowerShell スクリプトを使用して、ビルドフォルダーのクリーンアップやカスタムログファイルへのエントリの書き込みを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-147">For example, you might use a Windows PowerShell script to clean up build folders or write entries to a custom log file.</span></span>

<span data-ttu-id="7ba61-148">構文に関しては、MSBuild プロジェクトファイルから Windows PowerShell スクリプトを実行することは、通常のコマンドプロンプトから Windows PowerShell スクリプトを実行することと同じです。</span><span class="sxs-lookup"><span data-stu-id="7ba61-148">In terms of syntax, running a Windows PowerShell script from an MSBuild project file is the same as running a Windows PowerShell script from a regular command prompt.</span></span> <span data-ttu-id="7ba61-149">Powershell 実行可能ファイルを起動し、 **– command**スイッチを使用して、Windows powershell で実行するコマンドを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-149">You need to invoke the powershell.exe executable and use the **–command** switch to provide the commands you want Windows PowerShell to run.</span></span> <span data-ttu-id="7ba61-150">(Windows PowerShell v2 では、 **– file**スイッチを使用することもできます)。</span><span class="sxs-lookup"><span data-stu-id="7ba61-150">(In Windows PowerShell v2, you can also use the **–file** switch).</span></span> <span data-ttu-id="7ba61-151">コマンドの形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-151">The command should take this format:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

<span data-ttu-id="7ba61-152">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-152">For example:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

<span data-ttu-id="7ba61-153">スクリプトへのパスにスペースが含まれている場合は、アンパサンドで始まる単一引用符でファイルパスを囲む必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-153">If the path to your script includes spaces, you need to enclose the file path in single quotes preceded by an ampersand.</span></span> <span data-ttu-id="7ba61-154">二重引用符は使用できません。コマンドを囲むために既に使用されているためです。</span><span class="sxs-lookup"><span data-stu-id="7ba61-154">You can't use double quotes, because you've already used them to enclose the command:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

<span data-ttu-id="7ba61-155">MSBuild からこのコマンドを呼び出す際には、いくつかの追加の考慮事項があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-155">There are a few additional considerations when you invoke this command from MSBuild.</span></span> <span data-ttu-id="7ba61-156">最初に、スクリプトが自動的に実行されるように、 **–非対話**フラグを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-156">First, you should include the **–NonInteractive** flag to ensure that the script executes quietly.</span></span> <span data-ttu-id="7ba61-157">次に、適切な引数値を使用して **– set-executionpolicy**フラグを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-157">Next, you should include the **–ExecutionPolicy** flag with an appropriate argument value.</span></span> <span data-ttu-id="7ba61-158">これにより、Windows PowerShell がスクリプトに適用する実行ポリシーが指定され、既定の実行ポリシーをオーバーライドできるようになります。これにより、スクリプトの実行が妨げられる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-158">This specifies the execution policy that Windows PowerShell will apply to your script and allows you to override the default execution policy, which may prevent execution of your script.</span></span> <span data-ttu-id="7ba61-159">次の引数の値から選択できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-159">You can choose from these argument values:</span></span>

- <span data-ttu-id="7ba61-160">値を**無制限**に設定すると、スクリプトが署名されているかどうかに関係なく、Windows PowerShell でスクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-160">A value of **Unrestricted** will allow Windows PowerShell to execute your script, regardless of whether the script is signed.</span></span>
- <span data-ttu-id="7ba61-161">**RemoteSigned**の値を指定すると、Windows PowerShell はローカルコンピューター上で作成された未署名のスクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-161">A value of **RemoteSigned** will allow Windows PowerShell to execute unsigned scripts that were created on the local machine.</span></span> <span data-ttu-id="7ba61-162">ただし、他の場所で作成されたスクリプトには署名が必要です。</span><span class="sxs-lookup"><span data-stu-id="7ba61-162">However, scripts that were created elsewhere must be signed.</span></span> <span data-ttu-id="7ba61-163">(実際には、ビルドサーバーで Windows PowerShell スクリプトをローカルに作成することはほとんどありません)。</span><span class="sxs-lookup"><span data-stu-id="7ba61-163">(In practice, you're very unlikely to have created a Windows PowerShell script locally on a build server).</span></span>
- <span data-ttu-id="7ba61-164">**AllSigned**の値を指定すると、Windows PowerShell は署名されたスクリプトのみを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-164">A value of **AllSigned** will allow Windows PowerShell to execute signed scripts only.</span></span>

<span data-ttu-id="7ba61-165">既定の実行ポリシーは**制限**されています。これにより、Windows PowerShell はスクリプトファイルを実行できなくなります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-165">The default execution policy is **Restricted**, which prevents Windows PowerShell from running any script files.</span></span>

<span data-ttu-id="7ba61-166">最後に、Windows PowerShell コマンドで発生した予約済み XML 文字をエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-166">Finally, you need to escape any reserved XML characters that occur in your Windows PowerShell command:</span></span>

- <span data-ttu-id="7ba61-167">単一引用符を **&amp;apos;** に置き換える</span><span class="sxs-lookup"><span data-stu-id="7ba61-167">Replace single quotes with **&amp;apos;**</span></span>
- <span data-ttu-id="7ba61-168">二重引用符を **&amp;quot; に置き換えます。**</span><span class="sxs-lookup"><span data-stu-id="7ba61-168">Replace double quotes with **&amp;quot;**</span></span>
- <span data-ttu-id="7ba61-169">アンパサンドを **&amp;amp; に置き換えます。**</span><span class="sxs-lookup"><span data-stu-id="7ba61-169">Replace ampersands with **&amp;amp;**</span></span>

- <span data-ttu-id="7ba61-170">これらの変更を行うと、コマンドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-170">When you make these changes, your command will resemble this:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

<span data-ttu-id="7ba61-171">カスタム MSBuild プロジェクトファイル内で、新しいターゲットを作成し、 **Exec**タスクを使用して次のコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-171">Within your custom MSBuild project file, you can create a new target and use the **Exec** task to run this command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

<span data-ttu-id="7ba61-172">この例では、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="7ba61-172">In this example, note that:</span></span>

- <span data-ttu-id="7ba61-173">パラメーター値や Windows PowerShell 実行可能ファイルの場所など、すべての変数は MSBuild プロパティとして宣言されます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-173">Any variables, like parameter values and the location of the Windows PowerShell executable, are declared as MSBuild properties.</span></span>
- <span data-ttu-id="7ba61-174">ユーザーがコマンドラインからこれらの値をオーバーライドできるようにするための条件が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7ba61-174">Conditions are included to enable users to override these values from the command line.</span></span>
- <span data-ttu-id="7ba61-175">**Msdeploycomputername**プロパティは、プロジェクトファイル内の他の場所で宣言されています。</span><span class="sxs-lookup"><span data-stu-id="7ba61-175">The **MSDeployComputerName** property is declared elsewhere in the project file.</span></span>

<span data-ttu-id="7ba61-176">このターゲットをビルドプロセスの一部として実行すると、Windows PowerShell によってコマンドが実行され、指定したファイルにログエントリが書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-176">When you execute this target as part of your build process, Windows PowerShell will run your command and write a log entry to the file you specified.</span></span>

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a><span data-ttu-id="7ba61-177">リモートコンピューターでの Windows PowerShell スクリプトの実行</span><span class="sxs-lookup"><span data-stu-id="7ba61-177">Executing a Windows PowerShell Script on a Remote Computer</span></span>

<span data-ttu-id="7ba61-178">Windows PowerShell は、 [Windows リモート管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)(WinRM) を介してリモートコンピューターでスクリプトを実行することができます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-178">Windows PowerShell is capable of running scripts on remote computers through [Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span></span> <span data-ttu-id="7ba61-179">これを行うには、[コマンド](https://technet.microsoft.com/library/dd347578.aspx)レットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-179">To do this, you need to use the [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span></span> <span data-ttu-id="7ba61-180">これにより、スクリプトをリモートコンピューターにコピーせずに、1つまたは複数のリモートコンピューターに対してスクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-180">This lets you execute your script against one or more remote computers without copying the script to the remote computers.</span></span> <span data-ttu-id="7ba61-181">スクリプトを実行したローカルコンピューターに結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-181">Any results are returned to the local computer from which you ran the script.</span></span>

> [!NOTE]
> <span data-ttu-id="7ba61-182">**コマンド**レットを使用してリモートコンピューターで Windows PowerShell スクリプトを実行する前に、リモートメッセージを受け入れるように WinRM リスナーを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-182">Before you use the **Invoke-Command** cmdlet to execute Windows PowerShell scripts on a remote computer, you need to configure a WinRM listener to accept remote messages.</span></span> <span data-ttu-id="7ba61-183">これを行うには、リモートコンピューターでコマンド**winrm quickconfig**を実行します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-183">You can do this by running the command **winrm quickconfig** on the remote computer.</span></span> <span data-ttu-id="7ba61-184">詳細については、「 [Windows リモート管理のインストールと構成](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ba61-184">For more information, see [Installation and Configuration for Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).</span></span>

<span data-ttu-id="7ba61-185">Windows PowerShell ウィンドウから、次の構文を使用してリモートコンピューターで**Logdeploy. ps1**スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-185">From a Windows PowerShell window, you'd use this syntax to run the **LogDeploy.ps1** script on a remote computer:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> <span data-ttu-id="7ba61-186">**呼び出しコマンド**を使用してスクリプトファイルを実行するには、他にもさまざまな方法がありますが、この方法は、パラメーター値を指定し、パスをスペースで管理する必要がある場合に最も簡単です。</span><span class="sxs-lookup"><span data-stu-id="7ba61-186">There are various other ways of using **Invoke-Command** to run a script file, but this approach is the most straightforward when you need to provide parameter values and manage paths with spaces.</span></span>

<span data-ttu-id="7ba61-187">これをコマンドプロンプトから実行する場合は、Windows PowerShell 実行可能ファイルを起動し、 **– command**パラメーターを使用して指示を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-187">When you run this from a command prompt, you need to invoke the Windows PowerShell executable and use the **–command** parameter to provide your instructions:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

<span data-ttu-id="7ba61-188">前と同様に、MSBuild からコマンドを実行するときに、いくつかの追加のスイッチを指定し、予約済みの XML 文字をエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ba61-188">As before, you need to provide some additional switches and escape any reserved XML characters when you run the command from MSBuild:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

<span data-ttu-id="7ba61-189">最後に、前と同様に、カスタム MSBuild ターゲット内で**Exec**タスクを使用してコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-189">Finally, as before, you can use the **Exec** task within a custom MSBuild target to execute your command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

<span data-ttu-id="7ba61-190">このターゲットをビルドプロセスの一部として実行すると、Windows PowerShell は、 **– computername**引数で指定したコンピューター上でスクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-190">When you execute this target as part of your build process, Windows PowerShell will run your script on the computer you specified in the **–computername** argument.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7ba61-191">まとめ</span><span class="sxs-lookup"><span data-stu-id="7ba61-191">Conclusion</span></span>

<span data-ttu-id="7ba61-192">このトピックでは、MSBuild プロジェクトファイルから Windows PowerShell スクリプトを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7ba61-192">This topic described how to run a Windows PowerShell script from an MSBuild project file.</span></span> <span data-ttu-id="7ba61-193">この方法を使用すると、自動または単一ステップのビルドおよび展開プロセスの一部として、ローカルまたはリモートコンピューターで Windows PowerShell スクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7ba61-193">You can use this approach to run a Windows PowerShell script, either locally or on a remote computer, as part of an automated or single-step build and deployment process.</span></span>

## <a name="further-reading"></a><span data-ttu-id="7ba61-194">参考資料</span><span class="sxs-lookup"><span data-stu-id="7ba61-194">Further Reading</span></span>

<span data-ttu-id="7ba61-195">Windows PowerShell スクリプトへの署名と実行ポリシーの管理に関するガイダンスについては、「 [Windows Powershell スクリプトの実行](https://technet.microsoft.com/library/ee176949.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ba61-195">For guidance on signing Windows PowerShell scripts and managing execution policies, see [Running Windows PowerShell Scripts](https://technet.microsoft.com/library/ee176949.aspx).</span></span> <span data-ttu-id="7ba61-196">リモートコンピューターからの Windows PowerShell コマンドの実行に関するガイダンスについては、「[リモートコマンドの実行](https://technet.microsoft.com/library/dd819505.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ba61-196">For guidance on running Windows PowerShell commands from a remote computer, see [Running Remote Commands](https://technet.microsoft.com/library/dd819505.aspx).</span></span>

<span data-ttu-id="7ba61-197">カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ba61-197">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7ba61-198">[前へ](taking-web-applications-offline-with-web-deploy.md)
> [次へ](troubleshooting-the-packaging-process.md)</span><span class="sxs-lookup"><span data-stu-id="7ba61-198">[Previous](taking-web-applications-offline-with-web-deploy.md)
[Next](troubleshooting-the-packaging-process.md)</span></span>
